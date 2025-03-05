---
title: Adobe Experience Platform Web SDK 릴리스 노트
description: Adobe Experience Platform Web SDK에 대한 최신 릴리스 정보입니다.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;릴리스 정보;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 8fd86a170433c4eb07a7370dbd3aa2cb3ef10922
workflow-type: tm+mt
source-wordcount: '2285'
ht-degree: 5%

---


# 릴리스 정보

이 문서에서는 Adobe Experience Platform Web SDK의 릴리스 정보를 다룹니다.
웹 SDK 태그 확장에 대한 최신 릴리스 노트는 [웹 SDK 태그 확장 릴리스 노트](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md)를 참조하십시오.

## 버전 2.26.0 - 2025년 3월 5일

**새로운 기능**

- 이제 웹 SDK NPM 패키지를 사용하여 사용자 지정 웹 SDK 빌드를 만들고 필요한 라이브러리 구성 요소만 선택할 수 있습니다. 이로 인해 라이브러리 크기가 줄어들고 로드 시간이 최적화됩니다. [NPM 패키지를 사용하여 사용자 지정 웹 SDK 빌드를 만드는 방법](install/create-custom-build.md)에 대한 설명서를 참조하십시오.
- 이제 [`getIdentity`](commands/getidentity.md) 명령이 `kndctr` ID 쿠키에서 직접 ECID를 자동으로 읽습니다. `ECID` 네임스페이스로 `getIdentity`을(를) 호출하고 ID 쿠키가 이미 있는 경우 Web SDK에서 더 이상 Edge Network에 ID 가져오기 요청을 하지 않습니다. 이제 쿠키에서 ID를 읽습니다.

**수정 사항 및 개선 사항**

- `collect` 호출이 전송된 후 `getIdentity` 명령이 ID를 반환하지 않는 문제가 해결되었습니다.
- 개인화 리디렉션으로 인해 리디렉션이 발생하기 전에 콘텐츠가 깜박거리는 문제가 해결되었습니다.

## 버전 2.25.0 - 2025년 1월 23일 금요일

**수정 및 개선 사항**

- `setDebug` 명령에 옵션 유효성 검사가 추가되었습니다.
- 클릭 컬렉션을 사용하지 않도록 설정할 때 `onBeforeLinkClickSend` 함수 또는 다운로드 링크 한정자를 구성할 때 경고가 추가되었습니다.
- 렌더링된 제안이 디스플레이 알림에 포함되지 않던 문제를 수정했습니다.

**새로운 기능**

- 서드파티 쿠키가 활성화되고 adobedc.demdex.net에 대한 요청이 차단되는 경우 구성된 Edge 도메인에 대한 폴백이 구현되었습니다.

## 버전 2.24.1 - 2024년 12월 6일 토요일

**수정 및 개선 사항**

