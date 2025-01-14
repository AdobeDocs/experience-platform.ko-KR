---
title: 흐름 서비스 API를 사용하여 Zendesk용 데이터 흐름 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Zendesk에 연결하는 방법을 알아봅니다.
exl-id: 3e00e375-c6f8-407c-bded-7357ccf3482e
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 1%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Zendesk]에 대한 데이터 흐름 만들기

다음 자습서에서는 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)를 사용하여 [!DNL Zendesk] 데이터를 플랫폼으로 가져오기 위한 소스 연결 및 데이터 흐름을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 다음 Experience Platform 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]은(는) 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Zendesk]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

플랫폼에서 [!DNL Zendesk] 계정에 액세스하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `subdomain` | 계정과 연결된 고유 도메인. | `https://yoursubdomain.zendesk.com` |
| `accessToken` | Zendesk API 토큰. | `0lZnClEvkJSTQ7olGLl7PMhVq99gu26GTbJtf` |

[!DNL Zendesk] 원본 인증에 대한 자세한 내용은 [[!DNL Zendesk] 원본 개요](../../../../connectors/customer-success/zendesk.md)를 참조하세요.

## [!DNL Flow Service] API를 사용하여 [!DNL Zendesk]을(를) 플랫폼에 연결

다음 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Zendesk] 데이터를 플랫폼으로 가져오기 위해 [!DNL Zendesk] 소스 연결을 만들고 데이터 흐름을 만드는 단계를 안내합니다.

