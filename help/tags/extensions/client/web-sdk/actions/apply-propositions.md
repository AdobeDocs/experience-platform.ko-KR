---
title: 제안 적용
description: 지표를 증가시키지 않고 단일 페이지 애플리케이션에서 제안을 렌더링합니다.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# 제안 적용

**[!UICONTROL Apply propositions]** 작업 유형을 사용하면 지표를 증가시키지 않고 단일 페이지 애플리케이션에서 제안을 렌더링할 수 있습니다. 이 작업 유형은 페이지의 일부가 다시 렌더링되는 단일 페이지 애플리케이션으로 작업할 때 유용하며, 페이지에 이미 적용된 개인화를 덮어쓸 수 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정한 다음 [!UICONTROL Action type]을(를) **[!UICONTROL Apply propositions]**(으)로 설정합니다.

![제안 적용 작업 유형을 표시하는 Experience Platform 태그 UI입니다.](../assets/apply-propositions.png)

## 사용 사례

다음과 같은 다양한 사용 사례에 이 작업 유형을 사용할 수 있습니다.

1. **mbox HTML 오퍼 렌더링**. **[!UICONTROL Send event]** 작업에서 범위 또는 표면을 통해 명시적으로 요청한 제안에 대해서는 자동으로 렌더링되지 않습니다. 제안 메타데이터를 지정하여 웹 SDK에 렌더링할 위치를 알려 주는 **[!UICONTROL Apply propositions]** 작업 형식을 사용할 수 있습니다.
2. **단일 페이지 응용 프로그램의 보기에 대한 오퍼를 렌더링합니다**. 보기 변경 이벤트를 렌더링할 때 분석 데이터가 아직 준비되지 않은 경우 **[!UICONTROL Apply propositions]** 작업을 사용하여 페이지 상단의 보기 제안을 렌더링할 수 있습니다. 자세한 내용은 [페이지 이벤트 상단 및 하단(두 번째 페이지 보기 - 옵션 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md)을 참조하십시오. 이를 사용하려면 양식에 **[!UICONTROL View name]**&#x200B;을(를) 입력하십시오.
3. **제안을 다시 렌더링합니다**. 사이트에서 React와 같은 프레임워크를 사용하여 콘텐츠를 다시 렌더링하는 경우 개인화를 다시 적용해야 할 수 있습니다. 이러한 경우 **[!UICONTROL Apply propositions]** 작업 유형을 사용하여 이 작업을 수행할 수 있습니다.

이 작업 유형은 렌더링된 제안에 대한 표시 이벤트를 보내지 않습니다. 렌더링된 제안을 추적하여 후속 **[!UICONTROL Send event]** 호출에 포함할 수 있도록 합니다.

## 사용 가능한 필드

이 작업 유형은 다음 필드를 지원합니다.

* **[!UICONTROL Instance]**: 작업이 적용되는 SDK 인스턴스입니다. 구현에서 단일 SDK 인스턴스를 사용하는 경우 이 드롭다운 메뉴가 비활성화됩니다.
* **[!UICONTROL Propositions]**: 다시 렌더링할 제안 개체의 배열입니다.
* **[!UICONTROL View name]**: 렌더링할 보기의 이름입니다.
* **[!UICONTROL Proposition metadata]**: HTML 오퍼를 적용할 수 있는 방법을 결정하는 개체입니다. 양식 또는 데이터 요소를 통해 이 정보를 제공할 수 있습니다. 여기에는 다음 속성이 포함됩니다.
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
