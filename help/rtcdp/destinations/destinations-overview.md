---
title: 대상 개요
seo-title: 대상 개요
description: 대상은 실시간 고객 데이터 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. Adobe의 실시간 고객 데이터 플랫폼에서 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례를 위해 알려진 알 수 없는 데이터를 활성화할 수 있습니다.
seo-description: 대상은 실시간 고객 데이터 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. Adobe의 실시간 고객 데이터 플랫폼에서 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례를 위해 알려진 알 수 없는 데이터를 활성화할 수 있습니다.
translation-type: tm+mt
source-git-commit: e66f4df13afb3c9f9ddb440ccb5e479caeef2142

---


# 대상 개요

![대상 개요 배너](/help/rtcdp/destinations/assets/destinations-overview-banner.png)

**대상은** 대상 플랫폼과 사전 구축된 통합으로 실시간 고객 데이터 플랫폼에서 데이터를 원활하게 활성화할 수 있습니다. 대상을 사용하여 **크로스채널** 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 많은 사용 사례를 위해 알려진 데이터 및 알 수 없는 데이터를 활성화할 수 있습니다.

## 대상 및 소스

실시간 CDP의 핵심 기능 중 하나는 자사 데이터를 수집하여 비즈니스 요구에 맞게 활성화하는 것입니다. 데이터를 **[!UICONTROL Sources]** 실시간 CDP로 인제스트하고 실시간 CDP에서 데이터를 내보낼 **[!UICONTROL Destinations]** 수 있습니다.

## 대상 단계

* 프로필 또는 세그먼트를 **[!UICONTROL Destinations]** 활성화하고 [](/help/rtcdp/destinations/activate-destinations.md) 마케팅 자동화 플랫폼, 디지털 광고 플랫폼 등으로 보낼 수 있습니다.
* 실시간 CDP에서 사용할 수 있는 모든 대상의 [셀프 서비스 카탈로그](/help/rtcdp/destinations/destinations-catalog.md) 중에서 선택할 수 있습니다.
* 데이터 내보내기를 주기적으로 원하는 대상으로 예약합니다.

## 컨트롤

대상 작업 [영역의](/help/rtcdp/destinations/destinations-workspace.md) 컨트롤을 사용하여 다음을 수행할 수 있습니다.

* 데이터를 활성화할 수 있는 대상 플랫폼 카탈로그를 찾아봅니다.
* 카탈로그의 대상에 대한 데이터 흐름 만들기, 편집, 활성화 및 비활성화
* 스토리지 위치에 계정을 만들거나 타겟 플랫폼의 계정에 실시간 CDP 연결
* 대상에 활성화할 세그먼트를 선택합니다.
* 세그먼트를 이메일 [마케팅 대상으로 활성화할 때 내보낼 경험 데이터 모델(XDM) 필드를](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/xdm_system/xdm_system_in_experience_platform.md) 선택합니다.

## 대상 유형 및 카테고리 - 비디오 개요

Adobe Real-time CDP에는 프로파일 내보내기 대상 및 세그먼트 내보내기 대상 두 가지 유형이 있습니다. 아래 비디오에서는 두 가지 유형의 대상에 대해 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29707?quality=12)

### 프로필 내보내기 대상

프로필 내보내기 대상은 프로필 및/또는 속성이 포함된 파일을 생성합니다. 이러한 대상은 종종 이메일 주소와 함께 원시 데이터를 사용합니다.

### 세그먼트 내보내기 대상

세그먼트 내보내기 대상은 자격이 있는 프로필과 세그먼트를 보냅니다. 이러한 대상은 세그먼트 ID 또는 사용자 ID를 사용합니다.

### 대상 카테고리

대상 카탈로그의 [대상은 대상 카테고리(](/help/rtcdp/destinations/destinations-catalog.md) 광고&#x200B;**,**&#x200B;클라우드 **스토리지**, **이메일**&#x200B;마케팅또는이메일 마케팅)별로 그룹화됩니다. 각 대상에 대한 자세한 내용은 대상 카탈로그를 [참조하십시오](/help/rtcdp/destinations/destinations-catalog.md).

## 대상 및 액세스 제어

실시간 CDP의 **[!UICONTROL Destinations]** 기능은 Adobe Experience Platform 액세스 제어 권한과 연동됩니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. 개별 권한에 대한 자세한 내용은 [Adobe Experience Platform의](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-overview.md) 액세스 제어를 참조하고 페이지 아래쪽으로 스크롤을 참조하십시오.

액세스 컨트롤에 대한 자세한 내용은 액세스 [제어 사용 안내서를](https://www.adobe.io/apis/experienceplatform/home/permissions-and-sandboxes/permissions-and-sandboxes.html#!api-specification/markdown/narrative/technical_overview/access-control/access-control-user-guide.md)참조하십시오.