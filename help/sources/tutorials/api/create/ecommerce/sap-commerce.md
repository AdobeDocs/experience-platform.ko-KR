---
title: 흐름 서비스 API를 사용하여 SAP Commerce에 대한 소스 연결 및 데이터 흐름 만들기
description: 흐름 서비스 API를 사용하여 SAP Commerce 데이터를 Experience Platform 상태로 만들기 위해 소스 연결 및 데이터 흐름을 만드는 방법을 알아봅니다.
badge: Beta
exl-id: 580731b9-0c04-4f83-a475-c1890ac5b7cd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2314'
ht-degree: 1%

---

# 흐름 서비스 API를 사용하여 [!DNL SAP Commerce]에 대한 소스 연결 및 데이터 흐름을 만듭니다.

>[!NOTE]
>
>[!DNL SAP Commerce] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

다음 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [[!DNL SAP] 구독 청구](https://www.sap.com/products/financial-management/subscription-billing.html) 연락처 및 고객 데이터를 Adobe Experience Platform으로 가져오기 위해 [!DNL SAP Commerce] 소스 연결 및 데이터 흐름을 만드는 단계를 안내합니다.

## 시작하기

이 안내서를 사용하려면 다음 Experience Platform 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL SAP Commerce]에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL SAP Commerce]을(를) Experience Platform에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `clientId` | 서비스 키의 `clientId` 값입니다. |
| `clientSecret` | 서비스 키의 `clientSecret` 값입니다. |
| `tokenEndpoint` | 서비스 키의 `url` 값은 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`과(와) 비슷합니다. |
| `region` | 데이터 센터 위치. 영역이 `url`에 있으며 `eu10` 또는 `us10`과(와) 유사한 값을 갖습니다. 예를 들어 `url`이(가) `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`이면 `eu10`이(가) 필요합니다. |

이러한 자격 증명에 대한 자세한 내용은 [[!DNL SAP Commerce] 설명서](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html)를 참조하세요.

## [!DNL Flow Service] API를 사용하여 [!DNL SAP Commerce]을(를) 플랫폼에 연결

다음은 [!DNL SAP Commerce] 원본을 인증하고, 원본 연결을 만들고, 데이터 흐름을 만들어 계정과 연락처 데이터를 Experience Platform 상태로 만드는 데 필요한 단계를 간략하게 설명합니다.

### 기본 연결 만들기 {#base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL SAP Commerce] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL SAP Commerce]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce base connection",
      "description": "Authenticated base connection for SAP Commerce",
      "connectionSpec": {
          "id": "d8ee38de-7ae9-4058-9610-c79ce75f8e92",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params": {
              "region": "{REGION}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
              "tokenEndpoint": "{TOKEN_ENDPOINT}"
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
| `auth.params.region` | 데이터 센터 위치. 영역이 `url`에 있으며 `eu10` 또는 `us10`과(와) 유사한 값을 갖습니다. 예를 들어 `url`이(가) `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`이면 `eu10`이(가) 필요합니다. |
| `auth.params.clientId` | 서비스 키의 `clientId` 값입니다. |
| `auth.params.clientSecret` | 서비스 키의 `clientSecret` 값입니다. |
| `auth.params.tokenEndpoint` | 서비스 키의 `url` 값은 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`과(와) 비슷합니다. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
     "id": "5f6d6022-3f64-400c-ba01-d4010de2d8ff",
     "etag": "\"f8018de1-0000-0200-0000-6482d7210000\""
}
```

### 소스 탐색 {#explore}

기본 연결 ID가 있으면 이제 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 `/connections` 끝점에 대한 GET 요청을 수행하여 소스 데이터의 내용과 구조를 탐색할 수 있습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

소스의 파일 구조 및 컨텐츠를 탐색하기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `objectType=rest` | 탐색하려는 오브젝트의 유형입니다. 현재 이 값은 항상 `rest`(으)로 설정되어 있습니다. |
| `{OBJECT}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. 이 원본의 값은 `json`입니다. |
| `fileType=json` | Platform으로 가져올 파일의 파일 유형입니다. 현재 지원되는 파일 형식은 `json`뿐입니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | Platform으로 가져올 소스 파일의 매개 변수를 정의합니다. `{SOURCE_PARAMS}`에 대해 허용되는 형식 유형을 검색하려면 전체 문자열을 base64로 인코딩해야 합니다. <br> [!DNL SAP Commerce]이(가) 여러 API를 지원합니다. 활용하고 있는 오브젝트 유형에 따라 다음 중 하나를 전달하십시오. <ul><li>`customers`</li><li>`contacts`</li></ul> |

