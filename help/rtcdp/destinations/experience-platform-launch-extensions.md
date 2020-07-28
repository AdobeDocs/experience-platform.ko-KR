---
title: Experience Platform Launch 확장
seo-title: Experience Platform Launch 확장
description: Launch는 Adobe의 차세대 태그 관리 기능입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.
seo-description: Launch는 Adobe의 차세대 태그 관리 기능입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.
translation-type: tm+mt
source-git-commit: 98c3356db178507e0a8d94b47030e9490e721e46
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 21%

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch는 Adobe의 차세대 태그 관리 기능입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다. Launch는 Adobe Experience Cloud 고객에게 부가가치 기능으로 제공됩니다.

Experience Platform Launch 기능에 대한 자세한 내용은 아래 리소스를 참조하십시오.
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/ko-KR/launch/using/overview.html)
* Experience Platform Launch [빠른 시작 비디오](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html). Experience Platform Launch [소개](https://www.youtube.com/embed/rwqqkG1SERU) 및 [퍼블리싱 프로세스](https://helpx.adobe.com/kr/analytics/how-to/adobe-launch-publishing-process.html)개요로 시작한 다음 다음 개념으로 이동합니다.

## Adobe 실시간 CDP 인터페이스에서 Launch 익스텐션을 찾는 방법 {#how-to-find-extensions-in-interface}

Adobe 실시간 CDP 인터페이스에서 Launch 익스텐션을 찾으려면 **[!UICONTROL 대상 > 카탈로그]** 로 이동하고 **[!UICONTROL 유형]** 필터에서 **[!UICONTROL 익스텐션]** 을선택합니다.

![인터페이스의 확장 필터](/help/rtcdp/destinations/assets/extensions-filter.png)

## 실행 확장 기능 작동 방식 {#how-extensions-work}

익스텐션을 실행하면 원시 이벤트 데이터를 여러 유형의 대상으로 전달할 수 있습니다. 익스텐션을 대상의 **이벤트 전달** 유형으로 간주합니다. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 이러한 예는 [Gainsight 개인화 확장](/help/rtcdp/destinations/gainsight-extension.md) 또는 [고객 확장의 확인 음보입니다](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

**Adobe의 프로필/세그먼트 내보내기** 대상 실시간 고객 데이터 Platform은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하고, 세그먼트 및 자격이 있는 프로필을 대상에 내보냅니다. 이러한 예로는 [Amazon S3 클라우드 스토리지 대상](/help/rtcdp/destinations/amazon-s3-destination.md) 또는 [Google 디스플레이 및 비디오 360 광고 대상이 있습니다](/help/rtcdp/destinations/google-dv360-destination.md).

![다른 대상과 Experience Platform Launch 확장](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Launch 익스텐션의 이점 {#extensions-benefits}

Experience Platform Launch은 기존 Experience Cloud 고객에게 무료로 제공됩니다. Launch를 사용하면 설치, 구성, 업데이트 및 삭제할 수 있는 편리한 확장 기능을 통해 웹 사이트에 태그 배포를 간소화할 수 있습니다. Launch는 웹 사이트에서 적은 풋프린트를 제공하므로 페이지를 빠르게 로드할 수 있습니다.

>[!IMPORTANT]
>
>세그먼트를 실행 확장 기능에 활성화할 수는 없지만 특정 상황에서 이벤트 데이터만 전달하도록 규칙을 설정할 수 있습니다. 자세한 내용을 살펴보십시오.

이벤트 데이터를 익스텐션으로 전달할 시기를 결정하는 *규칙을* 만들 수 있습니다. 이 강력한 기능을 사용하면 모든 상호 작용에 대해 이벤트 데이터를 보내는 것과 반대로 특정 상황에서만 이벤트 데이터를 전달할 수 있습니다. 자세한 내용은 [론치 설명서에서 규칙에 대해 참조하십시오](https://docs.adobe.com/help/ko-KR/launch/using/reference/manage-resources/rules.html).

## 실행 확장 사용 사례 예 {#extensions-use-cases}

Launch extensions를 사용하면 다양한 고객 사례를 충족할 수 있습니다. 론치 확장 사용 사례 중 일부는 다음과 같습니다.

* Facebook 픽셀 확장 기능을 통해 웹 사이트 또는 기본 앱 데이터를 Facebook으로 보낼 수 있습니다. Facebook 픽셀: 방문자가 탐색한 사이트 또는 앱의 일부 또는 해당 정보를 Facebook으로 전달하며 Facebook을 통해 방문자를 재타깃팅할 수 있습니다.
* 웹 사이트 및 앱의 이벤트 데이터를 Google Analytics으로 전달하여 분석 및 해당 데이터를 기반으로 의사 결정을 내릴 수 있습니다.
* Launch에서 설정한 규칙에 따라 사용자가 페이지와 상호 작용하는 방법을 기반으로 적시에 클라이언트측 채팅 박스 앱을 활성화할 수 있습니다.


## 확장 카테고리 {#extension-categories}

실행 익스텐션은 실시간 CDP Adobe에서 다음과 같은 범주로 분류될 수 있습니다.

* [광고](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [데이터 관리 Platform](/help/rtcdp/destinations/dmp-destinations.md)
* [이메일 마케팅 대상](/help/rtcdp/destinations/email-marketing-destinations.md)
* [개인화](/help/rtcdp/destinations/personalization-destinations.md)
* [설문 조사](/help/rtcdp/destinations/survey-destinations.md)
* [고객의 소리](/help/rtcdp/destinations/voice-of-customer-destinations.md)
