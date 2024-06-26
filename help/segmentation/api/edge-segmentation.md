---
solution: Experience Platform
title: API를 사용한 Edge 세그멘테이션
description: 이 문서에는 Adobe Experience Platform 세그멘테이션 서비스 API와 함께 에지 세그멘테이션을 사용하는 방법에 대한 예제가 포함되어 있습니다.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# 에지 세분화

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 에지 세분화를 수행하는 방법을 설명합니다. UI를 사용하여 에지 세분화를 수행하는 방법에 대한 자세한 내용은 [edge 세그멘테이션 UI 안내서](../ui/edge-segmentation.md).
>
>이제 모든 Platform 사용자가 Edge 세그멘테이션을 일반적으로 사용할 수 있습니다. Beta 실행 중에 에지 세그먼트 정의를 생성한 경우 이러한 세그먼트 정의는 계속 작동합니다.

에지 세그멘테이션은 에지에서 즉시 Adobe Experience Platform의 세그먼트 정의를 평가하는 기능으로, 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

>[!IMPORTANT]
>
> 에지 데이터는 수집된 위치에서 가장 가까운 에지 서버 위치에 저장되고 허브(또는 주) Adobe Experience Platform 데이터 센터로 지정된 위치 이외의 위치에 저장될 수 있다.
>
> 또한 에지 세분화 엔진은 가 있는 에지의 요청만 처리합니다 **1** 에지 기반이 아닌 기본 id와 일치하는 기본 표시 id.

## 시작하기

이 개발자 안내서를 사용하려면 여러 가지 사항에 대한 작업 이해가 필요합니다 [!DNL Adobe Experience Platform] 에지 세분화와 관련된 서비스. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 소비자 프로필을 실시간으로 제공합니다.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): 다음에서 대상자를 빌드할 수 있습니다. [!DNL Real-Time Customer Profile] 데이터.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

Experience Platform API 엔드포인트를 성공적으로 호출하려면 의 안내서를 참조하십시오. [platform API 시작하기](../../landing/api-guide.md) 필수 헤더와 샘플 API 호출을 읽는 방법에 대해 알아봅니다.

## Edge 세그멘테이션 쿼리 유형 {#query-types}

가장자리 세분화를 사용하여 세그먼트를 평가하려면 쿼리가 다음 지침을 준수해야 합니다.

| 쿼리 유형 | 세부 사항 | 예 | PQL 예 |
| ---------- | ------- | ------- | ----------- |
| 단일 이벤트 | 시간 제한 없이 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의. | 장바구니에 항목을 추가한 사람. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 단일 프로필 | 단일 프로필 전용 속성을 참조하는 모든 세그먼트 정의 | 미국에 사는 사람들. | `homeAddress.countryCode = "US"` |
| 프로필을 참조하는 단일 이벤트 | 하나 이상의 프로필 속성 및 시간 제한 없이 수신되는 단일 이벤트를 참조하는 모든 세그먼트 정의. | 홈페이지를 방문한 미국 거주자. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 프로필 속성을 사용하여 단일 이벤트 무효화 | 무효화된 단일 수신 이벤트와 하나 이상의 프로필 속성을 참조하는 세그먼트 정의 | 미국에 거주하고 다음을 보유한 사람 **아님** 홈페이지를 방문했습니다. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 기간 내 단일 이벤트 | 설정된 기간 내의 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. | 지난 24시간 동안 홈페이지를 방문한 사람. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| 24시간 미만의 상대 시간 창 내에 프로필 속성이 있는 단일 이벤트 | 하나 이상의 프로필 속성을 가진 단일 수신 이벤트를 참조하고 24시간 미만의 상대 시간 창 내에서 발생하는 모든 세그먼트 정의입니다. | 지난 24시간 동안 홈페이지를 방문한 미국 거주자. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)])` |
| 기간 내에 프로필 속성이 있는 단일 이벤트가 무효화됨 | 일정 기간 내에 하나 이상의 프로필 속성 및 차단된 단일 수신 이벤트를 참조하는 모든 세그먼트 정의. | 미국에 거주하고 다음을 보유한 사람 **아님** 지난 24시간 동안 홈페이지를 방문했습니다. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 24 hours before now)]))` |
| 24시간 기간 내 빈도 이벤트 | 24시간의 기간 내에서 특정 횟수로 발생하는 이벤트를 참조하는 세그먼트 정의입니다. | 홈 페이지를 방문한 사람 **최소** 지난 24시간 동안 5번 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 24시간 기간 내에 프로필 속성이 있는 빈도 이벤트 | 하나 이상의 프로필 속성을 참조하는 세그먼트 정의와 24시간의 기간 내에서 특정 횟수만큼 발생하는 이벤트. | 홈페이지를 방문한 미국 출신 **최소** 지난 24시간 동안 5번 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 24시간 기간 내에 프로필로 빈도 이벤트를 무효화했습니다. | 하나 이상의 프로필 속성을 참조하는 세그먼트 정의와 24시간의 기간 내에서 특정 횟수만큼 발생하는 차단된 이벤트입니다. | 홈 페이지를 방문하지 않은 사람 **기타** 지난 24시간 동안 5번 이상 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 24시간의 시간 프로필 내에 여러 개의 수신 히트 | 24시간의 기간 내에 발생하는 여러 이벤트를 참조하는 모든 세그먼트 정의. | 홈 페이지를 방문한 사람 **또는** 지난 24시간 내에 체크아웃 페이지를 방문했습니다. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 24시간 기간 내에 프로필이 있는 여러 이벤트 | 24시간의 기간 내에 발생하는 하나 이상의 프로필 속성 및 여러 이벤트를 참조하는 모든 세그먼트 정의. | 홈페이지를 방문한 미국 출신 **및** 지난 24시간 내에 체크아웃 페이지를 방문했습니다. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 세그먼트 | 하나 이상의 일괄 처리 또는 스트리밍 세그먼트를 포함하는 모든 세그먼트 정의입니다. | 미국에 거주하며 &quot;기존 세그먼트&quot; 세그먼트에 있는 사람. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 맵을 참조하는 쿼리 | 속성 맵을 참조하는 모든 세그먼트 정의입니다. | 외부 세그먼트 데이터를 기반으로 장바구니에 추가한 사람입니다. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

