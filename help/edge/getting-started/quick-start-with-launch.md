---
title: 빠른 시작
seo-title: Adobe Experience Platform 웹 SDK 빠른 시작(시작)
description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
seo-description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
translation-type: tm+mt
source-git-commit: 9d58693646f472e84f04a64c4ad66f61dc5d3eba
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 4%

---


# 시작

이 안내서에서는 Adobe Launch에서 Adobe Experience Platform 웹 SDK를 설정하는 방법에 대한 다양한 단계를 안내합니다. 이 기능을 사용하려면 권한이 있어야 하며 허용 목록에 있어야 합니다. 대기 목록에 오르려면 CSM에 문의하십시오. 또한 이 기능을 사용하려면 다음을 수행해야 합니다.

- 자사 도메인(CNAME)이 [활성화되어 있어야](https://docs.adobe.com/content/help/ko-KR/core-services/interface/ec-cookies/cookies-first-party.html) 합니다. 이미 Adobe Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다. 개발 중인 테스트는 CNAME 없이 작동하지만 프로덕션으로 이동하기 전에 필요합니다
- 최신 버전의 방문자 ID 서비스 사용

## 구성 ID 만들기

Adobe Launch에서 [Edge 구성 도구를 사용하여 구성 ID를](../fundamentals/edge-configuration.md) 만들 수 있습니다. 이를 통해 Edge Network에서 데이터를 다양한 솔루션으로 보낼 수 있습니다. 각 옵션을 찾는 방법에 대한 자세한 내용은 [에지 구성 도구](../fundamentals/edge-configuration.md) 페이지를 참조하십시오.

>[!NOTE]
>
>이 기능을 사용하려면 조직에서 허용 목록에 있어야 합니다. 허용 목록에 추가하려면 CSM에 문의하십시오.

## 스키마 준비

Experience Platform 에지 네트워크는 데이터를 XDM으로 가져옵니다. XDM은 스키마를 정의할 수 있는 데이터 형식입니다. 스키마는 Edge Network에서 데이터 형식을 예상하는 방법을 정의합니다. 데이터를 전송하려면 스키마를 정의해야 합니다. 다음을 완료해야 합니다.

1. [스키마 만들기](../../xdm/tutorials/create-schema-ui.md)
2. 만든 스키마에 AEP 웹 SDK ExperienceEvent Mixin을 추가합니다.
3. 만든 스키마에서 데이터 집합을 만듭니다.

다음 비디오는 웹 SDK 데이터에 대한 스키마, 데이터 세트 및 스트리밍 소스 커넥터를 만드는 데 도움이 되도록 만들어졌습니다.

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## Adobe Launch에서 SDK 설치

Adobe Launch에 로그인하여 익스텐션을 `AEP Web SDK` 설치합니다. SDK 설치 시 익스텐션을 구성하라는 메시지가 표시됩니다. 위에서 요청한 구성 ID를 입력합니다. 익스텐션은 조직 ID에 자동으로 채워집니다.

다양한 구성 옵션에 대한 자세한 내용은 SDK [구성을 참조하십시오](../fundamentals/configuring-the-sdk.md).

## 스키마를 기반으로 데이터 요소 만들기

Adobe Launch에서 확장 기능을 AEP Web SDK로 변경하고 유형을 XDM 개체로 설정하여 스키마를 참조하는 데이터 요소를 만듭니다. 스키마를 로드할 수 있으므로 데이터 요소를 스키마의 다른 부분에 매핑할 수 있습니다.

![론치의 날짜 요소](../../assets/edge_data_element.png)

## 이벤트 보내기

익스텐션이 설치되면 AEP 웹 SDK 익스텐션에서 규칙에 &quot;sendEvent&quot; 동작을 추가하여 이벤트 전송을 시작합니다. 이벤트에 방금 만든 데이터 요소를 XDM 데이터로 추가해야 합니다. 페이지가 로드될 때마다 하나 이상의 이벤트를 보내는 것이 좋습니다.

이벤트를 추적하는 방법에 대한 자세한 내용은 이벤트 [추적을 참조하십시오](../fundamentals/tracking-events.md).

## 다음 단계

데이터 흐름이 끝나면 다음을 수행할 수 있습니다.

- [스키마 구축](https://docs.adobe.com/content/help/ko-KR/experience-platform/xdm/schema/composition.html)
- [디버깅에 대한 자세한 내용](../fundamentals/debugging.md)
- 경험 [개인화](../fundamentals/rendering-personalization-content.md)
- 여러 솔루션으로 데이터 전송 방법 살펴보기
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
