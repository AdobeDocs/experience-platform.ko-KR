---
title: SAP Commerce Source 개요
description: API 또는 사용자 인터페이스를 사용하여 SAP Commerce을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>[!DNL SAP Commerce] 원본이 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

B2B 및 B2C 엔터프라이즈를 위한 클라우드 기반 전자 상거래 플랫폼 솔루션인 [[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html)은(는) SAP Customer Experience 포트폴리오의 일부로 사용할 수 있습니다. [[!DNL SAP] 구독 청구](https://www.sap.com/products/financial-management/subscription-billing.html)는 포트폴리오의 제품이며 표준화된 통합을 통해 간소화된 판매 및 결제 환경을 통해 완전한 구독 라이프사이클 관리를 가능하게 합니다.

[!DNL SAP Commerce] 소스를 사용하면 아래 [[!DNL SAP] 구독 청구](https://www.sap.com/products/financial-management/subscription-billing.html) 비즈니스 파트너 API 끝점에서 고객 및 연락처 정보를 Experience Platform으로 수집할 수 있습니다.

* [고객](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [연락처](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

또한 고객 데이터를 검색하기 위해 [!DNL SAP Commerce]을(를) 실행하는 경우 고객의 연락처 정보를 검색하기 위해 [고객 연락처 관계](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) API도 호출됩니다.

## IP 주소 허용 목록 {#ip-allow-list}

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 할 수 있습니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

## 전제 조건 {#prerequisites}

[!DNL SAP Commerce] 데이터를 Experience Platform으로 가져오려면 먼저 다음 사항을 확인해야 합니다.

* [!DNL SAP Subscription Billing] 계정입니다. 아직 유효한 청구 계정이 없는 경우 [!DNL SAP] 계정 관리자에게 문의하십시오. 자세한 내용은 [[!DNL SAP] 플랫폼 구성](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) 문서를 참조하십시오.

* [!DNL SAP] 서비스 키입니다. [!DNL SAP] 서비스 키를 사용하면 Experience Platform을 통해 [!DNL SAP Subscription Billing] API에 액세스할 수 있습니다. [!DNL SAP Commerce]를 사용하려면 다음 요구 사항을 충족해야 합니다.
   * 클라이언트 ID
   * 클라이언트 암호
   * URL. URL 패턴은 `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`입니다. 이 값은 API를 사용하여 [기본 연결을 만듭니다](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) 또는 Experience Platform UI를 통해 [계정 연결 [!DNL SAP Commerce] 을(를) ](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account)할 때 `region` 및 `tokenEndpoint`의 값을 얻는 데 나중에 사용됩니다.

+++서비스 키의 예를 보려면 선택

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## 다음 단계

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL SAP Commerce]을(를) Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

* [API를 사용하여  [!DNL SAP Commerce] 데이터를 Experience Platform으로 가져오기](../../tutorials/api/create/ecommerce/sap-commerce.md)할 원본 연결 및 데이터 흐름을 만듭니다.
* [UI를 사용하여  [!DNL SAP Commerce] 계정을 Experience Platform에 연결](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [UI를 사용하여 소스에 대한 데이터 흐름 만들기](../../tutorials/ui/dataflow/ecommerce.md)
