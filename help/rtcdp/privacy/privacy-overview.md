---
keywords: 데이터 거버넌스 rtcdp;rtcdp 데이터 거버넌스;실시간 고객 데이터 프로필 데이터 거버넌스;개인 정보 rtcdp;rtcdp privacy
title: 실시간 고객 데이터 프로필의 개인 정보
seo-title: 실시간 고객 데이터 프로필의 개인 정보
description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 작업을 간소화할 수 있습니다.
seo-description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 작업을 간소화할 수 있습니다.
translation-type: tm+mt
source-git-commit: 49c984a60fd699706eec508ec1d786340df40b57
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# [!DNL Real-time CDP]의 개인 정보

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]마케터는 여러 엔터프라이즈 시스템의 데이터를 통합하여 고객을 보다 효과적으로 식별, 이해 및 참여시킬 수 있습니다. Adobe은 소비자 데이터 개인 정보를 기본적인 디자인 원칙으로서 보유하고 있으며 마케터가 고객의 데이터 개인 정보를 관리하는 데 도움이 되는 다양한 제어 기능을 제공합니다.

대부분의 [!DNL Real-time CDP] 기능은 Adobe Experience Platform에서 제공합니다. 이 문서에서는 [!DNL Real-time CDP]에서 지원하는 다양한 개인정보 보호 강화 기술에 대한 정보와 자세한 내용은 [!DNL Experience Platform] 설명서에 대한 링크를 제공합니다.

## 고객 액세스 및 삭제 요청 준수

[!DNL General Data Protection Regulation](GDPR) 및 [!DNL California Consumer Privacy Act](CPA)과 같은 법적 개인 정보 보호 규정은 고객이 자신에게 수집하는 개인 정보에 대한 액세스 또는 삭제를 요청할 수 있는 권한을 부여합니다. [!DNL Real-time CDP]은 데이터 수집 및 저장에 대해 [!DNL Experience Platform] 기능을 활용하므로, 고객 액세스 및 삭제에 대한 요청은 [!DNL Platform] 내에서 관리해야 합니다. 자세한 내용은 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)의 개요를 참조하십시오.

## 옵트아웃 기능

[!DNL Real-time CDP] 고객은 세그멘테이션 사용 사례에 자신의 개인 데이터를 포함시키지 않도록 선택할 수 있습니다. 고객의 옵트아웃 환경 설정은 [!DNL Real-time Customer Profile]에서 캡처 및 저장되며, 세그먼트 조건자에서 부울 논리(&quot;AND NOT&quot;)를 사용하여 세그먼트에서 옵트아웃한 사용자를 제외하여 적용할 수 있습니다.

자세한 내용은 Adobe Experience Platform 세그멘테이션 서비스 문서의 [수신 거부 요청](../../segmentation/honoring-opt-outs.md)에 대한 문서를 참조하십시오.

## IAB TCF 2.0 지원

[!DNL Real-time CDP] 는 Adobe Experience Platform을 기반으로 하며, 이 [ ](https://iabeurope.eu/vendor-list-tcf-v2-0/)   [!DNL Transparency & Consent Framework (TCF)]  [!DNL Interactive Advertising Bureau (IAB)]는 TCF 2.0 요구 사항을 준수하는 Platform을 사용하면 고객의 세부 동의 데이터를 수집하여 저장된 고객 프로파일에 통합할 수 있습니다. 그런 다음 사용 사례에 따라 특정 프로필이 내보낸 대상 세그먼트에 포함되는지 여부를 결정하도록 이 동의 데이터를 고려할 수 있습니다.

자세한 내용은 Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md)의 [IAB TCF 2.0 지원에 대한 개요를 참조하십시오.

## 다음 단계

이 문서에서는 [!DNL Real-time CDP]의 개인정보 보호 기능에 대해 간략하게 소개합니다. 각 기능에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.