---
title: Adobe Experience Platform Web SDK 릴리스 노트
description: Adobe Experience Platform Web SDK에 대한 최신 릴리스 정보입니다.
keywords: Adobe Experience Platform 웹 SDK;플랫폼 웹 SDK;웹 SDK;릴리스 노트;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 10%

---


# 릴리스 노트

## 버전 2.3.0

* 더 엄격한 컨텐츠 보안 정책을 허용하는 추가 지원을 추가했습니다.
* 단일 페이지 애플리케이션에 대한 개인화 지원을 추가했습니다.
* `window.console` API를 덮어쓸 수 있는 다른 페이지 JavaScript 코드와의 호환성을 개선했습니다.
* 버그 수정:`documentUnloading`이(가) `true`로 설정되었거나 링크 클릭이 자동으로 추적되었을 때 `sendBeacon`이(가) 사용되지 않았습니다.
* 버그 수정:앵커 요소에 HTML 내용이 포함되어 있으면 링크가 자동으로 추적되지 않습니다.
* 버그 수정:읽기 전용 `message` 속성을 포함하는 특정 브라우저 오류가 적절하게 처리되지 않아 고객에게 다른 오류가 표시됩니다.
* 버그 수정:iframe 내에서 SDK를 실행하면 iframe의 HTML 페이지가 상위 창의 HTML 페이지와 다른 하위 도메인의 경우 오류가 발생합니다.

## 버전 2.2.0

* 버그 수정:`idMigrationEnabled`이(가) `true`인 경우 Opt-in 개체가 합금으로 호출을 수행할 수 없도록 차단했습니다.
* 버그 수정:합금은 개인화 제안을 반환해야 하는 요청을 인식하여 깜박이는 문제를 방지합니다.

## 버전 2.1.0

* `syncIdentity` 명령을 제거하고 `sendEvent` 명령에서 해당 ID 전달을 지원합니다.
* IAB 2.0 동의 표준을 지원합니다.
* `setConsent` 명령에서 추가 ID 전달을 지원합니다.
* `sendEvent` 명령에서 `datasetId` 재정의가 지원됩니다.
* 합금 모니터 지원([자세히 보기](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 구현 세부 정보 컨텍스트 데이터에 `environment: browser`을(를) 전달합니다.
