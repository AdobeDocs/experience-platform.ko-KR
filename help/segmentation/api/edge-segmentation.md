---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;가장자리 세그멘테이션;Edge segmentation;streaming edge
solution: Experience Platform
title: 'API를 사용한 에지 세그멘테이션 '
topic-legacy: developer guide
description: 이 문서에는 Adobe Experience Platform 세그멘테이션 서비스 API에서 가장자리 세그멘테이션을 사용하는 방법에 대한 예가 포함되어 있습니다.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# 에지 세분화(베타)

>[!NOTE]
>
>다음 문서에서는 API를 사용하여 가장자리 세그멘테이션을 수행하는 방법을 설명합니다. UI를 사용하여 에지 세그멘테이션을 수행하는 방법에 대한 자세한 내용은 [가장자리 세그멘테이션 UI 안내서](../ui/edge-segmentation.md)를 참조하십시오. 또한 에지 세그먼테이션은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

Edge Segmentation은 Adobe Experience Platform에서 세그먼트를 바로 에지 시 평가하는 기능으로, 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화합니다.

## 시작하기

이 개발자 가이드는 가장자리 세그멘테이션과 관련된 다양한 [!DNL Adobe Experience Platform] 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md):여러 소스의 데이터를 집계하여 실시간으로 통합 소비자 프로파일을 제공합니다.
- [[!DNL Segmentation]](../home.md):데이터에서 세그먼트와 대상을 만드는 기능을  [!DNL Real-time Customer Profile] 제공합니다.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크

[!DNL Data Prep] API 끝점을 성공적으로 호출하려면 [플랫폼 API 시작](../../landing/api-guide.md)의 안내서를 참조하여 필요한 헤더와 샘플 API 호출을 읽는 방법에 대해 알아보십시오.

## 에지 세그멘테이션 쿼리 유형 {#query-types}

에지 세그먼테이션을 사용하여 세그먼트를 평가하려면 쿼리는 다음 지침을 따라야 합니다.

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하는 모든 세그먼트 정의 |
| 프로필을 참조하는 들어오는 히트 | 시간 제한 없이 단일 들어오는 이벤트를 참조하고 하나 이상의 프로필 속성을 참조하는 세그먼트 정의입니다. |
| 주파수 쿼리 | 이벤트를 참조하는 세그먼트 정의 중 적어도 일정 횟수만큼 발생하는 모든 세그먼트 정의입니다. |
| 프로필을 참조하는 빈도 쿼리 | 이벤트를 참조하는 세그먼트 정의에는 적어도 일정 횟수만큼 발생하며 하나 이상의 프로필 속성이 있습니다. |

{style=&quot;table-layout:auto&quot;}

다음 쿼리 유형은 현재 Edge 세그멘테이션에서 지원되지 않는 **입니다.**

| 쿼리 유형 | 세부 사항 |
| ---------- | ------- |
| 상대 시간 창 | 쿼리가 시간 창을 참조하면 가장자리 세그멘테이션을 사용하여 평가할 수 없습니다. |
| 부정 | 쿼리에 부정 또는 `not` 이벤트가 포함된 경우 가장자리 세그멘테이션을 사용하여 평가할 수 없습니다. |
| 여러 이벤트 | 쿼리에 이벤트가 두 개 이상 있으면 에지 세그멘테이션을 사용하여 평가할 수 없습니다. |

{style=&quot;table-layout:auto&quot;}

## 에지 세그먼테이션에 대해 활성화된 모든 세그먼트 검색

`/segment/definitions` 종단점에 GET 요청을 함으로써 IMS 내에서 에지 세그먼테이션에 대해 활성화된 모든 세그먼트 목록을 검색할 수 있습니다.

**API 형식**

에지 세그먼테이션에 대해 활성화된 세그먼트를 검색하려면 요청 경로에 쿼리 매개 변수 `evaluationInfo.synchronous.enabled=true`을(를) 포함해야 합니다.

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

성공적인 응답은 에지 세그먼테이션에 대해 활성화된 IMS 조직의 세그먼트 배열을 반환합니다. 반환된 세그먼트 정의에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서](./segment-definitions.md)에서 확인할 수 있습니다.

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

## 가장자리 세그멘테이션에 사용할 수 있는 세그먼트 만들기

`/segment/definitions` 종단점에 POST 요청을 하여 에지 세그먼테이션에 사용할 수 있는 세그먼트를 만들 수 있습니다. ](#query-types) 위에 나열된 [에지 세그멘테이션 쿼리 유형 중 하나를 일치시킬 것 외에도 페이로드의 `evaluationInfo.synchronous.enabled` 플래그를 true로 설정해야 합니다.

**API 형식**

```http
POST /segment/definitions
```

**요청**

>[!NOTE]
>
>아래 예는 세그먼트를 만들기 위한 표준 요청입니다. 세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 만들기](../tutorials/create-a-segment.md)의 자습서를 참조하십시오.

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
    },
    "evaluationInfo": {
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | `evaluationInfo` 개체는 세그먼트 정의가 수행할 평가 유형을 결정합니다. 가장자리 세그멘테이션을 사용하려면 `evaluationInfo.synchronous.enabled` 값을 `true`으로 설정합니다. |

**응답**

성공적으로 응답하면 에지 세그먼테이션에 대해 활성화된 새로 만든 세그먼트 정의의 세부 정보가 반환됩니다.

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

이제 Edge Segmentation이 활성화된 세그먼트를 만드는 방법을 알고 있으므로 이 세그먼트를 사용하여 동일한 페이지 및 다음 페이지 개인화 사용 사례를 활성화할 수 있습니다.

유사한 작업을 수행하고 Adobe Experience Platform 사용자 인터페이스를 사용하여 세그먼트를 작업하는 방법에 대해 알아보려면 [세그먼트 빌더 사용자 안내서](../ui/segment-builder.md)를 방문하십시오.
