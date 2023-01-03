---
keywords: Experience Platform;홈;인기 항목;계정 모니터링;데이터 흐름 모니터링;데이터 흐름;소스
description: 이 자습서에서는 집계 모니터링 보기와 서비스 간 모니터링을 모두 사용하여 데이터 흐름을 모니터링하는 단계를 제공합니다.
solution: Experience Platform
title: UI에서 소스에 대한 데이터 흐름 모니터링
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---

# UI에서 소스에 대한 데이터 흐름 모니터링

>[!IMPORTANT]
>
>스트리밍 소스(예: [HTTP API 소스](../../sources/connectors/streaming/http.md) 모니터링 대시보드에서 지원하지 않습니다. 현재는 대시보드만 사용하여 배치 소스를 모니터링할 수 있습니다.

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되어 Experience Platform 내에서 분석되고 다양한 대상으로 활성화됩니다. 플랫폼 을 사용하면 데이터 흐름에 투명성을 제공하여 비선형 이외의 데이터 흐름을 쉽게 추적할 수 있습니다.

모니터링 대시보드는 데이터 흐름 여정을 시각적으로 나타냅니다. 집계된 모니터링 보기를 사용하고 소스 수준, 데이터 흐름 및 데이터 흐름 실행으로 세로로 이동하여 데이터 흐름의 성공 또는 실패에 기여하는 해당 지표를 볼 수 있습니다. 모니터링 대시보드의 서비스 간 모니터링 용량을 사용하여 소스에서 데이터 흐름 여정을 모니터링할 수도 있습니다 [!DNL Identity Service], 및에 [!DNL Profile].

이 자습서에서는 집계 모니터링 보기와 서비스 간 모니터링을 모두 사용하여 데이터 흐름을 모니터링하는 단계를 제공합니다.

## 시작하기 {#getting-started}

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [데이터 흐름](../home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 서로 다른 서비스 간에 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 [!DNL Identity] 및 [!DNL Profile], 및에 [!DNL Destinations].
   * [데이터 흐름 실행](../../sources/notifications.md): 데이터 흐름 실행은 선택한 데이터 흐름의 빈도 구성에 따라 반복되는 예약된 작업입니다.
* [소스](../../sources/home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [ID 서비스](../../identity-service/home.md): 여러 장치와 시스템에서 ID를 브리징하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
* [실시간 고객 프로필](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 집계 모니터링 보기 {#aggregated-monitoring-view}

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="소스 수집"
>abstract="소스 수집 보기에는 수집된 레코드 및 실패한 레코드를 포함하여, 데이터 레이크 서비스의 데이터 활동 상태 및 지표에 대한 정보가 포함되어 있습니다. 지표 및 그래프에 대한 자세한 내용을 보려면 지표 정의 안내서를 검토하십시오."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="데이터 흐름 실행 세부 정보"
>abstract="소스 처리에는 수집된 레코드 및 실패한 레코드를 포함하여, 데이터 레이크 서비스의 데이터 활동 상태 및 지표에 대한 정보가 포함되어 있습니다. 지표 및 그래프에 대한 자세한 내용을 보려면 지표 정의 안내서를 검토하십시오."
>text="Learn more in documentation"

에서 [플랫폼 UI](https://platform.adobe.com), 선택 **[!UICONTROL 모니터링]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 모니터링] 대시보드 . 다음 [!UICONTROL 모니터링] 대시보드에는 소스에서 로의 데이터 트래픽 상태에 대한 통찰력을 포함하여 모든 소스 데이터 흐름에 대한 지표와 정보가 포함되어 있습니다 [!DNL Identity Service], 및에 [!DNL Profile].

대시보드 중앙에는 다음이 있습니다 [!UICONTROL 소스 수집] 수집된 레코드 및 실패한 레코드에 대한 데이터를 표시하는 지표와 그래프가 포함된 패널입니다.

![모니터링 대시보드](../assets/ui/monitor-sources/monitoring-dashboard.png)

기본적으로 표시되는 데이터에는 지난 24시간의 수집 비율이 포함됩니다. 선택 **[!UICONTROL 최근 24시간]** 를 눌러 표시되는 레코드의 시간대를 조정합니다.

![변경 날짜](../assets/ui/monitor-sources/change-date.png)

대체 수집 시간 프레임에 대한 옵션을 제공하는 달력 팝업 창이 나타납니다. 선택 **[!UICONTROL 최근 30일]** 그런 다음 **[!UICONTROL 적용]**

![조정 시간 프레임](../assets/ui/monitor-sources/adjust-timeframe.png)

그래프는 기본적으로 활성화되어 있으며 아래 소스 목록을 확장하도록 비활성화할 수 있습니다. 을(를) 선택합니다 **[!UICONTROL 지표 및 그래프]** 그래프를 비활성화하려면 을(를) 전환합니다.

![지표 및 그래프](../assets/ui/monitor-sources/metrics-graphs.png)

| 소스 수집 | 설명 |
| ---------------- | ----------- |
| [!UICONTROL 수집된 레코드 ] | 수집된 총 레코드 수입니다. |
| [!UICONTROL 레코드 실패] | 데이터 오류로 인해 수집되지 않은 총 레코드 수입니다. |
| [!UICONTROL 실패한 총 데이터 흐름 수] | 다음을 사용하는 총 데이터 흐름 수 `failed` 상태. |

소스 수집 목록에는 하나 이상의 기존 계정이 포함된 모든 출처가 표시됩니다. 이 목록에는 적용한 기간을 기준으로 각 소스의 수집 비율, 실패한 레코드 수 및 실패한 데이터 흐름의 총 수에 대한 정보도 포함되어 있습니다.

![소스 수집](../assets/ui/monitor-sources/source-ingestion.png)

소스 목록을 정렬하려면 **[!UICONTROL 내 소스]** 그런 다음 드롭다운 메뉴에서 선택한 카테고리를 선택합니다. 예를 들어, 클라우드 스토리지에 집중하려면 을 선택합니다  **[!UICONTROL 클라우드 스토리지]**

![정렬 기준 범주](../assets/ui/monitor-sources/sort-by-category.png)

모든 소스에서 기존 데이터 흐름을 모두 보려면 **[!UICONTROL 데이터 흐름]**.

![모든 데이터 흐름 보기](../assets/ui/monitor-sources/view-all-dataflows.png)

또는 검색 막대에 소스를 입력하여 단일 소스를 분리할 수 있습니다. 소스를 확인했으면 필터 아이콘을 선택합니다 ![필터](../assets/ui/monitor-sources/filter.png) 옆에 활성 데이터 흐름 목록을 보려면 해당 데이터 흐름 목록을 확인하십시오.

![검색](../assets/ui/monitor-sources/search.png)

데이터 흐름 목록이 나타납니다. 목록 범위를 좁히고 오류가 있는 데이터 흐름에 집중하려면 다음을 선택합니다 **[!UICONTROL 실패만 표시]**.

![표시 실패 전용](../assets/ui/monitor-sources/show-failures-only.png)

모니터링할 데이터 흐름을 찾은 다음 필터 아이콘을 선택합니다 ![필터](../assets/ui/monitor-sources/filter.png) 옆에 있는 를 참조하십시오.

![데이터 흐름](../assets/ui/monitor-sources/dataflow.png)

데이터 흐름 실행 페이지에는 데이터 흐름의 실행 시작 날짜, 데이터 크기, 상태 및 처리 시간 정보가 표시됩니다. 필터 아이콘을 선택합니다 ![필터](../assets/ui/monitor-sources/filter.png) 데이터 흐름 실행 시작 시간 옆의 데이터 흐름 실행 세부 사항을 확인합니다.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

다음 [!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에 데이터 흐름의 메타데이터, 부분 수집 상태 및 오류 요약에 대한 정보가 표시됩니다. 오류 요약에는 수집 프로세스에서 오류가 발생한 단계를 보여주는 특정 최상위 수준의 오류가 포함되어 있습니다.

발생한 오류에 대한 자세한 내용을 보려면 아래로 스크롤하십시오.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

다음 [!UICONTROL 데이터 흐름 실행 오류] 패널에 데이터 흐름의 수집 실패를 초래한 특정 오류 및 오류 코드가 표시됩니다. 이 시나리오에서는 매퍼 변환 오류가 발생하여 24개의 레코드가 실패합니다.

선택 **[!UICONTROL 파일]** 추가 정보.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

다음 [!UICONTROL 파일] 패널에는 파일 이름과 경로에 대한 정보가 포함되어 있습니다.

오류를 더 세분화하려면 **[!UICONTROL 미리 보기 오류 진단]**.

![파일](../assets/ui/monitor-sources/files.png)

다음 [!UICONTROL 오류 진단 미리 보기] 데이터 집합에 최대 100개의 오류 미리 보기가 표시되는 창이 나타납니다. 선택할 수 있습니다 **[!UICONTROL 다운로드]** curl 명령을 검색하려면 오류 진단을 다운로드할 수 있습니다.

완료되면 을 선택합니다 **[!UICONTROL 닫기]**

![오류 진단](../assets/ui/monitor-sources/error-diagnostics.png)

상단 헤더에 있는 탐색 표시 시스템을 사용하여 이동 경로를 [!UICONTROL 모니터링] 대시보드 . 선택 **[!UICONTROL 실행 시작: 2/14/2021, 오후 9:47]** 이전 페이지로 돌아가려면 을 선택하고 을 선택합니다 **[!UICONTROL 데이터 흐름: 충성도 데이터 수집 데모 - 실패]** 를 눌러 데이터 흐름 페이지로 돌아갑니다.

![탐색 표시](../assets/ui/monitor-sources/breadcrumbs.png)

## 다음 단계 {#next-steps}

이 자습서를 따라 다음을 사용하여 소스 수준에서 수집 데이터 플로우를 모니터링했습니다 **[!UICONTROL 모니터링]** 대시보드 . 또한 수집 프로세스 중에 데이터 흐름의 실패에 기여한 오류를 성공적으로 식별했습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [데이터 흐름에서 ID 모니터링](./monitor-identities.md)
* [데이터 흐름에서 프로필 모니터링](./monitor-profiles.md)
