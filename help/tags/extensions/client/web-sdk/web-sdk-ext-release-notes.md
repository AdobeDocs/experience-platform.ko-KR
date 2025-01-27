---
title: Adobe Experience Platform 웹 SDK 확장 릴리스 노트
description: Adobe Experience Platform 웹 SDK 태그 확장
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: 5bf69773d0502185bbe8db3b13cb2684d6d06ac4
workflow-type: tm+mt
source-wordcount: '2413'
ht-degree: 26%

---

# Adobe Experience Platform 웹 SDK 확장 릴리스 노트

이 문서에서는 Adobe Experience Platform Web SDK 태그 확장에 대한 릴리스 정보를 다룹니다. SDK 자체에 대한 최신 릴리스 노트는 [Platform Web SDK 릴리스 노트](/help/web-sdk/release-notes.md)를 참조하십시오.

## 버전 2.28.0 - 2025년 1월 23일 금요일

**수정 사항 및 개선 사항**

- Audience Manager을 활성화하지 않으면 ID 동기화 컨테이너 재정의를 설정할 수 없는 문제를 수정했습니다.
- 최신 버전으로 업그레이드할 때 데이터 스트림 구성 무시가 비활성화되는 문제를 해결했습니다.
- 사용자가 Target 자동 클릭 컬렉션 설정을 저장할 수 없는 문제를 해결했습니다.

**새로운 기능**

