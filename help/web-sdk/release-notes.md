---
title: Adobe Experience Platform Web SDK 릴리스 노트
description: Adobe Experience Platform Web SDK에 대한 최신 릴리스 정보입니다.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;릴리스 노트;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 1%

---


# 릴리스 정보

이 문서에서는 Adobe Experience Platform Web SDK에 대한 릴리스 정보를 다룹니다.
Web SDK 태그 확장에 대한 최신 릴리스 노트는 [Web SDK 태그 확장 릴리스 노트](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## 버전 2.19.2 - 2024년 1월 10일

**수정 사항 및 향상된 기능**

* ID 오류가 다른 오류를 마스킹하고 ID 오류를 경고로 변경하던 문제가 수정되었습니다.
* 의 상위 페이지 호출이 있는 경우 하위 페이지 호출이 전송되지 않는 문제가 해결되었습니다. `renderDecisions` 을 로 설정 `false`.
* 여러 개가 있는 경우 웹 SDK에서 도메인 간 ID를 읽지 못하는 문제가 해결되었습니다. `adobe_mc` 쿼리 문자열 매개 변수.

## 버전 2.19.1 - 2023년 11월 10일

**수정 사항 및 향상된 기능**

* 제안 배열이에서 반환되는 문제가 해결되었습니다. `sendEvent` 호출은 항상 비어 있었습니다.

## 버전 2.19.0 - 2023년 11월 1일

**새로운 기능**

* Adobe Journey Optimizer의 인앱 메시지 렌더링에 대한 지원이 추가되었습니다.
* 에 대한 지원이 추가됨 [페이지 이벤트 상단 및 하단](use-cases/top-bottom-page-events.md).
* 추가됨 [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) 옵션 `sendEvent` 페이지 범위 및 기본 표면 요청을 제어하는 명령입니다.

**수정 사항 및 향상된 기능**

* 결합된 개인화는 여러 유형의 개인화를 렌더링할 때 이벤트를 함께 표시합니다.
* 단일 페이지 애플리케이션 보기 이름이 대소문자를 구분하던 문제가 수정되었습니다.
* 그림자 DOM 맞춤형 오퍼 선택기 문제가 해결되었습니다.

## 버전 2.18.0 - 2023년 7월 31일

**새로운 기능**

* 에 대한 지원이 추가됨 [데이터스트림 ID의 명령별 재정의](../datastreams/overrides.md).

**수정 사항 및 향상된 기능**

* 도메인이 쿼리의 일부로 인해 종료 링크를 분류하지 못하는 문제가 해결되었습니다.
* 더 이상 사용되지 않음 `edgeConfigId` 에 찬성하여 `datastreamId` 웹 SDK 구성에서.

## 버전 2.17.0 - 2023년 5월 17일

**수정 사항 및 향상된 기능**

* 이제 웹 SDK는 다음과 유사하게 Audience Manager 쿠키 대상 값을 인코딩합니다. [Data Integration Library(DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=ko-KR).

## 버전 2.16.0 - 2023년 4월 25일

**새로운 기능**

* 에 대한 지원이 추가됨 [데이터 스트림 구성 무시](../datastreams/overrides.md).

## 버전 2.15.0 - 2023년 3월 30일

**새로운 기능**

* 에 대한 지원이 추가됨 [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) 링크 클릭 콜백.
* Adobe Journey Optimizer 클릭 추적에 대한 지원이 추가되었습니다.

**수정 사항 및 향상된 기능**

* 이제 링크 컬렉션에 링크 이름 및 방문자 영역이 포함됩니다.
* 실패한 URL 대상에 대한 콘솔 오류가 제거되었습니다.

## 버전 2.14.0 - 2023년 1월 25일

* (베타) Adobe Journey Optimizer 표면 및 제안에 대한 지원이 추가되었습니다.

**수정 사항 및 향상된 기능**

* 코드가 가 아닌 대체 위치에 주입된 Adobe Target VEC 사용자 지정 코드 작업 문제를 수정했습니다 [!DNL at.js].
* 일부 에지 사례에서 &quot;referer&quot; 헤더가 Edge Network에 대한 요청에 대해 제대로 설정되지 않던 문제를 해결했습니다.
* 다음과 같은 문제가 해결되었습니다. [사용자 에이전트 클라이언트 힌트](/help/web-sdk/use-cases/client-hints.md) 속성을 잘못된 유형으로 설정할 수 있습니다.
* 다음과 같은 문제가 해결되었습니다. `placeContext.localTime` 이(가) 스키마와 일치하지 않습니다.

## 버전 2.13.1 - 2022년 10월 13일

* 구성 후 window.Visitor가 정의된 경우 방문자 마이그레이션이 작동하지 않는 문제를 해결했습니다. 이는 Adobe 태그로 실행할 때 특히 문제가 됩니다.
* 다음과 같은 문제가 해결되었습니다. `device.screenWidth` 및 `device.screenHeight` 일부 환경에서 문자열로 채워집니다.

## 버전 2.13.0 - 2022년 9월 28일

**새로운 기능**

* 에 대한 지원이 추가됨 [페이지별 페이지 전체 마이그레이션](home.md#migrating-to-web-sdk). 이제 방문자가 at.js와 Web SDK 페이지 간을 이동할 때 Adobe Target 프로필이 유지됩니다.
* 에 대한 구성 가능한 지원이 추가되었습니다. [높은 엔트로피 사용자 에이전트 클라이언트 힌트](/help/web-sdk/use-cases/client-hints.md).
* 에 대한 지원이 추가되었습니다. [`applyResponse`](/help/web-sdk/commands/applyresponse.md) 명령입니다. 이렇게 하면 를 통해 하이브리드 개인화가 활성화됩니다. [Edge Network Server API](../server-api/overview.md).
* 이제 QA 모드 링크가 여러 페이지에서 작동합니다.

**수정 사항 및 향상된 기능**

* 링크 추적이 비활성화될 때 개인화 클릭 추적 지표가 업데이트되지 않던 문제를 수정했습니다.
* 알 수 없는 옵션이 지정되었을 때 유효성 검사 오류가 발생하도록 명령을 업데이트했습니다.
* 다음 `_experience.decisioning.propositionEventType` 이제 디스플레이 및 상호 작용 개인화 이벤트를 자동으로 전송할 때 속성이 채워집니다.
* 에 대한 중복 네임스페이스 유효성 검사가 추가되었습니다. `getIdentity` 명령입니다.
* 에 대해 중복된 결정 범위 유효성 검사가 추가되었습니다. `sendEvent` 명령입니다.

## 버전 2.12.0 - 2022년 6월 29일

* Edge Network에 대한 요청을 변경하여 `cluster` 쿠키 위치 힌트가 URL의 일부입니다. 이렇게 하면 중간 세션에서 위치를 변경하는(예: VPN을 통해 또는 모바일 장치로 운전하는 등) 사용자가 동일한 에지에 도달하고 동일한 개인화 프로필을 갖게 됩니다.
* getLibraryInfo 명령 응답에서 구성된 함수를 문자열 변환합니다.

## 버전 2.11.0 - 2022년 6월 13일

**새로운 기능**

* 이제 모바일 앱과 모바일 웹 콘텐츠 및 도메인 간에 방문자 ID를 공유하여 개인화된 경험을 보다 정확하게 제공할 수 있습니다. 다음을 참조하십시오. [전용 설명서](identity/id-sharing.md) 자세히 알아보십시오.
* 이제에서 제안 배열을 렌더링하거나 실행할 수 있습니다. [!DNL Adobe Target] analytics 지표를 증가시키지 않고 단일 페이지 애플리케이션으로 복제합니다. 이렇게 하면 보고 오류가 줄어들고 분석 정확도가 높아집니다. 다음을 참조하십시오. [전용 설명서](personalization/rendering-personalization-content.md#applypropositions) 자세히 알아보십시오.
* 에 추가 정보를 추가했습니다. `getLibraryInfo` 사용 가능한 명령을 포함하는 명령 및 인스턴스에 대한 최종 구성.

**수정 사항 및 향상된 기능**

* 사용할 쿠키 설정이 업데이트되었습니다. `sameSite="none"` 및 `secure` 플래그 설정 [!DNL HTTPS] 페이지.
* 를 사용할 때 개인화된 콘텐츠가 올바르게 적용되지 않던 문제를 수정했습니다. `eq` 의사 선택기입니다.
* 다음과 같은 문제가 해결되었습니다. `localTimezoneOffset` Experience Platform 유효성 검사에 실패할 수 있습니다.

## 버전 2.10.1 - 2022년 5월 3일

* ID 동기화 및 세그먼트 대상에 대해 여러 영구 iframe이 생성되던 문제를 수정했습니다.

## 버전 2.10.0 - 2022년 4월 22일

* 모든 ID 동기화 및 세그먼트 대상에 영구 iframe을 사용합니다.
* 에서 병합된 지표 제안이 복제되는 문제가 해결되었습니다. `sendEvent` 결과.

## 버전 2.9.0 - 2022년 3월 10일

* 추적에 대한 지원이 추가됨 [!DNL control (default)] Adobe Target 환경.
* 단일 페이지 애플리케이션에 대한 보기 변경 이벤트를 최적화했습니다. 이제 개인화된 경험이 렌더링될 때 표시 알림이 보기 변경 이벤트에 포함됩니다.
* 이(가) 없을 때 콘솔 경고가 제거됨 `eventType` 이(가) 있습니다.
* 이(가) 다음을 포함하는 문제가 해결되었습니다. `propositions` 속성은 다음에서 반환되었습니다. `sendEvent` 캐시에서 경험을 요청하거나 검색할 때의 명령입니다. 다음 `propositions` 이제 속성이 항상 배열로 정의됩니다.
* Edge Network에서 오류가 반환되었을 때 숨겨진 컨테이너가 표시되지 않던 문제를 수정했습니다.
* Adobe Target에서 상호 작용 이벤트가 계산되지 않던 문제를 수정했습니다. 이 문제는 web.webPageDetails.viewName에서 보기 이름을 XDM에 추가하여 해결되었습니다.
* 콘솔 메시지에서 끊어진 설명서 링크를 수정합니다.

## 버전 2.8.0 - 2022년 1월 19일

* 개인화를 위해 섀도 DOM 선택기를 지원합니다.
* 개인화 이벤트 유형 이름이 변경되었습니다. (`display` 및 `click` bear `decisioning.propositionDisplay` 및 `decisioning.propositionInteract`)
* 스크립트가 한 번만 실행되더라도 인라인 스크립트 태그가 있는 HTML 오퍼가 스크립트 태그를 페이지에 두 번 추가하는 문제를 해결했습니다.

## 버전 2.7.0 - 2021년 10월 26일

* 의 반환 값에 Edge Network의 추가 정보 표시 `sendEvent`, 포함 `inferences` 및 `destinations`. 이러한 기능은 현재 베타의 일부로 출시되고 있으므로 이러한 속성의 형식이 변경될 수 있습니다.

## 버전 2.6.4 - 2021년 9월 7일

* set HTML Adobe Target 작업이 `head` 요소가 전체를 대체하고 있습니다. `head` 콘텐츠. 이제 다음에 적용되는 HTML 작업 설정 `head` 요소가 추가 HTML으로 변경되었습니다.

## 버전 2.6.3 - 2021년 8월 16일

* 공용 사용이 아닌 개체가 의 해결된 약속을 통해 노출되는 문제를 해결했습니다. `configure` 명령입니다.

## 버전 2.6.2 - 2021년 8월 4일

* 의 사용 중단에 대한 경고가 표시되는 문제가 해결되었습니다. `result.decisions` (제공: `sendEvent` 명령)을 입력하면 콘솔에 `result.decisions` 속성에 액세스하지 못했습니다. 에 액세스할 때 경고가 기록되지 않습니다. `result.decisions` 속성은 삭제되지만 속성은 더 이상 사용되지 않습니다.

## 버전 2.6.1 - 2021년 7월 29일

* 개인화 콘텐츠가 없는 단일 페이지 앱 보기에 대한 개인화를 렌더링하면 오류가 발생하고 다음에서 약속이 반환되는 문제가 해결되었습니다. `sendEvent` 거부될 명령입니다.

## 버전 2.6.0 - 2021년 7월 27일

* 에서 더 많은 개인화 콘텐츠 제공 `sendEvent` Adobe Target 응답 토큰을 포함한 확인된 약속입니다. 다음의 경우 `sendEvent` 명령이 실행되면 약속이 반환되고, 이 약속은 결국 `result` 서버에서 받은 정보가 포함된 개체입니다. 이전에는 이 결과 개체에 라는 속성이 포함되었습니다. `decisions`. 이 `decisions` 속성이 더 이상 사용되지 않습니다. 새 속성, `propositions`이(가) 추가되었습니다. 이 새 속성을 통해 고객은 다음을 포함한 더 많은 개인화 콘텐츠에 액세스할 수 있습니다. [응답 토큰](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## 버전 2.5.0 - 2021년 6월

* 리디렉션 개인화 오퍼에 대한 지원이 추가되었습니다.
* 자동으로 수집된 뷰포트 너비 및 높이가 음수 값으로 더 이상 서버에 전송되지 않습니다.
* 재방문으로 이벤트가 취소된 경우 `false` 다음에서: `onBeforeEventSend` 콜백, 이제 메시지가 기록됩니다.
* 단일 이벤트용으로 설계된 특정 XDM 데이터가 여러 이벤트에 포함된 문제가 해결되었습니다.

## 버전 2.4.0 - 2021년 3월

* 이제 SDK를 다음으로 설치할 수 있습니다. [NPM 패키지](/help/web-sdk/install/npm.md).
* 에 대한 지원이 추가됨 `out` 옵션 [기본 동의 구성](/help/web-sdk/commands/configure/defaultconsent.md)- 동의를 받을 때까지 모든 이벤트를 삭제합니다(기존 `pending` 옵션은 이벤트를 큐에 넣고 동의를 받으면 보냅니다).
* 다음 [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) 이제 콜백을 사용하여 이벤트가 전송되지 않도록 할 수 있습니다.
* 이제 에서는 대신 XDM 스키마 필드 그룹을 사용합니다. `meta.personalization` 렌더링하거나 클릭하는 개인화된 콘텐츠에 대한 이벤트를 보낼 때.
* 다음 [`getIdentity`](/help/web-sdk/commands/getidentity.md) 이제 명령은 id와 함께 에지 영역 ID를 반환합니다.
* 서버에서 받은 경고 및 오류가 개선되었으며 더 적절한 방식으로 처리됩니다.
* 다음에 대한 Adobe 동의 2.0 표준에 대한 지원이 추가되었습니다. [`setConsent`](/help/web-sdk/commands/setconsent.md) 명령입니다.
* 동의 환경 설정이 수신되면 해시되어 CMP, Platform Web SDK 및 Platform Edge Network 간의 최적화된 통합을 위해 로컬 저장소에 저장됩니다. 동의 환경 설정을 수집하는 경우 `setConsent` 페이지를 로드할 때마다
* 2 [후크 모니터링](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 및 `onCommandRejected`이(가) 추가되었습니다.
* 버그 수정: 개인화 상호 작용 알림 이벤트에는 사용자가 새 단일 페이지 앱 보기로 이동했다가 원래 보기로 돌아간 다음 전환 대상 요소를 클릭할 때 동일한 활동에 대한 중복 정보가 포함됩니다.
* 버그 수정: SDK에서 보낸 첫 번째 이벤트에 `documentUnloading` 을 로 설정 `true`, [`sendBeacon`](https://developer.mozilla.org/ko-KR/docs/Web/API/Navigator/sendBeacon) 가 이벤트를 전송하는 데 사용되므로 id가 설정되지 않는 것과 관련된 오류가 발생합니다.

## 버전 2.3.0 - 2020년 11월

* 더 엄격한 콘텐츠 보안 정책을 허용하도록 nonce 지원이 추가되었습니다.
* 단일 페이지 애플리케이션에 대한 개인화 지원이 추가되었습니다.
* 덮어쓸 수 있는 다른 페이지 JavaScript 코드와의 호환성이 개선되었습니다. `window.console` API.
* 버그 수정: `sendBeacon` 이(가) 을(를) 사용하지 않는 경우 `documentUnloading` 이(가) (으)로 설정되었습니다. `true` 또는 링크 클릭이 자동으로 추적되는 경우입니다.
* 버그 수정: 앵커 요소에 HTML 콘텐츠가 포함된 경우 링크가 자동으로 추적되지 않습니다.
* 버그 수정: 읽기 전용이 포함된 특정 브라우저 오류 `message` 속성이 적절하게 처리되지 않아 다른 오류가 고객에게 노출되었습니다.
* 버그 수정: iframe의 HTML 페이지가 상위 창의 HTML 페이지가 아닌 다른 하위 도메인에서 온 경우 iframe 내에서 SDK를 실행하면 오류가 발생합니다.

## 버전 2.2.0 - 2020년 10월

* 버그 수정: 옵트인 개체는 다음의 경우에 웹 SDK가 호출하지 못하도록 차단합니다. `idMigrationEnabled` 은(는) `true`.
* 버그 수정: 웹 SDK에서 개인화 오퍼를 반환해야 하는 요청을 인식하도록 하여 깜박이는 문제를 방지합니다.

## 버전 2.1.0 - 2020년 8월

* 제거 `syncIdentity` 명령 및 지원에서 해당 ID 전달 `sendEvent` 명령입니다.
* IAB 2.0 동의 표준을 지원합니다.
* 에서 추가 ID 전달 지원 `setConsent` 명령입니다.
* 재정의 지원 `datasetId` 다음에서 `sendEvent` 명령입니다.
* 모니터링 후크 지원([자세히 보기](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 합격 `environment: browser` 구현 세부 사항 컨텍스트 데이터에서 확인할 수 있습니다.
