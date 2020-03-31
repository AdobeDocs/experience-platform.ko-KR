---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 리소스 삭제
topic: developer guide
translation-type: tm+mt
source-git-commit: d9ab2b1226b051be43f8fc0dd222bc075caed6f0

---


# 리소스 삭제

스키마 레지스트리에서 리소스를 제거(삭제)해야 하는 경우가 있습니다. 테넌트 컨테이너에서 만든 리소스만 삭제할 수 있습니다. 삭제할 리소스의 DELETE 요청을 `$id` 사용하여 이 작업을 수행합니다.

**API 형식**

```http
DELETE /tenant/{RESOURCE_TYPE}/{RESOURCE_ID} 
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_TYPE}` | 스키마 라이브러리에서 삭제할 리소스 유형입니다. 유효한 유형은 `datatypes`, `mixins`, `schemas`및 `classes`입니다. |
| `{RESOURCE_ID}` | URL로 인코딩된 `$id` URI 또는 `meta:altId` 리소스의 URL입니다. |

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

자원에 대한 조회(GET) 요청을 시도하여 삭제를 확인할 수 있습니다. 요청에 Accept 헤더를 포함해야 하지만 리소스가 스키마 레지스트리에서 제거되었으므로 HTTP 상태 404(찾을 수 없음)를 받아야 합니다.