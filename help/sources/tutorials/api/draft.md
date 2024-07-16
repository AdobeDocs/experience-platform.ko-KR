---
title: 흐름 서비스 엔티티 API의 초안 만들기
description: 흐름 서비스 API를 사용하여 기본 연결, 소스 연결, 타겟 연결 및 데이터 흐름의 초안을 만드는 방법을 알아봅니다
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: ebd650355a5a4c2a949739384bfd5c8df9577075
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 3%

---

# API를 사용하여 [!DNL Flow Service] 엔터티의 초안 만들기

[[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)에서 `mode=draft` 쿼리 매개 변수를 사용하여 기본 연결, 소스 연결, 대상 연결 및 데이터 흐름과 같은 [!DNL Flow Service] 엔터티를 초안 상태로 설정할 수 있습니다.

`op=publish` 쿼리 매개 변수를 사용하여 나중에 새 정보로 초안을 업데이트한 다음 준비가 되면 게시할 수 있습니다.

이 자습서에서는 [!DNL Flow Service] 엔터티를 초안 상태로 설정하고 나중에 완료할 수 있도록 워크플로우를 일시 중지하고 저장하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 잘 알고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

### 초안 모드 지원 확인

사용 중인 소스의 연결 사양 ID 및 해당 흐름 사양 ID가 초안 모드에 대해 활성화되어 있는지도 확인해야 합니다.

>[!BEGINTABS]

>[!TAB 연결 사양 세부 정보 조회]

+++요청
다음 요청은 [!DNL Azure File Storage]에 대한 연결 사양 정보를 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be5ec48c-5b78-49d5-b8fa-7c89ec4569b8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공한 응답은 소스에 대한 연결 사양 정보를 반환합니다. 소스에 대해 초안 모드가 지원되는지 확인하려면 `items[0].attributes.isDraftModeSupported`의 값이 `true`인지 확인하십시오.

```json {line-numbers="true" start-line="1" highlight="252"}
{
    "items": [
        {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "name": "azure-file-storage",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "basicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "host": {
                                "type": "string",
                                "description": "Specifies the Azure File Storage endpoint."
                            },
                            "userid": {
                                "type": "string",
                                "description": "Specify the user to access the Azure File Storage."
                            },
                            "password": {
                                "type": "string",
                                "description": "Specify the storage access key",
                                "format": "password"
                            }
                        },
                        "required": [
                            "host",
                            "userid",
                            "password"
                        ]
                    }
                }
            ],
            "sourceSpec": {
                "name": "CloudStorage",
                "type": "CloudStorage",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "type": "string",
                            "description": "input path for copying files, can be a folder path, file path or a wildcard pattern"
                        },
                        "recursive": {
                            "type": "boolean",
                            "description": "indicates recursive copy in case of folder or wild card path, default is false"
                        }
                    },
                    "required": [
                        "path"
                    ]
                },
                "attributes": {
                    "uiAttributes": {
                        "documentationLink": "http://www.adobe.com/go/sources-azure-file-storage-en",
                        "isSource": true,
                        "category": {
                            "key": "cloudStorage"
                        },
                        "icon": {
                            "key": "azureFileStorage"
                        },
                        "description": {
                            "key": "azureFileStorageDescription"
                        },
                        "label": {
                            "key": "azureFileStorageLabel"
                        }
                    }
                }
            },
            "exploreSpec": {
                "name": "FileSystem",
                "type": "FileSystem",
                "requestSpec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "description": "defines explorable objects",
                    "properties": {
                        "objectType": {
                            "type": "string",
                            "enum": [
                                "file",
                                "folder",
                                "root"
                            ]
                        }
                    },
                    "allOf": [
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "file"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string",
                                        "description": "defines file to get schema or preview of."
                                    },
                                    "fileType": {
                                        "type": "string",
                                        "enum": [
                                            "delimited"
                                        ]
                                    },
                                    "preview": {
                                        "type": "boolean"
                                    }
                                },
                                "required": [
                                    "object",
                                    "fileType"
                                ]
                            }
                        },
                        {
                            "if": {
                                "properties": {
                                    "objectType": {
                                        "enum": [
                                            "folder"
                                        ]
                                    }
                                }
                            },
                            "then": {
                                "properties": {
                                    "object": {
                                        "type": "string"
                                    }
                                },
                                "required": [
                                    "object"
                                ]
                            }
                        }
                    ]
                },
                "responseSpec": {
                    "root": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "description": "lists tables/items under the database/container requested.",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string",
                                    "description": "defines type of an item."
                                },
                                "name": {
                                    "type": "string",
                                    "description": "defines display name of an item."
                                },
                                "path": {
                                    "type": "string",
                                    "description": "defines path of an item."
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether an item is previewable or not."
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false,
                                    "description": "defines whether schema can be fetched for an item or not."
                                }
                            }
                        }
                    },
                    "folder": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "type": {
                                    "type": "string"
                                },
                                "name": {
                                    "type": "string"
                                },
                                "path": {
                                    "type": "string"
                                },
                                "canPreview": {
                                    "type": "boolean",
                                    "default": false
                                },
                                "canFetchSchema": {
                                    "type": "boolean",
                                    "default": false
                                }
                            }
                        }
                    },
                    "file": {
                        "delimited": {
                            "$schema": "http://json-schema.org/draft-07/schema#",
                            "type": "object",
                            "properties": {
                                "format": {
                                    "type": "string"
                                },
                                "schema": {
                                    "type": "object",
                                    "properties": {
                                        "columns": {
                                            "type": "array",
                                            "items": {
                                                "type": "object",
                                                "properties": {
                                                    "name": {
                                                        "type": "string"
                                                    },
                                                    "type": {
                                                        "type": "string"
                                                    }
                                                }
                                            }
                                        }
                                    }
                                },
                                "data": {
                                    "type": "array",
                                    "items": {
                                        "type": "object"
                                    }
                                }
                            }
                        }
                    }
                }
            },
            "attributes": {
                "category": "Cloud Storage",
                "connectorName": "Azure File Storage",
                "isSource": true,
                "isDraftModeSupported": true,
                "uiAttributes": {
                    "apiFeatures": {
                        "explorePaginationSupported": false
                    }
                }
            },
            "permissionsInfo": {
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "write"
                        ]
                    }
                ],
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "EnterpriseSource",
                        "permissions": [
                            "read"
                        ]
                    }
                ]
            }
        }
    ]
}
```

+++

>[!TAB 흐름 사양 세부 정보 조회]

+++요청
다음 요청은 클라우드 스토리지 소스에 대한 플로우 사양 세부 정보를 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs?property=name==%22CloudStorageToAEP%22' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++응답

성공한 응답은 소스에 대한 흐름 사양 정보를 반환합니다. 소스에 대해 초안 모드가 지원되는지 확인하려면 `items[0].attributes.isDraftModeSupported`의 값이 `true`인지 확인하십시오.

```json {line-numbers="true" start-line="1" highlight="167"}
{
  "items": [
    {
      "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
      "name": "CloudStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "sourceConnectionSpecIds": [
        "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "ecadc60c-7455-4d87-84dc-2a0e293d997b",
        "b7829c2f-2eb0-4f49-a6ee-55e33008b629",
        "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
        "32e8f412-cdf7-464c-9885-78184cb113fd",
        "b7bf2577-4520-42c9-bae9-cad01560f7bc",
        "998b8ae3-cec0-43b7-8abe-40b1eb4ee069",
        "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
        "54e221aa-d342-4707-bcff-7a4bceef0001",
        "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
        "26f526f2-58f4-4712-961d-e41bf1ccc0e8"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "optionSpec": {
        "name": "OptionSpec",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "errorDiagnosticsEnabled": {
              "title": "Error diagnostics.",
              "description": "Flag to enable detailed and sample error diagnostics summary.",
              "type": "boolean",
              "default": false
            },
            "partialIngestionPercent": {
              "title": "Partial ingestion threshold.",
              "description": "Percentage which defines the threshold of errors allowed before the run is marked as failed.",
              "type": "number",
              "exclusiveMinimum": 0
            }
          }
        }
      },
      "transformationSpecs": [
        {
          "name": "Mapping",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for different mapping from source to target",
            "properties": {
              "mappingId": {
                "type": "string"
              },
              "mappingVersion": {
                "type": "string"
              }
            }
          }
        },
        {
          "name": "Encryption",
          "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "defines various params required for encrypted data ingestion",
            "properties": {
              "publicKeyId": {
                "type": "string",
                "description": "publicKeyId returned in encryptionKey creation API. One must use the publicKeyId corresponding to the same publicKey they used for encrypting the files"
              }
            }
          }
        }
      ],
      "scheduleSpec": {
        "name": "PeriodicSchedule",
        "type": "Periodic",
        "spec": {
          "$schema": "http://json-schema.org/draft-07/schema#",
          "type": "object",
          "properties": {
            "startTime": {
              "description": "epoch time",
              "type": "integer"
            },
            "frequency": {
              "type": "string",
              "enum": [
                "once",
                "minute",
                "hour",
                "day",
                "week"
              ]
            },
            "interval": {
              "type": "integer"
            },
            "backfill": {
              "type": "boolean",
              "default": true
            }
          },
          "required": [
            "startTime",
            "frequency"
          ],
          "if": {
            "properties": {
              "frequency": {
                "const": "once"
              }
            }
          },
          "then": {
            "allOf": [
              {
                "not": {
                  "required": [
                    "interval"
                  ]
                }
              },
              {
                "not": {
                  "required": [
                    "backfill"
                  ]
                }
              }
            ]
          },
          "else": {
            "required": [
              "interval"
            ],
            "if": {
              "properties": {
                "frequency": {
                  "const": "minute"
                }
              }
            },
            "then": {
              "properties": {
                "interval": {
                  "minimum": 15
                }
              }
            },
            "else": {
              "properties": {
                "interval": {
                  "minimum": 1
                }
              }
            }
          }
        }
      },
      "attributes": {
        "isSourceFlow": true,
        "flacValidationSupported": true,
        "isDraftModeSupported": true,
        "frequency": "batch",
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "permissionsInfo": {
        "manage": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "write"
            ]
          }
        ],
        "view": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "read"
            ]
          }
        ]
      }
    }
  ]
}
```

+++

>[!ENDTABS]



## 구배 베이스 연결 생성 {#create-a-draft-base-connection}

초안 기본 연결을 만들려면 [!DNL Flow Service] API의 `/connections` 끝점에 POST 요청을 하고 `mode=draft`을(를) 쿼리 매개 변수로 제공하십시오.

**API 형식**

```http
POST /connections?mode=draft
```

| 매개변수 | 설명 |
| --- | --- |
| `mode` | 기본 연결의 상태를 결정하는 사용자 제공 쿼리 매개 변수입니다. 기본 연결을 초안으로 설정하려면 `mode`을(를) `draft`(으)로 설정하십시오. |

**요청**

다음 요청은 [!DNL Azure File Storage] 소스에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "ACME Azure File Storage Base Connection",
        "description": "Azure File Storage base connection for ACME data (DRAFT)",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
      }'
