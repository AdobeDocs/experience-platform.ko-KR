---
title: 사용자 정의 대시보드
description: 맞춤형 위젯을 만들고, 추가하고, 편집하여 주요 지표를 시각화할 수 있는 사용자 정의 대시보드를 만들고 관리하는 방법을 알아봅니다.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: b3bd7a5ba1847518beafd12240c0d3a433a891d0
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 4%

---

# 사용자 정의 대시보드

Adobe Experience Platform 대시보드는 사용자 정의 대시보드 기능을 통해 통찰력을 신속하게 파악하고 시각화를 사용자 정의할 수 있도록 지원합니다. 이 기능을 사용하면 맞춤형 위젯을 만들고, 추가하고, 편집하여 조직과 관련된 주요 지표를 시각화할 수 있는 사용자 정의 대시보드를 작성하고 관리할 수 있습니다.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## 사용자 지정 대시보드 만들기

사용자 지정 대시보드를 만들려면 먼저 대시보드 인벤토리로 이동합니다. 선택 **[!UICONTROL 대시보드]** Platform UI의 왼쪽 탐색에서 **[!UICONTROL 대시보드 만들기]**.

![왼쪽 탐색 영역에 대시보드가 있고 &quot;대시보드 만들기&quot;가 강조 표시된 대시보드 인벤토리.](./images/user-defined-dashboards/create-dashboard.png)

사용자 정의 대시보드를 추가하기 전에 대시보드 인벤토리가 비어 있고 &quot;대시보드를 찾을 수 없음&quot;이 표시됩니다. 메시지. 대시보드가 생성되면 사용자 정의 대시보드가 모두 대시보드 인벤토리에 나열됩니다.

>[!NOTE]
>
>기존 대시보드를 편집하려면 인벤토리 목록에서 대시보드 이름을 선택한 다음 연필 아이콘(![연필 아이콘.](./images/user-defined-dashboards/edit-icon.png))

다음 [!UICONTROL 대시보드 만들기] 대화 상자가 나타납니다. 만들려는 위젯 컬렉션에 대해 사용자에게 친숙한 설명 이름을 입력하고 을(를) 선택합니다 **[!UICONTROL 저장]**.

![대시보드 만들기 대화 상자](./images/user-defined-dashboards/create-dashboard-dialog.png)

새로 생성된 빈 대시보드가 뷰의 왼쪽 상단 모서리에 선택한 이름과 함께 나타납니다.

## 위젯 만들기 {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="최대 위젯 수"
>abstract="사용자 정의 대시보드는 최대 10개의 위젯을 지원합니다. 10개의 위젯을 대시보드에 추가하면 [!UICONTROL 새 위젯 추가] 옵션이 비활성화되어 회색으로 표시됩니다."

새 대시보드 보기에서 을(를) 선택합니다 **[!UICONTROL 새 위젯 추가]** 을 클릭하여 위젯 만들기 프로세스를 시작합니다.

>[!IMPORTANT]
>
>사용자 정의 대시보드는 최대 10개의 위젯을 지원합니다. 10개의 위젯을 대시보드에 추가하면 [!UICONTROL 새 위젯 추가] 옵션이 비활성화되어 회색으로 표시됩니다.

![새 위젯 추가 가 강조 표시된 새 빈 대시보드.](./images/user-defined-dashboards/add-new-widget.png)

### 위젯 작성기

위젯 작성기 작업 영역이 나타납니다. 그런 다음 을 선택합니다. **[!UICONTROL 데이터 선택]** 위젯에 속성을 추가할 데이터 모델을 선택합니다.

![위젯 작성기 작업 영역.](./images/user-defined-dashboards/widget-composer.png)

#### 데이터 모델 선택 {#select-data-model}

다음 [!UICONTROL 데이터 모델 선택] 대화 상자가 나타납니다. 사용 가능한 모든 테이블의 미리보기 목록을 표시하려면 왼쪽 열에서 데이터 모델을 선택합니다. Real-time Customer Data Platform에 대해 사전 구성된 데이터 모델의 이름은 입니다 [!UICONTROL CDPInsights].

