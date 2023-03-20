---
keywords: Experience Platform;홈;인기 항목;계정 모니터링;데이터 흐름 모니터링;데이터 흐름
description: Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 소스 작업 영역에서 스트리밍 데이터 흐름을 모니터링하는 단계를 제공합니다.
title: UI에서 스트리밍 소스에 대한 데이터 흐름 모니터링
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# UI에서 스트리밍 소스에 대한 데이터 흐름 모니터링

이 튜토리얼에서는 다음을 사용하여 스트리밍 소스의 데이터 흐름을 모니터링하는 단계를 설명합니다 [!UICONTROL 소스] 작업 공간.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [데이터 흐름](../../../dataflows/home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 서로 다른 서비스 간에 구성되므로 소스 커넥터에서 대상 데이터 세트로 데이터를 [!DNL Identity] 및 [!DNL Profile], 및에 [!DNL Destinations].
   * [데이터 흐름 실행](../../notifications.md): 데이터 흐름 실행은 선택한 데이터 흐름의 빈도 구성에 따라 반복되는 예약된 작업입니다.
* [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 스트리밍 소스에 대한 데이터 흐름 모니터링

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

스트리밍 소스에 대한 기존 데이터 흐름을 보려면 **[!UICONTROL 데이터 흐름]** 상단 헤더에서

![카탈로그](../../images/tutorials/monitor-streaming/catalog.png)

다음 [!UICONTROL 데이터 흐름] 페이지에는 소스 데이터, 계정 이름 및 데이터 흐름 실행 상태에 대한 정보를 포함하여 조직의 기존 데이터 흐름 목록이 포함되어 있습니다.

보려는 데이터 흐름의 이름을 선택합니다.

![데이터 흐름](../../images/tutorials/monitor-streaming/dataflows.png)

다음 표에는 데이터 흐름 실행 상태에 대한 자세한 정보가 포함되어 있습니다.

| 상태 | 설명 |
| ------ | ----------- |
| 완료됨 | 다음 `Completed` 상태는 해당 데이터 흐름 실행에 대한 모든 레코드가 1시간 기간 내에 처리되었음을 나타냅니다. A `Completed` 상태는 여전히 데이터 흐름 실행에 오류를 포함할 수 있습니다. |
| 성공 | 다음 `Success` 상태는 해당 데이터 흐름 실행에 대한 모든 레코드가 1시간 기간 내에 처리되었으며 데이터 흐름 실행 중에 오류가 발생하지 않았음을 나타냅니다. |
| 처리 중 | 다음 `Processing` 상태는 데이터 흐름이 아직 활성화되지 않았음을 나타냅니다. 이 상태는 종종 새 데이터 흐름을 만든 후 즉시 발생합니다. |
| 오류 | 다음 `Error` 상태는 데이터 흐름의 활성화 프로세스가 중단되었음을 나타냅니다. |
| 실행 안 함 | 다음 `No runs` 상태는 데이터 흐름을 만들었지만 데이터 흐름 실행이 시작되지 않았음을 나타냅니다. |

다음 [!UICONTROL 데이터 흐름 활동] 페이지에 스트리밍 데이터 플로우에 대한 특정 정보가 표시됩니다. 위쪽 배너에는 선택한 날짜 범위에서 모든 스트리밍 데이터 흐름 실행에 대해 수집된 레코드 수와 실패한 레코드 수가 포함되어 있습니다.

![데이터 흐름 활동](../../images/tutorials/monitor-streaming/dataflow-activity.png)

기본적으로 표시되는 데이터에는 최근 7일의 수집 비율이 포함됩니다. 선택 **[!UICONTROL 최근 7일]** 를 눌러 표시되는 레코드의 시간대를 조정합니다.

대체 수집 시간 프레임에 대한 옵션을 제공하는 달력 팝업 창이 나타납니다. 이전 7일 또는 최근 30일에서 흐름 실행을 보도록 데이터 흐름 실행 시간 프레임을 구성할 수 있습니다. 또는 원하는 사용자 지정 시간대를 설정하도록 대화형 달력을 구성합니다. 완료되면 을 선택합니다 **[!UICONTROL 적용]**.

![달력](../../images/tutorials/monitor-streaming/calendar.png)

페이지 하단에는 흐름 실행당 받은 레코드, 수집된 레코드 수 및 실패한 레코드 수에 대한 정보가 표시됩니다. 각 흐름 실행은 시간별 창 내에 기록됩니다.

![데이터 흐름 실행](../../images/tutorials/monitor-streaming/dataflow-run.png)

### 데이터 흐름 실행 지표 {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="받은 레코드"
>abstract="받은 레코드 지표는 데이터 플로우에서 받은 총 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="수집된 레코드"
>abstract="수집된 레코드 지표는 데이터 레이크에 수집된 총 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="레코드 실패"
>abstract="실패한 레코드 지표는 데이터의 오류로 인해 데이터 레이크에 수집되지 않은 총 레코드 수를 나타냅니다."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="경고가 있는 레코드"
>abstract="경고가 있는 레코드는 맵 변환 경고와 함께 수집된 총 레코드 수를 나타냅니다. 모든 매퍼 변환 오류는 경고로 보고되며 부분적으로 수집된 행은 경고와 함께 성공적인 것으로 간주됩니다"
>text="Learn more in documentation"

각 개별 데이터 흐름 실행에는 다음 세부 정보가 표시됩니다.

* **[!UICONTROL 데이터 흐름 실행 시작]**: 데이터 흐름 실행이 시작된 시간입니다.
* **[!UICONTROL 처리 시간]**: 데이터 흐름을 처리하는 데 걸린 시간입니다.
* **[!UICONTROL 받은 레코드]**: 소스 커넥터에서 데이터 흐름에서 받은 총 레코드 수입니다.
* **[!UICONTROL 수집된 레코드]**: 에 수집된 총 레코드 수입니다. [!DNL Data Lake].
* **[!UICONTROL 경고가 있는 레코드]**: 수집된 경고가 있는 총 레코드 수입니다. 모든 매퍼 변환 오류는 경고로 보고되며 부분적으로 수집된 행은 다음과 같이 레이블이 지정됩니다 `success` 경고. **참고**: 경고가 있는 레코드 섭취를 지원하는 것은 스트리밍 소스에서만 사용할 수 있습니다.
* **[!UICONTROL 레코드 실패]**: 수집되지 않은 레코드 수입니다. [!DNL Data Lake] 데이터 오류로 인해 발생합니다.
* **[!UICONTROL 수집 비율]**: 에 수집된 레코드의 성공률 [!DNL Data Lake]. 이 지표는 다음과 같은 경우에 적용할 수 있습니다 [!UICONTROL 부분 수집] 이 활성화되어 있습니다.
* **[!UICONTROL 상태]**: 데이터 흐름의 상태를 나타냅니다. 둘 중 하나 [!UICONTROL 완료됨] 또는 [!UICONTROL 처리 중]. [!UICONTROL 완료됨] 는 해당 데이터 흐름 실행에 대한 모든 레코드가 1시간 기간 내에 처리되었음을 의미합니다. [!UICONTROL 처리 중] 은(는) 데이터 흐름 실행이 아직 완료되지 않았음을 의미합니다.

다음 [!UICONTROL 데이터 흐름 실행 개요] 페이지에 해당 데이터 흐름 실행 ID, target 데이터 세트 및 조직 ID와 같은 데이터 흐름에 대한 추가 정보가 포함되어 있습니다.

오류가 있는 흐름 실행에는 도 포함됩니다 [!UICONTROL 데이터 흐름 실행 오류] 실패한 총 레코드 수와 실행 오류를 일으킨 특정 오류를 표시하는 패널입니다.

![dataflow-run-overview](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### 경고가 있는 레코드 보기 {#warnings}

[!UICONTROL 경고가 있는 레코드] 흐름 실행 중에 발생한 매퍼 변환 경고 목록을 표시합니다. 부분적으로 수집된 행은 성공한 것으로 간주되며 매퍼 변환 오류가 발견된 경우 경고가 추가됩니다.

기본적으로 모든 매퍼 변환 오류는 다음과 같은 경우 제외하고 경고로 간주됩니다.

* 구문 오류
* 존재하지 않는 속성에 대한 참조
* XDM 데이터 유형이 일치하지 않습니다

오류 진단을 보려면 **[!UICONTROL 미리 보기 오류 진단]**.

![경고를 사용한 레코드](../../images/tutorials/monitor-streaming/records-with-warnings.png)

다음 [!UICONTROL 오류 진단 미리 보기] 창에서 데이터 흐름 실행에 대한 최대 100개의 오류 및/또는 경고를 미리 볼 수 있습니다. 여기에서 자세한 내용을 보려면 수집 실패 매니페스트를 다운로드할 수도 있습니다. [!DNL Data Access] API.

![진단](../../images/tutorials/monitor-streaming/diagnostics.png)

## 다음 단계

이 자습서를 따라 다음을 성공적으로 사용했습니다. [!UICONTROL 소스] 작업 공간을 사용하여 스트리밍 데이터 흐름을 모니터링하고 실패한 데이터 흐름을 발생시키는 오류를 식별할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [소스 개요](../../home.md)
* [데이터 흐름 개요](../../../dataflows/home.md)
