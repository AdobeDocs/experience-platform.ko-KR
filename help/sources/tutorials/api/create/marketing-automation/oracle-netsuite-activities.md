---
title: 흐름 서비스 API를 사용하여 Oracle NetSuite 활동에 대한 소스 연결 및 데이터 흐름 만들기
description: 흐름 서비스 API를 사용하여 Oracle NetSuite 이벤트 데이터를 Experience Platform으로 가져오기 위해 소스 연결 및 데이터 흐름을 만드는 방법을 알아봅니다.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 4f695389-2261-469c-8d40-7bd29a4e7f77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1974'
ht-degree: 1%

---

# 흐름 서비스 API를 사용하여 [!DNL Oracle NetSuite Activities]에 대한 소스 연결 및 데이터 흐름을 만듭니다.

>[!NOTE]
>
>[!DNL Oracle NetSuite Activities] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Oracle NetSuite Activities] 계정의 이벤트 데이터를 Adobe Experience Platform으로 가져오는 방법에 대해 알아보려면 다음 자습서를 참조하십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Oracle NetSuite Activities]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 인증

인증 자격 증명을 검색하는 방법에 대한 자세한 내용은 [[!DNL Oracle NetSuite] 개요](../../../../connectors/marketing-automation/oracle-netsuite.md)를 참조하십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## [!DNL Flow Service] API를 사용하여 [!DNL Oracle NetSuite Activities]을(를) Experience Platform에 연결

[!DNL Oracle NetSuite Activities] 소스를 인증하고, 소스 연결을 만들고, 데이터 흐름을 만들어 이벤트 데이터를 Experience Platform으로 가져오는 방법을 알아보려면 아래 안내서를 따르십시오.

### 기본 연결 만들기 {#base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Oracle NetSuite Activities] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Oracle NetSuite Activities]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NeSuite Activities base connection",
      "description": "Authenticated base connection for Oracle NetSuite Activities",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "accessTokenUrl": "{ACCESS_TOKEN_URL}",
              "accessToken": "{ACCESS_TOKEN_URL}"
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 [!DNL Flow Service] API를 통해 소스를 등록 및 승인한 후에 검색할 수 있습니다. |
| `auth.specName` | Experience Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.clientId` | 통합 레코드를 만들 때 클라이언트 ID 값입니다. 대화형 레코드를 만드는 프로세스를 [여기](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)에서 찾을 수 있습니다. 값은 `7fce.....b42f`과(와) 유사한 64자 문자열입니다. |
| `auth.params.clientSecret` | 통합 레코드를 만들 때 클라이언트 ID 값입니다. 대화형 레코드를 만드는 프로세스를 [여기](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981)에서 찾을 수 있습니다. 값은 `5c98.....1b46`과(와) 유사한 64자 문자열입니다. |
| `auth.params.accessTokenUrl` | ACCOUNT_ID를 [!DNL NetSuite] 계정 ID로 바꾸는 `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/auth/oauth2/v1/token`과(와) 유사한 [!DNL NetSuite] 액세스 토큰 URL. |
| `auth.params.accessToken` | 액세스 토큰 값이 [OAuth 2.0 인증 코드 부여 흐름](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) 자습서의 [2단계](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint)의 끝에 생성됩니다. 액세스 토큰 만료는 60분 동안만 유효합니다. 값은 `eyJr......f4V0`과(와) 유사한 JSON 웹 토큰(JWT) 형식의 1024자 문자열입니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
    "id": "60c81023-99b4-4aae-9c31-472397576dd2",
    "etag": "\"fa003785-0000-0200-0000-6555c5310000\""
}
```

### 소스 탐색 {#explore}

기본 연결 ID가 있으면 이제 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 `/connections` 끝점에 대한 GET 요청을 수행하여 소스 데이터의 내용과 구조를 탐색할 수 있습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**요청**

