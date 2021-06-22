---
keywords: launch 확장;launch 확장;launch 대상platform launch 확장;platform launch 확장;platform launch 대상
title: Adobe Experience Platform Launch 확장
description: Adobe Experience Platform Launch은 Adobe의 차세대 태그 관리 기능입니다. Platform Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 20a9103dd96116f3099bccc9eeb678be5ac2bb79
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 12%

---

# Adobe Experience Platform Launch 확장

Adobe Experience Platform Launch은 Adobe의 차세대 태그 관리 기능입니다. Platform Launch는 관련 고객 환경을 향상하는 데 필요한 모든 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다. platform launch은 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다.

Experience Platform Launch 기능에 대한 소개는 아래 리소스를 참조하십시오.

- Adobe Experience Platform Launch [설명서](https://experienceleague.adobe.com/docs/launch/using/home.html)
- Adobe Experience Platform Launch [빠른 시작 비디오](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?) [Adobe Experience Platform Launch 소개](https://www.youtube.com/embed/rwqqkG1SERU) 및 [게시 프로세스 개요](https://helpx.adobe.com/kr/analytics/how-to/adobe-launch-publishing-process.html)로 시작한 다음 다음 개념으로 이동합니다.

## 플랫폼 인터페이스에서 Platform launch 확장을 찾는 방법 {#how-to-find-extensions-in-interface}

플랫폼 인터페이스에서 Platform launch 확장을 찾으려면 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동한 다음 **[!UICONTROL 유형]** 필터에서 **[!UICONTROL 확장]**&#x200B;을 선택하십시오.

![인터페이스의 확장 필터](../../assets/catalog/launch-extensions/filter.png)

## platform launch 확장 작동 방식 {#how-extensions-work}

platform launch 확장은 원시 이벤트 데이터를 여러 유형의 대상에 전달합니다. 확장을 대상의 **이벤트 전달** 유형으로 간주합니다. 이는 원시 이벤트 데이터만 전달하는 대상 플랫폼과의 단순한 통합 유형입니다. 그 예로는 [Gainsight 개인화 확장](../personalization/gainsight.md) 또는 고객 확장](../voice/confirmit-digital-feedback.md)의 [확인 음성이 있습니다.

**Adobe Experience Platform** 의 프로필/세그먼트 내보내기 대상은 이벤트 데이터를 캡처하고, 다른 데이터 소스와 결합하고, 세그멘테이션을 적용하고, 세그먼트와 자격이 있는 프로필을 대상으로 내보냅니다. 그 예로는 [Amazon S3 클라우드 스토리지 대상](../cloud-storage/amazon-s3.md) 또는 [Google Display &amp; Video 360 광고 대상](../advertising/google-dv360.md)이 있습니다.

![다른 대상과 비교 Experience Platform Launch 확장](../../assets/common/launch-and-other-destinations.png)

## platform launch 확장 {#extensions-benefits} 을 사용하면 얻을 수 있는 이점

Adobe Experience Platform Launch은 기존 Experience Cloud 고객에게 무료로 제공됩니다. platform launch은 설치, 구성, 업데이트 및 삭제할 수 있는 사용하기 쉬운 확장을 통해 웹 사이트에서 태그 배포를 단순화합니다. platform launch은 웹 사이트에서 적은 사용 공간을 가지며 페이지를 빠르게 로드할 수 있도록 해줍니다.

>[!IMPORTANT]
>
>세그먼트를 Platform launch 확장에 활성화할 수는 없지만, 특정 상황에서 이벤트 데이터를 전달하는 규칙을 설정할 수 있습니다. 아래 내용을 참조하십시오.

이벤트 데이터를 확장에 전달할 시기를 결정하는 *규칙*&#x200B;을 만들 수 있습니다. 이 강력한 기능을 사용하면 모든 상호 작용에서 이벤트 데이터를 전송하는 것과 대조적으로 특정 상황에서 이벤트 데이터만 전달할 수 있습니다. 자세한 내용은 [Adobe Experience Platform Launch 설명서](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)에서 규칙에 대해 읽어보십시오.

## platform launch 확장 {#extensions-use-cases} 의 사용 사례 예

platform launch 확장을 사용하면 다양한 고객 활용 사례를 충족할 수 있습니다. platform launch 확장 사용에 대한 일부 사용 사례는 다음과 같습니다.

- facebook 픽셀 확장 기능을 통해 웹 사이트나 기본 앱 데이터를 Facebook에 보낼 수 있습니다. Facebook 픽셀 은 방문자가 탐색한 사이트 또는 앱의 일부를 나타내며 해당 정보를 Facebook에 전달하며 Facebook을 통해 방문자를 재타깃팅할 수 있습니다.
- 웹 사이트 및 앱의 이벤트 데이터를 Google Analytics으로 전달하여 해당 데이터를 기반으로 분석하고 결정할 수 있습니다.
- platform launch에서 설정한 규칙에 따라 사용자가 페이지와 상호 작용하는 방법을 기반으로 적절한 시간에 클라이언트측 차트박스 앱을 설정할 수 있습니다.

## 확장 카테고리 {#extension-categories}

platform launch 확장은 Platform에서 다음 카테고리에 해당할 수 있습니다.

- [광고](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [데이터 관리 플랫폼](../data-management/overview.md)
- [이메일 마케팅 대상](../email-marketing/overview.md)
- [개인화](../personalization/overview.md)
- [설문 조사](../survey/overview.md)
- [고객의 의견](../voice/overview.md)
