---
title: sendEvent
description: Adobe Experience Platform Edge Network로 데이터를 전송합니다.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---


# `sendEvent`

다음 `sendEvent` 명령은 데이터를 Adobe에 보내고 개인화된 콘텐츠, id 및 대상자 대상을 검색하는 기본 방법입니다. 사용 [`xdm`](xdm.md) Adobe Experience Platform 스키마에 매핑되는 데이터를 전송하는 개체입니다. 사용 [`data`](data.md) 비XDM 데이터를 보낼 개체입니다. 데이터 스트림 매퍼를 사용하여 이 개체 내의 데이터를 스키마 필드에 정렬할 수 있습니다.

## 웹 SDK 태그 확장을 사용하여 이벤트 데이터 보내기

이벤트 데이터 전송은 Adobe Experience Platform 데이터 수집 태그 인터페이스의 규칙 내에서 작업으로 수행됩니다.

1. 에 로그인 [experience.adobe.com](https://experience.adobe.com) Adobe ID 자격 증명을 사용합니다.
1. 다음으로 이동 **[!UICONTROL 데이터 수집]** > **[!UICONTROL 태그]**.
1. 원하는 태그 속성을 선택합니다.
1. 다음으로 이동 **[!UICONTROL 규칙]**&#x200B;을 클릭한 다음 원하는 규칙을 선택합니다.
1. 아래 [!UICONTROL 작업]를 클릭하고 기존 작업을 선택하거나 작업을 만듭니다.
1. 설정 [!UICONTROL 확장] 드롭다운 필드 **[!UICONTROL Adobe Experience Platform 웹 SDK]**, 및 설정 [!UICONTROL 작업 유형] 끝 **[!UICONTROL 이벤트 보내기]**.
1. 원하는 필드를 설정하고 **[!UICONTROL 변경 내용 유지]**&#x200B;그런 다음 게시 워크플로우를 실행합니다.

## 웹 SDK JavaScript 라이브러리를 사용하여 이벤트 데이터 보내기

실행 `sendEvent` 명령을 사용하여 웹 SDK의 구성된 인스턴스를 호출할 수 있습니다. 다음을 호출했는지 확인하십시오. [`configure`](../configure/overview.md) 호출 전 명령 `sendEvent` 명령입니다.

```js
alloy("sendEvent", {
  "data": dataObject,
  "documentUnloading": true,
  "edgeConfigOverrides": { "datastreamId": "0dada9f4-fa94-4c9c-8aaf-fdbac6c56287" },
  "renderDecisions": true,
  "type": "commerce.purchases",
  "xdm": adobeDataLayer.getState(reference)
});
```

## 응답 개체

다음을 결정하시면 [응답 처리](../command-responses.md) 이 명령을 사용하면 응답 개체에서 다음 속성을 사용할 수 있습니다.

* **`propositions`**: Edge Network에서 반환되는 제안 배열. 자동으로 렌더링되는 제안에 플래그가 포함됩니다 `renderAttempted` 을 로 설정 `true`.
* **`inferences`**: 이 사용자에 대한 머신 러닝 정보가 포함된 추론 개체의 배열입니다.
* **`destinations`**: Edge Network에서 반환되는 대상 개체의 배열입니다.
