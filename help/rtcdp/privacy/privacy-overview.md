---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: 실시간 고객 데이터 프로필의 개인 정보
seo-title: 실시간 고객 데이터 프로필의 개인 정보
description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 운영을 간소화할 수 있습니다.
seo-description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 운영을 간소화할 수 있습니다.
translation-type: tm+mt
source-git-commit: bdd80b15258bf4e3c0dee1e260fd3469c76d5885
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---


# 개인 정보 보호 [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) 마케터는 여러 엔터프라이즈 시스템의 데이터를 통합하여 고객을 보다 효과적으로 식별, 이해 및 참여시킬 수 있습니다. Adobe은 소비자 데이터 개인 정보를 기본적인 디자인 원칙에 포함하며 마케터가 고객의 데이터 개인 정보를 관리하는 데 도움이 되는 다양한 컨트롤을 제공합니다.

대다수의 [!DNL Real-time CDP] 역량은 Adobe Experience Platform이 한다. 이 문서에서는 에서 지원하는 다양한 개인정보 보호 강화 기술에 대한 정보 [!DNL Real-time CDP]와 자세한 내용은 설명서 링크 [!DNL Experience Platform] 를 참조하십시오.

## 고객 액세스 및 삭제 요청 준수

GDPR [!DNL General Data Protection Regulation] (Adobe Certified Document Services) 및 [!DNL California Consumer Privacy Act] (CPA)와 같은 법적 개인 정보 보호 규정에서는 고객이 수집한 개인 데이터의 액세스 또는 삭제를 요청할 수 있습니다. 데이터 수집 및 저장에 대한 [!DNL Real-time CDP] 기능을 활용하므로 고객 개인 정보에 액세스하거나 삭제하기 위한 요청은 내부에서 관리되어야 [!DNL Experience Platform] [!DNL Platform]합니다. 자세한 내용은 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) 개요를 참조하십시오.

## 옵트아웃 기능

[!DNL Real-time CDP] 세그멘테이션 사용 사례에 고객 개인 데이터 포함 거부 고객의 옵트아웃 환경 설정은 에 의해 캡처되고 저장되며, 세그먼트 설명 [!DNL Real-time Customer Profile]에서 부울 논리(&quot;AND NOT&quot;)를 사용하여 세그먼트에서 옵트아웃한 사용자를 제외하여 적용할 수 있습니다.

자세한 내용은 Adobe Experience Platform 세그멘테이션 서비스 문서의 [옵트아웃 요청](../../segmentation/honoring-opt-outs.md) 수리에 관한 문서를 참조하십시오.

## IAB TCF 2.0 지원

[!DNL Real-time CDP] 은 에 대한 등록된 [공급업체 목록](https://iabeurope.eu/vendor-list-tcf-v2-0/) 중 [!DNL Transparency & Consent Framework (TCF)]에 포함되어 있으며, 에 나와 [!DNL Interactive Advertising Bureau (IAB)]있습니다. TCF 2.0 요구 사항을 준수하여 자세한 고객 동의 데이터를 수집하여 저장된 고객 프로파일에 통합할 수 [!DNL Real-time CDP] 있습니다. 그런 다음 이 동의 데이터를 사용 사례에 따라 내보낸 대상 세그먼트에 특정 프로필이 포함되는지 여부를 고려시킬 수 있습니다.

자세한 내용은 IAB [TCF 2.0 지원에 [!DNL Real-time CDP]](./iab/overview.md) 대한 개요를 참조하십시오.

## 다음 단계

이 문서는 개인정보 보호 기능에 대한 간단한 소개를 제공합니다 [!DNL Real-time CDP]. 각 기능에 대한 자세한 내용은 이 안내서 전체에 연결된 설명서를 참조하십시오.