---
title: Adobe Experience Platform Web SDK 릴리스 노트
description: Adobe Experience Platform Web SDK에 대한 최신 릴리스 정보입니다.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;릴리스 노트;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 777a1749670f36abc09e4bacd190b1be17a9a237
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 3%

---


# 릴리스 정보

이 문서에서는 Adobe Experience Platform Web SDK에 대한 릴리스 노트를 다룹니다.
웹 SDK 태그 확장에 대한 최신 릴리스 노트는 [웹 SDK 태그 확장 릴리스 노트](extension/web-sdk-ext-release-notes.md).

## 버전 2.13.0 - 2022년 9월 28일

**새로운 기능**

* 페이지별 전체 마이그레이션에 대한 지원이 추가되었습니다. 이제 방문자가 at.js와 Web SDK 페이지 간을 이동할 때 Adobe Target 프로필이 유지됩니다.
* 에 대한 구성 가능한 지원이 추가되었습니다. [높은 엔트로피 사용자 에이전트 클라이언트 힌트](fundamentals/user-agent-client-hints.md#high-entropy).
* 새로운 기능에 대한 지원이 추가되었습니다 `applyResponse` 명령. 이를 통해 다음을 통해 하이브리드 개인화를 사용할 수 있습니다 [Edge Network Server API](../server-api/overview.md).
* 이제 여러 페이지에서 QA 모드 링크가 작동합니다.

**수정 사항 및 향상된 기능**

* 링크 추적이 비활성화될 때 개인화 클릭 추적 지표가 업데이트되지 않는 문제를 해결했습니다.
* 알 수 없는 옵션이 지정된 경우 유효성 검사 오류를 발생하도록 명령을 업데이트했습니다.
* 다음 `_experience.decisioning.propositionEventType` 이제 디스플레이 및 상호 작용 개인화 이벤트를 자동으로 전송할 때 속성이 채워집니다.
* 에 대해 중복된 네임스페이스 유효성 검사가 추가되었습니다. `getIdentity` 명령.
* 에 대해 중복된 결정 범위 유효성 검사가 추가되었습니다. `sendEvent` 명령.

## 버전 2.12.0 - 2022년 6월 29일

* 요청을 Edge Network로 변경하여 `cluster` 쿠키 위치 힌트를 URL의 일부로 사용합니다. 따라서 VPN을 통해 위치를 변경하거나 모바일 장치 등을 사용하여 운전하는 등의 중간 세션을 사용하는 사용자가 동일한 에지를 히트하고 동일한 개인화 프로필을 갖도록 할 수 있습니다.
* getLibraryInfo 명령 응답에서 구성된 함수를 지정합니다.

## 버전 2.11.0 - 2022년 6월 13일

**새로운 기능**

* 이제 모바일 앱과 모바일 웹 콘텐츠 간 및 도메인 간에 방문자 ID를 공유하여 개인화된 경험을 더 정확하게 제공할 수 있습니다. 자세한 내용은 [전용 설명서](identity/id-sharing.md) 추가 정보
* 이제 다음 위치에서 일련의 proposition을 렌더링하거나 실행할 수 있습니다 [!DNL Adobe Target] analytics 지표를 증가시키지 않고 단일 페이지 애플리케이션에 기여합니다. 이렇게 하면 보고 오류가 줄어들고 분석 정확도가 높아집니다. 자세한 내용은 [전용 설명서](personalization/rendering-personalization-content.md#applypropositions) 추가 정보
* 에 추가 정보를 추가했습니다. `getLibraryInfo` 사용 가능한 명령과 인스턴스에 대한 최종 구성을 포함하는 명령

**수정 사항 및 향상된 기능**

* 사용할 쿠키 설정이 업데이트되었습니다. `sameSite="none"` 및 `secure` 플래그 [!DNL HTTPS] 페이지.
* 를 사용할 때 개인화된 콘텐츠가 올바르게 적용되지 않던 문제를 수정했습니다. `eq` 유사 선택기.
* 다음 상황에서 `localTimezoneOffset` Experience Platform 유효성 검사에 실패할 수 있습니다.

## 버전 2.10.1 - 2022년 5월 3일

* ID 동기화 및 세그먼트 대상에 대해 여러 영구 iframe이 생성되던 문제를 해결했습니다.

## 버전 2.10.0 - 2022년 4월 22일

* 모든 ID 동기화 및 세그먼트 대상에 영구 iframe을 사용합니다.
* 병합된 지표 포지션이 `sendEvent` 결과.

## 버전 2.9.0 - 2022년 3월 10일

* 추적에 대한 지원이 추가되었습니다 [!DNL control (default)] Adobe Target 경험.
* 단일 페이지 애플리케이션에 대해 보기 변경 이벤트를 최적화했습니다. 이제 개인화된 경험이 렌더링될 때 디스플레이 알림이 보기 변경 이벤트에 포함됩니다.
* 없을 때 콘솔 경고가 제거됨 `eventType` 이 있습니다.
* 이 `propositions` 속성은 `sendEvent` 캐시에서 경험을 요청하거나 검색할 때 명령 다음 `propositions` 이제 속성이 항상 배열로 정의됩니다.
* Adobe Experience Edge에서 반환된 오류가 있을 때 숨겨진 컨테이너가 표시되지 않던 문제를 수정했습니다.
* 상호 작용 이벤트가 Adobe Target에서 계산되지 않는 문제를 해결했습니다. 이 오류는 web.webPageDetails.viewName의 XDM에 보기 이름을 추가하여 수정되었습니다.
* 콘솔 메시지의 끊어진 설명서 링크를 수정합니다.

## 버전 2.8.0 - 2022년 1월 19일

* 개인화를 위해 섀도 DOM 선택기를 지원합니다.
* 개인화 이벤트 유형의 이름이 변경되었습니다. (`display` 및 `click` 다음과 같음 `decisioning.propositionDisplay` 및 `decisioning.propositionInteract`)
* 스크립트가 한 번만 실행되어도 인라인 스크립트 태그가 있는 HTML 오퍼이 페이지에 스크립트 태그를 두 번 추가하는 문제가 해결되었습니다.

## 버전 2.7.0 - 2021년 10월 26일

* 반환 값에서 Experience Edge의 추가 정보 표시 `sendEvent`, 포함 `inferences` 및 `destinations`. 이러한 기능은 현재 베타의 일부로 롤아웃되고 있으므로 이러한 속성의 형식이 변경될 수 있습니다. 자세한 내용은 [이벤트 추적.](fundamentals/tracking-events.md)

## 버전 2.6.4 - 2021년 9월 7일

* Adobe Target 설정 작업이 `head` 요소가 전체 `head` 컨텐츠 배포. 이제 다음에 적용되는 HTML 작업을 설정합니다. `head` HTML 추가으로 요소가 변경되었습니다.

## 버전 2.6.3 - 2021년 8월 16일

* 에서 확인된 약속을 통해 공용 목적이 아닌 개체가 노출되는 문제가 해결되었습니다. `configure` 명령.

## 버전 2.6.2 - 2021년 8월 4일

* 의 사용 중단에 대한 경고가 표시되는 문제가 해결되었습니다. `result.decisions` (제공) `sendEvent` 명령)은 `result.decisions` 속성에 액세스할 수 없습니다. 에 액세스할 때 경고가 기록되지 않습니다 `result.decisions` 속성은 여전히 더 이상 사용되지 않습니다.

## 버전 2.6.1 - 2021년 7월 29일

* 개인화 콘텐츠가 없는 단일 페이지 앱 보기에 대한 개인화를 렌더링하면 오류가 발생하고 다음에서 반환된 약속이 발생하는 문제를 수정했습니다 `sendEvent` 거부할 명령

## 버전 2.6.0 - 2021년 7월 27일

* 에서 더 많은 개인화 콘텐츠를 제공합니다 `sendEvent` Adobe Target 응답 토큰을 포함한 약속 이 해결되었습니다. 이 `sendEvent` 명령이 실행되면 약속이 반환되고, 결국 `result` 서버에서 받은 정보를 포함하는 개체입니다. 이전에는 이 결과 개체에 라는 속성이 포함되었습니다 `decisions`. 이 `decisions` 속성은 더 이상 사용되지 않습니다. 새 등록 정보, `propositions`이 추가되었습니다. 이 새 속성은 고객에게 다음을 포함한 더 많은 개인화 컨텐츠에 대한 액세스 권한을 제공합니다 [응답 토큰](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## 버전 2.5.0 - 2021년 6월

* 리디렉션 개인화 오퍼에 대한 지원을 추가했습니다.
* 음수 값인 자동으로 수집된 뷰포트 너비 및 높이는 더 이상 서버로 전송되지 않습니다.
* 를 반환하여 이벤트가 취소된 경우 `false` 변환 후 `onBeforeEventSend` callback, 이제 메시지가 기록됩니다.
* 단일 이벤트에 대한 특정 XDM 데이터 세트가 여러 이벤트에 포함되는 문제가 해결되었습니다.

## 버전 2.4.0 - 2021년 3월

* 이제 SDK를 [npm 패키지로 설치됨](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html?lang=ko-KR?lang=ko-KR).
* 에 대한 지원을 추가했습니다. `out` 옵션 [기본 동의 구성](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent): 동의를 받을 때까지 모든 이벤트를 삭제합니다(기존 `pending` 옵션은 이벤트를 큐에 넣고 동의를 받으면 전송합니다.)
* 다음 [onBeforeEventSend 콜백](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) 이제 를 사용하여 이벤트가 전송되지 않도록 할 수 있습니다.
* 이제 는 대신 XDM 스키마 필드 그룹을 사용합니다 `meta.personalization` 렌더링하거나 클릭하는 개인화된 콘텐츠에 대한 이벤트를 보낼 때.
* 다음 [getIdentity 명령](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) 이제 id와 함께 에지 영역 ID를 반환합니다.
* 서버에서 받은 경고 및 오류가 개선되었으며 보다 적절한 방식으로 처리됩니다.
* 에 대한 지원이 추가되었습니다 [Adobe의 동의 2.0 표준](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* 동의 환경 설정이 수신되면 CMP, Platform Web SDK 및 Platform Edge 네트워크 간의 최적화된 통합을 위해 로컬 저장소에 해시되고 저장됩니다. 동의 기본 설정을 수집하는 경우에는 다음을 호출하는 것이 좋습니다 `setConsent` 페이지를 로드할 때마다 at.
* 2 [후크 모니터링](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 및 `onCommandRejected`이 추가되었습니다.
* 버그 수정: 개인화 상호 작용 알림 이벤트는 사용자가 새로운 단일 페이지 앱 보기로 이동한 후 원래 보기로 돌아간 다음 전환을 위한 자격 요소를 클릭했을 때 동일한 활동에 대한 중복 정보를 포함합니다.
* 버그 수정: SDK에서 보낸 첫 번째 이벤트인 경우 `documentUnloading` 설정 `true`, [`sendBeacon`](https://developer.mozilla.org/ko-KR/docs/Web/API/Navigator/sendBeacon) 를 사용하여 이벤트를 전송하면 ID가 설정되지 않은 경우 오류가 발생합니다.

## 버전 2.3.0 - 2020년 11월

* 더 엄격한 컨텐츠 보안 정책을 허용하는 임시 지원이 추가되었습니다.
* 단일 페이지 애플리케이션에 대한 개인화 지원을 추가했습니다.
* 덮어쓸 수 있는 다른 페이지 JavaScript 코드와의 호환성을 개선했습니다 `window.console` API.
* 버그 수정: `sendBeacon` 다음 경우에 사용되지 않음 `documentUnloading` 이(가) `true` 또는 링크 클릭이 자동으로 추적되는 경우입니다.
* 버그 수정: 앵커 요소에 HTML 컨텐츠가 포함된 경우 링크가 자동으로 추적되지 않습니다.
* 버그 수정: 읽기 전용이 포함된 특정 브라우저 오류 `message` 속성이 적절하게 처리되지 않아 고객에게 다른 오류가 표시됩니다.
* 버그 수정: iframe 내에서 SDK를 실행하면 iframe의 HTML 페이지가 상위 창의 HTML 페이지와 다른 하위 도메인에서 나온 경우 오류가 발생합니다.

## 버전 2.2.0 - 2020년 10월

* 버그 수정: 옵트인 개체가 Alloy가 `idMigrationEnabled` is `true`.
* 버그 수정: 깜박이는 문제를 방지하기 위해 개인화 오퍼를 반환해야 하는 요청을 Alloy에서 인지합니다.

## 버전 2.1.0 - 2020년 8월

* 제거 `syncIdentity` 명령 및 지원 `sendEvent` 명령.
* IAB 2.0 동의 표준을 지원합니다.
* 에서 추가 ID 전달 지원 `setConsent` 명령.
* 재정의 지원 `datasetId` 에서 `sendEvent` 명령.
* 지원 합금 모니터([자세한 내용](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 패스 `environment: browser` 구현 세부 사항 컨텍스트 데이터
