---
keywords: Experience Platform;홈;인기 항목;OneTrust
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 OneTrust 통합 소스에 대한 데이터 흐름 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 OneTrust 통합에 연결하는 방법을 알아봅니다.
exl-id: e224efe0-4756-4b8a-b446-a3e1066f2050
source-git-commit: 9846dc24321d7b32a110cfda9df3511b1e3a82ed
workflow-type: tm+mt
source-wordcount: '1961'
ht-degree: 1%

---

# 에 대한 데이터 흐름 만들기 [!DNL OneTrust Integration] 소스 사용 [!DNL Flow Service] API

>[!NOTE]
>
>다음 [!DNL OneTrust Integration] 소스는 쿠키가 아닌 동의 및 환경 설정 데이터 수집만 지원합니다.

다음 튜토리얼은 소스 연결 및 데이터 흐름을 만들어 기록 데이터와 예약된 동의 데이터를 모두 가져오는 단계를 안내합니다 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 를 사용하여 Adobe Experience Platform에 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 사전 요구 사항

>[!IMPORTANT]
>
>다음 [!DNL OneTrust Integration] 소스 커넥터 및 설명서는 [!DNL OneTrust Integration] 팀. 문의 사항이나 업데이트 요청은 다음 주소로 문의하십시오. [[!DNL OneTrust] 팀](https://my.onetrust.com/s/contactsupport?language=en_US) 직접.

연결하기 전에 [!DNL OneTrust Integration] 플랫폼으로 이동하려면 먼저 액세스 토큰을 검색해야 합니다. 액세스 토큰을 찾는 방법에 대한 자세한 지침은 [[!DNL OneTrust Integration] OAuth 2 안내서](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

액세스 토큰은 시스템 간 새로 고침 토큰이 지원되지 않으므로 만료된 후 자동으로 새로 고쳐지지 않습니다. [!DNL OneTrust]. 따라서 액세스 토큰이 만료되기 전에 연결에서 업데이트되었는지 확인해야 합니다. 액세스 토큰의 최대 구성 가능한 수명은 1년입니다. 액세스 토큰 업데이트에 대한 자세한 내용은 [[!DNL OneTrust] oauth 2.0 클라이언트 자격 증명 관리에 대한 문서](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

## 연결 [!DNL OneTrust Integration] 를 사용하여 플랫폼으로 [!DNL Flow Service] API

>[!NOTE]
>
>다음 [!DNL OneTrust Integration] API 사양이 데이터 수집을 위해 Adobe과 공유되고 있습니다.

다음 튜토리얼에서는 다음을 만드는 단계를 설명합니다. [!DNL OneTrust Integration] 소스 연결 및 가져올 데이터 흐름 만들기 [!DNL OneTrust Integration] 를 사용하여 데이터를 플랫폼에 전송 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### 기본 연결 만들기 {#base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL OneTrust Integration] 요청 본문의 일부인 인증 자격 증명입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST base connection",
      "description": "ONETRUST base connection to authenticate to Platform",
      "connectionSpec": {
          "id": "cf16d886-c627-4872-9936-fb08d6cba8cc",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
              "accessToken": "{ACCESS_TOKEN}"
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. 이 ID는 소스를 등록하고 를 통해 승인한 후에 검색할 수 있습니다. [!DNL Flow Service] API. |
| `auth.specName` | Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.` | API에 연결하기 위한 액세스 토큰을 포함하여 소스 인증에 필요한 자격 증명을 포함합니다. |
| `auth.params.accessToken` | 에 해당하는 액세스 토큰 [!DNL OneTrust Integration] 계정입니다. |

**응답**

성공한 응답은 고유 연결 식별자를 포함하여 새로 만든 기본 연결을 반환합니다(`id`). 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
     "id": "622124ca-6d18-47f7-999c-66f599955309",
     "etag": "\"2e026443-0000-0200-0000-621f1af80000\""
}
```

### 소스 탐색 {#explore}

이전 단계에서 생성한 기본 연결 ID를 사용하여 GET 요청을 수행하여 파일 및 디렉터리를 탐색할 수 있습니다.

다음 호출을 사용하여 가져올 파일의 경로를 찾습니다 [!DNL Platform]:

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

소스의 파일 구조 및 컨텐츠를 탐색하기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.


| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `objectType=rest` | 탐색하려는 오브젝트의 유형입니다. 현재 이 값은 항상 로 설정됩니다. `rest`. |
| `{OBJECT}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. |
| `fileType=json` | Platform으로 가져올 파일의 파일 유형입니다. 현재, `json` 는 유일하게 지원되는 파일 유형입니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/622124ca-6d18-47f7-999c-66f599955309/explore?objectType=rest&object=json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 쿼리된 파일의 구조를 반환합니다.

>[!NOTE]
>
>간결성을 위해 아래의 JSON 응답 페이로드가 숨겨집니다. 응답 페이로드를 보려면 나를 클릭합니다 를 선택합니다.

+++여기 클릭

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "number": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "size": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "numberOfElements": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
            },
            "last": {
                "type": "boolean"
            },
            "pageable": {
                "type": "object",
                "properties": {
                    "paged": {
                        "type": "boolean"
                    },
                    "pageNumber": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "offset": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "tokenId": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "limit": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "pageSize": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                    },
                    "unpaged": {
                        "type": "boolean"
                    },
                    "sort": {
                        "type": "object",
                        "properties": {
                            "unsorted": {
                                "type": "boolean"
                            },
                            "sorted": {
                                "type": "boolean"
                            },
                            "empty": {
                                "type": "boolean"
                            }
                        }
                    }
                }
            },
            "sort": {
                "type": "object",
                "properties": {
                    "unsorted": {
                        "type": "boolean"
                    },
                    "sorted": {
                        "type": "boolean"
                    },
                    "empty": {
                        "type": "boolean"
                    }
                }
            },
            "content": {
                "type": "object",
                "properties": {
                    "LastUpdatedDate": {
                        "type": "string"
                    },
                    "Identifier": {
                        "type": "string"
                    },
                    "Language": {
                        "type": "string"
                    },
                    "TestDataSubject": {
                        "type": "boolean"
                    },
                    "CreatedDate": {
                        "type": "string"
                    },
                    "DataElements": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {}
                        }
                    },
                    "Id": {
                        "type": "string"
                    },
                    "Purposes": {
                        "type": "array",
                        "items": {
                            "type": "object",
                            "properties": {
                                "Status": {
                                    "type": "string"
                                },
                                "LastTransactionDate": {
                                    "type": "string"
                                },
                                "CustomPreferences": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "properties": {}
                                    }
                                },
                                "LastUpdatedDate": {},
                                "ExpiryDate": {},
                                "Topics": {
                                    "type": "array",
                                    "items": {
                                        "type": "object",
                                        "properties": {
                                            "IsConsented": {
                                                "type": "boolean"
                                            },
                                            "Id": {
                                                "type": "string"
                                            },
                                            "Name": {
                                                "type": "string"
                                            }
                                        }
                                    }
                                },
                                "TotalTransactionCount": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "LastReceiptId": {},
                                "ConsentDate": {
                                    "type": "string"
                                },
                                "LastInteractionDate": {},
                                "Name": {
                                    "type": "string"
                                },
                                "FirstTransactionDate": {
                                    "type": "string"
                                },
                                "LastTransactionCollectionPointId": {
                                    "type": "string"
                                },
                                "LastTransactionCollectionPointVersion": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "Version": {
                                    "type": "integer",
                                    "minimum": -9007199254740992,
                                    "maximum": 9007199254740991
                                },
                                "attributes": {
                                    "type": "object",
                                    "properties": {}
                                },
                                "Id": {
                                    "type": "string"
                                },
                                "PurposeNote": {},
                                "WithdrawalDate": {
                                    "type": "string"
                                }
                            }
                        }
                    }
                }
            },
            "first": {
                "type": "boolean"
            },
            "empty": {
                "type": "boolean"
            }
        }
    },
    "data": [
        {
            "number": 0,
            "size": 100,
            "numberOfElements": 100,
            "last": false,
            "pageable": {
                "limit": 100,
                "offset": 0,
                "sort": {
                    "sorted": true,
                    "unsorted": false,
                    "empty": false
                },
                "tokenId": 100,
                "pageSize": 100,
                "pageNumber": 0,
                "unpaged": false,
                "paged": true
            },
            "sort": {
                "sorted": true,
                "unsorted": false,
                "empty": false
            },
            "content": {
                "Id": "de1ab4d2-6ccf-42bd-b363-2d8cac60c88c",
                "Language": "en-us",
                "Identifier": "gkumar@onetrust.com",
                "LastUpdatedDate": "2019-06-05T12:02:07Z",
                "CreatedDate": "2018-05-02T03:14:28Z",
                "Purposes": [
                    {
                        "Id": "9edf57bb-0449-4c15-98e4-8641522e5ff4",
                        "Name": "Purpose_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:14:27Z",
                        "LastTransactionDate": "2019-05-29T11:08:26Z",
                        "WithdrawalDate": "2019-05-29T11:05:30Z",
                        "ConsentDate": "2018-05-02T03:14:27Z",
                        "TotalTransactionCount": 5,
                        "Topics": [
                            {
                                "Id": "d6e3d675-3d6f-4f4e-a157-bd93829ee632",
                                "Name": "Topic_UAT",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "814c073a-95f1-4fc9-8263-1ec62225c5e9",
                        "Name": "Multi Pur_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:17:33Z",
                        "LastTransactionDate": "2018-05-02T03:19:49Z",
                        "ConsentDate": "2018-05-02T03:17:33Z",
                        "TotalTransactionCount": 4,
                        "LastTransactionCollectionPointId": "9a5b7375-bc13-47e8-8a58-1ca7d9c06c8e",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "4d52dcc4-82bf-44bf-ac49-854eba6ff8f3",
                        "Name": "Eloqua_UAT",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2018-05-02T03:26:36Z",
                        "LastTransactionDate": "2019-03-07T03:23:25Z",
                        "ConsentDate": "2018-05-02T03:26:36Z",
                        "TotalTransactionCount": 3,
                        "Topics": [
                            {
                                "Id": "690ad782-6280-4ea4-b62a-1514c39fc838",
                                "Name": "Eloqua_topic",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "f8886377-e4b1-45e4-b1c0-d7dacb744db8",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "723300e3-96cb-4da4-abdd-4913c05be215",
                        "Name": "Purpose 1",
                        "Version": 2,
                        "Status": "EXPIRED",
                        "FirstTransactionDate": "2019-02-27T06:29:48Z",
                        "LastTransactionDate": "2019-02-28T12:00:45Z",
                        "ConsentDate": "2019-02-27T06:29:48Z",
                        "ExpiryDate": "2019-02-28T12:00:45Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "3dbfb978-10f9-44a9-9669-d699674edd9d",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "4a5e6278-17f1-4283-beee-29f81cde2bd0",
                        "Name": "kbpurpose1",
                        "Version": 1,
                        "Status": "NO_CONSENT",
                        "FirstTransactionDate": "2019-03-07T03:21:58Z",
                        "LastTransactionDate": "2019-05-29T03:56:37Z",
                        "TotalTransactionCount": 6,
                        "LastTransactionCollectionPointId": "cea42a12-5de4-421a-b429-092e8d523948",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a36f98d0-c662-4f61-a2a1-8bdab69e3c3a",
                        "Name": "Pur 1",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-03-07T03:23:25Z",
                        "LastTransactionDate": "2019-03-07T03:23:27Z",
                        "ConsentDate": "2019-03-07T03:23:25Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "f8886377-e4b1-45e4-b1c0-d7dacb744db8",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "41ebdf32-068b-4239-89ac-42e20262c5a9",
                        "Name": "Send Notifications about Changes to Preferences",
                        "Version": 1,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-03-07T03:24:11Z",
                        "LastTransactionDate": "2019-03-07T03:27:29Z",
                        "ConsentDate": "2019-03-07T03:24:11Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "c29a99a9-de4d-4367-973b-95b0217d0640",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "759d8b24-e4c0-4107-86e2-3a408db13e6b",
                        "Name": "GJ Purpose 07",
                        "Version": 2,
                        "Status": "WITHDRAWN",
                        "FirstTransactionDate": "2019-03-07T03:27:29Z",
                        "LastTransactionDate": "2019-05-29T11:09:03Z",
                        "WithdrawalDate": "2019-05-29T11:09:03Z",
                        "ConsentDate": "2019-03-07T03:27:29Z",
                        "TotalTransactionCount": 18,
                        "LastTransactionCollectionPointId": "cea42a12-5de4-421a-b429-092e8d523948",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a57ee9da-b494-49e2-b562-6dfa31f190df",
                        "Name": "kbpurpose2",
                        "Version": 1,
                        "Status": "WITHDRAWN",
                        "FirstTransactionDate": "2019-03-28T03:23:44Z",
                        "LastTransactionDate": "2019-03-28T03:24:29Z",
                        "WithdrawalDate": "2019-03-28T03:24:29Z",
                        "ConsentDate": "2019-03-28T03:23:44Z",
                        "TotalTransactionCount": 2,
                        "LastTransactionCollectionPointId": "c29a99a9-de4d-4367-973b-95b0217d0640",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a1ccd810-94a0-4b58-946b-6705eae15c5b",
                        "Name": "Purpose01 v2",
                        "Version": 2,
                        "Status": "EXPIRED",
                        "FirstTransactionDate": "2019-05-29T04:05:42Z",
                        "LastTransactionDate": "2019-06-05T12:02:06Z",
                        "WithdrawalDate": "2019-05-29T11:09:12Z",
                        "ConsentDate": "2019-05-29T04:05:42Z",
                        "ExpiryDate": "2019-06-05T12:02:06Z",
                        "TotalTransactionCount": 8,
                        "Topics": [
                            {
                                "Id": "af7bf604-2058-4089-985c-c84083e3e3e3",
                                "Name": "New_Topic",
                                "IsConsented": true
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    },
                    {
                        "Id": "a313353a-e13b-4554-be08-22cf4a78a31c",
                        "Name": "Purpose_1804 v2",
                        "Version": 2,
                        "Status": "ACTIVE",
                        "FirstTransactionDate": "2019-05-29T04:05:42Z",
                        "LastTransactionDate": "2019-05-29T11:09:30Z",
                        "WithdrawalDate": "2019-05-29T11:05:30Z",
                        "ConsentDate": "2019-05-29T04:05:42Z",
                        "TotalTransactionCount": 4,
                        "CustomPreferences": [
                            {
                                "Id": "4935d35a-7216-480d-9da9-1aef0e078b89",
                                "Name": "Custom_S",
                                "Options": [
                                    {
                                        "Id": "8acc2f9f-37f8-4ace-a513-fae6b7dd0aa9",
                                        "Name": "Option2",
                                        "IsConsented": true
                                    }
                                ]
                            }
                        ],
                        "LastTransactionCollectionPointId": "735c85c8-c69c-44bc-8bad-ec0e806090bd",
                        "LastTransactionCollectionPointVersion": 1
                    }
                ],
                "TestDataSubject": false
            },
            "first": true,
            "empty": false
        }
    ]
}
```

+++

### 소스 연결 만들기 {#source-connection}

에 POST 요청을 하여 소스 연결을 만들 수 있습니다. [!DNL Flow Service] API. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은에 대한 소스 연결을 만듭니다. [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST Source Connection",
      "description": "ONETRUST Source Connection",
      "baseConnectionId": "622124ca-6d18-47f7-999c-66f599955309",
      "connectionSpec": {
          "id": "cf16d886-c627-4872-9936-fb08d6cba8cc",
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
| `baseConnectionId` | 의 기본 연결 ID [!DNL OneTrust Integration]. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 형식 [!DNL OneTrust Integration] 수집할 데이터. 현재 지원되는 데이터 형식은 `json`. |

**응답**

성공적인 응답은 고유 식별자()를 반환합니다.`id`)을 참조하십시오. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
     "id": "eb5833d3-230d-4700-80cc-bda396e7af8a",
     "etag": "\"da04c07f-0000-0200-0000-621f1afc0000\""
}
```

### 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

에 대한 POST 요청을 수행하여 대상 XDM 스키마를 생성할 수 있습니다. [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 다음 자습서를 참조하십시오. [api를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md).

### 타겟 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 타겟 데이터 세트를 생성할 수 있습니다. [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공합니다.

Target 데이터 세트를 만드는 방법에 대한 자세한 단계는 의 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../../../catalog/api/create-dataset.md).

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 다음에 해당하는 고정 연결 사양 ID를 제공해야 합니다. [!DNL Data Lake]. 이 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 연결 사양 ID가 있습니다. [!DNL Data Lake]. 이러한 식별자를 사용하여 다음을 사용하여 대상 연결을 만들 수 있습니다. [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은에 대한 대상 연결을 만듭니다. [!DNL OneTrust Integration] :

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ONETRUST Target Connection",
      "description": "ONETRUST Target Connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "dataSetId": "61f6ca3f33978c19486bb463"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 에 해당하는 연결 사양 ID [!DNL Data Lake]. 이 고정 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 형식 [!DNL OneTrust Integration] 플랫폼에 가져올 데이터입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

성공적인 응답은 새 타겟 연결의 고유 식별자( )를 반환합니다.`id`). 이 ID는 이후 단계에서 필수입니다.

```json
{
     "id": "495f761f-310a-4a7b-ae78-5b1152d74b38",
     "etag": "\"410a7b0c-0000-0200-0000-621f1afd0000\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다. 이에 대한 POST 요청을 수행함으로써 수행됩니다. [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) (요청 페이로드 내에 정의된 데이터 매핑 포함)

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/cfc8cee182e546c1fb35071185524b465e06bf1acb74f30d",
      "xdmVersion": "1.0",
      "id": null,
      "mappings": [{
              "sourceType": "ATTRIBUTE",
              "source": "content.Identifier",
              "destination": "_id",
              "name": "id",
              "description": "Identifier field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Identifier",
              "destination": "_exchangesandboxbravo.Identifier"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Language",
              "destination": "_exchangesandboxbravo.Language",
              "description": "Language field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.CreatedDate",
              "destination": "_exchangesandboxbravo.CreatedDate",
              "description": "Created Date field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.LastUpdatedDate",
              "destination": "_exchangesandboxbravo.LastUpdatedDate",
              "description": "Created Date field"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.DataElements",
              "destination": "_exchangesandboxbravo.DataElements"
          },
          {
              "sourceType": "ATTRIBUTE",
              "source": "content.Purposes",
              "destination": "_exchangesandboxbravo.Purposes"
          }

      ]
  }'
```

| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 의 ID [대상 XDM 스키마](#target-schema) 이전 단계에서 생성됩니다. |
| `mappings.destinationXdmPath` | 소스 속성이 매핑되는 대상 XDM 경로. |
| `mappings.sourceAttribute` | 대상 XDM 경로에 매핑해야 하는 소스 속성입니다. |

**응답**

성공적인 응답은 고유한 식별자( )를 포함하여 새로 생성된 매핑의 세부 정보를 반환합니다.`id`). 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "a87f130e82f04d5188da01f087805c4b",
    "version": 0,
    "createdDate": 1646205694395,
    "modifiedDate": 1646205694395,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 플로우 만들기 {#flow}

데이터 가져오기를 위한 마지막 단계 [!DNL OneTrust Integration] 를 플랫폼으로 가져와서 데이터 흐름을 만듭니다. 이제 다음 필수 값이 준비되었습니다.

* [소스 연결 ID](#source-connection)
* [Target 연결 ID](#target-connection)
* [ID 매핑](#mapping)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에 이전에 언급된 값을 제공하면서 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

수집을 예약하려면 먼저 시작 시간 값을 에포크 시간(초)으로 설정해야 합니다. 그런 다음 빈도 값을 다음 다섯 가지 옵션 중 하나로 설정해야 합니다. `once`, `minute`, `hour`, `day`, 또는 `week`. 간격 값은 두 개의 연속 수집 사이의 기간을 지정하지만, 일회성 수집을 만들 때는 간격을 설정할 필요가 없습니다. 다른 모든 주파수의 경우 간격 값이 보다 크거나 같게 설정되어야 합니다. `15`.

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
      "name": "ONETRUST dataflow",
      "description": "ONETRUST dataflow",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "eb5833d3-230d-4700-80cc-bda396e7af8a"
      ],
      "targetConnectionIds": [
          "495f761f-310a-4a7b-ae78-5b1152d74b38"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "a87f130e82f04d5188da01f087805c4b",
                  "mappingVersion": 0
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
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID: `6499120c-0b15-42dc-936e-847ea3c24d72`. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전. 이 값의 기본값은 입니다. `1.0`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source-connection) 이전 단계에서 생성됩니다. |
| `targetConnectionIds` | 다음 [대상 연결 ID](#target-connection) 이전 단계에서 생성됩니다. |
| `transformations` | 이 속성에는 데이터에 적용하는 데 필요한 다양한 변형이 포함되어 있습니다. 이 속성은 XDM 규격이 아닌 데이터를 Platform으로 가져올 때 필요합니다. |
| `transformations.name` | 변환에 지정된 이름입니다. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 생성됩니다. |
| `transformations.params.mappingVersion` | 매핑 ID의 해당 버전. 이 값의 기본값은 입니다. `0`. |
| `scheduleParams.startTime` | 이 속성은 데이터 흐름의 수집 예약에 대한 정보를 포함합니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 허용되는 값은 다음과 같습니다. `once`, `minute`, `hour`, `day`, 또는 `week`. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. 빈도를 로 설정하면 간격이 필요하지 않습니다. `once` 다음보다 크거나 같아야 합니다. `15` 다른 빈도 값의 경우. |

**응답**

성공적인 응답은 ID( )를 반환합니다.`id`)을 참조하십시오. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "70045189-42f0-493d-9b9e-be1045a9f4fa",
     "etag": "\"1601e900-0000-0200-0000-621f1b080000\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대해 설명합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 모니터링](../../monitor.md).

### 데이터 흐름 업데이트

에 PATCH 요청을 하여 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트 등 세부 정보를 업데이트합니다. `/flows` 엔드포인트 [!DNL Flow Service] API, 데이터 흐름의 ID 제공. PATCH 요청을 할 때는 데이터 흐름의 고유한 값을 제공해야 합니다 `etag` 다음에서 `If-Match` 머리글입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 업데이트](../../update-dataflows.md).

### 계정 업데이트

에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. [!DNL Flow Service] 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 API입니다. PATCH 요청을 할 때는 소스 계정의 고유한 이름을 제공해야 합니다 `etag` 다음에서 `If-Match` 머리글입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 계정 업데이트](../../update.md).

### 데이터 흐름 삭제

에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. [!DNL Flow Service] 쿼리 매개변수의 일부로 삭제할 데이터 흐름의 ID를 제공하는 동안 API입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 데이터 흐름 삭제](../../delete-dataflows.md).

### 계정 삭제

에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. [!DNL Flow Service] 삭제할 계정의 기본 연결 ID를 제공하는 동안 API입니다. 전체 API 예제는 의 안내서를 참조하십시오. [api를 사용하여 소스 계정 삭제](../../delete.md).