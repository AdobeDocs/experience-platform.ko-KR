---
keywords: Experience Platform;홈;인기 항목;결제 커넥터;InDesign;home;popular topics;payment connector
solution: Experience Platform
title: UI에서 결제 소스 연결에 대한 데이터 흐름 구성
topic-legacy: overview
type: Tutorial
description: 데이터 흐름(Dataflow)은 소스에서 Adobe Experience Platform 데이터 세트로 데이터를 검색하고 인제스트하는 예약된 작업입니다. 이 자습서에서는 결제 계정을 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.
exl-id: 7355435b-c038-4310-b04a-8ac6b6723b9b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 0%

---

# UI에서 지불 연결에 대한 데이터 흐름 구성

데이터 흐름(Dataflow)은 소스에서 Adobe Experience Platform 데이터 세트로 데이터를 검색하고 인제스트하는 예약된 작업입니다. 이 자습서에서는 결제 계정을 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 자습서에서는 이미 결제 계정을 만들어야 합니다. UI에서 다른 지불 커넥터를 만들기 위한 자습서 목록은 [소스 커넥터 개요](../../../home.md)에서 찾을 수 있습니다.

## 데이터 선택

결제 계정을 만든 후, 파일 계층 구조를 탐색하기 위한 대화형 인터페이스를 제공하는 **[!UICONTROL Select data]** 단계가 나타납니다.

- 인터페이스의 왼쪽 절반은 서버 파일과 디렉토리를 표시하는 디렉토리 브라우저입니다.
- 인터페이스의 오른쪽 절반을 사용하면 호환 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

페이지 맨 위에 있는 **[!UICONTROL Search]** 옵션을 사용하여 사용할 소스 데이터를 빠르게 식별할 수 있습니다.

>[!NOTE]
>
>검색 소스 데이터 옵션은 Analytics, 분류, 이벤트 허브 및 Kinesis 커넥터를 제외한 모든 테이블 형식 기반 소스 커넥터에서 사용할 수 있습니다.

소스 데이터를 찾으면 디렉토리를 선택한 다음 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## 데이터 필드를 XDM 스키마에 매핑

소스 데이터를 [!DNL Platform] 데이터 세트에 매핑하기 위한 대화형 인터페이스를 제공하는 **[!UICONTROL Mapping]** 단계가 나타납니다.

수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 집합을 사용하거나 새 데이터 집합을 만들 수 있습니다.

### 기존 데이터 세트 사용

데이터를 기존 데이터 세트에 인제스트하려면 **[!UICONTROL Use existing dataset]**&#x200B;을 선택한 다음 데이터 세트 아이콘을 클릭합니다.

![use-existing-dataset](../../../images/tutorials/dataflow/payments/existing-dataset.png)

**[!UICONTROL Select dataset]** 대화 상자가 나타납니다. 사용할 데이터 세트를 찾아 선택한 다음 **[!UICONTROL Continue]**&#x200B;을 클릭합니다.

![select-existing-dataset](../../../images/tutorials/dataflow/payments/select-dataset.png)

### 새 데이터 세트 사용

데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL Create new dataset]**&#x200B;을 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다.

**[!UICONTROL Select schema]** 검색 막대에 스키마 이름을 입력하여 스키마 필드를 첨부할 수 있습니다. 드롭다운 아이콘을 선택하여 기존 스키마 목록을 볼 수도 있습니다. 또는 **[!UICONTROL Advanced search]**&#x200B;을 선택하여 해당 세부 정보를 포함한 기존 스키마의 화면에 액세스할 수 있습니다.

이 단계 동안 데이터 세트에 [!DNL Real-time Customer Profile]을(를) 사용할 수 있도록 하고 엔티티의 속성 및 행동을 전체적으로 볼 수 있습니다. 활성화된 모든 데이터 집합의 데이터는 [!DNL Profile]에 포함되며 데이터 흐름을 저장할 때 변경 내용이 적용됩니다.

**[!UICONTROL Profile dataset]** 단추를 전환하여 [!DNL Profile]에 대한 대상 데이터 세트를 활성화합니다.

![새로운 데이터 세트 만들기](../../../images/tutorials/dataflow/payments/new-dataset.png)

**[!UICONTROL Select schema]** 대화 상자가 나타납니다. 새 데이터 세트에 적용할 스키마를 선택한 다음 **[!UICONTROL Done]**&#x200B;을 클릭합니다.

![select-schema](../../../images/tutorials/dataflow/payments/select-schema.png)

