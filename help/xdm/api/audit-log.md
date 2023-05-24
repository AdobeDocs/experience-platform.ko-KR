---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;감사;감사 로그;변경 로그;변경 로그;rpc;
solution: Experience Platform
title: 감사 로그 API 끝점
description: 스키마 레지스트리 API의 /auditlog 끝점을 사용하면 기존 XDM 리소스에 수행된 변경 사항의 시간 목록을 검색할 수 있습니다.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# 감사 로그 끝점

각 XDM(Experience Data Model) 리소스에 대해 [!DNL Schema Registry] 는 다른 업데이트 간에 발생한 모든 변경 사항의 로그를 유지 관리합니다. 다음 `/auditlog` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 ID로 지정된 클래스, 스키마 필드 그룹, 데이터 유형 또는 스키마에 대한 감사 로그를 검색할 수 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

다음 `/auditlog` 끝점은 이 지원하는 원격 프로시저 호출(RPC)의 일부입니다. [!DNL Schema Registry]. 의 다른 끝점과 달리 [!DNL Schema Registry] API, RPC 끝점에는 다음과 같은 추가 헤더가 필요하지 않습니다. `Accept` 또는 `Content-Type`, 및 를 사용하지 않음 `CONTAINER_ID`. 대신 `/rpc` 네임스페이스. 아래 API 호출에 나와 있습니다.

## 리소스에 대한 감사 로그 검색

에 대한 GET 요청의 경로에 리소스 ID를 지정하여 스키마 라이브러리 내의 모든 클래스, 필드 그룹, 데이터 유형 또는 스키마에 대한 감사 로그를 검색할 수 있습니다. `/auditlog` 엔드포인트.

**API 형식**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{RESOURCE_ID}` | 다음 `meta:altId` 또는 URL로 인코딩 `$id` 감사 로그를 검색할 리소스의 입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 스키마에 대한 감사 로그를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 가장 최근 항목에서 가장 최근 항목까지 리소스에 수행된 변경 사항의 시간 순 목록을 반환합니다.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| 속성 | 설명 |
| --- | --- |
| `updates` | 각 객체가 지정된 리소스 또는 종속 리소스 중 하나에 대한 변경 사항을 나타내는 객체의 배열입니다. |
| `id` | 다음 `$id` 변경된 리소스. 이 값은 일반적으로 요청 경로에 지정된 리소스를 나타내지만, 변경 소스인 경우 종속 리소스를 나타낼 수 있습니다. |
| `xdmType` | 변경된 리소스 유형. |
| `action` | 수행된 변경 유형입니다. |
| `path` | A [JSON 포인터](../../landing/api-fundamentals.md#json-pointer) 변경하거나 추가한 특정 필드의 경로를 나타내는 문자열입니다. |
| `value` | 새 필드 또는 업데이트된 필드에 지정된 값입니다. |

{style="table-layout:auto"}
