---
title: 예약된 쿼리 모니터링
description: 쿼리 서비스 UI를 통해 쿼리를 모니터링하는 방법을 알아봅니다.
exl-id: 4640afdd-b012-4768-8586-32f1b8232879
source-git-commit: 1b4554e204663d40c3a18da792614305abb7d296
workflow-type: tm+mt
source-wordcount: '1252'
ht-degree: 0%

---

# 예약된 쿼리 모니터링

Adobe Experience Platform은 UI를 통해 모든 쿼리 작업의 상태에 대한 향상된 가시성을 제공합니다. 출처: [!UICONTROL 예약된 쿼리] 탭 이제 상태, 일정 세부 정보 및 오류 메시지/코드가 실패할 경우 이를 포함하는 쿼리 실행에 대한 중요한 정보를 찾을 수 있습니다. 다음 작업을 통해 이러한 쿼리에 대한 UI를 통해 해당 상태에 따라 쿼리에 대한 경고를 구독할 수도 있습니다. [!UICONTROL 예약된 쿼리] 탭.

## [!UICONTROL 예약된 쿼리]

다음 [!UICONTROL 예약된 쿼리] 탭에서는 모든 예약된 CTAS 및 ITAS 쿼리에 대한 개요를 제공합니다. 모든 예약된 쿼리와 실패한 쿼리에 대한 오류 코드 및 메시지에 대한 실행 세부 정보를 찾을 수 있습니다.

로 이동하려면 [!UICONTROL 예약된 쿼리] 탭, 선택 **[!UICONTROL 쿼리]** 왼쪽 탐색 모음 뒤에 오는 **[!UICONTROL 예약된 쿼리]**

![쿼리 작업 영역의 예약된 쿼리 탭.](../images/ui/monitor-queries/scheduled-queries.png)

아래 표에서는 사용 가능한 각 열에 대해 설명합니다.

