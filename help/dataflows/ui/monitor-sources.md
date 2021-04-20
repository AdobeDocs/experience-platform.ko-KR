---
keywords: Experience Platform;홈;인기 항목;모니터 계정;데이터 흐름;데이터 흐름;소스
description: 이 자습서에서는 집계 모니터링 보기 및 서비스 간 모니터링을 사용하여 데이터 흐름을 모니터링하는 단계를 제공합니다.
solution: Experience Platform
title: UI에서 소스의 데이터 흐름 모니터링
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4c668a47e62ba7736dd2d7afe4e71fd015198356
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 0%

---


# UI에서 소스의 데이터 흐름 모니터링

Adobe Experience Platform에서 데이터는 다양한 소스에서 수집되어 Experience Platform 내에서 분석되고 다양한 대상으로 활성화됩니다. Platform(플래시 플랫폼)을 사용하면 데이터 흐름 투명도를 활용하여 잠재적으로 선형 방식으로 데이터 흐름을 보다 손쉽게 추적할 수 있습니다.

모니터링 대시보드에서는 데이터 흐름 여정을 시각적으로 표시할 수 있습니다. 집계 모니터링 보기를 사용하고 소스 수준에서 데이터 흐름 및 데이터 흐름 실행으로 세로로 이동할 수 있으므로 데이터 흐름 성공 또는 실패에 기여하는 해당 지표를 볼 수 있습니다. 모니터링 대시보드의 서비스 간 모니터링 기능을 사용하여 소스에서 데이터 흐름 여정을 [!DNL Identity Service](으)로, [!DNL Profile]로 모니터링할 수도 있습니다.

이 자습서에서는 집계 모니터링 보기 및 서비스 간 모니터링을 사용하여 데이터 흐름을 모니터링하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [데이터 흐름](../home.md):데이터 프롤링은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름 구성은 여러 서비스에서 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 [!DNL Identity] 및 [!DNL Profile], [!DNL Destinations]로 이동할 수 있습니다.
   * [데이터 흐름 실행](../../sources/notifications.md):Dataflow 실행은 선택한 데이터 흐름의 주파수 구성을 기반으로 하는 반복되는 예약된 작업입니다.
