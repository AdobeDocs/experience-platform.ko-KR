---
title: API 끝점 내보내기
description: 스키마 레지스트리 API의 /export 끝점을 사용하면 샌드박스 간에 XDM 리소스를 공유할 수 있습니다.
exl-id: 1dcbfa59-af98-4db5-b6f4-f848e5bf5e81
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---

# 엔드포인트 내보내기

[!DNL Schema Library] 내의 모든 리소스는 Adobe Experience Platform 내의 특정 샌드박스에 포함되어 있습니다. 경우에 따라 샌드박스와 조직 간에 XDM(Experience Data Model) 리소스를 공유할 수 있습니다. [!DNL Schema Registry] API의 `/rpc/export` 끝점을 사용하면 [!DNL Schema Library]의 모든 스키마, 스키마 필드 그룹 또는 데이터 형식에 대한 내보내기 페이로드를 생성한 다음 해당 페이로드를 사용하여 해당 리소스(및 모든 종속 리소스)를 [`/rpc/import` 끝점](./import.md)을 통해 대상 샌드박스 및 조직으로 가져올 수 있습니다.

## 시작하기

`/rpc/export` 끝점은 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

`/rpc/export` 끝점은 [!DNL Schema Registry]에서 지원하는 원격 프로시저 호출(RPC)의 일부입니다. [!DNL Schema Registry] API의 다른 끝점과 달리 RPC 끝점에는 `Accept` 또는 `Content-Type`과(와) 같은 추가 헤더가 필요하지 않으며 `CONTAINER_ID`을(를) 사용하지 않습니다. 대신 아래 API 호출에 나와 있는 대로 `/rpc` 네임스페이스를 사용해야 합니다.

## 리소스에 대한 내보내기 페이로드 생성 {#export}

[!DNL Schema Library]의 기존 스키마, 필드 그룹 또는 데이터 형식에 대해 `/export` 끝점에 GET 요청을 하여 경로에 리소스 ID를 제공하여 내보내기 페이로드를 생성할 수 있습니다.

**API 형식**

```http
GET /rpc/export/{RESOURCE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{RESOURCE_ID}` | 내보낼 XDM 리소스의 `meta:altId` 또는 URL 인코딩 `$id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 `Restaurant` 필드 그룹에 대한 내보내기 페이로드를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/export/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

**응답**

성공적인 응답은 대상 XDM 리소스 및 모든 종속 리소스를 나타내는 오브젝트 배열을 반환합니다. 이 예제에서 배열의 첫 번째 개체는 `Restaurant` 필드 그룹이 사용하는 테넌트에서 만든 `Property` 데이터 형식이며, 두 번째 개체는 `Restaurant` 필드 그룹 자체입니다. 그런 다음 이 페이로드를 사용하여 [리소스를 다른 샌드박스 또는 조직으로 가져오기](#import)할 수 있습니다.

리소스의 테넌트 ID의 모든 인스턴스가 `<XDM_TENANTID_PLACEHOLDER>`(으)로 대체됩니다. 그러면 스키마 레지스트리는 후속 가져오기 호출에서 보낸 위치에 따라 리소스에 올바른 테넌트 ID를 자동으로 적용할 수 있습니다.

```json
[
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.datatypes.fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
        "meta:resourceType": "datatypes",
        "version": "1.0",
        "title": "Property",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "properties": {
                    "propertyId": {
                        "title": "Property ID",
                        "description": "ID for a company-owned property.",
                        "type": "string",
                        "isRequired": false,
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.propertyId",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    },
                    "jurisdiction": {
                        "title": "Jurisdiction",
                        "description": "",
                        "type": "string",
                        "isRequired": false,
                        "enum": [
                            "NA",
                            "UK",
                            "EU"
                        ],
                        "meta:enum": {
                            "NA": "North America",
                            "UK": "United Kingdom",
                            "EU": "European Union"
                        },
                        "meta:ui": {
                            "ref": [
                                "schema://5fbc29ec292534000055dd55",
                                "#/definitions/customFields"
                            ],
                            "path": "{}._<XDM_TENANTID_PLACEHOLDER>{}.property{}.jurisdiction",
                            "editable": true,
                            "generateDate": 1606168175975
                        },
                        "meta:xdmType": "string"
                    }
                }
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    },
    {
        "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "meta:resourceType": "mixins",
        "version": "1.0",
        "title": "Restaurant",
        "type": "object",
        "description": "",
        "definitions": {
            "customFields": {
                "type": "object",
                "properties": {
                    "_<XDM_TENANTID_PLACEHOLDER>": {
                        "type": "object",
                        "properties": {
                            "capacity": {
                                "title": "Capacity",
                                "description": "Restaurant capacity",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "kitchen": {
                                "title": "Kitchen Style",
                                "description": "Style of kitchen",
                                "type": "string",
                                "isRequired": false,
                                "meta:xdmType": "string"
                            },
                            "rating": {
                                "title": "Rating",
                                "description": "",
                                "type": "integer",
                                "isRequired": false,
                                "meta:xdmType": "int"
                            },
                            "property": {
                                "title": "Property",
                                "description": "",
                                "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/datatypes/fc07162ee7ca8d18e074a3bb50c3938c76160bf6040e8495",
                                "type": "object",
                                "meta:xdmType": "object"
                            }
                        },
                        "meta:xdmType": "object"
                    }
                },
                "meta:xdmType": "object"
            }
        },
        "allOf": [
            {
                "$ref": "#/definitions/customFields",
                "type": "object",
                "meta:xdmType": "object"
            }
        ],
        "meta:extensible": true,
        "meta:abstract": true,
        "meta:intendedToExtend": [],
        "meta:xdmType": "object",
        "meta:sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "meta:sandboxType": "production"
    }
]
```

## 리소스 가져오기 {#import}

CSV 파일에서 내보내기 페이로드를 생성한 후 해당 페이로드를 `/rpc/import` 엔드포인트로 전송하여 스키마를 생성할 수 있습니다.

내보내기 페이로드에서 스키마를 생성하는 방법에 대한 자세한 내용은 [끝점 가져오기 안내서](./import.md)를 참조하십시오.
