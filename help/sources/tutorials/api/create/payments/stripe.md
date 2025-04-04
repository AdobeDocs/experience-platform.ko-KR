---
title: API를 사용하여  [!DNL Stripe] 계정의 결제 데이터를 Experience Platform으로 수집
description: 플로우 서비스 API를 사용하여 Stripe 계정에서 Experience Platform으로 결제 데이터를 수집하는 방법에 대해 알아봅니다
badge: Beta
exl-id: a9cb3ef6-aab0-4a5b-894e-ce90b82f35a8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 1%

---

# API를 사용하여 [!DNL Stripe] 계정에서 Experience Platform으로 결제 데이터 수집

>[!NOTE]
>
>[!DNL Stripe] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 소스 개요에서 [약관](../../../../home.md#terms-and-conditions)을 참조하십시오.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 [!DNL Stripe]에서 Adobe Experience Platform으로 결제 데이터를 수집하는 방법에 대해 알아보려면 다음 자습서를 읽어 보십시오.

## 시작하기

이 안내서를 사용하려면 Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### 인증

인증 자격 증명을 검색하는 방법에 대한 자세한 내용은 [[!DNL Stripe] 개요](../../../../connectors/payments/stripe.md)를 참조하십시오.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## Experience Platform에 [!DNL Stripe] 연결

[!DNL Stripe] 소스를 인증하고, 소스 연결을 만들고, 데이터 흐름을 만들어 결제 데이터를 Experience Platform으로 가져오는 방법을 알아보려면 아래 안내서를 따르십시오.

### 기본 연결 만들기 {#base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 Experience Platform 간에 정보를 유지합니다. 기본 연결 ID를 사용하여 소스 내에서 파일을 탐색하고 탐색할 수 있습니다. 또한 해당 항목의 데이터 유형 및 형식에 대한 세부 정보를 포함하여 수집하려는 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Stripe] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Stripe]에 대한 기본 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe base connection",
      "description": "Authenticated base connection for Stripe",
      "connectionSpec": {
          "id": "cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3",
          "version": "1.0"
      },
      "auth": {
          "specName": "OAuth2 Refresh Code",
          "params": {
            "accessToken": "{ACCESS_TOKEN}",
          }
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. 기본 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 기본 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 기본 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스의 연결 사양 ID입니다. [!DNL Stripe]의 연결 사양 ID는 `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`이며 이 ID는 고정되어 있습니다. |
| `auth.specName` | Experience Platform에 소스를 인증하기 위해 사용하는 인증 유형입니다. |
| `auth.params.accessToken` | [!DNL Stripe] 계정의 액세스 토큰입니다. 액세스 토큰을 검색하는 방법에 대한 단계는 [[!DNL Stripe] 인증 안내서](../../../../connectors/payments/stripe.md#prerequisites)를 참조하십시오. |

**응답**

성공한 응답은 고유 연결 식별자(`id`)를 포함하여 새로 만든 기본 연결을 반환합니다. 이 ID는 다음 단계에서 소스의 파일 구조 및 콘텐츠를 탐색하는 데 필요합니다.

```json
{
  "id": "a9950001-a386-4642-a0cd-5eaac6db5556",
  "etag": "\"dc01244d-0000-0200-0000-65ea4e500000\""
}
```

### 소스 탐색 {#explore}

기본 연결 ID가 있으면 이제 기본 연결 ID를 쿼리 매개 변수로 제공하면서 `/connections` 끝점에 대한 GET 요청을 수행하여 소스 데이터의 내용과 구조를 탐색할 수 있습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=rest&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&sourceParams={SOURCE_PARAMS}
```

**요청**

소스의 파일 구조 및 콘텐츠를 살펴보기 위해 GET 요청을 수행할 때 아래 표에 나열된 쿼리 매개 변수를 포함해야 합니다.

| 매개변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 이전 단계에서 생성된 기본 연결 ID입니다. |
| `objectType=rest` | 탐색하려는 오브젝트의 유형입니다. 이 값은 항상 `rest`(으)로 설정됩니다. |
| `{OBJECT}` | 이 매개 변수는 특정 디렉터리를 볼 때만 필요합니다. 해당 값은 탐색하려는 디렉터리의 경로를 나타냅니다. 이 원본의 값은 `json`입니다. |
| `fileType=json` | Experience Platform으로 가져올 파일의 파일 유형입니다. 현재 지원되는 파일 형식은 `json`뿐입니다. |
| `{PREVIEW}` | 연결 콘텐츠가 미리 보기를 지원하는지 여부를 정의하는 부울 값. |
| `{SOURCE_PARAMS}` | 탐색할 리소스 경로를 가리키는 [!DNL Base64-]인코딩된 문자열입니다. `{SOURCE_PARAMS}`에 대해 승인된 형식을 가져오려면 리소스 경로를 [!DNL Base64]로 인코딩해야 합니다. 예를 들어 `{"resourcePath":"charges"}`은(는) `eyJyZXNvdXJjZVBhdGgiOiJjaGFyZ2VzIn0%3D`(으)로 인코딩됩니다. 사용 가능한 리소스 경로 목록은 다음과 같습니다. <ul><li>`charges`</li><li>`subscriptions`</li><li>`refunds`</li><li>`balance_transactions`</li><li>`customers`</li><li>`prices`</li></ul> |

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/a9950001-a386-4642-a0cd-5eaac6db5556/explore?objectType=rest&object=json&fileType=json&preview=false&sourceParams=eyJyZXNvdXJjZVBhdGgiOiJjaGFyZ2VzIn0%3D' \
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
      "data": {
        "type": "object",
        "properties": {
          "balance_transaction": {},
          "billing_details": {
            "type": "object",
            "properties": {
              "address": {
                "type": "object",
                "properties": {
                  "country": {},
                  "city": {},
                  "state": {},
                  "postal_code": {},
                  "line2": {},
                  "line1": {}
                }
              },
              "phone": {},
              "name": {},
              "email": {}
            }
          },
          "metadata": {
            "type": "object",
            "properties": {}
          },
          "livemode": {
            "type": "boolean"
          },
          "radar_options": {
            "type": "object",
            "properties": {}
          },
          "destination": {},
          "description": {
            "type": "string"
          },
          "failure_message": {},
          "fraud_details": {
            "type": "object",
            "properties": {}
          },
          "source": {},
          "amount_refunded": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "statement_descriptor": {
            "type": "string"
          },
          "transfer_data": {},
          "receipt_url": {
            "type": "string"
          },
          "shipping": {},
          "review": {},
          "captured": {
            "type": "boolean"
          },
          "calculated_statement_descriptor": {
            "type": "string"
          },
          "currency": {
            "type": "string"
          },
          "refunded": {
            "type": "boolean"
          },
          "id": {
            "type": "string"
          },
          "outcome": {
            "type": "object",
            "properties": {
              "reason": {},
              "risk_level": {
                "type": "string"
              },
              "risk_score": {
                "type": "integer",
                "minimum": -9007199254740992,
                "maximum": 9007199254740991
              },
              "seller_message": {
                "type": "string"
              },
              "network_status": {
                "type": "string"
              },
              "type": {
                "type": "string"
              }
            }
          },
          "payment_method": {
            "type": "string"
          },
          "order": {},
          "dispute": {},
          "amount": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "disputed": {
            "type": "boolean"
          },
          "failure_code": {},
          "transfer_group": {},
          "on_behalf_of": {},
          "created": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "payment_method_details": {
            "type": "object",
            "properties": {
              "type": {
                "type": "string"
              },
              "card": {
                "type": "object",
                "properties": {
                  "country": {
                    "type": "string"
                  },
                  "last4": {
                    "type": "string"
                  },
                  "funding": {
                    "type": "string"
                  },
                  "mandate": {},
                  "wallet": {},
                  "exp_month": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "exp_year": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "overcapture": {
                    "type": "object",
                    "properties": {
                      "maximum_amount_capturable": {
                        "type": "integer",
                        "minimum": -9007199254740992,
                        "maximum": 9007199254740991
                      },
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "amount_authorized": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "network": {
                    "type": "string"
                  },
                  "network_token": {
                    "type": "object",
                    "properties": {
                      "used": {
                        "type": "boolean"
                      }
                    }
                  },
                  "incremental_authorization": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "checks": {
                    "type": "object",
                    "properties": {
                      "cvc_check": {
                        "type": "string"
                      },
                      "address_line1_check": {},
                      "address_postal_code_check": {}
                    }
                  },
                  "extended_authorization": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  },
                  "installments": {},
                  "capture_before": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                  },
                  "fingerprint": {
                    "type": "string"
                  },
                  "three_d_secure": {},
                  "brand": {
                    "type": "string"
                  },
                  "multicapture": {
                    "type": "object",
                    "properties": {
                      "status": {
                        "type": "string"
                      }
                    }
                  }
                }
              }
            }
          },
          "amount_captured": {
            "type": "integer",
            "minimum": -9007199254740992,
            "maximum": 9007199254740991
          },
          "source_transfer": {},
          "failure_balance_transaction": {},
          "receipt_number": {},
          "application": {},
          "receipt_email": {},
          "paid": {
            "type": "boolean"
          },
          "application_fee": {},
          "payment_intent": {
            "type": "string"
          },
          "invoice": {},
          "statement_descriptor_suffix": {},
          "application_fee_amount": {},
          "object": {
            "type": "string"
          },
          "customer": {
            "type": "string"
          },
          "status": {
            "type": "string"
          }
        }
      }
    }
  }
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

다음 요청은 [!DNL Stripe]에 대한 소스 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe Source Connection For Charges Data",
      "description": "Stripe source connection for charges data",
      "baseConnectionId": "a9950001-a386-4642-a0cd-5eaac6db5556",
      "connectionSpec": {
        "id": "cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3",
        "version": "1.0"
      },
      "data": {
        "format": "json"
      },
      "params": {
        "resourcePath": "charges"
      },
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 사용할 수 있으므로 소스 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `baseConnectionId` | [!DNL Stripe]의 기본 연결 ID. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID. |
| `data.format` | 수집할 [!DNL Stripe] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |

성공한 응답은 새로 만든 원본 연결의 고유 식별자(`id`)를 반환합니다. 이 ID는 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
  "id": "abbfac4e-202c-4e04-902d-6f73e9041068",
  "etag": "\"0a033818-0000-0200-0000-65ea5a770000\""
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

다음 요청은 [!DNL Stripe]에 대한 대상 연결을 만듭니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Stripe Target Connection For Charges Data",
      "description": "Stripe target connection for charges data",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "parquet_xdm",
          "schema": {
              "id": "https://ns.adobe.com/{ORG_ID}/schemas/5f76be8c4e4b847fdac13ca42aa6b596a89a5b91dea48b16",
              "version": "application/vnd.adobe.xed-full+json;version=1.3"
          }
      },
      "params": {
          "dataSetId": "65e622315f78042c9e8166e8"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 찾을 때 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인하십시오. |
| `description` | 대상 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 데이터 레이크에 해당하는 연결 사양 ID입니다. 이 고정 ID는 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다. |
| `data.format` | 수집할 [!DNL Stripe] 데이터의 형식입니다. |
| `params.dataSetId` | 대상 데이터 세트의 ID입니다. 이 ID는 [대상 데이터 집합을 만드는 중](#target-dataset)에 생성됩니다. |

**응답**

응답이 성공하면 새 대상 연결의 고유 식별자(`id`)가 반환됩니다. 이 ID는 이후 단계에서 필수입니다.

```json
{
  "id": "69879751-ba43-48df-8cd0-39d2bb76a5b8",
  "etag": "\"4b02ef5b-0000-0200-0000-65ea5f730000\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 타겟 데이터 세트에 수집하려면 먼저 타겟 데이터 세트가 준수하는 타겟 스키마에 매핑해야 합니다. 요청 페이로드 내에 정의된 데이터 매핑을 사용하여 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/)에 대한 POST 요청을 수행하면 됩니다.

**API 형식**

```http
POST /conversion/mappingSets
```

다음 요청은 [!DNL Stripe]에 대한 매핑을 만듭니다.

+++요청 예제를 보려면 선택

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
      "xdmSchema": "https://ns.adobe.com/exchangesandboxcharlie/schemas/5f76be8c4e4b847fdac13ca42aa6b596a89a5b91dea48b16",
      "xdmVersion": "1.0",
      },
      "mappings":[
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.id",
            "sourceAttribute":"data.id",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.refunded",
            "sourceAttribute":"data.refunded",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.disputed",
            "sourceAttribute":"data.disputed",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.last4",
            "sourceAttribute":"data.payment_method_details.card.last4",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.livemode",
            "sourceAttribute":"data.livemode",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.status",
            "sourceAttribute":"data.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.overcapture.maximum_amount_capturable",
            "sourceAttribute":"data.payment_method_details.card.overcapture.maximum_amount_capturable",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.receipt_url",
            "sourceAttribute":"data.receipt_url",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.fingerprint",
            "sourceAttribute":"data.payment_method_details.card.fingerprint",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_intent",
            "sourceAttribute":"data.payment_intent",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.overcapture.status",
            "sourceAttribute":"data.payment_method_details.card.overcapture.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.network_token.used",
            "sourceAttribute":"data.payment_method_details.card.network_token.used",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.funding",
            "sourceAttribute":"data.payment_method_details.card.funding",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount",
            "sourceAttribute":"data.amount",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.customer",
            "sourceAttribute":"data.customer",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.incremental_authorization.status",
            "sourceAttribute":"data.payment_method_details.card.incremental_authorization.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.multicapture.status",
            "sourceAttribute":"data.payment_method_details.card.multicapture.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount_captured",
            "sourceAttribute":"data.amount_captured",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method",
            "sourceAttribute":"data.payment_method",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.object",
            "sourceAttribute":"data.object",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.captured",
            "sourceAttribute":"data.captured",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.created",
            "sourceAttribute":"data.created",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.paid",
            "sourceAttribute":"data.paid",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.amount_refunded",
            "sourceAttribute":"data.amount_refunded",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.currency",
            "sourceAttribute":"data.currency",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.country",
            "sourceAttribute":"data.payment_method_details.card.country",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.exp_year",
            "sourceAttribute":"data.payment_method_details.card.exp_year",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.amount_authorized",
            "sourceAttribute":"data.payment_method_details.card.amount_authorized",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.network",
            "sourceAttribute":"data.payment_method_details.card.network",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details",
            "sourceAttribute":"data.payment_method_details",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.exp_month",
            "sourceAttribute":"data.payment_method_details.card.exp_month",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.calculated_statement_descriptor",
            "sourceAttribute":"data.calculated_statement_descriptor",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.brand",
            "sourceAttribute":"data.payment_method_details.card.brand",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.balance_transaction",
            "sourceAttribute":"data.balance_transaction",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.payment_method_details.card.extended_authorization.status",
            "sourceAttribute":"data.payment_method_details.card.extended_authorization.status",
            "identity":false,
            "version":0
        },
        {
            "destinationXdmPath":"_{ORG_ID}.charges_data.outcome",
            "sourceAttribute":"data.outcome",
            "identity":false,
            "version":0
        }
      ]
}
```


| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 대상 XDM 스키마의 ID입니다. 이 ID는 [대상 XDM 스키마](#target-schema)을(를) 만들어 생성합니다. |
| `destinationXdmPath` | 소스 속성이 매핑되는 XDM 필드. |
| `sourceAttribute` | 매핑 중인 소스 데이터 필드입니다. |
| `identity` | 필드가 [ID 서비스](../../../../../identity-service/home.md)에서 유지되는지 여부를 정의하는 부울 값입니다. |
| `version` | 사용 중인 매핑 버전입니다. |

+++

**응답**

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 매핑의 세부 정보를 반환합니다. 이 값은 데이터 흐름을 만들기 위해 이후 단계에서 필요합니다.

```json
{
  "id": "f4aad280fdec4770b7e33066945919d8",
  "version": 0,
  "createdDate": 1709860257007,
  "modifiedDate": 1709860257007,
  "createdBy": "{CREATED_BY}",
  "modifiedBy": "{MODIFIED_BY}"
}
```

### 플로우 만들기 {#flow}

[!DNL Stripe]에서 Experience Platform으로 데이터를 가져오는 마지막 단계는 데이터 흐름을 만드는 것입니다. 이제 다음 필수 값이 준비되었습니다.

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
    "name": "Stripe Connector Flow Generic Rest",
    "description": "Stripe Connector Description Flow Generic Rest",
    "flowSpec": {
        "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "abbfac4e-202c-4e04-902d-6f73e9041068"
    ],
    "targetConnectionIds": [
        "69879751-ba43-48df-8cd0-39d2bb76a5b8"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "f4aad280fdec4770b7e33066945919d8",
                "mappingVersion": 0
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1710267858",
        "frequency": "minute",
        "interval": {{interval}}
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
| `scheduleParams.startTime` | 데이터 흐름이 시작되는 시간입니다. Unix 타임스탬프 형식으로 시작 시간 값을 제공해야 합니다. |
| `scheduleParams.frequency` | 데이터 흐름이 데이터를 수집하는 빈도입니다. 수집 빈도를 다음과 같이 구성할 수 있습니다.  <ul><li>**한 번**: 빈도를 `once`(으)로 설정하여 일회성 수집을 만듭니다. 일회성 수집 데이터 흐름을 만들 때는 간격 및 채우기 구성을 사용할 수 없습니다. 기본적으로 예약 빈도는 한 번으로 설정됩니다.</li><li>**분**: 분 단위로 데이터를 수집하도록 데이터 흐름을 예약하려면 빈도를 `minute`(으)로 설정하십시오.</li><li>**시간**: 빈도를 `hour`(으)로 설정하여 시간당 기준으로 데이터를 수집하도록 데이터 흐름을 예약합니다.</li><li>**일**: 빈도를 `day`(으)로 설정하여 하루 단위로 데이터를 수집하도록 데이터 흐름을 예약합니다.</li><li>**주**: 주별로 데이터를 수집하도록 데이터 흐름을 예약하려면 빈도를 `week`(으)로 설정하십시오.</li></ul> |
| `scheduleParams.interval` | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 예를 들어 빈도를 일로 설정하고 간격을 15로 구성한 경우 데이터 흐름이 15일마다 실행됩니다. 간격 값은 0이 아닌 정수여야 합니다. 각 주파수에 대해 허용되는 최소 간격 값은 다음과 같습니다.<ul><li>**한 번**: 해당 없음</li><li>**분**: 15</li><li>**시간**: 1</li><li>**일**: 1</li><li>**주**: 1</li></ul> |

**응답**

성공한 응답은 새로 만든 데이터 흐름의 ID(`id`)를 반환합니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "84c64142-1741-4b0b-95a9-65644eba0cf6",
     "etag": "\"3901770b-0000-0200-0000-655708970000\""
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제하는 데 사용할 수 있는 단계에 대한 정보를 제공합니다.

### 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름 모니터링](../../monitor.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 업데이트

데이터 흐름의 ID를 제공하는 동안 [!DNL Flow Service] API의 /flows 끝점에 PATCH 요청을 만들어 데이터 흐름의 이름, 설명, 실행 일정 및 관련 매핑 세트와 같은 데이터 흐름의 세부 정보를 업데이트합니다. PATCH 요청을 할 때는 `If-Match` 헤더에 데이터 흐름의 고유한 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 데이터 흐름을 업데이트하는 방법](../../update-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 업데이트

기본 연결 ID를 쿼리 매개 변수로 제공하면서 [!DNL Flow Service] API에 대한 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다. PATCH을 요청할 때 `If-Match` 헤더에 소스 계정의 고유 `etag`을(를) 제공해야 합니다. 전체 API 예제는 [API를 사용하여 소스 계정을 업데이트하는 방법](../../update.md)에 대한 안내서를 참조하십시오.

### 데이터 흐름 삭제

쿼리 매개 변수의 일부로 삭제할 데이터 흐름의 ID를 제공하면서 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. 전체 API 예제는 [API를 사용하여 데이터 흐름 삭제](../../delete-dataflows.md)에 대한 안내서를 참조하십시오.

### 계정 삭제

삭제할 계정의 기본 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 대한 DELETE 요청을 수행하여 계정을 삭제합니다. 전체 API 예제는 [API를 사용하여 소스 계정 삭제](../../delete.md)에 대한 안내서를 참조하십시오.
