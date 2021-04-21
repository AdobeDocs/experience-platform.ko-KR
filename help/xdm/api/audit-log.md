---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;감사;감사 로그;변경 로그;rpc;rpc
solution: Experience Platform
title: 감사 로그 API 끝점
description: 스키마 레지스트리 API의 /audition 끝점을 사용하면 기존 XDM 리소스에 대해 수행된 변경 사항의 시간순 목록을 검색할 수 있습니다.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 2%

---

# 감사 로그 끝점

각 XDM(경험 데이터 모델) 리소스에 대해 [!DNL Schema Registry]은 다른 업데이트 사이에 발생한 모든 변경 내용의 로그를 유지 관리합니다. [!DNL Schema Registry] API의 `/auditlog` 끝점을 사용하면 ID로 지정한 클래스, 믹싱, 데이터 유형 또는 스키마에 대한 감사 로그를 검색할 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, Experience Platform API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

`/auditlog` 끝점은 [!DNL Schema Registry]에서 지원하는 RPC(원격 프로시저 호출)의 일부입니다. [!DNL Schema Registry] API의 다른 끝점과 달리 RPC 끝점에는 `Accept` 또는 `Content-Type` 같은 추가 헤더가 필요하지 않으며 `CONTAINER_ID`을(를) 사용하지 않습니다. 대신, 아래 API 호출에 설명된 대로 `/rpc` 네임스페이스를 사용해야 합니다.

## 리소스에 대한 감사 로그 검색

`/auditlog` 끝점에 대한 GET 요청 경로에 리소스 ID를 지정하여 스키마 라이브러리 내의 모든 클래스, 믹싱, 데이터 유형 또는 스키마에 대한 감사 로그를 검색할 수 있습니다.

**API 형식**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_ID}` | 감사 로그를 검색할 리소스의 `meta:altId` 또는 URL 인코딩 `$id`. |

**요청**

다음 요청은 `Restaurant` 믹싱에 대한 감사 로그를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 최신 응답에서 최신 응답까지 리소스에 대한 변경 사항 목록을 시간 순으로 반환합니다.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| 속성 | 설명 |
| --- | --- |
| `auditTrails` | 지정된 리소스 또는 종속 리소스 중 하나에 대한 변경 사항을 나타내는 각 객체가 포함된 객체의 배열입니다. |
| `id` | 변경된 리소스의 `$id`. 이 값은 일반적으로 요청 경로에 지정된 리소스를 나타내지만, 이 리소스가 변경 소스인 경우 종속 리소스를 나타낼 수 있습니다. |
| `action` | 수행된 변경 유형입니다. |
| `path` | 변경하거나 추가한 특정 필드의 경로를 나타내는 [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 문자열. |
| `value` | 새 필드나 업데이트된 필드에 지정된 값입니다. |