필요에 따라 필드를 직접 매핑하거나 매퍼 함수를 사용하여 계산된 값 또는 계산된 값을 파생하도록 소스 데이터를 변형할 수 있습니다. 데이터 매핑 및 매퍼 함수에 대한 자세한 내용은 [CSV 데이터를 XDM 스키마 필드](../../../../ingestion/tutorials/map-a-csv-file.md)에 매핑하기 튜토리얼을 참조하십시오.

>[!TIP]
>
>[!DNL Platform] 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑 필드에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

![](../../../images/tutorials/dataflow/all-tabular/mapping.png)

선택한 데이터 세트에서 최대 100개의 샘플 데이터 행 매핑 결과를 보려면 **[!UICONTROL Preview data]**&#x200B;을 선택합니다.

미리 보기 중에 ID 열은 매핑 결과를 확인할 때 필요한 주요 정보이므로 첫 번째 필드로 우선 순위가 지정됩니다.

![](../../../images/tutorials/dataflow/all-tabular/mapping-preview.png)

소스 데이터가 매핑되면 **[!UICONTROL Close]**&#x200B;을 선택합니다.

## 통합 실행 예약

**[!UICONTROL Scheduling]** 단계가 나타나 구성된 매핑을 사용하여 선택한 소스 데이터를 자동으로 인제스트하도록 통합 일정을 구성할 수 있습니다. 다음 표에서는 스케줄링에 대해 다른 구성 가능한 필드에 대해 설명합니다.

| 필드 | 설명 |
| --- | --- |
| 빈도 | 선택 가능한 주파수는 `Once`, `Minute`, `Hour`, `Day` 및 `Week`입니다. |
| 간격 | 선택한 주파수의 간격을 설정하는 정수입니다. |
| 시작 시간 | 첫 번째 수집이 발생하도록 설정된 시기를 나타내는 UTC 타임스탬프. |
| 채우기 | 처음에 인제스트할 데이터를 결정하는 부울 값입니다. **[!UICONTROL Backfill]**&#x200B;이(가) 활성화되어 있으면, 지정된 경로의 현재 파일이 처음 예약된 수집 중에 모두 수집됩니다. **[!UICONTROL Backfill]**&#x200B;이(가) 비활성화된 경우 처음 통합 실행과 시작 시간 사이에 로드된 파일만 인제스트됩니다. 시작 시간 전에 로드된 파일은 인제스트되지 않습니다. |
| 델타 열 | 유형, 날짜 또는 시간의 소스 스키마 필드 필터링된 세트가 있는 옵션입니다. 이 필드는 새 데이터와 기존 데이터를 구분하는 데 사용됩니다. 선택한 열의 타임스탬프를 기반으로 증분 데이터를 인제스트합니다. |

데이터 흐름 기능은 예약된 시간에 자동으로 데이터를 인제스트하도록 디자인되었습니다. 섭취 빈도를 선택하여 시작합니다. 그런 다음 두 흐름 실행 사이의 기간을 지정하는 간격을 설정합니다. 간격의 값은 0이 아닌 정수여야 하며 15보다 크거나 같도록 설정해야 합니다.

통합 시작 시간을 설정하려면 시작 시간 상자에 표시된 날짜와 시간을 조정합니다. 또는 달력 아이콘을 선택하여 시작 시간 값을 편집할 수 있습니다. 시작 시간은 현재 UTC 시간보다 크거나 같아야 합니다.

델타 열을 지정하려면 **[!UICONTROL Load incremental data by]**&#x200B;을 선택합니다. 이 필드는 새 데이터와 기존 데이터를 구분합니다.

![](../../../images/tutorials/dataflow/databases/schedule-interval-on.png)

### 일회성 데이터 흐름 설정

1회 통합 설정을 하려면 빈도 드롭다운 화살표를 선택하고 **[!UICONTROL Once]**&#x200B;을 선택합니다.

>[!TIP]
>
>**[!UICONTROL Interval]** 일회성  **[!UICONTROL Backfill]** 섭취 중에는 표시되지 않습니다.

일정에 적절한 값을 제공했으면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../../../images/tutorials/dataflow/databases/schedule-once.png)

## 데이터 흐름 세부 정보 제공

**[!UICONTROL Dataflow detail]** 단계가 나타나 새 데이터 흐름 이름을 지정하고 간단한 설명을 제공할 수 있습니다.

