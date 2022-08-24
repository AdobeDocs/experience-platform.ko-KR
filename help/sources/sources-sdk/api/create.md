---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: Flow Service API를 사용하여 새 연결 사양을 만듭니다
topic-legacy: tutorial
description: 다음 문서에서는 Flow Service API를 사용하여 연결 사양을 만들고 Self-Serve Sources를 통해 새 소스를 통합하는 방법에 대해 설명합니다.
exl-id: 0b0278f5-c64d-4802-a6b4-37557f714a97
source-git-commit: ae5bb475bca90b31d8eb7cf6b66d4d191d36ac5c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 를 사용하여 새 연결 사양을 만듭니다 [!DNL Flow Service] API

연결 사양은 소스의 구조를 나타냅니다. 소스 인증 요구 사항에 대한 정보를 포함하고, 소스 데이터를 탐색하고 검사할 수 있는 방법을 정의하며, 지정된 소스의 특성에 대한 정보를 제공합니다. 다음 `/connectionSpecs` 의 엔드포인트 [!DNL Flow Service] API를 사용하면 조직 내에서 연결 사양을 프로그래밍 방식으로 관리할 수 있습니다.

다음 문서에서는 [!DNL Flow Service] API를 사용하고 셀프서비스 소스(배치 SDK)를 통해 새 소스를 통합합니다.

## 시작하기

계속하기 전에 [시작 안내서](./getting-started.md) 관련 설명서에 대한 링크의 경우, 이 문서에서 샘플 API 호출을 읽는 안내서와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 제공합니다.

## 객체 수집

셀프 서비스 소스를 사용하여 새 배치 소스를 만들려면 먼저 Adobe과 조정하고, 비공개 Git 리포지토리를 요청하며, 소스의 레이블, 설명, 카테고리 및 아이콘에 대한 세부 사항에 대해 Adobe과 정렬해야 합니다.

제공되면 다음과 같이 개인 Git 리포지토리를 구성해야 합니다.

