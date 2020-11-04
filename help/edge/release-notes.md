---
title: Adobe Experience Platform 웹 SDK 릴리스 노트
seo-title: Adobe Experience Platform 웹 SDK 릴리스 노트
description: Adobe Experience Platform 웹 SDK 릴리스 노트.
seo-description: Adobe Experience Platform 웹 SDK 릴리스 노트.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 77c1e693668bc50a81713d02cfe4b0fabc661404
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 14%

---


# 릴리스 노트

## 버전 2.3.0

* 더 엄격한 컨텐츠 보안 정책을 허용하는 한 번의 지원을 추가했습니다.
* 단일 페이지 애플리케이션에 대한 개인화 지원을 추가했습니다.
* API를 덮어쓸 수 있는 다른 페이지 JavaScript 코드와의 호환성이 `window.console` 개선되었습니다.
* 버그 수정: `sendBeacon` 를 사용하지 않거나 링크 클릭 `documentUnloading` 이 자동으로 추적될 `true` 때 사용되지 않습니다.
* 버그 수정:앵커 요소에 HTML 내용이 포함되어 있으면 링크가 자동으로 추적되지 않습니다.
* 버그 수정:읽기 전용 `message` 속성을 포함하는 특정 브라우저 오류가 적절하게 처리되지 않아 다른 오류가 고객에게 노출되었습니다.
* 버그 수정:iframe 내에서 SDK를 실행하면 iframe의 HTML 페이지가 상위 창의 HTML 페이지와 다른 하위 도메인에서 오는 경우 오류가 발생합니다.

## 버전 2.2.0

* 버그 수정:옵트인 개체가 합금이 전화하는 것을 막고 `idMigrationEnabled` 있었습니다 `true`.
* 버그 수정:합금은 개인화 제안을 반환해야 하는 요청을 인지하여 깜박이는 문제를 방지합니다.

## 버전 2.1.0

* 명령을 `syncIdentity` 제거하고 명령에서 해당 ID 전달을 `sendEvent` 지원합니다.
* IAB 2.0 동의 표준 지원.
* 명령에서 추가 ID 전달을 `setConsent` 지원합니다.
* 명령 `datasetId` 의 덮어쓰기를 `sendEvent` 지원합니다.
* 합금 모니터 지원([자세한 내용](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 구현 세부 정보 컨텍스트 데이터 `environment: browser` 를 전달합니다.
