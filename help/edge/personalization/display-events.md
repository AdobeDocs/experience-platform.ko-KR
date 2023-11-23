---
title: Web SDK에서 디스플레이 이벤트 관리
description: 이 문서에서는 디스플레이 이벤트의 정의와 Web SDK에서 이 이벤트를 사용하는 방법에 대해 설명합니다.
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Web SDK에서 디스플레이 이벤트 관리

디스플레이 이벤트는 특정 개인화 콘텐츠가 페이지에 표시될 때 Web SDK에서 개인화 또는 분석 서비스에 알리는 데 사용됩니다.

디스플레이 이벤트를 보내면 개인화 지표의 정확도가 향상되고 사용자가 페이지에서 볼 수 있는 내용에 대한 정확한 개요를 제공합니다.

Web SDK를 사용하면 두 가지 방법으로 디스플레이 이벤트를 전송할 수 있습니다.

* [자동](#send-automatically): 개인화된 콘텐츠가 페이지에 렌더링된 직후. 방법 설명서 참조 [개인화된 콘텐츠 렌더링](rendering-personalization-content.md) 추가 정보.
* [수동](#send-sendEvent-calls), 후속 작업 `sendEvent` 호출.

>[!NOTE]
>
>디스플레이 이벤트는 를 호출할 때 자동으로 전송되지 않습니다. `applyPropositions` 함수.

## 디스플레이 이벤트를 자동으로 보내기 {#send-automatically}

디스플레이 이벤트를 보내면 개인화가 로드된 후 바로 이벤트가 전송되므로, 보다 정확한 분석 지표가 자동으로 제공됩니다. 이 구현에는 보다 간소화된 구현 방법도 있습니다.

개인화된 콘텐츠가 페이지에서 렌더링된 후 디스플레이 이벤트를 자동으로 보내려면 다음 매개 변수를 구성해야 합니다.

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` 또는 지정되지 않음

Web SDK는 의 결과로 개인화가 렌더링되면 바로 디스플레이 이벤트를 보냅니다. `sendEvent` 호출합니다.

## 후속 sendEvent 호출에서 표시 이벤트 보내기 {#send-sendEvent-calls}

비교 대상 [자동으로](#send-automatically) 디스플레이 이벤트 보내기(후속 이벤트에 포함할 때) `sendEvent` 호출 시 호출에 페이지 로드에 대한 자세한 정보를 포함할 수도 있습니다. 이는 개인화된 콘텐츠를 요청할 때 이용할 수 없었던 추가 정보일 수 있다.

또한 디스플레이 이벤트를에서 전송 `sendEvent` 호출은 Adobe Analytics 사용 시 바운스 비율 오류를 최소화합니다.

>[!IMPORTANT]
>
>수동으로 렌더링된 제안을 사용하는 경우 디스플레이 이벤트는 를 통해서만 지원됩니다. `sendEvent` 호출. 이 경우 디스플레이 이벤트를 자동으로 전송할 수 없습니다.

### 자동으로 렌더링된 제안에 대한 디스플레이 이벤트 보내기 {#auto-rendered-propositions}

자동으로 렌더링된 제안에 대한 표시 이벤트를 보내려면 `sendEvent` 호출:

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` 페이지 조회수의 맨 위에

디스플레이 이벤트를 보내려면 `sendEvent` 포함 `personalization.includePendingDisplayNotifications: true`

### 수동으로 렌더링된 제안에 대한 디스플레이 이벤트 보내기 {#manually-rendered-propositions}

수동으로 렌더링된 제안에 대한 표시 이벤트를 보내려면 해당 이벤트를 `_experience.decisioning.propositions` XDM 필드(포함) `id`, `scope`, 및 `scopeDetails` 제안의 필드.

또한 다음을 설정합니다. `include _experience.decisioning.propositionEventType.display` 필드 대상 `1`.