[!DNL SAP Commerce] 원본이 여러 API를 지원합니다. 보낼 요청을 활용하는 오브젝트 유형에 따라 다음과 같습니다.

>[!NOTE]
>
>더 나은 프레젠테이션을 위해 일부 응답 레코드가 잘렸습니다.

>[!BEGINTABS]

>[!TAB 고객]

+++요청

[!DNL SAP Commerce] 고객 API의 경우 `{SOURCE_PARAMS}`의 값이 `{"object_type":"customers"}`(으)로 전달됩니다. Base64로 인코딩하면 아래와 같이 `eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9`과(와) 같습니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImN1c3RvbWVycyJ9' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공적인 응답은 다음과 같은 JSON 구조를 반환합니다.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "addresses": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "isDefault": {
                            "type": "boolean"
                        },
                        "phone": {
                            "type": "string"
                        },
                        "city": {
                            "type": "string"
                        },
                        "street": {
                            "type": "string"
                        },
                        "postalCode": {
                            "type": "string"
                        },
                        "addressUUID": {
                            "type": "string"
                        },
                        "houseNumber": {
                            "type": "string"
                        },
                        "additionalAddressInfo": {
                            "type": "string"
                        },
                        "state": {
                            "type": "string"
                        },
                        "email": {
                            "type": "string"
                        }
                    }
                }
            },
            "customerNumber": {
                "type": "string"
            },
            "corporateInfo": {
                "type": "object",
                "properties": {}
            },
            "customReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "externalSystemId": {
                            "type": "string"
                        },
                        "externalId": {
                            "type": "string"
                        },
                        "externalIdTypeCode": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "customerType": {
                "type": "string"
            },
            "markets": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "country": {
                            "type": "string"
                        },
                        "salesArea": {
                            "type": "object",
                            "properties": {
                                "division": {
                                    "type": "string"
                                },
                                "distributionChannel": {
                                    "type": "string"
                                },
                                "salesOrganization": {
                                    "type": "string"
                                }
                            }
                        },
                        "priceType": {
                            "type": "string"
                        },
                        "active": {
                            "type": "boolean"
                        },
                        "currency": {
                            "type": "string"
                        },
                        "marketId": {
                            "type": "string"
                        }
                    }
                }
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            },
            "defaultAddress": {
                "type": "object",
                "properties": {
                    "country": {
                        "type": "string"
                    },
                    "isDefault": {
                        "type": "boolean"
                    },
                    "phone": {
                        "type": "string"
                    },
                    "city": {
                        "type": "string"
                    },
                    "street": {
                        "type": "string"
                    },
                    "postalCode": {
                        "type": "string"
                    },
                    "addressUUID": {
                        "type": "string"
                    },
                    "houseNumber": {
                        "type": "string"
                    },
                    "additionalAddressInfo": {
                        "type": "string"
                    },
                    "state": {
                        "type": "string"
                    },
                    "email": {
                        "type": "string"
                    }
                }
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "addresses": [
                {
                    "email": "user1@test.com",
                    "phone": "123456890",
                    "houseNumber": "123",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                    "isDefault": true
                }
            ],
            "customerNumber": "2863620303",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t090000",
                    "externalId": "1324566",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.499Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedAt": "2023-05-31T06:39:28.499Z",
            "defaultAddress": {
                "email": "user1@test.com",
                "phone": "123456890",
                "houseNumber": "123",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "ff871221-ab48-435c-b1f5-903db1c3cea2",
                "isDefault": true
            }
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "addresses": [
                {
                    "email": "user2@test.com",
                    "phone": "1234567899",
                    "houseNumber": "876",
                    "city": "New Orleans",
                    "state": "LA",
                    "postalCode": "700089",
                    "country": "US",
                    "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                    "isDefault": true
                }
            ],
            "customerNumber": "6776445404",
            "externalObjectReferences": [
                {
                    "externalSystemId": "t089999",
                    "externalId": "1324565",
                    "externalIdTypeCode": "201"
                }
            ],
            "createdAt": "2023-05-31T06:39:28.142Z",
            "customerType": "INDIVIDUAL",
            "markets": [
                {
                    "marketId": "US",
                    "active": true,
                    "currency": "USD",
                    "country": "US",
                    "salesArea": {
                        "salesOrganization": "SE10",
                        "distributionChannel": "00",
                        "division": "00"
                    },
                    "priceType": "Net"
                }
            ],
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b12345",
            "changedAt": "2023-05-31T06:39:28.142Z",
            "defaultAddress": {
                "email": "user2@test.com",
                "phone": "1234567899",
                "houseNumber": "876",
                "city": "New Orleans",
                "state": "LA",
                "postalCode": "700089",
                "country": "US",
                "addressUUID": "1cd039aa-5b86-4e46-8e37-9ef263332c6b",
                "isDefault": true
            }
        }
    ]
}
```

+++

>[!TAB 연락처]

+++요청

[!DNL SAP Commerce] 연락처 API의 경우 `{SOURCE_PARAMS}`의 값이 `{"object_type":"contacts"}`(으)로 전달됩니다. Base64로 인코딩하면 아래와 같이 `eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=`과(와) 같습니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/f5421911-6f6c-41c7-aafa-5d9d2ce51535/explore?objectType=rest&object=json&fileType=json&preview=true&sourceParams=eyJvYmplY3RfdHlwZSI6ImNvbnRhY3RzIn0=' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++응답

성공적인 응답은 다음과 같은 JSON 구조를 반환합니다.

```json
{
    "format": "hierarchical",
    "schema": {
        "type": "object",
        "properties": {
            "externalObjectReferences": {
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {}
                }
            },
            "personalInfo": {
                "type": "object",
                "properties": {
                    "firstName": {
                        "type": "string"
                    },
                    "lastName": {
                        "type": "string"
                    }
                }
            },
            "createdAt": {
                "type": "string"
            },
            "createdBy": {
                "type": "string"
            },
            "changedBy": {
                "type": "string"
            },
            "contactNumber": {
                "type": "string"
            },
            "changedAt": {
                "type": "string"
            }
        }
    },
    "data": [
        {
            "personalInfo": {
                "firstName": "Test 1",
                "lastName": "User 1"
            },
            "createdAt": "2023-05-31T13:33:52.689Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4365374130",
            "changedAt": "2023-05-31T13:33:52.689Z"
        },
        {
            "personalInfo": {
                "firstName": "Test 2",
                "lastName": "User 2"
            },
            "createdAt": "2023-05-31T13:33:52.37Z",
            "createdBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "changedBy": "sb-subscription-billing!b123456|revenue-cloud!b1234",
            "contactNumber": "4075431868",
            "changedAt": "2023-05-31T13:33:52.37Z"
        }
    ]
}
```

+++

>[!ENDTABS]

### 소스 연결 만들기 {#source-connection}

[!DNL Flow Service] API의 `/sourceConnections` 끝점에 대한 POST 요청을 수행하여 소스 연결을 만들 수 있습니다. 소스 연결은 연결 ID, 소스 데이터 파일에 대한 경로 및 연결 사양 ID로 구성됩니다.

**API 형식**

```https
POST /sourceConnections
```

활용 중인 오브젝트 유형에 따라 아래 탭에서 선택하십시오.

>[!BEGINTABS]

>[!TAB 고객]

+++요청

다음 요청은 [!DNL SAP Commerce] 고객 데이터에 대한 소스 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "customers"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | [!DNL SAP Commerce]의 기본 연결 ID. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 수집할 [!DNL SAP Commerce] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |
| `object_type` | [!DNL SAP Commerce]이(가) 여러 API를 지원합니다. 고객 API의 경우 `object_type` 매개 변수를 `customers`(으)로 설정해야 합니다. |
| `path` | 이 값은 `object_type`에 대해 선택한 값과 동일합니다. |

+++

+++응답

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!TAB 연락처]

+++요청

다음 요청은 [!DNL SAP Commerce] 연락처 데이터에 대한 원본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Source Connection",
      "description": "SAP Commerce Source Connection",
      "baseConnectionId": "f5421911-6f6c-41c7-aafa-5d9d2ce51535",
      "connectionSpec": {
          "id": "63d2b27b-69a5-45c9-a7fe-78148a25de3c",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "object_type": "contacts"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | [!DNL SAP Commerce]의 기본 연결 ID. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 수집할 [!DNL SAP Commerce] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |
| `object_type` | [!DNL SAP Commerce]이(가) 여러 API를 지원합니다. 연락처 API의 경우 `object_type` 매개 변수는 `contacts`(으)로 설정해야 합니다. |
| `path` | 이 값은 *`object_type`*&#x200B;에 대해 선택한 값과 동일합니다. |

+++

+++응답

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
    "id": "8f1fc72a-f562-4a1d-8597-85b5ca1b1cd3",
    "etag": "\"ed05f1e1-0000-0200-0000-6368b8710000\""
}
```

