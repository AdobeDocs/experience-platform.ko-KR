---
keywords: Experience Platform;홈;인기 항목;계정 모니터링;데이터 흐름 모니터링;데이터 흐름;소스
description: 이 자습서에서는 집계 모니터링 보기와 서비스 간 모니터링을 모두 사용하여 데이터 흐름을 모니터링하는 단계를 제공합니다.
solution: Experience Platform
title: UI에서 소스에 대한 데이터 흐름 모니터링
topic-legacy: overview
type: Tutorial
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: a5b52d7cc2a39ce15b5a9568df14c86624ae069a
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 1%

---

# UI에서 소스에 대한 데이터 흐름 모니터링

>[!IMPORTANT]
>
>[HTTP API 소스](../../sources/connectors/streaming/http.md)와 같은 스트리밍 소스는 현재 모니터링 대시보드에서 지원하지 않습니다. 현재는 대시보드만 사용하여 배치 소스를 모니터링할 수 있습니다.

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되어 Experience Platform 내에서 분석되고 다양한 대상으로 활성화됩니다. 플랫폼 을 사용하면 데이터 흐름에 투명성을 제공하여 비선형 이외의 데이터 흐름을 쉽게 추적할 수 있습니다.

모니터링 대시보드는 데이터 흐름 여정을 시각적으로 나타냅니다. 집계된 모니터링 보기를 사용하고 소스 수준, 데이터 흐름 및 데이터 흐름 실행으로 세로로 이동하여 데이터 흐름의 성공 또는 실패에 기여하는 해당 지표를 볼 수 있습니다. 모니터링 대시보드의 서비스 간 모니터링 용량을 사용하여 데이터 흐름의 여정을 소스에서 [!DNL Identity Service], [!DNL Profile]로 모니터링할 수도 있습니다.

