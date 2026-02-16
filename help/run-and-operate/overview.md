---
title: 실행 및 운영 개요
description: 실행 및 운영 도구를 사용하여 Adobe Experience Platform 구현을 검사, 문제 해결 및 최적화합니다. 예약된 일괄 처리 활성화에 대한 가시성을 확보하고 구성 문제를 식별하며 시스템 안정성을 개선합니다.
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 1%

---


# 실행 및 운영 개요

>[!AVAILABILITY]
>
>실행 및 운영 기능은 현재 제한된 릴리스로 사용할 수 있습니다.

일괄 처리 작업이 실패하거나 불완전한 데이터를 전달할 때 문제의 원인을 빨리 이해해야 합니다. 근본 원인은 데이터 가용성 문제, 잘못된 타이밍, 구성 문제 또는 시스템 용량 제한일 수 있습니다. 명확한 가시성이 없으면 답을 찾기 전에 여러 시스템을 조사하는 데 몇 시간이 걸릴 수 있습니다.

[!UICONTROL Run and Operate] 도구를 사용하여 다음을 수행할 수 있습니다.

* **데이터 작업 검사**: 모든 워크플로우에서 작업 실행 상태 및 상태를 전체적으로 볼 수 있습니다.
* **더 빠른 문제 해결**: 자세한 진단 정보 및 실행 기록에 액세스하여 근본 원인을 신속하게 식별하고 평균 해결 시간을 단축할 수 있습니다.
* **사전에 문제 방지**: 작업 패턴을 분석하고, 오류가 발생하기 전에 구성 문제를 감지하고, 데이터 작업을 최적화합니다.

## 타깃 대상자 {#target-audiences}

[!UICONTROL Run and Operate] 도구는 조직 전체에서 여러 대상자에게 서비스를 제공하도록 설계되었습니다.

* **데이터 및 IT 팀**: 신뢰할 수 있는 데이터 파이프라인을 유지하고 기술 문제를 해결하는 시스템 관리자 및 데이터 엔지니어
* **마케팅 작업**: 마케팅 플랫폼으로의 데이터 전달을 검사하고 활성화 문제를 해결하는 마케팅 기술 전문가
* **구현자**: 구현 효율성, 안정성을 확인하고 기술 문제를 해결하는 실무자.

## 전제 조건 {#prerequisites}

실행 및 운영 도구에 액세스하려면 **[!UICONTROL View Job Schedules]** 및 **[!UICONTROL View Profile Management]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다.
[!UICONTROL Job Schedules] 페이지에서는 모든 예약된 일괄 처리 작업에 대한 개요를 제공합니다.
적절한 권한이 있는지 확인하려면 시스템 관리자에게 문의하십시오.

## 시작 {#getting-started}

Experience Platform UI에서 실행 및 작업 도구에 액세스하려면 다음을 수행하십시오.

1. Experience Platform 계정에 로그인하고 왼쪽 탐색에서 **[!UICONTROL Run and Operate]**&#x200B;을(를) 선택합니다.
2. 검사 또는 문제 해결 요구 사항과 일치하는 도구를 선택합니다.

   >[!NOTE]
   >
   >현재 사용 가능한 기능은 [작업 일정](job-schedules.md)뿐입니다.

![실행 및 왼쪽 탐색 표시가 있는 Experience Platform UI.](assets/overview/run-and-operate.png)

## 사용 가능한 도구 {#available-tools}

다음 도구는 데이터 작업을 검사하고 최적화하는 데 도움이 됩니다.

### 작업 일정 {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules]은(는) 현재 다음 Real-Time CDP 작업에만 사용할 수 있습니다.
>
> * 일괄 데이터 레이크 수집
> * 일괄 프로필 수집
> * 일괄 처리 세분화
> * 일괄 처리 대상 활성화.

[작업 일정](job-schedules.md)을 사용하면 데이터 레이크 수집, 프로필 수집, 세분화 및 대상 활성화를 포함하여 조직 전체에서 샌드박스별로 예약된 일괄 처리 작업을 모두 검사할 수 있습니다. 작업 실행 상태, 성능 지표 및 실행 기록을 보고 패턴을 식별하며 안정성에 영향을 주는 구성 문제를 진단합니다.

![작업 일정 화면을 표시하는 Experience Platform UI.](assets/overview/job-schedules-interface.png)

작업 스케줄은 세 가지 수준의 조사를 제공합니다.

* **[작업 일정 검사](job-schedules.md)**: 타임라인에서 모든 데이터 세트와 예약된 작업을 보고 전체 파이프라인에 걸쳐 패턴 및 일정 충돌을 식별합니다.
* **[앤티 패턴 식별](job-schedules-anti-patterns.md)**: 일정 겹침, 고밀도 일괄 처리 스택, 성능에 영향을 주는 과도한 일괄 처리와 같은 일반적인 구성 문제를 찾아 해결하는 방법에 대해 알아봅니다.
* **[작업 세부 정보 보기](job-schedules-details.md)**: 특정 데이터 세트와 개별 작업 실행으로 드릴다운하여 오류를 조사하고, 타이밍을 확인하고, 처리된 레코드를 확인합니다.

또한 데이터 처리 단계 간의 종속성을 이해하여 Experience Platform 워크플로 전체에서 안정적인 데이터 흐름을 확보할 수 있습니다.

## 다음 단계 {#next-steps}

[!UICONTROL Run and Operate] 도구의 목적과 기능을 이해했으므로 다음 리소스를 탐색하여 지식을 심화하십시오.

* Experience Platform에 데이터가 수집되는 방식을 이해하려면 [일괄 처리 수집](../ingestion/batch-ingestion/overview.md)에 대해 알아보십시오
* 일괄 처리 수집 및 활성화를 위해 [작업 일정을 검사](job-schedules.md)하는 방법에 대해 알아봅니다
* 일괄 처리 대상에 대해 [예약된 활성화를 구성](../destinations/ui/activate-batch-profile-destinations.md)하는 방법 이해
* 대상에 대한 [데이터 흐름 모니터링](../dataflows/ui/monitor-destinations.md) 탐색

