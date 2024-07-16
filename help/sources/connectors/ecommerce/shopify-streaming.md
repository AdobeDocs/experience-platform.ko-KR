---
title: Shopify 스트리밍 Source
description: 소스 연결 및 데이터 흐름을 만들어 Shopify 인스턴스에서 Adobe Experience Platform으로 스트리밍 데이터를 수집하는 방법을 알아봅니다
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>[!DNL Shopify Streaming] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 스트리밍 공급자에 대한 지원에는 [!DNL Shopify]이(가) 포함됩니다.

## 전제 조건 {#prerequisites}

다음 단원에서는 [!DNL Shopify Streaming] 원본을 사용하기 전에 완료해야 하는 필수 조건 단계에 대해 설명합니다.

[!DNL Shopify] API에 연결하려면 유효한 [!DNL Shopify] 파트너 계정이 있어야 합니다. 파트너 계정이 아직 없는 경우 [[!DNL Shopify] 파트너 대시보드](https://www.shopify.com/partners)를 사용하여 등록하십시오.

### 애플리케이션 만들기

이제 올바른 [!DNL Shopify] 파트너 계정을 사용하여 파트너 대시보드를 사용하여 계속 진행하고 앱을 만들 수 있습니다. [!DNL Shopify]에서 앱을 만드는 방법에 대한 포괄적인 단계는 [[!DNL Shopify] 시작 가이드](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token)를 참조하십시오.

앱이 만들어지면 [!DNL Shopify] 파트너 대시보드의 **클라이언트 자격 증명** 탭에서 **클라이언트 ID** 및 **클라이언트 암호**&#x200B;를 검색합니다. 클라이언트 ID 및 클라이언트 암호는 다음 단계에서 인증 코드 및 액세스 토큰을 검색하는 데 사용됩니다.

### 인증 코드 검색

그런 다음 API 키, 범위 및 리디렉션 URI를 정의하는 쿼리 문자열과 함께 도메인의 `myshopify.com` URL을 브라우저에 입력하여 인증 코드를 검색합니다.

이 URL의 형식은 다음과 같습니다.

**API 형식**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 매개변수 | 설명 |
| --- | --- |
| `shop` | 하위 도메인 `myshopify.com` URL입니다. |
| `api_key` | [!DNL Shopify] 클라이언트 ID입니다. [!DNL Shopify] 파트너 대시보드의 **클라이언트 자격 증명** 탭에서 클라이언트 ID를 검색할 수 있습니다. |
| `scopes` | 정의할 액세스 유형입니다. 예를 들어 범위를 `scope=write_orders,read_customers`(으)로 설정하여 주문을 수정하고 고객을 읽을 수 있는 권한을 허용할 수 있습니다. |
| `redirect_uri` | 액세스 토큰을 생성할 스크립트의 URL입니다. |

**요청**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**응답**

성공적인 응답은 액세스 토큰을 생성하는 데 필요한 인증 코드를 포함하여 리디렉션 URL을 반환합니다.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### 액세스 토큰 검색

클라이언트 ID, 클라이언트 암호 및 인증 코드가 있으므로 액세스 토큰을 검색할 수 있습니다. 액세스 토큰을 검색하려면 [!DNL Shopify's] API 끝점 `/admin/oauth/access_token`을(를) 사용하여 이 URL을 추가하는 동안 도메인의 `myshopify.com` URL에 POST 요청을 합니다.

**API 형식**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**요청**

다음 요청은 [!DNL Shopify] 인스턴스에 대한 액세스 토큰을 생성합니다.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**응답**

성공적인 응답은 액세스 토큰과 권한 범위를 반환합니다.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## [!DNL Shopify] 데이터 스트리밍을 위한 웹후크 만들기 {#webhook}

웹후크를 사용하면 응용 프로그램이 [!DNL Shopify] 데이터와 계속 동기화되거나 특정 이벤트가 상점에서 발생한 후 작업을 수행할 수 있습니다. [!DNL Shopify] 데이터를 Experience Platform으로 스트리밍하기 위해 웹후크를 사용하여 HTTP 끝점과 구독 항목을 정의할 수 있습니다.

**요청**

다음 요청은 [!DNL Shopify Streaming] 데이터에 대한 웹후크를 만듭니다.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| 매개변수 | 설명 |
| --- | --- | 
| `webhook.address` | 스트리밍 메시지가 전송되는 HTTP 종단점입니다. |
| `webhook.topic` | Webhook 구독의 주제. 자세한 내용은 [[!DNL Shopify] webhook 이벤트 항목 안내서](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics)를 참조하십시오. |
| `webhook.format` | 데이터의 형식입니다. |

**응답**

성공한 응답은 해당 `id`, 주소 및 기타 메타데이터 정보를 포함하여 웹후크에 대한 정보를 반환합니다.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### 제한 사항 {#limitations}

다음은 [!DNL Shopify Streaming] 원본과 함께 웹후크를 사용할 때 발생할 수 있는 알려진 제한 사항 목록입니다.

* 동일한 리소스에 대해 서로 다른 주제의 전달 순서를 조정할 수 있는 것은 아닙니다. 예를 들어 `products/update` 웹후크가 `products/create` 웹후크 전에 배달될 수 있습니다.
* 웹후크 이벤트를 엔드포인트에 한 번 이상 전달하도록 웹후크를 설정할 수 있습니다. 즉, 끝점이 동일한 이벤트를 두 번 이상 받을 수 있습니다. `X-Shopify-Webhook-Id` 헤더를 이전 이벤트와 비교하여 중복된 웹후크 이벤트를 검색할 수 있습니다.
* [!DNL Shopify]이(가) HTTP 2xx 상태 응답을 성공한 알림으로 처리합니다. 기타 모든 상태 코드 응답은 실패로 간주됩니다. [!DNL Shopify]에서 실패한 웹후크 알림에 대한 다시 시도 메커니즘을 제공합니다. 5초를 기다린 후 **응답이 없는 경우**, [!DNL Shopify]은(는) 다음 **48시간** 동안 **19회** 연결을 다시 시도합니다. 다시 시도 기간이 끝날 때까지 응답이 없으면 [!DNL Shopify]에서 웹후크를 삭제합니다.

## 다음 단계

다음 자습서에서는 API 및 UI를 사용하여 [!DNL Shopify Streaming] 소스를 Experience Platform에 연결하는 방법에 대한 단계를 제공합니다.

* [흐름 서비스 API를 사용하여 Shopify 스트리밍 소스 연결 및 데이터 흐름 만들기](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [UI에서 Shopify 스트리밍 소스 연결 및 데이터 흐름 만들기](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