* 소스
   * {your_source}
      * 가공물
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 객체(파일 이름) | 설명 | 예 |
| --- | --- | --- |
| {your_source} | 소스의 이름입니다. 이 폴더에는 개인 Git 리포지토리 내에서 소스와 관련된 모든 아티팩트가 포함되어야 합니다. | `mailchimp-members` |
| {your_source}-category.txt | 소스가 속한 범주로 텍스트 파일로 서식이 지정됩니다. 셀프 서비스 소스(배치 SDK)에서 지원하는 사용 가능한 소스 카테고리 목록은 다음과 같습니다. <ul><li>광고</li><li>Analytics</li><li>동의 및 기본 설정</li><li>CRM</li><li>고객 성공</li><li>데이터베이스</li><li>eCommerce</li><li>마케팅 자동화</li><li>결제</li><li>프로토콜</li></ul> **참고**: 소스가 위의 카테고리에 맞지 않는다고 생각되면 Adobe 담당자에게 연락하여 상의하십시오. | `mailchimp-members-category.txt` 파일 내에서 다음과 같이 소스의 카테고리를 지정하십시오. `marketingAutomation`. |
| {your_source}-description.txt | 출처에 대한 간략한 설명. | [!DNL Mailchimp Members] 가져올 수 있는 마케팅 자동화 소스입니다 [!DNL Mailchimp Members] Experience Platform 데이터. |
| {your_source}-icon.svg | Experience Platform 소스 카탈로그에서 소스를 나타내는 데 사용할 이미지입니다. 이 아이콘은 SVG 파일이어야 합니다. |
| {your_source}-label.txt | Experience Platform 소스 카탈로그에 표시되는 소스의 이름입니다. | 메일 그룹 구성원 |
| {your_source}-connectionSpec.json | 소스의 연결 사양을 포함하는 JSON 파일입니다. 이 안내서를 완료할 때 연결 사양을 채울 것이므로 이 파일이 처음에 필요하지 않습니다. | `mailchimp-members-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>연결 사양의 테스트 기간 동안 키 값 대신 를 사용할 수 있습니다 `text` 연결 사양에서 참조할 수 있습니다.

개인 Git 리포지토리에 필요한 파일을 추가했으면 Adobe이 검토할 가져오기 요청(PR)을 만들어야 합니다. PR이 승인되고 병합되면 소스의 레이블, 설명 및 아이콘을 참조하기 위해 연결 사양에 사용할 수 있는 ID가 제공됩니다.

다음으로, 연결 사양을 구성하려면 아래 설명된 단계를 따릅니다. 고급 예약, 사용자 지정 스키마 또는 다양한 페이지 매김 유형과 같이 소스에 추가할 수 있는 다양한 기능에 대한 추가 지침은 [소스 사양 구성](../config/sourcespec.md).

## 연결 사양 템플릿 복사

필요한 가공물을 수집한 후에는 아래 연결 사양 템플릿을 복사하여 선택한 텍스트 편집기에 붙여넣은 다음 대괄호로 속성을 업데이트합니다 `{}` 을 참조하십시오.

```json
{
  "name": "generic-rest-extension",
  "type": "generic-rest",
  "description": "{DESCRIPTION}",
  "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
  "version": "1.0",
  "attributes": {
    "uiAttributes": {
      "apiFeatures": {
        "explorePaginationSupported": false
      }
    }
  },
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "clientId": {
            "description": "Client id of user account.",
            "type": "string"
          },
          "clientSecret": {
            "description": "Client secret of user account.",
            "type": "string",
            "format": "password"
          },
          "accessToken": {
            "description": "Access Token",
            "type": "string",
            "format": "password"
          },
          "refreshToken": {
            "description": "Refresh Token",
            "type": "string",
            "format": "password"
          },
          "expirationDate": {
            "description": "Date of token expiry.",
            "type": "string",
            "format": "date",
            "uiAttributes": {
              "hidden": true
            }
          },
          "accessTokenUrl": {
            "description": "Access token url to fetch access token.",
            "type": "string"
          },
          "requestParameterOverride": {
            "type": "object",
            "description": "Specify parameter to override.",
            "properties": {
              "accessTokenField": {
                "description": "Access token field name to override.",
                "type": "string"
              },
              "refreshTokenField": {
                "description": "Refresh token field name to override.",
                "type": "string"
              },
              "expireInField": {
                "description": "ExpireIn field name to override.",
                "type": "string"
              },
              "authenticationMethod": {
                "description": "Authentication method override.",
                "type": "string",
                "enum": [
                  "GET",
                  "POST"
                ]
              },
              "clientId": {
                "description": "ClientId field name override.",
                "type": "string"
              },
              "clientSecret": {
                "description": "ClientSecret field name override.",
                "type": "string"
              }
            }
          }
        },
        "required": [
          "host",
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
          "username": {
            "description": "Username to connect rest endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect rest endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "protocols"
        },
        "icon": {
          "key": "genericRestIcon"
        },
        "description": {
          "key": "genericRestDescription"
        },
        "label": {
          "key": "genericRestLabel"
        }
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "Http method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "query parameters in json format",
              "example": "{'key':'value','key1':'value1'} in JSON format"
            }
          },
          "required": [
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "header parameters in json format",
          "example": "{'user':'c26f50c88dc035610e6753f807e28e9','x-api-key':'apiKey'}"
        },
        "contentPath": {
          "type": "object",
          "description": "Params required for main collection content.",
          "properties": {
            "path": {
              "description": "path to main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "Params required for sub-array content.",
          "properties": {
            "path": {
              "description": "path to sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "rename root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "Params required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "Pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "number of records per page to fetch.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "pointer property name",
              "example": "pointer"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "Params required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
  "exploreSpec": {
    "name": "Resource",
    "type": "Resource",
    "requestSpec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object"
    },
    "responseSpec": {
      "$schema": "http: //json-schema.org/draft-07/schema#",
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
```

## 연결 사양 만들기 {#create}

연결 사양 템플릿을 획득하면 이제 소스에 해당하는 적절한 값을 입력하여 새 연결 사양 작성을 시작할 수 있습니다.

연결 사양은 세 개의 개별 부분으로 나눌 수 있습니다. 인증 사양, 소스 사양 및 탐색 사양입니다.

연결 사양의 각 부분의 값을 채우는 방법에 대한 지침은 다음 문서를 참조하십시오.

* [인증 사양 구성](../config/authspec.md)
* [소스 사양 구성](../config/sourcespec.md)
* [탐색 사양 구성](../config/explorespec.md)

사양명세 정보가 업데이트되면, POST 요청을 수행하여 새 연결 사양을 `/connectionSpecs` 의 끝점 [!DNL Flow Service] API.

**API 형식**

```http
POST /connectionSpecs
```

**요청**

다음 요청은 페이지에 대해 완전히 작성된 연결 사양의 예입니다 [!DNL MailChimp] 소스:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "MailChimp Members source",
      "description": "MailChimp Members source using generic-rest and SDK",
      "type": "generic-rest",
      "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
      "version": "1.0",
      "attributes": {
          "uiAttributes": {
              "apiFeatures": {
                  "explorePaginationSupported": false
              }
          }
      },
      "authSpec": [
          {
              "name": "OAuth2 Refresh Code",
              "type": "OAuth2RefreshCode",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                  "properties": {
                      "domain": {
                        "type": "string",
                        "description": "Enter domain name for host url"
                      },
                      "authorizationTestUrl": {
                          "description": "Authorization test url to validate accessToken.",
                          "type": "string"
                      },
                      "accessToken": {
                          "description": "Access Token of mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "domain",
                      "accessToken"
                  ]
              }
          },
          {
              "name": "Basic Authentication",
              "type": "BasicAuthentication",
              "spec": {
                  "$schema": "http://json-schema.org/draft-07/schema#",
                  "type": "object",
                  "description": "defines auth params required for connecting to rest service.",
                  "properties": {
                      "domain": {
                        "type": "string",
                        "description": "Enter domain name for host url"
                      },
                      "username": {
                          "description": "Username to connect mailChimp endpoint.",
                          "type": "string"
                      },
                      "password": {
                          "description": "Password to connect mailChimp endpoint.",
                          "type": "string",
                          "format": "password"
                      }
                  },
                  "required": [
                      "domain",
                      "username",
                      "password"
                  ]
              }
          }
      ],
      "sourceSpec": {
          "attributes": {
              "uiAttributes": {
                  "isSource": true,
                  "isPreview": true,
                  "isBeta": true,
                  "icon": {
                      "key": "mailchimpMembersIcon"
                  },
                  "description": {
                      "key": "mailchimpMembersDescription"
                  },
                  "label": {
                      "key": "mailchimpMembersLabel"
                  }
              },
              "urlParams": {
                  "host": "https://${domain}.api.mailchimp.com",
                  "path": "/3.0/lists/${listId}/members",
                  "method": "GET"
              },
              "contentPath": {
                  "path": "$.members",
                  "skipAttributes": [
                    "_links",
                    "total_items",
                    "list_id"
                  ],
                  "overrideWrapperAttribute": "member"
                },
              "paginationParams": {
                  "type": "OFFSET",
                  "limitName": "count",
                  "limitValue": "100",
                  "offSetName": "offset"
              },
              "scheduleParams": {
                  "scheduleStartParamName": "since_last_changed",
                  "scheduleEndParamName": "before_last_changed",
                  "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                  "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
              }
          },
          "spec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object",
              "description": "Define user input parameters to fetch resource values.",
              "properties": {
                  "listId": {
                      "type": "string",
                      "description": "listId for which members need to fetch."
                  }
              }
          }
      },
      "exploreSpec": {
          "name": "Resource",
          "type": "Resource",
          "requestSpec": {
              "$schema": "http://json-schema.org/draft-07/schema#",
              "type": "object"
          },
          "responseSpec": {
              "$schema": "http: //json-schema.org/draft-07/schema#",
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
  }'
```

**응답**

성공적인 응답은 해당 고유한 연결을 포함하여 새로 생성된 연결 사양을 반환합니다 `id`.

```json
{
    "id": "f6c0de0c-0a42-4cd9-9139-8768bf2f1b55",
    "createdAt": 1633388930134,
    "updatedAt": 1633388930134,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "imsOrgId": "{ORG_ID}",
    "name": "MailChimp Members source",
    "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
    "version": "1.0",
    "type": "generic-rest",
    "authSpec": [
        {
            "name": "OAuth2 Refresh Code",
            "type": "OAuth2RefreshCode",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path"
                    },
                    "authorizationTestUrl": {
                        "description": "Authorization test url to validate accessToken.",
                        "type": "string"
                    },
                    "accessToken": {
                        "description": "Access Token of mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "accessToken"
                ]
            }
        },
        {
            "name": "Basic Authentication",
            "type": "BasicAuthentication",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "description": "defines auth params required for connecting to rest service.",
                "properties": {
                    "host": {
                        "type": "string",
                        "description": "Enter resource url host path."
                    },
                    "username": {
                        "description": "Username to connect mailChimp endpoint.",
                        "type": "string"
                    },
                    "password": {
                        "description": "Password to connect mailChimp endpoint.",
                        "type": "string",
                        "format": "password"
                    }
                },
                "required": [
                    "host",
                    "username",
                    "password"
                ]
            }
        }
    ],
    "sourceSpec": {
        "spec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object",
            "description": "Define user input parameters to fetch resource values.",
            "properties": {
                "listId": {
                    "type": "string",
                    "description": "listId for which members need to fetch."
                }
            }
        },
        "attributes": {
            "uiAttributes": {
                "isSource": true,
                "isPreview": true,
                "isBeta": true,
                "icon": {
                    "key": "mailchimpMembersIcon"
                },
                "description": {
                    "key": "mailchimpMembersDescription"
                },
                "label": {
                    "key": "mailchimpMembersLabel"
                }
            },
            "urlParams": {
                "path": "/3.0/lists/${listId}/members",
                "method": "GET"
            },
            "contentPath": {
                    "path": "$.members",
                    "skipAttributes": [
                      "_links",
                      "total_items",
                      "list_id"
                    ],
                    "overrideWrapperAttribute": "member"
                  },
            "paginationParams": {
                "type": "OFFSET",
                "limitName": "count",
                "limitValue": "100",
                "offSetName": "offset"
            },
            "scheduleParams": {
                "scheduleStartParamName": "since_last_changed",
                "scheduleEndParamName": "before_last_changed",
                "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
                "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
            }
        }
    },
    "exploreSpec": {
        "name": "Resource",
        "type": "Resource",
        "requestSpec": {
            "$schema": "http://json-schema.org/draft-07/schema#",
            "type": "object"
        },
        "responseSpec": {
            "$schema": "http: //json-schema.org/draft-07/schema#",
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
    },
    "attributes": {
        "uiAttributes": {
            "apiFeatures": {
                "explorePaginationSupported": false
            }
        }
    }
}
```

## 다음 단계

새 연결 사양을 만들었으므로 이제 해당 연결 사양 ID를 기존 흐름 사양에 추가해야 합니다. 다음에서 자습서를 참조하십시오. [흐름 사양 업데이트](./update-flow-specs.md) 추가 정보.

생성한 연결 사양을 수정하려면 다음을 참조하십시오. [연결 사양 업데이트](./update-connection-specs.md).
