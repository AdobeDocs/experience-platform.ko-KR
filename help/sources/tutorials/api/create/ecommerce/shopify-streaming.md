---
title: Flow Service API를 사용하여 데이터를 배포할 스트리밍 소스 연결 및 데이터 흐름 만들기
description: Flow Service API를 사용하여 Shopify 데이터를 위한 스트리밍 소스 연결 및 데이터 흐름을 만드는 방법을 알아봅니다.
badge: Beta
exl-id: d44414a1-48fb-41e2-8cec-23cad867ba7d
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '1472'
ht-degree: 1%

---

# 에 대한 스트리밍 소스 연결 및 데이터 흐름 만들기 [!DNL Shopify] 흐름 서비스 API를 사용한 데이터

>[!NOTE]
>
>다음 [!DNL Shopify] 스트리밍 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

다음 자습서에서는 스트리밍 소스 연결 및 데이터 흐름을 만들어 데이터를 스트리밍하는 방법을 설명합니다 [[!DNL Shopify]](https://www.shopify.com/) 를 사용하여 Adobe Experience Platform에 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기 {#getting-started}

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 데이터를 다양한 소스에서 수집할 수 있으며 를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공할 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md).

## 스트림 [!DNL Shopify] Flow Service API를 사용하여 플랫폼에 데이터를 추가합니다

다음은 소스 연결 및 데이터 흐름을 만들어 데이터를 스트리밍하기 위해 수행해야 하는 절차에 대해 설명합니다 [!DNL Shopify] Platform으로 데이터를 전송할 수 있습니다.

### 소스 연결 만들기 {#source-connection}

