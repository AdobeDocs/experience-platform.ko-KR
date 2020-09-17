---
keywords: Experience Platform;home;popular topics;dataflow;Dataflow
solution: Experience Platform
title: UI에서 클라우드 스토리지 배치 커넥터에 대한 데이터 흐름 구성
topic: overview
description: 데이터 흐름(Dataflow)은 소스에서 플랫폼 데이터 집합으로 데이터를 검색하고 인제스트하는 예약된 작업입니다. 이 자습서에서는 클라우드 저장소 계정을 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.
translation-type: tm+mt
source-git-commit: a4fd95904159a7b3e9c420f720a315641fd6706f
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---


# UI에서 클라우드 스토리지 배치 커넥터에 대한 데이터 흐름 구성

데이터 흐름(Dataflow)은 소스에서 데이터 세트로 데이터를 검색하고 인제스트하는 예약된 [!DNL Platform] 작업입니다. 이 자습서에서는 클라우드 저장소 계정을 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model] (XDM) 시스템](../../../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL 실시간 고객 프로필]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 튜토리얼을 사용하려면 기존 클라우드 스토리지 계정이 있어야 합니다. UI에서 다른 클라우드 스토리지 계정을 만들기 위한 자습서 목록은 [소스 커넥터 개요에 있습니다](../../../../home.md).

### 지원되는 파일 형식

[!DNL Experience Platform] 는 외부 저장소에서 인제스트할 다음 파일 형식을 지원합니다.

* 구분 기호 구분 값(DSV):DSV 형식 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다. DSV 형식 파일 내의 필드 헤더 값은 영숫자 및 밑줄로만 구성되어야 합니다. 일반 DSV 파일에 대한 지원이 나중에 제공될 예정입니다.
* [!DNL JavaScript Object Notation] (JSON):JSON 형식의 데이터 파일은 XDM과 호환되어야 합니다.
* [!DNL Apache Parquet]:쪽모이 세공된 데이터 파일은 XDM과 호환되어야 합니다.

## 데이터 선택

클라우드 스토리지 계정을 만든 후 **[!UICONTROL 데이터]** 선택 단계가 나타나며, 클라우드 스토리지 계층 구조를 탐색하는 데 필요한 대화형 인터페이스를 제공합니다.

* 인터페이스의 왼쪽 절반은 서버의 파일과 디렉토리를 표시하는 디렉토리 브라우저입니다.
* 인터페이스의 오른쪽 절반을 사용하면 호환 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

나열된 폴더를 선택하면 폴더 계층 구조를 더 깊은 폴더로 이동할 수 있습니다. 호환되는 파일 또는 폴더를 선택하면 **[!UICONTROL 데이터 형식]** 선택 드롭다운이 나타나며, 이 드롭다운에서 데이터를 미리 보기 창에 표시할 형식을 선택할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

미리 보기 창이 채워지면 **[!UICONTROL 다음을 선택하여]** 선택한 폴더 내의 모든 파일을 업로드할 수 있습니다. 특정 파일에 업로드하려면 다음을 선택하기 전에 목록에서 해당 파일을 **[!UICONTROL 선택합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-preview.png)

### 인제스트 쪽모이 세공 또는 JSON 파일

클라우드 스토리지 계정에 대해 지원되는 파일 형식에는 JSON 및 Parentoter도 포함되어 있습니다. JSON 및 Partiented 파일은 XDM과 호환되어야 합니다. JSON 또는 쪽모이 세공 마룻파일을 인제스트하려면 디렉토리 브라우저에서 해당 파일 포맷을 선택하고 올바른 인터페이스에서 호환 데이터 포맷을 적용합니다. 계속하려면 **[!UICONTROL 다음]** 을 선택합니다.

>[!IMPORTANT]
>
>구분된 파일 형식과는 달리 JSON 및 쪽모이 세공된 형식의 파일은 미리 볼 수 없습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## 데이터 필드를 XDM 스키마에 매핑

소스 데이터를 데이터 세트에 매핑하기 위한 대화형 인터페이스를 제공하는 **[!UICONTROL 매핑]** 단계가 [!DNL Platform] 나타납니다. JSON 또는 쪽모이 세공된 환경에서 포맷된 소스 파일은 XDM과 호환되어야 하며 매핑을 수동으로 구성할 필요가 없습니다. 반대로 CSV 파일은 매핑을 명시적으로 구성해야 하지만 매핑할 소스 데이터 필드를 선택할 수 있도록 합니다.

수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

**기존 데이터 세트 사용**

