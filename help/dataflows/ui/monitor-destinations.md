---
keywords: Experience Platform;홈;인기 항목;계정 모니터링;데이터 흐름 모니터링;데이터 흐름;대상
description: 대상을 사용하면 Adobe Experience Platform에서 수많은 외부 파트너로 데이터를 활성화할 수 있습니다. 이 자습서에서는 Experience Platform 사용자 인터페이스를 사용하여 대상에 대한 데이터 흐름을 모니터링하는 방법에 대한 지침을 제공합니다.
solution: Experience Platform
title: UI에서 대상에 대한 데이터 흐름 모니터링
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '3211'
ht-degree: 0%

---

# UI에서 대상에 대한 데이터 흐름 모니터링

대상을 사용하면 Adobe Experience Platform에서 수많은 외부 파트너로 데이터를 활성화할 수 있습니다. 플랫폼 을 사용하면 데이터 흐름에 투명성을 제공하여 대상으로의 데이터 흐름 추적 프로세스를 보다 쉽게 수행할 수 있습니다.

모니터링 대시보드는 데이터가 활성화된 대상을 포함하여 데이터 흐름의 여정을 시각적으로 나타냅니다. 이 자습서에서는 대상 작업 영역에서 직접 데이터 흐름을 모니터링하거나 모니터링 대시보드를 사용하여 Experience Platform 사용자 인터페이스를 사용하여 대상의 데이터 흐름을 모니터링하는 방법에 대한 지침을 제공합니다.