- XDM 오브젝트에서 기술 이름과 표시 이름 간을 전환하는 새 기능이 추가되었습니다.
- Adobe Experience Platform Web SDK의 [버전 2.25.0](../../../../web-sdk/release-notes.md#2-25-0)을 포함합니다.

## 버전 2.27.0 - 2024년 10월 31일 금요일

**새로운 기능**

- [데이터스트림 재정의](../web-sdk/web-sdk-extension-configuration.md#datastream-overrides)에 Experience Cloud 솔루션 및 Adobe Experience Platform 서비스를 비활성화하는 설정이 포함됩니다.
- 이제 미디어 세션에 대해 [데이터 스트림 무시](../web-sdk/web-sdk-extension-configuration.md)를 만들 수 있습니다.

Adobe Experience Platform Web SDK 버전 2.24.0을 포함합니다.

## 버전 2.26.1 - 2024년 9월 19일

**수정 사항 및 개선 사항**

- 웹 SDK을 로컬로 실행할 때 쿠키가 올바르게 작성되지 않는 문제를 해결했습니다.

Adobe Experience Platform Web SDK 버전 2.23.0을 포함합니다.

## 버전 2.26.0 - 2024년 8월 22일

**새로운 기능**

- 모니터링 후크 `triggered` 이벤트가 추가되었습니다.
- [안내 이벤트](action-types.md#instance), [기본 개인화 요청](action-types.md#personalization), [규칙 집합 항목 구독](event-types.md#subscribe-ruleset-items) 및 [규칙 집합 평가](action-types.md#evaluate-rulesets)를 이제 일반적으로 사용할 수 있습니다.

**수정 사항 및 개선 사항**

- 복제된 변수 데이터 요소가 서로 덮어쓰기될 수 있는 문제를 해결했습니다.
- [기본 개인화 요청](action-types.md#personalization) 안내 이벤트를 사용할 때 이제 시각적 개인화 결정이 자동으로 활성화됩니다.

Adobe Experience Platform Web SDK 버전 2.22.0을 포함합니다.

## 버전 2.25.0 - 2024년 7월 18일 금요일

**새로운 기능**

- Adobe Journey Optimizer에서 자동 추적 개인화에 대한 지원이 추가되었습니다.
- 향상된 클릭 컬렉션을 관리하는 새로운 설정이 도입되었습니다.

Adobe Experience Platform Web SDK 버전 2.21.1을 포함합니다.

## 버전 2.24.0 - 2024년 6월 5일 목요일

**수정 사항 및 개선 사항**

- 구성 재정의가 정의될 때 확장 구성을 수정할 때 발생하는 오류를 수정했습니다.
- 미디어 컬렉션 Ping 간격에 대해 빈 값을 설정할 수 있습니다.
- 변수 업데이트 작업을 수정할 때 발생하는 오류를 수정했습니다.
- 구성 재정의에서 ID 동기화 컨테이너 재설정을 허용합니다.

Adobe Experience Platform Web SDK 버전 2.20.0을 포함합니다.

## 버전 2.23.1 - 2024년 5월 28일 수요일

**새로운 기능**

- 확장 구성에 [`Streaming Media Collection`](web-sdk-extension-configuration.md#streaming-media) 구성 요소에 대한 지원을 추가했습니다.
- [!DNL Streaming Media Collection] 기능에 대한 [`Send Media Event`](action-types.md#send-media-event) 작업을 추가했습니다.
- [!DNL Streaming Media Collection] 기능에 대한 [`Media: Quality of Experience`](data-element-types.md#quality-experience) 데이터 요소를 추가했습니다.

Adobe Experience Platform Web SDK 버전 2.20.0을 포함합니다.

**수정 사항 및 개선 사항**

- [변수 업데이트](action-types.md#update-variable) 작업에서 데이터 요소를 검색할 때 발생하는 오류를 수정했습니다.
- `sendEvent` 작업에 사용하도록 권장된 이벤트 유형에서 [!UICONTROL Media] 이벤트 유형을 제거했습니다.

## 버전 2.22.0 - 2024년 5월 3일 토요일

**새로운 기능**

- 변수 데이터 요소를 확장하여 데이터 개체를 지원합니다.
- 이제 변수 업데이트 작업은 통과 Adobe Analytics, Adobe Audience Manager 및 Adobe Target 데이터 수정을 지원합니다.

Adobe Experience Platform Web SDK 버전 2.19.2를 포함합니다.

## 버전 2.21.4 - 2024년 1월 10일 목요일

**수정 사항 및 개선 사항**

- 3개의 환경 세트를 모두 설정하지 않고 구성 재정의를 저장하면 확장 UI가 충돌하던 문제가 해결되었습니다.
- 변수 업데이트 작업을 편집할 때 루트 기존 값 지우기 확인란이 채워지지 않는 문제를 해결했습니다.

Adobe Experience Platform Web SDK 버전 2.19.2를 포함합니다.

## 버전 2.21.3 - 2023년 11월 10일 토요일

Adobe Experience Platform Web SDK 버전 2.19.1을 포함합니다.

**수정 사항 및 개선 사항**

- `Send event complete` 이벤트에서 사용할 수 있는 제안 배열이 항상 비어 있는 문제가 해결되었습니다.

## 버전 2.21.2 - 2023년 11월 1일 목요일

**새로운 기능**

- 이벤트 작업을 보내는 `Request default personalization` 옵션을 추가했습니다.
- 이벤트 보내기 작업에서 페이지 이벤트의 상단 및 하단에 대한 지원을 추가했습니다.
- `Apply propositions` 작업이 추가되었습니다.
- 인앱 메시지에 대해 `Evaluate rulesets` 작업 및 `Subscribe ruleset items` 이벤트가 추가되었습니다.
- 이벤트 작업을 보낼 `Decision context`을(를) 추가했습니다.

**수정 사항 및 개선 사항**

- Adobe Experience Platform Web SDK 버전 2.19.0을 포함합니다.

## 버전 2.20.3 - 2023년 8월 8일

**수정 사항 및 개선 사항**

- ID 동기화 컨테이너 ID 재정의 필드에 데이터 요소를 저장할 수 없는 문제가 해결되었습니다.

## 버전 2.20.1 - 2023년 8월 3일

**수정 사항 및 개선 사항**

- 저장된 데이터 스트림 재정의 설정의 유효성 검사를 개선했습니다.

## 버전 2.20.0 - 2023년 7월 31일 화요일

**새로운 기능**

- 데이터 스트림 ID](../../../../datastreams/overrides.md)의 명령당 [재정의에 대한 지원을 추가했습니다.

**수정 사항 및 개선 사항**

- SDK 구성에서 `datastreamId`을(를) 위해 더 이상 사용되지 않는 `edgeConfigId`입니다.
- 데이터 스트림 구성에 대한 여러 사용자 경험 개선 사항이 사용자 인터페이스를 무시합니다.

## 버전 2.19.0 - 2023년 6월 21일 목요일

- 이제 **[!UICONTROL 변수]** 데이터 요소와 **[!UICONTROL 변수 업데이트]** 작업을 일반적으로 사용할 수 있습니다.

## 버전 2.18.0 - 2023년 5월 18일 금요일

- Adobe Experience Platform Web SDK 버전 2.17.0을 포함합니다.

## 버전 2.17.0 - 2023년 4월 25일

**새로운 기능**

- Adobe Experience Platform Web SDK 버전 2.16.0을 포함합니다.
- [데이터 스트림 구성 재정의](/help/datastreams/overrides.md)에 대한 지원이 추가되었습니다.
- `sendEvent` 명령의 `datasetId` 옵션에 사용 중단 알림을 추가합니다.

**수정 사항 및 개선 사항**

- Safari에서 스크롤하면 데이터 스트림 선택기가 닫히는 문제가 해결되었습니다.

## 버전 2.16.1 - 2023년 4월 14일

- 기본값이 아닌 샌드박스에서 스키마를 선택할 수 없는 XDM 개체 및 변수 데이터 요소 문제를 해결했습니다.

## 버전 2.16.0 - 2023년 3월 30일

**새로운 기능**

- (Beta) **[!UICONTROL 변수 업데이트]** 작업과 **[!UICONTROL 변수]** 데이터 요소를 추가했습니다.
- [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) 콜백 함수에 대한 구성을 추가했습니다.

**수정 사항 및 개선 사항**

- **[!UICONTROL ID를 사용하여 리디렉션]** 작업을 사용할 때 앵커 태그 내의 요소를 클릭하는 기능이 작동하지 않는 문제를 해결했습니다.
- 스키마가 하나만 있을 때 XDM 개체 데이터 요소가 작동하지 않는 문제를 수정했습니다.
- Adobe Experience Platform Web SDK 버전 2.15.0을 포함합니다.

## 버전 2.15.1 - 2023년 1월 26일 금요일

- 데이터스트림에 액세스할 수 없는 사용자가 확장 구성을 편집할 수 없는 문제를 해결했습니다.
- `sendEvent` 작업에서 표면에 대한 지원을 추가했습니다.

Adobe Experience Platform Web SDK 버전 2.14.0을 포함합니다.

## 버전 2.14.1 - 2022년 10월 13일 금요일

- 웹 SDK에서 Experience Cloud ID 서비스의 ID를 승인하지 않는 문제가 해결되었습니다.

Adobe Experience Platform Web SDK 라이브러리 버전 2.13.1을 포함합니다.

## 버전 2.14.0 - 2022년 9월 28일

- 페이지 전체 마이그레이션을 활성화하는 새 `targetMigrationEnabled` 구성을 추가했습니다.
- 하이브리드 서버-클라이언트 구현을 활성화하는 응답 적용 작업이 추가되었습니다.
- 높은 엔트로피 사용자 에이전트 클라이언트 힌트 컨텍스트 옵션이 추가되었습니다.

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.13.0을 포함합니다.

## 버전 2.13.0 - 2022년 6월 29일 목요일

- XDM 개체 데이터 요소에서 eVar와 같은 숫자 속성의 정렬 순서를 수정했습니다.

Adobe Experience Platform Web SDK 라이브러리 버전 2.12.0을 포함합니다.

## 버전 2.12.0 - 2022년 6월 13일 화요일

- 확장 설정에 정의된 샌드박스를 기반으로 네임스페이스 옵션을 채우도록 `identityMap` 데이터 요소를 업데이트했습니다.
- 도메인 간 ID 공유를 허용하기 위해 **[!UICONTROL ID로 리디렉션]** 작업이 추가되었습니다.
- `sendEvent` 작업에 대한 설명서 링크를 추가했습니다.
- React 스펙트럼 UI 라이브러리가 업그레이드되었습니다.
- 다양한 사용자 인터페이스 개선 사항.

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.11.0을 포함합니다.

## 버전 2.11.2 - 2022년 5월 3일 수요일

Adobe Experience Platform Web SDK 라이브러리 버전 2.10.1을 포함합니다.

## 버전 2.11.1 - 2022년 4월 22일

- 버전 2.11.0의 구성 명령 오류를 수정했습니다.

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.10.0을 포함합니다.

## 버전 2.11.0 - 2022년 4월 22일

- 태그 UI 성능이 향상되었습니다.
- 샌드박스 선택기를 데이터스트림 확장 구성에 추가합니다.

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.10.0을 포함합니다.

## 버전 2.10.0 - 2022년 3월 10일

- 업데이트된 Adobe Target VEC 편집기에서 작동하도록 구성 페이지에서 복사할 수 있는 코드 조각 사전 숨김을 업데이트합니다.

Adobe Experience Platform Web SDK 라이브러리의 버전 2.9.0을 포함합니다.

## 버전 2.9.0 - 2022년 1월 19일 목요일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.8.0을 포함합니다.

## 버전 2.8.0 - 2021년 10월 26일 수요일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.7.0을 포함합니다.

- `inferences` 및 `destinations`을(를) 포함하여 Edge Network 완료 보내기 이벤트에서 이벤트의 추가 정보를 사용할 수 있습니다. 이러한 기능은 현재 Beta의 일부로 롤아웃되고 있으므로 이러한 속성의 형식이 변경될 수 있습니다.

## 버전 2.7.3 - 2021년 9월 7일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.6.4를 포함합니다.

- `container.buildInfo.environment.`에 대한 사용 중단 경고가 더 이상 없습니다.

## 버전 2.7.0 - 2021년 8월 16일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.6.3을 포함합니다.

- ID 맵 데이터 요소 유형을 사용할 때 ID가 채워지지 않은 문자열로 확인되는 식별자는 이제 ID 맵에서 자동으로 제거됩니다.
- XDM 개체 데이터 요소 유형을 사용하여 데이터 요소를 저장하려고 할 때 스키마를 선택하지 않았을 때 발생하는 오류를 해결했습니다.
- 사용자 인터페이스 타이포그래피가 개선되었습니다.

## 버전 2.6.2 - 2021년 8월 4일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.6.2를 포함합니다.

## 버전 2.6.1 - 2021년 7월 29일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.6.1을 포함합니다.

## 버전 2.6.0 - 2021년 7월 27일 수요일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.6.0을 포함합니다.

- &quot;에지 구성&quot;이라는 용어를 사용하는 레이블, 설명 및 오류 메시지가 &quot;데이터스트림&quot;이라는 용어를 사용하여 최신 Adobe Experience Platform 용어에 맞게 변경되었습니다.
- 확장 구성 보기에서 많은 수의 데이터스트림 및 데이터스트림 환경을 처리하기 위한 지원이 추가되었습니다.
- XDM 개체 데이터 요소 보기에서 많은 스키마를 처리하는 지원이 추가되었습니다.
- 이벤트를 서버로 전송하고 응답을 받은 후 규칙을 실행하는 데 사용할 수 있는 이벤트 전송 완료 이벤트 유형이 추가되었습니다. 곧 추가 설명서를 사용할 수 있습니다.
- 수신된 결정 이벤트 유형은 더 이상 사용되지 않습니다. 대신 이벤트 전송 완료 이벤트 유형을 사용하십시오.
- 사용자 인터페이스 및 오류 처리가 전반적으로 개선되었습니다.

## 버전 2.5.0 - 2021년 6월 1일 수요일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.5.0을 포함합니다.

- 이벤트 보내기 작업에 `data` 필드를 추가했습니다. 향후 설명서에서는 특정 시나리오에서 이 기능을 사용하는 방법을 설명합니다.
- XDM 개체 데이터 요소 보기에서 사용자가 Adobe Experience Platform 샌드박스에 액세스할 수 있지만 조직의 기본값으로 구성된 샌드박스에 액세스할 수 없는 경우 오류가 발생하는 문제가 수정되었습니다.
- XDM 개체 데이터 요소 보기에서 상위 개체에 값이 없는 경우에도 필수 스키마 필드가 유효하지 않은 것으로 간주되는 문제가 수정되었습니다.

## 버전 2.4.0 - 2021년 3월 9일

Adobe Experience Platform Web SDK 라이브러리의 버전 2.4.0을 포함합니다.

- 이벤트 작업 UI 보내기에 [&quot;문서 언로딩&quot;](/help/web-sdk/commands/sendevent/documentunloading.md) 확인란이 추가되었습니다.
- [기본 동의를 구성](/help/web-sdk/commands/configure/defaultconsent.md)할 때 `out` 옵션에 대한 지원이 추가되었습니다. 이 옵션은 동의를 받을 때까지 모든 이벤트를 삭제합니다(기존 `pending` 옵션은 이벤트를 큐에 넣고 동의를 받으면 전송합니다).
- 기본 동의 필드에 도구 설명을 추가했습니다.
- [`setConsent`](/help/web-sdk/commands/setconsent.md) 명령을 사용할 때 Adobe의 동의 2.0 표준에 대한 지원이 추가되었습니다.
- 사용자의 액세스 토큰이 잘못되었거나 잘못 제공된 경우 XDM 개체 데이터 요소 UI에 더 나은 오류가 표시됩니다.
- XDM 개체 데이터 요소를 볼 때 브라우저 개발자 콘솔에 표시되는 교차 원본 오류(확장 작업에 영향을 주지 않음)가 수정되었습니다.

## 버전 2.3.0 - 2020년 11월 4일 목요일

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.3.0을 포함합니다.

- 기본 동의를 구성할 때 데이터 요소 사용에 대한 지원이 추가되었습니다.
- XDM 개체 데이터 요소 유형으로 XDM 스키마를 검색하는 기능이 추가되었습니다.
- XDM 데이터 개체의 후속 변경 내용이 요청에 반영되지 않도록 이벤트 보내기 작업 유형 내에 XDM 데이터 복제가 추가되었습니다.

## 버전 2.2.0 - 2020년 10월 1일 금요일

- 고객이 샌드박스 스키마에서 XDM 개체를 만들려고 했을 때 인증 문제가 발생했습니다. Platform을 호출하는 API는 이제 환경을 인식하므로 사용자가 편집할 수 있는 액세스 권한이 있는 스키마만 표시됩니다.
- `identityMap` 데이터 요소를 사용할 때 이제 네임스페이스가 드롭다운에 미리 채워지므로 수동으로 채우지 않아도 됩니다.
- `xdmObject` 데이터 요소의 UI를 개선했습니다. 새 UI에서는 개체의 각 항목을 입력하지 않고도 채운 필드를 확인할 수 있습니다.

## 버전 2.1.1 - 2020년 8월 26일

- XDM 개체 보기의 Adobe Experience Platform 샌드박스가 잘못 표시되는 문제를 수정했습니다. 이 버전의 확장 프로그램을 사용할 때 예상 샌드박스가 목록에 표시되지 않으면 사용자는 Adobe Experience Platform 관리자에게 문의하여 액세스 권한이 올바르게 설정되었는지 확인해야 합니다.

## 버전 2.1.0 - 2020년 8월 5일

- 변경 내용: `syncIdentity` 작업을 제거하고 대신 `sendEvent` 작업에서 이러한 ID를 전달할 수 있도록 지원합니다. 확장을 업그레이드하기 전에 이 작업을 사용하여 기존 규칙을 비활성화하십시오.
- Alloy v. 2.1.0로 업데이트([릴리스 노트](/help/web-sdk/release-notes.md))
- `setConsent` 작업에서 IAB 2.0 동의 표준을 지원합니다.
- `sendEvent` 작업에서 데이터 세트 ID 재정의를 지원합니다.
- 이제 활성화된 XDM 개체 데이터 요소와 `IdentityMap` 작업에 `identityMap` 항목을 채우는 데 사용할 수 있는 `setConsent` 유형의 새 데이터 요소를 추가합니다.
- `setConsent` 작업에서 ID 맵 전달을 지원합니다.
- XDM 개체 데이터 요소에서 Platform 샌드박스 선택을 지원합니다.

## 버전 1.0.0 - 2020년 5월 26일 수요일

- 구성 서비스에서 환경 선택을 지원합니다.

## 버전 0.1.2 - 2020년 5월 4일 화요일

- `configId`가 `edgeConfigId`로 이름이 변경되었습니다.
- `viewStart`가 `renderDecisions`로 이름이 변경된 경우 기본적으로 false로 설정됩니다. true로 설정하면 개인화 오퍼를 가져와서 자동으로 렌더링됩니다.
- `Get Decisions` 관련 변경 사항:
   - `getDecisions` 명령이 제거되었습니다.
   - `scopes` 옵션이 `sendEvent` 명령에 추가되었습니다. 결정은 `sendEvent`에서 확인된 약속에서 반환됩니다.
   - 페이지/보기 전체 오퍼를 반환하는 내장 `__view__` 범위가 추가되었습니다. (예: Target의 VEC 오퍼)
`renderDecisions`이(가) false로 설정된 경우에만 `sendEvent` 명령에서 이러한 결과가 반환됩니다.
   - 결정을 사용할 수 있을 때 발생하는 `Decisions Received` 이벤트가 추가되었습니다.
- 단일 서버 호출에 여러 개인화 알림이 결합되었습니다.
- 데이터 요소가 참조될 때마다 재설정되는 이벤트 병합 ID의 문제가 해결되었습니다.
- `setCustomerIds` 작업 이름이 `syncIdentity`로 변경되었습니다.
- `getIdentity` 명령이 추가되었습니다. 현재는 사용자 지정 코드를 통해서만 사용할 수 있습니다.
- `_satellite`을(를) 사용하여 디버그를 활성화하면 Adobe Experience Platform 웹 SDK에서 디버깅이 활성화됩니다.
- XDM 개체에 입력 값(부울, 숫자 및 소수점)에 대한 지원이 추가되었습니다.

## 버전 0.0.10 - 2020년 3월 16일

- `Consent` 아래에 옵트인 및 옵트아웃의 개념을 결합하고 새 `setConsent` 명령을 추가했습니다.
- JavaScript/JSON에서 XDM으로 매핑을 허용하는 새로운 데이터 요소 유형 `XDM Object`가 추가되었습니다.

## 버전 0.0.7 - 2020년 2월 18일

- idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled 및 cookieDestinationsEnabled 옵션이 제거됨
- edgeDomain 옵션값에 하이픈 지원이 추가됨
- demdex 쿠키가 설정되지 않은 경우 ID 마이그레이션 중에 이루어진 요청은 도메인 간 식별을 개선하기 위해 demdex 종단점으로 전송됨
- ID 마이그레이션 중에 이루어진 요청은 항상 ID 쿠키를 설정하기 위해 응답이 필요함
- 잘못된 명령을 실행하면 콘솔에 유효한 명령 이름 목록이 기록됨
- 타사 쿠키 지원을 태그 확장으로 전환하는 확인란이 추가되었습니다. 이 확인란을 선택하면 demdex.net 호출이 비활성화됨

## 버전 0.0.5 - 2019년 12월 20일 토요일

- 태그 확장에 Activity Tracker 구성 추가
- 이벤트 명령에 EventType 및 EventMergeId 표시
- 태그 확장에 onBeforeEventSend 구성 추가
- 태그 확장에 edgeBasePath 구성 추가

## 버전 0.0.3 - 2019년 11월 25일 화요일

- 이벤트 보내기 작업의 새 병합 ID 및 유형 필드입니다. 병합 ID는 XDM 스키마에서 `xdm.eventMergeID`에 매핑되고 유형은 XDM 스키마에서 `xdm.eventType`에 매핑됩니다.

## 버전 0.0.2 - 2019년 11월 18일 화요일

- 초기 릴리스
