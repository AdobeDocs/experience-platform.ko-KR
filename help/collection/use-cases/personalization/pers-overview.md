---
title: Personalization 사용 사례 개요
description: 컨텐츠 렌더링 및 표시 추적을 위한 패턴을 포함하여 Adobe Experience Platform Web SDK을 사용하여 개인화 사용 사례를 구현하는 방법을 알아봅니다.
keywords: 개인화;sendEvent;renderDecisions;applyPropositions;decisionScopes;이벤트 표시;깜박임;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Personalization 사용 사례 개요

Adobe Experience Platform 웹 SDK을 사용하면 웹 속성에 대해 다양한 개인화 사용 사례를 사용할 수 있습니다. 유연한 아키텍처(클라이언트측, 서버측 및 하이브리드)를 지원하므로, 사이트 요구 사항에 부합하는 방식으로 의사 결정을 요청하고 콘텐츠를 렌더링할 수 있습니다.

## 개인화된 콘텐츠 렌더링

웹 SDK은 개인화 결정(_제안_&#x200B;이라고도 함)을 검색하고 페이지에서 렌더링하는 데 도움이 될 수 있습니다. 렌더링은 비동기적이므로 콘텐츠가 적용되는 시기에 대해 특정 타이밍을 가정하지 마십시오.

받은 제안 항목과 일치하는 패턴을 선택합니다.

1. **DOM 작업 제안 자동 렌더링**: 제안에 Web SDK에서 자동으로 적용할 수 있는 선택기와 작업 유형이 있는 `dom-action`개 항목이 포함된 경우 사용합니다. [DOM 작업 제안 자동 렌더링](render-auto-pers-content.md)을 참조하십시오.
1. **applyPropositions를 사용하여 선택기 없이 HTML 오퍼 렌더링**: HTML 콘텐츠를 받을 때 사용하지만 메타데이터를 통해 적용할 위치와 방법(선택기 + 작업 유형)을 제공해야 합니다. [선택기 없이 HTML 오퍼 렌더링](render-html-offers.md)을 참조하십시오.
1. **수동으로 제안 렌더링**: 렌더링 논리를 완전히 제어해야 할 때 사용합니다(예: JSON에서 UI 작성 또는 사용자 지정 비즈니스 규칙 적용). [수동으로 제안 렌더링](render-manual-propositions.md)을 참조하십시오.

>[!TIP]
>
>이러한 패턴은 결합할 수 있습니다. 예를 들어 자동 DOM 작업 렌더링을 활성화하면서 특정 결정 범위에서 콘텐츠를 수동으로 렌더링할 수 있습니다.

## 일반적인 컴패니언 항목

대부분의 개인화 구현에는 다음과 같은 일반적인 주제가 포함됩니다.

* **깜박임 방지**(선택 사항): 개인 설정 중에 컨테이너를 숨기거나 표시합니다. [깜박임 관리](manage-flicker.md)를 참조하십시오.
* **표시된 내용을 추적합니다**: 렌더링된 콘텐츠에 대한 표시 이벤트를 기록합니다. [디스플레이 이벤트 관리](display-events.md)를 참조하세요.
* **페이지 상단 가져오기/페이지 하단 지표**: 결정을 일찍 요청한 다음 나중에 측정을 포함합니다. [페이지 이벤트 상단 및 하단 구성](top-bottom-page-events.md)을 참조하십시오.

## 웹 SDK 샘플

이 폴더의 문서 페이지 외에도 Adobe은 참조할 수 있는 샘플 애플리케이션의 저장소를 유지 관리합니다. 다음을 포함한 추가 개인화 시나리오는 GitHub에서 [웹 SDK 샘플](https://github.com/adobe/alloy-samples/)을 참조하십시오.

* 클라이언트측 개인화
* 서버측 개인화
* 하이브리드 개인화
* 단일 페이지 애플리케이션의 Personalization