또한 세그먼트는 **필수** edge에서 활성 상태인 병합 정책에 연결됩니다. 병합 정책에 대한 자세한 내용은 [병합 정책 안내서](../../profile/api/merge-policies.md).

세그먼트 정의는 **아님** 다음 시나리오에서 edge 세그멘테이션에 대해 활성화하십시오.

- 세그먼트 정의는 단일 이벤트와 `inSegment` 이벤트.
   - 그러나 세그먼트에 포함된 경우 `inSegment` 이벤트는 프로필 전용이며, 세그먼트 정의는 입니다. **의지** 에지 세분화에 대해 활성화되어야 합니다.
- 세그먼트 정의는 시간 제한의 일부로서 &quot;연도 무시&quot;를 사용합니다.

## 에지 세그멘테이션에 대해 활성화된 모든 세그먼트 검색

에 GET 요청을 하여 조직 내에서 Edge 세그멘테이션에 대해 활성화된 모든 세그먼트 목록을 검색할 수 있습니다. `/segment/definitions` 엔드포인트.

**API 형식**

모서리 세그멘테이션에 대해 활성화된 세그먼트를 검색하려면 쿼리 매개 변수를 포함해야 합니다 `evaluationInfo.synchronous.enabled=true` 요청 경로에서.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 조직에서 에지 세분화에 대해 활성화된 일련의 세그먼트를 반환합니다. 반환된 세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## 가장자리 세분화가 활성화된 세그먼트 만들기

에 POST 요청을 하여 에지 세분화에 대해 활성화된 세그먼트를 만들 수 있습니다. `/segment/definitions` 다음 중 하나와 일치하는 엔드포인트 [위에 나열된 에지 세분화 쿼리 유형](#query-types).

**API 형식**

```http
POST /segment/definitions
```

**요청**

>[!NOTE]
>
>아래 예제는 세그먼트를 만들기 위한 표준 요청입니다. 세그먼트 정의 만들기에 대한 자세한 내용은 다음 자습서를 참조하십시오. [세그먼트 만들기](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    }
}'
```

**응답**

성공한 응답은 에지 세분화에 대해 활성화된 새로 생성된 세그먼트 정의의 세부 정보를 반환합니다.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## 다음 단계

이제 에지 세그멘테이션이 활성화된 세그먼트를 만드는 방법을 알았으므로 이를 사용하여 동일 페이지 및 다음 페이지 개인화 사용 사례를 활성화할 수 있습니다.

Adobe Experience Platform 사용자 인터페이스를 사용하여 유사한 작업을 수행하고 세그먼트를 사용하는 방법을 알아보려면 다음을 방문하십시오. [세그먼트 빌더 사용 안내서](../ui/segment-builder.md).

## 부록

다음 섹션에는 에지 세분화에 대해 자주 묻는 질문이 나와 있습니다.

### Edge Network에서 세그먼트를 사용할 수 있는 데 시간이 얼마나 걸립니까?

Edge Network에서 세그먼트를 사용할 수 있는 데 최대 1시간이 소요됩니다.