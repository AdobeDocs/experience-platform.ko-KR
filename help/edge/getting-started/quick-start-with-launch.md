---
title: 빠른 시작
seo-title: Adobe Experience Platform 웹 SDK 빠른 시작(Launch)
description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
seo-description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
keywords: 1st-party domain;CNAME;schema;create schema;launch;aep web sdk extension;extension;configuration id;configuration tool;data element;create data element;XDM Object;sendEvent;send Event;
translation-type: tm+mt
source-git-commit: a9c45aed92dc7c7148db7c9383060bbeab763447
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 4%

---


# Adobe Experience Platform 웹 SDK 시작 빠른 시작 가이드

이 가이드는 Launch에서 Adobe Experience Platform 웹 SDK를 설정하는 다양한 방법을 안내합니다. 이 기능을 사용하려면에 있어야 허용 목록에 추가하다 합니다. 대기 목록에 오르려면 CSM(Certified Software Manager)에 문의하십시오.

- 자사 도메인(CNAME)이 [활성화되어 있어야](https://docs.adobe.com/content/help/ko-KR/core-services/interface/ec-cookies/cookies-first-party.html) 합니다. 이미 Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다. 개발 테스트에서는 CNAME이 없어도 되지만 프로덕션으로 이동하려면 먼저 테스트가 필요합니다.
- Adobe Experience Platform에 대한 자격 부여 플랫폼을 구매하지 않은 경우, Adobe은 SDK와 함께 제한된 방식으로 사용할 수 있도록 Experience Platform 데이터 서비스 재단을 추가 비용 없이 제공합니다.
- 최신 버전의 방문자 ID 서비스를 사용하십시오.

## 스키마 준비

Experience Platform 에지 네트워크는 경험 데이터 모델(XDM)을 사용합니다. XDM은 스키마를 정의할 수 있는 데이터 형식입니다. 스키마는 Edge Network에서 데이터 형식을 예상하는 방법을 정의합니다. 데이터를 전송하려면 스키마를 정의해야 합니다.

1. [스키마 만들기](../../xdm/tutorials/create-schema-ui.md)
2. 만든 스키마에 AEP [!DNL Web SDK ExperienceEvent] Mixin을 추가합니다.
3. 만든 스키마에서 데이터 집합을 만듭니다.

다음 비디오는 데이터에 대한 스키마, 데이터 집합 및 스트리밍 소스 커넥터를 만드는 데 도움이 되도록 [!DNL Web SDK] 만들어졌습니다.


>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

Launch에 로그인하여 `AEP Web SDK` 익스텐션을 설치합니다. SDK를 설치하면 익스텐션을 구성하라는 메시지가 표시됩니다. 위에 요청한 구성 ID를 입력합니다. 익스텐션은 조직 ID에 자동으로 채워집니다.


다양한 구성 옵션에 대한 자세한 내용은 SDK [구성을 참조하십시오](../fundamentals/configuring-the-sdk.md).

## 구성 ID 만들기

Launch에서 [Edge 구성 도구를 사용하여 구성](../fundamentals/edge-configuration.md) ID를 만들 수 있습니다. 이를 통해 Edge Network에서 데이터를 다양한 솔루션으로 보낼 수 있습니다. 각 옵션을 찾는 방법에 대한 자세한 내용은 [에지 구성 도구](../fundamentals/edge-configuration.md) 페이지를 참조하십시오.

>[!NOTE]
>
>이 기능을 사용하려면 조직이허용 목록에 추가하다에 있어야 합니다. CSM(Certified Software Manager)에 문의하여를 허용 목록에 추가하다 이용하십시오.

## 스키마를 기반으로 데이터 요소 만들기

론치에서 확장을 AEP 웹 SDK로 변경하고 유형을 다음으로 설정하여 스키마를 참조하는 데이터 요소를 만듭니다 `XDM Object`. 이렇게 하면 스키마가 로드되고 데이터 요소를 스키마의 다른 부분에 매핑할 수 있습니다.

![론치의 날짜 요소](../../assets/edge_data_element.png)

## 이벤트 보내기

익스텐션이 설치되면 AEP 웹 SDK 익스텐션에서 규칙에 동작을 추가하여 이벤트 전송을 시작합니다. `sendEvent` 이벤트에 방금 만든 데이터 요소를 XDM 데이터로 추가합니다. Adobe에서는 페이지가 로드될 때마다 하나 이상의 이벤트를 보낼 것을 권장합니다.

이벤트를 추적하는 방법에 대한 자세한 내용은 이벤트 [추적을 참조하십시오](../fundamentals/tracking-events.md).

## 다음 단계

데이터를 이동한 후 다음을 수행할 수 있습니다.

- [스키마 구축](https://docs.adobe.com/content/help/ko-KR/experience-platform/xdm/schema/composition.html)
- [디버깅에 대한 자세한 내용](../fundamentals/debugging.md)
- 경험 [개인화](../fundamentals/rendering-personalization-content.md)
- Adobe Experience Platform Launch에서 [IAB Transparency &amp; Consent Framework 2.0을](../solution-specific/iab-tcf/with-launch.md) 통합합니다.
- 여러 솔루션으로 데이터 전송 방법 살펴보기
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