>[!TIP]
>
>정보 아이콘(![정보 아이콘](./images/user-defined-dashboards/info-icon.png)가) 너무 길어 데이터 레일에 표시할 수 없는 경우 전체 데이터 모델 이름을 표시합니다.

![데이터 선택 대화 상자](./images/user-defined-dashboards/select-data-model-dialog.png)

미리보기 목록은 데이터 모델에 포함된 테이블에 대한 세부 정보를 제공합니다. 아래 표에는 열 필드와 해당 잠재적 값에 대한 설명이 나와 있습니다.

| 열 필드 | 설명 |
|---|---|
| [!UICONTROL Title] | 테이블 이름. |
| [!UICONTROL 테이블 유형] | 테이블 유형. 잠재적 유형은 다음과 같습니다. `fact`, `dimension`, 및 `none`. |
| [!UICONTROL 레코드] | 선택한 테이블과 연결된 레코드 수입니다. |
| [!UICONTROL 조회] | 선택한 테이블에 연결된 테이블 수입니다. |
| [!UICONTROL 속성] | 선택한 테이블에 대한 속성의 수입니다. |

선택 **[!UICONTROL 다음]** 을 클릭하여 데이터 모델 선택을 확인합니다. 다음 보기는 왼쪽 레일에 사용 가능한 테이블 목록을 표시합니다. 선택한 테이블에 포함된 데이터에 대한 포괄적인 분류를 보려면 테이블을 선택합니다.

### 위젯 채우기 {#populate-widget}

다음 [!UICONTROL 미리 보기] 패널에 다음 탭이 포함됨: [!UICONTROL 샘플 레코드] 및 [!UICONTROL 속성]. 다음 [!UICONTROL 샘플 레코드] 탭은 테이블 보기에서 선택한 테이블의 레코드 하위 집합을 제공합니다. 다음 [!UICONTROL 속성] 탭은 선택한 테이블과 연관된 모든 속성에 대해 속성 이름, 데이터 유형 및 소스 테이블을 제공합니다.

위젯에 데이터를 제공할 왼쪽 레일의 목록에서 테이블을 선택하고 을 선택합니다. **[!UICONTROL 선택]** 을 클릭하여 위젯 작성기로 돌아갑니다.

![선택 이 강조 표시된 데이터 선택 대화 상자.](./images/user-defined-dashboards/select-a-table.png)

이제 위젯 작성기가 선택한 테이블의 데이터로 채워집니다.

데이터 모델과 현재 선택한 테이블이 왼쪽 레일의 맨 위에 표시되고 위젯을 만드는 데 사용할 수 있는 속성이에 나열되어 있습니다. [!UICONTROL 속성] 열. 목록을 스크롤하는 대신 검색 창을 사용하여 속성을 찾거나 연필 아이콘( )을 선택하여 선택한 데이터 모델을 변경할 수 있습니다.![연필 아이콘.](./images/user-defined-dashboards/edit-icon.png))을 클릭하여 왼쪽 레일에서 사용할 수 있습니다.

![위젯 작성기 내의 데이터로 채워진 위젯.](./images/user-defined-dashboards/populated-widget-composer.png)

#### 속성 추가 및 필터링 {#add-and-filter-attributes}

추가 아이콘(![추가 아이콘](./images/user-defined-dashboards/add-icon.png))을 클릭하여 위젯에 속성을 추가할 수 있습니다. 표시되는 드롭다운 메뉴를 사용하여 속성을 위젯의 X축, Y축, 색상 또는 필터 중 하나로 추가할 수 있습니다. 다음 [!UICONTROL 색상] 속성을 사용하면 색상을 기준으로 X 및 Y 축 표시의 결과를 구분할 수 있습니다. 이렇게 하려면 세 번째 속성의 구성에 따라 결과를 다른 색상으로 분할합니다.

>[!TIP]
>
>X축과 Y축의 배열을 전환하려면 위쪽 및 아래쪽 화살표 아이콘(![위쪽 및 아래쪽 화살표 아이콘](./images/user-defined-dashboards/switch-axis-icon.png))을 클릭하여 배열을 전환합니다.

