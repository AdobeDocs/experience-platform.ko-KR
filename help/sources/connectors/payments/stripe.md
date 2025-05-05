---
title: Stripe
description: Stripe 계정에서 Adobe Experience Platform으로 결제 데이터를 수집하는 방법에 대해 알아봅니다
badge: Beta
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>[!DNL Stripe] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

규모에 관계없이 수천 개의 비즈니스가 온라인과 직접 [!DNL Stripe]을(를) 활용하여 결제를 수락하고 새로운 매출원을 창출하며 Adobe Experience Platform, Adobe Commerce 및 [!DNL Magento Open Source]의 도움을 받아 전 세계적으로 확장하고 있습니다.

Experience Platform의 [!DNL Stripe] 소스를 사용하여 고객이 구매 플로우를 진행하는 동안 캡처한 데이터를 수집합니다. 수집되면 이 데이터를 사용하여 개인화된 오퍼를 만들고 더 풍부한 비즈니스 통찰력을 얻을 수 있습니다.

>[!TIP]
>
>Experience Platform의 [!DNL Stripe] 소스에 대한 질문이 있으면 adobe-partnership<span>@stripe.com에서 [!DNL Stripe]에게 문의하십시오.

>[!BEGINSHADEBOX]

[!DNL Stripe] 소스에 대한 **샘플 사용 사례**

귀하의 비즈니스에서 고객은 온라인 스토어에서 항목을 구매할 수 있습니다(**지금 구매** 및 **나중에 결제** 옵션([!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] 또는 [!DNL Zip] 사용).

[!DNL Stripe] 데이터 원본을 사용하여 **지금 구입** 및 **나중에 결제** 옵션의 사용을 분석하고 이러한 고객에게 개인화된 오퍼를 실험하세요. 예를 들어 체크아웃 전에 추가 기능 항목을 추천하여 장바구니에 있는 항목 수를 늘리는 것이 좋습니다.

>[!ENDSHADEBOX]

[!DNL Stripe] 소스 계정을 설정하고 필요한 자격 증명을 검색하며 스키마를 만드는 방법에 대한 자세한 내용은 아래 문서를 참조하십시오.

## 전제 조건 {#prerequisites}

다음 섹션에서는 [!DNL Stripe] 계정을 Experience Platform에 연결하기 전에 완료해야 하는 필수 구성 요소 설정에 대한 정보를 제공합니다.

### 액세스 토큰 검색

* [!DNL Stripe] 전자 메일 주소와 암호를 사용하여 [[!DNL Stripe] 대시보드](https://dashboard.stripe.com/login)에 로그인합니다.
* [!DNL Developers] 대시보드에서 **[!DNL API keys for developers]**&#x200B;을(를) 선택합니다.
* **API 키** 탭에서 **[!DNL Reveal test key]**&#x200B;을(를) 선택하여 액세스 토큰을 표시합니다.
* 이제 [!DNL Flow Service] API 또는 Experience Platform UI를 사용하여 [!DNL Stripe] 계정을 Experience Platform에 연결할 때 이 토큰을 액세스 토큰으로 사용할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Stripe] 계정을 Experience Platform에 연결하려면 다음 인증 자격 증명에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB API]

[!DNL Flow Service] API를 사용하여 [!DNL Stripe] 계정에 연결할 때 다음 자격 증명을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `accessToken` | [!DNL Stripe] OAuth 2 코드 새로 고침 인증 토큰입니다. |
| `connectionSpec.id` | [!DNL Stripe] 소스의 연결 사양 ID입니다. 이 ID는 `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`(으)로 수정되었습니다. |

>[!TAB UI]

Experience Platform 사용자 인터페이스를 사용하여 [!DNL Stripe] 계정에 연결할 때 다음 자격 증명을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 액세스 토큰 | [!DNL Stripe] OAuth 2 코드 새로 고침 인증 토큰입니다. |

