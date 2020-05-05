---
title: 'Adobe Target 및 Adobe Experience Platform 웹 SDK. '
seo-title: Adobe Experience Platform 웹 SDK 및 Adobe Target 사용
description: Adobe Target을 사용하여 Experience Platform 웹 SDK로 개인화된 컨텐츠를 렌더링하는 방법 학습
seo-description: Adobe Target을 사용하여 Experience Platform 웹 SDK로 개인화된 컨텐츠를 렌더링하는 방법 학습
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Target 개요

Adobe Experience Platform Web SDK는 개인화 기능을 통해 Adobe Target과 [통합되어](../../fundamentals/rendering-personalization-content.md) 개인화된 콘텐츠와 의사 결정을 간단하게 제공할 수 있습니다.

## Adobe Target 활성화

Target을 활성화하려면 다음을 수행해야 합니다.

- 적절한 클라이언트 코드를 사용하여 [Edge 구성에서](../../fundamentals/edge-configuration.md) target을 활성화합니다.
- 이벤트에 `renderDecisions` 옵션을 추가합니다.

그런 다음 다음을 수행할 수도 있습니다.

- 이벤트 `scopes` 에 추가하여 특정 활동을 검색할 수 있습니다(양식 기반 컴포저를 사용하여 만든 활동에 유용함).
- 코드 [조각을](../../fundamentals/managing-flicker.md) 추가하여 페이지의 특정 부분만 숨깁니다.

## VEC 사용

SDK를 사용하면 VEC를 일반적으로 사용할 수 있습니다. 단, [대상 VEC 도우미 확장이](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) 설치 및 활성화되어 있어야 합니다.

## 양식 기반 컴포저 사용

양식 기반 컴포저를 사용하여 컨텐츠를 반환할 수도 있습니다. 범위는 타겟 UI에 위치(mBox)로 표시됩니다. 또한 범위를 사용하려는 경우 개발자가 응답을 찾고 있는지 확인해야 합니다.

## XDM 고객

Target XDM 데이터 내에 사용자 지정 매개 변수로 Audience Builder에 표시됩니다. XDM은 점 표기법(예: `web.webPageDetails.name`)

## 용어

__결정__ - Target에서 이러한 상관 관계는 활동에서 선택한 경험과 관련이 있습니다.

__범위__ - 결정의 범위입니다. Target에서 mBox입니다. 글로벌 mBox는 `__view__` 범위입니다.

__스키마__ - 결정 스키마는 Target의 오퍼 유형입니다.

__XDM__ - XDM은 점 표기법으로 시리얼라이즈 된 다음 Target에 mBox 매개 변수로 넣습니다.