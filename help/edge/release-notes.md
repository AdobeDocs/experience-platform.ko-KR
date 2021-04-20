---
title: Adobe Experience Platform Web SDK 릴리스 노트
description: Adobe Experience Platform Web SDK에 대한 최신 릴리스 정보입니다.
keywords: Adobe Experience Platform 웹 SDK;플랫폼 웹 SDK;웹 SDK;릴리스 노트;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
translation-type: tm+mt
source-git-commit: d4ed6c8fa9c86eb2beec829ab24c381b665c2f03
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# 릴리스 정보

## 버전 2.4.0, 2021년 3월

* 이제 SDK는 npm 패키지](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html)로 [설치할 수 있습니다.
* 동의를 받을 때까지 모든 이벤트를 반환하는 기본 동의](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)를 구성하는 경우 `out` 옵션에 대한 지원을 추가했습니다(기존 `pending` 옵션은 이벤트를 대기열에 넣고 동의를 받으면 전송합니다).[
* 이제 [onBeforeEventSend 콜백](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend)을(를) 사용하여 이벤트가 전송되지 않도록 할 수 있습니다.
* 이제 렌더링되거나 클릭되는 맞춤형 콘텐츠에 대한 이벤트를 전송할 때 `meta.personalization` 대신 XDM 믹싱을 사용합니다.
* 이제 [getIdentity 명령](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id)은 ID와 함께 가장자리 영역 ID를 반환합니다.
* 서버에서 받은 경고 및 오류가 개선되었으며 보다 적절한 방식으로 처리됩니다.
* [Adobe의 동의 2.0 표준](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)에 대한 지원을 추가했습니다.
* 동의 환경 설정이 수신되면 해시되어 로컬 스토리지에 저장되므로 CMP, Platform Web SDK 및 Platform Edge Network 간의 최적의 통합을 활용할 수 있습니다. 동의 기본 설정을 수집하는 경우, 이제 모든 페이지 로드 시 `setConsent`에 전화하도록 권장합니다.
* 2개의 [모니터링 후크](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 및 `onCommandRejected`이(가) 추가되었습니다.
* 버그 수정:개인화 상호 작용 알림 이벤트는 사용자가 새로운 단일 페이지 앱 보기로 이동, 원래 보기로 돌아가기, 전환 적격 요소를 클릭할 때 동일한 활동에 대한 중복 정보를 포함합니다.
* 버그 수정:SDK에서 보낸 첫 번째 이벤트에 `documentUnloading`이(가) `true`으로 설정된 경우 [`sendBeacon`](https://developer.mozilla.org/ko-KR/docs/Web/API/Navigator/sendBeacon)이(가) 이벤트를 전송하는 데 사용되므로 ID가 설정되지 않은 경우 오류가 발생합니다.

## 버전 2.3.0, 2020년 11월

* 더 엄격한 컨텐츠 보안 정책을 허용하는 추가 지원을 추가했습니다.
* 단일 페이지 애플리케이션에 대한 개인화 지원을 추가했습니다.
* `window.console` API를 덮어쓸 수 있는 다른 페이지 JavaScript 코드와의 호환성을 개선했습니다.
* 버그 수정:`documentUnloading`이(가) `true`로 설정되었거나 링크 클릭이 자동으로 추적되었을 때 `sendBeacon`이(가) 사용되지 않았습니다.
* 버그 수정:앵커 요소에 HTML 내용이 포함되어 있으면 링크가 자동으로 추적되지 않습니다.
* 버그 수정:읽기 전용 `message` 속성을 포함하는 특정 브라우저 오류가 적절하게 처리되지 않아 고객에게 다른 오류가 표시됩니다.
* 버그 수정:iframe 내에서 SDK를 실행하면 iframe의 HTML 페이지가 상위 창의 HTML 페이지와 다른 하위 도메인의 경우 오류가 발생합니다.

## 버전 2.2.0, 2020년 10월

* 버그 수정:`idMigrationEnabled`이(가) `true`인 경우 Opt-in 개체가 합금으로 호출을 수행할 수 없도록 차단했습니다.
* 버그 수정:합금은 개인화 제안을 반환해야 하는 요청을 인식하여 깜박이는 문제를 방지합니다.

## 버전 2.1.0, 2020년 8월

* `syncIdentity` 명령을 제거하고 `sendEvent` 명령에서 해당 ID 전달을 지원합니다.
* IAB 2.0 동의 표준을 지원합니다.
* `setConsent` 명령에서 추가 ID 전달을 지원합니다.
* `sendEvent` 명령에서 `datasetId` 재정의가 지원됩니다.
* 합금 모니터 지원([자세히 보기](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 구현 세부 정보 컨텍스트 데이터에 `environment: browser`을(를) 전달합니다.
