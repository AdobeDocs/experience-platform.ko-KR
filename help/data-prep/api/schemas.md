---
keywords: Experience Platform;홈;인기 항목;데이터 준비;api 안내서;스키마;home;popular topics;data prepare;api guide;schemas;
solution: Experience Platform
title: 스키마 API 끝점
topic: 스키마
description: 'Adobe Experience Platform API의 ''/schemas'' 끝점을 사용하여 프로그래밍 방식으로 Mapper에서 사용할 스키마를 검색, 생성 및 업데이트할 수 있습니다. '
translation-type: tm+mt
source-git-commit: 435d27f7187074c78209948c0e57b610b63d2055
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 3%

---



# 스키마 끝점

Mapper에서 스키마를 사용하여 인제스트할 데이터가 Adobe Experience Platform에 있는지 확인합니다. `/schemas` 종단점을 사용하여 프로그래밍 방식으로 매퍼에 사용할 사용자 정의 스키마를 만들고 나열하고 가져올 수 있습니다.

>[!NOTE]
>
>이 끝점을 사용하여 만든 스키마는 매퍼 및 매핑 집합에만 사용됩니다. 다른 플랫폼 서비스에서 액세스할 수 있는 스키마를 만들려면 [스키마 레지스트리 개발자 안내서](../../xdm/api/schemas.md)를 참조하십시오.

## 모든 스키마 가져오기

IMS에 대해 사용 가능한 모든 매퍼 스키마 목록을 검색할 수 있습니다. 조직은 `/schemas` 끝점에 GET 요청을 수행하여 구성을 검색합니다.

**API 형식**

`/schemas` 끝점은 결과를 필터링하는 데 도움이 되는 여러 쿼리 매개 변수를 지원합니다. 이러한 매개 변수의 대부분은 선택 사항이지만 값비싼 오버헤드를 줄이려면 매개 변수를 사용하는 것이 좋습니다. 그러나 요청의 일부로 `start` 및 `limit` 매개 변수를 모두 포함해야 합니다. 여러 매개 변수를 앰퍼샌드(`&`)로 구분하여 포함할 수 있습니다.

```http
GET /schemas?limit={LIMIT}&start={START}
GET /schemas?limit={LIMIT}&start={START}&name={NAME}
GET /schemas?limit={LIMIT}&start={START}&orderBy={ORDER_BY}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{LIMIT}` | **필수 여부**. 반환된 스키마 수를 지정합니다. |
| `{START}` | **필수 여부**. 결과 페이지의 오프셋을 지정합니다. 결과의 첫 페이지를 가져오려면 값을 `start=0`으로 설정합니다. |
| `{NAME}` | 이름을 기준으로 스키마를 필터링합니다. |
| `{ORDER_BY}` | 결과 순서를 정렬합니다. 지원되는 필드는 `modifiedDate` 및 `createdDate`입니다. 속성을 `+` 또는 `-`로 프리펜드하여 각각 오름차순이나 내림차순으로 정렬할 수 있습니다. |

**요청**

다음 요청은 IMS 조직에 대해 마지막으로 두 개의 생성된 스키마를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas&start=0&limit=2 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 요청된 스키마 목록이 있는 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>다음 응답이 공간에 대해 잘렸습니다.

```json
{
    "data": [
        {
            "id": "823ac494f35e4e84bcb2f061378fcca6",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
                "contentType": "1.0"
            }
        },
        {
            "id": "0f868d3a1b804fb0abf738306290ae79",
            "version": 0,
            "jsonSchema": {
                "title": "Sample schema 2",
                "type": "object",
                "properties": {
                    "_id": {
                        "title": "Identifier",
                        "description": "A unique identifier for the record.",
                        "type": "string",
                        "format": "uri-reference",
                        "meta:xdmField": "@id",
                        "meta:xdmType": "string"
                    },
                    "city": {
                        "title": "City",
                        "description": "The name of the city.",
                        "type": "string",
                        "meta:xdmField": "xdm:city",
                        "meta:xdmType": "string"
                    }
                }
            },
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0f868d3a1b804fb0abf738306290ae79",
                "contentType": "1.0"
            }
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

## 스키마 만들기

`/schemas` 끝점에 POST 요청을 수행하여 유효성을 검사할 스키마를 만들 수 있습니다. 스키마를 만드는 방법은 다음과 같습니다.[JSON 스키마](https://json-schema.org/) 전송, 샘플 데이터 사용 또는 기존 XDM 스키마 참조

```http
POST /schemas
```

### JSON 스키마 사용

**요청**

다음 요청을 통해 [JSON 스키마](https://json-schema.org/)를 전송하여 스키마를 만들 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}'
```

**응답**

성공적인 응답은 새로 만든 스키마에 대한 정보가 있는 HTTP 상태 200을 반환합니다.

