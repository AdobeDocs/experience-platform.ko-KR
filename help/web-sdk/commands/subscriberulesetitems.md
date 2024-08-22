---
title: subscribeRulesetItems
description: subscribeRulesetItems 명령을 사용하여 특정 표면에 대한 컨텐트 카드에 가입합니다.
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---


# `subscribeRulesetItems`

`subscribeRulesetItems` 명령을 사용하면 충족된 규칙 세트의 결과인 제안을 구독할 수 있습니다. 필터링할 기준 표면 및 스키마를 지정하고 콜백 함수를 제공하여 이 작업을 수행할 수 있습니다.

모든 시간 규칙 집합이 평가되면 콜백 함수는 그 안에 제안 배열이 있는 `result` 개체를 수신합니다.

>[!IMPORTANT]
>
>`subscribeRulesetItems` 명령은 [`sendEvent`](sendevent/overview.md)개의 결과와 함께 반환되지 않으므로 규칙 세트에서 가져온 제안을 가져올 수 있는 유일한 방법입니다.

## 명령 옵션 {#command-options}

이 명령은 다음 속성을 가진 `options` 개체를 사용합니다.

| 속성 | 유형 | 설명 |
| --- | --- | --- |
| `surfaces` | 문자열 배열 | 서피스 목록입니다. 여기에 제공된 표면 중 하나와 일치하는 경우에만 제안이 콜백 함수에 의해 수신됩니다. |
| `schemas` | 문자열 배열 | 스키마 목록. 제안이 여기에 제공된 스키마 중 하나와 일치하는 경우 콜백 함수에서만 수신됩니다. |
| `callback` | 함수 | 제안이 충족된 규칙 세트의 결과일 때 호출되는 콜백 함수입니다. 콜백 함수를 호출할 때 두 개의 매개 변수를 받습니다. `result` 및 `collectEvent`. 자세한 내용은 [콜백 매개 변수](#callback-parameters)를 참조하십시오. |

### 콜백 매개 변수 {#callback-parameters}

콜백 함수는 호출 시 아래 표에 설명된 두 매개 변수를 수신합니다.

| 매개변수 | 유형 | 설명 |
| --- | --- | --- |
| `result` | 오브젝트 | 이 개체에는 `propositions` 배열이 있습니다.  이 제안은 충족된 규칙 세트의 직접적인 결과입니다. `result` 개체는 `then` 절을 사용하여 `sendEvent`에서 반환된 [결과 개체](command-responses.md)와 동일하게 구조화되었습니다. |
| `collectEvent` | 함수 | 인터랙션, 디스플레이 및 기타 이벤트를 추적하기 위해 Edge Network 이벤트를 전송하는 데 사용할 수 있는 편의 함수입니다. |

### `collectEvent` 함수 {#collectevent-function}

`collectEvent` 함수는 Edge Network 이벤트를 전송하여 상호 작용, 디스플레이 및 기타 이벤트를 추적하는 데 사용할 수 있는 편의 함수입니다. 이는 아래 표에 설명된 두 매개 변수를 허용합니다.

| 매개변수 | 유형 | 설명 |
| --- | --- | --- |
| 이벤트 유형 | 문자열 | 내보낼 제안 이벤트 유형을 나타내는 문자열입니다. 지원되는 이벤트 유형은 `display`, `interact` 또는 `dismiss`입니다. |
| `propositions` | 배열 | 이벤트에 해당하는 제안 배열. |

## Web SDK 태그 확장을 사용하여 콘텐츠 카드 구독 {#tag-extension}

아래 단계에 따라 태그 사용자 인터페이스를 통해 콘텐츠 카드를 구독하십시오.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 이벤트]에서 기존 이벤트를 선택하거나 새 이벤트를 만듭니다.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 **[!UICONTROL 이벤트 유형]**&#x200B;을(를) **[!UICONTROL 규칙 집합 항목 구독]**(으)로 설정합니다.
1. 화면 오른쪽에서 콘텐츠 카드에 가입할 스키마 및 표면을 선택합니다.
1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택한 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 콘텐츠 카드 구독 {#library}

다음 샘플 코드는 콘텐츠 카드에 대해 `web://mywebsite.com/#welcome` 표면을 구독하고 `collectEvent` 편의 메서드를 사용하여 모든 제안에 대해 `display` 이벤트를 내보냅니다.

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
