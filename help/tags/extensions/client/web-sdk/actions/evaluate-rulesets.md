---
title: 규칙 세트 평가
description: 규칙 세트 평가를 수동으로 트리거합니다.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# 규칙 세트 평가

**[!UICONTROL Evaluate rulesets]** 작업 유형을 사용하면 규칙 집합 평가를 수동으로 트리거할 수 있습니다. 규칙 세트는 브라우저 내 메시지와 같은 기능을 지원하기 위해 Adobe Journey Optimizer에서 반환됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정한 다음 [!UICONTROL Action type]을(를) **[!UICONTROL Evaluate rulesets]**(으)로 설정합니다.

![규칙 집합 평가 응답 작업 유형을 표시하는 Experience Platform 사용자 인터페이스의 이미지입니다.](../assets/evaluate-rulesets.png)

## 사용 가능한 필드

이 작업 유형은 다음 옵션을 지원합니다.

* **[!UICONTROL Render visual personalization decisions]**: 활성화되면 일치하는 규칙 집합 항목에 대한 시각적 개인화 결정을 렌더링하는 확인란입니다.
* **[!UICONTROL Decision context]**: 온디바이스 의사 결정을 위해 Adobe Journey Optimizer 규칙 세트를 평가할 때 사용되는 키-값 맵입니다. 결정 컨텍스트를 수동으로 또는 데이터 요소를 통해 제공할 수 있습니다.
