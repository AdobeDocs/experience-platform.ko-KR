---
keywords: Experience Platform;홈;인기 항목;데이터 흐름;데이터 흐름
solution: Experience Platform
title: UI에서 클라우드 스토리지 배치 커넥터에 대한 데이터 흐름 구성
topic-legacy: overview
type: Tutorial
description: 데이터 흐름(Dataflow)은 소스에서 플랫폼 데이터 집합으로 데이터를 검색하고 인제스트하는 예약된 작업입니다. 이 자습서에서는 클라우드 저장소 계정을 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 0%

---

# UI에서 클라우드 스토리지 일괄 연결에 대한 데이터 흐름 구성

데이터 흐름(Dataflow)은 소스의 데이터를 검색하여 [!DNL Platform] 데이터 세트로 인제스트하는 예약된 작업입니다. 이 자습서에서는 클라우드 저장소 계정을 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 튜토리얼을 사용하려면 이미 설정된 클라우드 스토리지 계정이 있어야 합니다. UI에서 다른 클라우드 저장소 계정을 만들기 위한 자습서 목록은 [소스 커넥터 개요](../../../../home.md)에서 찾을 수 있습니다.

### 지원되는 파일 형식

[!DNL Experience Platform] 외부 저장소에서 인제스트할 다음 파일 형식을 지원합니다.

* 구분 기호 구분 값(DSV):모든 단일 문자 값을 DSV 형식 데이터 파일에 대한 구분 기호로 사용할 수 있습니다.
* [!DNL JavaScript Object Notation] (JSON):JSON 형식 데이터 파일은 XDM과 호환되어야 합니다.
* [!DNL Apache Parquet]:쪽모이 세공 마룻바닥으로 된 데이터 파일은 XDM과 호환되어야 합니다.

## 데이터 선택

클라우드 스토리지 계정을 만든 후 **[!UICONTROL Select data]** 단계가 나타나 클라우드 스토리지 파일 계층 구조를 탐색할 수 있는 인터페이스를 제공합니다.

* 인터페이스의 왼쪽 부분은 클라우드 스토리지 파일과 디렉토리를 표시하는 디렉토리 브라우저입니다.
* 인터페이스의 오른쪽에서는 호환 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

![인터페이스](../../../../images/tutorials/dataflow/cloud-storage/batch/interface.png)

나열된 폴더를 선택하면 폴더 계층 구조를 더 깊은 폴더로 이동할 수 있습니다. 하나의 폴더를 선택하여 폴더의 모든 파일을 재귀적으로 인제스트할 수 있습니다. 전체 폴더를 인제스트할 때 폴더의 모든 파일이 동일한 스키마를 공유하는지 확인해야 합니다.

호환되는 파일 또는 폴더를 선택한 후에는 [!UICONTROL Select data format] 드롭다운 메뉴에서 해당 데이터 형식을 선택합니다.

다음 표에는 지원되는 파일 유형에 적합한 데이터 형식이 표시됩니다.

| 파일 유형 | 데이터 형식 |
| --- | --- |
| CSV로 내보내기 | [!UICONTROL Delimited] |
| JSON | [!UICONTROL JSON] |
| 쪽모이 세공 | [!UICONTROL XDM Parquet] |

**[!UICONTROL JSON]**&#x200B;을 선택하고 미리 보기 인터페이스가 채워질 때까지 몇 초 동안 기다립니다.

