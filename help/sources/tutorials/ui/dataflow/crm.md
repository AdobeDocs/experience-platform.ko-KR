---
keywords: Experience Platform;홈;인기 항목;crm 스키마;crm;CRM;데이터 흐름;데이터 흐름
solution: Experience Platform
title: UI에서 CRM 소스 연결에 대한 데이터 흐름 구성
topic-legacy: overview
type: Tutorial
description: 데이터 흐름은 소스에서 플랫폼 데이터 집합으로 데이터를 검색하고 수집하는 예약된 작업입니다. 이 자습서에서는 CRM 계정을 사용하여 새 데이터 흐름을 구성하는 단계를 제공합니다.
exl-id: e14eafa7-6594-48e6-ab7a-f6c928d1e5fb
source-git-commit: 38f64f2ba0b40a20528aac6efff0e2fd6bc12ed2
workflow-type: tm+mt
source-wordcount: '1415'
ht-degree: 0%

---

# UI에서 CRM 연결에 대한 데이터 흐름 구성

데이터 흐름은 소스에서 플랫폼 데이터 집합으로 데이터를 검색하고 수집하는 예약된 작업입니다. 이 자습서에서는 CRM 계정을 사용하여 새 데이터 흐름을 구성하는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-time Customer Profile]](../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 자습서에서는 이미 CRM 계정을 만들어야 합니다. UI에서 다른 CRM 커넥터를 만드는 자습서 목록은 [소스 커넥터 개요](../../../home.md).

## 데이터 선택

CRM 계정을 만든 후 [!UICONTROL 데이터 선택] 파일 계층 구조를 탐색할 수 있는 인터페이스를 제공하는 단계가 나타납니다.

* 인터페이스 왼쪽 절반 이상은 디렉터리 브라우저로, CRM의 파일 및 디렉터리를 표시합니다.
* 인터페이스의 오른쪽 절반을 사용하면 호환되는 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

를 사용할 수 있습니다 **[!UICONTROL 검색]** 페이지 상단에 있는 옵션을 사용하여 사용할 소스 데이터를 신속하게 식별할 수 있습니다.

>[!NOTE]
>
>검색 소스 데이터 옵션은 Analytics, 분류, 이벤트 허브 및 Kinesis 커넥터를 제외한 모든 표 형식의 소스 커넥터에서 사용할 수 있습니다.

소스 데이터를 찾으면 디렉토리를 선택한 다음 **[!UICONTROL 다음]**.

![select-data](../../../images/tutorials/dataflow/all-tabular/select-data.png)

## XDM 스키마에 데이터 필드 매핑

다음 **[!UICONTROL 매핑]** 소스 데이터를 Platform 데이터 세트에 매핑할 인터페이스를 제공하는 단계가 나타납니다.

수집할 인바운드 데이터에 대한 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

### 기존 데이터 세트 사용

기존 데이터 세트에 데이터를 수집하려면 을 선택합니다 **[!UICONTROL 기존 데이터 세트]**&#x200B;를 선택한 다음 데이터 아이콘을 선택합니다 ![데이터](../../../images/tutorials/dataflow/crm/data.png) 입력 막대 옆에 있습니다.

![기존 데이터 세트](../../../images/tutorials/dataflow/crm/existing-dataset.png)

다음 **[!UICONTROL 데이터 세트 선택]** 대화 상자가 나타납니다. 사용할 데이터 세트를 찾아 선택한 다음 를 클릭합니다 **[!UICONTROL 계속]**.

![select-dataset](../../../images/tutorials/dataflow/crm/select-dataset.png)

### 새 데이터 세트 사용

데이터를 새 데이터 세트에 수집하려면 을 선택합니다 **[!UICONTROL 새 데이터 세트]** 제공된 필드에 데이터 집합의 이름과 설명을 입력합니다.

에 스키마 이름을 입력하여 스키마 필드를 첨부할 수 있습니다 **[!UICONTROL 스키마 선택]** 검색 창. 드롭다운 아이콘을 선택하여 기존 스키마 목록을 볼 수도 있습니다. 또는 다음을 선택할 수 있습니다 **[!UICONTROL 고급 검색]** 각각의 세부 정보를 포함하여 기존 스키마의 화면에 액세스합니다.

이 단계에서에 데이터 세트를 활성화할 수 있습니다 [!DNL Real-time Customer Profile] 엔티티의 속성 및 동작을 전체적으로 확인할 수 있습니다. 활성화된 모든 데이터 세트의 데이터는 [!DNL Profile] 및 변경 사항은 데이터 흐름을 저장할 때 적용됩니다.

전환 **[!UICONTROL 프로필 데이터 세트]** target 데이터 세트에 대한 활성화 단추 [!DNL Profile].

![새로운 데이터 세트 만들기](../../../images/tutorials/dataflow/crm/new-dataset.png)

다음 **[!UICONTROL 스키마 선택]** 대화 상자가 나타납니다. 새 데이터 세트에 적용할 스키마를 선택한 다음 를 클릭합니다 **[!UICONTROL 완료]**.

![select-schema](../../../images/tutorials/dataflow/crm/select-schema.png)

필요에 따라 필드를 직접 매핑하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산 또는 계산된 값을 도출할 수 있습니다. 매퍼 인터페이스 및 계산된 필드를 사용하는 방법에 대한 포괄적인 단계는 다음을 참조하십시오 [데이터 준비 UI 안내서](../../../../data-prep/ui/mapping.md)

>[!TIP]
>
>를 사용하는 경우 [!DNL Salesforce] B2B CDP의 일부로 소스를 참조하려면 [[!DNL Salesforce] 필드 매핑 테이블](../../../connectors/adobe-applications/mapping/salesforce.md) 다음 사이에 적절한 매핑 세트에 대한 안내서입니다. [!DNL Salesforce] 소스 필드 및 XDM 대상 필드.

플랫폼은 선택한 대상 스키마나 데이터 세트를 기반으로 자동 매핑 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

선택 **[!UICONTROL 데이터 미리 보기]** 선택한 데이터 세트에서 최대 100개의 샘플 데이터 행의 매핑 결과를 확인하십시오.

![](../../../images/tutorials/dataflow/crm/preview-data.png)

미리 보기 중에 ID 열은 매핑 결과를 확인할 때 필요한 주요 정보이므로 첫 번째 필드로 우선 순위가 지정됩니다.

소스 데이터가 매핑되면 **[!UICONTROL 닫기]**.

![](../../../images/tutorials/dataflow/crm/preview.png)

다음, [!UICONTROL 매핑] 화면, 선택 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../../images/tutorials/dataflow/crm/mapping.png)

