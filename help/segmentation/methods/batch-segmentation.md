---
title: Batch Segmentation 안내서
description: 정의, 배치 세그먼테이션을 사용하여 평가된 대상을 만드는 방법, 배치 세그먼테이션을 사용하여 만든 대상을 보는 방법 등을 포함하여 배치 세그먼테이션에 대해 알아봅니다.
exl-id: b6fba2fb-8eec-4429-92fd-ece5c79d379d
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---

# 일괄 처리 세그멘테이션 안내서

일괄 세분화는 프로필 데이터를 한 번에 이동하여 해당 대상자를 만들 수 있는 세분화 평가 방법입니다.

배치 세분화를 사용하면 상세하고 풍부한 대상을 만들고 세분화 작업을 실행하여 이 데이터를 다운스트림 서비스에 전파하려는 시기를 확인할 수 있습니다.

## 적격 쿼리 유형 {#query-types}

모든 쿼리는 배치 세분화에 적합합니다.

## 대상자 만들기 {#create-audience}

세분화 서비스 API를 사용하거나 UI의 대상 포털을 통해 배치 세분화를 사용하여 평가되는 대상을 만들 수 있습니다.

>[!BEGINTABS]

>[!TAB 세그먼테이션 서비스 API]

**API 형식**

```http
POST /segment/definitions
```

**요청**

+++ 배치 세분화가 활성화된 세그먼트 정의를 만들기 위한 샘플 요청

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
                "enabled": true
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": false
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
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
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

![대상자 만들기 단추가 대상자 포털에서 강조 표시됩니다.](../images/methods/batch/select-create-audience.png)

팝오버가 나타납니다. 세그먼트 빌더를 입력하려면 **[!UICONTROL 규칙 작성]**&#x200B;을 선택하십시오.

![대상 만들기 팝오버에서 빌드 규칙 단추가 강조 표시됩니다.](../images/methods/batch/select-build-rules.png)

세그먼트 정의를 만든 후 **[!UICONTROL 일괄 처리]**&#x200B;를 **[!UICONTROL 평가 메서드]**(으)로 선택합니다.

![세그먼트 정의가 표시됩니다. 평가 유형이 강조 표시되어 스트리밍 세분화를 사용하여 세그먼트 정의를 평가할 수 있음을 보여 줍니다.](../images/methods/batch/batch-evaluation-method.png)

세그먼트 정의 만들기에 대한 자세한 내용은 [세그먼트 빌더 안내서](../ui/segment-builder.md)를 참조하세요.

>[!ENDTABS]

## 대상자 검색 {#retrieve-audiences}

세분화 서비스 API를 사용하거나 UI의 대상 포털을 통해 배치 세분화를 사용하여 평가된 모든 대상을 검색할 수 있습니다.

>[!BEGINTABS]

>[!TAB 세그먼테이션 서비스 API]

`/segment/definitions` 끝점에 대한 GET 요청을 통해 조직 내에서 일괄 처리 세그먼테이션을 사용하여 평가되는 모든 세그먼트 정의 목록을 검색합니다.

**API 형식**

일괄 처리 세분화를 사용하여 평가된 세그먼트 정의를 검색하려면 요청 경로에 쿼리 매개 변수 `evaluationInfo.batch.enabled=true`을(를) 포함해야 합니다.

```http
GET /segment/definitions?evaluationInfo.batch.enabled=true
```

**요청**

+++ 일괄 처리가 활성화된 모든 세그먼트 정의를 나열하는 샘플 요청

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.batch.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**응답**

성공적인 응답은 배치 세그먼테이션을 사용하여 평가되는 조직의 세그먼트 정의 배열과 함께 HTTP 상태 200을 반환합니다.

+++조직의 모든 일괄 처리 세분화 평가 세그먼트 정의 목록을 포함하는 샘플 응답

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
                    "enabled": true
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": false
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
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
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

Audience Portal의 필터를 사용하여 조직 내에서 일괄 세분화에 대해 활성화된 모든 대상을 검색할 수 있습니다. 필터 목록을 표시하려면 ![필터 아이콘](../../images/icons/filter.png) 아이콘을 선택하십시오.

![Audience Portal에서 필터 아이콘이 강조 표시되어 있습니다.](../images/methods/filter-audiences.png)

사용 가능한 필터 내에서 **[!UICONTROL 빈도 업데이트]**(으)로 이동하여 &quot;[!UICONTROL 일괄 처리]&quot;을(를) 선택하십시오. 이 필터를 사용하면 배치 세분화를 사용하여 평가되는 조직의 모든 대상이 표시됩니다.

![일괄 처리 업데이트 빈도를 선택하여 일괄 처리 세분화를 사용하여 평가되는 조직의 모든 대상을 표시합니다.](../images/methods/batch/filter-batch.png)

Experience Platform에서 대상자를 보는 방법에 대한 자세한 내용은 [대상자 포털 안내서](../ui/audience-portal.md)를 참조하십시오.

>[!ENDTABS]

## 다음 단계

이 안내서에서는 Adobe Experience Platform에서 배치 세그먼테이션을 사용하여 평가할 수 있는 세그먼트 정의를 만드는 방법을 설명합니다.

Experience Platform 사용자 인터페이스 사용에 대한 자세한 내용은 [세그먼테이션 사용 안내서](../ui/overview.md)를 참조하세요.

일괄 처리 세분화에 대한 FAQ는 FAQ](../faq.md#batch-segmentation)의 [일괄 처리 세분화 섹션을 참조하십시오.
