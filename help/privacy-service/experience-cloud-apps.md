---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 및 Experience Cloud 애플리케이션
description: 이 문서에서는 개인 정보 관련 작업을 위해 다양한 Experience Cloud 응용 프로그램을 구성하는 방법에 대한 참조를 제공합니다.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 4a078a09da131260fa44b64cd5f707482afdce04
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 12%

---

# [!DNL Privacy Service] 및 [!DNL Experience Cloud] 애플리케이션

Adobe Experience Platform [!DNL Privacy Service] 여러 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 보호 요청을 지원하기 위해 빌드되었습니다. 각 애플리케이션은 데이터 주체를 식별하기 위해 서로 다른 제품 값과 ID를 지원합니다.

이 문서는 [!DNL Experience Cloud] 개인 정보 보호 관련 작업에 대해 해당 애플리케이션을 구성하는 방법을 간략하게 설명하는 애플리케이션 문서입니다. 여기에는 데이터 형식을 지정하고 레이블을 지정하는 방법이 포함됩니다. 두 가지 애플리케이션 범주는 다음과 같습니다.

* [Privacy Service과 통합된 애플리케이션](#integrated): 액세스, 삭제 또는 옵트아웃 요청을 보낼 수 있는 응용 프로그램 [!DNL Privacy Service].
* [셀프 서비스 애플리케이션](#self-serve): 내부적으로 개인 정보 보호 요청을 관리해야 하며 통신하지 못하는 응용 프로그램 [!DNL Privacy Service] 직접 액세스할 수 있습니다.

다음 문서를 검토하십시오 [!DNL Experience Cloud] 애플리케이션 에서는 개인 정보 보호 요청의 형식을 지정하는 방법과 이러한 요청에 대해 지원되는 값을 알아보십시오.

## 통합 애플리케이션 [!DNL Privacy Service] {#integrated}

다음은 [!DNL Experience Cloud] 와 통합된 애플리케이션 [!DNL Privacy Service]를 포함한 [!DNL Privacy Service] 이러한 기능과 호환되는 기능, 삭제 요청 처리를 위한 프로토콜 및 자세한 내용은 설명서 링크를 참조하십시오.

>[!NOTE]
>
>모든 통합 제품은 30일 이내에 개인 정보 보호 요청에 응답합니다.

| 애플리케이션 | 액세스/삭제 | 판매 거부 | 동작 삭제 | 설명서 및 기타 고려 사항 |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | 데이터 주체의 쿠키 ID 또는 장치 ID가 쿠키와 연결된 모든 비용, 클릭 및 매출 데이터와 함께 시스템에서 삭제됩니다. | <ul><li>[GDPR에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[CCPA에 대한 설명서 액세스/삭제](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[CCPA용 판매 중지 설명서](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics는 그 민감도 및 계약 제한 사항에 따라 데이터를 라벨링하는 도구를 제공합니다. 레이블은 다음과 같은 중요한 단계입니다.<ol><li>데이터 주체 식별.</li><li>액세스 요청의 일부로 반환할 데이터를 결정합니다.</li><li>삭제 요청의 일부로 삭제해야 하는 데이터 필드 식별</li></ol> | <ul><li>[개인 정보 보호 워크플로우](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Analytics 레이블 지정](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | 요청에 포함된 Audience Manager 식별자와 연관된 모든 트레이트와 세그먼트가 삭제됩니다. 또한 개인의 각 식별자가 추가적인 데이터 수집을 옵트아웃하고 각 ID 매핑이 제거됩니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[옵트아웃 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | 데이터 주체의 저장된 데이터가 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=ko#getting-started)</li><li>[옵트아웃 설명서](../segmentation/consents.md)</li></ul> |
| CRS(Adobe 고객 속성) | ✓ | 해당 없음 | 데이터 주체의 속성이 시스템에서 삭제됩니다. | <ul><li>[GDPR에 대한 액세스/삭제 설명서](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[CCPA에 대한 설명서 액세스/삭제](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>고객 속성에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Experience Platform이 Privacy Service에서 삭제 요청을 받으면가 요청을 수신하고 영향을 받는 데이터가 삭제로 표시되었다는 확인을 Privacy Service에게 보냅니다. 그러면 개인 정보 작업이 완료되면 레코드가 Data Lake 또는 프로필 저장소에서 제거됩니다. 작업이 완료되기 전에 데이터가 소프트 삭제되므로 Platform 서비스에서 액세스할 수 없습니다. | <ul><li>[Data Lake에 대한 액세스/삭제 설명서](../catalog/privacy.md)</li><li>[ID 서비스에 대한 액세스/삭제 설명서](../identity-service/privacy.md)</li><li>[실시간 고객 프로필에 대한 액세스/삭제 설명서](../profile/privacy.md)</li><li>[!DNL Experience Platform] 우대 [대상 세그먼트에 대한 옵트아웃 요청](../segmentation/consents.md).</li></ul> |
| Adobe Primetime 인증 | ✓ | 해당 없음 | 데이터 주체의 저장된 데이터가 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] 에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Adobe Target | ✓ | 해당 없음 | 데이터 주체의 ID와 연관된 모든 데이터는 해당 방문자 프로필에서 삭제됩니다. 개인을 식별하지 않거나 관련이 없는(예: 컨텐츠 데이터) 집계 또는 익명화 데이터는 삭제 요청에 적용되지 않습니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] 에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |
| Marketo Engage | ✓ | 해당 없음 | 데이터 주체의 저장된 데이터가 시스템에서 삭제됩니다. | <ul><li>[설명서 액세스/삭제](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] 에는 데이터를 전송할 기능이 없으므로 판매 중지 요청을 적용할 수 없습니다.</li></ul> |

{style="table-layout:auto"}

## 셀프 서비스 애플리케이션 {#self-serve}

다음은 [!DNL Experience Cloud] 와 통합되지 않은 애플리케이션 [!DNL Privacy Service] 또한 이러한 개인 정보 보호 문제를 내부적으로 관리해야 합니다. 각 애플리케이션의 설명서에 대한 링크와 설명서 내용에 대한 설명이 제공됩니다.

| 애플리케이션 | 설명서 설명 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=ko) | Adobe Campaign Classic의 GDPR 기능에 대한 개요입니다. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | 고객 개인 정보 보호 관리자 또는 AEM 관리자가 GDPR 요청을 처리하는 방법에 대한 개요입니다. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Livefyre를 사용하여 GDPR 액세스 및 삭제 요청을 만드는 절차. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Magento Commerce 설치가 특정 개인 정보 보호 법규 요구 사항을 준수하도록 하십시오. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Marketo에 개인 정보 보호 규정이 적용되는 방법을 알아봅니다. |
| [Adobe Experience Platform의 태그](../tags/ui/client-side/consent.md) | 개발자가 확장 프로그램 및 규칙 작성기를 사용하여 옵트인 및 옵트아웃 솔루션을 정의할 수 있는 방법입니다. |
| [Workfront](https://www.workfront.com/privacy-notice) | Workfront에서 개인 데이터를 수집하는 방법과 데이터 주체가 양식을 통해 개인 정보 보호 요청을 제출하는 방법을 알아봅니다. |

{style="table-layout:auto"}
