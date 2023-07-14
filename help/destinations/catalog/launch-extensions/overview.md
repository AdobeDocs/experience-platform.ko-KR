---
keywords: 태그 확장;태그 확장;launch 대상;platform tag 확장;platform tag 확장;platform launch 대상
title: Adobe Experience Platform의 태그 확장
description: Adobe Experience Platform은 Adobe의 차세대 태그 관리 기능을 제공합니다. Platform은 관련 고객 환경을 향상시키는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 제공합니다.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Adobe Experience Platform의 태그 확장

Adobe Experience Platform은 Adobe의 차세대 태그 관리 기능을 제공합니다. Platform은 관련 고객 환경을 향상시키는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 제공합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다.

태그에 대한 소개는 아래 리소스를 참조하십시오.

- [태그 개요](../../../tags/home.md)
- [빠른 시작 안내서](../../../tags/quick-start/quick-start.md)

## Platform 인터페이스에서 태그 확장을 찾는 방법 {#how-to-find-extensions-in-interface}

Platform 인터페이스에서 확장을 찾으려면 다음을 찾아 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 및 선택 **[!UICONTROL 확장]** 다음에서 **[!UICONTROL 유형]** 필터.

![인터페이스의 확장 필터](../../assets/catalog/launch-extensions/filter.png)

## 태그 확장 작동 방식 {#how-extensions-work}

A [태그 확장](../../../tags/home.md#extensions) 는 웹 사이트 또는 모바일 앱의 기능을 향상시키는 코드 패키지입니다. 여기에는 다음과 같은 대상에 원시 이벤트 데이터 전송이 포함될 수 있습니다 [Google Analytics](/help/destinations/catalog/analytics/google-universal-analytics.md) 하지만 다른 기능도 사용할 수 있습니다.

태그와 이벤트 전달 확장을 구분하는 것이 중요합니다. 플랫폼 대상 사용자 인터페이스에 표시되는 확장은 다음과 같습니다 *태그 확장*. 자세한 내용은 이벤트 전달 개요를 참조하십시오. [태그와 이벤트 전달 간의 차이점](/help/tags/ui/event-forwarding/overview.md#differences-between-event-forwarding-and-tags).



<!--

Extensions forward raw event data to several types of destinations. Think of extensions as an **Event Forwarding** type of destination. This is a simpler type of integration with destination platforms, which only forwards raw event data. Examples of those are the [Gainsight personalization extension](../personalization/gainsight.md) or the [Confirmit Voice of the Customer extension](../voice/confirmit-digital-feedback.md).

**Profile/Segment Export** destinations in Adobe Experience Platform capture event data, combine it with other data sources, apply segmentation, and export audiences and qualified profiles to destinations. Examples of those are the [Amazon S3 cloud storage destination](../cloud-storage/amazon-s3.md) or the [Google Display & Video 360 advertising destination](../advertising/google-dv360.md).

![Tag extensions compared to other destinations](../../assets/common/launch-and-other-destinations.png)

-->

## 태그 확장 사용의 이점 {#extensions-benefits}

기존 Experience Cloud 고객은 플랫폼의 태그 기능을 무료로 사용할 수 있습니다. 이 시스템은 설치, 구성, 업데이트 및 삭제할 수 있는 사용하기 쉬운 확장을 통해 웹 사이트에서의 태그 배포를 단순화합니다. 태그는 웹 사이트에 작은 공간을 남겨 두므로 페이지를 빠르게 로드할 수 있습니다.

태그 확장에 대해 대상을 활성화할 수 없지만, 특정 상황에서 이벤트 데이터만 전달하도록 규칙을 설정할 수 있습니다. 이 강력한 기능을 사용하면 모든 상호 작용에 이벤트 데이터를 보내는 것이 아니라 특정 상황에서만 이벤트 데이터를 전달할 수 있습니다. 자세한 내용은 의 규칙에 대해 참조하십시오. [태그 설명서](../../../tags/ui/managing-resources/rules.md).

## 확장에 대한 예제 사용 사례 {#extensions-use-cases}

확장을 사용하면 다양한 고객 사용 사례를 충족할 수 있습니다. 확장을 사용하는 몇 가지 사용 사례는 다음과 같습니다.

- facebook 픽셀 확장을 통해 웹 사이트 또는 기본 앱 데이터를 Facebook으로 보낼 수 있습니다. Facebook 픽셀은 방문자가 탐색한 사이트 또는 앱의 일부를 나타내며 해당 정보를 Facebook에 전달합니다. 사용자는 Facebook을 통해 방문자를 재타겟팅할 수 있습니다.
- 웹 사이트 및 앱의 이벤트 데이터를 Google Analytics에 전달하여 해당 데이터를 기반으로 분석하고 결정을 내릴 수 있습니다.
- 사용자가 설정한 규칙에 따라 페이지와 상호 작용하는 방법에 따라 클라이언트측 챗박스 앱을 적시에 켤 수 있습니다.

## 확장 범주 {#extension-categories}

확장은 Platform에서 다음 카테고리에 속할 수 있습니다.

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [데이터 관리 플랫폼](../data-management/overview.md)
- [이메일 마케팅 대상](../email-marketing/overview.md)
- [개인화](../personalization/overview.md)
- [설문 조사](../survey/overview.md)
- [고객의 소리](../voice/overview.md)
