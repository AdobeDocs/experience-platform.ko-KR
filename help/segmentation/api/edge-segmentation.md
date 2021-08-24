---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;에지 세그멘테이션;에지 세그멘테이션;스트리밍 에지
solution: Experience Platform
title: 'API를 사용한 Edge Segmentation '
topic-legacy: developer guide
description: 이 문서에는 Adobe Experience Platform 세그멘테이션 서비스 API와 함께 에지 세그멘테이션을 사용하는 방법에 대한 예가 나와 있습니다.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: af1eee8787d7fa2ae2d56e541823100d2620dd2d
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 3%

---

# 에지 세그먼테이션(베타)

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 에지 세그멘테이션을 수행하는 방법을 설명합니다. UI를 사용하여 Edge Segmentation을 수행하는 방법에 대한 내용은 [Edge Segmentation UI 안내서](../ui/edge-segmentation.md)를 참조하십시오. 또한 에지 세그먼테이션은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

Edge Segmentation은 Adobe Experience Platform의 세그먼트를 즉시 평가하여 동일한 페이지와 다음 페이지 개인화 사용 사례를 가능하게 하는 기능입니다.

## 시작하기

이 개발자 안내서를 사용하려면 Edge Segmentation과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대한 작업 이해를 필요로 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 실시간으로 통합 소비자 프로필을 제공합니다.
- [[!DNL Segmentation]](../home.md): 데이터에서 세그먼트와 대상을 만드는 기능을  [!DNL Real-time Customer Profile] 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다.

[!DNL Data Prep] API 엔드포인트를 성공적으로 호출하려면 [플랫폼 API 시작](../../landing/api-guide.md)의 안내서를 참조하여 필요한 헤더와 샘플 API 호출을 읽는 방법에 대해 알아보십시오.

## 에지 세그멘테이션 쿼리 유형 {#query-types}

에지 세그먼테이션을 사용하여 세그먼트를 평가하려면 쿼리가 다음 지침을 준수해야 합니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 수신 히트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의입니다. |
| 프로필을 참조하는 수신 히트 | 시간 제한 없이 단일 수신 이벤트를 참조하는 모든 세그먼트 정의와 하나 이상의 프로필 속성을 참조합니다. |
| 24시간의 시간 창이 있는 수신 히트 | 24시간 이내에 단일 수신 이벤트를 참조하는 모든 세그먼트 정의 |
| 24시간의 시간 창이 있는 프로필을 참조하는 수신 히트 | 24시간 이내에 단일 수신 이벤트와 하나 이상의 프로필 속성을 참조하는 모든 세그먼트 정의 |

{style=&quot;table-layout:auto&quot;}

다음 쿼리 유형은 현재 에지 세그먼테이션에서 지원되지 않는 **입니다.**

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 여러 이벤트 | 쿼리에 두 개 이상의 이벤트가 포함된 경우 에지 세그멘테이션을 사용하여 평가할 수 없습니다. |
| 빈도 쿼리 | 특정 횟수 이상 발생하는 이벤트를 참조하는 모든 세그먼트 정의입니다. |
| 프로필을 참조하는 빈도 쿼리 | 특정 횟수 이상 발생하는 이벤트를 참조하며 하나 이상의 프로필 속성을 갖는 모든 세그먼트 정의입니다. |

{style=&quot;table-layout:auto&quot;}

## 에지 세그먼테이션에 대해 활성화된 모든 세그먼트 검색

`/segment/definitions` 종단점에 GET 요청을 수행하여 IMS 조직 내에서 에지 세그먼테이션에 활성화된 모든 세그먼트 목록을 검색할 수 있습니다.

**API 형식**

에지 세그먼테이션에 대해 활성화된 세그먼트를 검색하려면 요청 경로에 쿼리 매개 변수 `evaluationInfo.synchronous.enabled=true`을 포함해야 합니다.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 Edge Segmentation에 대해 활성화된 IMS 조직의 세그먼트 배열이 반환됩니다. 반환된 세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 종단점 안내서](./segment-definitions.md)에서 확인할 수 있습니다.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
            "imsOrgId": "{IMS_ORG_ID}",
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

## 에지 세그먼테이션을 위해 활성화된 세그먼트 만들기

위에 나열된 [edge segmentation 쿼리 유형 중 하나와 일치하는 `/segment/definitions` 종단점에 POST 요청을 하여 에지 세그먼테이션에 활성화된 세그먼트를 만들 수 있습니다.](#query-types)

**API 형식**

```http
POST /segment/definitions
```

**요청**

>[!NOTE]
>
>아래 예제는 세그먼트를 만들기 위한 표준 요청입니다. 세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 만들기](../tutorials/create-a-segment.md)에서 자습서를 참조하십시오.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    }
}'
```

**응답**

성공적으로 응답하면 에지 세그멘테이션에 대해 활성화된 새로 생성된 세그먼트 정의의 세부 사항이 반환됩니다.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
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
```

## 다음 단계

에지 세그먼테이션이 활성화된 세그먼트를 만드는 방법을 알고 있으므로 이 세그먼트를 사용하여 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화할 수 있습니다.

유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [세그먼트 빌더 사용 안내서](../ui/segment-builder.md)를 방문하십시오.