## 수집 실행 예약

다음 **[!UICONTROL 예약]** 구성된 매핑을 사용하여 선택한 소스 데이터를 자동으로 수집하도록 수집 일정을 구성할 수 있는 단계가 나타납니다. 다음 표에서는 스케줄링에 대해 다양한 구성 가능한 필드에 대해 설명합니다.

| 필드 | 설명 |
| --- | --- |
| 빈도 | 선택할 수 있는 주파수는 다음과 같습니다 `Once`, `Minute`, `Hour`, `Day`, 및 `Week`. |
| 간격 | 선택한 주파수의 간격을 설정하는 정수입니다. |
| 시작 시간 | 첫 번째 수집이 발생하도록 설정된 시기를 나타내는 UTC 타임스탬프입니다. |
| 채우기 | 처음에 수집되는 데이터를 결정하는 부울 값입니다. If **[!UICONTROL 채우기]** 이 활성화되어 있으면 지정된 경로에 있는 모든 현재 파일이 첫 번째 예약된 수집 중에 수집됩니다. If **[!UICONTROL 채우기]** 이 비활성화되어 있으면 첫 번째 수집 실행과 **[!UICONTROL 시작 시간]** 가 수집됩니다. 이전에 로드된 파일 **[!UICONTROL 시작 시간]** 수집되지 않습니다. |
| 델타 열 | 유형, 날짜 또는 시간의 소스 스키마 필드 필터링된 옵션이 있습니다. 이 필드는 새 데이터와 기존 데이터를 구분하는 데 사용됩니다. 증분 데이터는 선택한 열의 타임스탬프를 기반으로 수집됩니다. |

데이터 흐름은 예약된 기준에 따라 데이터를 자동으로 수집하도록 설계되었습니다. 먼저 수집 빈도를 선택합니다. 그런 다음 간격을 설정하여 두 흐름 실행 사이의 기간을 지정합니다. 간격 값은 0이 아닌 정수여야 하며 15보다 크거나 같도록 설정해야 합니다.