![추가 아이콘 드롭다운이 강조 표시된 위젯 작성기입니다.](./images/user-defined-dashboards/attributes-dropdown.png)

위젯의 그래프 또는 차트 유형을 변경하려면 [!UICONTROL 표시] 드롭다운을 클릭하고 사용 가능한 옵션 중에서 선택합니다. 옵션에는 막대, 점, 틱, 선 또는 영역이 포함됩니다. 선택하면 위젯의 현재 설정에 대한 미리보기 시각화가 생성됩니다.

![표시 드롭다운이 강조 표시된 위젯 작성기입니다.](./images/user-defined-dashboards/marks-dropdown.png)

속성을 필터로 추가하여 위젯에서 포함하거나 제외할 값을 선택할 수 있습니다. 속성 목록에서 필터를 추가한 후 [!UICONTROL 필터] 확인란을 사용하여 값을 선택하거나 선택 취소할 수 있는 대화 상자가 나타납니다.

![위젯의 값을 필터링할 수 있는 필터 대화 상자입니다.](./images/user-defined-dashboards/filter-dialog.png)

#### 내역 데이터 필터링 {#filter-historical-data}

위젯으로 생성된 통찰력에서 내역 데이터를 필터링하려면 다음을 추가합니다. `date_key` 속성을 필터로 사용하고 선택 **[!UICONTROL 최근 일자]** 뒤에 오는 **[!UICONTROL 적용]**. 이 필터는 인사이트를 도출하는 데 사용되는 데이터를 최신 시스템 스냅샷에서 가져옵니다.

![다음 [!UICONTROL 필터: date_key] 대화 상자 [!UICONTROL 최근 일자] 및 [!UICONTROL 적용] 강조 표시됨.](./images/user-defined-dashboards/recent-date.png)

또는 사용자 지정 기간을 만들어 데이터를 필터링 기준으로 사용할 수 있습니다. 선택 **[!UICONTROL 날짜 선택]** 사용 가능한 날짜 목록으로 대화 상자를 확장합니다. 사용 **[!UICONTROL 모두 선택]** 확인란을 선택하여 사용 가능한 모든 옵션을 활성화 또는 비활성화하거나 각 날짜의 확인란을 개별적으로 선택합니다. 마지막으로 다음을 선택합니다. **[!UICONTROL 적용]** 을 클릭하여 선택 항목을 확인합니다.

>[!NOTE]
>
>다음과 같은 경우 `date_key` 속성이 이미 필터로 추가되었습니다. 줄임표를 선택한 다음 다음을 선택하십시오. **[!UICONTROL 편집]** 을 클릭하여 필터 기간을 변경합니다.

![다음 [!UICONTROL 필터: date_key] 일별 확인란이 선택되어 있고 선택 해제된 대화 상자](./images/user-defined-dashboards/select-dates.png)

### 위젯 속성

속성 아이콘(![속성 아이콘.](./images/user-defined-dashboards/properties-icon.png)) 오른쪽 레일에서 속성 패널을 엽니다. 다음에서 [!UICONTROL 속성] 패널에서 위젯의 이름을 [!UICONTROL 위젯 제목] 텍스트 필드.

![속성 아이콘과 위젯 제목 필드가 강조 표시된 속성 패널.](./images/user-defined-dashboards/properties-panel.png)

위젯 속성 패널에서 위젯의 여러 측면을 편집할 수 있습니다. 위젯 범례의 위치를 편집할 수 있는 완전한 제어 권한이 있습니다. 범례를 이동하려면 [!UICONTROL 범례 배치] 드롭다운을 클릭하고 사용 가능한 옵션 목록에서 원하는 위치를 선택합니다. 범례와 연관된 레이블의 이름을 바꿀 수도 있고, X축 또는 Y축에 새 이름을 입력할 수도 있습니다. [!UICONTROL 범례 제목] 텍스트 필드 또는 [!UICONTROL 축 레이블] 텍스트 필드 각각.

#### 위젯 저장 {#save-widget}

