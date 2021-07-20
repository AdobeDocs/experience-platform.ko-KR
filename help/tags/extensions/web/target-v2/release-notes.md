---
title: Adobe Target v2 확장에 대한 릴리스 노트
description: Adobe Experience Platform의 Adobe Target v2 태그 확장에 대한 최신 릴리스 노트입니다.
source-git-commit: ae6b69ecea54942c1bbf8a2765768bac50a8b930
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 44%

---

# Adobe Target v2 확장 릴리스 노트

>[!NOTE]
>
>Adobe Experience Platform Launch은 Experience Platform에서 데이터 수집 기술 세트로 브랜드 재지정되었습니다. 그 결과 제품 설명서에서 몇 가지 용어 변경 사항이 롤아웃되었습니다. 용어 변경 내용을 통합 참조하려면 다음 [document](../../../term-updates.md)을 참조하십시오.

## 2021년 7월 20일

### Adobe Target v2 확장 0.15.1

- `stringify` 함수 이름 충돌이 발생하여 `sessionId`, `requestId` 등에 대해 잘못된 UUID 값이 생성되던 문제를 수정했습니다.

## 2021년 7월 16일

### Adobe Target v2 확장 0.15.0

- at.js 설정 secureOnly 가 true로 설정될 때마다 쿠키에 보안 속성을 추가합니다
- 이제 `triggerView()` 을 사용할 때 응답 토큰을 사용할 수 있습니다
- `CONTENT_RENDERING_NO_OFFERS` 이벤트와 관련된 버그가 수정되었습니다. 이제 Target에서 반환된 컨텐츠가 없을 때마다 올바르게 트리거됩니다
- 미리 가져오기 요청을 사용할 때 A4T 클릭 지표 세부 사항이 올바르게 반환됩니다
- UUID 생성은 더 이상 `Math.random()`을 사용하지 않지만 `window.crypto`에 의존합니다.
- `sessionId` 쿠키 만료는 모든 네트워크 호출에서 올바르게 확장됩니다
- 이제 SPA 보기 캐시 초기화가 올바르게 처리되었으며 `viewsEnable` 설정을 적용합니다.

## 2021년 6월 2일

### Adobe Target v2 확장 0.14.2

- 최종 Launch 번들에 at.js 버전 2개가 포함되어 있는 버그를 수정합니다. 이 단계에서 On-Device Decisioning이 수행되고, 그렇지 않은 버전이 각각 있습니다.

## 2021년 5월 19일

### Adobe Target v2 확장 0.14.1

- Target 로드 작업이 글로벌 mbox 호출을 실행하는 v0.14 릴리스에서 도입된 회귀 수정

## 2021년 5월 14일

### Adobe Target v2 확장 0.14

- On-Device Decisioning 기능이 있는 at.js 2.5를 로드하는 [On-Device Decisioning](./overview.md#load-target-with-on-device-decisioning)을 사용하여 새 작업 로드 Target이 추가되었습니다
- at.js가 2.5로 업데이트되었습니다.


## 2021년 3월 25일

### Adobe Target v2 확장 0.13.7

- mbox 요청에 포함되는 `targetPageParams`에 관한 문제가 해결되었습니다. `targetPageParams` 는 요청에만 포함해야  `pageLoad` 합니다.
- 전역 개체 종속성을 직접 참조로 대체하여 태그 확장에서 문서 및 창 전역 개체 문제를 해결했습니다.
- at.js가 2.4.1로 업데이트되었습니다.

## 2021년 1월 25일

### Adobe Target v2 확장 0.13.6

- 통합 프로필/플랫폼 ID에 대한 지원을 게재 API customerId에 추가
- 잘못된 스타일 태그 삽입 수정
- at.s가 2.4.0으로 업데이트되었습니다.
- 정의되지 않은 매개 변수가 잘못된 게재 요청을 초래할 수 있는 문제가 해결되었습니다.

## 2020년 11월 25일

### Adobe Target v2 확장 0.13.4

- mbox 매개 변수가 UI에 표시되지 않던 버그를 수정했습니다.
- 브랜딩 업데이트
- at.js 버전이 2.3.3으로 업데이트되었습니다.

## 2020년 7월 24일

### Adobe Target v2 확장 0.13.3

- 비활성 활동에 대해 QA 모드 링크가 작동하지 않던 버그를 수정했습니다
- 스크립트나 코드가 `default` 속성을 `window` 또는 `document`에 추가할 때 확장에 실패하는 경우 버그를 수정했습니다

## 2020년 6월 15일

### Adobe Target v2 확장 0.13.2

- at.js 1.x에서 서버 도메인을 잘못 만들어 Target 요청이 실패하는 CNAME 및 Edge Override를 사용할 때 발생하는 문제가 해결되었습니다.
- Target 및 Adobe Analytics 태그 확장에 v2 태그 확장을 사용할 때 Target이 Analytics sendBeacon 호출을 지연하는 문제가 해결되었습니다.
- `deviceIdLifetime`을 통해 재정의 가능하도록 하여 `targetGlobalSettings` 설정을 개선했습니다.

## 2020년 3월 25일

### Adobe Target v2 확장 0.13.0

- at.js가 v2.3로 업데이트되었습니다.
- adobe.target.getOffer API에 Target Global Mbox 지원 추가됨
- 매개 변수 및 페이지 로드 매개 변수가 올바르게 처리되지 않는 문제가 해결되었습니다.

## 2019년 10월 10일

### Adobe Target v2 확장 0.12.0

- at.js가 v2.2로 업데이트되었습니다.
- ECID(Experience Cloud ID 라이브러리) v4.4와 at.js 2.2 간의 통합을 위해 성능이 향상되었습니다.
- 이전에는 at.js가 경험을 가져오기 전에 ECID 라이브러리가 두 개의 차단 호출을 생성했습니다. 이는 단일 호출로 감소하여 성능이 크게 향상되었습니다.

>[!NOTE]
>ECID 태그 확장을 v4.4.1로 업그레이드하여 향상된 성능을 이용해 보십시오.

## 2019년 7월 31일

### Adobe Target v2 확장 0.11.1

- at.js 2.1.1을 사용할 확장 버전이 업데이트되었습니다.
- 매개 변수 처리에 대한 수정이 추가되었습니다.

## 2019년 6월 3일

### Adobe Target v2 확장 0.11.0

- at.js 2.1에서 지원하는 새 태그 확장