>[!ENDTABS]

[!DNL Stripe] API 사용에 대한 자세한 내용은 API 키에 대한 [[!DNL Stripe] 설명서](https://docs.stripe.com/keys)를 참조하십시오.

### XDM(경험 데이터 모델) 스키마 만들기

[!DNL Stripe] 원본은 다음 리소스 경로에서 데이터 수집을 지원합니다.

* 청구
* 구독수
* 환불
* 잔고 거래
* 고객
* 가격

[!DNL Stripe]에서 Experience Platform으로 보낼 필드 및 데이터 형식을 저장할 수 있는 데이터 집합을 설명하는 XDM 스키마를 만들어야 합니다.

>[!BEGINTABS]

>[!TAB 청구]

[!DNL Stripe]에서 **청구**&#x200B;는 [!DNL Stripe] (으)로 돈을 이동하려는 시도를 나타냅니다. 특정 요금 특성에 대한 자세한 내용은 [[!DNL Stripe] 요금 관련 API 안내서](https://docs.stripe.com/api/charges)를 참조하십시오.

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

[!DNL Stripe]에서 **구독**&#x200B;을 사용하여 정기적으로 고객에게 요금을 청구할 수 있습니다. 특정 구독 특성에 대한 자세한 내용은 [[!DNL Stripe] 구독에 대한 API 안내서](https://docs.stripe.com/api/subscriptions)를 참조하십시오.

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

[!DNL Stripe]에서 **환불**&#x200B;을 사용하여 이전에 만든 요금을 환불할 수 있습니다. 특정 환불 특성에 대한 자세한 내용은 [[!DNL Stripe] 환불 관련 API 안내서](https://docs.stripe.com/api/refunds)를 참조하십시오.

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

[!DNL Stripe]에서 **잔고 거래**&#x200B;는 [!DNL Stripe] 계정 간의 자금 이동을 나타냅니다. 특정 잔고 거래 특성에 대한 자세한 내용은 [[!DNL Stripe] 잔고 거래에 대한 API 안내서](https://docs.stripe.com/api/balance_transactions)를 참조하십시오.

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

[!DNL Stripe]에서 **customers**&#x200B;은(는) 비즈니스의 특정 고객을 나타냅니다. 특정 고객 특성에 대한 자세한 내용은 [[!DNL Stripe] 고객에 대한 API 안내서](https://docs.stripe.com/api/customers)를 참조하십시오.

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

[!DNL Stripe]에서 **가격**&#x200B;은(는) 제품의 반복 구매와 일회성 구매 모두에 대한 단가, 통화 및 선택적 청구 주기를 나타냅니다. 특정 가격 특성에 대한 자세한 내용은 [[!DNL Stripe] 가격에 대한 API 안내서](https://docs.stripe.com/api/prices)를 참조하십시오.

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

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

### Experience Platform에 대한 권한 구성

[!DNL Stripe] 계정을 Experience Platform에 연결하려면 계정에 대해 **[!UICONTROL 소스 보기]** 및 **[!UICONTROL 소스 관리]** 사용 권한이 모두 활성화되어 있어야 합니다. 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

## 다음 단계

필수 구성 요소 설정을 완료하면 연결을 계속 진행하고 [!DNL Stripe] 데이터를 Experience Platform으로 수집할 수 있습니다. API 또는 Experience Platform 인터페이스를 사용하여 [!DNL Stripe] 결제 데이터를 사용자에게 수집하는 방법에 대해 알아보려면 다음 안내서를 읽어 보십시오.

* [흐름 서비스 API를 사용하여 Stripe 계정에서 Experience Platform으로 결제 데이터를 수집합니다](../../tutorials/api/create/payments/stripe.md).
* [사용자 인터페이스를 사용하여 Stripe 계정에서 Experience Platform으로 결제 데이터를 수집합니다](../../tutorials/ui/create/payments/stripe.md).
