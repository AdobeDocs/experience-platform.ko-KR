---
description: 모니터링 대시보드를 사용하여 소스에서 수집된 데이터를 모니터링하는 방법에 대해 알아봅니다.
title: UI에서 소스에 대한 데이터 흐름 모니터링
exl-id: 53fa4338-c5f8-4e1a-8576-3fe13d930846
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 11%

---

# UI에서 소스의 데이터 흐름 모니터링

>[!IMPORTANT]
>
>[HTTP API 원본](../../sources/connectors/streaming/http.md)과 같은 스트리밍 원본은 현재 모니터링 대시보드에서 지원되지 않습니다. 현재는 대시보드만 사용하여 배치 소스를 모니터링할 수 있습니다.

모니터링 대시보드를 사용하여 Experience Platform UI에서 소스 데이터 흐름을 모니터링하는 방법을 알아보려면 이 문서 를 참조하십시오.

## 시작하기 {#get-started}

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [데이터 흐름](../home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 여러 서비스에 걸쳐 구성되어 있으므로 데이터를 소스 커넥터에서 대상 데이터 세트로, [!DNL Identity] 및 [!DNL Profile], [!DNL Destinations](으)로 이동하는 데 도움이 됩니다.
   * [데이터 흐름 실행](../../sources/notifications.md): 데이터 흐름 실행은 선택한 데이터 흐름의 빈도 구성에 따라 반복되는 예약된 작업입니다.
* [소스](../../sources/home.md): Experience Platform을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [ID 서비스](../../identity-service/home.md): 장치 및 시스템 간에 ID를 연결하여 개별 고객 및 개별 고객의 행동을 더 잘 볼 수 있습니다.
* [실시간 고객 프로필](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합된 실시간 고객 프로필을 제공합니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## 모니터링 대시보드를 사용하여 소스 데이터 모니터링

>[!CONTEXTUALHELP]
>id="platform_monitoring_source_ingestion"
>title="소스 수집"
>abstract="소스 수집 보기에는 레코드 수집과 레코드 실패 등 데이터 레이크 서비스의 데이터 활동 상태와 지표에 대한 정보가 포함됩니다. 지표와 그래프에 대해 자세한 내용은 지표 정의 안내서를 검토하십시오."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_ingestion"
>title="데이터 흐름 실행 세부 정보"
>abstract="소스 처리에는 레코드 수집과 레코드 실패 등 데이터 레이크 서비스의 데이터 활동 상태와 지표에 대한 정보가 포함됩니다. 지표와 그래프에 대해 자세한 내용은 지표 정의 안내서를 검토하십시오."
>text="Learn more in documentation"

<!-- In the [Platform UI](https://platform.adobe.com), select **[!UICONTROL Monitoring]** from the left navigation to access the [!UICONTROL Monitoring] dashboard. The [!UICONTROL Monitoring] dashboard contains metrics and information on all sources dataflows, including insights into the health of data traffic from a source to [!DNL Identity Service], and to [!DNL Profile].

At the center of the dashboard is the [!UICONTROL Source ingestion] panel, which contains metrics and graphs that display data on records ingested and records failed. -->

모니터링 대시보드의 기본 헤더에서 [!UICONTROL 소스]를 선택하여 소스 데이터 흐름 수집 비율 표시로 대시보드를 업데이트합니다.

![소스 카드가 있는 모니터링 대시보드를 선택했습니다.](../assets/ui/monitor-sources/sources.png)

[!UICONTROL 수집 속도] 그래프는 구성된 시간대에 따라 데이터 수집 속도를 표시합니다. 기본적으로 모니터링 대시보드에는 지난 24시간 동안의 수집 비율이 표시됩니다. 시간대를 구성하는 방법에 대한 단계는 [모니터링 시간대를 구성](monitor.md#configure-monitoring-time-frame)하는 방법에 대한 안내서를 참조하십시오.

그래프는 기본적으로 표시되도록 활성화되어 있습니다. 그래프를 숨기려면 **[!UICONTROL 지표 및 그래프]**&#x200B;를 선택하여 토글을 비활성화하고 그래프를 숨깁니다.

![수집 비율 지표 그래프입니다.](../assets/ui/monitor-sources/metrics-graph.png)

대시보드 하단에는 모든 기존 소스 데이터 흐름에 대한 현재 지표 보고서를 요약한 표가 표시됩니다.

![모니터링 대시보드 지표 테이블입니다.](../assets/ui/monitor-sources/metrics-table.png)

| 지표 | 설명 |
| --- | --- |
| 레코드 수신됨 | 소스에서 받은 총 레코드 수입니다. |
| 레코드 수집됨 | 데이터 레이크에 수집된 총 레코드 수입니다. |
| 건너뛴 레코드 | 건너뛴 총 레코드 수입니다. |
| 레코드 실패 | 오류로 인해 수집할 수 없는 총 레코드 수입니다. |
| 수집 비율 | 받은 총 레코드 수를 기반으로 하여 수집된 레코드의 백분율입니다. |
| 총 실패한 데이터 흐름 | 실패한 총 데이터 흐름 수입니다. |

{style="table-layout:auto"}

지표 테이블 위에 제공된 옵션을 사용하여 데이터를 추가로 필터링할 수 있습니다.

| 필터링 옵션 | 설명 |
| --- | --- |
| 검색 | 검색 창을 사용하여 뷰를 단일 소스 유형으로 필터링합니다. |
| 소스 | 소스 유형별로 보기를 필터링하고 지표 데이터를 표시하려면 **[!UICONTROL 소스]**&#x200B;를 선택하십시오. 모니터링 대시보드에서 사용하는 기본 표시입니다. |
| 데이터 흐름 | **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하여 데이터 흐름별로 보기 및 지표 데이터를 필터링합니다. |
| 실패만 표시 | 보기를 필터링하고 수집 실패를 보고한 데이터 흐름만 표시하려면 **[!UICONTROL 오류만 표시]**&#x200B;를 선택하십시오. |
| 내 소스 | [!UICONTROL 내 소스] 드롭다운 메뉴를 사용하여 보기를 추가로 필터링할 수 있습니다. 드롭다운 메뉴를 사용하여 범주별로 보기를 필터링합니다. 또는 **[!UICONTROL 모든 소스]**&#x200B;를 선택하여 모든 소스 또는 소스에 지표를 표시하거나 **[!UICONTROL 내 소스]**&#x200B;를 선택하여 해당 계정이 있는 소스만 표시할 수 있습니다. |

{style="table-layout:auto"}

특정 데이터 흐름에서 수집되는 데이터를 모니터링하려면 소스 옆에 있는 필터 아이콘 ![filter](/help/images/icons/filter-add.png)을(를) 선택하십시오.

![지정된 원본 옆에 있는 필터 아이콘을 선택하여 특정 데이터 흐름을 모니터링합니다.](../assets/ui/monitor-sources/monitor-dataflow.png)

지표 테이블은 선택한 소스에 해당하는 활성 데이터 흐름 테이블로 업데이트됩니다. 이 단계에서는 해당 데이터 세트 및 데이터 유형과 마지막으로 활성화된 시간을 나타내는 타임스탬프를 포함하여 데이터 흐름에 대한 추가 정보를 볼 수 있습니다.

데이터 흐름을 추가로 검사하려면 데이터 흐름 옆에 있는 필터 아이콘 ![filter](/help/images/icons/filter-add.png)을(를) 선택하십시오.

![모니터링 대시보드의 데이터 흐름 테이블입니다.](../assets/ui/monitor-sources/select-dataflow.png)

그런 다음 선택한 데이터 흐름의 모든 데이터 흐름 실행 이터레이션을 나열하는 인터페이스로 이동합니다.

데이터 흐름 실행은 데이터 흐름 실행의 인스턴스를 나타냅니다. 예를 들어 데이터 흐름이 시간별로 오전 9:00, 오전 10:00 및 오전 11:00에 실행되도록 예약되어 있는 경우 흐름 실행의 인스턴스가 3개 있습니다. 플로우 실행은 특정 조직에만 해당됩니다.

특정 데이터 흐름 실행 반복의 지표를 검사하려면 데이터 흐름 옆에 있는 필터 아이콘 ![filter](/help/images/icons/filter-add.png)을(를) 선택하십시오.

![데이터 흐름 실행 지표 페이지입니다.](../assets/ui/monitor-sources/dataflow-page.png)

데이터 흐름 실행 세부 정보 페이지에서는 선택한 실행 반복의 측정 단위 및 정보를 확인할 수 있습니다.

![데이터 흐름 실행 세부 정보 페이지입니다.](../assets/ui/monitor-sources/dataflow-run-details.png)

| 데이터 흐름 실행 세부 정보 | 설명 |
| --- | --- |
| 레코드 수집됨 | 데이터 흐름 실행에서 수집된 총 레코드 수입니다. |
| 레코드 실패 | 데이터 흐름 실행의 오류로 인해 수집되지 않은 총 레코드 수입니다. |
| 총 파일 수 | 데이터 흐름이 실행되는 총 파일 수입니다. |
| 데이터 크기 | 데이터 흐름 실행에 포함된 총 데이터 크기입니다. |
| 데이터 흐름 실행 ID | 데이터 흐름 실행 반복의 ID입니다. |
| 조직 ID | 데이터 흐름 실행이 생성된 조직의 ID입니다. |
| 상태 | 데이터 흐름 실행의 상태입니다. |
| 데이터 흐름 실행 시작 | 데이터 흐름 실행이 시작된 시기를 나타내는 타임스탬프입니다. |
| 데이터 흐름 실행 종료 | 데이터 흐름 실행이 종료된 시점을 나타내는 타임스탬프입니다. |
| 데이터 세트 | 데이터 흐름을 만드는 데 사용되는 데이터 세트입니다. |
| 데이터 유형 | 데이터 흐름에 있었던 데이터의 유형입니다. |
| 부분 수집 | 부분 일괄 처리 수집은 구성 가능한 특정 임계값까지 오류가 포함된 데이터를 수집하는 기능입니다. 이 기능을 사용하면 모든 정확한 데이터를 Experience Platform으로 성공적으로 수집할 수 있으며 잘못된 데이터는 모두 잘못된 이유에 대한 정보로 별도로 배치됩니다. 데이터 흐름 생성 프로세스 중에 부분 수집을 활성화할 수 있습니다. |
| 오류 진단 | 오류 진단은 소스에서 데이터 세트 활동 및 데이터 흐름 상태를 모니터링할 때 나중에 참조할 수 있는 오류 진단을 생성하도록 지시합니다. 데이터 흐름 생성 프로세스 중에 오류 진단을 활성화할 수 있습니다. |
| 오류 요약 | 데이터 흐름 실행이 실패한 경우 오류 요약에는 실행 반복이 실패한 이유를 요약하는 오류 코드와 설명이 표시됩니다. |

{style="table-layout:auto"}

데이터 흐름 실행에서 오류가 보고되면 [!UICONTROL 데이터 흐름 실행 오류] 인터페이스를 사용하여 페이지 아래쪽으로 스크롤할 수 있습니다.

오류로 인해 수집되지 않은 레코드에 대한 지표를 보려면 [!UICONTROL 레코드 실패] 섹션을 사용하십시오. 포괄적인 오류 보고서를 보려면 **[!UICONTROL 오류 진단 미리 보기]**&#x200B;를 선택하십시오. 오류 진단 및 파일 매니페스트의 복사본을 다운로드하려면 **[!UICONTROL 다운로드]**&#x200B;를 선택한 다음 [!DNL Data Access] API와 함께 사용할 예제 API 호출을 복사합니다.

>[!NOTE]
>
>소스 연결 생성 프로세스 중에 기능이 활성화된 경우에만 오류 진단을 사용할 수 있습니다.

![데이터 흐름 실행 오류 패널입니다.](../assets/ui/monitor-sources/errors.png)

## 다음 단계 {#next-steps}

이 자습서에 따라 **[!UICONTROL 모니터링]** 대시보드를 사용하여 소스 수준에서 수집 데이터 흐름을 모니터링했습니다. 또한 수집 프로세스 중에 데이터 흐름 실패의 원인이 되는 오류를 정상적으로 식별했습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [ID 데이터 모니터링](./monitor-identities.md).
* [프로필 데이터 모니터링](./monitor-profiles.md).
