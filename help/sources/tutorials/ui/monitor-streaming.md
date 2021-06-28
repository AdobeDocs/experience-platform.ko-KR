---
keywords: Experience Platform;홈;인기 항목;계정 모니터링;데이터 흐름 모니터링;데이터 흐름
description: Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 소스 작업 영역에서 스트리밍 데이터 흐름을 모니터링하는 단계를 제공합니다.
solution: Experience Platform
title: UI에서 스트리밍 소스에 대한 데이터 흐름 모니터링
topic-legacy: overview
type: Tutorial
source-git-commit: 58761cbe8465f4a00f07f33f751f481d34493cf7
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---


# UI에서 스트리밍 소스에 대한 데이터 흐름 모니터링

이 자습서에서는 [!UICONTROL 소스] 작업 공간을 사용하여 스트리밍 소스에 대한 데이터 흐름을 모니터링하는 단계를 설명합니다.

## 시작

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [데이터 흐름](../../../dataflows/home.md):데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 서로 다른 서비스에 구성되어 있어 소스 커넥터에서 대상 데이터 세트로 데이터를 [!DNL Identity] 및 [!DNL Profile] 로 이동하고 [!DNL Destinations] 로 이동하는 데 도움이 됩니다.
   * [데이터 흐름 실행](../../notifications.md):데이터 흐름 실행은 선택한 데이터 흐름의 빈도 구성에 따라 반복되는 예약된 작업입니다.
* [소스](../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 스트리밍 소스에 대한 데이터 흐름 모니터링

플랫폼 UI의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 공간에 액세스합니다. [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

스트리밍 소스에 대한 기존 데이터 흐름을 보려면 맨 위 헤더에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하십시오.

![카탈로그](../../images/tutorials/monitor-streaming/catalog.png)

[!UICONTROL 데이터 흐름] 페이지에는 소스 데이터, 계정 이름 및 데이터 흐름 실행 상태에 대한 정보를 포함하여 조직의 기존 데이터 흐름 목록이 포함되어 있습니다.

보려는 데이터 흐름의 이름을 선택합니다.

![데이터 흐름](../../images/tutorials/monitor-streaming/dataflows.png)

다음 표에는 데이터 흐름 실행 상태에 대한 자세한 정보가 포함되어 있습니다.

| 상태 | 설명 |
| ------ | ----------- |
| 완료됨 | `Completed` 상태는 해당 데이터 흐름 실행에 대한 모든 레코드가 1시간 기간 내에 처리되었음을 나타냅니다. 데이터 흐름 실행에서 `Completed` 상태에 여전히 오류가 있을 수 있습니다. |
| 처리 중 | `Processing` 상태는 데이터 흐름이 아직 활성 상태가 아님을 나타냅니다. 이 상태는 종종 새 데이터 흐름을 만든 후 즉시 발생합니다. |
| 오류 | `Error` 상태는 데이터 흐름의 활성화 프로세스가 중단되었음을 나타냅니다. |

[!UICONTROL 데이터 흐름 활동] 페이지에는 스트리밍 데이터 플로우에 대한 특정 정보가 표시됩니다. 위쪽 배너에는 선택한 날짜 범위에서 모든 스트리밍 데이터 흐름 실행에 대해 수집된 레코드 수와 실패한 레코드 수가 포함되어 있습니다.

페이지 하단에는 흐름 실행당 받은 레코드, 수집된 레코드 수 및 실패한 레코드 수에 대한 정보가 표시됩니다. 각 흐름 실행은 시간별 창 내에 기록됩니다.

![데이터 흐름 활동](../../images/tutorials/monitor-streaming/dataflow-activity.png)

각 개별 데이터 흐름 실행에는 다음 세부 정보가 표시됩니다.

* **[!UICONTROL 데이터 흐름 실행 시작]**:데이터 흐름 실행이 시작된 시간입니다.
* **[!UICONTROL 처리 시간]**:데이터 흐름을 처리하는 데 걸린 시간입니다.
* **[!UICONTROL 받은 레코드]**:소스 커넥터에서 데이터 흐름에서 받은 총 레코드 수입니다.
* **[!UICONTROL 수집된 레코드]**:에 수집된 총 레코드 수입니다 [!DNL Data Lake].
* **[!UICONTROL 레코드 실패]**:데이터 오류로  [!DNL Data Lake] 인해 수집되지 않은 레코드 수입니다.
* **[!UICONTROL 수집 비율]**:에 수집된 레코드의 성공률  [!DNL Data Lake]. 이 지표는 [!UICONTROL 부분 수집]이 활성화되어 있을 때 적용할 수 있습니다.
* **[!UICONTROL 상태]**:데이터 흐름의 상태를 나타냅니다.완료   또는  [!UICONTROL 처리 중].  완료됨 은 해당 데이터 흐름 실행에 대한 모든 레코드가 1시간 기간 내에 처리되었음을 의미합니다.  처리란 데이터 흐름 실행이 아직 완료되지 않았음을 의미합니다.

기본적으로 표시되는 데이터에는 최근 7일의 수집 비율이 포함됩니다. **[!UICONTROL 최근 7일]**&#x200B;을 선택하여 표시된 레코드의 시간대를 조정합니다.

![변경 시간](../../images/tutorials/monitor-streaming/change-time.png)

대체 수집 시간 프레임에 대한 옵션을 제공하는 달력 팝업 창이 나타납니다. **[!UICONTROL 최근 30일]**&#x200B;을 선택한 다음 **[!UICONTROL 적용]**&#x200B;을 선택합니다.

![달력](../../images/tutorials/monitor-streaming/calendar.png)

오류를 포함하여 특정 데이터 흐름 실행에 대한 세부 정보를 보려면 목록에서 실행 시작 시간을 선택합니다.

![select-fail](../../images/tutorials/monitor-streaming/select-fail.png)

[!UICONTROL 데이터 흐름 실행 개요] 페이지에는 해당 데이터 흐름 실행 ID, 대상 데이터 세트 및 IMS 조직 ID와 같은 데이터 로드에 대한 추가 정보가 포함되어 있습니다.

오류가 있는 흐름 실행에는 [!UICONTROL 데이터 흐름 실행 오류] 패널도 포함되어 있습니다. 이 패널에는 실행 실패로 이어지는 특정 오류와 실패한 총 레코드 수가 표시됩니다.

![실패](../../images/tutorials/monitor-streaming/failure.png)

## 다음 단계

이 자습서를 따라 [!UICONTROL 소스] 작업 공간을 사용하여 스트리밍 데이터 흐름을 모니터링하고 실패한 데이터 흐름이 발생한 오류를 식별했습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [소스 개요](../../home.md)
* [데이터 흐름 개요](../../../dataflows/home.md)