```

**응답**

성공적인 응답은 기본 연결 ID와 초안 기본 연결에 대한 해당 etag를 반환합니다. 나중에 이 ID를 사용하여 기본 연결을 업데이트하고 게시할 수 있습니다.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 초안 기본 연결 Publish {#publish-your-draft-base-connection}

초안을 게시할 준비가 되면 `/connections` 끝점에 POST 요청을 만들고 게시할 초안 기본 연결의 ID와 게시를 위한 작업 작업을 제공합니다.

**API 형식**

```http
POST /connections/{BASE_CONNECTION_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `op` | 쿼리된 기본 연결의 상태를 업데이트하는 작업 작업입니다. 초안 기본 연결을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

**요청**

다음 요청은 이전 단계에서 만든 [!DNL Azure File Storage]에 대한 기본 연결 초안을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f9377f50-607a-4818-b77f-50607a181860/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공한 응답은 게시된 기본 연결에 대해 ID와 해당 etag를 반환합니다.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 초안 소스 연결 만들기 {#create-a-draft-source-connection}

초안 원본 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 끝점에 POST 요청을 하고 `mode=draft`을(를) 쿼리 매개 변수로 제공하십시오.

**API 형식**

```http
POST /sourceConnections?mode=draft
```

| 매개변수 | 설명 |
| --- | --- |
| `mode` | 소스 연결의 상태를 결정하는 사용자 제공 쿼리 매개 변수입니다. 원본 연결을 초안으로 설정하려면 `mode`을(를) `draft`(으)로 설정하십시오. |

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Source Connection",
      "description: "Azure File Storage source connection for ACME data (DRAFT)",
      "baseConnectionId": "f9377f50-607a-4818-b77f-50607a181860",
      "data": {
          "format": "delimited",
      },
      "params": {
          "path": "/acme/summerCampaign/account.csv",
          "type": "file"
      },
      "connectionSpec": {
          "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
          "version": "1.0"
      }
  }'
```

**응답**

성공적인 응답은 초안 소스 연결에 대해 소스 연결 ID와 해당 태그를 반환합니다. 나중에 이 ID를 사용하여 소스 연결을 업데이트하고 게시할 수 있습니다.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## 초안 소스 연결 Publish {#publish-your-draft-source-connection}

>[!NOTE]
>
>연관된 기본 연결이 여전히 초안 상태인 경우 소스 연결을 게시할 수 없습니다. 소스 연결을 게시하기 전에 기본 연결이 먼저 게시되었는지 확인하십시오.

초안을 게시할 준비가 되면 `/sourceConnections` 끝점에 POST 요청을 만들고 게시할 초안 원본 연결의 ID와 게시를 위한 작업 작업을 제공합니다.

**API 형식**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `op` | 쿼리된 소스 연결의 상태를 업데이트하는 작업 작업입니다. 초안 원본 연결을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

**요청**

다음 요청은 이전 단계에서 만든 [!DNL Azure File Storage]에 대한 초안 원본 연결을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/26b53912-1005-49f0-b539-12100559f0e2/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 게시된 소스 연결에 대한 ID 및 해당 etag를 반환합니다.

```json
{
    "id": "26b53912-1005-49f0-b539-12100559f0e2",
    "etag": "\"11004d97-0000-0200-0000-5f3c3b140000\""
}
```

## 초안 대상 연결 만들기 {#create-a-draft-target-connection}

초안 대상 연결을 만들려면 [!DNL Flow Service] API의 `/targetConnections` 끝점에 POST 요청을 하고 `mode=draft`을(를) 쿼리 매개 변수로 제공하십시오.

**API 형식**

```http
POST /targetConnections?mode=draft
```

| 매개변수 | 설명 |
| --- | --- |
| `mode` | 대상 연결의 상태를 결정하는 사용자 제공 쿼리 매개 변수입니다. 대상 연결을 초안으로 설정하려면 `mode`을(를) `draft`(으)로 설정하십시오. |

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "ACME Azure File Storage Target Connection",
      "description": "Azure File Storage target connection ACME data (DRAFT)",
      "data": {
          "schema": {
              "id": "{SCHEMA_ID}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{DATASET_ID}"
      },
          "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
  }'
```

**응답**

성공적인 응답은 대상 연결 ID와 초안 대상 연결에 대한 해당 etag를 반환합니다. 나중에 이 ID를 사용하여 대상 연결을 업데이트하고 게시할 수 있습니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 초안 대상 연결 Publish {#publish-your-draft-target-connection}

>[!NOTE]
>
>연관된 기본 연결이 여전히 초안 상태인 경우 대상 연결을 게시할 수 없습니다. 대상 연결을 게시하기 전에 기본 연결이 먼저 게시되었는지 확인하십시오.

초안을 게시할 준비가 되면 `/targetConnections` 끝점에 POST 요청을 만들고 게시하려는 초안 대상 연결의 ID와 게시를 위한 작업 작업을 제공합니다.

**API 형식**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `op` | 쿼리된 대상 연결의 상태를 업데이트하는 작업 작업입니다. 초안 대상 연결을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

**요청**

다음 요청은 이전 단계에서 만든 [!DNL Azure File Storage]에 대한 초안 대상 연결을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dbc5c132-bc2a-4625-85c1-32bc2a262558/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 게시된 타겟 연결에 대한 ID 및 해당 etag를 반환합니다.

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 초안 데이터 흐름 만들기 {#create-a-draft-dataflow}

데이터 흐름을 초안으로 설정하려면 `mode=draft`을(를) 쿼리 매개 변수로 추가하는 동안 `/flows` 끝점에 POST 요청을 하십시오. 이를 통해 데이터 흐름을 만들고 초안으로 저장할 수 있습니다.

**API 형식**

```http
POST /flows?mode=draft
```

| 매개변수 | 설명 |
| --- | --- |
| `mode` | 데이터 흐름의 상태를 결정하는 사용자 제공 쿼리 매개 변수입니다. 데이터 흐름을 초안으로 설정하려면 `mode`을(를) `draft`(으)로 설정하십시오. |

**요청**

다음 요청은 초안 데이터 흐름을 만듭니다.

```shell
  'https://platform.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "ACME Azure File Storage Dataflow",
    "description": "Azure File Storage dataflow for ACME data (DRAFT)",
    "sourceConnectionIds": [
        "26b53912-1005-49f0-b539-12100559f0e2"
    ],
    "targetConnectionIds": [
        "dbc5c132-bc2a-4625-85c1-32bc2a262558"
    ],
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    }
  }'
```

**응답**

성공적인 응답은 초안 데이터 흐름에 대한 흐름 ID와 해당 태그를 반환합니다. 나중에 이 ID를 사용하여 데이터 흐름을 업데이트하고 게시할 수 있습니다.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## 초안 데이터 흐름 Publish {#publish-your-draft-dataflow}

>[!NOTE]
>
>연결된 소스 및 타겟 연결이 여전히 초안 상태인 경우 데이터 흐름을 게시할 수 없습니다. 데이터 흐름을 게시하기 전에 소스 및 타겟 연결이 먼저 게시되었는지 확인하십시오.

초안을 게시할 준비가 되면 게시하려는 초안 데이터 흐름의 ID와 게시를 위한 작업 작업을 제공하면서 `/flows` 끝점에 POST 요청을 만듭니다.

**API 형식**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 매개변수 | 설명 |
| --- | --- |
| `op` | 쿼리된 데이터 흐름의 상태를 업데이트하는 작업 작업입니다. 초안 데이터 흐름을 게시하려면 `op`을(를) `publish`(으)로 설정하십시오. |

**요청**

다음 요청은 초안 데이터 흐름을 게시합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 ID와 데이터 흐름의 해당 `etag`을(를) 반환합니다.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

## 다음 단계

이 자습서를 통해 [!DNL Flow Service] 엔터티의 초안을 만들고 이러한 초안을 게시하는 방법을 배웠습니다. 소스에 대한 자세한 내용은 [ 소스 개요](../../home.md)를 참조하십시오.