+++

>[!ENDTABS]

### 대상 XDM 스키마 만들기 {#target-schema}

소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

[스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)에 대한 POST 요청을 수행하여 대상 XDM 스키마를 만들 수 있습니다.

대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md#create-a-schema)에 대한 자습서를 참조하십시오.

### 타겟 데이터 세트 만들기 {#target-dataset}

[카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)에 대한 POST 요청을 수행하고 페이로드 내에 대상 스키마의 ID를 제공하여 대상 데이터 집합을 만들 수 있습니다.

대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오.

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크에 해당하는 고정 연결 사양 ID를 제공해야 합니다. 이 ID: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에 대한 고유 식별자, 대상 데이터 세트 및 데이터 레이크에 대한 연결 사양 ID가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] API를 사용하여 대상 연결을 만들어 인바운드 원본 데이터를 포함할 데이터 집합을 지정할 수 있습니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은 [!DNL SAP Commerce]에 대한 대상 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SAP Commerce Target Connection Generic Rest",
      "description": "SAP Commerce Target Connection Generic Rest",
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
          "dataSetId": "645923cd7aeeea1c06c5e92e"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 데이터 레이크에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `6b137bf6-d2a0-48c8-914b-d50f4942eb85`입니다. |
| `data.format` | 수집할 [!DNL SAP Commerce] 데이터의 형식입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |

