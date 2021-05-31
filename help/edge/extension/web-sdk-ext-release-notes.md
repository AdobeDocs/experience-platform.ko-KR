---
title: Adobe Experience Platform Web SDK Extension 릴리스 노트
description: Adobe Experience Platform Launch의 Adobe Experience Platform 웹 SDK 확장
seo-description: Adobe Experience Platform Launch의 Adobe Experience Platform 웹 SDK 확장
exl-id: 91de8c91-023a-45b6-9f67-ac75ee471e50
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 78%

---

# Adobe Experience Platform Web SDK 확장 릴리스 노트

이 문서에서는 Adobe Experience Platform Launch용 Adobe Experience Platform 웹 SDK 확장에 대한 릴리스 노트를 다룹니다. SDK 자체에 대한 최신 릴리스 노트는 [Platform Web SDK 릴리스 노트](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html)를 참조하십시오.

## 2020년 3월 9일

### Adobe Experience Platform 웹 SDK 2.4.0

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.4.0을 포함합니다.

* 이벤트 보내기 작업 UI에 [&quot;document reloading&quot;](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) 확인란이 추가되었습니다.
* 동의를 받을 때까지 모든 이벤트를 삭제하는 [기본 동의](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent)를 구성할 때 `out` 옵션에 대한 지원이 추가되었습니다(기존 `pending` 옵션은 이벤트를 큐에 넣고 동의를 받으면 전송합니다.).
* 기본 동의 필드에 도구 설명이 추가되었습니다.
* [Adobe의 동의 2.0 표준](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard)에 대한 지원이 추가되었습니다.
* 사용자의 액세스 토큰이 잘못되었거나 잘못 제공된 경우 이제 XDM 개체 데이터 요소 UI에 더 나은 오류가 표시됩니다.
* XDM 개체 데이터 요소를 볼 때 브라우저 개발자 콘솔에 표시되는 원본 간 오류(확장의 작업에 영향을 주지 않음)를 수정했습니다.

## 2020년 11월 4일

### Adobe Experience Platform 웹 SDK 2.3.0

Adobe Experience Platform 웹 SDK 라이브러리의 버전 2.3.0을 포함합니다.

#### 기능

* 기본 동의를 구성할 때 데이터 요소 사용에 대한 지원이 추가되었습니다.
* XDM 개체 데이터 요소 유형으로 XDM 스키마를 검색하는 기능이 추가되었습니다.
* XDM 데이터 개체의 후속 변경 내용이 요청에 반영되지 않도록 이벤트 보내기 작업 유형 내에 XDM 데이터 복제가 추가되었습니다.

## 2020년 10월 1일

### Adobe Experience Platform 웹 SDK 2.2.0

#### 버그 수정

* 고객이 샌드박스 스키마에서 XDM 개체를 만들려고 했을 때 인증 문제가 발생했습니다. Platform을 호출하는 API는 이제 환경을 인식하므로 사용자가 편집할 수 있는 액세스 권한이 있는 스키마만 표시됩니다.

#### 기능

* `identityMap` 데이터 요소를 사용할 때 이제 네임스페이스가 드롭다운에서 미리 채워지므로 수동으로 일일이 채우지 않아도 됩니다.
* `xdmObject` 데이터 요소의 UI를 개선했습니다. 새 UI에서는 개체의 각 항목을 입력하지 않고도 채운 필드를 확인할 수 있습니다.


## 2020년 8월 26일

### Adobe Experience Platform 웹 SDK 2.1.1

#### 기능

* XDM 개체 보기의 Adobe Experience Platform 샌드박스가 잘못 표시되는 문제를 수정했습니다. 이 버전의 확장 프로그램을 사용할 때 예상 샌드박스가 목록에 표시되지 않으면 사용자는 Adobe Experience Platform 관리자에게 문의하여 액세스 권한이 올바르게 설정되었는지 확인해야 합니다.


## 2020년 8월 5일

### Adobe Experience Platform 웹 SDK 2.1.0

#### 기능

* 변경 내용: `syncIdentity` 작업을 제거하고 대신 `sendEvent` 작업에서 이러한 ID를 전달할 수 있도록 지원합니다. 확장을 업그레이드하기 전에 이 작업을 사용하여 기존 규칙을 비활성화하십시오.
* Alloy v. 2.1.0로 업데이트([릴리스 노트](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html))
* `setConsent` 작업에서 IAB 2.0 동의 표준을 지원합니다.
* `sendEvent` 작업에서 데이터 세트 ID 재정의를 지원합니다.
* 이제 활성화된 XDM 개체 데이터 요소와 `IdentityMap` 작업에 `identityMap` 항목을 채우는 데 사용할 수 있는 `setConsent` 유형의 새 데이터 요소를 추가합니다.
* `setConsent` 작업에서 ID 맵 전달을 지원합니다.
* XDM 개체 데이터 요소에서 Platform 샌드박스 선택을 지원합니다.


## 2020년 5월 26일

### Adobe Experience Platform 웹 SDK 1.0.0

#### 기능

* 구성 서비스에서 환경 선택을 지원합니다.


## 2020년 5월 4일

### Adobe Experience Platform 웹 SDK 0.1.2

#### 기능

