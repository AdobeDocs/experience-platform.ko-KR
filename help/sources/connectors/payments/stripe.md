---
title: Stripe
description: Stripe 계정에서 Adobe Experience Platform으로 결제 데이터를 수집하는 방법에 대해 알아봅니다
badge: Beta
source-git-commit: f8df3ddb96ad0810a7a46b0a55125336c427aebd
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>다음 [!DNL Stripe] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

규모에 관계없이 수천 개의 비즈니스가 다음을 활용합니다. [!DNL Stripe] Adobe Experience Platform, Adobe Commerce 및 의 도움을 받아 온라인과 직접 결제를 수락하고 새로운 수익원을 창출하며 전 세계로 확장할 수 있습니다. [!DNL Magento Open Source].

사용 [!DNL Stripe] 고객이 구매 플로우 동안 캡처한 데이터를 수집할 Experience Platform 소스. 수집되면 이 데이터를 사용하여 개인화된 오퍼를 만들고 더 풍부한 비즈니스 통찰력을 얻을 수 있습니다.

>[!TIP]
>
>다음에 대한 질문: [!DNL Stripe] 소스 - Experience Platform, 연락처 [!DNL Stripe] adobe-partnership에서<span>@stripe.com.

>[!BEGINSHADEBOX]

**샘플 사용 사례 [!DNL Stripe] 소스**

귀하의 비즈니스에서 고객은 옵션을 사용하여 온라인 스토어에서 항목을 구입할 수 있습니다. **지금 구입** 및 **나중에 지불** (사용 [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm], 또는 [!DNL Zip]).

사용 [!DNL Stripe] 사용 분석을 위한 데이터 소스 **지금 구입** 및 **나중에 지불** 이러한 고객에게 개인화된 오퍼를 제공하고 테스트합니다. 예를 들어 체크아웃 전에 추가 기능 항목을 추천하여 장바구니에 있는 항목 수를 늘리는 것이 좋습니다.

>[!ENDSHADEBOX]

을(를) 설정하는 방법에 대한 자세한 내용은 아래 문서를 참조하십시오 [!DNL Stripe] 소스 계정에서 필요한 자격 증명을 검색하고 스키마를 만듭니다.

## 전제 조건 {#prerequisites}

다음 섹션에서는 연결하기 전에 완료해야 하는 사전 요구 사항 설정에 대한 정보를 제공합니다. [!DNL Stripe] Experience Platform 계정.

### 액세스 토큰 검색

* 에 로그인합니다 [[!DNL Stripe] 대시보드](https://dashboard.stripe.com/login) 사용 [!DNL Stripe] 이메일 주소 및 암호.
* 다음에서 [!DNL Developers] 대시보드, 선택 **[!DNL API keys for developers]**.
* 아래 **API 키** 탭, 선택 **[!DNL Reveal test key]** 액세스 토큰을 표시합니다.
* 이제 연결할 때 이 토큰을 액세스 토큰으로 사용할 수 있습니다. [!DNL Stripe] 다음 중 하나를 사용하여 Experience Platform 할 계정 [!DNL Flow Service] API 또는 Experience Platform UI.

### 필요한 자격 증명 수집

을(를) 연결하려면 [!DNL Stripe] 계정을 Experience Platform 하려면 다음 인증 자격 증명에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB API]

에 연결할 때 다음 자격 증명을 제공해야 합니다. [!DNL Stripe] 계정 사용 [!DNL Flow Service] API.

