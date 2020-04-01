---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 마케팅 작업
topic: developer guide
translation-type: tm+mt
source-git-commit: 08d02e7323f75c450e7a250835f26a569685cdd1

---


# 마케팅 작업

Adobe Experience Platform 데이터 거버넌스의 맥락에서 마케팅 작업은 경험 플랫폼 데이터 소비자가 취하는 조치이며, 데이터 사용 정책 위반을 확인해야 합니다.

API에서 마케팅 작업을 사용하려면 `/marketingActions` 끝점을 사용해야 합니다.

## 모든 마케팅 작업 나열

모든 마케팅 작업의 목록을 보려면 지정된 컨테이너에 대한 모든 정책을 반환하거나 `/marketingActions/core` GET 요청을 `/marketingActions/custom` 수행할 수 있습니다.

**API 형식**

```http
GET /marketingActions/core
GET /marketingActions/custom
```

**요청**

다음 요청은 IMS 조직에서 정의한 모든 사용자 지정 마케팅 작업 목록을 반환합니다.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 개체는 컨테이너의 총 마케팅 작업(`count`)을 제공하며 `children` 배열은 마케팅 작업에 대한 `name` 및 `href` 정보를 포함하여 각 마케팅 작업에 대한 세부 사항을 포함합니다. 이 경로(`_links.self.href`)는 데이터 사용 정책을 `marketingActionsRefs` [만들 때](policies.md#create-policy)배열을 완료하는 데 사용됩니다.

```JSON
{
    "_page": {
        "start": "sampleMarketingAction",
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

## 특정 마케팅 활동 보기

특정 마케팅 작업의 세부 사항을 보기 위해 조회(GET) 요청을 수행할 수도 있습니다. 이 작업은 마케팅 `name` 작업의 기능을 사용하여 수행됩니다. 이름을 알 수 없으면 이전에 표시된 목록(GET) 요청을 사용하여 찾을 수 있습니다.

**API 형식**

```http
GET /marketingActions/core/{marketingActionName}
GET /marketingActions/custom/{marketingActionName}
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/combineData \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 객체에는 데이터 사용 정책(`_links.self.href`)을 정의할 때 마케팅 작업을 참조하는 데 필요한 경로(`marketingActionsRefs`)를 비롯하여 마케팅 작업에 대한 세부 사항이 포함됩니다.

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

## 마케팅 작업 만들기 또는 업데이트

정책 서비스 API를 사용하면 고유한 마케팅 작업을 정의하고 기존 마케팅 작업을 업데이트할 수 있습니다. 생성 및 업데이트는 모두 마케팅 작업의 이름에 PUT 작업을 사용하여 수행됩니다.

**API 형식**

```http
PUT /marketingActions/custom/{marketingActionName}
```

**요청**

다음과 같은 요청에서 요청 페이로드의 `name` 내용이 API `{marketingActionName}` 호출의 요청과 동일함을 알 수 있습니다. 읽기 전용 및 시스템에서 생성된 `id` 정책의 정책과 달리 마케팅 작업을 만들려면 마케팅 작업의 _의도된_ 이름을 제공해야 합니다.

>[!NOTE] 호출에서 PUT을 `{marketingActionName}` 직접 수행할 수 없으므로 405 오류(메서드가 허용되지 않음)가 `/marketingActions/custom` 발생합니다. 또한 페이로드의 `name` 내용이 경로의 항목과 일치하지 `{marketingActionName}` 않으면 400 오류(잘못된 요청)가 표시됩니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "crossSiteTargeting",
        "description": "Perform targeting on information obtained across multiple web sites."
      }'
```

**응답**

성공적으로 만들어지면 HTTP 상태 201(작성됨)이 수신되고 새로 만든 마케팅 작업의 세부 정보가 응답 본문에 포함됩니다. 응답의 `name` 값은 요청에서 전송된 것과 일치해야 합니다.

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

## 마케팅 작업 삭제

제거하려는 마케팅 작업에 DELETE 요청을 보내 마케팅 작업을 삭제할 `{marketingActionName}` 수 있습니다.

>[!NOTE] 기존 정책에서 참조하는 마케팅 작업은 삭제할 수 없습니다. 이렇게 하면 삭제하려는 마케팅 작업에 대한 참조가 포함된 정책(또는 정책의 여러 ID)의 `id` (또는)을 포함하는 오류 메시지와 함께 400 오류(잘못된 요청)가 발생합니다.

**API 형식**

```http
DELETE /marketingActions/custom/{marketingActionName}
```

**요청**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

마케팅 작업이 성공적으로 삭제되면 HTTP 상태 200(확인)으로 응답 본문이 비어 있게 됩니다.

마케팅 작업을 조회(GET)하여 삭제를 확인할 수 있습니다. 마케팅 작업이 제거되었기 때문에 &quot;찾을 수 없음&quot; 오류 메시지와 함께 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.