에 POST 요청을 수행하여 소스 연결을 만듭니다. [!DNL Flow Service] API로, 소스의 연결 사양 ID를 제공하는 동안 이름, 설명 및 데이터 형식과 같은 세부 사항을 제공합니다.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은에 대한 소스 연결을 만듭니다 *YOURSOURCE*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Source Connection",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Shopify Streaming Source Connection",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID입니다. |
| `data.format` | 의 형식 [!DNL Shopify] 수집할 데이터입니다. 현재 지원되는 데이터 형식은 `json`. |

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 대상 XDM 스키마 만들기 {#target-schema}

Platform에서 소스 데이터를 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

대상 XDM 스키마는에 대한 POST 요청을 수행하여 만들 수 있습니다 [스키마 레지스트리 API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [api를 사용하여 스키마 만들기](../../../../../xdm/api/schemas.md).

### 대상 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 대상 데이터 세트를 만들 수 있습니다 [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공하는 것이 좋습니다.

대상 데이터 세트를 만드는 방법에 대한 자세한 단계는 다음 사항에 대한 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../../../catalog/api/create-dataset.md).

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크에 해당하는 고정 연결 사양 ID를 제공해야 합니다. 이 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 고유 식별자, 대상 스키마, 대상 데이터 세트 및 데이터 레이크에 대한 연결 사양 ID가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은에 대한 대상 연결을 만듭니다 [!DNL Shopify]:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Shopify Streaming Target Connection",
      "description": "Shopify Streaming Target Connection",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 을 사용하여 타겟 연결에 대한 정보를 조회할 수 있으므로 대상 연결의 이름이 설명적인지 확인합니다. |
| `description` | Target 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 데이터 레이크에 해당하는 연결 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 의 형식 [!DNL Shopify] Platform으로 가져올 데이터입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |


**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`). 이 ID는 이후 단계에서 필요합니다.

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다. 이것은 POST 요청을 수행하여에 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) (요청 페이로드 내에 정의된 데이터 매핑 사용)

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| 속성 | 설명 |
| --- | --- |
| `xdmSchema` | 의 ID입니다 [target XDM 스키마](#target-schema) 이전 단계에서 생성된 . |
| `mappings.destinationXdmPath` | 소스 속성이 매핑되는 대상 XDM 경로입니다. |
| `mappings.sourceAttribute` | 대상 XDM 경로에 매핑해야 하는 소스 속성입니다. |
| `mappings.identity` | 매핑 세트가 표시 여부를 지정하는 부울 값입니다 [!DNL Identity Service]. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 값은 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 흐름 만들기 {#flow}

에서 데이터를 가져오는 마지막 단계 [!DNL Shopify] 플랫폼 목표는 데이터 흐름을 만드는 것입니다. 현재까지는 다음 필수 값이 준비되었습니다.

* [소스 연결 ID](#source-connection)
* [Target 연결 ID](#target-connection)
* [ID 매핑](#mapping)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에서 이전에 언급된 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

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
      "name": "Shopify Streaming Dataflow",
      "description": "Shopify Streaming Dataflow",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름의 이름입니다. 데이터 흐름에서 정보를 조회하는 데 사용할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인합니다. |
| `description` | 데이터 플로우에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전입니다. 이 값의 기본값은 입니다. `1.0`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source-connection) 이전 단계에서 생성된 . |
| `targetConnectionIds` | 다음 [target 연결 ID](#target-connection) 이전 단계에서 생성된 . |
| `transformations` | 이 속성에는 데이터에 적용해야 하는 다양한 변형이 포함되어 있습니다. 이 속성은 XDM 규격 이외의 데이터를 Platform에 가져올 때 필요합니다. |
| `transformations.name` | 변환에 지정된 이름입니다. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 생성된 . |
| `transformations.params.mappingVersion` | 매핑 ID의 해당 버전입니다. 이 값의 기본값은 입니다. `0`. |

**응답**

성공적인 응답은 ID(`id`)을 만들 수 있습니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### 스트리밍 끝점 URL 가져오기

이제 데이터 흐름이 만들어지면 스트리밍 끝점 URL을 검색할 수 있습니다. 이 끝점 URL을 사용하여 소스를 웹 후크에 가입하여 소스가 Experience Platform과 통신할 수 있도록 합니다.

스트리밍 끝점 URL을 검색하려면 에 GET 요청을 수행하십시오 `/flows` 엔드포인트 및 데이터 흐름의 ID를 제공합니다.

**API 형식**

```http
GET /flows/{FLOW_ID}
```

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 끝점 URL을 다음으로 표시된 데이터 플로우에 대한 정보를 반환합니다 `inletUrl`.

```json
{
   "header":{
      "xactionId":"1658464615769:0062:161",
      "source":{
         "name":"shopify"
      },
      "sandboxId":"d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName":"prod",
      "originalTimestamp":1658464615770,
      "msgId":"1658464615769:0062:161",
      "msgVersion":"1.0",
      "traceContext":{
         "traceId":"ff3e7544618471eee6b934a4c5929d4e",
         "spanId":"74a759c5cc5f5a06",
         "isSampled":1.0
      },
      "_dcsMeta":{
         "inletId":"9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
         "authenticatedRequest":false,
         "debug":true
      }
   },
   "body":{
      "id":4135234371722,
      "admin_graphql_api_id":"gid://shopify/Order/4135234371722",
      "app_id":1354745,
      "browser_ip":null,
      "buyer_accepts_marketing":false,
      "cancel_reason":null,
      "cancelled_at":null,
      "cart_token":null,
      "checkout_id":21706716217482,
      "checkout_token":"b143503216124d50141fe0832fa3f4b0",
      "client_details":{
         "accept_language":null,
         "browser_height":null,
         "browser_ip":null,
         "browser_width":null,
         "session_hash":null,
         "user_agent":null
      },
      "closed_at":null,
      "confirmed":true,
      "contact_email":null,
      "created_at":"2022-07-22T00:36:48-04:00",
      "currency":"INR",
      "current_subtotal_price":"40000.00",
      "current_subtotal_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "current_total_discounts":"0.00",
      "current_total_discounts_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "current_total_duties_set":null,
      "current_total_price":"47200.00",
      "current_total_price_set":{
         "shop_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         }
      },
      "current_total_tax":"7200.00",
      "current_total_tax_set":{
         "shop_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         }
      },
      "customer_locale":null,
      "device_id":null,
      "discount_codes":[
          
      ],
      "email":"",
      "estimated_taxes":false,
      "financial_status":"paid",
      "fulfillment_status":null,
      "gateway":"manual",
      "landing_site":null,
      "landing_site_ref":null,
      "location_id":39129743498,
      "name":"#1005",
      "note":null,
      "note_attributes":[
          
      ],
      "number":5,
      "order_number":1005,
      "order_status_url":"https://connnectors-test.myshopify.com/31913214090/orders/ffd48198c78ef460177e44e22b19e6ab/authenticate?key=79a40d7da4b23d6a0beb2ba774f6ac83",
      "original_total_duties_set":null,
      "payment_gateway_names":[
         "manual"
      ],
      "phone":null,
      "presentment_currency":"INR",
      "processed_at":"2022-07-22T00:36:48-04:00",
      "processing_method":"manual",
      "reference":null,
      "referring_site":null,
      "source_identifier":null,
      "source_name":"shopify_draft_order",
      "source_url":null,
      "subtotal_price":"40000.00",
      "subtotal_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "tags":"",
      "tax_lines":[
         {
            "price":"7200.00",
            "rate":0.18,
            "title":"IGST",
            "price_set":{
               "shop_money":{
                  "amount":"7200.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"7200.00",
                  "currency_code":"INR"
               }
            },
            "channel_liable":false
         }
      ],
      "taxes_included":false,
      "test":false,
      "token":"ffd48198c78ef460177e44e22b19e6ab",
      "total_discounts":"0.00",
      "total_discounts_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "total_line_items_price":"40000.00",
      "total_line_items_price_set":{
         "shop_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"40000.00",
            "currency_code":"INR"
         }
      },
      "total_outstanding":"0.00",
      "total_price":"47200.00",
      "total_price_set":{
         "shop_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"47200.00",
            "currency_code":"INR"
         }
      },
      "total_price_usd":"589.95",
      "total_shipping_price_set":{
         "shop_money":{
            "amount":"0.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"0.00",
            "currency_code":"INR"
         }
      },
      "total_tax":"7200.00",
      "total_tax_set":{
         "shop_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         },
         "presentment_money":{
            "amount":"7200.00",
            "currency_code":"INR"
         }
      },
      "total_tip_received":"0.00",
      "total_weight":800,
      "updated_at":"2022-07-22T00:36:49-04:00",
      "user_id":44968935562,
      "discount_applications":[
          
      ],
      "fulfillments":[
          
      ],
      "line_items":[
         {
            "id":10630730743946,
            "admin_graphql_api_id":"gid://shopify/LineItem/10630730743946",
            "fulfillable_quantity":1,
            "fulfillment_service":"manual",
            "fulfillment_status":null,
            "gift_card":false,
            "grams":800,
            "name":"Mobile Phones",
            "origin_location":{
               "id":3141069111434,
               "country_code":"IN",
               "province_code":"UP",
               "name":"Noida",
               "address1":"Noida",
               "address2":"",
               "city":"Noida",
               "zip":"201301"
            },
            "price":"40000.00",
            "price_set":{
               "shop_money":{
                  "amount":"40000.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"40000.00",
                  "currency_code":"INR"
               }
            },
            "product_exists":true,
            "product_id":4525859963018,
            "properties":[
                
            ],
            "quantity":1,
            "requires_shipping":true,
            "sku":"",
            "taxable":true,
            "title":"Mobile Phones",
            "total_discount":"0.00",
            "total_discount_set":{
               "shop_money":{
                  "amount":"0.00",
                  "currency_code":"INR"
               },
               "presentment_money":{
                  "amount":"0.00",
                  "currency_code":"INR"
               }
            },
            "variant_id":32045196640394,
            "variant_inventory_management":"shopify",
            "variant_title":"",
            "vendor":"Connnectors Test",
            "tax_lines":[
               {
                  "channel_liable":false,
                  "price":"7200.00",
                  "price_set":{
                     "shop_money":{
                        "amount":"7200.00",
                        "currency_code":"INR"
                     },
                     "presentment_money":{
                        "amount":"7200.00",
                        "currency_code":"INR"
                     }
                  },
                  "rate":0.18,
                  "title":"IGST"
               }
            ],
            "duties":[
                
            ],
            "discount_allocations":[
                
            ]
         }
      ],
      "payment_terms":null,
      "refunds":[
          
      ],
      "shipping_lines":[
          
      ]
   }
}
```

## 부록

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제하는 데 사용할 수 있는 단계에 대한 정보를 제공합니다.

### 데이터 흐름 모니터링

데이터 흐름을 만든 후에는 데이터 흐름을 통해 수집 중인 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 소스 데이터 흐름 모니터링](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 데이터 흐름 업데이트

PATCH 요청을 수행하여 데이터 흐름의 세부 정보(예: 이름 및 설명, 실행 일정 및 관련 매핑 세트)를 업데이트합니다 `/flows` 의 끝점 [!DNL Flow Service] API, 데이터 흐름의 ID를 제공합니다. PATCH 요청을 만들 때 데이터 흐름의 고유한 정보를 제공해야 합니다 `etag` 에서 `If-Match` 헤더. 전체 API 예는 다음 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 업데이트](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 계정 업데이트

에 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다 [!DNL Flow Service] 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 API입니다. PATCH 요청을 만들 때 소스 계정의 고유한 `etag` 에서 `If-Match` 헤더. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 소스 계정 업데이트](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 데이터 흐름 삭제

에 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. [!DNL Flow Service] 삭제할 데이터 흐름의 ID를 쿼리 매개 변수의 일부로 제공하는 API입니다. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 데이터 흐름 삭제](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 계정 삭제

에 DELETE 요청을 수행하여 계정을 삭제합니다. [!DNL Flow Service] 삭제할 계정의 기본 연결 ID를 제공하는 동안 API가 제공됩니다. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 소스 계정 삭제](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).