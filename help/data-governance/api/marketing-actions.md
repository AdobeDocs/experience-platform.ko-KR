---
keywords: Experience Platform;홈;인기 항목;정책 적용;마케팅 작업 api;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 마케팅 작업 API 끝점
topic-legacy: developer guide
description: Adobe Experience Platform 데이터 거버넌스 컨텍스트에서 마케팅 작업은 Experience Platform 데이터 소비자가 취하는 동작으로, 데이터 사용 정책 위반을 확인해야 합니다.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 2%

---

# 마케팅 작업 끝점

Adobe Experience Platform [!DNL Data Governance] 컨텍스트에서 마케팅 작업은 데이터 사용 정책 위반을 확인해야 하는 [!DNL Experience Platform] 데이터 소비자가 취하는 작업입니다.

정책 서비스 API에서 `/marketingActions` 끝점을 사용하여 조직에 대한 마케팅 작업을 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 마케팅 작업 목록 검색 {#list}

각각 `/marketingActions/core` 또는 `/marketingActions/custom`에 GET 요청을 하여 핵심 또는 사용자 지정 마케팅 작업 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**요청**

다음 요청은 조직에서 유지 관리하는 사용자 지정 마케팅 작업 목록을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 `name` 및 `href`을 포함하여 검색된 각 마케팅 작업에 대한 세부 정보를 반환합니다. `href` 값은 [데이터 사용 정책](policies.md#create-policy)을 만들 때 마케팅 작업을 식별하는 데 사용됩니다.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io/marketingActions/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "sampleMarketingAction",
            "description": "Marketing Action description.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550714012088,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550714012088,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
                }
            }
        },
        {
            "name": "newMarketingAction",
            "description": "Another marketing action.",
            "imsOrg": "{IMS_ORG}",
            "created": 1550793833224,
            "createdClient": "string",
            "createdUser": "string",
            "updated": 1550793833224,
            "updatedClient": "string",
            "updatedUser": "string",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/newMarketingAction"
                }
            }
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `_page.count` | 반환된 총 마케팅 작업 수입니다. |
| `children` | 검색된 마케팅 작업의 세부 사항이 포함된 개체 배열입니다. |
| `name` | 특정 마케팅 작업](#lookup)을(를) 조회할 때 고유한 식별자로 작동하는 마케팅 작업의 이름입니다.[ |
| `_links.self.href` | [데이터 사용 정책](policies.md#create-policy)을 만들 때 `marketingActionsRefs` 배열을 완료하는 데 사용할 수 있는 마케팅 작업에 대한 URI 참조입니다. |

## 특정 마케팅 작업 {#lookup} 조회

GET 요청 경로에 마케팅 작업의 `name` 속성을 포함하여 특정 마케팅 작업의 세부 사항을 조회합니다.

**API 형식**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 조회할 마케팅 작업의 `name` 속성. |

**요청**

다음 요청은 `combineData`이라는 사용자 지정 마케팅 작업을 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 개체에는 [데이터 사용 정책](policies.md#create-policy)(`marketingActionsRefs`)을 정의할 때 마케팅 작업을 참조하는 데 필요한 경로(`_links.self.href`)를 포함하여 마케팅 작업에 대한 세부 사항이 포함됩니다.

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550793805590,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550793805590,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData"
        }
    }
}
```

## 사용자 지정 마케팅 작업 {#create-update} 만들기 또는 업데이트

PUT 요청 경로에 마케팅 작업의 기존 또는 의도한 이름을 포함하여 새 사용자 지정 마케팅 작업을 만들거나 기존 마케팅 작업을 업데이트할 수 있습니다.

**API 형식**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 만들거나 업데이트할 마케팅 작업의 이름. 제공된 이름의 마케팅 작업이 이미 시스템에 있는 경우 해당 마케팅 작업이 업데이트됩니다. 존재하지 않는 경우 제공된 이름에 대해 새 마케팅 작업이 만들어집니다. |

**요청**

동일한 이름의 마케팅 작업이 아직 시스템에 없는 경우 다음 요청은 `crossSiteTargeting`이라는 새 마케팅 작업을 만듭니다. `crossSiteTargeting` 마케팅 작업이 존재하는 경우 이 호출은 대신 페이로드에 제공된 속성을 기반으로 마케팅 작업을 업데이트합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 만들거나 업데이트할 마케팅 작업의 이름. <br><br>**중요**:이 속성은 경로 `{MARKETING_ACTION_NAME}` 의 속성과 일치해야 하며, 그렇지 않으면 HTTP 400(잘못된 요청) 오류가 발생합니다. 즉, 마케팅 작업이 만들어지면 `name` 속성을 변경할 수 없습니다. |
| `description` | 마케팅 작업에 대한 추가 컨텍스트를 제공하는 선택적 설명입니다. |

**응답**

성공적인 응답은 마케팅 작업의 세부 사항을 반환합니다. 기존 마케팅 작업이 업데이트되면 응답은 HTTP 상태 200(확인)을 반환합니다. 새 마케팅 작업이 만들어진 경우 응답은 HTTP 상태 201(만들음)을 반환합니다.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{IMS_ORG}",
    "created": 1550713341915,
    "createdClient": "string",
    "createdUser": "string",
    "updated": 1550713856390,
    "updatedClient": "string",
    "updatedUser": "string",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
        }
    }
}
```

## 사용자 지정 마케팅 작업 {#delete} 삭제

DELETE 요청 경로에 사용자 지정 마케팅 작업의 이름을 포함시켜 삭제할 수 있습니다.

>[!NOTE]
>
>기존 정책에서 참조하는 마케팅 작업은 삭제할 수 없습니다. 이러한 마케팅 작업 중 하나를 삭제하려고 하면 마케팅 작업을 참조하는 모든 정책의 ID를 포함하는 메시지와 함께 HTTP 400(잘못된 요청) 오류가 발생합니다.

**API 형식**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 삭제할 마케팅 작업의 이름입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 빈 응답 본문을 포함하는 HTTP 상태 200(OK)을 반환합니다.

[마케팅 작업](#look-up)을 조회하여 삭제를 확인할 수 있습니다. 시스템에서 마케팅 작업을 제거한 경우 HTTP 404(찾을 수 없음) 오류가 표시됩니다.
