---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: 실시간 고객 데이터 프로필의 개인 정보
seo-title: 실시간 고객 데이터 프로필의 개인 정보
description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 운영을 간소화할 수 있습니다.
seo-description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 운영을 간소화할 수 있습니다.
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---


# 실시간 CDP의 개인 정보 보호

[!DNL Real-time Customer Data Platform] (실시간 CDP)를 통해 마케터는 여러 엔터프라이즈 시스템의 데이터를 통합하여 고객을 보다 효과적으로 식별, 이해 및 참여시킬 수 있습니다. Adobe은 소비자 데이터 개인 정보를 기본적인 디자인 원칙에 포함하며 마케터가 고객의 데이터 개인 정보를 관리하는 데 도움이 되는 다양한 컨트롤을 제공합니다.

대부분의 실시간 CDP 기능은 Adobe Experience Platform에서 제공합니다. 이 문서에서는 실시간 CDP가 지원하는 다양한 개인 정보 보호 개선 기술에 대한 정보와 자세한 내용은 설명서에 대한 링크를 [!DNL Experience Platform] 참조하십시오.

## [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] 를 사용하면 데이터 작업을 GDPR(개인 정보 보호 규정) [!DNL General Data Protection Regulation] 및 [!DNL California Consumer Privacy Act] (CPA)와 같은 개인 정보 보호 규정을 준수하는 프로세스를 간소화할 수 있습니다. 실시간 CDP는 데이터 수집 및 스토리지 [!DNL Experience Platform] 에 대한 기능을 활용하므로 GDPR 및 CPA에 대한 액세스 및 삭제 요청은 내부에서 관리되어야 합니다 [!DNL Platform]. 서비스에 대한 자세한 내용은 [Privacy Service 개요](../../privacy-service/home.md) 문서를 참조하십시오.

고객 데이터에 액세스하고 삭제할 수 있는 개별 GDPR 및 CPA 데이터 주체의 요청을 제출하는 방법에는 두 가지가 있습니다.

* 시각적 작업 공간 [!DNL Privacy Service UI](https://gdprui.cloud.adobe.io/) 내에서 액세스 및 삭제 요청을 만들고 모니터링합니다. 단계별 지침은 [Privacy Service UI 자습서를](../../privacy-service/ui/overview.md) 참조하십시오.
* RESTful API 호출 [!DNL Privacy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) 을 사용하여 액세스 및 삭제 요청을 관리합니다. 단계별 지침은 [Privacy Service API 자습서를](../../privacy-service/api/getting-started.md) 참조하십시오.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## 다음 단계

이 문서에서는 실시간 CDP의 개인 정보 보호 기능에 대해 간략하게 소개합니다. 액세스/삭제 요청을 제출하는 우수 사례 및 단계에 대한 자세한 내용은 [Privacy Service 설명서를 참조하십시오](../../privacy-service/home.md).