소스의 파일 구조 및 콘텐츠를 살펴보기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `objectType=rest` | 탐색하려는 오브젝트의 유형입니다. 현재 이 값은 항상 `rest`(으)로 설정되어 있습니다. |
| `{OBJECT}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. 이 원본의 값은 `json`입니다. |
| `fileType=json` | Experience Platform으로 가져올 파일의 파일 유형입니다. 현재 지원되는 파일 형식은 `json`뿐입니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | Experience Platform으로 가져올 소스 파일의 매개 변수를 정의합니다. `{SOURCE_PARAMS}`에 대해 허용되는 형식 유형을 검색하려면 전체 문자열을 base64로 인코딩해야 합니다. <br> [!DNL Oracle NetSuite Activities]에 대한 값이 비어 있습니다.</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=e30%3D' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 다음과 같은 JSON 구조를 반환합니다.

+++JSON 페이로드를 보려면 선택

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "totalResults": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "offset": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "count": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "hasMore": {
                "type": "boolean"
            },
            "links": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "rel": {
                            "type": "string"
                        },
                        "href": {
                            "type": "string"
                        }
                    }
                }
            },
            "items": {
                "type": "object",
                "properties": {
                    "owner": {
                        "type": "string"
                    },
                    "createddate": {
                        "type": "string"
                    },
                    "lastmodifieddate": {
                        "type": "string"
                    },
                    "accesslevel": {
                        "type": "string"
                    },
                    "alldayevent": {
                        "type": "string"
                    },
                    "message": {
                        "type": "string"
                    },
                    "startdate": {
                        "type": "string"
                    },
                    "title": {
                        "type": "string"
                    },
                    "organizer": {
                        "type": "string"
                    },
                    "response": {
                        "type": "string"
                    },
                    "links": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "location": {
                        "type": "string"
                    },
                    "timedevent": {
                        "type": "string"
                    },
                    "id": {
                        "type": "string"
                    },
                    "status": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2022-12-15",
                "id": "5",
                "lastmodifieddate": "2022-12-15",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-02-01",
                "id": "103",
                "lastmodifieddate": "2023-02-01",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2022-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
        {
            "totalResults": 13,
            "offset": 0,
            "count": 13,
            "hasMore": false,
            "links": [
                {
                    "rel": "self",
                    "href": "https://{ACCOUNT_ID}.suitetalk.api.netsuite.com/services/rest/query/v1/suiteql"
                }
            ],
            "items": {
                "accesslevel": "BUSY",
                "alldayevent": "F",
                "createddate": "2023-11-09",
                "id": "204",
                "lastmodifieddate": "2023-11-09",
                "location": "Caffe West",
                "message": "Bring Monthly Results",
                "organizer": "-5",
                "owner": "-5",
                "response": "ACCEPTED",
                "startdate": "2023-12-15",
                "status": "CONFIRMED",
                "timedevent": "T",
                "title": "Meeting with Tom"
            }
        },
    ]
}
```

+++

### 소스 연결 만들기 {#source-connection}