| 자격 증명 | 설명 |
| --- | --- |
| `accessToken` | 사용자 [!DNL Stripe] OAuth 2 코드 새로 고침 인증 토큰. |
| `connectionSpec.id` | 의 연결 사양 ID [!DNL Stripe] 소스. 이 ID는 다음과 같이 수정됩니다. `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB UI]

에 연결할 때 다음 자격 증명을 제공해야 합니다. [!DNL Stripe] Experience Platform 사용자 인터페이스를 사용하는 계정입니다.

| 자격 증명 | 설명 |
| --- | --- |
| 액세스 토큰 | 사용자 [!DNL Stripe] OAuth 2 코드 새로 고침 인증 토큰. |

>[!ENDTABS]

사용에 대한 자세한 내용 [!DNL Stripe] API, 읽기 [[!DNL Stripe] api 키에 대한 설명서](https://docs.stripe.com/keys).

### XDM(경험 데이터 모델) 스키마 만들기

다음 [!DNL Stripe] 소스는 다음 리소스 경로에서 데이터 수집을 지원합니다.

* 청구
* 구독수
* 환불
* 잔고 거래
* 고객
* 가격

전송할 필드 및 데이터 유형을 저장할 수 있는 데이터 세트를 설명하는 XDM 스키마를 만들어야 합니다 [!DNL Stripe] Experience Platform.

>[!BEGINTABS]

>[!TAB 청구]

위치 [!DNL Stripe], **청구** 돈에 대한 접근 시도를 나타냅니다. [!DNL Stripe]. 읽기 [[!DNL Stripe] 요금에 대한 API 안내서](https://docs.stripe.com/api/charges) 자세한 내용은 특정 요금 속성을 참조하십시오.

+++Stripe 비용 객체를 보려면 선택

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB 구독]

위치 [!DNL Stripe], 다음을 사용할 수 있습니다 **구독** 고객에게 반복해서 비용을 청구하다. 읽기 [[!DNL Stripe] 구독에 대한 API 안내서](https://docs.stripe.com/api/subscriptions) 를 참조하십시오.

+++Stripe 가입 개체를 보려면 선택

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB 환불]

위치 [!DNL Stripe], 다음을 사용할 수 있습니다 **환불** 이전에 생성한 비용을 환불합니다. 읽기 [[!DNL Stripe] 환불 관련 API 안내서](https://docs.stripe.com/api/refunds) 자세한 내용은 환불 속성을 참조하십시오.

+++Stripe 환불 오브젝트를 보려면 선택

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB 잔고 거래]

위치 [!DNL Stripe], **잔고 거래** 다음 항목 간의 자금 이동을 나타냅니다. [!DNL Stripe] 계정. 읽기 [[!DNL Stripe] 잔고 거래에 대한 API 안내서](https://docs.stripe.com/api/balance_transactions) 특정 잔고 거래 속성에 대한 자세한 내용.

+++Stripe 잔액 거래 객체를 보려면 선택합니다.

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB 고객]

위치 [!DNL Stripe], **고객** 비즈니스의 해당 고객을 나타냅니다. 특정 고객 특성에 대한 자세한 내용은 [[!DNL Stripe] 고객에 대한 API 안내서](https://docs.stripe.com/api/customers) 를 참조하십시오.

+++Stripe 고객 개체를 보려면 선택

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB 가격]

위치 [!DNL Stripe], **가격** 제품의 반복 구매와 일회성 구매 모두에 대한 단가, 통화 및 선택적 청구 주기를 나타냅니다. 읽기 [[!DNL Stripe] 가격에 대한 API 안내서](https://docs.stripe.com/api/prices) 특정 가격 속성에 대한 자세한 정보입니다.

+++Stripe 가격 객체를 보려면 선택

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

### Experience Platform에 대한 권한 구성

둘 다 있어야 합니다. **[!UICONTROL 소스 보기]** 및 **[!UICONTROL 소스 관리]** 에 연결하기 위해 계정에 대해 활성화된 권한 [!DNL Stripe] Experience Platform 계정. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md).

## 다음 단계

사전 요구 사항 설정을 완료하면 을(를) 계속 연결하여 수집할 수 있습니다. [!DNL Stripe] Experience Platform 대상 데이터. 수집 방법을 알아보려면 다음 안내서를 참조하십시오 [!DNL Stripe] api 또는 Experience Platform 인터페이스를 사용하여 사용자에게 결제 데이터:

* [플로우 서비스 API를 사용하여 Stripe 계정에서 Experience Platform으로 결제 데이터 수집](../../tutorials/api/create/payments/stripe.md).
* [사용자 인터페이스를 사용하여 Stripe 계정에서 Experience Platform으로 결제 데이터 수집](../../tutorials/ui/create/payments/stripe.md).