![select-data](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

>[!NOTE]
>
>구분된 파일 유형 및 JSON 파일 형식과 달리, 미리 보기에서는 쪽모이 세공 문서 형식 파일을 사용할 수 없습니다.

미리 보기 인터페이스를 사용하면 파일의 내용 및 구조를 검사할 수 있습니다. 기본적으로 미리 보기 인터페이스는 선택한 폴더의 첫 번째 파일을 표시합니다.

다른 파일을 미리 보려면 검사할 파일 이름 옆에 있는 미리 보기 아이콘을 선택합니다.

![default-preview](../../../../images/tutorials/dataflow/cloud-storage/batch/default-preview.png)

폴더에 있는 파일의 내용과 구조를 검사했으면 **[!UICONTROL Next]**&#x200B;을 선택하여 폴더에 있는 모든 파일을 재귀적으로 인제스트합니다.

![select-folder](../../../../images/tutorials/dataflow/cloud-storage/batch/select-folder.png)

특정 파일을 선택하려면 인제스트할 파일을 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![select-file](../../../../images/tutorials/dataflow/cloud-storage/batch/select-file.png)

### 구분된 파일에 대한 사용자 정의 구분 기호 설정

구분된 파일을 인제스트할 때 사용자 지정 구분 기호를 설정할 수 있습니다. **[!UICONTROL Delimiter]** 옵션을 선택한 다음 드롭다운 메뉴에서 구분 기호를 선택합니다. 메뉴는 쉼표(`,`), 탭(`\t`) 및 파이프(`|`)를 포함하여 구분 기호에 가장 자주 사용되는 옵션을 표시합니다. 사용자 정의 구분 기호를 사용하려면 **[!UICONTROL Custom]**&#x200B;을 선택하고 팝업 입력 막대에서 원하는 단일 문자 구분 기호를 입력합니다.

데이터 형식을 선택하고 구분 기호를 설정한 후 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

## 데이터 필드를 XDM 스키마에 매핑

소스 데이터를 [!DNL Platform] 데이터 세트에 매핑하기 위한 대화형 인터페이스를 제공하는 **[!UICONTROL Mapping]** 단계가 나타납니다. Parameter에서 형식이 지정된 소스 파일은 XDM과 호환되어야 하며 수동으로 매핑을 구성할 필요가 없습니다. CSV 파일을 사용하려면 매핑을 명시적으로 구성해야 하지만 매핑할 소스 데이터 필드를 선택할 수 있어야 합니다. XDM 불만 사항으로 표시된 JSON 파일은 수동 구성이 필요하지 않습니다. 그러나 XDM 규격으로 표시되지 않으면 매핑을 명시적으로 구성해야 합니다.

수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 집합을 사용하거나 새 데이터 집합을 만들 수 있습니다.

**기존 데이터 세트 사용**

데이터를 기존 데이터 세트에 인제스트하려면 **[!UICONTROL Existing dataset]**&#x200B;을 선택한 다음 데이터 세트 아이콘을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

**[!UICONTROL Select dataset]** 대화 상자가 나타납니다. 사용할 데이터 세트를 찾아 선택한 다음 **[!UICONTROL Continue]**&#x200B;을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**새 데이터 세트 사용**

데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL New dataset]**&#x200B;을 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 스키마를 추가하려면 **[!UICONTROL Select schema]** 대화 상자에 기존 스키마 이름을 입력할 수 있습니다. 또는 **[!UICONTROL Schema advanced search]**&#x200B;을 선택하여 적절한 스키마를 검색할 수 있습니다.

이 단계 동안 데이터 세트에 [!DNL Real-time Customer Profile]을(를) 사용할 수 있도록 하고 엔티티의 속성 및 행동을 전체적으로 볼 수 있습니다. 활성화된 모든 데이터 집합의 데이터는 [!DNL Profile]에 포함되며 데이터 흐름을 저장할 때 변경 내용이 적용됩니다.

**[!UICONTROL Profile dataset]** 단추를 전환하여 [!DNL Profile]에 대한 대상 데이터 세트를 활성화합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

**[!UICONTROL Select schema]** 대화 상자가 나타납니다. 새 데이터 세트에 적용할 스키마를 선택한 다음 **[!UICONTROL Done]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

필요에 따라 필드를 직접 매핑하거나 매퍼 함수를 사용하여 계산된 값 또는 계산된 값을 파생하도록 소스 데이터를 변형할 수 있습니다. 데이터 매핑 및 매퍼 함수에 대한 자세한 내용은 [CSV 데이터를 XDM 스키마 필드](../../../../../ingestion/tutorials/map-a-csv-file.md)에 매핑하기 튜토리얼을 참조하십시오.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

JSON 파일의 경우 필드를 다른 필드에 직접 매핑하는 것 외에도 개체를 다른 개체 및 배열에 직접 매핑할 수 있습니다. 또한 클라우드 스토리지 소스 커넥터를 사용하여 JSON 파일의 배열과 같은 복잡한 데이터 유형을 미리 보고 매핑할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