[!DNL Flow Service] API의 `/sourceConnections` 끝점에 대한 POST 요청을 수행하여 소스 연결을 만들 수 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은 [!DNL Oracle NetSuite Activities]에 대한 소스 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Source Connection",
      "description": "Oracle NetSuite Activities Source Connection",
      "baseConnectionId": "60c81023-99b4-4aae-9c31-472397576dd2",
      "connectionSpec": {
          "id": "fdf850b4-5a8d-4a5a-9ce8-4caef9abb2a8",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | [!DNL Oracle NetSuite Activities]의 기본 연결 ID. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 수집할 [!DNL Oracle NetSuite Activities] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "574c049f-29fc-411f-be0d-f80002025f51",
    "etag": "\"0704acb3-0000-0200-0000-6555c5470000\""
}
```

### 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 Experience Platform에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Experience Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md#create-a-schema)에 대한 자습서를 참조하십시오.

### 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/)에 대한 POST 요청을 수행하여 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크에 해당하는 고정 연결 사양 ID를 제공해야 합니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 데이터 레이크에 대한 연결 사양 ID가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 원본 데이터를 포함할 데이터 집합을 지정할 수 있습니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은 [!DNL Oracle NetSuite Activities]에 대한 대상 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle NetSuite Activities Target Connection Generic Rest",
      "description": "Oracle NetSuite Activities Target Connection Generic Rest",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
              "version": "1.2"
          }
      },
      "params": {
          "dataSetId": "65004470082ac828d2c3d6a0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 데이터 레이크에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `6b137bf6-d2a0-48c8-914b-d50f4942eb85`입니다. |
| `data.format` | 수집할 [!DNL Oracle NetSuite Activities] 데이터의 형식입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |

**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 이후 단계에서 필수입니다.

```json
{
    "id": "382fc614-3c5b-46b9-a971-786fb0ae6c5d",
    "etag": "\"e0016100-0000-0200-0000-655707a40000\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다. 요청 페이로드 내에 정의된 데이터 매핑을 사용하여 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)에 대한 POST 요청을 수행하면 됩니다.

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

다음 요청은 [!DNL DNL NetSuite Activities]에 대한 매핑을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/b156e6f818f923e048199173c45e55e20fd2487f5eb03d22",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.id",
            "destination": "_extconndev.NSA_ID"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.title",
            "destination": "_extconndev.NSA_title"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.createddate",
            "destination": "_extconndev.NSA_createddate"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.location",
            "destination": "_extconndev.NSA_location"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "items.lastmodifieddate",
            "destination": "_extconndev.NSA_lastmodifieddate"
        }
      ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `outputSchema.schemaRef.id` | 이전 단계에서 생성된 [대상 XDM 스키마](#target-schema)의 ID입니다. |
| `mappings.sourceType` | 매핑되는 소스 속성 유형입니다. |
| `mappings.source` | 대상 XDM 경로에 매핑해야 하는 소스 속성입니다. |
| `mappings.destination` | 소스 속성이 매핑되는 대상 XDM 경로. |

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "ddf0592bcc9d4ac391803f15f2429f87",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 플로우 만들기 {#flow}

[!DNL Oracle NetSuite Activities]에서 Experience Platform으로 데이터를 가져오는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

* [Source 연결 ID](#source-connection)
* [대상 연결 ID](#target-connection)
* [ID 매핑](#mapping)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle NetSuite Activities connector Flow Generic Rest",
    "description": "Oracle NetSuite Activities connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "d8827440-339f-428d-bf38-5e2ab1f0f7bb"
    ],
    "targetConnectionIds": [
        "e349a15e-c639-4047-8b2a-154aa7a857d7"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "10787532e0994eb686e76bdab69a9e88",
                "mappingVersion": 0
            }
        }
    ],
      "scheduleParams": {
          "startTime": 1700202649,
          "frequency": "once"
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
| `transformations` | 이 속성에는 데이터에 적용하는 데 필요한 다양한 변형이 포함되어 있습니다. 이 속성은 XDM 규격이 아닌 데이터를 Experience Platform으로 가져올 때 필요합니다. |
| `transformations.name` | 변환에 지정된 이름입니다. |
| `transformations.params.mappingId` | 이전 단계에서 생성된 [매핑 ID](#mapping)입니다. |
| `transformations.params.mappingVersion` | 매핑 ID의 해당 버전. 이 값은 기본적으로 `0`입니다. |
| `scheduleParams.startTime` | 이 속성은 데이터 흐름의 수집 예약에 대한 정보를 포함합니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대해 설명합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름 모니터링](../../monitor.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 업데이트

데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API의 `/flows` 끝점에 PATCH 요청을 수행하여 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트와 같은 데이터 흐름의 세부 정보를 업데이트합니다. PATCH 요청을 할 때는 `If-Match` 헤더에 데이터 흐름의 고유한 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름을 업데이트하는 방법](../../update-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 업데이트

기본 연결 ID를 쿼리 매개 변수로 제공하면서 [!DNL Flow Service] API에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. PATCH을 요청할 때 `If-Match` 헤더에 소스 계정의 고유 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 계정을 업데이트하는 방법](../../update.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 삭제

쿼리 매개 변수의 일부로 삭제할 데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. 전체 API 예제는 [API를 사용하여 데이터 흐름 삭제](../../delete-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 삭제

삭제할 계정의 기본 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. 전체 API 예제는 [API를 사용하여 소스 계정 삭제](../../delete.md)에 대한 안내서를 참조하십시오.
