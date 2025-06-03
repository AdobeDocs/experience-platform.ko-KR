---
title: Edge 세그멘테이션 안내서
description: 에지 세분화를 사용하여 에지에서 즉시 Experience Platform의 대상을 평가하여 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화하는 방법에 대해 알아봅니다.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: a741fdb4393863dbc011c03c733e27572da0ae6c
workflow-type: tm+mt
source-wordcount: '1116'
ht-degree: 1%

---

# 에지 세분화 안내서

Edge 세그멘테이션은 Adobe Experience Platform의 세그먼트 정의를 즉시 [edge](../../landing/edge-and-hub-comparison.md)에서 평가하는 기능으로, 동일한 페이지와 다음 페이지 개인화 사용 사례를 활성화합니다.

>[!IMPORTANT]
>
> 에지 데이터는 수집된 위치와 가장 가까운 에지 서버 위치에 저장됩니다. 이 데이터는 허브(또는 주체) Adobe Experience Platform 데이터 센터로 지정된 위치 이외의 위치에도 저장될 수 있다.
>
> 또한 에지 세분화 엔진은 에지 기반이 아닌 기본 ID와 일치하는 **one** 기본 표시 ID가 있는 에지의 요청만 처리합니다.

## Edge 세그멘테이션 쿼리 유형 {#query-types}

쿼리가 다음 표에 요약된 기준을 충족하는 경우 가장자리 세분화를 사용하여 평가할 수 있습니다.

>[!NOTE]
>
>쿼리가 다음 표의 쿼리 유형과 일치하는 경우, 가장자리 세분화를 사용하여 자동으로 평가됩니다. 시스템은 쿼리 표현식을 기반으로 이 기능을 자동으로 결정합니다.

| 쿼리 유형 | 세부 사항 | 쿼리 | 예 |
| ---------- | ------- | ----- | ------- |
| 24시간 미만의 기간 내 단일 이벤트 | 24시간 미만의 기간 내에 들어오는 단일 이벤트를 참조하는 모든 세그먼트 정의. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![상대 시간 범위 내의 단일 이벤트의 예가 표시됩니다.](../images/methods/edge/single-event.png) |
| 프로필만 | 프로필 속성만 참조하는 모든 세그먼트 정의. | `homeAddress.country.equals("US", false)` | ![프로필 특성의 예제가 표시됩니다.](../images/methods/edge/profile-attribute.png) |
| 24시간 미만의 상대 시간 창 내에 프로필 속성이 있는 단일 이벤트 | 하나 이상의 프로필 속성을 가진 단일 수신 이벤트를 참조하고 24시간 미만의 상대 시간 창 내에서 발생하는 모든 세그먼트 정의입니다. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![상대 기간 내에 프로필 특성이 있는 단일 이벤트의 예가 표시됩니다.](../images/methods/edge/single-event-with-profile-attribute.png) |
| 세그먼트 | 하나 이상의 배치 또는 모서리 세그먼트를 포함하는 모든 세그먼트 정의입니다. **참고:** 세그먼트의 세그먼트가 사용되는 경우 **24시간마다**&#x200B;프로필의 자격이 상실됩니다. | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![세그먼트 예제가 표시됩니다.](../images/methods/edge/segment-of-segments.png) |

또한 세그먼트 정의 **must**&#x200B;은(는) Edge에서 활성 상태인 병합 정책에 연결됩니다. 병합 정책에 대한 자세한 내용은 [병합 정책 안내서](../../profile/api/merge-policies.md)를 참조하십시오.

다음 시나리오에서 세그먼트 정의는 **not**&#x200B;이(가) 에지 세분화에 적합하지 않습니다.

- 세그먼트 정의에는 단일 이벤트와 `inSegment` 이벤트의 조합이 포함됩니다.
   - 그러나 `inSegment` 이벤트에 포함된 세그먼트 정의가 프로필인 경우 세그먼트 정의 **will**&#x200B;이(가) 에지 세분화에 대해 활성화됩니다.
- 세그먼트 정의는 시간 제한의 일부로서 &quot;연도 무시&quot;를 사용합니다.

## 대상자 만들기 {#create-audience}

세분화 서비스 API를 사용하거나 UI의 대상 포털을 통해 에지 세분화를 사용하여 평가되는 대상을 만들 수 있습니다.

세그먼트 정의가 [적격 쿼리 유형](#eligible-query-types) 중 하나와 일치하는 경우 Edge를 사용할 수 있습니다.

>[!BEGINTABS]

>[!TAB 세그먼테이션 서비스 API]

**API 형식**

```http
POST /segment/definitions
```

**요청**

+++ 에지 세분화에 대해 활성화된 세그먼트 정의를 만들기 위한 샘플 요청

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
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
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**응답**

성공적인 응답은 새로 생성된 세그먼트 정의에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++세그먼트 정의를 생성할 때 샘플 응답.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
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
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

이 끝점 사용에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서](../api/segment-definitions.md)에서 확인할 수 있습니다.

>[!TAB 대상자 포털]

대상 포털에서 **[!UICONTROL 대상 만들기]**&#x200B;를 선택합니다.

![대상자 만들기 단추가 대상자 포털에서 강조 표시됩니다.](../images/methods/edge/select-create-audience.png)

팝오버가 나타납니다. 세그먼트 빌더를 입력하려면 **[!UICONTROL 규칙 작성]**&#x200B;을 선택하십시오.

