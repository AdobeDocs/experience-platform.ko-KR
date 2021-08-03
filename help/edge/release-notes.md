---
title: Adobe Experience Platform Web SDK 릴리스 노트
description: Adobe Experience Platform Web SDK에 대한 최신 릴리스 정보입니다.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;릴리스 노트;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 165c9bce5dabce9704202ebab6b97a4a30e4ca00
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 4%

---

# 릴리스 정보

## 버전 2.6.2 - 2021년 8월 4일

* `result.decisions` 속성에 액세스할 수 없는 경우에도 `sendEvent` 명령으로 제공되는 `result.decisions` 사용 중단 경고가 콘솔에 기록되는 문제가 해결되었습니다. `result.decisions` 속성에 액세스할 때 경고가 기록되지 않지만 속성은 계속 사용되지 않습니다.

## 버전 2.6.1 - 2021년 7월 29일

* 개인화 콘텐츠가 없는 단일 페이지 앱 보기에 대한 개인화를 렌더링하면 오류가 발생하고 `sendEvent` 명령에서 반환된 약속이 거부되는 문제가 해결되었습니다.

## 버전 2.6.0 - 2021년 7월 27일

* Adobe Target 응답 토큰을 포함하여 `sendEvent` 확인된 약속에서 더 많은 개인화 콘텐츠를 제공합니다. `sendEvent` 명령이 실행되면 약속이 반환되고, 이 작업은 서버에서 받은 정보가 포함된 `result` 개체로 해결됩니다. 이 결과 개체에는 `decisions` 속성이 포함되어 있습니다. 이 `decisions` 속성은 더 이상 사용되지 않습니다. 새 속성 `propositions`이 추가되었습니다. 이 새 속성은 고객에게 응답 토큰을 포함하여 더 많은 개인화 컨텐츠에 대한 액세스 권한을 제공합니다. 더 많은 설명서가 곧 제공될 예정입니다.

## 버전 2.5.0 - 2021년 6월

* 리디렉션 개인화 오퍼에 대한 지원을 추가했습니다.
* 음수 값인 자동으로 수집된 뷰포트 너비 및 높이는 더 이상 서버로 전송되지 않습니다.
* `onBeforeEventSend` 콜백에서 `false` 을 반환하여 이벤트가 취소되면 이제 메시지가 기록됩니다.
* 단일 이벤트에 대한 특정 XDM 데이터 세트가 여러 이벤트에 포함되는 문제가 해결되었습니다.

## 버전 2.4.0 - 2021년 3월

* 이제 SDK는 [npm 패키지](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=ko-KR)로 설치할 수 있습니다.
* [기본 동의](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)를 구성할 때 `out` 옵션에 대한 지원을 추가했습니다. 이 경우 동의를 받을 때까지 모든 이벤트가 삭제됩니다(기존 `pending` 옵션은 이벤트를 큐에 넣고 동의를 받으면 전송합니다.).
* 이제 [onBeforeEventSend 콜백](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend)을 사용하여 이벤트가 전송되지 않도록 할 수 있습니다.
* 이제 렌더링되거나 클릭되는 개인화된 컨텐츠에 대한 이벤트를 전송할 때 `meta.personalization` 대신 XDM 스키마 필드 그룹을 사용합니다.
* 이제 [getIdentity 명령](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id)이 ID와 함께 에지 영역 ID를 반환합니다.
* 서버에서 받은 경고 및 오류가 개선되었으며 보다 적절한 방식으로 처리됩니다.
* [Adobe의 동의 2.0 표준](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)에 대한 지원이 추가되었습니다.
* 동의 환경 설정이 수신되면 CMP, Platform Web SDK 및 Platform Edge 네트워크 간의 최적화된 통합을 위해 로컬 저장소에 해시되고 저장됩니다. 이제 동의 환경 설정을 수집하는 경우 페이지 로드 시마다 `setConsent`을 호출하는 것이 좋습니다.
* 두 개의 [모니터링 후크](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 및 `onCommandRejected`가 추가되었습니다.
* 버그 수정: 개인화 상호 작용 알림 이벤트는 사용자가 새로운 단일 페이지 앱 보기로 이동한 후 원래 보기로 돌아간 다음 전환을 위한 자격 요소를 클릭했을 때 동일한 활동에 대한 중복 정보를 포함합니다.
* 버그 수정: SDK에서 보낸 첫 번째 이벤트에서 `documentUnloading`이 `true`로 설정된 경우 [`sendBeacon`](https://developer.mozilla.org/ko-KR/docs/Web/API/Navigator/sendBeacon)가 이벤트를 전송하는 데 사용되어 ID가 설정되지 않은 경우 오류가 발생합니다.

## 버전 2.3.0 - 2020년 11월

* 더 엄격한 컨텐츠 보안 정책을 허용하는 임시 지원이 추가되었습니다.
* 단일 페이지 애플리케이션에 대한 개인화 지원을 추가했습니다.
* `window.console` API를 덮어쓸 수 있는 다른 페이지 JavaScript 코드와의 호환성을 개선했습니다.
* 버그 수정: `documentUnloading`이 `true`로 설정되어 있거나 링크 클릭이 자동으로 추적될 때 `sendBeacon`이 사용되지 않았습니다.
* 버그 수정: 앵커 요소에 HTML 콘텐츠가 포함되어 있으면 링크가 자동으로 추적되지 않습니다.
* 버그 수정: 읽기 전용 `message` 속성이 포함된 특정 브라우저 오류가 제대로 처리되지 않아 고객에게 다른 오류가 표시됩니다.
* 버그 수정: iframe 내에서 SDK를 실행하면 iframe의 HTML 페이지가 상위 창의 HTML 페이지와 다른 하위 도메인에서 나온 경우 오류가 발생합니다.

## 버전 2.2.0 - 2020년 10월

* 버그 수정: `idMigrationEnabled`이 `true`인 경우 Alloy가 호출을 하지 못하도록 옵트인 개체가 차단했습니다.
* 버그 수정: 깜박이는 문제를 방지하기 위해 개인화 오퍼를 반환해야 하는 요청을 Alloy에서 인지합니다.

## 버전 2.1.0 - 2020년 8월

* `syncIdentity` 명령을 제거하고 `sendEvent` 명령에서 해당 ID 전달을 지원합니다.
* IAB 2.0 동의 표준을 지원합니다.
* `setConsent` 명령에서 추가 ID 전달을 지원합니다.
* `sendEvent` 명령에서 `datasetId` 재정의를 지원합니다.
* 지원 합금 모니터([자세히 보기](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 구현 세부 사항 컨텍스트 데이터에 `environment: browser`을 전달합니다.
