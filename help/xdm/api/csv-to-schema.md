---
title: CSV 템플릿에서 스키마 변환 API 엔드포인트로
description: 스키마 레지스트리 API의 /rpc/csv2schema 끝점을 사용하면 CSV 템플릿을 사용하여 XDM(경험 데이터 모델) 스키마를 자동으로 만들 수 있습니다.
exl-id: cf08774a-db94-4ea1-a22e-bb06385f8d0e
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 5%

---

# CSV 템플릿을 스키마 변환 API 엔드포인트로

다음 `/rpc/csv2schema` 의 엔드포인트 [!DNL Schema Registry] API를 사용하면 CSV 파일을 템플릿으로 사용하여 XDM(경험 데이터 모델) 스키마를 자동으로 만들 수 있습니다. 이 끝점을 사용하면 템플릿을 만들어 스키마 필드를 대량 가져오고 수동 API 또는 UI 작업을 줄일 수 있습니다.

## 시작하기

다음 `/rpc/csv2schema` 끝점이 의 일부임 [[!DNL Schema Registry] API](https://www.adobe.io/experience-platform-apis/references/schema-registry/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Adobe Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

다음 `/rpc/csv2schema` 끝점은 이 지원하는 원격 프로시저 호출(RPC)의 일부입니다. [!DNL Schema Registry]. 의 다른 끝점과 달리 [!DNL Schema Registry] API, RPC 끝점에는 다음과 같은 추가 헤더가 필요하지 않습니다. `Accept` 또는 `Content-Type`, 및 를 사용하지 않음 `CONTAINER_ID`. 대신 `/rpc` 아래 API 호출에 나와 있는 대로 네임스페이스.

## CSV 파일 요구 사항

이 끝점을 사용하려면 먼저 적절한 열 헤더와 해당 값이 있는 CSV 파일을 만들어야 합니다. 일부 열은 필수이고 나머지는 선택 사항입니다. 아래 표에서는 이러한 열과 스키마 구성에서 해당 역할에 대해 설명합니다.

| CSV 헤더 위치 | CSV 헤더 이름 | 필수/선택 사항 | 설명 |
| --- | --- | --- | --- |
| 1 | `isIgnored` | 선택 사항입니다 | 포함 시 로 설정 `true`는 필드가 API 업로드에 준비되지 않았으므로 무시해야 함을 나타냅니다. |
| 2 | `isCustom` | 필수 여부 | 필드가 사용자 정의 필드인지 여부를 나타냅니다. |
| 3 | `fieldGroupId` | 선택 사항입니다 | 사용자 정의 필드를 연결해야 하는 필드 그룹의 ID입니다. |
| 4 | `fieldGroupName` | (설명 참조) | 이 필드를 연결할 필드 그룹의 이름입니다.<br><br>기존 표준 필드를 확장하지 않는 사용자 정의 필드의 경우 선택 사항입니다. 비워 두면 이름이 자동으로 할당됩니다.<br><br>표준 필드 그룹을 확장하는 표준 필드 또는 사용자 정의 필드에 필요하며, 이 필드는 `fieldGroupId`. |
| 5 | `fieldPath` | 필수 여부 | 필드에 대한 전체 XED 점 표기법 경로. 표준 필드 그룹의 모든 필드를 포함하려면 다음을 수행합니다. `fieldGroupName`), 값을 로 설정합니다. `ALL`. |
| 6 | `displayName` | 선택 사항입니다 | 필드의 제목 또는 친숙한 표시 이름입니다. 제목이 있는 경우 제목의 별칭이 될 수도 있습니다. |
| 7 | `fieldDescription` | 선택 사항입니다 | 필드에 대한 설명입니다. 설명이 있는 경우 해당 설명의 별칭도 될 수 있습니다. |
| 8 | `dataType` | (설명 참조) | 다음을 나타냅니다. [기본 데이터 유형](../schema/field-constraints.md#basic-types) 필드용입니다. 모든 사용자 정의 필드에 필수입니다.<br><br>If `dataType` 이(가) (으)로 설정됨 `object`, 중 하나 `properties` 또는 `$ref` 동일한 행에 대해서도 정의해야 하지만 둘 다 정의해서는 안 됩니다. |
| 9 | `isRequired` | 선택 사항입니다 | 데이터 수집에 필드가 필요한지 여부를 나타냅니다. |
| 10 | `isArray` | 선택 사항입니다 | 필드가 표시된 배열인지 여부를 나타냅니다. `dataType`. |
| 11 | `isIdentity` | 선택 사항입니다 | 필드가 ID 필드인지 여부를 나타냅니다. |
| 12 | `identityNamespace` | 다음과 같은 경우 필수 `isIdentity` true임 | 다음 [id 네임스페이스](../../identity-service/features/namespaces.md) id 필드. |
| 13 | `isPrimaryIdentity` | 선택 사항입니다 | 필드가 스키마의 기본 ID인지 여부를 나타냅니다. |
| 14 | `minimum` | 선택 사항입니다 | (숫자 필드만 해당) 필드의 최소값입니다. |
| 15 | `maximum` | 선택 사항입니다 | (숫자 필드만 해당) 필드의 최대값입니다. |
| 16 | `enum` | 선택 사항입니다 | 필드에 대한 열거형 값 목록으로서, 배열로 표현됩니다(예: `[value1,value2,value3]`). |
| 17 | `stringPattern` | 선택 사항입니다 | (문자열 필드만 해당) 데이터 수집 중에 유효성 검사를 통과하기 위해 문자열 값이 일치해야 하는 정규 표현식 패턴입니다. |
| 18 | `format` | 선택 사항입니다 | (문자열 필드만 해당) 문자열 필드의 형식입니다. |
| 19 | `minLength` | 선택 사항입니다 | (문자열 필드만 해당) 문자열 필드의 최소 길이입니다. |
| 20 | `maxLength` | 선택 사항입니다 | (문자열 필드만 해당) 문자열 필드의 최대 길이입니다. |
| 21 | `properties` | (설명 참조) | 다음과 같은 경우 필수 `dataType` 이(가) (으)로 설정됨 `object` 및 `$ref` 가 정의되지 않았습니다. 오브젝트 본문을 JSON 문자열로 정의합니다(예: `{"myField": {"type": "string"}}`). |
| 22 | `$ref` | (설명 참조) | 다음과 같은 경우 필수 `dataType` 이(가) (으)로 설정됨 `object` 및 `properties` 가 정의되지 않았습니다. 다음을 정의합니다. `$id` 객체 유형에 대해 참조된 객체(예: `https://ns.adobe.com/xdm/context/person`). |
| 23 | `comment` | 선택 사항입니다 | 날짜 `isIgnored` 이(가) (으)로 설정됨 `true`, 이 열은 스키마의 헤더 정보를 제공하는 데 사용됩니다. |

{style="table-layout:auto"}

다음을 참조하십시오 [CSV 템플릿](../assets/sample-csv-template.csv) 를 사용하여 CSV 파일의 형식을 지정하는 방법을 결정합니다.

## CSV 파일에서 내보내기 페이로드 만들기

CSV 템플릿을 설정한 후에는 파일을 로 보낼 수 있습니다. `/rpc/csv2schema` 끝점을 지정하고 내보내기 페이로드로 변환합니다.

**API 형식**

```http
POST /rpc/csv2schema
```

**요청**

요청 페이로드는 양식 데이터를 해당 형식으로 사용해야 합니다. 필수 양식 필드가 아래에 표시되어 있습니다.

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
| `schema-class-id` | 다음 `$id` XDM의 [클래스](../schema/composition.md#class) 이 스키마에 사용될 것입니다. |
| `schema-name` | 스키마의 표시 이름입니다. |
| `schema-description` | 스키마에 대한 설명입니다. |

**응답**

성공적인 응답은 CSV 파일에서 생성된 내보내기 페이로드를 반환합니다. 페이로드는 배열의 형태를 취하며 각 배열 항목은 스키마에 대한 종속 XDM 구성 요소를 나타내는 개체입니다. CSV 파일에서 생성된 내보내기 페이로드의 전체 예를 보려면 아래 섹션을 선택하십시오.

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

CSV 파일에서 내보내기 페이로드를 생성한 후 해당 페이로드를 로 전송할 수 있습니다. `/rpc/import` 스키마를 생성할 끝점입니다.

다음을 참조하십시오. [끝점 가져오기 안내서](./import.md) 내보내기 페이로드에서 스키마를 생성하는 방법에 대한 자세한 내용
