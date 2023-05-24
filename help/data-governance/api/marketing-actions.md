---
keywords: Experience Platform;홈;인기 항목;정책 적용;마케팅 작업 api;API 기반 적용;데이터 거버넌스
solution: Experience Platform
title: 마케팅 액션 API 엔드포인트
description: Adobe Experience Platform 데이터 거버넌스 컨텍스트에서 마케팅 작업은 Experience Platform 데이터 소비자가 수행하는 작업으로서 데이터 사용 정책 위반을 확인해야 합니다.
exl-id: bc16b318-d89c-4fe6-bf5a-1a4255312f54
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# 마케팅 액션 엔드포인트

Adobe Experience Platform 데이터 거버넌스 컨텍스트에서 마케팅 작업은 [!DNL Experience Platform] 데이터 소비자는 데이터 사용 정책 위반 여부를 확인할 필요가 있습니다.

다음을 사용하여 조직의 마케팅 작업을 관리할 수 있습니다. `/marketingActions` 정책 서비스 API의 끝점입니다.

## 시작하기

이 안내서에 사용된 API 엔드포인트는 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기에 대한 안내서 및 를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보 [!DNL Experience Platform] API.

## 마케팅 액션 목록 검색 {#list}

에 GET 요청을 하여 핵심 또는 사용자 지정 마케팅 작업 목록을 검색할 수 있습니다. `/marketingActions/core` 또는 `/marketingActions/custom`, 각각

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 검색된 각 마케팅 작업에 대한 세부 정보를 반환합니다(다음을 포함). `name` 및 `href`. 다음 `href` 다음 경우에 마케팅 액션을 식별하는 데 값이 사용됨: [데이터 사용 정책 만들기](policies.md#create-policy).

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
            "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `children` | 검색된 마케팅 작업의 세부 정보가 포함된 객체의 배열입니다. |
| `name` | 다음의 경우 고유 식별자로 작동하는 마케팅 작업의 이름 [특정 마케팅 작업 조회](#lookup). |
| `_links.self.href` | 마케팅 액션에 대한 URI 참조로, 다음을 완료하는 데 사용할 수 있습니다. `marketingActionsRefs` 다음과 같은 경우 배열 [데이터 사용 정책 만들기](policies.md#create-policy). |

## 특정 마케팅 액션 조회 {#lookup}

마케팅 작업을 포함하여 특정 마케팅 작업의 세부 정보를 조회합니다. `name` GET 요청 경로에 있는 속성입니다.

**API 형식**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 다음 `name` 조회할 마케팅 작업의 속성입니다. |

**요청**

다음 요청은 이라는 사용자 지정 마케팅 작업을 검색합니다. `combineData`.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 개체에는 경로( )를 포함한 마케팅 작업에 대한 세부 정보가 포함되어 있습니다.`_links.self.href`다음과 같은 경우 마케팅 작업을 참조해야 합니다. [데이터 사용 정책 정의](policies.md#create-policy) (`marketingActionsRefs`).

```JSON
{
    "name": "combineData",
    "description": "Combine multiple data sources together.",
    "imsOrg": "{ORG_ID}",
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

## 사용자 지정 마케팅 액션 만들기 또는 업데이트 {#create-update}

마케팅 작업의 기존 이름 또는 의도한 이름을 PUT 요청 경로에 포함하여 새 사용자 지정 마케팅 작업을 만들거나 기존 사용자 지정 마케팅 작업을 업데이트할 수 있습니다.

**API 형식**

```http
PUT /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 만들거나 업데이트할 마케팅 액션의 이름입니다. 입력한 이름의 마케팅 작업이 시스템에 이미 있으면 해당 마케팅 작업이 업데이트됩니다. 마케팅 액션이 없으면 제공된 이름에 대해 새 마케팅 액션이 만들어집니다. |

**요청**

다음 요청은 이라는 새 마케팅 작업을 만듭니다. `crossSiteTargeting`동일한 이름의 마케팅 작업이 시스템에 아직 존재하지 않는 경우. 다음과 같은 경우 `crossSiteTargeting` 마케팅 액션이 존재하지 않습니다. 대신 이 호출은 페이로드에 제공된 속성을 기반으로 해당 마케팅 액션을 업데이트합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 만들거나 업데이트할 마케팅 액션의 이름입니다. <br><br>**중요 사항**: 이 속성은 다음과 일치해야 합니다. `{MARKETING_ACTION_NAME}` 그렇지 않으면 HTTP 400(잘못된 요청) 오류가 발생합니다. 즉, 마케팅 액션이 만들어지면 `name` 속성을 변경할 수 없습니다. |
| `description` | 마케팅 작업에 대한 추가 컨텍스트를 제공하기 위한 선택적 설명입니다. |

**응답**

성공적인 응답은 마케팅 액션의 세부 정보를 반환합니다. 기존 마케팅 작업이 업데이트된 경우 응답은 HTTP 상태 200(OK)을 반환합니다. 새 마케팅 작업이 생성되면 응답은 HTTP 상태 201(생성됨)을 반환합니다.

```JSON
{
    "name": "crossSiteTargeting",
    "description": "Perform targeting on information obtained across multiple web sites.",
    "imsOrg": "{ORG_ID}",
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

## 사용자 지정 마케팅 액션 삭제 {#delete}

사용자 지정 마케팅 액션의 이름을 DELETE 요청 경로에 포함하여 삭제할 수 있습니다.

>[!NOTE]
>
>기존 정책에서 참조하는 마케팅 작업은 삭제할 수 없습니다. 이러한 마케팅 작업 중 하나를 삭제하려고 하면 마케팅 작업을 참조하는 모든 정책의 ID를 포함하는 메시지와 함께 HTTP 400(잘못된 요청) 오류가 발생합니다.

**API 형식**

```http
DELETE /marketingActions/custom/{MARKETING_ACTION_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 삭제할 마케팅 액션의 이름입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 빈 응답 본문과 함께 HTTP 상태 200(OK)을 반환합니다.

다음을 시도하여 삭제를 확인할 수 있습니다 [마케팅 액션 조회](#look-up). 마케팅 작업이 시스템에서 제거된 경우 HTTP 404(찾을 수 없음) 오류가 표시됩니다.
