---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;감사;감사 로그;변경 로그;rpc;
solution: Experience Platform
title: 감사 로그 API 끝점
description: 스키마 레지스트리 API의 /auditlog 종단점을 사용하면 기존 XDM 리소스에 대한 변경 사항을 시간 순서대로 가져올 수 있습니다.
topic-legacy: developer guide
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 3%

---

# 감사 로그 끝점

각 XDM(Experience Data Model) 리소스에 대해 [!DNL Schema Registry]은(는) 다른 업데이트 간에 발생한 모든 변경 사항의 로그를 유지합니다. [!DNL Schema Registry] API의 `/auditlog` 종단점을 사용하면 ID로 지정된 클래스, 스키마 필드 그룹, 데이터 유형 또는 스키마에 대한 감사 로그를 검색할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

`/auditlog` 끝점은 [!DNL Schema Registry]에서 지원하는 원격 프로시저 호출(RPC)의 일부입니다. [!DNL Schema Registry] API의 다른 끝점과 달리 RPC 끝점은 `Accept` 또는 `Content-Type` 같은 추가 헤더가 필요하지 않으며 `CONTAINER_ID`를 사용하지 않습니다. 대신 아래 API 호출에 설명된 대로 `/rpc` 네임스페이스를 사용해야 합니다.

## 리소스에 대한 감사 로그 검색

`/auditlog` 종단점에 대한 GET 요청 경로에 리소스의 ID를 지정하여 스키마 라이브러리 내에서 클래스, 필드 그룹, 데이터 유형 또는 스키마에 대한 감사 로그를 검색할 수 있습니다.

**API 형식**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{RESOURCE_ID}` | 검색할 감사 로그가 있는 리소스의 `meta:altId` 또는 URL 인코딩 `$id`. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `Restaurant` 필드 그룹에 대한 감사 로그를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 가장 최근-가장 최근 간 리소스에 대한 변경 사항 목록을 시간 순서대로 반환합니다.

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
| `auditTrails` | 지정된 리소스 또는 종속 리소스 중 하나에 대한 변경 사항을 나타내는 객체의 배열입니다. |
| `id` | 변경된 리소스의 `$id`. 이 값은 일반적으로 요청 경로에 지정된 리소스를 나타내지만, 이 값이 변경 사항의 소스인 경우 종속 리소스를 나타낼 수 있습니다. |
| `action` | 수행된 변경 유형입니다. |
| `path` | 변경하거나 추가한 특정 필드의 경로를 나타내는 [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 문자열. |
| `value` | 새 필드 또는 업데이트된 필드에 지정된 값입니다. |

{style=&quot;table-layout:auto&quot;}
