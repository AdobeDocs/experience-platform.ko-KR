---
title: Adobe Experience Platform 웹 SDK 릴리스 노트
seo-title: Adobe Experience Platform 웹 SDK 릴리스 노트
description: Adobe Experience Platform 웹 SDK 릴리스 노트.
seo-description: Adobe Experience Platform 웹 SDK 릴리스 노트.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
translation-type: tm+mt
source-git-commit: 738dfe782ee7d6bef06d14910e0c26540b0ec734
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# 릴리스 노트

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