위젯 작성기에 저장하면 위젯이 대시보드에 로컬로 저장됩니다. 작업을 저장하고 나중에 다시 시작하려면 을 선택합니다. **[!UICONTROL 저장]**. 위젯 이름 아래에 있는 확인 표시 아이콘은 위젯이 저장되었음을 나타냅니다. 또는 위젯에 만족하면 을 선택합니다. **[!UICONTROL 저장 및 닫기]** 대시보드에 액세스할 수 있는 다른 모든 사용자가 위젯을 사용할 수 있도록 합니다. 선택 **[!UICONTROL 취소]** 작업을 포기하고 사용자 지정 대시보드로 돌아갑니다.

![새 위젯 저장 확인](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>속성 아이콘(![속성 아이콘.](./images/user-defined-dashboards/properties-icon.png))을 클릭하여 대시보드 이름 옆에 항목을 만들 수 있습니다. 표시되는 대화 상자에서 대시보드 이름을 변경할 수 있습니다.

이 작업 영역에 있는 동안 위젯을 다시 정렬하고 크기를 조정할 수 있습니다. 선택 **[!UICONTROL 저장]** 대시보드 이름과 구성된 레이아웃을 유지합니다.

![사용자 정의 위젯 및 저장 버튼이 강조 표시된 사용자 정의 대시보드.](./images/user-defined-dashboards/user-defined-dashboard.png)

Adobe Real-time Customer Data Platform 인사이트 대시보드에 대한 각 쿼리에 효율적으로 실행할 수 있는 리소스가 충분히 있는지 확인하기 위해 API는 각 쿼리에 동시 슬롯을 할당하여 리소스 사용을 추적합니다. 시스템은 최대 4개의 동시 쿼리를 처리할 수 있으므로 주어진 시간에 4개의 동시 쿼리 슬롯을 사용할 수 있습니다. 쿼리는 동시성 슬롯을 기반으로 대기열에 추가된 다음 충분한 동시성 슬롯을 사용할 수 있을 때까지 대기합니다.

### 위젯 복제

위젯을 만든 후에는 처음부터 새로 시작하지 않고도 전체 위젯을 복제하고 해당 속성을 사용자 정의하여 고유한 위젯을 만들 수 있습니다. 위젯을 복제하려면 먼저 대시보드 인벤토리로 이동합니다. 그런 다음 인벤토리 목록에서 대시보드 이름을 선택합니다. 맞춤화된 대시보드가 나타납니다.

![대시보드와 사용자 지정 대시보드 이름이 강조 표시된 Platform UI입니다.](./images/user-defined-dashboards/dashbaord-inventory.png)

연필 아이콘(![연필 아이콘.](./images/user-defined-dashboards/edit-icon.png))을 클릭하여 편집 모드로 전환할 수 있습니다.

![연필 아이콘이 강조 표시된 사용자 지정 대시보드.](./images/user-defined-dashboards/edit-mode.png)

그런 다음 복사할 위젯의 오른쪽 상단에서 생략 부호를 선택한 다음 을 선택합니다 **[!UICONTROL 복제]** 사용 가능한 옵션 목록에서.

![줄임표 및 중복 위젯이 강조 표시된 사용자 정의 대시보드의 위젯입니다.](./images/user-defined-dashboards/duplicate.png)

중복 위젯이 사용자 정의 대시보드에 나타납니다. 새 위젯의 생략 부호를 선택한 다음 **[!UICONTROL 편집]**: 새 위젯을 사용자 정의합니다.

## 다음 단계 및 추가 리소스

이 문서를 읽으면 사용자 정의 대시보드를 만드는 방법과 해당 대시보드에 대한 사용자 정의 위젯을 만들고, 편집하고, 업데이트하는 방법을 더 잘 이해할 수 있습니다.

에 대해 사용 가능한 사전 구성된 지표 및 시각화를 검색하려면 [프로필](./guides/profiles.md#standard-widgets), [세그먼트](./guides/audiences.md#standard-widgets), 및 [대상](./guides/destinations.md#standard-widgets) 대시보드의 각 설명서에서 표준 위젯 목록을 참조하십시오.

Experience Platform의 사용자 정의 대시보드에 대한 이해를 강화하려면 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
