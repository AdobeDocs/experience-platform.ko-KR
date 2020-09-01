---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;delete
solution: Experience Platform
title: 리소스 삭제
describe: It may occasionally be necessary to remove resource from the Schema Registry. Only resources that you create in the tenant container may be deleted. This is done by performing a DELETE request using the $id of the resource you wish to delete.
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 7%

---


# 리소스 삭제

경우에 따라 리소스에서 리소스를 제거(DELETE)해야 할 수 있습니다 [!DNL Schema Registry]. 테넌트 컨테이너에서 만든 리소스만 삭제할 수 있습니다. 삭제하려는 리소스 `$id` 를 사용하여 DELETE 요청을 수행하면 됩니다.

**API 형식**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_TYPE}` | 에서 삭제할 리소스 [!DNL Schema Library]유형입니다. 유효한 유형은 `datatypes`, `mixins``schemas`, `classes`및 입니다. |
| `{RESOURCE_ID}` | URL로 인코딩된 `$id` URI 또는 리소스 `meta:altId` 의 URL입니다. |

**요청**

DELETE 요청에는 헤더 수락을 필요로 하지 않습니다.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fmixins%2F4fbd5368aa67f0e74d5838f67694c867 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

리소스에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 요청에 Accept 헤더를 포함해야 하지만 리소스는 HTTP 상태 404(찾을 수 없음)를 수신해야 합니다. 이는 리소스가 HTTP [!DNL Schema Registry]에서 제거되었기 때문입니다.