* `configId`가 `edgeConfigId`로 이름이 변경되었습니다.
* `viewStart`가 `renderDecisions`로 이름이 변경된 경우 기본적으로 false로 설정됩니다. true로 설정하면 개인화 오퍼를 가져와서 자동으로 렌더링됩니다.
* `Get Decisions` 관련 변경 사항:
   * `getDecisions` 명령이 제거되었습니다.
   * `scopes` 옵션이 `sendEvent` 명령에 추가되었습니다. 결정은 `sendEvent`에서 확인된 약속에서 반환됩니다.
   * 페이지/보기 전체 오퍼를 반환하는 내장 `__view__` 범위가 추가되었습니다. (예: Target의 VEC 오퍼)
`renderDecisions`가 false로 설정된 경우에만 `sendEvent` 명령에서 이러한 결과가 반환됩니다.
   * 결정을 사용할 수 있을 때 발생하는 `Decisions Received` 이벤트가 추가되었습니다.
* 단일 서버 호출에 여러 개인화 알림이 결합되었습니다.
* 데이터 요소가 참조될 때마다 재설정되는 이벤트 병합 ID의 문제가 해결되었습니다.
* `setCustomerIds` 작업 이름이 `syncIdentity`로 변경되었습니다.
* `getIdentity` 명령이 추가되었습니다. 현재는 사용자 지정 코드를 통해서만 사용할 수 있습니다.
* 이제 `_satellite`을 사용하여 디버그를 활성화하면 Adobe Experience Platform Web SDK에서 디버깅이 활성화됩니다.
* XDM 개체에 입력 값(부울, 숫자 및 소수점)에 대한 지원이 추가되었습니다.

## 2020년 3월 16일

### Adobe Experience Platform 웹 SDK 0.0.10

#### 기능

* `Consent` 아래에 옵트인 및 옵트아웃의 개념을 결합하고 새 `setConsent` 명령을 추가했습니다.
* JavaScript/JSON에서 XDM으로 매핑을 허용하는 새로운 데이터 요소 유형 `XDM Object`가 추가되었습니다.

## 2020년 2월 18일

### Adobe Experience Platform 웹 SDK 0.0.7

#### 기능

* idSyncContainerId, datasetId, schemaId, urlDestinationsEnabled 및 cookieDestinationsEnabled 옵션이 제거됨
* edgeDomain 옵션값에 하이픈 지원이 추가됨
* demdex 쿠키가 설정되지 않은 경우 ID 마이그레이션 중에 이루어진 요청은 도메인 간 식별을 개선하기 위해 demdex 종단점으로 전송됨
* ID 마이그레이션 중에 이루어진 요청은 항상 ID 쿠키를 설정하기 위해 응답이 필요함
* 잘못된 명령을 실행하면 콘솔에 유효한 명령 이름 목록이 기록됨
* 타사 쿠키 지원을 Adobe Experience Platform Launch 확장으로 전환하는 확인란이 추가되었습니다. 이 확인란을 선택하면 demdex.net 호출이 비활성화됨

## 2019년 12월 20일

### Adobe Experience Platform 웹 SDK 0.0.5

#### 기능

* Platform Launch 확장에 Activity Tracker 구성 추가
* 이벤트 명령에 EventType 및 EventMergeId 표시
* Platform Launch 확장에 onBeforeEventSend 구성 추가
* Platform Launch 확장에 edgeBasePath 구성 추가

#### 다음 변경 사항이 포함된 Alloy v. 0.0.10으로 업데이트하십시오.

* 클라이언트 스토리지 구현: 서버로 이동한 상태 및 쿠키 논리
* 이벤트 명령에 EventType 및 EventMergeId 표시
* 종료 링크 이외의 링크 추적에는 sendBeacon 사용
* ID 동기화 마이너스 만료 확인 가져오기
* SSL(http)이 아닌 페이지에서 id를 해싱하지 않은 setCustomerIds 명령
* 상태/쿠키를 설정할 때 사용할 서버에 APEX 도메인을 전달
* 새로운 핸들 유형을 사용하여 응답에서 ECID 선택
* 활성화 및 ID 구성의 기본값 제거
* 이름 바꾸기 + 메타로 쿼리 옵션 이동
* 기존 ECID 마이그레이션

#### 버그 수정

* 예기치 않은 상태 코드에서 오류 메시지에 대한 응답을 분석하고 형식을 지정
* 디버그 명령 실행 또는 comply_debug 사용은 구성에 의해 덮어쓰기

## 2019년 11월 25일

### Adobe Experience Platform 웹 SDK 0.0.3

#### 기능

* 이벤트 보내기 작업의 새 병합 ID 및 유형 필드입니다. 병합 ID는 XDM 스키마에서 `xdm.eventMergeID`에 매핑되고 유형은 XDM 스키마에서 `xdm.eventType`에 매핑됩니다.
* 향상된 오류 처리 및 보고
* 이제 모든 링크에 `sendBeacon` 사용

#### 버그 수정

* 쿼리 문자열 매개 변수를 통해 디버깅을 전환하거나 `debug` 명령이 세션을 통해 지속되지 않는 문제를 해결했습니다.

## 2019년 11월 18일

### Adobe Experience Platform 웹 SDK 0.0.2

#### 기능

* 확장이 존재하게 됨
* 추가 라이브러리 또는 네트워크 호출 없이 ECID 지원
* 옵트인 지원
* XDM을 플랫폼으로 전송 지원
* 자사 도메인 지원
* 브라우저 컨텍스트 자동 수집
* 전체 오픈 소스([확장](https://github.com/adobe/reactor-extension-alloy), [SDK](https://github.com/adobe/reactor-extension-alloy))
* 자세한 로깅
* 프로덕션 단계에서 오류 숨기기 기능
