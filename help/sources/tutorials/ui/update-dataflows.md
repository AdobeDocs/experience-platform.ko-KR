---
keywords: Experience Platform;홈;인기 있는 항목;데이터 흐름 업데이트;편집 일정
description: 이 자습서에서는 소스 작업 영역을 사용하여 데이터 흐름 빈도 및 간격 속도를 포함하여 데이터 흐름 예약을 업데이트하는 단계를 설명합니다.
solution: Experience Platform
title: UI에서 소스 연결 데이터 흐름 업데이트
topic: 개요
type: Tutorial
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
translation-type: tm+mt
source-git-commit: 3a36996b43760bc9161b8d4750a1121e9ada8d30
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# UI에서 데이터 흐름 업데이트

이 자습서에서는 [!UICONTROL Sources] 작업 영역을 사용하여 데이터 흐름 예약 및 매핑 편집에 대한 정보를 포함하여 기존 소스 데이터 흐름을 업데이트하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [소스](../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
- [샌드박스](../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 매핑 편집

>[!NOTE]
>
>편집 매핑 기능은 현재 다음 소스에서 지원되지 않습니다.Adobe Analytics, Adobe Audience Manager, HTTP API 및 [!DNL Marketo Engage].

플랫폼 UI의 왼쪽 탐색 메뉴에서 **[!UICONTROL Sources]**&#x200B;을 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. 기존 데이터 흐름 목록을 보려면 상단 헤더에서 **[!UICONTROL Dataflows]**&#x200B;을 선택합니다.

![카탈로그](../../images/tutorials/update-dataflows/catalog.png)

[!UICONTROL Dataflows] 페이지에는 실행 상태, 마지막 실행 날짜 및 계정 이름에 대한 정보를 포함하여 모든 기존 데이터 흐름 목록이 포함되어 있습니다.

정렬 패널을 시작하려면 왼쪽 상단에 있는 필터 아이콘 ![필터](../../images/tutorials/update/filter.png)를 선택합니다.

![필터 데이터 흐름](../../images/tutorials/update-dataflows/filter-dataflows.png)

정렬 패널은 사용 가능한 모든 소스 목록을 제공합니다. 목록에서 둘 이상의 소스를 선택하여 다른 소스에 속하는 필터링된 데이터 흐름 선택 항목에 액세스할 수 있습니다.

작업할 소스를 선택하여 기존 데이터 흐름 목록을 확인합니다. 업데이트할 데이터 흐름을 식별한 후 계정 이름 옆에 있는 줄임표(`...`)를 선택합니다.

![편집 소스](../../images/tutorials/update-dataflows/edit-source.png)

선택한 데이터 흐름을 업데이트하는 옵션이 있는 드롭다운 메뉴가 나타납니다. 여기에서 데이터 흐름 매핑 세트와 통합 일정을 업데이트하도록 선택할 수 있습니다. 모니터링 대시보드에서 데이터 흐름을 검사할 옵션을 선택하고 데이터 흐름을 비활성화 또는 삭제할 수도 있습니다.

**[!UICONTROL Edit source]**&#x200B;을 선택하여 매핑을 업데이트합니다.

![edit-dataflow](../../images/tutorials/update-dataflows/edit-dataflow.png)

[!UICONTROL Add data] 단계가 나타납니다. 선택한 데이터의 내용을 검토할 적절한 데이터 형식을 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택하여 계속 진행합니다.

![add-data](../../images/tutorials/update-dataflows/add-data.png)

[!UICONTROL Mapping] 페이지는 데이터 세트와 관련된 매핑 세트를 추가하고 제거할 수 있는 인터페이스를 제공합니다.

>[!TIP]
>
>매핑 업데이트는 나중에 예약된 데이터 흐름 실행에 대해서만 적용됩니다.

새 매핑 세트를 추가하려면 **[!UICONTROL Add new mapping]**&#x200B;을 선택합니다.

![add-new-mapping](../../images/tutorials/update-dataflows/add-new-mapping.png)

그런 다음 적절한 소스 필드 속성과 대상 XDM 필드 값을 입력하여 추가 매핑 세트를 완료합니다. 계속하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![new-mapping-added](../../images/tutorials/update-dataflows/new-mapping-added.png)

[!UICONTROL Scheduling] 단계가 나타나 데이터 흐름 통합 일정을 업데이트하고 업데이트된 매핑으로 선택한 소스 데이터를 자동으로 인제스트할 수 있습니다.

>[!NOTE]
>
>일회성 인제기로 예약되고 시작 시간이 과거인 데이터 흐름 매핑 집합을 업데이트할 수 없습니다.

![예약](../../images/tutorials/update-dataflows/scheduling.png)

[!UICONTROL Dataflow detail] 페이지에서 데이터 플로의 업데이트된 이름과 설명을 제공할 수 있을 뿐만 아니라 데이터 플로의 오류 임계값을 다시 구성할 수 있습니다.

업데이트된 값을 제공했으면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![데이터 흐름 세부 정보](../../images/tutorials/update-dataflows/dataflow-detail.png)

**[!UICONTROL Review]** 단계가 나타나 데이터 흐름을 업데이트하기 전에 검토할 수 있습니다.

데이터 흐름을 검토했으면 **[!UICONTROL Finish]**&#x200B;을 선택하고 새 매핑 세트를 만들어 데이터 흐름 시간을 허용합니다.

![검토](../../images/tutorials/update-dataflows/review.png)

## 예약 편집

기존 데이터 흐름 통합 일정을 편집하려면 데이터 흐름 이름 옆에 있는 줄임표(`...`)를 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL Edit schedule]**&#x200B;을 선택합니다.

![편집 일정](../../images/tutorials/update-dataflows/edit-schedule.png)

**[!UICONTROL Edit schedule]** 대화 상자는 데이터 흐름 통합 빈도 및 간격 속도를 업데이트하는 옵션을 제공합니다. 업데이트된 빈도 및 간격 값을 설정한 후 **[!UICONTROL Save]**&#x200B;을 선택합니다.

>[!NOTE]
>
>1회 수집으로 예약된 데이터 프롤로는 다시 예약할 수 없습니다.

![schedule-dialog-box](../../images/tutorials/update-dataflows/schedule-dialog-box.png)

| 예약 | 설명 |
| ---------- | ----------- |
| 빈도 | 데이터 흐름 데이터가 수집되는 빈도. 이미 기존 데이터 플로우에 대한 주파수 예약을 편집할 수 있는 값은 다음과 같습니다.`minute`, `hour`, `day` 또는 `week`. |
| 간격 | 간격은 두 개의 연속 흐름 실행 사이의 기간을 지정합니다. 간격의 값은 0이 아닌 정수여야 하며 `15`보다 크거나 같아야 합니다. |

잠시 후 화면 하단에 확인 상자가 표시되어 성공적인 업데이트를 확인합니다.

![예약 확인](../../images/tutorials/update-dataflows/schedule-confirm.png)

## 다음 단계

이 튜토리얼을 따라 [!UICONTROL Sources] 작업 영역을 사용하여 데이터 흐름 통합 일정 및 매핑 세트를 업데이트했습니다.

[!DNL Flow Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 자세한 내용은 Flow Service API](../../tutorials/api/update-dataflows.md)를 사용하여 데이터 흐름 업데이트에 대한 자습서를 참조하십시오.[