### 기본 연결 만들기 {#base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Zendesk] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Zendesk]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk base connection",
        "description": "Zendesk base connection to authenticate to Platform",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "auth": {
            "specName": "OAuth2 Refresh Code",
            "params": {
                "subdomain": "{SUBDOMAIN}",
                "accessToken": "{ACCESS_TOKEN}"
            }
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 [!DNL Flow Service] API를 통해 소스를 등록 및 승인한 후에 검색할 수 있습니다. |
| `auth.specName` | Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.` | 소스 인증에 필요한 자격 증명을 포함합니다. |
| `auth.params.subdomain` | 계정과 연결된 고유 도메인. 하위 도메인의 형식은 `https://yoursubdomain.zendesk.com`입니다. |
| `auth.params.accessToken` | 소스 인증에 사용되는 해당 액세스 토큰입니다. OAuth 기반 인증에 필요합니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### 소스 탐색 {#explore}

이전 단계에서 생성한 기본 연결 ID를 사용하여 GET 요청을 수행하여 파일 및 디렉터리를 탐색할 수 있습니다.
다음 호출을 사용하여 [!DNL Platform](으)로 가져올 파일의 경로를 찾으십시오.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

소스의 파일 구조 및 컨텐츠를 탐색하기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.


| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `objectType=rest` | 탐색하려는 오브젝트의 유형입니다. 현재 이 값은 항상 `rest`(으)로 설정되어 있습니다. |
| `{OBJECT}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. |
| `fileType=json` | Platform으로 가져올 파일의 파일 유형입니다. 현재 지원되는 파일 형식은 `json`뿐입니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | Platform으로 가져올 소스 파일의 매개 변수를 정의합니다. `{SOURCE_PARAMS}`에 대해 허용되는 형식 유형을 검색하려면 base64에서 전체 `parameter` 문자열을 인코딩해야 합니다. 아래 예에서 base64로 인코딩된 `"{}"`은(는) `e30`과(와) 같습니다. |


**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/70383d02-2777-4be7-a309-9dd6eea1b46d/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 쿼리된 파일의 구조를 반환합니다. ``data[]`` 페이로드 내의 아래 예제에서는 단일 레코드만 표시되지만 여러 레코드가 있을 수 있습니다.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "result": {
                "type": "object",
                "properties": {
                    "organization_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "external_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "role_type": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "custom_role_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "default_group_id": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "phone": {
                        "type": "string"
                    },
                    "shared_phone_number": {
                        "type": "boolean"
                    },
                    "alias": {
                        "type": "string"
                    },
                    "last_login_at": {
                        "type": "string"
                    },
                    "signature": {
                        "type": "string"
                    },
                    "details": {
                        "type": "string"
                    },
                    "notes": {
                        "type": "string"
                    },
                    "photo": {
                        "type": "string",
                        "media": {
                            "binaryEncoding": "base64",
                            "type": "image/png"
                        }
                    },
                    "active": {
                        "type": "boolean"
                    },
                    "created_at": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    },
                    "iana_time_zone": {
                        "type": "string"
                    },
                    "id": {
                        "type": "integer"
                    },
                    "locale": {
                        "type": "string"
                    },
                    "locale_id": {
                        "type": "integer"
                    },
                    "moderator": {
                        "type": "boolean"
                    },
                    "name": {
                        "type": "string"
                    },
                    "only_private_comments": {
                        "type": "boolean"
                    },
                    "report_csv": {
                        "type": "boolean"
                    },
                    "restricted_agent": {
                        "type": "boolean"
                    },
                    "result_type": {
                        "type": "string"
                    },
                    "role": {
                        "type": "integer"
                    },
                    "shared": {
                        "type": "boolean"
                    },
                    "shared_agent": {
                        "type": "boolean"
                    },
                    "suspended": {
                        "type": "boolean"
                    },
                    "ticket_restriction": {
                        "type": "string"
                    },
                    "time_zone": {
                        "type": "string"
                    },
                    "two_factor_auth_enabled": {
                        "type": "boolean"
                    },
                    "updated_at": {
                        "type": "string"
                    },
                    "url": {
                        "type": "string"
                    },
                    "verified": {
                        "type": "boolean"
                    },
                    "tags": {
                        "type": "array",
                        "items": {
                            "type": "string"
                        }
                    }
                }
            }
        }
    },
    "data": [
        {
            "result": {
                "id": 6106699702801,
                "url": "https://{YOURSUBDOMAIN}.zendesk.com/api/v2/users/6106699702801.json",
                "name": "test",
                "email": "test@org.com",
                "created_at": "2022-05-13T08:04:22Z",
                "updated_at": "2022-05-13T08:04:22Z",
                "time_zone": "Asia/Kolkata",
                "iana_time_zone": "Asia/Kolkata",
                "locale_id": 1,
                "locale": "en-US",
                "role": "end-user",
                "verified": false,
                "active": true,
                "shared": false,
                "shared_agent": false,
                "two_factor_auth_enabled": false,
                "moderator": false,
                "ticket_restriction": "requested",
                "only_private_comments": false,
                "restricted_agent": true,
                "suspended": false,
                "report_csv": false,
                "result_type": "user"
            }
        }
    ]
}
```

### 소스 연결 만들기 {#source-connection}

[!DNL Flow Service] API에 대한 POST 요청을 수행하여 소스 연결을 만들 수 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은 [!DNL Zendesk]에 대한 소스 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Source Connection",
        "description": "Zendesk Source Connection",
        "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
        "connectionSpec": {
            "id": "0a27232b-2c6e-4396-b8c6-c9fc24e37ba4",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {}
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | [!DNL Zendesk]의 기본 연결 ID. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 수집할 [!DNL Zendesk] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |

**응답**

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

## 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오.

### 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 수행하고 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크에 해당하는 고정 연결 사양 ID를 제공해야 합니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 데이터 레이크에 대한 연결 사양 ID가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 원본 데이터를 포함할 데이터 집합을 지정할 수 있습니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은 Zendesk에 대한 대상 연결을 만듭니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk Target Connection",
        "description": "Zendesk Target Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "dataSetId": "624bf42e16519d19496e3f67"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 데이터 레이크에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다. |
| `data.format` | 플랫폼으로 가져올 [!DNL Zendesk] 데이터의 형식입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 이후 단계에서 필수입니다.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다. 요청 페이로드 내에 정의된 데이터 매핑을 사용하여 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)에 대한 POST 요청을 수행하면 됩니다.

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "version": 0,
        "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/995dabbea86d58e346ff91bd8aa741a9f36f29b1019138d4",
        "xdmVersion": "1.0",
        "mappings": [
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.id",
                "destination": "_extconndev.id",
                "name": "id",
                "description": "Zendesk"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.external_id",
                "destination": "_extconndev.external_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role_type",
                "destination": "_extconndev.role_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.custom_role_id",
                "destination": "_extconndev.custom_role_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.default_group_id",
                "destination": "_extconndev.default_group_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.phone",
                "destination": "_extconndev.phone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_phone_number",
                "destination": "_extconndev.shared_phone_number"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.alias",
                "destination": "_extconndev.alias"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.last_login_at",
                "destination": "_extconndev.last_login_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.signature",
                "destination": "_extconndev.signature"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.details",
                "destination": "_extconndev.details"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.notes",
                "destination": "_extconndev.notes"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.active",
                "destination": "_extconndev.active"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.created_at",
                "destination": "_extconndev.created_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.email",
                "destination": "_extconndev.email"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.iana_time_zone",
                "destination": "_extconndev.iana_time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.organization_id",
                "destination": "_extconndev.organization_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale",
                "destination": "_extconndev.locale"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.locale_id",
                "destination": "_extconndev.locale_id"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.moderator",
                "destination": "_extconndev.moderator"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.name",
                "destination": "_extconndev.name"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.only_private_comments",
                "destination": "_extconndev.only_private_comments"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.report_csv",
                "destination": "_extconndev.report_csv"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.restricted_agent",
                "destination": "_extconndev.restricted_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.result_type",
                "destination": "_extconndev.result_type"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.role",
                "destination": "_extconndev.role"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared",
                "destination": "_extconndev.shared"
            },        {
                "sourceType": "ATTRIBUTE",
                "source": "result.shared_agent",
                "destination": "_extconndev.shared_agent"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.time_zone",
                "destination": "_extconndev.time_zone"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.two_factor_auth_enabled",
                "destination": "_extconndev.two_factor_auth_enabled"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.suspended",
                "destination": "_extconndev.suspended"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.updated_at",
                "destination": "_extconndev.updated_at"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.url",
                "destination": "_extconndev.url"
            },
            {
                "sourceType": "ATTRIBUTE",
                "source": "result.verified",
                "destination": "_extconndev.verified"
            }
        ]
    }'
