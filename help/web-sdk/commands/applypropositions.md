---
title: propositions 적용
description: 이미 sendEvent로 렌더링된 제안을 다시 렌더링합니다.
exl-id: 6b79f334-4ea6-4ba4-8640-d35b7f90df98
source-git-commit: 9aab41b338907f3c9fb15d08bfa877eb218f5627
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# `applyPropositions`

`applyPropositions` 명령을 사용하면 [`sendEvent`](sendevent/overview.md) 명령을 사용하여 이미 렌더링된 제안을 다시 렌더링할 수 있습니다. 이 명령은 페이지의 일부가 다시 렌더링되어 페이지에 이미 적용된 개인화를 덮어쓸 수 있는 단일 페이지 애플리케이션으로 작업할 때 유용합니다.

이 명령은 다음 필드를 지원합니다.

* **제안**: 다시 렌더링할 제안 개체의 배열입니다.
* **보기 이름**: 렌더링할 보기의 이름입니다. 이러한 결정에 대한 표시 알림은 캐시되며 `personalization.includePendingDisplayNotifications` 옵션을 사용하여 후속 `sendEvent` 명령에 포함될 수 있습니다.
* **메타데이터**: HTML 오퍼를 적용할 수 있는 방법을 결정하는 개체입니다. 여기에는 다음 속성이 포함됩니다.
   * 범위
   * 선택기
   * 작업 유형

## 웹 SDK 태그 확장을 사용하여 제안 적용

제안 적용은 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 제안 적용]**(으)로 설정합니다.
1. 오른쪽에서 원하는 필드를 설정합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 제안 적용

웹 SDK의 구성된 인스턴스를 호출할 때 `applyPropositions` 명령을 실행합니다. 구성 옵션이 포함된 개체는 다음 필드를 지원합니다.

* **`propositions`**: 다시 렌더링할 제안 개체의 배열입니다. 일반적으로 `propositionScopes` 필드에 따라 다시 렌더링할 범위 또는 표면이 결정되므로 이 개체는 일반적으로 사용되지 않습니다.
* **`metadata`**: HTML 오퍼가 적용되는 방법을 결정합니다. 키가 범위 또는 표면이고 값이 `selector` 및 `actionType` 키를 포함하는 개체인 맵입니다.
   * `selector`: HTML을 적용할 위치의 CSS 선택기가 포함된 문자열입니다.
   * `actionType`: HTML 시 수행할 작업입니다. 유효한 값은 `setHtml`, `replaceHtml` 및 `appendHtml`입니다.
* **`viewName`**: 단일 페이지 응용 프로그램에서 렌더링할 보기의 이름입니다. 이러한 결정에 대한 표시 알림이 캐시되며 `personalization.includePendingDisplayNotifications`을(를) 사용하여 후속 `sendEvent` 명령에 포함될 수 있습니다.

```js
alloy("applyPropositions",{
  "propositions": [],
  "metadata": {},
  "viewName": ""
});
```
