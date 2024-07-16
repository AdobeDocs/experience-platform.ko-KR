---
title: Assurance에서 Adobe Analytics 보기
description: 이 안내서에서는 Adobe Experience Platform Assurance와 함께 Adobe Analytics를 사용하는 방법을 설명합니다.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# Assurance에서 Adobe Analytics 보기

Adobe Analytics와 Adobe Experience Platform Assurance를 통합하면 Adobe Analytics 구현을 디버깅하고 확인하는 사용자에게 보다 자세한 SDK 이벤트 보기를 지원합니다. 이제 보기에 [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/)에서 Adobe Analytics로 전송된 작업/상태 이벤트 및 수명 주기가 표시됩니다. 이 보기에는 각 보고서 세트의 처리 규칙을 적용한 후 이벤트가 처리되는 방법에 대한 정보를 제공하는 “응답” 세부 정보도 있습니다.

![](./images/adobe-analytics/overview.png)

## 시작하기

계속하기 전에 다음 서비스가 있는지 확인하십시오.

- [Adobe Experience Platform 데이터 수집 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

애플리케이션에 Assurance를 설치하는 방법에 대한 내용은 [Assurance 구현 안내서](../tutorials/implement-assurance.md)를 참조하십시오.

## 후처리 상태

SDK가 Adobe Analytics로 네트워크 요청을 한 후 Assurance가 Adobe Analytics 요청에 대한 후처리 정보를 검색할 수 있었는지 상태를 알려 줍니다.

후처리 정보를 검색하려면 로그인한 사용자에게 해당 보고서 세트에 대한 액세스 권한이 있어야 합니다.

| 상태 | 설명 |
| :----- | :---------- |
| `Queued` | 네트워크 요청이 후처리 정보를 가져오는 중입니다. |
| `Processed` | 네트워크 요청이 성공했으며 후처리 정보가 수신되었습니다. |
| `Delayed` | 후처리 정보를 가져오기 위한 최대 요청 재시도 횟수를 초과했습니다. |
| `Error` | 오류로 인해 네트워크 요청이 실패했습니다. 오류에 대한 자세한 내용은 이벤트 상세 보기에 표시됩니다. |
| `Unauthorized` | 사용자는 Adobe Analytics 보고서 세트에 액세스할 수 없습니다. |
| `Unavailable` | Adobe Analytics 요청에는 해당 `AnalyticsResponse` 이벤트가 없습니다. |
| `No Debug Flag` | 현재 Adobe Analytics 또는 Assurance SDK 버전은 Analytics 디버깅 기능을 지원하지 않을 수 있습니다. 자세한 내용은 [문제 해결 안내서](../troubleshooting.md)를 참조하십시오. |
| `Expired` | `AnalyticsTrack` 또는 `LifecycleStart` 이벤트는 24시간이 지났습니다. |

## 이벤트 상세 보기

Analytics 추적 이벤트의 경우 상세 보기에는 다음과 같은 중요한 부분이 포함됩니다.

- 원래 SDK Analytics 요청 이벤트입니다.
- 보고서 세트 ID, SDK 확장 기능 버전, OOTB 컨텍스트 데이터 등과 같은 요청의 OOTB 메타 및 컨텍스트 데이터.
- Revar, eVar, prop 등의 매핑이 포함된 Analytics 이벤트에 대한 후처리 정보입니다.
