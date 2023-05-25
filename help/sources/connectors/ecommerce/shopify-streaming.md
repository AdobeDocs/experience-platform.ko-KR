---
title: Shopify 스트리밍 소스
description: 소스 연결 및 데이터 흐름을 만들어 Shopify 인스턴스에서 Adobe Experience Platform으로 스트리밍 데이터를 수집하는 방법을 알아봅니다
badge: 베타
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: cfe5f34316e9db072f0a320143354f2771b4a3a9
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>다음 [!DNL Shopify Streaming] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform은 스트리밍 애플리케이션에서 데이터를 수집할 수 있도록 지원합니다. 스트리밍 공급자에 대한 지원은 다음과 같습니다 [!DNL Shopify].

## 사전 요구 사항 {#prerequisites}

다음 섹션에서는 를 사용하기 전에 완료해야 하는 사전 요구 사항에 대해 간략히 설명합니다. [!DNL Shopify Streaming] 소스.

유효한 권한이 있어야 합니다. [!DNL Shopify] 에 연결하기 위한 파트너 계정 [!DNL Shopify] API. 아직 파트너 계정이 없는 경우 다음을 사용하여 등록하십시오. [[!DNL Shopify] 파트너 대시보드](https://www.shopify.com/partners).

### 애플리케이션 만들기

유효한 [!DNL Shopify] 파트너 계정에서 이제 파트너 대시보드를 사용하여 앱을 계속 진행하고 만들 수 있습니다. 에서 앱을 만드는 방법에 대한 포괄적인 단계를 설명합니다. [!DNL Shopify], 다음을 읽습니다 [[!DNL Shopify] 시작 안내서](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

앱이 생성되면 을 검색합니다. **클라이언트 ID** 및 **클라이언트 암호** 다음에서 **클라이언트 자격 증명** 의 탭 [!DNL Shopify] 파트너 대시보드입니다. 클라이언트 ID 및 클라이언트 암호는 다음 단계에서 인증 코드 및 액세스 토큰을 검색하는 데 사용됩니다.

### 인증 코드 검색

그런 다음 도메인의 `myshopify.com` API 키, 범위 및 리디렉션 URI를 정의하는 쿼리 문자열과 함께 URL을 브라우저에 삽입합니다.

이 URL의 형식은 다음과 같습니다.

**API 형식**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| 매개변수 | 설명 |
| --- | --- |
| `shop` | 하위 도메인 `myshopify.com` URL. |
| `api_key` | 사용자 [!DNL Shopify] 클라이언트 ID. 에서 클라이언트 ID를 검색할 수 있습니다. **클라이언트 자격 증명** 의 탭 [!DNL Shopify] 파트너 대시보드입니다. |
| `scopes` | 정의할 액세스 유형입니다. 예를 들어 범위를 다음과 같이 설정할 수 있습니다. `scope=write_orders,read_customers` 주문 수정 및 고객 읽기 권한을 허용합니다. |
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

클라이언트 ID, 클라이언트 암호 및 인증 코드가 있으므로 액세스 토큰을 검색할 수 있습니다. POST 액세스 토큰을 검색하려면 도메인의 `myshopify.com` 이 URL을 로 추가하는 동안 URL [!DNL Shopify's] API 끝점: `/admin/oauth/access_token`.

**API 형식**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**요청**

다음 요청은 다음에 대한 액세스 토큰을 생성합니다. [!DNL Shopify] 인스턴스.

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

## 스트리밍용 웹후크 만들기 [!DNL Shopify] 데이터 {#webhook}

웹후크를 사용하면 응용 프로그램이 [!DNL Shopify] 특정 이벤트가 상점에서 발생한 후 데이터 또는 작업 수행 스트리밍용 [!DNL Shopify] 웹후크를 사용하여 Experience Platform 할 데이터를 http 종단점 및 구독 주제를 정의할 수 있습니다.

**요청**

다음 요청은 을 위한 웹후크를 생성합니다. [!DNL Shopify Streaming] 데이터.

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
| `webhook.topic` | Webhook 구독의 주제. 자세한 내용은 [[!DNL Shopify] webhook 이벤트 항목 안내서](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | 데이터의 형식입니다. |

**응답**

성공적인 응답은 웹후크의 해당 정보를 포함하여 웹후크에 대한 정보를 반환합니다 `id`, 주소 및 기타 메타데이터 정보.

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

다음은 웹 후크를 와 함께 사용할 때 발생할 수 있는 알려진 제한 사항 목록입니다 [!DNL Shopify Streaming] 소스.

* 동일한 리소스에 대해 서로 다른 주제의 전달 순서를 조정할 수 있는 것은 아닙니다. 예를 들어 `products/update` webhook이 다음 전에 전달됨 `products/create` webhook.
* 웹후크 이벤트를 엔드포인트에 한 번 이상 전달하도록 웹후크를 설정할 수 있습니다. 즉, 끝점이 동일한 이벤트를 두 번 이상 받을 수 있습니다. 다음을 비교하여 중복 웹후크 이벤트를 검색할 수 있습니다. `X-Shopify-Webhook-Id` 헤더를 이전 이벤트로 변경합니다.
* [!DNL Shopify] 은 HTTP 2xx 상태 응답을 성공적인 알림으로 처리합니다. 기타 모든 상태 코드 응답은 실패로 간주됩니다. [!DNL Shopify] 실패한 웹후크 알림에 대한 재시도 메커니즘을 제공합니다. 있는 경우 **5초 동안 기다린 후 응답 없음**, [!DNL Shopify] 연결을 다시 시도합니다. **19회** 다음 과정에서 **48시간**. 재시도 기간이 끝날 때까지 응답이 없는 경우 [!DNL Shopify] 웹후크를 삭제합니다.

## 다음 단계

다음 튜토리얼에서는 을(를) 연결하는 방법에 대한 단계를 제공합니다 [!DNL Shopify Streaming] api 및 UI를 사용하여 소스-Experience Platform:

* [흐름 서비스 API를 사용하여 Shopify 스트리밍 소스 연결 및 데이터 흐름 만들기](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [UI에서 Shopify 스트리밍 소스 연결 및 데이터 흐름 만들기](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