수집 시작 시간을 설정하려면 시작 시간 상자에 표시되는 날짜 및 시간을 조정하십시오. 또는 달력 아이콘을 선택하여 시작 시간 값을 편집할 수 있습니다. 시작 시간은 현재 UTC 시간보다 크거나 같아야 합니다.

선택 **[!UICONTROL 증분 데이터 로드 기준]** 델타 열을 할당하려면 이 필드는 새 데이터와 기존 데이터를 구별합니다.

![](../../../images/tutorials/dataflow/crm/scheduling.png)

### 1회 수집 데이터 흐름 설정

1회 수집을 설정하려면 빈도 드롭다운 화살표를 선택하고 을(를) 선택합니다 **[!UICONTROL 한 번]**.

>[!TIP]
>
>**[!UICONTROL 간격]** 및 **[!UICONTROL 채우기]** 일회성 수집 중에 표시되지 않습니다.

일정에 적절한 값을 제공한 후 **[!UICONTROL 다음]**.

![예약-한 번](../../../images/tutorials/dataflow/crm/one-time-ingestion.png)

## 데이터 흐름 세부 정보 제공

다음 **[!UICONTROL 데이터 흐름 세부 정보]** 새 데이터 흐름의 이름을 지정하고 간단한 설명을 제공할 수 있는 단계가 나타납니다.

이 프로세스 중에 **[!UICONTROL 부분 수집]** 및 **[!UICONTROL 오류 진단]**. 활성화 **[!UICONTROL 부분 수집]** 은 특정 임계값까지 오류가 포함된 데이터를 수집할 수 있는 기능을 제공합니다. 한 번 **[!UICONTROL 부분 수집]** 이 활성화되어 있으면 **[!UICONTROL 오류 임계값 %]** 을 눌러 일괄 처리의 오류 임계값을 조정합니다. 또는 입력 상자를 선택하여 임계값을 수동으로 조정할 수 있습니다. 자세한 내용은 [부분 배치 수집 개요](../../../../ingestion/batch-ingestion/partial.md).

데이터 흐름의 값을 제공하고 을 선택합니다 **[!UICONTROL 다음]**.

![데이터 흐름 세부 정보](../../../images/tutorials/dataflow/crm/dataflow-detail.png)

## 데이터 흐름 검토

다음 *검토* 새 데이터 흐름을 만들기 전에 검토할 수 있는 단계가 나타납니다. 세부 사항은 다음 범주 내에 그룹화됩니다.

* **[!UICONTROL 연결]**: 소스 계정 이름, 소스 플랫폼, 선택한 소스 파일의 관련 경로 및 해당 소스 파일 내의 열 양을 표시합니다.
* **[!UICONTROL 데이터 세트 및 맵 필드 할당]**: 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되는 대상 데이터 세트를 표시합니다.
* **[!UICONTROL 예약]**: 데이터 흐름의 시작 시간 및 빈도 비율을 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]** 데이터 흐름을 만들 시간을 허용합니다.

![검토](../../../images/tutorials/dataflow/crm/review.png)

## 데이터 흐름 모니터링

데이터 흐름이 만들어지면 이를 통해 수집되는 데이터를 모니터링하여 수집률, 성공 및 오류에 대한 정보를 볼 수 있습니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 [UI에서 계정 및 데이터 흐름 모니터링](../monitor.md).

## 데이터 흐름 삭제

더 이상 필요하지 않거나 잘못된 데이터 흐름을 **[!UICONTROL 삭제]** 함수에서 사용 가능한 함수 **[!UICONTROL 데이터 흐름]** 작업 공간. 데이터 흐름을 삭제하는 방법에 대한 자세한 내용은 [UI에서 데이터 흐름 삭제](../delete.md).

## 다음 단계

이 자습서를 따라 CRM에서 데이터를 가져올 데이터 흐름을 성공적으로 만들어 데이터 세트 모니터링에 대한 통찰력을 얻을 수 있습니다. 데이터 흐름 만들기에 대한 자세한 내용을 보려면 아래 비디오를 시청하여 학습 내용을 보완할 수 있습니다. 또한 이제 다음과 같은 다운스트림 Platform 서비스에서 들어오는 데이터를 사용할 수 있습니다 [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../profile/home.md)
* [Data Science Workspace 개요](../../../../data-science-workspace/home.md)

>[!WARNING]
>
> 다음 비디오에 표시된 플랫폼 UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.
>
>[!VIDEO](https://video.tv.adobe.com/v/29711?quality=12&learn=on)
