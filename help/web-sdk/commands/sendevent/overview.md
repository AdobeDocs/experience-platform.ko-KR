---
title: sendEvent
description: Adobe Experience Platform Edge Network으로 데이터를 전송합니다.
exl-id: 83de368d-78d4-4e28-aadd-afaea1ca091d
source-git-commit: 9ea7b678f5cfa19c7fd1e3ba6633cdeed4084b18
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# `sendEvent`

`sendEvent` 명령은 개인화된 Adobe, ID 및 대상 대상을 검색하기 위해 데이터를 사용자에게 보내는 기본 방법입니다. [`xdm`](xdm.md) 개체를 사용하여 Adobe Experience Platform 스키마에 매핑되는 데이터를 보냅니다. [`data`](data.md) 개체를 사용하여 XDM이 아닌 데이터를 보냅니다. 데이터 스트림 매퍼를 사용하여 이 개체 내의 데이터를 스키마 필드에 정렬할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 이벤트 데이터 보내기

이벤트 데이터 전송은 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL 규칙]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL 작업]에서 기존 작업을 선택하거나 작업을 만드십시오.
1. [!UICONTROL 확장] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정하고 [!UICONTROL 작업 유형]을(를) **[!UICONTROL 이벤트 보내기]**(으)로 설정합니다.
1. 원하는 필드를 설정하고 **[!UICONTROL 변경 내용 유지]**&#x200B;를 클릭한 다음 게시 워크플로우를 실행하십시오.

## 웹 SDK JavaScript 라이브러리를 사용하여 이벤트 데이터 보내기

웹 SDK의 구성된 인스턴스를 호출할 때 `sendEvent` 명령을 실행합니다. `sendEvent` 명령을 호출하기 전에 [`configure`](../configure/overview.md) 명령을 호출해야 합니다.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": false,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## 응답 개체

이 명령을 사용하여 [응답을 처리](../command-responses.md)하기로 결정하는 경우 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`propositions`**: Edge Network이 반환한 제안 배열. 자동으로 렌더링되는 제안에 `true`(으)로 설정된 `renderAttempted` 플래그가 포함되어 있습니다.
* **`inferences`**: 이 사용자에 대한 기계 학습 정보가 포함된 추론 개체의 배열입니다.
* **`destinations`**: Edge Network이 반환한 대상 개체의 배열입니다.