서로 다른 유형으로는 매핑할 수 없습니다. 예를 들어 객체를 배열에 매핑하거나 필드를 객체에 매핑할 수 없습니다.

>[!TIP]
>
>[!DNL Platform] 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑 필드에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

선택한 데이터 세트에서 최대 100개의 샘플 데이터 행 매핑 결과를 보려면 **[!UICONTROL Preview data]**&#x200B;을 선택합니다.

미리 보기 중에 ID 열은 매핑 결과를 확인할 때 필요한 주요 정보이므로 첫 번째 필드로 우선 순위가 지정됩니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

소스 데이터가 매핑되면 **[!UICONTROL Close]**&#x200B;을 선택합니다.

## 통합 실행 예약

**[!UICONTROL Scheduling]** 단계가 나타나 구성된 매핑을 사용하여 선택한 소스 데이터를 자동으로 인제스트하도록 통합 일정을 구성할 수 있습니다. 다음 표에서는 스케줄링에 대해 다른 구성 가능한 필드에 대해 설명합니다.

| 필드 | 설명 |
| --- | --- |
| 빈도 | 선택 가능한 주파수는 `Once`, `Minute`, `Hour`, `Day` 및 `Week`입니다. |
| 간격 | 선택한 주파수의 간격을 설정하는 정수입니다. |
| 시작 시간 | 첫 번째 수집이 발생하도록 설정된 시기를 나타내는 UTC 타임스탬프. |
| 채우기 | 처음에 인제스트할 데이터를 결정하는 부울 값입니다. **[!UICONTROL Backfill]**&#x200B;이(가) 활성화되어 있으면, 지정된 경로의 현재 파일이 처음 예약된 수집 중에 모두 수집됩니다. **[!UICONTROL Backfill]**&#x200B;이(가) 비활성화된 경우 처음 통합 실행과 시작 시간 사이에 로드된 파일만 인제스트됩니다. 시작 시간 전에 로드된 파일은 인제스트되지 않습니다. |

데이터 흐름 기능은 예약된 시간에 자동으로 데이터를 인제스트하도록 디자인되었습니다. 섭취 빈도를 선택하여 시작합니다. 그런 다음 두 흐름 실행 사이의 기간을 지정하는 간격을 설정합니다. 간격의 값은 0이 아닌 정수여야 하며 15보다 크거나 같도록 설정해야 합니다.

통합 시작 시간을 설정하려면 시작 시간 상자에 표시된 날짜와 시간을 조정합니다. 또는 달력 아이콘을 선택하여 시작 시간 값을 편집할 수 있습니다. 시작 시간은 UTC의 현재 시간보다 크거나 같아야 합니다.

일정 값을 입력하고 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### 일회성 데이터 흐름 설정

1회 통합 설정을 하려면 빈도 드롭다운 화살표를 선택하고 **[!UICONTROL Once]**&#x200B;을 선택합니다. 시작 시간이 앞으로 남아 있는 한 1회 빈도 수집에 대해 데이터 흐름 세트를 계속 편집할 수 있습니다. 시작 시간이 지나면 1회 빈도 값을 더 이상 편집할 수 없습니다. **[!UICONTROL Interval]** 일회성 데이터 흐름 **[!UICONTROL Backfill]** 을 설정할 때는 표시되지 않습니다.

>[!IMPORTANT]
>
>[FTP 커넥터](../../../../connectors/cloud-storage/ftp.md)을(를) 사용할 때는 데이터 흐름을 1회 수집하도록 예약하는 것이 좋습니다.

일정에 적절한 값을 제공했으면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## 데이터 흐름 세부 정보 제공

**[!UICONTROL Dataflow detail]** 단계가 나타나 새 데이터 흐름 이름을 지정하고 간단한 설명을 제공할 수 있습니다.