>[!NOTE]
>
>경고 구독 아이콘은 제목 없는 열의 각 행에 포함됩니다. 다음을 참조하십시오. [경고 구독](#alert-subscription) 섹션에 자세히 설명되어 있습니다.

| 열 | 설명 |
|---|---|
| **[!UICONTROL 이름]** | 이름 필드는 템플릿 이름 또는 SQL 쿼리의 처음 몇 문자입니다. UI를 통해 쿼리 편집기로 만든 모든 쿼리의 이름은 처음 만들 때 로 지정됩니다. API를 통해 쿼리를 만든 경우 해당 이름은 쿼리를 만드는 데 사용되는 초기 SQL 코드 조각이 됩니다. 에서 항목 선택 [!UICONTROL 이름] 쿼리와 연결된 모든 실행 목록을 표시하는 열입니다. 자세한 내용은 [쿼리 실행 일정 세부 정보](#query-runs) 섹션. |
| **[!UICONTROL 템플릿]** | 쿼리의 템플릿 이름입니다. 템플릿 이름을 선택하여 쿼리 편집기로 이동합니다. 쿼리 템플릿은 편의를 위해 쿼리 편집기에 표시됩니다. 템플릿 이름이 없는 경우 행은 하이픈으로 표시되며 쿼리를 보기 위해 쿼리 편집기로 리디렉션할 수 없습니다. |
| **[!UICONTROL SQL]** | SQL 쿼리의 코드 조각입니다. |
| **[!UICONTROL 실행 빈도]** | 쿼리가 실행되도록 설정된 케이던스입니다. 사용 가능한 값은 다음과 같습니다 `Run once` 및 `Scheduled`. 쿼리는 실행 빈도에 따라 필터링될 수 있습니다. |
| **[!UICONTROL 작성자]** | 쿼리를 만든 사용자의 이름입니다. |
| **[!UICONTROL 생성됨]** | 쿼리가 생성된 타임스탬프(UTC 형식)입니다. |
| **[!UICONTROL 마지막 실행 타임스탬프]** | 쿼리가 실행된 가장 최근 타임스탬프입니다. 이 열에서는 쿼리가 현재 예약에 따라 실행되었는지 여부를 강조 표시합니다. |
| **[!UICONTROL 마지막 실행 상태]** | 가장 최근 쿼리 실행의 상태입니다. 상태 값: `Success`, `Failed`, `In progress`, 및 `No runs`. |

>[!TIP]
>
>쿼리 편집기로 이동하면 다음을 선택할 수 있습니다 **[!UICONTROL 쿼리]** (으)로 돌아가기 [!UICONTROL 템플릿] 탭.

### 예약된 쿼리에 대한 표 설정 사용자 지정

에서 열을 조정할 수 있습니다. [!UICONTROL 예약된 쿼리] 탭하여 필요에 맞게 변경합니다. 설정 아이콘(![설정 아이콘](../images/ui/monitor-queries/settings-icon.png))을 클릭하여 엽니다. [!UICONTROL 표 맞춤화] 설정 대화 상자 및 사용 가능한 열 편집

![표 설정 사용자 지정 아이콘](../images/ui/monitor-queries/customze-table-settings-icon.png)

관련 확인란을 전환하여 테이블 열을 제거하거나 추가합니다. 그런 다음 을 선택합니다. **[!UICONTROL 적용]** 을 클릭하여 선택 항목을 확인합니다.

>[!NOTE]
>
>UI를 통해 생성된 모든 쿼리는 작성 프로세스의 일부로 이름이 지정된 템플릿이 됩니다. 템플릿 이름은 템플릿 열에 표시됩니다. API를 통해 쿼리를 만든 경우 템플릿 열이 비어 있습니다.

![표 설정 사용자 지정 대화 상자](../images/ui/monitor-queries/customize-table-dialog.png)

### 경고 구독 {#alert-subscription}

다음에서 경고를 구독할 수 있습니다. [!UICONTROL 예약된 쿼리] 탭. 경고 알림 아이콘(![경고 아이콘.](../images/ui/monitor-queries/alerts-icon.png))을 클릭하여 엽니다. [!UICONTROL 경고] 대화 상자. 다음 [!UICONTROL 경고] 대화 상자가 UI 알림 및 이메일 경고를 모두 구독합니다. 경고는 쿼리 상태를 기반으로 합니다. 다음 세 가지 옵션을 사용할 수 있습니다. `start`, `success`, 및 `failure`. 해당 상자를 선택하고 **[!UICONTROL 저장]** 구독하기.

![경고 구독 대화 상자.](../images/ui/monitor-queries/alert-subscription-dialog.png)

다음을 참조하십시오. [경고 구독 API 설명서](../api/alert-subscriptions.md) 추가 정보.

### 쿼리 필터링 {#filter}

실행 빈도에 따라 쿼리를 필터링할 수 있습니다. 다음에서 [!UICONTROL 예약된 쿼리] 탭에서 필터 아이콘(![필터 아이콘](../images/ui/monitor-queries/filter-icon.png))을 클릭하여 필터 사이드바를 엽니다.

![필터 아이콘이 강조 표시된 예약된 쿼리 탭.](../images/ui/monitor-queries/filter-queries.png)

다음 중 하나를 선택합니다. **[!UICONTROL 예약됨]** 또는 **[!UICONTROL 한 번 실행]** 빈도 필터 확인란을 실행하여 쿼리 목록을 필터링합니다.

>[!NOTE]
>
>실행되었지만 예약되지 않은 모든 쿼리는 [!UICONTROL 한 번 실행].

![필터 사이드바가 강조 표시된 예약된 쿼리 탭입니다.](../images/ui/monitor-queries/filter-sidebar.png)

필터 기준을 활성화했으면 다음을 선택합니다. **[!UICONTROL 필터 숨기기]** 필터 패널을 닫습니다.

## 쿼리 실행 일정 세부 정보 {#query-runs}

일정 세부 정보 페이지로 이동하려면 쿼리 이름을 선택합니다. 이 보기는 예약된 쿼리의 일부로 실행된 모든 실행의 목록을 제공합니다. 제공되는 정보에는 시작 및 종료 시간, 상태 및 사용된 데이터 세트가 포함됩니다.

![일정 세부 정보 페이지](../images/ui/monitor-queries/schedule-details.png)

이 정보는 5열 표로 제공됩니다. 각 행은 쿼리 실행을 나타냅니다.

| 열 이름 | 설명 |
|---|---|
| **[!UICONTROL 쿼리 실행 ID]** | 일별 실행에 대한 쿼리 실행 ID입니다. 다음 항목 선택 **[!UICONTROL 쿼리 실행 ID]** 을 클릭하여 다음 위치로 이동합니다. [!UICONTROL 쿼리 실행 개요]. |
| **[!UICONTROL 쿼리 실행 시작]** | 쿼리가 실행된 타임스탬프. UTC 형식입니다. |
| **[!UICONTROL 쿼리 실행 완료]** | 쿼리가 완료된 타임스탬프. UTC 형식입니다. |
| **[!UICONTROL 상태]** | 가장 최근 쿼리 실행의 상태입니다. 세 가지 상태 값은 다음과 같습니다. `successful` `failed` 또는 `in progress`. |
| **[!UICONTROL 데이터 세트]** | 실행과 관련된 데이터 세트입니다. |

예약되는 쿼리에 대한 세부 정보는 다음에서 볼 수 있습니다. [!UICONTROL 속성] 패널. 이 패널에는 초기 쿼리 ID, 클라이언트 유형, 템플릿 이름, 쿼리 SQL 및 일정의 케이던스가 포함됩니다.

![속성 패널이 강조 표시된 예약 세부 정보 페이지입니다.](../images/ui/monitor-queries/properties-panel.png)

쿼리 실행 ID를 선택하여 실행 세부 정보 페이지로 이동하고 쿼리 정보를 확인합니다.

![실행 ID가 강조 표시된 예약 세부 정보 화면입니다.](../images/ui/monitor-queries/navigate-to-run-details.png)

## 쿼리 실행 개요 {#query-run-overview}

다음 [!UICONTROL 쿼리 실행 개요] 은(는) 이 예약된 쿼리의 개별 실행에 대한 정보와 실행 상태에 대한 보다 자세한 분류를 제공합니다. 이 페이지에는 또한 클라이언트 정보와 쿼리 실패의 원인이 될 수 있는 모든 오류에 대한 세부 정보가 포함되어 있습니다.

![개요 섹션이 강조 표시된 실행 세부 정보 화면입니다.](../images/ui/monitor-queries/query-run-details.png)

쿼리 상태 섹션은 쿼리가 실패한 경우 오류 코드와 오류 메시지를 제공합니다.

![오류 섹션이 강조 표시된 실행 세부 정보 화면입니다.](../images/ui/monitor-queries/failed-query.png)

이 보기에서 쿼리 SQL을 클립보드에 복사할 수 있습니다. 쿼리를 복사하려면 SQL 코드 조각의 오른쪽 상단에 있는 복사 아이콘을 선택합니다. 코드가 복사되었음을 확인하는 팝업 메시지가 표시됩니다.

![SQL 복사 아이콘이 강조 표시된 실행 세부 정보 화면입니다.](../images/ui/monitor-queries/copy-sql.png)

### 익명 블록이 있는 쿼리에 대한 세부 정보 실행 {#anonymous-block-queries}

익명 블록을 사용하여 SQL 문을 구성하는 쿼리는 개별 하위 쿼리로 구분됩니다. 이렇게 하면 각 쿼리 블록에 대한 실행 세부 정보를 개별적으로 검사할 수 있습니다.

>[!NOTE]
>
>DROP 명령을 사용하는 익명 블록의 실행 세부 정보는 **아님** 별도의 하위 쿼리로 보고됩니다. 익명 블록 하위 쿼리로 사용되는 CTAS 쿼리, ITAS 쿼리 및 COPY 문에 대해 별도의 실행 세부 정보를 사용할 수 있습니다. DROP 명령에 대한 실행 세부 정보는 현재 지원되지 않습니다.

익명 블록은 `$$` 접두사를 쿼리 앞에 추가합니다. 다음을 참조하십시오. [익명 블록 문서](../essential-concepts/anonymous-block.md) query service에서 익명 블록에 대해 자세히 알아봅니다.

익명 블록 하위 쿼리는 실행 상태 왼쪽에 탭이 있습니다. 실행 세부 정보를 표시하려면 탭을 선택합니다.

![익명 블록 쿼리를 표시하는 쿼리 실행 개요입니다. 여러 쿼리 탭이 강조 표시됩니다.](../images/ui/monitor-queries/anonymous-block-overview.png)

익명 블록 쿼리가 실패할 경우 이 UI를 통해 해당 특정 블록에 대한 오류 코드를 찾을 수 있습니다.

![단일 블록에 대한 오류 코드가 강조 표시된 익명 블록 쿼리를 표시하는 쿼리 실행 개요입니다.](../images/ui/monitor-queries/anonymous-block-failed-query.png)

선택 **[!UICONTROL 쿼리]** 일정 세부 정보 화면으로 돌아가려면 **[!UICONTROL 예약된 쿼리]** (으)로 돌아가기 [!UICONTROL 예약된 쿼리] 탭.

![Query 가 강조 표시된 실행 세부 정보 화면입니다.](../images/ui/monitor-queries/return-navigation.png)
