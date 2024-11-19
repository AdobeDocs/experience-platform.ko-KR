---
title: Web SDK에서 디스플레이 이벤트 관리
description: 이 문서에서는 디스플레이 이벤트의 정의와 Web SDK에서 이 이벤트를 사용하는 방법에 대해 설명합니다.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: 4c7313afdce6645ab638b2998573e5a4f7c5de8f
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Web SDK에서 디스플레이 이벤트 관리

디스플레이 이벤트는 특정 개인화 콘텐츠가 페이지에 표시될 때 Web SDK에서 개인화 또는 분석 서비스에 알리는 데 사용됩니다.

디스플레이 이벤트를 보내면 개인화 지표의 정확도가 향상되고 사용자가 페이지에서 볼 수 있는 내용에 대한 정확한 개요를 제공합니다.

Web SDK를 사용하면 두 가지 방법으로 디스플레이 이벤트를 전송할 수 있습니다.

* 개인화된 콘텐츠가 페이지에 렌더링되면 바로 [자동으로](#send-automatically). 자세한 내용은 [개인화된 콘텐츠를 렌더링](rendering-personalization-content.md)하는 방법에 대한 설명서를 참조하십시오.
* 후속 `sendEvent`번의 호출을 통해 [수동으로](#send-sendEvent-calls).

>[!NOTE]
>
>`applyPropositions` 함수를 호출할 때 표시 이벤트가 자동으로 전송되지 않습니다.

## 디스플레이 이벤트를 자동으로 보내기 {#send-automatically}

디스플레이 이벤트를 보내면 개인화가 로드된 후 바로 이벤트가 전송되므로, 보다 정확한 분석 지표가 자동으로 제공됩니다. 이 구현에는 보다 간소화된 구현 방법도 있습니다.

개인화된 콘텐츠가 페이지에서 렌더링된 후 디스플레이 이벤트를 자동으로 보내려면 다음 매개 변수를 구성해야 합니다.

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true` 또는 지정되지 않음

Web SDK는 `sendEvent` 호출의 결과로 개인화가 렌더링되면 바로 디스플레이 이벤트를 보냅니다.

## 후속 sendEvent 호출에서 표시 이벤트 보내기 {#send-sendEvent-calls}

[자동으로](#send-automatically)에서 표시 이벤트를 보내는 것과 비교하여 후속 `sendEvent` 호출에 이 이벤트를 포함하면 호출에 페이지 로드에 대한 자세한 정보를 포함할 수 있습니다. 이는 개인화된 콘텐츠를 요청할 때 이용할 수 없었던 추가 정보일 수 있다.

또한 `sendEvent` 호출에서 표시 이벤트를 보내면 Adobe Analytics 사용 시 바운스 비율 오류가 최소화됩니다.

>[!IMPORTANT]
>
>수동으로 렌더링된 제안을 사용하는 경우 디스플레이 이벤트는 `sendEvent` 호출을 통해서만 지원됩니다. 이 경우 디스플레이 이벤트를 자동으로 전송할 수 없습니다.

### 자동으로 렌더링된 제안에 대한 디스플레이 이벤트 보내기 {#auto-rendered-propositions}

자동으로 렌더링된 제안에 대한 표시 이벤트를 보내려면 `sendEvent` 호출에서 다음 매개 변수를 구성해야 합니다.

* `renderDecisions: true`
* 페이지 조회수의 맨 위에 대한 `personalization.sendDisplayEvent: false`

디스플레이 이벤트를 보내려면 `personalization.includeRenderedPropositions: true`(으)로 `sendEvent`에 전화

### 수동으로 렌더링된 제안에 대한 디스플레이 이벤트 보내기 {#manually-rendered-propositions}

수동으로 렌더링된 제안에 대한 표시 이벤트를 보내려면 제안에 포함된 `id`, `scope` 및 `scopeDetails` 필드를 포함하여 `_experience.decisioning.propositions` XDM 필드에 해당 이벤트를 포함해야 합니다.

또한 `include _experience.decisioning.propositionEventType.display` 필드를 `1`(으)로 설정하십시오.
