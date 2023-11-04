---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 흐름 서비스 API를 사용하여 흐름 사양 업데이트
description: 다음 문서에서는 셀프 서비스 소스용 흐름 서비스 API(Batch SDK)를 사용하여 흐름 사양을 검색하고 업데이트하는 방법에 대한 단계를 설명합니다.
exl-id: 67a0cd3e-ac18-43a4-aa22-8f6376d5cc3f
source-git-commit: 21bccacf3555881ae731d0e60ff7d7677f18732d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# 를 사용하여 플로우 사양 업데이트 [!DNL Flow Service] API

새 연결 사양 ID를 생성한 후 데이터 흐름을 생성하려면 이 ID를 흐름 사양에 추가해야 합니다.

흐름 사양에는 흐름이 지원되는 소스 및 대상 연결 ID, 데이터에 적용해야 하는 변환 사양, 흐름을 생성하는 데 필요한 예약 매개 변수 등 흐름을 정의하는 정보가 포함됩니다. 다음을 사용하여 플로우 사양을 편집할 수 있습니다. `/flowSpecs` 엔드포인트.

다음 문서에서는 [!DNL Flow Service] 셀프 서비스 소스에 대한 API(일괄 처리 SDK).

## 시작하기

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크, 이 문서의 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 흐름 사양 조회 {#lookup}

소스 작성 `generic-rest-extension` 템플릿 모두 사용 `RestStorageToAEP` 흐름 사양. 에 GET 요청을 하여 이 흐름 사양을 검색할 수 있습니다. `/flowSpecs/` 끝점 및 제공 `flowSpec.id` / `6499120c-0b15-42dc-936e-847ea3c24d72`.

**API 형식**

```http
GET /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**요청**

다음 요청은 `6499120c-0b15-42dc-936e-847ea3c24d72` 연결 사양.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' 
```

**응답**

성공적인 응답은 질의된 플로우 사양의 상세내역을 반환합니다.

```json
{
  "items": [
      {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "createdAt": 1633080822911,
          "updatedAt": 1633080822911,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "{SANDBOX_ID}",
          "sandboxName": "{SANDBOX_NAME}",
          "imsOrgId": "{ORG_ID}",
          "name": "RestStorageToAEP",
          "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
          "version": "1.0",
          "sourceConnectionSpecIds": [
              "2d46966e-4fcc-4015-9f9e-a67594e395a3"
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
      },
  ]
}
```

## 플로우 사양 업데이트 {#update}

PUT 작업을 통해 연결 사양의 필드를 업데이트할 수 있습니다. PUT 요청을 통해 연결 사양을 업데이트할 때 본문에는 POST 요청에서 새 연결 사양을 만들 때 필요한 모든 필드가 포함되어야 합니다.

>[!IMPORTANT]
>
>다음 목록을 업데이트해야 합니다. `sourceConnectionSpecIds` 새 소스가 생성될 때마다 새 소스에 해당하는 흐름 사양 이렇게 하면 새 소스가 기존 플로우 사양에서 지원되므로 새 소스로 데이터 흐름 생성 프로세스를 완료할 수 있습니다.

**API 형식**

```http
PUT /flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72
```

**요청**

다음 요청은 의 흐름 사양을 업데이트합니다. `6499120c-0b15-42dc-936e-847ea3c24d72` 연결 사양 ID를 포함하려면 `f6c0de0c-0a42-4cd9-9139-8768bf2f1b55`.

```shell
PUT -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flowSpecs/6499120c-0b15-42dc-936e-847ea3c24d72' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
`     "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "name": "RestStorageToAEP",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
        "notification": {
          "category": "sources",
          "flowRun": {
            "enabled": true
          }
        }
      },
      "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
      ],
      "targetConnectionSpecIds": [
        "c604ff05-7f1a-43c0-8e18-33bf874cb11c"
      ],
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "EnterpriseSource",
            "permissions": [
              "write"
            ]
          }
        ]
      },
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
      "transformationSpec": [
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
        }
      ]
    }'
```

**응답**

성공적인 응답은 갱신된 목록을 포함하여 질의된 플로우 사양의 상세내역을 반환합니다. `sourceConnectionSpecIds`.

```json
{
    "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
    "updatedAt": 1633393222979,
    "updatedBy": "1633393222979",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "RestStorageToAEP",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "sourceConnectionSpecIds": [
        "4e98f16f-87d6-4ef0-bdc6-7a2b0fe76e62",
        "2e8580db-6489-4726-96de-e33f5f60295f",
        "c8ce8c8c-37fb-4162-9fbf-c2f181e04a7a",
        "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55"
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
```

## 다음 단계

새 연결 사양이 적절한 흐름 사양에 추가되면 이제 새 소스 테스트 및 제출로 진행할 수 있습니다. 다음 안내서를 참조하십시오 [새 소스 테스트 및 제출](./submit.md) 추가 정보.
