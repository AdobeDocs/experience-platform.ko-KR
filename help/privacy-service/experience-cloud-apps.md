---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 및 Experience Cloud 애플리케이션
topic-legacy: overview
description: 이 문서에서는 개인 정보 관련 작업을 위해 다양한 Experience Cloud 응용 프로그램을 구성하는 방법에 대한 참조를 제공합니다.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 892bb4fa5302d63923c1a2e4759f0253955576e2
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 11%

---

# [!DNL Privacy Service] 및  [!DNL Experience Cloud] 애플리케이션

Adobe Experience Platform [!DNL Privacy Service]은(는) 여러 Adobe Experience Cloud 응용 프로그램에 대한 개인 정보 보호 요청을 지원하기 위해 빌드되었습니다. 각 애플리케이션은 데이터 주체를 식별하기 위해 서로 다른 제품 값과 ID를 지원합니다.

이 문서는 개인 정보 보호 관련 작업에 대해 해당 응용 프로그램을 구성하는 방법을 개략적으로 설명하는 [!DNL Experience Cloud] 응용 프로그램 설명서에 대한 참조 역할을 합니다. 여기에는 데이터 형식을 지정하고 레이블을 지정하는 방법이 포함됩니다. 두 가지 애플리케이션 범주는 다음과 같습니다.

* [Privacy Service과 통합된 애플리케이션](#integrated): 액세스, 삭제 또는 옵트아웃 요청을 보낼 수 있는  [!DNL Privacy Service].
* [셀프 서비스 애플리케이션](#self-serve): 내부적으로 개인 정보 보호 요청을 관리해야 하며  [!DNL Privacy Service] 직접 통신할 수 없는 응용 프로그램입니다.

[!DNL Experience Cloud] 응용 프로그램에 대한 설명서를 검토하여 개인 정보 보호 요청의 서식을 지정하는 방법과 이러한 요청에 대해 지원되는 값을 알아보십시오.

## [!DNL Privacy Service]과 통합된 애플리케이션 {#integrated}

다음은 [!DNL Privacy Service]과 통합된 [!DNL Experience Cloud] 애플리케이션 목록이며, 이러한 응용 프로그램이 호환되는 [!DNL Privacy Service] 기능과 자세한 내용은 설명서 링크를 제공합니다.

| 애플리케이션 | 액세스/삭제 | 판매 거부 | 설명서 및 고려 사항 |
| --- | :---: | :---: | --- |
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[GDPR에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA에 대한 설명서 액세스/삭제](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA용 판매 중지 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=ko-KR)</li><li>[!DNL Analytics] 개인 정보 보고 변수를 사용하여 옵트아웃  [요청을 처리합니다](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[옵트아웃 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=ko#getting-started)</li><li>[옵트아웃 설명서](../segmentation/consents.md)</li></ul> |
| CRS(Adobe 고객 속성) | ✓ | N/A | <ul><li>[GDPR에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA에 대한 설명서 액세스/삭제](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>고객 속성에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Data Lake에 대한 액세스/삭제 설명서](../catalog/privacy.md)</li><li>[실시간 고객 프로필에 대한 액세스/삭제 설명서](../profile/privacy.md)</li><li>[!DNL Experience Platform] 대상  [세그먼트에 대한 옵트아웃 요청을 수행합니다](../segmentation/consents.md).</li></ul> |
| Adobe Primetime 인증 | ✓ | 해당 없음 | <ul><li>[설명서 액세스/삭제](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Adobe Target | ✓ | 해당 없음 | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 셀프 서비스 애플리케이션 {#self-serve}

다음은 [!DNL Privacy Service]과 통합되지 않고 내부적으로 개인 정보 보호 문제를 관리해야 하는 [!DNL Experience Cloud] 응용 프로그램 목록입니다. 각 애플리케이션의 설명서에 대한 링크와 설명서 내용에 대한 설명이 제공됩니다.

| 애플리케이션 | 설명서 설명 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html) | Adobe Campaign Classic의 GDPR 기능에 대한 개요입니다. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 고객 개인 정보 보호 관리자 또는 AEM 관리자가 GDPR 요청을 처리하는 방법에 대한 개요입니다. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Livefyre를 사용하여 GDPR 액세스 및 삭제 요청을 만드는 절차. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Magento Commerce 설치가 특정 개인 정보 보호 법규 요구 사항을 준수하도록 하십시오. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Marketo에 개인 정보 보호 규정이 적용되는 방법을 알아봅니다. |
| [Adobe Experience Platform의 태그](../tags/ui/client-side/consent.md) | 개발자가 확장 프로그램 및 규칙 작성기를 사용하여 옵트인 및 옵트아웃 솔루션을 정의할 수 있는 방법입니다. |
| [Workfront](https://www.workfront.com/privacy-notice) | Workfront에서 개인 데이터를 수집하는 방법과 데이터 주체가 양식을 통해 개인 정보 보호 요청을 제출하는 방법을 알아봅니다. |

{style=&quot;table-layout:auto&quot;}