```

| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 이전 단계에서 생성된 [대상 XDM 스키마](#target-schema)의 ID입니다. |
| `mappings.destinationXdmPath` | 소스 속성이 매핑되는 대상 XDM 경로. |
| `mappings.sourceAttribute` | 대상 XDM 경로에 매핑해야 하는 소스 속성입니다. |
| `mappings.identity` | 매핑 집합이 [!DNL Identity Service]에 대해 표시되는지 여부를 지정하는 부울 값입니다. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 플로우 만들기 {#flow}

Zendesk에서 플랫폼으로 데이터를 가져오는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

* [Source 연결 ID](#source-connection)
* [대상 연결 ID](#target-connection)
* [ID 매핑](#mapping)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 `once`, `minute`, `hour`, `day` 또는 `week` 옵션 중 하나로 설정해야 합니다. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하지만, 일회성 수집을 만들 때는 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값을 `15`보다 크거나 같게 설정해야 합니다.


**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/flows' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Zendesk dataflow",
        "description": "Zendesk dataflow",
        "flowSpec": {
            "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "246d052c-da4a-494a-937f-a0d17b1c6cf5"
        ],
        "targetConnectionIds": [
            "7c96c827-3ffd-460c-a573-e9558f72f263"
        ],
        "transformations": [
            {
                "name": "Mapping",
                "params": {
                    "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
                    "mappingVersion": "0"
                }
            }
        ],
        "scheduleParams": {
            "startTime": "1625040887",
            "frequency": "minute",
            "interval": 15
        }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름의 이름입니다. 이 옵션을 사용하여 데이터 흐름에서 정보를 조회할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인하십시오. |
| `description` | 데이터 흐름에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID는 `6499120c-0b15-42dc-936e-847ea3c24d72`입니다. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전. 이 값은 기본적으로 `1.0`입니다. |
| `sourceConnectionIds` | 이전 단계에서 생성된 [소스 연결 ID](#source-connection)입니다. |
| `targetConnectionIds` | 이전 단계에서 생성된 [대상 연결 ID](#target-connection)입니다. |
| `transformations` | 이 속성에는 데이터에 적용하는 데 필요한 다양한 변형이 포함되어 있습니다. 이 속성은 XDM 규격이 아닌 데이터를 Platform으로 가져올 때 필요합니다. |
| `transformations.name` | 변환에 지정된 이름입니다. |
| `transformations.params.mappingId` | 이전 단계에서 생성된 [매핑 ID](#mapping)입니다. |
| `transformations.params.mappingVersion` | 매핑 ID의 해당 버전. 이 값은 기본적으로 `0`입니다. |
| `scheduleParams.startTime` | 이 속성은 데이터 흐름의 수집 예약에 대한 정보를 포함합니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 `once`, `minute`, `hour`, `day` 또는 `week`입니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도가 `once`(으)로 설정된 경우 간격이 필요하지 않으며 다른 빈도 값의 경우 `15`보다 크거나 같아야 합니다. |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대해 설명합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름 모니터링](../../monitor.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 업데이트

데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API의 `/flows` 끝점에 PATCH 요청을 하여 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트와 같은 데이터 흐름의 세부 정보를 업데이트합니다. PATCH 요청을 할 때 `If-Match` 헤더에 데이터 흐름의 고유한 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름을 업데이트하는 방법](../../update-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 업데이트

기본 연결 ID를 쿼리 매개 변수로 제공하면서 [!DNL Flow Service] API에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. PATCH 요청을 할 때는 `If-Match` 헤더에 원본 계정의 고유 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 계정을 업데이트하는 방법](../../update.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 삭제

쿼리 매개 변수의 일부로 삭제할 데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제하십시오. 전체 API 예제는 [API를 사용하여 데이터 흐름 삭제](../../delete-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 삭제

삭제할 계정의 기본 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. 전체 API 예제는 [API를 사용하여 소스 계정 삭제](../../delete.md)에 대한 안내서를 참조하십시오.