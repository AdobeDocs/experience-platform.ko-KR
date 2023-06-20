---
title: SAP Hybris 소스 개요
description: API 또는 사용자 인터페이스를 사용하여 SAP Hybris를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badge: 베타
hide: true
hidefromtoc: true
source-git-commit: 32e2c13dcdbf2f13b4025354dfc50f5ccaf5f664
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 2%

---

# [!DNL SAP Hybris]

>[!NOTE]
>
>다음 [!DNL SAP Hybris] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

[[!DNL SAP Hybris]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), B2B 및 B2C 기업을 위한 클라우드 기반 전자 상거래 플랫폼 솔루션은 SAP 고객 경험 포트폴리오의 일부로 사용할 수 있습니다. [[!DNL SAP] 구독 청구](https://www.sap.com/products/financial-management/subscription-billing.html) 는 포트폴리오의 제품이며 표준화된 통합을 통해 간소화된 판매 및 결제 경험을 통해 완전한 구독 라이프사이클 관리를 가능하게 합니다.

다음 [!DNL SAP Hybris] 소스를 사용하면 고객 및 연락처 정보를 [[!DNL SAP] 구독 청구](https://www.sap.com/products/financial-management/subscription-billing.html) 아래 비즈니스 파트너 API 엔드포인트:

* [고객](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [연락처](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

또한 다음과 같은 경우 [!DNL SAP Hybris] 를 실행하여 고객 데이터를 검색한 다음 [고객-연락처 관계](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) 고객의 연락처 정보를 검색하기 위해 API도 호출됩니다.

## IP 주소 허용 목록 {#ip-allow-list}

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 할 수 있습니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 다음을 참조하십시오. [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지 를 참조하십시오.

## 사전 요구 사항 {#prerequisites}

가져오기 전에 [!DNL SAP Hybris] 데이터를 Experience Platform 하려면 먼저 다음 사항이 있는지 확인해야 합니다.

* A [!DNL SAP Subscription Billing] 계정입니다. 아직 유효한 청구 계정이 없는 경우 다음으로 문의하십시오. [!DNL SAP] 계정 관리자. 다음을 참조하십시오. [[!DNL SAP] 플랫폼 구성](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) 자세한 내용은 문서를 참조하십시오.

* [!DNL SAP] 서비스 키. 다음 [!DNL SAP] 서비스 키를 사용하면 [!DNL SAP Subscription Billing] Experience Platform을 통한 API. [!DNL SAP Hybris]를 사용하려면 다음 요구 사항을 충족해야 합니다.
   * 클라이언트 ID
   * 클라이언트 암호
   * URL. URL 패턴은 다음과 같습니다. `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. 이 값은 나중에 값을 얻는 데 사용됩니다. `region` 및 `tokenEndpoint` 다음을 수행하는 경우 [기본 연결 만들기](../../tutorials/api/create/crm/sap-hybris.md#base-connection) api 사용 또는 다음을 수행하는 경우 [연결 [!DNL SAP Hybris] account](../../tutorials/ui/create/crm/sap-hybris.md#connect-account) 플랫폼 UI를 통해

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

아래 설명서는 연결 방법에 대한 정보를 제공합니다 [!DNL SAP Hybris] API 또는 사용자 인터페이스를 사용하여 Platform으로

* [소스 연결 및 데이터 흐름을 만들어 가져오기 [!DNL SAP Hybris] API를 사용하여 데이터를 플랫폼에 전송](../../tutorials/api/create/crm/sap-hybris.md).
* [연결 [!DNL SAP Hybris] UI를 사용하여 Experience Platform 할 계정](../../tutorials/ui/create/crm/sap-hybris.md).
* [UI를 사용하여 CRM 소스의 데이터 흐름 만들기](../../tutorials/ui/dataflow/crm.md)