이 자습서에서는 집계 모니터링 보기와 서비스 간 모니터링을 모두 사용하여 데이터 흐름을 모니터링하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [데이터 흐름](../home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 서로 다른 서비스에 구성되어 있어 소스 커넥터에서 대상 데이터 세트로 데이터를 [!DNL Identity] 및 [!DNL Profile] 로 이동하고 [!DNL Destinations] 로 이동하는 데 도움이 됩니다.
   * [데이터 흐름 실행](../../sources/notifications.md): 데이터 흐름 실행은 선택한 데이터 흐름의 빈도 구성에 따라 반복되는 예약된 작업입니다.
* [소스](../../sources/home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [ID 서비스](../../identity-service/home.md): 여러 장치와 시스템에서 ID를 브리징하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
* [실시간 고객 프로필](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 집계 모니터링 보기

[플랫폼 UI](https://platform.adobe.com)의 왼쪽 탐색에서 **[!UICONTROL 모니터링]**&#x200B;을 선택하여 [!UICONTROL 모니터링] 대시보드에 액세스합니다. [!UICONTROL 모니터링] 대시보드에는 소스에서 [!DNL Identity Service](으)로의 데이터 트래픽 상태 및 [!DNL Profile]에 대한 통찰력을 포함하여 모든 소스 데이터 흐름에 대한 지표와 정보가 포함되어 있습니다.

대시보드 중앙에는 수집된 레코드 및 실패한 레코드에 대한 데이터를 표시하는 지표와 그래프가 포함된 [!UICONTROL 소스 수집] 패널이 있습니다.

![모니터링 대시보드](../assets/ui/monitor-sources/monitoring-dashboard.png)

기본적으로 표시되는 데이터에는 지난 24시간의 수집 비율이 포함됩니다. **[!UICONTROL 최근 24시간]**&#x200B;을 선택하여 표시된 레코드의 시간대를 조정합니다.

![변경 날짜](../assets/ui/monitor-sources/change-date.png)

대체 수집 시간 프레임에 대한 옵션을 제공하는 달력 팝업 창이 나타납니다. **[!UICONTROL 최근 30일]**&#x200B;을 선택한 다음 **[!UICONTROL 적용]**&#x200B;을 선택합니다

![조정 시간 프레임](../assets/ui/monitor-sources/adjust-timeframe.png)

그래프는 기본적으로 활성화되어 있으며 아래 소스 목록을 확장하도록 비활성화할 수 있습니다. **[!UICONTROL 지표 및 그래프]** 전환을 선택하여 그래프를 비활성화합니다.

![지표 및 그래프](../assets/ui/monitor-sources/metrics-graphs.png)

| 소스 수집 | 설명 |
| ---------------- | ----------- |
| [!UICONTROL 수집된 레코드  ] | 수집된 총 레코드 수입니다. |
| [!UICONTROL 레코드 실패] | 데이터 오류로 인해 수집되지 않은 총 레코드 수입니다. |
| [!UICONTROL 실패한 총 데이터 흐름 수] | `failed` 상태가 있는 총 데이터 흐름 수입니다. |

소스 수집 목록에는 하나 이상의 기존 계정이 포함된 모든 출처가 표시됩니다. 이 목록에는 적용한 기간을 기준으로 각 소스의 수집 비율, 실패한 레코드 수 및 실패한 데이터 흐름의 총 수에 대한 정보도 포함되어 있습니다.

![소스 수집](../assets/ui/monitor-sources/source-ingestion.png)

소스 목록을 정렬하려면 **[!UICONTROL 내 소스]**&#x200B;를 선택한 다음 드롭다운 메뉴에서 선택한 카테고리를 선택합니다. 예를 들어, 클라우드 스토리지에 집중하려면 **[!UICONTROL 클라우드 스토리지]**&#x200B;를 선택합니다

![정렬 기준 범주](../assets/ui/monitor-sources/sort-by-category.png)

모든 소스에서 기존 데이터 흐름을 모두 보려면 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택합니다.

![모든 데이터 흐름 보기](../assets/ui/monitor-sources/view-all-dataflows.png)

또는 검색 막대에 소스를 입력하여 단일 소스를 분리할 수 있습니다. 소스를 식별했으면 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택하여 활성 데이터 흐름 목록을 확인합니다.

![검색](../assets/ui/monitor-sources/search.png)

데이터 흐름 목록이 나타납니다. 목록 범위를 좁히고 오류가 있는 데이터 흐름에 초점을 맞추려면 **[!UICONTROL 실패만 표시]**&#x200B;를 선택합니다.

![표시 실패 전용](../assets/ui/monitor-sources/show-failures-only.png)

모니터링할 데이터 흐름을 찾은 다음 그 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)를 선택하여 실행 상태에 대한 자세한 정보를 확인합니다.

![데이터 흐름](../assets/ui/monitor-sources/dataflow.png)

데이터 흐름 실행 페이지에는 데이터 흐름의 실행 시작 날짜, 데이터 크기, 상태 및 처리 시간 정보가 표시됩니다. 데이터 흐름 실행 시작 시간 옆의 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택하여 해당 데이터 흐름 실행 세부 정보를 확인합니다.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

[!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에는 데이터 흐름의 메타데이터, 부분 수집 상태 및 오류 요약에 대한 정보가 표시됩니다. 오류 요약에는 수집 프로세스에서 오류가 발생한 단계를 보여주는 특정 최상위 수준의 오류가 포함되어 있습니다.

발생한 오류에 대한 자세한 내용을 보려면 아래로 스크롤하십시오.

![dataflow-run-details](../assets/ui/monitor-sources/dataflow-run-details.png)

[!UICONTROL 데이터 흐름 실행 오류] 패널에는 데이터 흐름의 수집 오류가 발생한 특정 오류 및 오류 코드가 표시됩니다. 이 시나리오에서는 매퍼 변환 오류가 발생하여 24개의 레코드가 실패합니다.

자세한 내용을 보려면 **[!UICONTROL 파일]**&#x200B;을 선택하십시오.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

[!UICONTROL 파일] 패널에는 파일의 이름과 경로에 대한 정보가 포함되어 있습니다.

오류를 더 세분화하려면 **[!UICONTROL 미리 보기 오류 진단]**&#x200B;을 선택합니다.

![파일](../assets/ui/monitor-sources/files.png)

[!UICONTROL 오류 진단 미리 보기] 창이 나타나고 데이터 플로우에 최대 100개의 오류 미리 보기가 표시됩니다. **[!UICONTROL 다운로드]**&#x200B;를 선택하여 curl 명령을 검색할 수 있습니다. 그러면 오류 진단을 다운로드할 수 있습니다.

완료되면 **[!UICONTROL 닫기]**&#x200B;를 선택합니다

![오류 진단](../assets/ui/monitor-sources/error-diagnostics.png)

상단 헤더의 탐색 표시 시스템을 사용하여 [!UICONTROL 모니터링] 대시보드로 다시 이동할 수 있습니다. **[!UICONTROL 실행 시작 선택: 2/14/2021, 9:47 PM]** 을 선택하여 이전 페이지로 이동한 다음 **[!UICONTROL 데이터 흐름: 데이터 흐름 페이지로 돌아가려면 충성도 데이터 수집 데모 -]**&#x200B;에 실패했습니다.

![탐색 표시](../assets/ui/monitor-sources/breadcrumbs.png)

## 교차 서비스 모니터링

대시보드의 위쪽 부분에는 소스 수준, [!DNL Identity Service] 및 [!DNL Profile]에 대한 수집 플로우의 표현이 포함되어 있습니다. 각 셀에는 해당 수집 단계에서 발생한 오류의 존재를 나타내는 점 마커가 포함되어 있습니다. 녹색 점은 오류 없는 수집을 의미하고 빨간색 점은 해당 수집 단계에서 오류가 발생했음을 의미합니다.

![크로스 서비스 모니터링](../assets/ui/monitor-sources/cross-service-monitoring.png)

데이터 흐름 페이지에서 성공적인 데이터 흐름을 찾은 다음 필터 아이콘 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택하여 해당 데이터 흐름 실행 정보를 확인합니다.

![데이터 흐름 성공](../assets/ui/monitor-sources/dataflow-success.png)

[!UICONTROL 소스 수집] 페이지에는 데이터 흐름을 성공적으로 수집하는지 확인하는 정보가 포함되어 있습니다. 여기에서 데이터 흐름의 여정 모니터링을 소스 수준에서 [!DNL Identity Service](으)로 시작한 다음 [!DNL Profile](으)로 시작할 수 있습니다.

**[!UICONTROL ID]**&#x200B;를 선택하여 [!UICONTROL ID] 단계에서 섭취를 확인합니다.

![소스](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] 메트릭

[!UICONTROL ID 처리] 페이지에는 추가된 ID 수, 생성된 그래프 및 업데이트된 그래프를 포함하여 [!DNL Identity Service]에 수집된 레코드에 대한 정보가 포함되어 있습니다.

데이터 흐름 시작 시간 옆의 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택하여 [!DNL Identity] 데이터 흐름 실행에 대한 자세한 정보를 확인합니다.

![id](../assets/ui/monitor-sources/identities.png)

| ID 지표 | 설명 |
| ---------------- | ----------- |
| [!UICONTROL 받은 레코드] | [!DNL Data Lake]에서 받은 레코드 수입니다. |
| [!UICONTROL 레코드 실패] | 데이터 오류로 인해 Platform에 수집되지 않은 레코드 수입니다. |
| [!UICONTROL 생략된 레코드] | 레코드 행에 식별자가 하나만 있으므로 수집된 레코드 수이지만 [!DNL Identity Service]에 넣을 수 없습니다. |
| [!UICONTROL 수집된 레코드] | [!DNL Identity Service]에 수집된 레코드 수입니다. |
| [!UICONTROL 총 레코드] | 실패한 레코드, 건너뛴 레코드, [!DNL Identities] 추가된 레코드 및 복제된 레코드를 포함한 모든 레코드의 총 수입니다. |
| [!UICONTROL 추가된 ID] | [!DNL Identity Service]에 추가된 순 새 식별자 수입니다. |
| [!UICONTROL 생성된 그래프] | [!DNL Identity Service]에서 생성된 새 ID 그래프의 개수입니다. |
| [!UICONTROL 그래프 업데이트] | 새 가장자리로 업데이트된 기존 ID 그래프 수입니다. |
| [!UICONTROL 실패한 데이터 흐름 실행] | 실패한 데이터 흐름 실행 수입니다. |
| [!UICONTROL 처리 시간] | 수집 시작에서 완료까지의 타임스탬프. |
| [!UICONTROL 상태] | 데이터 흐름의 전체 상태를 정의합니다. 가능한 상태 값은 다음과 같습니다. <ul><li>`Success`: 데이터 흐름이 활성 상태이고 제공된 일정에 따라 데이터를 수집 중임을 나타냅니다.</li><li>`Failed`: 오류로 인해 데이터 흐름의 활성화 프로세스가 중단되었음을 나타냅니다. </li><li>`Processing`: 데이터 흐름이 아직 활성 상태가 아님을 나타냅니다. 이 상태는 종종 새 데이터 흐름을 만든 후 즉시 발생합니다.</li></ul> |

[!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에는 IMS 조직 ID 및 데이터 흐름 실행 ID를 포함하여 [!DNL Identity] 데이터 흐름 실행에 대한 자세한 정보가 표시됩니다. 이 페이지에는 또한 수집 프로세스에서 오류가 발생할 경우 [!DNL Identity Service]에서 제공하는 해당 오류 코드와 오류 메시지도 표시됩니다.

**[!UICONTROL 실행 시작 선택: 2/14/2021, 9:47 PM]** 을 사용하여 이전 페이지로 돌아갑니다.

![identities-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

[!UICONTROL ID 처리] 페이지에서 **[!UICONTROL 프로필]**&#x200B;을 선택하여 [!UICONTROL 프로필] 단계에서 레코드 수집 상태를 확인합니다.

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] 메트릭

[!UICONTROL 프로필 처리] 페이지에는 생성된 프로필 조각 수, 업데이트된 프로필 조각 및 총 프로필 조각 수를 포함하여 [!DNL Profile]에 수집된 레코드에 대한 정보가 포함되어 있습니다.

데이터 흐름 시작 시간 옆의 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택하여 [!DNL Profile] 데이터 흐름 실행에 대한 자세한 정보를 확인합니다.

![프로필](../assets/ui/monitor-sources/profiles.png)

| 프로필 지표 | 설명 |
| --------------- | ----------- |
| [!UICONTROL 받은 레코드] | [!DNL Data Lake]에서 받은 레코드 수입니다. |
| [!UICONTROL 레코드 실패  ] | 오류로 인해 [!DNL Profile]에 수집되지 않은 수집된 레코드 수입니다. |
| [!UICONTROL 추가된 프로필 조각] | 추가된 순 새 [!DNL Profile] 조각 수입니다. |
| [!UICONTROL 프로필 조각 업데이트됨] | 업데이트된 기존 [!DNL Profile] 조각 수 |
| [!UICONTROL 총 프로필 조각] | 업데이트된 모든 기존 [!DNL Profile] 조각과 작성된 새 [!DNL Profile] 조각을 포함하여 [!DNL Profile]에 작성된 총 레코드 수입니다. |
| [!UICONTROL 실패한 데이터 흐름 실행] | 실패한 데이터 흐름 실행 수입니다. |
| [!UICONTROL 처리 시간] | 수집 시작에서 완료까지의 타임스탬프. |
| [!UICONTROL 상태] | 데이터 흐름의 전체 상태를 정의합니다. 가능한 상태 값은 다음과 같습니다. <ul><li>`Success`: 데이터 흐름이 활성 상태이고 제공된 일정에 따라 데이터를 수집 중임을 나타냅니다.</li><li>`Failed`: 오류로 인해 데이터 흐름의 활성화 프로세스가 중단되었음을 나타냅니다. </li><li>`Processing`: 데이터 흐름이 아직 활성 상태가 아님을 나타냅니다. 이 상태는 종종 새 데이터 흐름을 만든 후 즉시 발생합니다.</li></ul> |

[!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에는 IMS 조직 ID 및 데이터 흐름 실행 ID를 포함하여 [!DNL Profile] 데이터 흐름 실행에 대한 자세한 정보가 표시됩니다. 이 페이지에는 또한 수집 프로세스에서 오류가 발생할 경우 [!DNL Profile]에서 제공하는 해당 오류 코드와 오류 메시지도 표시됩니다.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## 다음 단계

이 자습서를 따르면 **[!UICONTROL 모니터링]** 대시보드를 사용하여 소스 수준, [!DNL Identity Service] 및 [!DNL Profile]에 대한 수집 데이터 흐름을 성공적으로 모니터링했습니다. 또한 수집 프로세스 중에 데이터 흐름의 실패에 기여한 오류를 성공적으로 식별했습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../profile/home.md)
* [Data Science Workspace 개요](../../data-science-workspace/home.md)
