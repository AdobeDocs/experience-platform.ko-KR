---
title: 위성 개체 참조
description: 클라이언트측 _satellite 개체 및 태그에서 이 개체를 사용하여 수행할 수 있는 다양한 기능에 대해 알아봅니다.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 05bf3a8c92aa221af153b4ce9949f0fdfc3c86ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---

# `_satellite` 개체 참조

_이 페이지에서는 JavaScript을 사용하여 태그 논리를 관리하고 사용자 지정할 수 있는 `_satellite` 개체의 사용 방법에 대해 간략히 설명합니다. 데이터 수집 UI에서 구현을 설정하는 방법에 대한 자세한 내용은 [Adobe Experience Platform Web SDK 태그 확장](/help/tags/extensions/client/web-sdk/overview.md)을 참조하십시오._

`_satellite` 개체는 사이트에 게시된 태그 라이브러리와 상호 작용하는 데 도움이 되는 몇 가지 지원되는 진입점을 노출합니다. 로더 태그가 올바르게 구현되면 모든 태그 배포에 `_satellite`이(가) 표시됩니다. 이 개체에는 다음과 같은 몇 가지 주요 사용 사례가 있습니다.

* 사용자 지정 코드 블록의 태그 라이브러리 내에서 사용하므로 태그 라이브러리 자체에 대한 전체 액세스 권한을 제공합니다.
* 모든 환경(개발, 스테이징 또는 프로덕션) 내에서 배포된 구현 디버깅
* 웹 사이트에서 직접 구현하여 이벤트 또는 태그 규칙이 트리거되는 시기를 완전히 제어할 수 있습니다. 새로운 구현의 경우 Adobe에서는 [Adobe 클라이언트 데이터 레이어](/help/tags/extensions/client/client-data-layer/overview.md)와 같은 보다 유연한 전략을 사용하는 것이 좋습니다.

>[!IMPORTANT]
>
>사이트 코드에서 `_satellite`을(를) 호출하는 경우(예: `_satellite.track()`), 사이트가 태그 라이브러리에 단단히 연결되지 않도록 **모든 호출을 보호**&#x200B;합니다.
>
>태그 속성의 사용자 지정 코드 내에서 또는 브라우저 콘솔에서 로컬로 `_satellite`을(를) 사용하면 보안이 필요하지 않습니다.

## 일반적인 사용 예

```js
// Read and write a temporary data element value (guarded)
if(window._satellite?.getVar && window._satellite?.setVar) {
  const region = _satellite.getVar('user_region');
  _satellite.setVar('promo_code', code);
}

// Manually trigger a rule configured in your tag property (guarded)
if (window._satellite?.track) {
  _satellite.track('cart_add', { sku: '123', qty: 2 });
}

// Local console debugging (guarding not needed)
_satellite.setDebug(true);
_satellite.logger.log('Rule evaluated');
```
