---
title: CSV 템플릿으로 스키마 변환 API 엔드포인트
description: 스키마 레지스트리 API의 /rpc/csv2schema 종단점을 사용하면 CSV 템플릿을 사용하여 XDM(Experience Data Model) 스키마를 자동으로 만들 수 있습니다.
source-git-commit: 3860724b97987e555e12807c47f65fe040912d69
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 6%

---

# CSV 템플릿으로 스키마 변환 API 엔드포인트

다음 `/rpc/csv2schema` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 CSV 파일을 템플릿으로 사용하여 XDM(Experience Data Model) 스키마를 자동으로 만들 수 있습니다. 이 종단점을 사용하여 스키마 필드를 대량 가져오고 수동 API 또는 UI 작업을 줄이는 템플릿을 만들 수 있습니다.

## 시작하기

다음 `/rpc/csv2schema` 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

다음 `/rpc/csv2schema` 끝점은 RPC(원격 프로시저 호출)에서 지원하는 일부입니다 [!DNL Schema Registry]. 의 다른 종단점과 달리 [!DNL Schema Registry] API, RPC 끝점은 다음과 같은 추가 헤더가 필요하지 않습니다. `Accept` 또는 `Content-Type`, 및 를 사용하지 않음 `CONTAINER_ID`. 대신 를 사용해야 합니다 `/rpc` 네임스페이스에 대해 자세히 알아보십시오.

## CSV 파일 요구 사항

이 종단점을 사용하려면 먼저 적절한 열 헤더와 해당 값이 있는 CSV 파일을 만들어야 합니다. 일부 열이 필요하지만 나머지는 선택 사항입니다. 아래 표에서는 스키마 구성에서 이러한 열과 해당 역할에 대해 설명합니다.