이 프로세스 동안 **[!UICONTROL Partial ingestion]** 및 **[!UICONTROL Error diagnostics]**&#x200B;을(를) 활성화할 수도 있습니다. **[!UICONTROL Partial ingestion]**&#x200B;을(를) 활성화하면 특정 임계값까지 오류가 포함된 데이터를 인제스트할 수 있습니다. **[!UICONTROL Partial ingestion]**&#x200B;이(가) 활성화되면 **[!UICONTROL Error threshold %]** 다이얼을 드래그하여 일괄 처리의 오류 임계값을 조정합니다. 또는 입력 상자를 선택하여 임계값을 수동으로 조정할 수 있습니다. 자세한 내용은 [부분 일괄 처리 통합 개요](../../../../ingestion/batch-ingestion/partial.md)를 참조하십시오.

데이터 흐름 값을 입력하고 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![데이터 흐름 세부 정보](../../../images/tutorials/dataflow/all-tabular/dataflow-detail.png)

## 데이터 흐름 검토

**[!UICONTROL Review]** 단계가 나타나 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

- **[!UICONTROL Connection]**:소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 양을 표시합니다.
- **[!UICONTROL Assign dataset & map fields]**:데이터 세트가 준수하는 스키마를 포함하여 원본 데이터를 수집할 데이터 집합을 표시합니다.
- **[!UICONTROL Scheduling]**:통합 일정의 활성 기간, 빈도 및 간격을 표시합니다.

데이터 흐름을 검토했으면 **[!UICONTROL Finish]**&#x200B;을(를) 클릭하고 데이터 흐름을 만들 시간을 잠시 기다립니다.

![검토](../../../images/tutorials/dataflow/payments/review.png)

## 데이터 흐름 모니터링

데이터 흐름 기능이 만들어지면 데이터 수집이 처리되는 데이터를 모니터링하여 데이터 수집률, 성공 및 오류에 대한 정보를 확인할 수 있습니다. 데이터 흐름 모니터링 방법에 대한 자세한 내용은 UI](../monitor.md)의 [모니터링 계정 및 데이터 흐름 관련 자습서를 참조하십시오.

## 데이터 흐름 삭제

**[!UICONTROL Dataflows]** 작업 영역에서 사용할 수 있는 **[!UICONTROL Delete]** 함수를 사용하여 더 이상 필요하지 않거나 잘못 만들어진 데이터 흐름을 삭제할 수 있습니다. 데이터 흐름 삭제 방법에 대한 자세한 내용은 UI](../delete.md)에서 데이터 흐름 삭제의 자습서를 참조하십시오.[

## 다음 단계

이 자습서를 따라 마케팅 자동화 시스템에서 데이터를 가져오는 데이터 흐름을 성공적으로 제작하여 데이터 세트 모니터링에 대한 통찰력을 얻을 수 있습니다. 이제 [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace] 등의 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [[!DNL Real-time Customer Profile] 개요](../../../../profile/home.md)
- [[!DNL Data Science Workspace] 개요](../../../../data-science-workspace/home.md)

## 부록

다음 섹션에서는 소스 커넥터 작업에 대한 추가 정보를 제공합니다.

### 데이터 흐름 비활성화

데이터 흐름을 만들면 즉시 활성 상태가 되어 지정된 일정에 따라 데이터를 인제스트합니다. 아래 지침에 따라 언제든지 활성 데이터 흐름을 비활성화할 수 있습니다.

**[!UICONTROL Dataflows]** 화면에서 비활성화할 데이터 흐름 이름을 선택합니다.

![browse-dataset-flow](../../../images/tutorials/dataflow/payments/view-dataset-flows.png)

**[!UICONTROL Properties]** 열이 화면의 오른쪽에 나타납니다. 이 패널에는 **[!UICONTROL Enabled]** 전환 단추가 있습니다. 토글을 클릭하여 데이터 흐름을 비활성화합니다. 데이터 흐름을 비활성화한 후 동일한 전환을 사용하여 데이터 흐름을 다시 활성화할 수 있습니다.

![disable](../../../images/tutorials/dataflow/payments/disable.png)

### [!DNL Profile] 모집단용 인바운드 데이터 활성화

소스 커넥터의 인바운드 데이터를 사용하여 [!DNL Real-time Customer Profile] 데이터를 누름 및 채울 수 있습니다. [!DNL Real-time Customer Profile] 데이터를 채우는 방법에 대한 자세한 내용은 [프로필 채우기](../profile.md)에 대한 자습서를 참조하십시오.
