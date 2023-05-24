---
title: Assurance의 Adobe Analytics 보기
description: 이 안내서에서는 Adobe Experience Platform Assurance와 함께 Adobe Analytics을 사용하는 방법을 설명합니다.
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# Assurance의 Adobe Analytics 보기

Adobe Analytics과 Adobe Experience Platform Assurance 통합을 사용하면 사용자가 Adobe Analytics 구현을 디버깅하고 확인할 수 있도록 SDK 이벤트를 더 다양하게 볼 수 있습니다. 이제 보기에는 Adobe Analytics으로 전송된 라이프사이클 및 작업/상태 이벤트가 표시됩니다. [ADOBE EXPERIENCE PLATFORM SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). 또한 이 보기에는 각 보고서 세트의 처리 규칙을 적용한 후 이벤트가 처리된 방법에 대한 정보를 제공하는 &quot;응답&quot; 세부 정보가 있습니다.

![](./images/adobe-analytics/overview.png)

## 시작하기

계속하기 전에 다음 서비스가 있는지 확인하십시오.

- 다음 [Adobe Experience Platform 데이터 수집 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

애플리케이션에 Assurance를 설치하는 방법을 알아보려면 [assurance 구현 안내서](../tutorials/implement-assurance.md).

## 후 처리 상태

SDK가 Adobe Analytics을 사용하여 네트워크 요청을 수행하면 Assurance가 Adobe Analytics 요청에 대한 사후 처리 정보를 검색할 수 있는지 상태가 알려줍니다.

사후 처리 정보를 검색하려면 로그인한 사용자가 해당 보고서 세트에 액세스할 수 있어야 합니다.

| 상태 | 설명 |
| :----- | :---------- |
| `Queued` | 네트워크 요청이 후 처리 정보를 가져오는 중입니다. |
| `Processed` | 네트워크 요청이 성공하고 사후 처리 정보가 수신됩니다. |
| `Delayed` | 후처리 정보를 가져오기 위한 최대 요청 재시도 횟수를 초과했습니다. |
| `Error` | 오류로 인해 네트워크 요청이 실패했습니다. 오류에 대한 자세한 내용은 이벤트 세부 사항 보기에 표시됩니다. |
| `Unauthorized` | 사용자는 Adobe Analytics 보고서 세트에 액세스할 수 없습니다. |
| `Unavailable` | Adobe Analytics 요청에는 해당하는 이(가) 없습니다. `AnalyticsResponse` 이벤트. |
| `No Debug Flag` | 현재 Adobe Analytics 또는 Assurance SDK 버전은 Analytics 디버깅 기능을 지원하지 않을 수 있습니다. 자세한 내용은 다음을 참조하십시오. [문제 해결 안내서](../troubleshooting.md). |
| `Expired` | 다음 `AnalyticsTrack` 또는 `LifecycleStart` 이벤트가 24시간 이전입니다. |

## 이벤트 세부 사항 보기

Analytics 추적 이벤트의 경우 상세 보기에는 다음과 같은 중요한 부분이 포함되어 있습니다.

- 원래 SDK Analytics 요청 이벤트입니다.
- 보고서 세트 ID, SDK 확장 버전, OOTB 컨텍스트 데이터 등과 같은 요청의 OOTB 메타 및 컨텍스트 데이터.
- revar, evar, prop 등의 매핑이 포함된 Analytics 이벤트에 대한 후 처리 정보입니다.