```json
{
    "id": "6daffabf14b1425292add3719afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

### 샘플 데이터 사용

**요청**

다음 요청을 통해 이전에 업로드한 샘플 데이터를 사용하여 스키마를 만들 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "sampleId": "45439a93d48d47d098d26e0f0840cc02"  
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `sampleId` | 스키마를 기준으로 하는 샘플 데이터의 ID. |

**응답**

성공적인 응답은 새로 만든 스키마에 대한 정보가 있는 HTTP 상태 200을 반환합니다.

```json
{
    "id": "b2ee78bd55ac45f781a93fb8b90d99b2",
    "version": 0,
    "jsonSchema": {
        "title": "SampleSchema:45439a93d48d47d098d26e0f0840cc02",
        "type": "object",
        "properties": {
            "gender": {
                "title": "gender",
                "type": "string"
            },
            "last_name": {
                "title": "last_name",
                "type": "string"
            },
            "id": {
                "title": "id",
                "type": "string"
            },
            "ip_address": {
                "title": "ip_address",
                "type": "string"
            },
            "first_name": {
                "title": "first_name",
                "type": "string"
            },
            "email": {
                "title": "email",
                "type": "string"
            }
        }
    },
    "sampleId": "45439a93d48d47d098d26e0f0840cc02"
}
```

### XDM 스키마 참조

**요청**

다음 요청을 통해 기존 XDM 스키마를 참조하여 스키마를 만들 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
 {
     "name": "outputSchema1",
     "schemaRef": {
         "id": "https://ns.adobe.com/{TENANT_ID}/schemas/0d555890502224d187b619f23c35c8d1",
         "contentType": "application/vnd.adobe.xed-full+json;version=1"
     }  
 }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 만들려는 스키마의 이름입니다. |
| `schemaRef.id` | 참조하는 스키마의 ID. |
| `schemaRef.contentType` | 참조된 스키마의 응답 형식을 결정합니다. 이 필드에 대한 자세한 내용은 [스키마 레지스트리 개발자 가이드](../../xdm/api/schemas.md#lookup)에서 확인할 수 있습니다. |

**응답**

성공적인 응답은 새로 만든 스키마에 대한 정보가 있는 HTTP 상태 200을 반환합니다.

>[!NOTE]
>
>다음 응답이 공간에 대해 잘렸습니다.

```json
{
    "id": "4b64daa51b774cb2ac21b61d80125ed0",
    "version": 0,
    "name": "schemaName",
    "jsonSchema": "{\"id\":null,\"schema\":null,\"_refId\":null,\"title\":\"SimpleUser\",...,\"imsOrg\":\"{IMS_ORG}\",\"$id\":\"https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96\"}",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/901c44cc5b2748488574f4e2824c5f96",
        "contentType": "application/vnd.adobe.xed+json;version=1.0"
    }
}
```

## 파일 업로드를 사용하여 스키마 만들기

변환할 JSON 파일을 업로드하여 스키마를 만들 수 있습니다.

**API 형식**

```http
POST /schemas/upload
```

**요청**

다음 요청을 통해 업로드된 JSON 파일에서 스키마를 만들 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/schemas/upload \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: multipart/form-data' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -F 'file=@{PATH_TO_FILE}.json'
```

**응답**

성공적인 응답은 새로 만든 스키마에 대한 정보가 있는 HTTP 상태 200을 반환합니다.

```json
{
    "id": "292add3716daffabf14b14259afc8fab",
    "version": 0,
    "jsonSchema": {
        "id": "string",
        "firstName": "string",
        "lastName": "string"
    }
}
```

## 특정 스키마 검색

`/schemas` 끝점에 GET 요청을 하고 요청 경로에서 검색할 스키마의 ID를 제공하여 특정 스키마에 대한 정보를 검색할 수 있습니다.

**API 형식**

```http
GET /schemas/{SCHEMA_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{SCHEMA_ID}` | 조회 중인 스키마의 ID. |

**요청**

다음 요청은 지정된 스키마에 대한 정보를 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/schemas/0f868d3a1b804fb0abf738306290ae79 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 스키마에 대한 정보가 있는 HTTP 상태 200을 반환합니다.

```json
{
    "id": "0f868d3a1b804fb0abf738306290ae79",
    "version": 0,
    "jsonSchema": {
        "title": "Sample schema",
        "description": "Sample description",
        "type": "object",
        "properties": {
            "_id": {
                "title": "Identifier",
                "description": "A unique identifier for the record.",
                "type": "string",
                "format": "uri-reference",
                "meta:xdmField": "@id",
                "meta:xdmType": "string"
            },
            "personalEmail": {
                "title": "Personal Email",
                "description": "A personal email address.",
                "type": "object",
                "properties": {
                    "primary": {
                        "title": "Primary",
                        "description": "Primary email indicator.\n\nA Profile can have only one `primary` email address at a given point of time.\n",
                        "type": "boolean",
                        "meta:xdmField": "xdm:primary",
                        "meta:xdmType": "boolean"
                    },
                    "address": {
                        "title": "Address",
                        "description": "The technical address, e.g 'name@domain.com' as commonly defined in RFC2822 and subsequent standards.",
                        "type": "string",
                        "format": "email",
                        "meta:xdmField": "xdm:address",
                        "meta:xdmType": "string"
                    }
                },
                "meta:xdmField": "xdm:personalEmail",
                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/emailaddress",
                "meta:xdmType": "object"
            }
        },
        "imsOrg": "6A29340459CA8D350A49413A@AdobeOrg",
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc"
    },
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/833b1d8a749943d49fe7e925ea19b5dc",
        "contentType": "1.0"
    }
}
```