![대상 만들기 팝오버에서 빌드 규칙 단추가 강조 표시됩니다.](../images/methods/edge/select-build-rules.png)

세그먼트 빌더 내에서 [적격 쿼리 유형](#eligible-query-types) 중 하나와 일치하는 세그먼트 정의를 만듭니다. 세그먼트 정의가 Edge 세그멘테이션에 적합하면 **[!UICONTROL Edge]**&#x200B;을(를) **[!UICONTROL 평가 메서드]**(으)로 선택할 수 있습니다.

![세그먼트 정의가 표시됩니다. 평가 유형이 강조 표시되어 가장자리 세분화를 사용하여 세그먼트 정의를 평가할 수 있음을 보여 줍니다.](../images/methods/edge/edge-evaluation-method.png)

세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 빌더 안내서](../ui/segment-builder.md)를 참조하세요.

>[!ENDTABS]

## 에지 세분화를 사용하여 평가된 대상 검색 {#retrieve-audiences}

세분화 서비스 API를 사용하거나 UI의 대상 포털을 통해 에지 세분화를 사용하여 평가되는 모든 대상을 검색할 수 있습니다.

>[!BEGINTABS]

>[!TAB 세그먼테이션 서비스 API]

`/segment/definitions` 끝점에 대한 GET 요청을 통해 조직 내에서 Edge 세그먼테이션을 사용하여 평가되는 모든 세그먼트 정의 목록을 검색합니다.

**API 형식**

가장자리 세분화를 사용하여 평가된 세그먼트 정의를 검색하려면 요청 경로에 쿼리 매개 변수 `evaluationInfo.synchronous.enabled=true`을(를) 포함해야 합니다.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**요청**

+++ 모든 에지 활성화 세그먼트 정의를 나열하는 샘플 요청

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 에지 세분화에 대해 활성화된 조직의 세그먼트 정의 배열과 함께 HTTP 상태 200을 반환합니다.

+++ 조직의 모든 에지 세분화 사용 세그먼트 정의 목록을 포함하는 샘플 응답

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
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

반환된 세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서](../api/segment-definitions.md)를 참조하십시오.

+++

>[!TAB 대상자 포털]

Audience Portal의 필터를 사용하여 조직 내에서 에지 세분화에 대해 활성화된 모든 대상을 검색할 수 있습니다. 필터 목록을 표시하려면 ![필터 아이콘](../../images/icons/filter.png) 아이콘을 선택하십시오.

![Audience Portal에서 필터 아이콘이 강조 표시되어 있습니다.](../images/methods/filter-audiences.png)

사용 가능한 필터 내에서 **빈도 업데이트**(으)로 이동하여 &quot;Edge&quot;을(를) 선택합니다. 이 필터를 사용하면 에지 세분화를 사용하여 평가되는 조직의 모든 대상이 표시됩니다.

![에지 세분화를 사용하여 평가되는 조직의 모든 대상을 표시하는 Edge 업데이트 빈도를 선택했습니다.](../images/methods/edge/filter-edge.png)

Experience Platform에서 대상자를 보는 방법에 대한 자세한 내용은 [대상자 포털 안내서](../ui/audience-portal.md)를 참조하십시오.

>[!ENDTABS]

## 대상자 세부 정보 {#audience-details}

Audience Portal 내에서 에지 세분화를 사용하여 평가된 특정 대상의 세부 사항을 선택하여 볼 수 있습니다.

Audience Portal에서 대상을 선택하면 대상 세부 사항 페이지가 표시됩니다. 대상자 세부 사항, 시간 경과에 따른 적격 프로필의 양뿐만 아니라 대상자가 활성화된 대상자에 대한 요약을 포함하여 대상자에 대한 정보가 표시됩니다.

![에지 세분화를 사용하여 평가된 대상에 대해 대상 세부 정보 페이지가 표시됩니다.](../images/methods/edge/audience-details.png)

Edge 사용 대상의 경우 **[!UICONTROL 시간 경과에 따른 프로필]** 카드가 표시되며, 여기에는 정규화된 총 지표와 새로 업데이트된 지표가 표시됩니다.

**[!UICONTROL 총 정규화]** 지표는 이 대상에 대한 에지 평가를 기반으로 전체 정규화 대상 수를 나타냅니다.

**[!UICONTROL 새로 업데이트된 대상]** 지표는 가장자리 세분화를 통해 대상 크기의 변화를 보여 주는 선 그래프로 표시됩니다. 드롭다운을 조정하여 지난 24시간, 지난 주 또는 지난 30일을 표시할 수 있습니다.

![시간 경과에 따른 프로필 카드가 강조 표시됩니다.](../images/methods/edge/profiles-over-time.png)

대상자 세부 정보에 대한 자세한 내용은 [대상자 포털 개요](../ui/audience-portal.md#audience-details)를 참조하십시오.

## 다음 단계

이 안내서에서는 에지 세그멘테이션의 의미와 Adobe Experience Platform에서 에지 세그멘테이션을 사용하여 평가할 수 있는 세그먼트 정의를 만드는 방법을 설명합니다.

Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그먼테이션 사용 안내서](./overview.md)를 참조하세요.

에지 세분화에 대한 FAQ는 FAQ[&#128279;](../faq.md#edge-segmentation)의 에지 세분화 섹션을 참조하십시오.