* [소스](../../sources/home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [ID 서비스](../../identity-service/home.md):다양한 디바이스와 시스템에 ID를 연결함으로써 개별 고객과 고객의 행동을 보다 정확하게 파악할 수 있습니다.
* [실시간 고객 프로필](../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 집계 모니터링 보기

[플랫폼 UI](https://platform.adobe.com)의 왼쪽 탐색 메뉴에서 **[!UICONTROL 모니터링]**&#x200B;을 선택하여 [!UICONTROL 모니터링] 대시보드에 액세스합니다. [!UICONTROL 모니터링] 대시보드에는 소스에서 [!DNL Identity Service]로 데이터 트래픽의 상태에 대한 통찰력을 포함하여 모든 소스 데이터 프롤에 대한 지표 및 정보가 포함되어 있습니다. [!DNL Profile].

대시보드 중앙에 [!UICONTROL 소스 통합] 패널이 있습니다. 이 패널에는 인제스트된 레코드와 실패한 레코드에 대한 데이터를 표시하는 지표 및 그래프가 들어 있습니다.

![monitoring-dashboard](../assets/ui/monitor-sources/monitoring-dashboard.png)

기본적으로 표시된 데이터에는 지난 24시간의 섭취 비율이 포함됩니다. 표시된 레코드의 시간대를 조정하려면 **[!UICONTROL 지난 24시간]**&#x200B;을 선택합니다.

![변경 날짜](../assets/ui/monitor-sources/change-date.png)

대체 통합 시간 프레임에 대한 옵션을 제공하는 달력 팝업 창이 나타납니다. **[!UICONTROL 최근 30일]**&#x200B;을 선택한 다음 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![조정 시간 프레임](../assets/ui/monitor-sources/adjust-timeframe.png)

그래프가 기본적으로 활성화되어 있으며 아래 소스 목록을 확장하도록 비활성화할 수 있습니다. 그래프를 비활성화하려면 **[!UICONTROL 지표 및 그래프]** 전환을 선택합니다.

![지표 및 그래프](../assets/ui/monitor-sources/metrics-graphs.png)

| 소스 통합 | 설명 |
| ---------------- | ----------- |
| [!UICONTROL 인제스트된 레코드  ] | 수집되는 총 레코드 수입니다. |
| [!UICONTROL 레코드 실패] | 데이터 오류로 인해 인제스트되지 않은 총 레코드 수입니다. |
| [!UICONTROL 실패한 총 데이터 흐름 수] | `failed` 상태의 총 데이터 흐름 수입니다. |

소스 통합 목록에는 적어도 하나의 기존 계정이 포함된 모든 소스가 표시됩니다. 또한 적용한 시간대를 기준으로 각 소스의 통합 속도, 실패한 레코드 수 및 실패한 총 데이터 흐름 수에 대한 정보도 포함되어 있습니다.

![소스 섭취](../assets/ui/monitor-sources/source-ingestion.png)

소스 목록을 정렬하려면 **[!UICONTROL 내 소스]**&#x200B;를 선택한 다음 드롭다운 메뉴에서 선택 범주를 선택합니다. 예를 들어 클라우드 스토리지에 집중하려면 **[!UICONTROL 클라우드 스토리지]**

![범주별 정렬](../assets/ui/monitor-sources/sort-by-category.png)

모든 소스에서 기존 데이터 흐름을 모두 보려면 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택합니다.

![모든 데이터 흐름 보기](../assets/ui/monitor-sources/view-all-dataflows.png)

또는 소스를 검색 표시줄에 입력하여 단일 소스를 분리할 수 있습니다. 소스를 확인했으면 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png) 옆에 있는 필터 아이콘을 선택하여 활성 데이터 흐름 목록을 확인합니다.

![검색](../assets/ui/monitor-sources/search.png)

데이터 흐름 목록이 나타납니다. 목록 범위를 좁히고 오류가 있는 데이터 흐름에 초점을 맞추려면 **[!UICONTROL 실패만 표시]**&#x200B;를 선택합니다.

![표시 실패 전용](../assets/ui/monitor-sources/show-failures-only.png)

모니터링할 데이터 흐름을 찾은 다음 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png) 옆에 있는 데이터 흐름 아이콘을 선택하여 해당 실행 상태에 대한 자세한 정보를 봅니다.

![데이터 흐름](../assets/ui/monitor-sources/dataflow.png)

데이터 흐름 실행 페이지에는 데이터 흐름의 실행 날짜, 데이터 크기, 상태 및 처리 시간에 대한 정보가 표시됩니다. 데이터 흐름 실행 시작 시간 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)를 선택하여 해당 데이터 흐름 실행 세부 정보를 확인합니다.

![dataflow-run-start](../assets/ui/monitor-sources/dataflow-run-start.png)