**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 이후 단계에서 필수입니다.

```json
{
    "id": "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c",
    "etag": "\"db00c6dc-0000-0200-0000-6482d8280000\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다. 요청 페이로드 내에 정의된 데이터 매핑을 사용하여 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)에 대한 POST 요청을 수행하면 됩니다.

**API 형식**

```http
POST /conversion/mappingSets
```

>[!BEGINTABS]

>[!TAB 고객]

+++요청

다음 요청은 [!DNL SAP Commerce] 고객 API 데이터에 대한 매핑을 만듭니다.

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
            "source": "customerNumber",
            "destination": "_extconndev.customerNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customerType",
            "destination": "_extconndev.customerType"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].email",
            "destination": "_extconndev.addresses[*].email"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].city",
            "destination": "_extconndev.addresses[*].city"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "addresses[*].addressUUID",
            "destination": "_extconndev.addresses[*].addressUUID"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].id",
            "destination": "_extconndev.customReferences[*].id"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "customReferences[*].typeCode",
            "destination": "_extconndev.customReferences[*].typeCode"
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

+++

+++응답

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

+++

>[!TAB 연락처]

+++요청

다음 요청은 [!DNL SAP Commerce] 연락처 API 데이터에 대한 매핑을 만듭니다.

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
            "source": "contactNumber",
            "destination": "_extconndev.contactNumber"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "createdAt",
            "destination": "_extconndev.createdAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "changedAt",
            "destination": "_extconndev.changedAt"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.lastName",
            "destination": "_extconndev.personalInfo.lastName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "personalInfo.firstName",
            "destination": "_extconndev.personalInfo.firstName"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectRefereneces[*].externalSystemId",
            "destination": "_extconndev.externalObjectReferences[*].externalSystemId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalId",
            "destination": "_extconndev.externalObjectReferences[*].externalId"
        },
         {
            "sourceType": "ATTRIBUTE",
            "source": "externalObjectReferences[*].externalIdTypeCode",
            "destination": "_extconndev.externalObjectReferences[*].externalIdTypeCode"
        }
    ],
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/extconndev/schemas/325fd5394ba421246b05c0a3c2cd5efeec2131058a63d473",
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

+++

+++응답

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

+++

>[!ENDTABS]

### 플로우 만들기 {#flow}

[!DNL SAP Commerce]에서 플랫폼으로 데이터를 가져오는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

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
      "name": "SAP Commerce Connector Description Flow Generic Rest",
      "description": "SAP Commerce Connector Description Flow Generic Rest",
      "flowSpec": {
          "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "2ef2e831-f4f1-4363-a0f7-08b4ea347164"
      ],
      "targetConnectionIds": [
          "5b72a4b6-2fb8-4ca7-8ad8-4114a3063c5c"
      ],
      "transformations": [
          {
              "name": "Mapping",
              "params": {
                  "mappingId": "ddf0592bcc9d4ac391803f15f2429f87",
                  "mappingVersion": "0"
              }
          }
      ],
      "scheduleParams": {
          "startTime": "1625040887",
          "frequency": "once",
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
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 합니다. |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "fcd16140-81b4-422a-8f9a-eaa92796c4f4",
     "etag": "\"9200a171-0000-0200-0000-6368c1da0000\""
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
