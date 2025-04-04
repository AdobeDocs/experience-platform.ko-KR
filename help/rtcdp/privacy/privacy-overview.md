---
keywords: 데이터 거버넌스 rtcdp;rtcdp 데이터 거버넌스;실시간 고객 데이터 프로필 데이터 거버넌스;개인정보 rtcdp;rtcdp 개인정보 보호
title: Real-Time Customer Data Platform의 개인 정보 보호
description: Adobe Real-Time Customer Data Platform을 사용하면 데이터 작업이 개인 정보 보호 규정을 준수하도록 하는 프로세스를 간소화할 수 있습니다.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Real-Time Customer Data Platform의 개인 정보 보호

[!DNL Adobe Real-Time Customer Data Platform]&#x200B;([!DNL Real-Time CDP])은(는) 마케터가 여러 엔터프라이즈 시스템의 데이터를 함께 가져와서 고객을 더 잘 식별하고 이해하고 참여할 수 있도록 지원합니다. Adobe은 소비자 데이터 개인정보 보호를 기본 디자인 원칙으로 하며 마케터가 고객의 데이터 개인정보 보호를 관리할 수 있도록 다양한 제어 기능을 제공합니다.

대부분의 [!DNL Real-Time CDP] 기능은 Adobe Experience Platform에서 제공합니다. 이 문서에서는 [!DNL Real-Time CDP]에서 지원하는 다양한 개인 정보 보호 개선 기술에 대한 정보를 제공합니다. 자세한 내용은 [!DNL Experience Platform] 설명서에 대한 링크를 참조하세요.

## 고객 액세스 및 삭제 요청 준수

[!DNL General Data Protection Regulation]&#x200B;(GDPR) 및 [!DNL California Consumer Privacy Act]&#x200B;(CCPA)과 같은 법적 개인 정보 보호 규정은 고객에게 수집된 개인 데이터에 대한 액세스 또는 삭제를 요청할 수 있는 권한을 제공합니다. [!DNL Real-Time CDP]은(는) 데이터 수집 및 저장을 위해 [!DNL Experience Platform] 기능을 활용하므로 개인 데이터 액세스 및 삭제에 대한 고객 요청은 [!DNL Experience Platform] 내에서 관리되어야 합니다. 자세한 내용은 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)의 개요를 참조하십시오.

>[!IMPORTANT]
>
> Adobe Marketo Engage용 Adobe Experience Platform Privacy Service을 통해 제출된 개인 정보 보호 요청은 Real-Time CDP B2B 고객에게만 적용됩니다.

## 옵트아웃 기능

[!DNL Real-Time CDP]을(를) 사용하면 개인 데이터를 세그먼테이션 사용 사례에 포함하는 것을 거부할 수 있습니다. 고객의 옵트아웃 환경 설정은 [!DNL Real-Time Customer Profile]에 의해 캡처 및 저장되며, 세그먼트 조건자에서 부울 논리(&quot;AND NOT&quot;)를 사용하여 대상에서 옵트아웃한 사용자를 제외하여 적용할 수 있습니다.

자세한 내용은 Adobe Experience Platform 세그멘테이션 서비스 설명서의 [옵트아웃 요청 준수](../../segmentation/tutorials/consents.md)에 대한 문서를 참조하십시오.

## IAB TCF 2.0 지원

[!DNL Real-Time CDP]은(는) [!DNL Interactive Advertising Bureau (IAB)]에 설명된 대로 [!DNL Transparency & Consent Framework (TCF)]에 대해 등록된 [공급업체 목록](https://iabeurope.eu/vendor-list-tcf/)의 일부인 Adobe Experience Platform에 빌드되어 있습니다. TCF 2.0 요구 사항을 준수하는 Experience Platform을 사용하면 자세한 고객 동의 데이터를 수집하고 이를 저장된 고객 프로필에 통합할 수 있습니다. 그런 다음 이 동의 데이터를 사용 사례에 따라 특정 프로필이 내보낸 대상에 포함되는지 여부에 팩터링할 수 있습니다.

자세한 내용은 Experience Platform의 [IAB TCF 2.0 지원에 대한 개요](../../landing/governance-privacy-security/consent/iab/overview.md)를 참조하십시오.

## 다음 단계

이 문서에서는 [!DNL Real-Time CDP]의 개인 정보 보호 기능에 대해 간략하게 소개합니다. 각 기능에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.
