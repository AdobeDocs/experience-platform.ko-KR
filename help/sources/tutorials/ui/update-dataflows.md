---
description: Experience Platform UI에서 기존 소스 데이터 흐름을 업데이트하는 방법을 알아봅니다.
title: UI에서 Source 연결 데이터 흐름 업데이트
exl-id: 0499a2a3-5a22-47b1-ac0e-76a432bd26c0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 8%

---

# UI에서 데이터 흐름 업데이트

Adobe Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여 일정 및 매핑 구성을 포함하여 기존 데이터 흐름을 업데이트하는 방법에 대한 절차를 알려면 이 튜토리얼을 참조하십시오.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## 데이터 흐름 업데이트 {#update-dataflows}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflows_daysRemaining"
>title="데이터 세트 만료"
>abstract="이 열은 대상 데이터 세트가 자동으로 만료되기 전에 남은 일 수를 나타냅니다.<br>대상 데이터 세트가 만료되면 데이터 흐름이 실패합니다. 데이터 흐름이 실패하지 않도록 대상 데이터 세트가 올바른 날짜에 만료되도록 설정되었는지 확인하십시오. 만료 일자를 업데이트하는 방법은 설명서를 참조하십시오."

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택한 다음 상단 헤더에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택합니다.

![데이터 흐름 헤더 탭이 선택된 소스 카탈로그입니다.](../../images/tutorials/update-dataflows/catalog.png)

>[!TIP]
>
>필터링 기능을 사용하여 데이터 흐름을 정렬하고 필터링할 수 있습니다. 자세한 내용은 [UI의 원본 개체 필터링](./filter.md)에 대한 안내서를 참조하십시오.

[!UICONTROL 데이터 흐름] 페이지에 조직에 있는 기존의 모든 데이터 흐름의 목록이 표시됩니다. 업데이트할 데이터 흐름을 찾은 다음 그 옆에 있는 줄임표(`...`)를 선택합니다. 드롭다운 메뉴가 나타나고 기존 데이터 흐름을 추가로 구성하기 위해 선택할 수 있는 옵션 목록이 표시됩니다.

데이터 흐름을 업데이트하려면 **[!UICONTROL 데이터 흐름 업데이트]**&#x200B;를 선택하세요.

![데이터 흐름을 업데이트하는 옵션이 나열된 드롭다운 메뉴입니다.](../../images/tutorials/update-dataflows/dropdown_update.png)

[!UICONTROL 데이터 흐름 세부 정보 제공] 단계의 세부 정보를 포함하여 데이터 흐름의 측면을 업데이트할 수 있는 소스 워크플로우로 이동합니다.

### 매핑 업데이트 {#update-mapping}

>[!NOTE]
>
>Adobe Analytics, Adobe Audience Manager, HTTP API 및 [!DNL Marketo Engage] 소스에 대해서는 매핑 편집 기능이 현재 지원되지 않습니다.

이 프로세스 중에 데이터 흐름과 연결된 매핑 세트를 업데이트할 수도 있습니다.  매핑 인터페이스는 새 권장 매핑 세트가 아니라 데이터 흐름의 기존 매핑을 표시합니다. 매핑 업데이트는 향후 예약된 데이터 흐름 실행에만 적용됩니다. 일회성 수집으로 예약된 데이터 흐름에는 매핑 세트가 업데이트될 수 없습니다.

매핑 인터페이스를 사용하여 데이터 흐름에 적용되는 매핑 세트를 수정합니다. 매핑 인터페이스를 사용하는 방법에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../data-prep/ui/mapping.md)를 참조하십시오.

![소스 워크플로우의 매핑 단계입니다. 이 단계를 사용하여 데이터 흐름과 연결된 매핑을 업데이트합니다.](../../images/tutorials/update-dataflows/mapping.png)

### 일정 업데이트

데이터 흐름의 매핑을 업데이트한 후 수집 일정 업데이트를 계속 진행하여 데이터 흐름을 해당 새 매핑 데이터로 수집할 수 있습니다. 반복 일정에 따라 수집하도록 구성된 데이터 흐름의 수집 일정만 업데이트할 수 있습니다. 일회성 수집에 대해 구성된 데이터 흐름의 일정을 조정할 수 없습니다.

데이터 흐름 페이지에 제공된 인라인 업데이트 옵션을 사용하여 데이터 흐름의 수집 일정을 업데이트할 수도 있습니다.

데이터 흐름 페이지에서 데이터 흐름 이름 옆의 생략 부호(`...`)를 선택한 다음 나타나는 드롭다운 메뉴에서 **[!UICONTROL 일정 편집]**&#x200B;을(를) 선택합니다.

![원본 워크플로의 예약 단계입니다. 이 단계를 사용하여 데이터 흐름의 일정을 업데이트합니다.](../../images/tutorials/update-dataflows/dropdown_edit.png)

**[!UICONTROL 일정 편집]** 대화 상자에는 데이터 흐름의 수집 빈도 및 간격 비율을 업데이트하는 옵션이 있습니다. 업데이트된 빈도 및 간격 값을 설정한 후 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![데이터 흐름의 수집 일정을 편집하는 데 사용할 수 있는 팝업 창](../../images/tutorials/update-dataflows/edit_schedule.png)

### 데이터 흐름 비활성화

동일한 드롭다운 메뉴를 사용하여 데이터 흐름을 비활성화할 수 있습니다. 데이터 흐름을 사용하지 않으려면 **[!UICONTROL 데이터 흐름 사용 안 함]**&#x200B;을 선택하세요.

![데이터 흐름을 사용하지 않도록 설정하는 옵션이 있는 드롭다운 메뉴](../../images/tutorials/update-dataflows/dropdown_disable.png)

그런 다음 표시되는 팝업 창에서 [!UICONTROL 사용 안 함]을 선택합니다.

![데이터 흐름을 사용하지 않도록 설정할지 확인하는 팝업 창](../../images/tutorials/update-dataflows/disable_dataflow.png)

나중에 이 데이터 흐름을 다시 활성화하면 Experience Platform에서 데이터 흐름이 비활성화된 기간을 포함하도록 채우기 실행을 자동으로 예약합니다. 예를 들어 데이터 흐름이 시간별로 실행되도록 구성되어 48시간 동안 비활성화되어 있는 경우 이 데이터 흐름을 다시 활성화하면 Experience Platform에서 48개의 채우기 실행을 만들어 놓친 간격을 처리합니다.

## 다음 단계

이 자습서에 따라 [!UICONTROL 소스] 작업 영역을 사용하여 데이터 흐름의 수집 일정 및 매핑 세트를 업데이트했습니다.

[!DNL Flow Service] API를 사용하여 프로그래밍 방식으로 이러한 작업을 수행하는 방법에 대한 단계는 [흐름 서비스 API를 사용하여 데이터 흐름 업데이트](../../tutorials/api/update-dataflows.md)에 대한 자습서를 참조하십시오.