- 일부 고객 통합에서 오류를 발생하는 [Adobe Experience Platform 규칙 엔진](https://github.com/adobe/aepsdk-rulesengine-typescript/)과(와) 관련된 종속성 문제를 해결했습니다. 이제 웹 SDK에 [Adobe Experience Platform 규칙 엔진](https://github.com/adobe/aepsdk-rulesengine-typescript/) 버전 2.0.3 이상이 필요합니다.

## 버전 2.24.0 - 2024년 10월 31일 금요일

**새로운 기능**

- 미디어 세션을 시작할 때 [데이터 스트림 무시](../datastreams/overrides.md)가 지원됩니다.

- [`onContentRendering`](monitoring-hooks.md#onContentRendering)모니터링 후크에서 Adobe Target 응답 토큰에 대한 지원을 추가했습니다.

**수정 사항 및 개선 사항**

- 여러 인앱 메시지가 반환되면 우선 순위가 가장 높은 메시지만 표시됩니다. 다른 항목은 억제된 것으로 기록됩니다.
- 빈 데이터 스트림 재정의는 더 이상 Edge Network으로 전송되지 않으므로 서버측 라우팅 구성과의 잠재적 충돌을 줄일 수 있습니다.
- 다른 Adobe SDK와 맞추기 위해 다음 로깅 메시지 구성 요소 이름의 이름을 변경했습니다.
   - `DecisioningEngine` 이름이 `RulesEngine`(으)로 바뀌었습니다.
   - `LegacyMediaAnalytics` 이름이 `MediaAnalyticsBridge`(으)로 바뀌었습니다.
   - `Privacy` 이름이 `Consent`(으)로 바뀌었습니다.
- 기본 콘텐츠 항목이 [`applyPropositions`](../web-sdk/commands/applypropositions.md)을(를) 통해 렌더링될 때 발생하는 오류를 해결했습니다.
- Adobe Target 이동 및 크기 조정 작업의 CSS 오류를 수정했습니다.
- [`sendEvent`](../web-sdk/commands/sendevent/overview.md) 응답에서 `machineLearning` 키를 제거했습니다.

## 버전 2.23.0 - 2024년 9월 19일

**새로운 기능**

- [getIdentity](commands/getidentity.md#get-identity-using-the-web-sdk-javascript-library) 명령에서 [CORE ID](identity/overview.md#tracking-coreid-web-sdk) 요청에 대한 지원을 추가했습니다.

**수정 사항 및 개선 사항**

- 웹 SDK을 로컬로 실행할 때 쿠키가 올바르게 작성되지 않는 문제를 해결했습니다.

## 버전 2.22.0 - 2024년 8월 22일

**새로운 기능**

- 개인화 모니터링 후크에 대한 지원을 추가했습니다.

**수정 사항 및 개선 사항**

- Internet Explorer에 대한 지원을 제거하여 라이브러리 gzip 크기를 9% 줄였습니다.
- `onInstanceConfigured` 모니터 후크를 호출할 때 Activity Map 링크 세부 정보가 초기화되지 않는 문제를 해결했습니다.
- 쿠키 대상이 올바른 경로로 설정되지 않던 문제를 수정했습니다.
- 에 대한 호출과 관련된 고객 문제가 해결되었습니다.
- `adobe_mc` 매개 변수의 잘못된 URL 인코딩으로 인해 [sendEvent](commands/sendevent/overview.md) 호출이 실패하는 문제가 해결되었습니다.

## 버전 2.21.1 - 2024년 7월 18일 금요일

**수정 사항 및 개선 사항**

- NPM 라이브러리를 사용할 때 발생하는 빌드 오류를 수정했습니다.

## 버전 2.21.0 - 2024년 7월 16일 수요일

**새로운 기능**

- 자동 제안 상호 작용 추적에 대한 지원이 추가되었습니다.
- alloy.js 파일을 제공하는 사용자 지정 빌드 스크립트가 추가되었습니다.
- ActivityMap 및 이벤트 그룹화 지원을 통해 클릭 수집이 개선되었습니다.

## 버전 2.20.0 - 2024년 5월 21일 수요일

**새로운 기능**

- [스트리밍 미디어 컬렉션](../web-sdk/commands/configure/streamingmedia.md)에 대한 지원을 추가했습니다.

**수정 사항 및 개선 사항**

- 동의가 옵트아웃되면 코드 조각 사전 숨김에 의해 기본 콘텐츠가 숨겨지는 버그를 수정했습니다.

## 버전 2.19.2 - 2024년 1월 10일 목요일

**수정 사항 및 개선 사항**

- ID 오류가 다른 오류를 마스킹하고 ID 오류를 경고로 변경하던 문제가 수정되었습니다.
- `renderDecisions`이(가) `false`(으)로 설정된 상위 페이지 호출이 있는 경우 하위 페이지 호출이 전송되지 않는 문제가 해결되었습니다.
- `adobe_mc` 쿼리 문자열 매개 변수가 여러 개 있는 경우 웹 SDK에서 도메인 간 ID를 읽지 못하는 문제가 해결되었습니다.

## 버전 2.19.1 - 2023년 11월 10일 토요일

**수정 사항 및 개선 사항**

- `sendEvent` 호출에서 반환된 제안 배열이 항상 비어 있는 문제가 해결되었습니다.

## 버전 2.19.0 - 2023년 11월 1일 목요일

**새로운 기능**

- Adobe Journey Optimizer의 인앱 메시지 렌더링에 대한 지원이 추가되었습니다.
- [페이지 이벤트의 상단 및 하단](use-cases/top-bottom-page-events.md)에 대한 지원을 추가했습니다.
- 페이지 전체 범위 및 기본 표면 요청을 제어하기 위해 [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) 옵션을 `sendEvent` 명령에 추가했습니다.

**수정 사항 및 개선 사항**

- 결합된 개인화는 여러 유형의 개인화를 렌더링할 때 이벤트를 함께 표시합니다.
- 단일 페이지 애플리케이션 보기 이름이 대소문자를 구분하던 문제가 수정되었습니다.
- 그림자 DOM 맞춤형 오퍼 선택기 문제가 해결되었습니다.

## 버전 2.18.0 - 2023년 7월 31일 화요일

**새로운 기능**

- 데이터 스트림 ID](../datastreams/overrides.md)의 명령당 [재정의에 대한 지원을 추가했습니다.

**수정 사항 및 개선 사항**

- 도메인이 쿼리의 일부로 인해 종료 링크를 분류하지 못하는 문제가 해결되었습니다.
- 웹 SDK 구성에서 `datastreamId`을(를) 위해 더 이상 사용되지 않는 `edgeConfigId`입니다.

## 버전 2.17.0 - 2023년 5월 17일 목요일

**수정 사항 및 개선 사항**

- 이제 웹 SDK이 [Data Integration Library(DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=ko-KR)과(와) 유사한 Audience Manager 쿠키 대상 값을 인코딩합니다.

## 버전 2.16.0 - 2023년 4월 25일

**새로운 기능**

- [데이터 스트림 구성 재정의](../datastreams/overrides.md)에 대한 지원이 추가되었습니다.

## 버전 2.15.0 - 2023년 3월 30일

**새로운 기능**

- [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) 링크 클릭 콜백에 대한 지원을 추가했습니다.
- Adobe Journey Optimizer 클릭 추적에 대한 지원이 추가되었습니다.

**수정 사항 및 개선 사항**

- 이제 링크 컬렉션에 링크 이름 및 방문자 영역이 포함됩니다.
- 실패한 URL 대상에 대한 콘솔 오류가 제거되었습니다.

## 버전 2.14.0 - 2023년 1월 25일 목요일

- (Beta) Adobe Journey Optimizer 표면 및 제안에 대한 지원이 추가되었습니다.

**수정 사항 및 개선 사항**

- [!DNL at.js]이(가) 아닌 대체 위치에 코드가 주입된 Adobe Target VEC 사용자 지정 코드 작업 문제를 수정했습니다.
- 일부 경계 사례에서 &quot;referer&quot; 헤더가 Edge Network에 대한 요청에 대해 제대로 설정되지 않는 문제가 해결되었습니다.
- [사용자 에이전트 클라이언트 힌트](/help/web-sdk/use-cases/client-hints.md) 속성을 잘못된 유형으로 설정할 수 있는 문제를 해결했습니다.
- `placeContext.localTime`이(가) 스키마와 일치하지 않는 문제를 해결했습니다.

## 버전 2.13.1 - 2022년 10월 13일 금요일

- 구성 후 window.Visitor가 정의된 경우 방문자 마이그레이션이 작동하지 않는 문제를 해결했습니다. 이 문제는 Adobe 태그로 실행할 때 특히 발생합니다.
- 일부 환경에서 `device.screenWidth` 및 `device.screenHeight`이(가) 문자열로 채워지는 문제를 해결했습니다.

## 버전 2.13.0 - 2022년 9월 28일

**새로운 기능**

- [페이지 전체 마이그레이션](home.md#migrating-to-web-sdk)에 대한 지원을 추가했습니다. 이제 Adobe Target 프로필은 방문자가 at.js와 웹 SDK 페이지 간을 이동할 때 보존됩니다.
- [높은 엔트로피 사용자 에이전트 클라이언트 힌트](/help/web-sdk/use-cases/client-hints.md)에 대한 구성 가능한 지원이 추가되었습니다.
- [`applyResponse`](/help/web-sdk/commands/applyresponse.md) 명령에 대한 지원을 추가했습니다. 이렇게 하면 [Edge Network Server API](../server-api/overview.md)를 통해 하이브리드 개인화가 가능합니다.
- 이제 QA 모드 링크가 여러 페이지에서 작동합니다.

**수정 사항 및 개선 사항**

- 링크 추적이 비활성화될 때 개인화 클릭 추적 지표가 업데이트되지 않던 문제를 수정했습니다.
- 알 수 없는 옵션이 지정되었을 때 유효성 검사 오류가 발생하도록 명령을 업데이트했습니다.
- 이제 표시 및 상호 작용 개인화 이벤트를 자동으로 전송할 때 `_experience.decisioning.propositionEventType` 속성이 채워집니다.
- `getIdentity` 명령에 대해 중복된 네임스페이스 유효성 검사가 추가되었습니다.
- `sendEvent` 명령에 대해 중복된 결정 범위 유효성 검사가 추가되었습니다.

## 버전 2.12.0 - 2022년 6월 29일 목요일

- `cluster` 쿠키 위치 힌트를 URL의 일부로 사용하도록 Edge Network에 대한 요청을 변경하십시오. 이렇게 하면 중간 세션에서 위치를 변경하는(예: VPN을 통해 또는 모바일 장치로 운전하는 등) 사용자가 동일한 에지에 도달하고 동일한 개인화 프로필을 갖게 됩니다.
- getLibraryInfo 명령 응답에서 구성된 함수를 문자열 변환합니다.

## 버전 2.11.0 - 2022년 6월 13일 화요일

**새로운 기능**

- 이제 모바일 앱과 모바일 웹 콘텐츠 및 도메인 간에 방문자 ID를 공유하여 개인화된 경험을 보다 정확하게 제공할 수 있습니다. 자세한 내용은 [전용 설명서](identity/id-sharing.md)를 참조하세요.
- 이제 분석 지표를 증가시키지 않고도 [!DNL Adobe Target]의 제안 배열을 단일 페이지 애플리케이션으로 렌더링하거나 실행할 수 있습니다. 이렇게 하면 보고 오류가 줄어들고 분석 정확도가 높아집니다. 자세한 내용은 [전용 설명서](personalization/rendering-personalization-content.md#applypropositions)를 참조하세요.
- 사용 가능한 명령 및 인스턴스에 대한 최종 구성을 포함하여 `getLibraryInfo` 명령에 추가 정보를 추가했습니다.

**수정 사항 및 개선 사항**

- [!DNL HTTPS] 페이지에서 `sameSite="none"` 및 `secure` 플래그를 사용하도록 쿠키 설정을 업데이트했습니다.
- `eq` 의사 선택기를 사용할 때 개인화된 콘텐츠가 올바르게 적용되지 않던 문제를 해결했습니다.
- `localTimezoneOffset`이(가) Experience Platform 유효성 검사에 실패할 수 있는 문제를 해결했습니다.

## 버전 2.10.1 - 2022년 5월 3일 수요일

- ID 동기화 및 세그먼트 대상에 대해 여러 영구 iframe이 생성되던 문제를 수정했습니다.

## 버전 2.10.0 - 2022년 4월 22일

- 모든 ID 동기화 및 세그먼트 대상에 영구 iframe을 사용합니다.
- 병합된 지표 제안이 `sendEvent` 결과에서 중복되던 문제를 해결했습니다.

## 버전 2.9.0 - 2022년 3월 10일

- [!DNL control (default)] Adobe Target 경험 추적에 대한 지원이 추가되었습니다.
- 단일 페이지 애플리케이션에 대한 보기 변경 이벤트를 최적화했습니다. 이제 개인화된 경험이 렌더링될 때 표시 알림이 보기 변경 이벤트에 포함됩니다.
- `eventType`이(가) 없는 경우 콘솔 경고가 제거되었습니다.
- 캐시에서 경험을 요청하거나 검색할 때 `sendEvent` 명령에서만 `propositions` 속성이 반환되던 문제를 해결했습니다. 이제 `propositions` 속성이 항상 배열로 정의됩니다.
- Edge Network에서 오류가 반환되었을 때 숨겨진 컨테이너가 표시되지 않던 문제를 수정했습니다.
- Adobe Target에서 상호 작용 이벤트가 계산되지 않던 문제를 수정했습니다. 이 문제는 web.webPageDetails.viewName에서 보기 이름을 XDM에 추가하여 해결되었습니다.
- 콘솔 메시지에서 끊어진 설명서 링크를 수정합니다.

## 버전 2.8.0 - 2022년 1월 19일 목요일

- 개인화를 위해 섀도 DOM 선택기를 지원합니다.
- 개인화 이벤트 유형 이름이 변경되었습니다. (`display` 및 `click`이(가) `decisioning.propositionDisplay` 및 `decisioning.propositionInteract`이(가) 됨)
- 스크립트가 한 번만 실행되는데도 인라인 스크립트 태그가 있는 HTML 오퍼가 스크립트 태그를 페이지에 두 번 추가하던 문제를 수정했습니다.

## 버전 2.7.0 - 2021년 10월 26일 수요일

- `inferences` 및 `destinations`을(를) 포함하여 `sendEvent`의 반환 값에 Edge Network의 추가 정보를 노출합니다. 이러한 기능은 현재 Beta의 일부로 롤아웃되고 있으므로 이러한 속성의 형식이 변경될 수 있습니다.

## 버전 2.6.4 - 2021년 9월 7일

- `head` 요소에 적용된 HTML Adobe Target 설정 작업이 전체 `head` 콘텐츠를 바꾸는 문제가 해결되었습니다. 이제 `head` 요소에 적용된 HTML 설정 작업이 HTML을 추가하도록 변경되었습니다.

## 버전 2.6.3 - 2021년 8월 16일

- 공용 사용이 아닌 개체가 `configure` 명령에서 확인된 약속을 통해 노출되는 문제를 해결했습니다.

## 버전 2.6.2 - 2021년 8월 4일

- `result.decisions` 속성에 액세스하지 않는 경우에도 `sendEvent` 명령으로 제공된 `result.decisions`의 사용 중단에 대한 경고가 콘솔에 기록되는 문제를 해결했습니다. `result.decisions` 속성에 액세스할 때 경고가 기록되지 않지만 속성은 더 이상 사용되지 않습니다.

## 버전 2.6.1 - 2021년 7월 29일 금요일

- 개인화 콘텐츠가 없는 단일 페이지 앱 보기에 대한 개인화를 렌더링하면 오류가 발생하고 `sendEvent` 명령에서 반환된 약속이 거부되는 문제가 해결되었습니다.

## 버전 2.6.0 - 2021년 7월 27일 수요일

- Adobe Target 응답 토큰을 포함하여 `sendEvent` 확인된 약속에 더 많은 개인화 콘텐츠를 제공합니다. `sendEvent` 명령이 실행되면 약속이 반환되고 서버에서 받은 정보가 포함된 `result` 개체로 해결됩니다. 이전에는 이 결과 개체에 이름이 `decisions`인 속성이 포함되었습니다. 이 `decisions` 속성은 더 이상 사용되지 않습니다. 새 속성 `propositions`이(가) 추가되었습니다. 이 새 속성은 [응답 토큰](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md)을(를) 포함하여 더 많은 개인화 콘텐츠에 액세스할 수 있는 권한을 고객에게 제공합니다.

## 버전 2.5.0 - 2021년 6월

- 리디렉션 개인화 오퍼에 대한 지원이 추가되었습니다.
- 자동으로 수집된 뷰포트 너비 및 높이가 음수 값으로 더 이상 서버에 전송되지 않습니다.
- `onBeforeEventSend` 콜백에서 `false`을(를) 반환하여 이벤트가 취소되면 이제 메시지가 기록됩니다.
- 단일 이벤트용으로 설계된 특정 XDM 데이터가 여러 이벤트에 포함된 문제가 해결되었습니다.

## 버전 2.4.0 - 2021년 3월

- 이제 SDK을 [NPM 패키지](/help/web-sdk/install/npm.md)(으)로 설치할 수 있습니다.
- [기본 동의를 구성](/help/web-sdk/commands/configure/defaultconsent.md)할 때 `out` 옵션에 대한 지원이 추가되었습니다. 이 옵션은 동의를 받을 때까지 모든 이벤트를 삭제합니다(기존 `pending` 옵션은 이벤트를 큐에 넣고 동의를 받으면 전송합니다).
- 이제 [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) 콜백을 사용하여 이벤트가 전송되지 않도록 할 수 있습니다.
- 이제 렌더링하거나 클릭하는 개인화된 콘텐츠에 대한 이벤트를 보낼 때 `meta.personalization` 대신 XDM 스키마 필드 그룹을 사용합니다.
- 이제 [`getIdentity`](/help/web-sdk/commands/getidentity.md) 명령이 ID와 함께 에지 영역 ID를 반환합니다.
- 서버에서 받은 경고 및 오류가 개선되었으며 더 적절한 방식으로 처리됩니다.
- [`setConsent`](/help/web-sdk/commands/setconsent.md) 명령에 대한 Adobe 동의 2.0 표준에 대한 지원이 추가되었습니다.
- 동의 환경 설정이 수신되면 해시되어 CMP, Platform Web SDK 및 Platform Edge Network 간의 최적화된 통합을 위해 로컬 저장소에 저장됩니다. 동의 환경 설정을 수집하는 경우 이제 모든 페이지 로드 시 `setConsent`을(를) 호출하는 것이 좋습니다.
- [모니터링 후크](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` 및 `onCommandRejected` 두 개가 추가되었습니다.
- 버그 수정: Personalization 상호 작용 알림 이벤트에는 사용자가 새 단일 페이지 앱 보기로 이동했다가 원래 보기로 돌아간 후, 전환을 위해 자격을 갖춘 요소를 클릭할 때 동일한 활동에 대한 중복 정보가 포함됩니다.
- 버그 수정: SDK에서 보낸 첫 번째 이벤트에 `documentUnloading`이(가) `true`(으)로 설정된 경우 [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon)이(가) 이벤트를 보내는 데 사용되므로 ID가 설정되지 않는 것과 관련된 오류가 발생합니다.

## 버전 2.3.0 - 2020년 11월

- 더 엄격한 콘텐츠 보안 정책을 허용하도록 nonce 지원이 추가되었습니다.
- 단일 페이지 애플리케이션에 대한 개인화 지원이 추가되었습니다.
- `window.console` API를 덮어쓸 수 있는 다른 페이지 내 JavaScript 코드와의 호환성을 개선했습니다.
- 버그 수정: `documentUnloading`이(가) `true`(으)로 설정되었거나 링크 클릭이 자동으로 추적되는 경우 `sendBeacon`이(가) 사용되지 않습니다.
- 버그 수정: 앵커 요소에 HTML 콘텐츠가 포함되어 있으면 링크가 자동으로 추적되지 않습니다.
- 버그 수정: 읽기 전용 `message` 속성이 포함된 특정 브라우저 오류가 적절하게 처리되지 않아 다른 오류가 고객에게 노출되었습니다.
- 버그 수정: iframe의 SDK 페이지가 상위 창의 HTML 페이지와 다른 하위 도메인에서 온 경우 iframe 내에서 HTML을 실행하면 오류가 발생합니다.

## 버전 2.2.0 - 2020년 10월

- 버그 수정: `idMigrationEnabled`이(가) `true`일 때 옵트인 개체가 웹 SDK에서 호출을 하지 못하도록 차단하고 있습니다.
- 버그 수정: 웹 SDK에서 깜박이는 문제를 방지하기 위해 개인화 오퍼를 반환해야 하는 요청을 인식하도록 합니다.

## 버전 2.1.0 - 2020년 8월

- `syncIdentity` 명령을 제거하고 `sendEvent` 명령에서 해당 ID를 전달할 수 있도록 지원합니다.
- IAB 2.0 동의 표준을 지원합니다.
- `setConsent` 명령에서 추가 ID 전달을 지원합니다.
- `sendEvent` 명령에서 `datasetId` 재정의를 지원합니다.
- 모니터링 후크 지원([자세한 내용](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- 구현 세부 정보 컨텍스트 데이터에 `environment: browser`을(를) 전달합니다.
