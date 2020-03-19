---
title: 실시간 고객 데이터 프로필의 개인 정보
seo-title: 실시간 고객 데이터 프로필의 개인 정보
description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 작업을 간소화할 수 있습니다.
seo-description: 실시간 고객 데이터 프로필을 사용하면 개인 정보 보호 규정을 준수하는 데이터 작업을 간소화할 수 있습니다.
translation-type: tm+mt
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# 실시간 CDP의 개인 정보 보호

실시간 고객 데이터 플랫폼(실시간 CDP)을 통해 마케터는 여러 엔터프라이즈 시스템의 데이터를 취합하여 고객을 보다 효과적으로 식별, 이해 및 참여시킬 수 있습니다. Adobe는 소비자 데이터 개인 정보를 기본 디자인 원칙으로 삼고 마케터가 고객의 데이터 개인 정보를 관리하는 데 도움이 되는 다양한 제어 기능을 제공합니다.

실시간 CDP 기능 중 대부분은 Adobe Experience Platform을 기반으로 합니다. 이 문서에서는 실시간 CDP에서 지원하는 다양한 개인 정보 보호 강화 기술에 대한 정보와 Experience Platform 설명서 링크를 통해 자세한 내용을 살펴볼 수 있습니다.

## 개인 정보 서비스

Adobe Experience Platform Privacy Service를 사용하면 개인 정보 보호 규정(GDPR) 및 CCPA(California Consumer Privacy Act)와 같은 개인 정보 보호 규정을 준수하는 데이터 운영을 간소화할 수 있습니다. 실시간 CDP는 데이터 수집 및 스토리지를 위한 경험 플랫폼 기능을 활용하므로 GDPR 및 CPA에 대한 액세스 및 삭제 요청은 플랫폼에서 관리해야 합니다. 서비스에 [대한 자세한 내용은 개인정보 보호 서비스 개요](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) 문서를 참조하십시오.

고객 데이터에 액세스하고 삭제할 수 있도록 개별 GDPR 및 CPA 데이터 주체의 요청을 제출하는 방법에는 두 가지가 있습니다.

* 개인 정보 [서비스 UI를](https://gdprui.cloud.adobe.io/) 사용하여 시각적 작업 영역 내에서 액세스 및 삭제 요청을 만들고 모니터링합니다. 단계별 지침은 [개인정보 보호 서비스 UI 자습서를](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) 참조하십시오.
* 개인정보 보호 서비스 [API를](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) 사용하여 RESTful API 호출을 사용하여 액세스 및 삭제 요청을 관리합니다. 단계별 지침은 [개인정보 보호 서비스 API 자습서를](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md) 참조하십시오.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## 다음 단계

이 문서에서는 실시간 CDP의 개인 정보 보호 기능에 대해 간략하게 소개합니다. 액세스/삭제 요청을 제출하는 모범 사례 및 단계에 대한 자세한 내용은 개인 정보 서비스 [설명서를](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html)참조하십시오.