---
title: Adobe Experience Platform 웹 SDK 릴리스 노트
seo-title: Adobe Experience Platform 웹 SDK 릴리스 노트
description: Adobe Experience Platform 웹 SDK 릴리스 노트.
seo-description: Adobe Experience Platform 웹 SDK 릴리스 노트.
translation-type: tm+mt
source-git-commit: e9a49c20f30d06fa125185865b4963c8472fa5e5
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 3%

---


# 릴리스 노트

## 버전 2.1.0

* 명령을 `syncIdentity` 제거하고 명령에서 해당 ID 전달을 `sendEvent` 지원합니다.
* IAB 2.0 동의 표준 지원.
* 명령에서 추가 ID 전달을 `setConsent` 지원합니다.
* 명령 `datasetId` 의 덮어쓰기를 `sendEvent` 지원합니다.
* 합금 모니터 지원([자세한 내용](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* 구현 세부 정보 컨텍스트 데이터 `environment: browser` 를 전달합니다.
