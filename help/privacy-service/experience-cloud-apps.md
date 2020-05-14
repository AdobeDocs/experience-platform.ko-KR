---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개인정보 보호 서비스 및 Experience Cloud 응용 프로그램
topic: overview
translation-type: tm+mt
source-git-commit: f4a007b66806cb0d322226e1e1837cfce7ca4095
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 14%

---


# 개인정보 보호 서비스 및 Experience Cloud 응용 프로그램

Adobe Experience Platform Privacy Service는 여러 Adobe Experience Cloud 응용 프로그램에 대한 개인정보 보호 요청을 지원하기 위해 구축되었습니다. 각 애플리케이션은 데이터 주체 식별을 위해 서로 다른 제품 값과 ID를 지원합니다.

이 문서는 개인정보 보호 관련 작업을 위해 해당 응용 프로그램을 구성하는 방법에 대한 개요를 설명하는 Experience Cloud 응용 프로그램 문서에 대한 참조로서 사용됩니다. 여기에는 데이터의 형식을 지정하고 레이블을 지정하는 방법이 포함됩니다. 두 가지 애플리케이션 범주는 다음과 같습니다.

* [개인정보 보호 서비스와 통합된 애플리케이션](#integrated): 개인정보 보호 서비스에 액세스, 삭제 또는 수신 거부 요청을 전송할 수 있는 응용 프로그램입니다.
* [셀프 서비스 애플리케이션](#self-serve): 개인정보 보호 요청을 내부적으로 관리해야 하며 개인정보 보호 서비스와 직접 통신할 수 없는 응용 프로그램입니다.

Experience Cloud 응용 프로그램의 설명서를 검토하여 개인정보 보호 요청의 형식 지정 방법 및 이러한 요청에 대해 지원되는 값을 확인하십시오.

## 개인정보 보호 서비스와 통합된 애플리케이션 {#integrated}

다음은 Privacy Service와 통합된 Experience Cloud 응용 프로그램 목록(호환되는 개인정보 보호 서비스 기능 및 문서 링크 포함)입니다.

| 애플리케이션 | 액세스/삭제 | 판매 거부 | 설명서 및 고려 사항 |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>Adobe Advertising Cloud는 Adobe 개인 정보 보호 센터에서 제공하는 기존의 글로벌 옵트아웃 기능을 활용합니다. 자세한 내용은 데이터 개인 정보 [보호 요청에](https://docs.adobe.com/content/help/ko-KR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) 대한 가이드를 참조하십시오.</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>Analytics는 [개인 정보 보고 변수를 사용하여 옵트아웃 요청을 처리합니다.](https://docs.adobe.com/content/help/ko-KR/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://docs.adobe.com/content/help/ko-KR/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[옵트아웃 설명서](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[설명서 액세스/삭제](https://docs.campaign.adobe.com/doc/standard/getting_started/en/ACS_GDPR.html)</li><li>[옵트아웃 설명서](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe 고객 속성(CRS) | ✓ | N/A | <ul><li>[GDPR 문서 액세스/삭제](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/gdpr.html)</li><li>[CPA용 문서 액세스/삭제](https://docs.adobe.com/content/help/en/core-services/interface/customer-attributes/ccpa.html)</li><li>고객 속성에는 데이터를 전송할 수 있는 기능이 없으므로 판매 거부 요청은 적용되지 않습니다.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Data Lake에 대한 문서 액세스/삭제](../catalog/privacy.md)</li><li>[실시간 고객 프로파일에 대한 문서 액세스/삭제](../profile/privacy.md)</li><li>경험 플랫폼은 대상 세그먼트에 대한 [옵트아웃 요청을 처리합니다](../segmentation/honoring-opt-outs.md).</li></ul> |
| Adobe Primetime 인증 | ✓ | N/A | <ul><li>[설명서 액세스/삭제](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Primetime에는 데이터를 전송할 수 있는 기능이 없으므로 판매 거부 요청은 적용되지 않습니다.</li></ul> |
| Adobe Target | ✓ | N/A | <ul><li>[설명서 액세스/삭제](https://docs.adobe.com/content/help/ko-KR/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>Target에는 데이터를 전송할 수 있는 기능이 없으므로 판매 거부 요청을 적용할 수 없습니다.</li></ul> |


## 셀프 서비스 애플리케이션 {#self-serve}

다음은 개인정보 보호 서비스와 통합되지 않으며 내부적으로 개인정보 보호 문제를 관리해야 하는 Experience Cloud 응용 프로그램 목록입니다. 각 응용 프로그램의 설명서에 대한 링크와 설명서 내용에 대한 설명이 제공됩니다.

| 애플리케이션 | 설명서 설명 |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/ACC_GDPR.html) | Adobe Campaign Classic의 GDPR 기능에 대한 개요입니다. |
| [Adobe 다이내믹 태그 관리자](https://docs.adobe.com/content/help/en/dtm/using/tools/opt-in.html) | Adobe 태그가 동의를 받을 때까지 실행되지 않도록 하는 절차. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | 고객 개인 정보 관리자 또는 AEM 관리자가 GDPR 요청을 처리하는 방법에 대한 개요입니다. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Livefyre를 사용하여 GDPR 액세스 및 요청 삭제 절차 |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | 개발자가 확장 프로그램 및 규칙 작성기를 사용하여 옵트인 및 옵트아웃 솔루션을 정의할 수 있는 방법입니다. |