[!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에는 데이터 흐름 메타데이터, 부분 통합 상태 및 오류 요약에 대한 정보가 표시됩니다. 오류 요약에는 통합 프로세스에서 오류가 발생한 단계를 보여주는 특정 최상위 오류가 포함되어 있습니다.

발생한 오류에 대한 자세한 내용을 보려면 아래로 스크롤하십시오.

![dataflow run details](../assets/ui/monitor-sources/dataflow-run-details.png)

[!UICONTROL Dataflow 실행 오류] 패널에는 데이터 흐름 수집에 실패한 특정 오류 및 오류 코드가 표시됩니다. 이 시나리오에서는 매퍼 변환 오류가 발생하여 24개의 레코드가 실패했습니다.

자세한 내용을 보려면 **[!UICONTROL 파일]**&#x200B;을 선택합니다.

![dataflow-run-errors](../assets/ui/monitor-sources/dataflow-run-errors.png)

[!UICONTROL 파일] 패널에는 파일의 이름과 경로에 대한 정보가 포함되어 있습니다.

오류를 보다 세부적으로 표현하려면 **[!UICONTROL 오류 진단 미리 보기]**&#x200B;를 선택합니다.

![파일](../assets/ui/monitor-sources/files.png)

데이터 플로우에서 최대 100개의 오류 미리 보기를 표시하는 [!UICONTROL 오류 진단 미리 보기] 창이 나타납니다. **[!UICONTROL 다운로드]**&#x200B;를 선택하여 말림 명령을 검색한 다음 오류 진단을 다운로드할 수 있습니다.

완료되면 **[!UICONTROL 닫기]**&#x200B;를 선택합니다.

![오류 진단](../assets/ui/monitor-sources/error-diagnostics.png)

상단 헤더의 탐색 표시 시스템을 사용하여 [!UICONTROL 모니터링] 대시보드로 돌아가는 길을 탐색할 수 있습니다. **[!UICONTROL 시작 실행:2/14/2021, 9:47 PM]**&#x200B;이 이전 페이지로 돌아가서 **[!UICONTROL 데이터 흐름:충성도 데이터 통합 데모 - 데이터 흐름 페이지로 돌아가기 위해]**&#x200B;에 실패했습니다.

![탐색 표시](../assets/ui/monitor-sources/breadcrumbs.png)

## 크로스 서비스 모니터링

대시보드의 위쪽 부분에는 소스 수준, [!DNL Identity Service] 및 [!DNL Profile]에 대한 통합 흐름이 표시됩니다. 각 셀에는 통합 단계에서 발생한 오류가 있음을 나타내는 점 마커가 포함됩니다. 녹색 점은 오류 없는 섭취, 빨간색 점은 섭취 특정 단계에서 오류가 발생했음을 의미합니다.

![크로스 서비스 모니터링](../assets/ui/monitor-sources/cross-service-monitoring.png)

데이터 흐름 페이지에서 성공적인 데이터 흐름을 찾아 그 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택하여 해당 데이터 흐름 실행 정보를 확인합니다.

![dataflow success](../assets/ui/monitor-sources/dataflow-success.png)

[!UICONTROL 소스 통합] 페이지에는 데이터 흐름 통합 성공 확인을 확인하는 정보가 포함되어 있습니다. 여기에서 데이터 흐름 여정을 소스 수준에서 [!DNL Identity Service]으로 모니터링한 다음 [!DNL Profile]으로 모니터링할 수 있습니다.

[!UICONTROL ID ]**스테이지에서 인제스트를 보려면**[!UICONTROL  ID]를 선택합니다.

![sources](../assets/ui/monitor-sources/sources.png)

### [!DNL Identity] 지표

[!UICONTROL ID 처리] 페이지에는 추가된 ID 수, 만들어진 그래프 및 업데이트된 그래프를 비롯하여 [!DNL Identity Service]에 수집되는 레코드에 대한 정보가 포함되어 있습니다.

[!DNL Identity] 데이터 흐름 실행에 대한 자세한 내용을 보려면 데이터 흐름 시작 시간 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택합니다.

![id](../assets/ui/monitor-sources/identities.png)

| ID 지표 | 설명 |
| ---------------- | ----------- |
| [!UICONTROL 받은 레코드] | [!DNL Data Lake]에서 받은 레코드 수입니다. |
| [!UICONTROL 레코드 실패] | 데이터 오류로 인해 플랫폼으로 인제스트되지 않은 레코드 수입니다. |
| [!UICONTROL 건너뛰는 레코드] | 레코드 행에 식별자가 하나만 있기 때문에 인제스트되었지만 [!DNL Identity Service]에 포함되지 않은 레코드 수입니다. |
| [!UICONTROL 인제스트된 레코드] | [!DNL Identity Service]에 인제스트된 레코드 수입니다. |
| [!UICONTROL 총 레코드 수] | 실패한 레코드, 건너뛴 레코드, [!DNL Identities] 추가됨 및 중복된 레코드를 포함하여 모든 레코드의 총 수입니다. |
| [!UICONTROL 추가된 ID] | [!DNL Identity Service]에 추가된 순 새 식별자 수입니다. |
| [!UICONTROL 만든 그래프] | [!DNL Identity Service]에서 만든 순 새 ID 그래프의 수입니다. |
| [!UICONTROL 그래프 업데이트됨] | 새 가장자리로 업데이트된 기존 ID 그래프 수입니다. |
| [!UICONTROL 실패한 데이터 흐름 실행] | 실패한 데이터 흐름 실행 수입니다. |
| [!UICONTROL 처리 시간] | 통합 시작에서 완료까지의 타임스탬프. |
| [!UICONTROL 상태] | 데이터 흐름의 전체 상태를 정의합니다. 가능한 상태 값은 다음과 같습니다. <ul><li>`Success`:데이터 흐름 기능이 활성 상태이며 제공된 일정에 따라 데이터를 인제스트하고 있음을 나타냅니다.</li><li>`Failed`:오류로 인해 데이터 흐름 활성화 프로세스가 중단되었음을 나타냅니다. </li><li>`Processing`:데이터 흐름 기능이 아직 활성화되지 않았음을 나타냅니다. 새 데이터 흐름 만들기 직후 이 상태가 발생하는 경우가 많습니다.</li></ul> |

[!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에는 IMS 조직 ID 및 데이터 흐름 실행 ID를 포함하여 [!DNL Identity] 데이터 흐름 실행에 대한 자세한 정보가 표시됩니다. 또한 이 페이지는 처리 프로세스에서 오류가 발생하는 경우 [!DNL Identity Service]에서 제공하는 해당 오류 코드와 오류 메시지를 표시합니다.

**[!UICONTROL 시작 실행:이전 페이지로 돌아가려면 2/14/2021, 9:47 PM]**

![id-dataflow-run](../assets/ui/monitor-sources/identities-dataflow-run.png)

[!UICONTROL ID 처리] 페이지에서 **[!UICONTROL 프로필]**&#x200B;을 선택하여 [!UICONTROL 프로필] 단계에서 레코드 수집의 상태를 확인합니다.

![select-profiles](../assets/ui/monitor-sources/select-profiles.png)

### [!DNL Profile] 지표

[!UICONTROL 프로필 처리] 페이지에는 생성된 프로필 조각 수, 업데이트된 프로필 조각 및 총 프로필 조각 수를 포함하여 [!DNL Profile]에 수집되는 레코드에 대한 정보가 포함되어 있습니다.

[!DNL Profile] 데이터 흐름 실행에 대한 자세한 내용을 보려면 데이터 흐름 시작 시간 옆에 있는 필터 아이콘 ![필터](../assets/ui/monitor-sources/filter.png)을 선택합니다.

![프로파일](../assets/ui/monitor-sources/profiles.png)

| 프로필 지표 | 설명 |
| --------------- | ----------- |
| [!UICONTROL 받은 레코드] | [!DNL Data Lake]에서 받은 레코드 수입니다. |
| [!UICONTROL 레코드 실패  ] | 오류로 인해 인제스트되었지만 [!DNL Profile]에 포함되지 않은 레코드 수입니다. |
| [!UICONTROL 프로필 조각 추가됨] | 추가된 순 새 [!DNL Profile] 조각 수입니다. |
| [!UICONTROL 프로필 조각 업데이트됨] | 업데이트된 기존 [!DNL Profile] 조각 수 |
| [!UICONTROL 총 프로필 조각] | 업데이트된 모든 기존 [!DNL Profile] 조각과 새로 만든 [!DNL Profile] 조각을 포함하여 [!DNL Profile]에 기록된 총 레코드 수입니다. |
| [!UICONTROL 실패한 데이터 흐름 실행] | 실패한 데이터 흐름 실행 수입니다. |
| [!UICONTROL 처리 시간] | 통합 시작에서 완료까지의 타임스탬프. |
| [!UICONTROL 상태] | 데이터 흐름의 전체 상태를 정의합니다. 가능한 상태 값은 다음과 같습니다. <ul><li>`Success`:데이터 흐름 기능이 활성 상태이며 제공된 일정에 따라 데이터를 인제스트하고 있음을 나타냅니다.</li><li>`Failed`:오류로 인해 데이터 흐름 활성화 프로세스가 중단되었음을 나타냅니다. </li><li>`Processing`:데이터 흐름 기능이 아직 활성화되지 않았음을 나타냅니다. 새 데이터 흐름 만들기 직후 이 상태가 발생하는 경우가 많습니다.</li></ul> |

[!UICONTROL 데이터 흐름 실행 세부 정보] 페이지에는 IMS 조직 ID 및 데이터 흐름 실행 ID를 포함하여 [!DNL Profile] 데이터 흐름 실행에 대한 자세한 정보가 표시됩니다. 또한 이 페이지는 처리 프로세스에서 오류가 발생하는 경우 [!DNL Profile]에서 제공하는 해당 오류 코드와 오류 메시지를 표시합니다.

![profiles-dataflow-run](../assets/ui/monitor-sources/profiles-dataflow-run.png)

## 다음 단계

이 자습서에서는 **[!UICONTROL 모니터링]** 대시보드를 사용하여 소스 수준, [!DNL Identity Service] 및 [!DNL Profile]에 대한 통합 데이터 흐름을 성공적으로 모니터링했습니다. 통합 프로세스 중 데이터 흐름 실패에 기여한 오류를 식별했습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../profile/home.md)
* [데이터 과학 작업 공간 개요](../../data-science-workspace/home.md)
