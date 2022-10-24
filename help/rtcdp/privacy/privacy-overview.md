---
keywords: 데이터 거버넌스 rtcdp;rtcdp 데이터 거버넌스;실시간 고객 데이터 프로필 데이터 거버넌스;개인 정보 보호 rtcdp;rtcdp 개인 정보
title: Real-time Customer Data Platform의 개인 정보
description: Adobe Real-time Customer Data Platform을 사용하면 데이터 작업을 개인 정보 보호 규정을 준수하도록 하는 프로세스를 간소화할 수 있습니다.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Real-time Customer Data Platform의 개인 정보

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP])은 마케터가 여러 엔터프라이즈 시스템의 데이터를 함께 가져와서 고객을 더 잘 식별, 이해 및 참여시킬 수 있도록 해줍니다. Adobe은 소비자 데이터 개인 정보 보호를 기본 디자인 원칙으로 하며, 마케터가 고객의 데이터 개인 정보를 관리하는 데 도움이 되는 다양한 컨트롤을 제공합니다.

다수의 [!DNL Real-Time CDP] 기능은 Adobe Experience Platform에서 제공합니다. 이 문서에서는 [!DNL Real-Time CDP], 링크 사용 [!DNL Experience Platform] 설명서 를 참조하십시오.

## 고객 액세스 및 삭제 요청 준수

다음과 같은 법적 개인 정보 보호 규정 [!DNL General Data Protection Regulation] (GDPR) 및 [!DNL California Consumer Privacy Act] (CCPA)는 고객이 수집하는 개인 데이터에 대한 액세스 또는 삭제를 고객에게 요청할 수 있는 권한을 제공합니다. 이후 [!DNL Real-Time CDP] 활용 [!DNL Experience Platform] 데이터 수집 및 저장 기능, 고객 개인 데이터 액세스 및 삭제 요청은 [!DNL Platform]. 다음 사항에 대한 개요를 참조하십시오. [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 추가 정보.

>[!IMPORTANT]
>
> Adobe Marketo Engage용 Adobe Experience Platform Privacy Service을 통해 제출된 개인 정보 보호 요청은 Real-Time CDP B2B 고객에게만 적용됩니다.

## 옵트아웃 기능

[!DNL Real-Time CDP] 을(를) 통해 고객은 개인 데이터가 세그먼테이션 사용 사례에 포함되지 않도록 선택할 수 있습니다. 고객의 옵트아웃 환경 설정은 [!DNL Real-time Customer Profile], 및 는 세그먼트 조건부에서 부울 논리(&quot;AND NOT&quot;)를 사용하여 세그먼트에서 옵트아웃한 사용자를 제외하여 적용할 수 있습니다.

다음 문서를 참조하십시오. [옵트아웃 요청 준수](../../segmentation/consents.md) 자세한 내용은 Adobe Experience Platform 세그멘테이션 서비스 설명서 를 참조하십시오.

## IAB TCF 2.0 지원

[!DNL Real-Time CDP] Adobe Experience Platform을 기반으로 구축되었으며,는 등록된 [공급업체 목록](https://iabeurope.eu/vendor-list-tcf-v2-0/) 대상 [!DNL Transparency & Consent Framework (TCF)]에 의해 요약된 대로 [!DNL Interactive Advertising Bureau (IAB)]. Platform을 사용하면 TCF 2.0 요구 사항을 준수하여 자세한 고객 동의 데이터를 수집하여 저장된 고객 프로필에 통합할 수 있습니다. 그런 다음 사용 사례에 따라 내보낸 대상 세그먼트에 특정 프로필이 포함되는지를 이 동의 데이터를 포함할 수 있습니다.

다음 사항에 대한 개요를 참조하십시오. [Experience Platform에서 IAB TCF 2.0 지원](../../landing/governance-privacy-security/consent/iab/overview.md) 추가 정보.

## 다음 단계

이 문서에서는 [!DNL Real-Time CDP]. 각 기능에 대한 자세한 내용은 이 안내서 전체에서 에 연결된 설명서를 참조하십시오.