데이터를 기존 데이터 세트에 인제스트하려면 **[!UICONTROL 기존 데이터]**&#x200B;세트를 선택한 다음 데이터 세트 아이콘을 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

데이터 **[!UICONTROL 세트]** 선택 대화 상자가 나타납니다. 사용할 데이터 세트를 찾아 선택한 다음 **[!UICONTROL 계속을 클릭합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**새 데이터 집합 사용**

데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL 새 데이터]** 세트를 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 스키마를 추가하려면 스키마 **[!UICONTROL 선택 대화 상자에 기존 스키마 이름을]** 입력할 수 있습니다. 또는 **[!UICONTROL 스키마 고급 검색을 선택하여]** 적절한 스키마를 검색할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-dataset.png)

스키마 **[!UICONTROL 선택]** 대화 상자가 나타납니다. 새 데이터 세트에 적용할 스키마를 선택한 다음 완료를 **[!UICONTROL 선택합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

필요에 따라 필드를 직접 매핑하거나 매퍼 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 추출할 수 있습니다. 데이터 매핑 및 매퍼 함수에 대한 자세한 내용은 CSV 데이터를 XDM 스키마 필드에 [매핑하는 방법에 대한 자습서를 참조하십시오](../../../../../ingestion/tutorials/map-a-csv-file.md).

>[!TIP]
>
>[!DNL Platform] 선택한 대상 스키마나 데이터 세트에 따라 자동 매핑 필드에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

선택한 **[!UICONTROL 데이터]** 세트에서 최대 100개의 샘플 데이터 행의 매핑 결과를 보려면 [데이터 미리 보기]를 선택합니다.

미리 보기 중에 매핑 결과의 유효성을 확인할 때 필요한 주요 정보이므로 ID 열의 우선 순위가 첫 번째 필드로 지정됩니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

소스 데이터가 매핑되면 닫기를 **[!UICONTROL 선택합니다]**.

## 처리 실행 예약

예약 **** 단계가 나타나면서 구성된 매핑을 사용하여 선택한 소스 데이터를 자동으로 인제스트하도록 통합 예약을 구성할 수 있습니다. 다음 표에서는 예약을 위해 구성 가능한 여러 필드에 대해 설명합니다.

| 필드 | 설명 |
| --- | --- |
| 빈도 | 선택 가능한 주파수는 `Once`, `Minute``Hour`, `Day`및 `Week`있습니다. |
| 간격 | 선택한 주파수의 간격을 설정하는 정수입니다. |
| 시작 시간 | 첫 번째 인제스트 발생 시간을 나타내는 UTC 타임스탬프. |
| 채우기 | 처음에 수집되는 데이터를 결정하는 부울 값입니다. 채우기 **[!UICONTROL 가]** 활성화되어 있으면, 지정된 경로에 있는 모든 현재 파일이 첫 번째 예약된 수집 중에 수집됩니다. 채우기 **[!UICONTROL 를]** 비활성화하면 인제스트 첫 번째 실행과 **[!UICONTROL 시작 시간]** 사이에 로드되는 파일만 인제스트됩니다. 시작 **[!UICONTROL 시간]** 전에 로드된 파일은 인제스트되지 않습니다. |

데이터 프롤링은 일정에 따라 데이터를 자동으로 인제스트하도록 디자인되었습니다. 섭취 빈도를 선택하여 시작합니다. 그런 다음 간격을 설정하여 두 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 하며 15보다 크거나 같도록 설정해야 합니다.

섭취 시작 시간을 설정하려면 시작 시간 상자에 표시된 날짜와 시간을 조정합니다. 또는 달력 아이콘을 선택하여 시작 시간 값을 편집할 수 있습니다. 시작 시간은 UTC의 현재 시간보다 크거나 같아야 합니다.

일정에 대한 값을 제공하고 **[!UICONTROL 다음을 선택합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### 일회성 데이터 흐름 설정

1회 질문을 설정하려면 빈도 드롭다운 화살표를 선택하고 **[!UICONTROL 한 번]**&#x200B;선택합니다. 1회 주파수 섭취를 위해 데이터 흐름 세트를 계속 편집할 수 있으므로 시작 시간이 앞으로 남아 있을 수 있습니다. 시작 시간이 경과하면 1회 빈도 값을 더 이상 편집할 수 없습니다.

>[!TIP]
>
>**[!UICONTROL 일회성]** 섭취 **[!UICONTROL 중에는 간격]** 및 채우기 기능이 표시되지 않습니다.

일정에 적절한 값을 제공한 후 다음을 **[!UICONTROL 선택합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## 데이터 흐름 세부 정보 제공

데이터 **[!UICONTROL 흐름 세부]** 정보 단계가 나타나므로 새 데이터 흐름 이름에 대해 간단한 설명을 제공할 수 있습니다.

이 프로세스 동안 부분 섭취 및 **[!UICONTROL 오류 진단을]** 활성화할 수도 **[!UICONTROL 있습니다]**. 부분 **[!UICONTROL 섭취]** 활성화는 사용자가 설정할 수 있는 특정 임계값까지 오류가 포함된 데이터를 인제스트하는 기능을 제공합니다. 오류 진단 **[!UICONTROL 을 활성화하면]** 별도로 묶인 잘못된 데이터에 대한 세부 정보를 제공합니다. 자세한 내용은 [부분 일괄 처리 통합 개요를 참조하십시오](../../../../../ingestion/batch-ingestion/partial.md).

데이터 흐름 값을 제공하고 [다음]을 **[!UICONTROL 선택합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## 데이터 흐름 검토

[ **[!UICONTROL 검토]** ] 단계가 표시되어 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**:소스 유형, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 양을 표시합니다.
* **[!UICONTROL 데이터 세트 및 매핑 필드 할당]**:데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되고 있는 데이터 세트를 표시합니다.
* **[!UICONTROL 예약]**:섭취 일정의 활성 기간, 빈도 및 간격을 표시합니다.

데이터 흐름을 검토한 후에는 [ **[!UICONTROL 마침]** ]을 클릭하고 데이터 흐름 만들기를 잠시 기다립니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## 데이터 흐름 모니터링

데이터 흐름을 만든 후 데이터 수집 중인 데이터를 모니터링하여 섭취 비율, 성공 및 오류에 대한 정보를 확인할 수 있습니다. 데이터 흐름 모니터링 방법에 대한 자세한 내용은 UI에서 계정 및 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오](../../monitor.md).

## 데이터 흐름 삭제

더 이상 필요하지 않거나 데이터 흐름 작업 영역에서 사용 가능한 **[!UICONTROL 삭제]** 기능을 사용하여 잘못 만들어진 데이터 **[!UICONTROL 를 삭제할]** 수 있습니다. 데이터 흐름 삭제 방법에 대한 자세한 내용은 UI에서 데이터 흐름 [삭제에 대한 자습서를 참조하십시오](../../delete.md).

## 다음 단계

이 튜토리얼을 따라 외부 클라우드 스토리지에서 데이터를 가져오는 데이터 흐름을 성공적으로 생성했으며 데이터 세트 모니터링에 대한 통찰력을 얻을 수 있었습니다. 데이터 흐름 만들기에 대한 자세한 내용을 살펴보려면 아래 비디오를 시청하여 학습 효과를 높일 수 있습니다. 또한 이제 들어오는 데이터를 [!DNL Platform] 및 [!DNL Real-time Customer Profile] [!DNL Data Science Workspace]과 같은 다운스트림 서비스에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## 부록

다음 섹션에서는 소스 커넥터 작업에 대한 추가 정보를 제공합니다.

### 데이터 흐름 비활성화

데이터 흐름 생성은 즉시 활성화되고 주어진 일정에 따라 데이터를 인제스트합니다. 아래 지침에 따라 언제든지 활성 데이터 흐름을 비활성화할 수 있습니다.

소스 **[!UICONTROL 작업]** 공간 내에서 **[!UICONTROL 찾아보기]** 탭을 클릭합니다. 그런 다음 비활성화할 활성 데이터 프롤과 연결된 계정 이름을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

소스 **[!UICONTROL 활동]** 페이지가 나타납니다. 목록에서 활성 데이터 흐름을 선택하여 화면 오른쪽의 **[!UICONTROL 속성]** 열을 엽니다. 이 열에는 활성화된 전환 단추가 **[!UICONTROL 포함되어]** 있습니다. 토글을 클릭하여 데이터 흐름을 비활성화합니다. 데이터 흐름을 비활성화한 후 동일한 전환을 사용하여 다시 활성화할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### 모집단 [!DNL Profile] 에 대한 인바운드 데이터 활성화

소스 커넥터의 인바운드 데이터를 [!DNL Real-time Customer Profile] 데이터 누락을 위해 사용할 수 있습니다. 데이터 채우기에 대한 자세한 내용은 [!DNL Real-time Customer Profile] 프로필 모집단 [에 대한 자습서를 참조하십시오](../../profile.md).
