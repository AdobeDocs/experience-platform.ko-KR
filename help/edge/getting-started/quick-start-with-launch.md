---
title: 빠른 시작
seo-title: Adobe Experience Platform 웹 SDK 빠른 시작(Launch)
description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
seo-description: Experience Platform 웹 SDK 익스텐션을 사용하여 데이터를 수집하는 빠른 시작 가이드
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 3%

---


# 시작

이 가이드는 Launch에서 Adobe Experience Platform 웹 SDK를 설정하는 다양한 방법을 설명합니다. 이 기능을 사용하려면 허용 목록에 포함되어야 합니다. 대기자 명단에 오르시려면 CSM으로 연락하십시오.

- 자사 도메인(CNAME)이 [활성화되어 있어야](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) 합니다. 이미 Analytics용 CNAME이 있는 경우 이 CNAME을 사용해야 합니다. 개발 중인 테스트는 CNAME 없이 작동하지만 프로덕션으로 이동하기 전에 필요합니다
- Adobe Experience Platform 데이터 플랫폼을 이용할 수 있습니다. 플랫폼을 구매하지 않은 경우, SDK와 함께 사용할 수 있도록 Experience Platform Data Services Foundation을 제공할 것입니다.
- 최신 버전의 방문자 ID 서비스 사용

## 구성 ID 만들기

실행 시 [에지 구성 도구를 사용하여 구성 ID를](../fundamentals/edge-configuration.md) 만들 수 있습니다. 이를 통해 Edge Network에서 데이터를 다양한 솔루션으로 보낼 수 있습니다. 각 옵션을 찾는 방법에 대한 자세한 내용은 [에지 구성 도구](../fundamentals/edge-configuration.md) 페이지를 참조하십시오.

>참고: 이 기능을 사용하려면 조직에서 허용 목록에 포함되어야 합니다. 최종 허용 목록에 포함하려면 CSM에 문의하십시오.

## 스키마 준비

경험 플랫폼 에지 네트워크는 데이터를 XDM으로 가져옵니다. XDM은 스키마를 정의할 수 있는 데이터 형식입니다. 스키마는 Edge Network에서 데이터 형식을 예상하는 방법을 정의합니다. 데이터를 전송하려면 스키마를 정의해야 합니다.

- [스키마 만들기](../../xdm/tutorials/create-schema-ui.md)
- 만든 스키마에 Adobe Experience Platform 웹 SDK 믹신 추가

## Launch에서 SDK 설치

Launch에 로그인하여 `AEP Web SDK` 익스텐션을 설치합니다. SDK 설치 시 익스텐션을 구성하라는 메시지가 표시됩니다. 위에 요청한 구성 ID를 입력합니다. 익스텐션은 조직 ID에 자동으로 채워집니다.

다양한 구성 옵션에 대한 자세한 내용은 SDK [구성을 참조하십시오](../fundamentals/configuring-the-sdk.md).

## 스키마를 기반으로 데이터 요소 만들기

론치에서 AEP 웹 SDK로 확장 기능을 변경하고 유형을 XDM 개체로 설정하여 스키마를 참조하는 데이터 요소를 만듭니다. 스키마를 로드할 수 있으므로 데이터 요소를 스키마의 다른 부분에 매핑할 수 있습니다.

![론치의 날짜 요소](../../assets/edge_data_element.png)

## 이벤트 보내기

익스텐션이 설치되면 AEP 웹 SDK 익스텐션에서 규칙에 &quot;sendEvent&quot; 동작을 추가하여 이벤트 전송을 시작합니다. 이벤트에 방금 만든 데이터 요소를 XDM 데이터로 추가해야 합니다. 페이지가 로드될 때마다 하나 이상의 이벤트를 보내는 것이 좋습니다.

이벤트를 추적하는 방법에 대한 자세한 내용은 이벤트 [추적을 참조하십시오](../fundamentals/tracking-events.md).

## 다음 단계

데이터 흐름을 마치면 다음을 수행할 수 있습니다.

- [스키마 구축](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)
- 경험 [개인화](../fundamentals/rendering-personalization-content.md)
- 여러 솔루션으로 데이터 전송 방법 살펴보기
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