| CSV 헤더 위치 | CSV 헤더 이름 | 필수/선택적 | 설명 |
| --- | --- | --- | --- |
| 1 | `isIgnored` | 선택 사항입니다 | 포함 및 을 로 설정한 경우 `true`: 필드가 API 업로드에 준비되지 않았으므로 무시해야 함을 나타냅니다. |
| 2 | `isCustom` | 필수 여부 | 필드가 사용자 지정 필드인지 여부를 나타냅니다. |
| 3 | `fieldGroupId` | 선택 사항입니다 | 사용자 지정 필드를 연결할 필드 그룹의 ID입니다. |
| 4 | `fieldGroupName` | (설명 참조) | 이 필드를 연결할 필드 그룹의 이름입니다.<br><br>기존 표준 필드를 확장하지 않는 사용자 지정 필드에 대한 선택 사항입니다. 비워 두면 자동으로 이름을 할당합니다.<br><br>표준 필드 또는 표준 필드 그룹을 확장하는 사용자 지정 필드에 필요합니다. 이 필드는 `fieldGroupId`. |
| 5 | `fieldPath` | 필수 여부 | 필드의 전체 XED 점 표기법 경로입니다. 표준 필드 그룹의 모든 필드를 포함하려면(아래에 표시된 대로) `fieldGroupName`) 값을 로 설정합니다. `ALL`. |
| 6 | `displayName` | 선택 사항입니다 | 필드의 제목 또는 친숙한 표시 이름입니다. 제목이 있는 경우 해당 제목의 별칭일 수도 있습니다. |
| 7 | `fieldDescription` | 선택 사항입니다 | 필드에 대한 설명입니다. 설명이 있을 경우 해당 설명의 별칭일 수도 있습니다. |
| 8 | `dataType` | (설명 참조) | 를 나타냅니다 [기본 데이터 유형](../schema/field-constraints.md#basic-types) 참조하십시오. 모든 사용자 지정 필드에 필요합니다.<br><br>If `dataType` 가 로 설정되어 있습니다. `object`, 다음 중 하나 `properties` 또는 `$ref` 동일한 행에 대해서도 정의해야 하지만 둘 다 정의되어 있지는 않습니다. |
| 9 | `isRequired` | 선택 사항입니다 | 필드가 데이터 처리에 필요한지 여부를 나타냅니다. |
| 10 | `isArray` | 선택 사항입니다 | 필드가 표시된 배열의 필드인지 여부를 나타냅니다 `dataType`. |
| 11 | `isIdentity` | 선택 사항입니다 | 필드가 ID 필드인지 여부를 나타냅니다. |
| 12 | `identityNamespace` | 필요한 경우 `isIdentity` true | 다음 [id 네임스페이스](../../identity-service/namespaces.md) ID 필드에 대해 을 참조하십시오. |
| 13 | `isPrimaryIdentity` | 선택 사항입니다 | 필드가 스키마의 기본 ID인지 여부를 나타냅니다. |
| 14 | `minimum` | 선택 사항입니다 | (숫자 필드만 해당) 필드의 최소값입니다. |
| 15 | `maximum` | 선택 사항입니다 | (숫자 필드만 해당) 필드의 최대 값입니다. |
| 16 | `enum` | 선택 사항입니다 | 배열(예: `[value1,value2,value3]`). |
| 17 | `stringPattern` | 선택 사항입니다 | (문자열 필드만 해당) 데이터 섭취 중 유효성 검사를 전달하려면 문자열 값이 일치해야 하는 정규 표현식 패턴입니다. |
| 18 | `format` | 선택 사항입니다 | (문자열 필드만 해당) 문자열 필드의 형식입니다. |
| 19 | `minLength` | 선택 사항입니다 | (문자열 필드만 해당) 문자열 필드의 최소 길이입니다. |
| 20 | `maxLength` | 선택 사항입니다 | (문자열 필드만 해당) 문자열 필드의 최대 길이입니다. |
| 21 | `properties` | (설명 참조) | 필요한 경우 `dataType` 가 로 설정되어 있습니다. `object` 및 `$ref` 가 정의되지 않았습니다. 개체 본문을 JSON 문자열(예: `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (설명 참조) | 필요한 경우 `dataType` 가 로 설정되어 있습니다. `object` 및 `properties` 가 정의되지 않았습니다. 이는 `$id` 객체 유형에 대해 참조된 객체(예: `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | 선택 사항입니다 | When `isIgnored` 가 로 설정되어 있습니다. `true`를 지정하는 경우, 이 열은 스키마의 헤더 정보를 제공하는 데 사용됩니다. |

{style=&quot;table-layout:auto&quot;}

다음을 참조하십시오 [CSV 템플릿](../assets/sample-csv-template.csv) csv 파일의 형식 지정 방법을 결정합니다.

## CSV 파일에서 내보내기 페이로드를 만듭니다

CSV 템플릿을 설정하고 나면 파일을 로 보낼 수 있습니다. `/rpc/csv2schema` 엔드포인트 및 내보내기 페이로드로 변환합니다.

**API 형식**

```http
POST /rpc/csv2schema
```

**요청**

요청 페이로드는 양식 데이터를 해당 형식으로 사용해야 합니다. 필수 양식 필드는 아래와 같습니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/csv2schema \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'csv-file=@"/Users/userName/Documents/sample-csv-template.csv"' \
  -F 'schema-class-id="https://ns.adobe.com/xdm/context/profile"' \
  -F 'schema-name="Example Schema"' \
  -F 'schema-description="Example schema description."'
```

| 속성 | 설명 |
| --- | --- |
| `csv-file` | 로컬 컴퓨터에 저장된 CSV 템플릿의 경로입니다. |
| `schema-class-id` | 다음 `$id` XDM [클래스](../schema/composition.md#class) 이 스키마에서 사용할 스키마. |
| `schema-name` | 스키마의 표시 이름입니다. |
| `schema-description` | 스키마에 대한 설명입니다. |

**응답**

성공적인 응답은 CSV 파일에서 생성된 내보내기 페이로드를 반환합니다. 페이로드는 배열 형식을 사용하며, 각 배열 항목은 스키마에 대한 종속 XDM 구성 요소를 나타내는 개체입니다. CSV 파일에서 생성된 내보내기 페이로드의 전체 예를 보려면 아래 섹션을 선택하십시오.

+++ 응답 페이로드 예

```json
[
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "description": "Generated field group 68397e9293a6904b3006311fb46c9573a8aaad49780dd65a",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "required": [
            "_ddgxdmint"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField1": {
                        "type": "string",
                        "title": "my custom field1",
                        "description": "Sample custom field1"
                    },
                    "customField2": {
                        "properties": {
                            "customerField22": {
                                "type": "string",
                                "title": "my custom field22",
                                "description": "Sample custom field22"
                            }
                        },
                        "type": "object",
                        "required": [
                            "customerField22"
                        ]
                    },
                    "customField3": {
                        "type": "number",
                        "title": "my custom field3",
                        "description": "Sample custom field3",
                        "minimum": 0,
                        "maximum": 10
                    },
                    "customField4": {
                        "type": "string",
                        "title": "my custom field4",
                        "description": "Sample custom field4",
                        "enum": [
                            "one",
                            "two",
                            "three"
                        ]
                    },
                    "customField5": {
                        "type": "array",
                        "title": "my custom field5",
                        "description": "Sample custom field5",
                        "items": {
                            "type": "string"
                        }
                    },
                    "customField6": {
                        "type": "string",
                        "title": "my custom field6",
                        "description": "Sample custom field6",
                        "format": "date"
                    }
                },
                "type": "object",
                "required": [
                    "customField1",
                    "customField2"
                ]
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "SampleFieldGroup",
        "description": "Generated field group 7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "properties": {
            "_ddgxdmint": {
                "properties": {
                    "customField7": {
                        "type": "object",
                        "title": "my custom field7",
                        "description": "Sample custom field7",
                        "properties": {
                            "myField": {
                                "type": "string"
                            }
                        }
                    },
                    "customField8": {
                        "type": "array",
                        "title": "my custom field8",
                        "description": "Sample custom field8",
                        "items": {
                            "type": "object",
                            "$ref": "https://ns.adobe.com/xdm/context/person"
                        }
                    }
                },
                "type": "object"
            }
        }
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Demographic Details:Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "description": "Generated field group 6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile-person-details"
        ],
        "allOf": [
            {
                "properties": {
                    "person": {
                        "properties": {
                            "name": {
                                "properties": {
                                    "_ddgxdmint": {
                                        "properties": {
                                            "nickName": {
                                                "type": "string"
                                            }
                                        },
                                        "type": "object",
                                        "required": [
                                            "nickName"
                                        ]
                                    }
                                },
                                "type": "object",
                                "required": [
                                    "_ddgxdmint"
                                ]
                            }
                        },
                        "type": "object",
                        "required": [
                            "name"
                        ]
                    }
                },
                "required": [
                    "person"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "mixins",
        "title": "Loyalty Details:Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "description": "Generated field group 39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241",
        "meta:intendedToExtend": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "meta:extends": [
            "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
        ],
        "allOf": [
            {
                "properties": {
                    "loyalty": {
                        "properties": {
                            "_ddgxdmint": {
                                "properties": {
                                    "joinDate": {
                                        "type": "string"
                                    }
                                },
                                "type": "object"
                            }
                        },
                        "type": "object"
                    }
                }
            },
            {
                "$ref": "https://ns.adobe.com/xdm/mixins/profile/profile-loyalty-details"
            }
        ]
    },
    {
        "$id": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "$schema": "http://json-schema.org/draft-06/schema#",
        "type": "object",
        "meta:xdmType": "object",
        "meta:resourceType": "schemas",
        "title": "My Sample Schema",
        "description": "My Sample Schema",
        "meta:extends": [
            "https://ns.adobe.com/xdm/context/profile"
        ],
        "allOf": [
            {
                "$ref": "https://ns.adobe.com/xdm/context/profile"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/68397e9293a6904b3006311fb46c9573a8aaad49780dd65a"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/7d4edf1a4c2b8c97d31f9931a10618e0b7341cefc97edad6"
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/6420020c79930a4c3aa7c9fd03b218e0e85c9a7d9990ecf",
                "meta:refProperty": [
                    "/person/name/firstName",
                    "/person/name/lastName",
                    "/person/name/_ddgxdmint/nickName"
                ]
            },
            {
                "$ref": "https://ns.adobe.com/ddgxdmint/mixins/39e6bb291e5b9072878c5c80c0ff5a325df79385ed10d241"
            }
        ]
    },
    {
        "@type": "xdm:alternateDisplayInfo",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/person/name/firstName",
        "xdm:title": {
            "en_us": "My first name"
        }
    },
    {
        "@type": "xdm:descriptorIdentity",
        "meta:resourceType": "descriptors",
        "xdm:sourceSchema": "https://ns.adobe.com/ddgxdmint/schemas/632cb76723ce2fd3876385168c03eb5201c5997f3f367a2f",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/_ddgxdmint/customField1",
        "xdm:namespace": "email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": true
    }
]
```

+++

## 스키마 페이로드 가져오기

CSV 파일에서 내보내기 페이로드를 생성한 후 해당 페이로드를 `/rpc/import` 스키마를 생성하기 위한 끝점입니다.

자세한 내용은 [끝점 가져오기 안내서](./import.md) 를 참조하십시오.
