---
title: Adobe Target v2 확장에 대한 릴리스 노트
description: Adobe Experience Platform의 Adobe Target v2 태그 확장에 대한 최신 릴리스 노트입니다.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: e086359916b3aeef73ba9c98e1bfa13da5a974cd
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 26%

---

# Adobe Target v2 확장 릴리스 노트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform에서 데이터 수집 기술 세트로 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

## v0.19.2(2023년 2월 14일)

- 시간 제한을 데이터 요소로 설정할 수 있는 문제를 수정했습니다.

## v0.19.0(2022년 9월 19일)

- 을 지원하도록 업데이트됨 `at.js` v2.10.0
- 도메인 간 추적 지원이 추가되었습니다.

## v0.18.0(2022년 6월 1일)

- 을 지원하도록 업데이트됨 `at.js` v2.9.0
- 사용자 에이전트 클라이언트 힌트 지원이 추가되었습니다.

## v0.17.1(2022년 1월 28일)

- 을 지원하도록 업데이트됨 `at.js` v2.8.1
- 고정 `pageLoad` 매핑되지 않음 `target-global-mbox` ODD 하이브리드 실행 모드에서
- Analytics 세부 사항 관련 문제가 해결되었습니다. `mbox` 요청
- 보안 취약성을 해결하기 위해 개발 종속성이 업그레이드되었습니다

## v0.17.0(2022년 1월 7일)

- 을 지원하도록 업데이트됨 `at.js` 이제 기능 사용 및 성능 원격 분석 데이터를 수집하는 v2.8.0입니다.  개인 데이터는 수집되지 않습니다. 이 기능을 옵트아웃하려면 다음을 설정합니다. `telemetryEnabled` to `false` in `targetGlobalSettings`.

## v0.16.0(2021년 10월 28일)

- 을 지원하도록 업데이트됨 `at.js` 이제 Adobe Target에서 다운로드할 수 있는 v2.7.0을 다운로드하십시오.

## v0.15.1(2021년 7월 20일)

- 다음 문제를 수정했습니다. `stringify` 함수 이름 충돌이 발생하여 UUID 값이 잘못 생성되었습니다. `sessionId`, `requestId`등

## v0.15.0(2021년 7월 16일)

- 항상 쿠키에 보안 속성 추가 `at.js` secureOnly 설정이 true로 설정되어 있습니다.
- 이제 응답 토큰을 사용할 수 있습니다 `triggerView()`
- 와 관련된 버그가 수정되었습니다. `CONTENT_RENDERING_NO_OFFERS` 이벤트. 이제 Target에서 반환된 컨텐츠가 없을 때마다 올바르게 트리거됩니다
- 미리 가져오기 요청을 사용할 때 A4T 클릭 지표 세부 사항이 올바르게 반환됩니다
- UUID 생성에서 더 이상 를 사용하지 않음 `Math.random()`, 그러나 는 `window.crypto`
- `sessionId` 쿠키 만료는 모든 네트워크 호출에서 올바르게 확장됩니다
- 이제 SPA 보기 캐시 초기화가 올바르게 처리되고 적용됩니다 `viewsEnable` 설정

## v0.14.2(2021년 6월 2일)

- 최종 번들에 두 개의 버그가 포함되어 있는 버그를 수정합니다 `at.js` 버전, On-Device Decisioning이 있는 버전 및 없는 버전.

## v0.14.1(2021년 5월 19일)

- Target 로드 작업이 글로벌 mbox 호출을 실행하는 v0.14 릴리스에서 도입된 회귀 수정

## v0.14(2021년 5월 14일)

- 을 사용하여 새 작업 로드 Target 추가 [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning): `at.js` On-Device Decisioning 기능 포함 2.5
- 업데이트됨 `at.js` to 2.5


## v0.13.7(2021년 3월 25일)

- mbox 요청에 포함되는 `targetPageParams`에 관한 문제가 해결되었습니다. `targetPageParams` 는 `pageLoad` 요청.
- 전역 개체 종속성을 직접 참조로 대체하여 태그 확장에서 문서 및 창 전역 개체 문제를 해결했습니다.
- 업데이트됨 `at.js` 변환 후: 2.4.1.

## v0.13.6(2021년 1월 25일)

- 통합 프로필/플랫폼 ID에 대한 지원을 게재 API customerId에 추가
- 잘못된 스타일 태그 삽입 수정
- at.s가 2.4.0으로 업데이트되었습니다.
- 정의되지 않은 매개 변수가 잘못된 게재 요청을 초래할 수 있는 문제가 해결되었습니다.

## v0.13.4(2020년 11월 25일)

- mbox 매개 변수가 UI에 표시되지 않던 버그를 수정했습니다.
- 브랜딩 업데이트
- 업데이트 날짜: `at.js` 버전 2.3.3으로

## v0.13.3(2020년 7월 24일)

- 비활성 활동에 대해 QA 모드 링크가 작동하지 않던 버그를 수정했습니다
- 스크립트나 코드가 `default` 속성을 `window` 또는 `document`에 추가할 때 확장에 실패하는 경우 버그를 수정했습니다

## v0.13.2(2020년 6월 15일)

- CNAME 및 Edge Override를 사용할 때 발생하는 문제가 해결되었습니다. `at.js` 1.x가 서버 도메인을 잘못 만들어 Target 요청이 실패할 수 있습니다
- Target 및 Adobe Analytics 태그 확장에 v2 태그 확장을 사용할 때 Target이 Analytics sendBeacon 호출을 지연하는 문제가 해결되었습니다.
- `deviceIdLifetime`을 통해 재정의 가능하도록 하여 `targetGlobalSettings` 설정을 개선했습니다.

## v0.13.0(2020년 3월 25일)

- 업데이트됨 `at.js` v2.3으로 이동합니다.
- adobe.target.getOffer API에 Target Global Mbox 지원 추가됨
- 매개 변수 및 페이지 로드 매개 변수가 올바르게 처리되지 않는 문제가 해결되었습니다.

## v0.12.0 (2019년 10월 10일)

- 업데이트됨 `at.js` v2.2로 업그레이드했습니다.
- ECID(Experience Cloud ID 라이브러리) v4.4와 간의 통합을 위해 성능이 향상되었습니다 `at.js` 2.2.
- 이전에는 ECID 라이브러리가 두 개의 차단 호출을 생성했습니다 `at.js` 경험을 가져올 수 있습니다. 이는 단일 호출로 감소하여 성능이 크게 향상되었습니다.

>[!NOTE]
>ECID 태그 확장을 v4.4.1로 업그레이드하여 향상된 성능을 이용해 보십시오.

## v0.11.1(2019년 7월 31일)

- 사용할 확장 버전이 업데이트되었습니다. `at.js` 2.1.1
- 매개 변수 처리에 대한 수정이 추가되었습니다.

## v0.11.0(2019년 6월 3일)

- 지원을 위한 새 태그 확장 `at.js` 2.1