이 프로세스 동안 **[!UICONTROL Partial ingestion]** 및 **[!UICONTROL Error diagnostics]**&#x200B;을(를) 활성화할 수도 있습니다. **[!UICONTROL Partial ingestion]**&#x200B;을 활성화하면 사용자가 설정할 수 있는 특정 임계값까지 오류가 포함된 데이터를 인제스트할 수 있습니다. **[!UICONTROL Error diagnostics]**&#x200B;을(를) 활성화하면 별도로 묶인 잘못된 데이터에 대한 세부 정보가 제공됩니다. 자세한 내용은 [부분 일괄 처리 통합 개요](../../../../../ingestion/batch-ingestion/partial.md)를 참조하십시오.

데이터 흐름 값을 입력하고 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## 데이터 흐름 검토

**[!UICONTROL Review]** 단계가 나타나 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

* **[!UICONTROL Connection]**:소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 양을 표시합니다.
* **[!UICONTROL Assign dataset & map fields]**:데이터 세트가 준수하는 스키마를 포함하여 원본 데이터를 수집할 데이터 집합을 표시합니다.
* **[!UICONTROL Scheduling]**:통합 일정의 활성 기간, 빈도 및 간격을 표시합니다.

데이터 흐름을 검토했으면 **[!UICONTROL Finish]**&#x200B;을(를) 클릭하고 데이터 흐름을 만들 시간을 잠시 기다립니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## 데이터 흐름 모니터링

데이터 흐름 기능이 만들어지면 데이터 수집이 처리되는 데이터를 모니터링하여 데이터 수집률, 성공 및 오류에 대한 정보를 확인할 수 있습니다. 데이터 흐름 모니터링 방법에 대한 자세한 내용은 UI](../../monitor.md)의 [모니터링 계정 및 데이터 흐름 관련 자습서를 참조하십시오.

## 데이터 흐름 삭제

**[!UICONTROL Dataflows]** 작업 영역에서 사용할 수 있는 **[!UICONTROL Delete]** 함수를 사용하여 더 이상 필요하지 않거나 잘못 만들어진 데이터 흐름을 삭제할 수 있습니다. 데이터 흐름 삭제 방법에 대한 자세한 내용은 UI](../../delete.md)에서 데이터 흐름 삭제의 자습서를 참조하십시오.[

## 다음 단계

이 튜토리얼을 따라 데이터 흐름을 만들어 외부 클라우드 스토리지에서 데이터를 가져오고 데이터 집합 모니터링에 대한 통찰력을 얻었습니다. 데이터 흐름 만들기에 대한 자세한 내용을 보려면 아래 비디오를 시청하여 학습 내용을 보완할 수 있습니다. 또한 이제 수신 데이터를 [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace] 등의 다운스트림 [!DNL Platform] 서비스에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 다음 비디오에 표시된 [!DNL Platform] UI가 최신 상태가 아닙니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## 부록

다음 섹션에서는 소스 커넥터 작업에 대한 추가 정보를 제공합니다.

### 데이터 흐름 비활성화

데이터 흐름을 만들면 즉시 활성 상태가 되어 지정된 일정에 따라 데이터를 인제스트합니다. 아래 지침에 따라 언제든지 활성 데이터 흐름을 비활성화할 수 있습니다.

**[!UICONTROL Sources]** 작업 영역에서 **[!UICONTROL Browse]** 탭을 클릭합니다. 그런 다음 비활성화할 활성 데이터 프롤에 연결된 계정 이름을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

**[!UICONTROL Source activity]** 페이지가 나타납니다. 목록에서 활성 데이터 흐름을 선택하여 화면 오른쪽의 **[!UICONTROL Properties]** 열을 엽니다. 이 열에는 **[!UICONTROL Enabled]** 전환 단추가 있습니다. 토글을 클릭하여 데이터 흐름을 비활성화합니다. 데이터 흐름을 비활성화한 후 동일한 전환을 사용하여 데이터 흐름을 다시 활성화할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### [!DNL Profile] 모집단용 인바운드 데이터 활성화

소스 커넥터의 인바운드 데이터를 사용하여 [!DNL Real-time Customer Profile] 데이터를 누름 및 채울 수 있습니다. [!DNL Real-time Customer Profile] 데이터를 채우는 방법에 대한 자세한 내용은 [프로필 채우기](../../profile.md)에 대한 자습서를 참조하십시오.