## 시작하기 {#getting-started}

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [데이터 흐름](../home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 서로 다른 서비스 간에 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 [!DNL Identity] 및 [!DNL Profile], 및에 [!DNL Destinations].
   - [데이터 흐름 실행](../../sources/notifications.md): 데이터 흐름 실행은 선택한 데이터 흐름의 빈도 구성에 따라 반복되는 예약된 작업입니다.
- [대상](../../destinations/home.md): 대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 일반적으로 사용되는 애플리케이션과의 사전 구축된 통합입니다.
- [샌드박스](../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

## 대상 작업 공간에서 데이터 흐름 모니터링 {#monitor-dataflows-in-the-destinations-workspace}

에서 **[!UICONTROL 대상]** 플랫폼 UI 내에서 **[!UICONTROL 찾아보기]** 탭하고 보려는 대상의 이름을 선택합니다.

![대상 보기 선택](../assets/ui/monitor-destinations/select-destination.png)

기존 데이터 흐름 목록이 나타납니다. 이 페이지에는 대상, 사용자 이름, 데이터 흐름 수 및 상태에 대한 정보를 포함하여 볼 수 있는 데이터 흐름 목록이 있습니다.

상태에 대한 자세한 내용은 다음 표를 참조하십시오.

| 상태 | 설명 |
| ------ | ----------- |
| 활성화됨 | 다음 `Enabled` 상태는 데이터 흐름이 활성 상태이며 제공된 일정에 따라 데이터를 내보내고 있음을 나타냅니다. |
| 비활성화됨 | 다음 `Disabled` 상태는 데이터 흐름이 비활성 상태이고 데이터를 내보내지 않고 있음을 나타냅니다. |
| 처리 중 | 다음 `Processing` 상태는 데이터 흐름이 아직 활성화되지 않았음을 나타냅니다. 이 상태는 종종 새 데이터 흐름을 만든 후 즉시 발생합니다. |
| 오류 | 다음 `Error` 상태는 데이터 흐름의 활성화 프로세스가 중단되었음을 나타냅니다. |

### 스트리밍 대상에 대해 데이터 흐름 실행 {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="데이터 흐름 실행 세부 정보"
>abstract="대상 데이터 흐름 실행 세부 사항에는 실시간 고객 프로필에서 가져온 세그먼트의 활성화 상태 및 지표에 대한 정보가 포함되어 있으며 고유한 ID를 생성합니다. 자세한 내용은 지표 정의 안내서를 참조하십시오."

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="받은 프로필"
>abstract="데이터 플로우에서 받은 총 프로필 수 이 값은 60분마다 업데이트됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="ID가 활성화됨"
>abstract="개별 프로필 ID의 수가 선택한 대상에 성공적으로 활성화되었습니다. 이 지표에는 내보낸 세그먼트에서 생성, 업데이트 및 제거된 ID가 포함됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="제외된 ID"
>abstract="누락된 속성 및 동의 위반을 기반으로 선택한 대상에 대한 활성화에서 제외된 개별 프로필 레코드 수입니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="ID 실패"
>abstract="선택한 대상에 대해 실패한 개별 프로필 ID의 수입니다. 자세한 내용은 오류 진단을 확인하십시오."

스트리밍 대상의 경우, [!UICONTROL 데이터 흐름 실행] 탭은 데이터 흐름 실행에 대한 지표 데이터에 대한 시간별 업데이트를 제공합니다. 가장 눈에 띄는 통계들은 ID에 대한 것이다.

ID는 프로필의 다른 패싯을 나타냅니다. 예를 들어 프로필에 전화 번호와 이메일 주소가 모두 포함된 경우 해당 프로필에는 두 개의 ID가 있습니다.

개별 실행 및 해당 특정 지표 목록과 ID에 대한 다음 합계가 표시됩니다.

- **[!UICONTROL ID가 활성화됨]**: 선택한 대상에 성공적으로 활성화된 총 프로필 ID 수입니다. 이 지표에는 내보낸 세그먼트에서 생성, 업데이트 및 제거된 ID가 포함됩니다.
- **[!UICONTROL 제외된 ID]**: 누락된 속성 및 동의 위반을 기반으로 하여 활성화를 위해 건너뛴 총 프로필 ID 수입니다.
- **[!UICONTROL ID 실패]**: 오류로 인해 대상에 활성화되지 않은 총 프로필 ID 수입니다.

![데이터 흐름은 스트리밍 대상에 대한 세부 정보를 실행합니다](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

각 개별 데이터 흐름 실행에는 다음 세부 정보가 표시됩니다.

- **[!UICONTROL 데이터 흐름 실행 시작]**: 데이터 흐름 실행이 시작된 시간입니다. 데이터 흐름 스트리밍 실행의 경우, Experience Platform은 데이터 흐름 실행의 시작을 기반으로 지표를 시간별 지표 형태로 캡처합니다. 스트리밍 데이터 흐름 실행의 경우, 예를 들어 데이터 흐름 실행이 오후 10:30에 시작된 경우, 지표는 UI에서 시작 시간을 오후 10:00으로 표시합니다.
- **[!UICONTROL 처리 시간]**: 데이터 흐름 실행이 처리되는 데 걸린 시간입니다.
   - 대상 **[!UICONTROL 완료됨]** 를 실행하면 처리 시간 지표에 항상 1시간이 표시됩니다.
   - 데이터 흐름의 경우 **[!UICONTROL 처리]** state, 데이터 흐름 실행에 해당하는 모든 지표를 처리하기 위해 1시간 이상 동안 모든 지표를 캡처하는 창이 열려 있습니다. 예를 들어, 오전 9:30에 시작된 데이터 흐름 실행은 1시간 30분 동안 처리 상태를 유지하여 모든 지표를 캡처하고 처리할 수 있습니다. 그런 다음 처리 창이 닫히고 데이터 흐름 실행 상태가 **완료됨**&#x200B;로 설정되면 표시된 처리 시간이 1시간으로 변경됩니다.
- **[!UICONTROL 받은 프로필]**: 데이터 플로우에서 받은 총 프로필 수
- **[!UICONTROL ID가 활성화됨]**: 데이터 흐름 실행의 일부로 선택한 대상에 성공적으로 활성화된 총 프로필 ID 수입니다. 이 지표에는 내보낸 세그먼트에서 생성, 업데이트 및 제거된 ID가 포함됩니다.
- **[!UICONTROL 제외된 ID]**: 누락된 속성 및 동의 위반으로 인해 활성화에서 제외된 총 프로필 ID 수입니다.
- **[!UICONTROL ID 실패]** 오류로 인해 대상에 활성화되지 않은 총 프로필 ID 수입니다.
- **[!UICONTROL 활성화 비율]**: 성공적으로 활성화되었거나 건너뛴 받은 ID의 백분율입니다. 다음 수식은 이 값을 계산하는 방법을 보여 줍니다.
   ![활성화 비율 공식](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL 상태]**: 데이터 흐름의 상태를 나타냅니다. 둘 중 하나 [!UICONTROL 완료됨] 또는 [!UICONTROL 처리 중]. [!UICONTROL 완료됨] 은(는) 해당 데이터 흐름 실행에 대한 모든 ID를 1시간 기간 내에 내보냈음을 의미합니다. [!UICONTROL 처리 중] 은(는) 데이터 흐름 실행이 아직 완료되지 않았음을 의미합니다.

특정 데이터 흐름 실행에 대한 세부 정보를 보려면 목록에서 실행 시작 시간을 선택합니다.

데이터 흐름 실행에 대한 세부 정보 페이지에는 받은 프로필 수, 활성화된 ID 수, 실패한 ID 수 및 제외된 ID 수와 같은 추가 정보가 포함되어 있습니다.

![스트리밍 대상에 대한 데이터 흐름 세부 정보](../assets/ui/monitor-destinations/dataflow-details-stream.png)

세부 사항 페이지에는 실패한 ID 목록과 제외된 ID도 표시됩니다. 오류 코드, ID 수 및 설명을 포함하여 실패한 ID와 제외된 ID에 대한 정보가 표시됩니다. 기본적으로 목록에 실패한 ID가 표시됩니다. 건너뛴 ID를 표시하려면 **[!UICONTROL 제외된 ID]** 토글.

![스트리밍 대상을 위한 데이터 흐름 레코드](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### 데이터 흐름은 배치 대상에 대해 실행됩니다 {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="데이터 흐름 실행 세부 정보"
>abstract="대상 데이터 흐름 실행 세부 사항에는 실시간 고객 프로필에서 가져온 세그먼트의 활성화 상태 및 지표에 대한 정보가 포함되어 있으며 고유한 ID를 생성합니다. 자세한 내용은 지표 정의 안내서를 참조하십시오."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html#dataflow-runs-for-streaming-destinations" text="스트리밍 대상에 대해 데이터 흐름 실행"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="받은 프로필"
>abstract="데이터 플로우에서 받은 총 프로필 수 이 값은 60분마다 업데이트됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="ID가 활성화됨"
>abstract="개별 프로필 ID의 수가 선택한 대상에 성공적으로 활성화되었습니다. 이 지표에는 내보낸 세그먼트에서 생성, 업데이트 및 제거된 ID가 포함됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="제외된 ID"
>abstract="누락된 속성 및 동의 위반을 기반으로 선택한 대상에 대한 활성화에서 제외된 개별 프로필 레코드 수입니다."

배치 대상의 경우, [!UICONTROL 데이터 흐름 실행] 탭은 데이터 흐름 실행에 대한 지표 데이터를 제공합니다. 개별 실행 및 해당 특정 지표 목록과 ID에 대한 다음 합계가 표시됩니다.

- **[!UICONTROL ID가 활성화됨]**: 선택한 대상에 성공적으로 활성화된 총 프로필 ID 수입니다. 이 지표에는 내보낸 세그먼트에서 생성, 업데이트 및 제거된 ID가 포함됩니다.
- **[!UICONTROL 제외된 ID]**: 누락된 속성 및 동의 위반을 기반으로 선택한 대상에 대한 활성화에서 제외된 개별 프로필 ID의 수입니다.

![데이터 흐름은 배치 대상에 대한 보기를 실행합니다](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

각 개별 데이터 흐름 실행에는 다음 세부 정보가 표시됩니다.

- **[!UICONTROL 데이터 흐름 실행 시작]**: 데이터 흐름 실행이 시작된 시간입니다.
- **[!UICONTROL 세그먼트]**: 각 데이터 흐름 실행과 연결된 세그먼트의 이름입니다.
- **[!UICONTROL 처리 시간]**: 데이터 흐름 실행을 처리하는 데 걸린 시간입니다.
- **[!UICONTROL 받은 프로필]**: 데이터 플로우에서 받은 총 프로필 수 이 값은 60분마다 업데이트됩니다.
- **[!UICONTROL ID가 활성화됨]**: 데이터 흐름 실행의 일부로 선택한 대상에 성공적으로 활성화된 총 프로필 ID 수입니다. 이 지표에는 내보낸 세그먼트에서 생성, 업데이트 및 제거된 ID가 포함됩니다.
- **[!UICONTROL 제외된 ID]**: 누락된 속성 및 동의 위반으로 인해 활성화에서 제외된 총 프로필 ID 수입니다.
- **[!UICONTROL 상태]**: 데이터 흐름의 상태를 나타냅니다. 다음 세 가지 상태 중 하나일 수 있습니다. [!UICONTROL 성공], [!UICONTROL 실패], 및 [!UICONTROL 처리 중]. [!UICONTROL 성공] 은(는) 데이터 흐름이 활성 상태이고 제공된 일정에 따라 데이터를 내보내고 있음을 의미합니다. [!UICONTROL 실패] 은(는) 오류로 인해 데이터 활성화가 일시 중단되었음을 의미합니다. [!UICONTROL 처리 중] 은(는) 데이터 흐름이 아직 활성 상태가 아니며 새 데이터 흐름을 만들 때 일반적으로 발생함을 의미합니다.

특정 데이터 흐름 실행에 대한 세부 정보를 보려면 목록에서 실행 시작 시간을 선택합니다.

>[!NOTE]
>
>데이터 흐름 실행은 대상 데이터 흐름의 예약 빈도를 기반으로 생성됩니다. 각 데이터에 대해 별도의 데이터 흐름 실행이 수행됩니다 [병합 정책](../../profile/merge-policies/overview.md) 세그먼트에 적용되었습니다.

데이터 흐름 목록에 표시된 세부 정보 외에 데이터 흐름의 세부 정보 페이지에는 데이터 흐름에 대한 보다 구체적인 정보가 표시됩니다.

- **[!UICONTROL 데이터 크기]**: 내보낼 데이터 흐름의 크기입니다.
- **[!UICONTROL 총 파일 수]**: 데이터 흐름에서 내보낸 총 파일 수입니다.
- **[!UICONTROL 마지막 업데이트 날짜]**: 데이터 흐름 실행이 마지막으로 업데이트된 시간입니다.

![일괄 처리 대상에 대한 데이터 흐름 실행 세부 정보](../assets/ui/monitor-destinations/dataflow-batch.png)

세부 사항 페이지에는 실패한 ID 목록과 제외된 ID도 표시됩니다. 오류 코드 및 설명을 포함하여 실패한 ID와 제외된 ID에 대한 정보가 표시됩니다. 기본적으로 목록에 실패한 ID가 표시됩니다. 제외된 ID를 표시하려면 **[!UICONTROL 제외된 ID]** 토글.

![배치 대상에 대한 데이터 흐름 레코드](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## 대상 대시보드 모니터링 {#monitoring-destinations-dashboard}

>[!NOTE]
>
>- 대상 모니터링 기능은 현재 Experience Platform의 모든 대상에 대해 지원됩니다 *제외* a [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 및 [사용자 지정 개인화](/help/destinations/catalog/personalization/custom-personalization.md) 대상.
>- 대상 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [Azure 이벤트 허브](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), 및 [HTTP API](/help/destinations/catalog/streaming/http-destination.md) 대상, 제외된 id가 현재 표시되지 않습니다.


>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="활성화"
>abstract="대상 활성화 보기에는 세그먼트의 활성화 상태 및 실시간 고객 프로필에서 가져와 고유한 ID를 생성하는 지표에 대한 정보가 포함되어 있습니다."

에 액세스하려면 [!UICONTROL 모니터링] 대시보드, 선택 **[!UICONTROL 모니터링]** (![모니터링 아이콘](../assets/ui/monitor-destinations/monitoring-icon.png))을 클릭하여 제품에서 사용할 수 있습니다. 에 한 번 [!UICONTROL 모니터링] 페이지를 선택하고 [!UICONTROL 대상]. 다음 [!UICONTROL 모니터링] 대시보드에는 대상 실행 작업에 대한 지표와 정보가 포함되어 있습니다.

를 사용하십시오 [!UICONTROL 대상] 대시보드 를 사용하여 활성화 흐름의 상태를 전체적으로 확인할 수 있습니다. 먼저 모든 일괄 처리 및 스트리밍 대상에 대해 집계된 수준에서 통찰력을 얻은 다음 데이터 흐름, 데이터 흐름, 데이터 흐름 실행 및 활성화된 세그먼트에 대한 세부 보기로 드릴다운하여 활성화 데이터를 심층적으로 살펴봅니다. 의 화면 [!UICONTROL 모니터링] 대시보드는 활성화 시나리오에서 발생할 수 있는 모든 문제를 해결하는 데 도움이 되는 지표와 오류 설명을 통해 실행 가능한 통찰력을 제공합니다.

대시보드 중앙에는 다음이 있습니다 [!UICONTROL 활성화] 패널에 포함된 패널에는 스트리밍 대상으로 내보낸 데이터의 활성화율 및 실패한 배치 데이터 흐름의 데이터를 배치 대상으로 실행하는 데이터 그래프가 들어 있습니다.

![스트리밍 및 일괄 활성화 그래프](../assets/ui/monitor-destinations/dashboard-graph.png)


기본적으로 표시되는 데이터에는 지난 24시간의 활성화 정보가 포함됩니다. 선택 **[!UICONTROL 최근 24시간]** 를 눌러 표시되는 레코드의 시간대를 조정합니다. 사용 가능한 옵션은 다음과 같습니다 **[!UICONTROL 최근 24시간]**, **[!UICONTROL 최근 7일]**, 및 **[!UICONTROL 최근 30일]**. 또는 나타나는 달력 팝업 창에서 날짜를 선택할 수 있습니다. 날짜를 선택한 후 **[!UICONTROL 적용]** 를 눌러 표시된 정보의 시간대를 조정합니다.

>[!NOTE]
>
>다음 스크린샷에서는 지난 24시간이 아닌 최근 30일 동안의 활성화 속도 및 배치 데이터 흐름 실행을 보여줍니다. 을(를) 선택하여 시간 프레임을 조정할 수 있습니다 **[!UICONTROL 최근 30일]**.

![활성화된 대상에 대한 전환 확인 날짜 범위 변경](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

화살표 아이콘 사용(![화살표 아이콘](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) 카드를 확장하거나 축소할 수 있습니다. 화면의 맨 위에 대상 유형(스트리밍 또는 배치)에 따라 활성화 세부 사항에 대한 요약 정보가 표시됩니다.

- **[!UICONTROL 스트리밍 활성화 비율]**: 성공적으로 활성화되었거나 건너뛴 받은 ID의 백분율을 나타냅니다. 이 백분율을 계산하는 데 사용되는 공식은 이 페이지의 [스트리밍 대상에 대해 데이터 흐름 실행](#dataflow-runs-for-streaming-destinations) 섹션을 참조하십시오.
- **[!UICONTROL 일괄 처리 실패 데이터 흐름 실행]**: 선택한 시간 간격에서 실패한 데이터 흐름 실행 수를 나타냅니다.

![페이지 맨 위에 카드 표시 또는 해제](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

다음 **[!UICONTROL 활성화]** 그래프가 기본적으로 표시되며, 이를 비활성화하여 아래 대상 목록을 확장할 수 있습니다. 을(를) 선택합니다 **[!UICONTROL 지표 및 그래프]** 그래프를 비활성화하려면 을(를) 전환합니다.

다음 **[!UICONTROL 활성화]** 패널에는 하나 이상의 기존 계정이 포함된 대상 목록이 표시됩니다. 이 목록에는 받은 프로필, 활성화된 ID, 실패한 ID, 제외된 ID, 활성화 비율, 실패한 총 데이터 흐름 및 이러한 대상에 대한 마지막 업데이트 날짜에 대한 정보도 포함됩니다. 모든 대상 유형에 일부 지표를 사용할 수 있는 것은 아닙니다. 아래 표는 대상 유형, 스트리밍 또는 배치별로 사용할 수 있는 지표를 간략하게 설명합니다.

| 지표 | 대상 유형 |
---------|----------|
| **[!UICONTROL 받은 프로필]** | 스트리밍 및 일괄 처리 |
| **[!UICONTROL ID가 활성화됨]** | 스트리밍 및 일괄 처리 |
| **[!UICONTROL ID 실패]** | 스트리밍 |
| **[!UICONTROL 제외된 ID]** | 스트리밍 및 일괄 처리 |
| **[!UICONTROL 활성화 비율]** | 스트리밍 |
| **[!UICONTROL 실패한 총 데이터 흐름 수]** | 일괄 처리 |
| **[!UICONTROL 마지막으로 업데이트됨]** | 스트리밍 및 일괄 처리 |

![활성화된 모든 대상을 대시보드](../assets/ui/monitor-destinations/dashboard-destinations.png)

대상 목록을 필터링하여 선택한 대상 카테고리만 표시할 수도 있습니다. 을(를) 선택합니다 **[!UICONTROL 내 대상]** 드롭다운을 선택하고 을(를) 선택합니다. [대상 카테고리](/help/destinations/destination-types.md#categories) 필터링합니다.

![드롭다운 선택기를 사용하여 대상 필터링](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

또한 검색 막대에 대상을 입력하여 단일 대상으로 분리할 수 있습니다. 대상의 데이터 흐름을 보려면 필터를 선택할 수 있습니다 ![필터](../assets/ui/monitor-destinations/filter-add.png) 옆에 활성 데이터 흐름 목록을 보려면 해당 데이터 흐름 목록을 확인하십시오.

![검색 막대를 사용하여 대상 필터링](../assets/ui/monitor-destinations/filtered-destinations.png)

모든 대상에서 기존 데이터 흐름을 모두 보려면 **[!UICONTROL 데이터 흐름]**.

마지막 데이터 흐름 실행을 기준으로 정렬된 데이터 흐름 목록이 나타납니다. 모니터링할 대상을 찾아 필터를 선택하여 특정 데이터 집합에 대한 추가 세부 정보를 볼 수 있습니다 ![필터](../assets/ui/monitor-destinations/filter-add.png) 옆에 있는 필터를 선택한 다음 필터를 선택합니다 ![필터](../assets/ui/monitor-destinations/filter-add.png) 데이터 흐름 옆의 정보 옆에 있어야 합니다.

![모니터링 대시보드에서 강조 표시된 모든 데이터 흐름](../assets/ui/monitor-destinations/dashboard-dataflows.png)

추가 검사를 위해 데이터 흐름을 선택하면 데이터 흐름 세부 정보 페이지에 데이터 흐름 실행 또는 세그먼트로 분류된 데이터 흐름에서 활성화된 데이터를 볼 수 있는 토글이 포함되어 있습니다.

### 데이터 흐름 실행 보기 {#dataflow-runs-view}

When **[!UICONTROL 데이터 흐름 실행]** 이 선택되면 선택한 데이터 흐름의 데이터 흐름 실행 목록과 각 실행에 대한 자세한 정보를 볼 수 있습니다.

>[!INFO]
>
>데이터 흐름에서 스트리밍 대상으로 데이터의 경우 데이터 흐름 실행은 시간별 창으로 분류됩니다. 각 시간별 창은 해당 데이터 흐름 실행 ID를 생성합니다.
>
>데이터 흐름에서 배치 대상으로 보내는 경우, 각 세그먼트에는 세그먼트 활성화 예약 빈도를 기반으로 생성된 해당 데이터 흐름 실행이 있습니다. 예를 들어 동일한 대상 데이터 흐름에서 5개의 세그먼트에 대해 일별 예약된 활성화를 설정하면 매일 5개의 개별 데이터 흐름 실행이 생성됩니다.

![흐름 실행 패널](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

를 사용하십시오 **[!UICONTROL 실패만 표시]** 데이터 플로우에 대해 실패한 실행만 표시하려면 토글 을 사용합니다.

![데이터 흐름 실행 - 실패만 표시 전환](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### 세그먼트 수준 보기 {#segment-level-view}

When **[!UICONTROL 세그먼트]** 을 선택하면 선택한 데이터 흐름으로 활성화된 세그먼트 목록이 선택한 시간 범위 내에 표시됩니다. 이 화면에는 활성화된 ID와 제외된 ID에 대한 세그먼트 수준 정보와 마지막 데이터 흐름 실행 상태 및 시간이 포함됩니다. 제외되고 활성화된 ID에 대한 지표를 검토하여 세그먼트가 성공적으로 활성화되었는지 확인할 수 있습니다.

예를 들어, &quot;캘리포니아 주의 충성도 멤버&quot;라는 세그먼트를 Amazon S3 대상 &quot;캘리포니아 12월 충성도 멤버&quot;에 활성화하는 것입니다. 선택한 세그먼트에 100개의 프로필이 있지만 100개 프로필 중 80개만 충성도 ID 속성을 포함하고 내보내기 매핑 규칙을 다음과 같이 정의했다고 가정합니다 `loyalty.id` 는 필수입니다. 이 경우 세그먼트 수준에서 80개의 ID가 활성화되고 20개의 ID가 제외됩니다.

>[!IMPORTANT]
>
>세그먼트 수준 지표와 관련된 현재 제한 사항을 확인합니다.
>- 세그먼트 수준 보기는 현재 배치 대상에 대해서만 사용할 수 있습니다.
>- 세그먼트 수준 지표는 현재 성공적인 데이터 흐름 실행에 대해서만 기록됩니다. 실패한 데이터 흐름 실행 및 제외된 레코드에 대해서는 기록되지 않습니다.


![데이터 흐름 패널의 세그먼트](../assets/ui/monitor-destinations/dashboard-segments-view.png)

세그먼트 수준 보기에서 지표는 선택한 시간 범위 내에서 여러 데이터 흐름 실행에서 집계됩니다. 여러 데이터 흐름 실행이 있는 경우, 세그먼트 수준에서 드릴다운하여 선택한 세그먼트로 필터링된 각 데이터 흐름 실행에 대한 분류를 확인할 수 있습니다.
필터 단추 사용 ![필터](../assets/ui/monitor-destinations/filter-add.png) 데이터 흐름의 각 세그먼트에 대한 데이터 흐름 실행 보기로 드릴다운하려면 다음을 수행합니다.

### 데이터 흐름 실행 페이지 {#dataflow-runs-page}

데이터 흐름 실행 페이지에는 데이터 흐름 실행 시작 시간, 처리 시간, 받은 프로필, 활성화된 ID, 제외된 ID, 실패한 ID, 활성화 비율 및 상태를 비롯한 데이터 흐름 관련 정보가 표시됩니다.

데이터 흐름 실행 페이지로 드릴다운하면 [세그먼트 수준 보기](#segment-level-view)에서는 다음 선택 사항으로 데이터 흐름 실행을 필터링하는 옵션이 있습니다.

- **[!UICONTROL 실패한 ID로 데이터 흐름 실행]**: 선택한 세그먼트의 경우 이 옵션은 활성화에 실패한 모든 데이터 흐름 실행을 나열합니다. 특정 데이터 흐름 실행에서 ID가 실패한 이유를 검사하려면 [데이터 흐름 실행 세부 정보 페이지](#dataflow-run-details-page) 해당 데이터 흐름 실행을 위한 것입니다.
- **[!UICONTROL 건너뛴 ID를 사용하여 데이터 흐름 실행]**: 선택한 세그먼트의 경우 이 옵션은 일부 ID가 완전히 활성화되지 않고 일부 프로필을 건너뛰었던 모든 데이터 흐름 실행을 나열합니다. 특정 데이터 흐름 실행에서 ID를 건너뛴 이유를 확인하려면 [데이터 흐름 실행 세부 정보 페이지](#dataflow-run-details-page) 해당 데이터 흐름 실행을 위한 것입니다.
- **[!UICONTROL 데이터 흐름은 활성화된 ID를 사용하여 실행됩니다]**: 선택한 세그먼트의 경우, 이 옵션은 성공적으로 활성화된 ID가 있는 모든 데이터 흐름 실행을 나열합니다.

![세그먼트에 대한 데이터 흐름 필터링 실행](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

특정 데이터 흐름 실행에 대한 자세한 내용을 보려면 필터를 선택합니다 ![필터](../assets/ui/monitor-destinations/filter-add.png) 데이터 흐름 실행 시작 시간 옆의 데이터 흐름 실행 세부 정보 페이지를 확인합니다.

![데이터 흐름은 모니터링 대시보드에서 필터를 실행합니다](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### 데이터 흐름 실행 세부 정보 페이지 {#dataflow-run-details-page}

데이터 흐름 실행 세부 정보 페이지에 데이터 흐름 실행 목록에 표시된 세부 정보 외에 데이터 흐름 세부 정보가 표시됩니다.

- **[!UICONTROL 데이터 흐름 실행 ID]**: 데이터 흐름의 ID입니다.
- **[!UICONTROL IMS 조직 ID]**: 데이터 흐름이 속한 IMS 조직입니다.
- **[!UICONTROL 마지막 업데이트 날짜]**: 데이터 흐름 실행이 마지막으로 업데이트된 시간입니다.

또한 세부 사항 페이지에 데이터 흐름 실행 오류와 세그먼트 간을 전환할 수 있는 토글이 있습니다. 이 옵션은 일괄 처리 대상에서 데이터 흐름 실행에만 사용할 수 있습니다.

데이터 흐름 실행 오류 보기에는 실패한 ID 목록과 제외된 ID가 표시됩니다. 오류 코드, ID 수 및 설명을 포함하여 실패한 ID와 제외된 ID에 대한 정보가 표시됩니다. 기본적으로 목록에 실패한 ID가 표시됩니다. 건너뛴 ID를 표시하려면 **[!UICONTROL 제외된 ID]** 토글.

![제외된 ID 전환](../assets/ui/monitor-destinations/identities-excluded.png)

When **[!UICONTROL 세그먼트]** 이 선택되면 선택한 데이터 흐름 실행에서 활성화된 세그먼트 목록이 표시됩니다. 이 화면에는 활성화된 ID와 제외된 ID에 대한 세그먼트 수준 정보와 마지막 데이터 흐름 실행 상태 및 시간이 포함됩니다.

![데이터 흐름 실행 - 세그먼트 보기](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## 다음 단계 {#next-steps}

이제 이 안내서를 통해 처리 시간, 활성화 비율 및 상태와 같은 모든 관련 정보를 포함하여 일괄 처리 및 스트리밍 대상 모두에 대한 데이터 흐름을 모니터링하는 방법을 알 수 있습니다. Platform의 데이터 플로우에 대한 자세한 내용은 [데이터 흐름 개요](../home.md). 대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).