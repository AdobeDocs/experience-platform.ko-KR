---
keywords: 시작 확장;시작 확장;시작 대상;launch extensions;launch destination;플랫폼 실행 확장;플랫폼 시작 확장;플랫폼 시작 대상
title: Experience Platform Launch 확장
seo-title: Experience Platform Launch 확장
description: Launch는 Adobe의 차세대 태그 관리 기능입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.
seo-description: Launch는 Adobe의 차세대 태그 관리 기능입니다. Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 19%

---


# Adobe Experience Platform Launch 확장 {#overview.md}

Adobe Experience Platform Launch은 Adobe의 차세대 태그 관리 기능입니다. Platform Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다. Platform Launch는 Adobe Experience Cloud 고객에게 부가 가치 기능으로 제공됩니다.

Experience Platform Launch 기능에 대한 소개는 아래 리소스를 참조하십시오.
- Adobe Experience Platform Launch [설명서](https://experienceleague.adobe.com/docs/launch/using/overview.html)
- Adobe Experience Platform Launch [빠른 시작 비디오](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). [Adobe Experience Platform Launch 소개](https://www.youtube.com/embed/rwqqkG1SERU) 및 [게시 프로세스 개요](https://helpx.adobe.com/kr/analytics/how-to/adobe-launch-publishing-process.html)로 시작한 다음 다음 개념으로 이동합니다.

## 플랫폼 인터페이스 {#how-to-find-extensions-in-interface}에서 플랫폼 시작 확장을 찾는 방법

플랫폼 시작 확장 기능을 플랫폼 인터페이스에서 찾으려면 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동하고 **[!UICONTROL 유형]** 필터에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다.

![인터페이스의 확장 필터](../../assets/catalog/launch-extensions/filter.png)

## 플랫폼 시작 확장 작동 방식 {#how-extensions-work}

플랫폼 시작 익스텐션은 원시 이벤트 데이터를 여러 유형의 대상으로 전달합니다. 확장을 대상의 **이벤트 전달** 유형으로 생각해 보십시오. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 이러한 예로는 [Gainsight 개인화 확장](../personalization/gainsight.md) 또는 고객 확장](../voice/confirmit-digital-feedback.md)의 [확인 음성이 있습니다.

**Adobe Experience Platform의 프로필/** 세그먼트 내보내기 대상(Profile/Segment Exporttarget)은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하고, 세그먼트 및 자격이 있는 프로파일을 대상에 내보낼 수 있습니다. 이러한 예로는 [Amazon S3 클라우드 스토리지 대상](../cloud-storage/amazon-s3.md) 또는 [Google 디스플레이 및 비디오 360 광고 대상](../advertising/google-dv360.md)이 있습니다.

![다른 대상과 Experience Platform Launch 확장](../../assets/common/launch-and-other-destinations.png)

## 플랫폼 시작 확장 사용 이점 {#extensions-benefits}

Adobe Experience Platform Launch은 기존 Experience Cloud 고객에게 무료로 제공됩니다. Platform Launch를 사용하면 설치, 구성, 업데이트 및 삭제할 수 있는 간편한 익스텐션을 통해 웹 사이트에 태그 배포를 간소화할 수 있습니다. Platform Launch는 웹 사이트에서 적은 풋프린트를 제공하므로 페이지를 신속하게 로드할 수 있습니다.

>[!IMPORTANT]
>
>세그먼트를 플랫폼 시작 확장 기능에 활성화할 수는 없지만 특정 상황에서 이벤트 데이터만 전달하도록 규칙을 설정할 수 있습니다. 아래에서 자세히 살펴보십시오.

이벤트 데이터를 확장으로 전달하는 시기를 결정하는 *규칙*&#x200B;을 만들 수 있습니다. 이 강력한 기능을 사용하면 모든 상호 작용에 대한 이벤트 데이터를 보내는 대신 특정 상황에서 이벤트 데이터만 전달할 수 있습니다. 자세한 내용은 [Adobe Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)의 규칙에 대해 참조하십시오.

## 플랫폼 시작 확장 {#extensions-use-cases}에 대한 사용 사례 예

Platform Launch 익스텐션을 사용하면 다양한 고객 사례를 충족할 수 있습니다. 플랫폼 실행 확장 사용에 대한 일부 사용 사례는 다음과 같습니다.

- Facebook 픽셀 확장 기능을 통해 웹 사이트 또는 기본 앱 데이터를 Facebook으로 보낼 수 있습니다. Facebook 픽셀은 방문자가 탐색한 사이트 또는 앱의 일부를 나타내며, 해당 정보를 Facebook으로 전달하며, Facebook을 통해 방문자를 재타깃팅할 수 있습니다.
- 웹 사이트 및 앱의 이벤트 데이터를 Google Analytics으로 전달하여 해당 데이터를 분석하고 결정할 수 있습니다.
- Platform Launch에서 설정한 규칙에 따라, 사용자가 페이지와 상호 작용하는 방법을 기반으로 적시에 클라이언트측 채팅 박스 앱을 활성화할 수 있습니다.

## 확장 카테고리 {#extension-categories}

플랫폼 시작 확장 기능은 플랫폼에서 다음 카테고리에 포함될 수 있습니다.

- [광고](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [데이터 관리 플랫폼](../data-management/overview.md)
- [이메일 마케팅 대상](../email-marketing/overview.md)
- [개인화](../personalization/overview.md)
- [설문 조사](../survey/overview.md)
- [고객의 소리](../voice/overview.md)
