---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 및 Experience Cloud 애플리케이션
description: 이 문서에서는 개인 정보 보호 관련 작업을 위해 다양한 Experience Cloud 애플리케이션을 구성하는 방법에 대한 참조를 제공합니다.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 8%

---

# [!DNL Privacy Service] 및 [!DNL Experience Cloud] 응용 프로그램

Adobe Experience Platform [!DNL Privacy Service]은(는) 여러 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 보호 요청을 지원하도록 빌드되었습니다. 각 애플리케이션은 데이터 주체를 식별하기 위한 다양한 제품 값과 ID를 지원합니다.

이 문서는 [!DNL Experience Cloud] 응용 프로그램 설명서에 대한 참조 역할을 하며, 이 설명서는 개인 정보 보호 관련 작업을 위해 해당 응용 프로그램을 구성하는 방법에 대해 설명합니다. 여기에는 데이터 형식을 지정하고 레이블을 지정하는 방법이 포함됩니다. 두 가지 애플리케이션 범주가 포함됩니다.

* [Privacy Service과 통합된 응용 프로그램](#integrated): [!DNL Privacy Service]에 액세스, 삭제 또는 옵트아웃 요청을 보낼 수 있는 응용 프로그램
* [셀프 서비스 응용 프로그램](#self-serve): 내부적으로 개인 정보 요청을 관리해야 하며 [!DNL Privacy Service]과(와) 직접 통신할 수 없는 응용 프로그램입니다.

개인 정보 보호 요청 형식을 지정하는 방법과 해당 요청에 대해 지원되는 값을 알아보려면 [!DNL Experience Cloud] 응용 프로그램에 대한 설명서를 검토하십시오.

## [!DNL Privacy Service]과(와) 통합된 응용 프로그램 {#integrated}

다음은 [!DNL Privacy Service]과(와) 통합된 [!DNL Experience Cloud] 응용 프로그램 목록이며, 호환되는 [!DNL Privacy Service] 기능, 삭제 요청 처리를 위한 프로토콜 및 자세한 내용을 보려면 설명서에 대한 링크를 포함합니다.

>[!NOTE]
>
>모든 통합 제품은 30일 이내에 개인 정보 보호 요청에 응답합니다.

| 애플리케이션 | 액세스/삭제 | 판매 옵트아웃 | 비헤이비어 삭제 | 설명서 및 기타 고려 사항 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | 데이터 주체의 쿠키 ID 또는 장치 ID는 쿠키와 연결된 모든 비용, 클릭 및 매출 데이터와 함께 시스템에서 삭제됩니다. | <ul><li>[GDPR에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA에 대한 판매 중지 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics은 민감도 및 계약 제한 사항에 따라 데이터에 레이블을 지정하는 도구를 제공합니다. 레이블은 다음에 대한 중요한 단계입니다.<ol><li>데이터 주체 식별.</li><li>액세스 요청의 일부로 반환할 데이터 결정</li><li>삭제 요청의 일부로 삭제해야 하는 데이터 필드 식별.</li></ol> | <ul><li>[개인 정보 보호 워크플로](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Analytics 레이블 지정](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Analytics 옵트아웃](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 요청에 포함된 Audience Manager 식별자와 연관된 모든 트레이트 및 세그먼트가 삭제됩니다. 또한 개인에 대한 각 식별자가 추가 데이터 수집에서 옵트아웃되고 각 ID 매핑이 제거됩니다. | <ul><li>[액세스](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [삭제](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data) 설명서</li><li>[옵트아웃 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[옵트아웃 요청](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | 데이터 주체의 저장된 데이터는 시스템에서 삭제됩니다. | <ul><li>[개인 정보 관리](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=ko)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 데이터 주체의 저장된 데이터는 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/en/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[옵트아웃 설명서](https://experienceleague.adobe.com/en/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Adobe 고객 속성(CRS) | ✓ | N/A | 데이터 주체의 속성이 시스템에서 삭제됩니다. | <ul><li>[GDPR에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>고객 속성에는 데이터를 전송할 수 있는 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Experience Platform이 Privacy Service에서 삭제 요청을 수신하면 Experience Platform은 요청이 수신되었고 영향을 받는 데이터가 삭제 대상으로 표시되었음을 Privacy Service에 확인합니다. 그런 다음 개인 정보 보호 작업이 완료되면 레코드가 데이터 레이크 또는 프로필 저장소에서 제거됩니다. 작업이 완료되기 전에 데이터가 일시 삭제되므로 Experience Platform 서비스에서 액세스할 수 없습니다. | <ul><li>[데이터 레이크에 대한 액세스/삭제 설명서](../catalog/privacy.md)</li><li>[ID 서비스에 대한 액세스/삭제 설명서](../identity-service/privacy.md)</li><li>[실시간 고객 프로필에 대한 액세스/삭제 설명서](../profile/privacy.md)</li><li>[!DNL Experience Platform]에서 대상 세그먼트에 대한 [옵트아웃 요청을 수행합니다](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | N/A | 데이터 주체의 저장된 데이터는 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass 인증 | ✓ | N/A | 데이터 주체의 저장된 데이터는 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>패스에는 데이터를 전송할 수 있는 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Adobe Target | ✓ | N/A | 데이터 주체의 ID와 관련된 모든 데이터가 해당 방문자 프로필에서 삭제됩니다. 개인을 식별하지 않거나 관련이 없는 집계 또는 익명화 데이터(예: 콘텐츠 데이터)는 삭제 요청에 적용되지 않습니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target]에 데이터를 전송할 수 있는 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Commerce(Personalization) | ✓ | N/A | Privacy Service은 마케팅 목적으로 Commerce SaaS 서비스에 저장된 [!DNL Commerce]개의 데이터를 삭제합니다. 즉, 데이터 주체의 프로필 및 순서가 더 이상 캠페인 및 고객 여정에 사용하기 위해 Adobe 마케팅 애플리케이션으로 전송되지 않습니다. 그러나 Privacy Service은 [!DNL Commerce] 응용 프로그램의 데이터를 삭제하지 않습니다. 상인 트랜잭션 요구 사항에 계속 필요할 수 있기 때문입니다. 판매자는 [!DNL Commerce] 응용 프로그램에서 데이터 삭제/액세스 요청을 담당합니다. | <ul><li>[Commerce에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | N/A | 데이터 주체의 저장된 데이터는 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo]에 데이터를 전송할 수 있는 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |

{style="table-layout:auto"}

## 셀프서비스 애플리케이션 {#self-serve}

다음은 [!DNL Privacy Service]과(와) 통합되지 않은 [!DNL Experience Cloud] 응용 프로그램 목록이며 내부적으로 해당 응용 프로그램의 개인 정보 문제를 관리해야 합니다. 설명서 내용에 대한 설명과 함께 각 애플리케이션의 설명서에 대한 링크가 제공됩니다.

| 애플리케이션 | 설명서 설명 |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 고객 개인 정보 보호 관리자 또는 AEM 관리자가 GDPR 요청을 처리할 수 있는 방법에 대한 개요입니다. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Livefyre를 사용하여 GDPR 액세스 및 삭제 요청을 수행하는 단계입니다. |
| [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/overview) | Adobe Commerce 설치가 특정 개인 정보 보호 규정의 요구 사항을 준수하는지 확인합니다. |
| Adobe Experience Platform의 [태그](../tags/ui/client-side/consent.md) | 개발자가 확장 프로그램 및 규칙 작성기를 사용하여 옵트인 및 옵트아웃 솔루션을 정의할 수 있는 방법입니다. |
| [Workfront](https://www.workfront.com/privacy-notice) | Workfront에서 개인 데이터를 수집하는 방법과 데이터 주체가 양식을 통해 개인 정보 보호 요청을 제출하는 방법을 알아봅니다. |

{style="table-layout:auto"}
