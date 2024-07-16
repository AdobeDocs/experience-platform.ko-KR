---
keywords: Experience Platform;홈;자주 찾는 항목;스트리밍;클라우드 스토리지 커넥터;클라우드 스토리지
solution: Experience Platform
title: UI에서 클라우드 스토리지 소스에 대한 스트리밍 데이터 흐름 만들기
type: Tutorial
description: 데이터 흐름은 소스에서 Platform 데이터 세트로 데이터를 검색하고 수집하는 예약된 작업입니다. 이 자습서에서는 클라우드 스토리지 기반 커넥터를 사용하여 새 데이터 흐름을 구성하는 단계를 제공합니다.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
source-git-commit: 6419ae7648a91dc7f9432281c1960beccc65bdb0
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# UI에서 클라우드 스토리지 소스에 대한 스트리밍 데이터 흐름 만들기

데이터 흐름은 소스에서 Adobe Experience Platform 데이터 세트로 데이터를 검색하고 수집하는 예약된 작업입니다. 이 자습서에서는 UI에서 클라우드 스토리지 소스에 대한 스트리밍 데이터 흐름을 만드는 단계를 제공합니다.

이 자습서를 시도하기 전에 먼저 클라우드 스토리지 계정과 플랫폼 간에 유효하고 인증된 연결을 설정해야 합니다. 인증된 연결이 없는 경우 스트리밍 클라우드 스토리지 계정 인증에 대한 자세한 내용은 다음 튜토리얼 중 하나를 참조하십시오.

- [[!DNL Amazon Kinesis]](../../../ui/create/cloud-storage/kinesis.md)
- [[!DNL Azure Event Hubs]](../../../ui/create/cloud-storage/eventhub.md)
- [[!DNL Google PubSub]](../../../ui/create/cloud-storage/google-pubsub.md)

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [데이터 흐름](../../../../../dataflows/home.md): 데이터 흐름은 플랫폼 간에 데이터를 이동하는 데이터 작업을 나타냅니다. 데이터 흐름은 원본에서 [!DNL Identity Service], [!DNL Profile] 및 [!DNL Destinations](으)로 다양한 서비스에 걸쳐 구성됩니다.
- [데이터 준비](../../../../../data-prep/home.md): 데이터 준비를 통해 데이터 엔지니어는 데이터를 XDM(Experience Data Model)에 매핑하고, 변환하고, 유효성을 검사할 수 있습니다. 데이터 준비는 CSV 수집 워크플로를 포함하여 데이터 수집 프로세스에서 &quot;맵&quot; 단계로 표시됩니다.
- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## 데이터 추가

>[!NOTE]
>
>지정된 이벤트 허브에 대해 소비자 그룹당 하나의 소스 데이터 흐름만 만들 수 있습니다.

스트리밍 클라우드 저장소 계정을 인증하면 플랫폼으로 가져올 데이터 스트림을 선택할 수 있는 인터페이스를 제공하는 **[!UICONTROL 데이터 선택]** 단계가 나타납니다.

- 인터페이스의 왼쪽 부분은 계정 내에서 사용 가능한 데이터 스트림을 볼 수 있는 브라우저입니다.
- 인터페이스의 오른쪽 부분에서 JSON 파일에서 최대 100개의 데이터 행을 미리 볼 수 있습니다.

![인터페이스](../../../../images/tutorials/dataflow/cloud-storage/streaming/interface.png)

사용할 데이터 스트림을 선택한 다음 **[!UICONTROL 파일 선택]**&#x200B;을 선택하여 샘플 스키마를 업로드합니다.

>[!TIP]
>
>데이터가 XDM을 준수하는 경우 샘플 스키마 업로드를 건너뛰고 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속할 수 있습니다.

![select-stream](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-stream.png)

스키마가 업로드되면 미리보기 인터페이스가 업데이트되어 업로드한 스키마의 미리보기가 표시됩니다. 미리보기 인터페이스를 사용하여 파일의 내용과 구조를 검사할 수 있습니다. [!UICONTROL 검색 필드] 유틸리티를 사용하여 스키마 내의 특정 항목에 액세스할 수도 있습니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![스키마 미리 보기](../../../../images/tutorials/dataflow/cloud-storage/streaming/schema-preview.png)

## 매핑

소스 데이터를 Platform 데이터 집합에 매핑하는 인터페이스를 제공하는 **[!UICONTROL 매핑]** 단계가 나타납니다.

수집할 인바운드 데이터에 대한 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

### 새 데이터 세트

데이터를 새 데이터 집합으로 수집하려면 **[!UICONTROL 새 데이터 집합]**&#x200B;을(를) 선택하고 제공된 필드에 데이터 집합의 이름과 설명을 입력하십시오. 스키마를 추가하려면 **[!UICONTROL 스키마 선택]** 대화 상자에 기존 스키마 이름을 입력할 수 있습니다. 또는 **[!UICONTROL 스키마 고급 검색]**&#x200B;을 선택하여 적절한 스키마를 검색할 수 있습니다.

![new-dataset](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-dataset.png)

선택할 수 있는 스키마 목록을 제공하는 [!UICONTROL 스키마 선택] 창이 나타납니다. 목록에서 스키마를 선택하여 오른쪽 레일을 업데이트하면 [!DNL Profile]에 대해 스키마를 사용할 수 있는지 여부에 대한 정보를 포함하여 선택한 스키마와 관련된 세부 정보를 표시할 수 있습니다.

사용할 스키마를 식별하고 선택하면 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

![스키마 선택](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-schema.png)

[!UICONTROL Target 데이터 세트] 페이지가 데이터 세트의 일부로 표시된 선택한 스키마로 업데이트됩니다. 이 단계에서는 [!DNL Profile]에 대한 데이터 세트를 활성화하고 엔터티의 특성과 동작을 전체적으로 볼 수 있습니다. 활성화된 모든 데이터 세트의 데이터가 [!DNL Profile]에 포함되며 데이터 흐름을 저장할 때 변경 내용이 적용됩니다.

**[!UICONTROL 프로필 데이터 세트]** 단추를 전환하여 [!DNL Profile]에 대한 대상 데이터 세트를 사용하도록 설정합니다.

![새 프로필](../../../../images/tutorials/dataflow/cloud-storage/streaming/new-profile.png)

### 기존 데이터 세트

기존 데이터 집합에 데이터를 수집하려면 **[!UICONTROL 기존 데이터 집합]**&#x200B;을 선택한 다음 데이터 집합 아이콘을 선택합니다.

![기존 데이터 세트](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-dataset.png)

선택할 수 있는 데이터 세트 목록을 제공하는 **[!UICONTROL 데이터 세트 선택]** 대화 상자가 나타납니다. 목록에서 데이터 세트를 선택하여 오른쪽 레일을 업데이트하면 [!DNL Profile]에 대해 데이터 세트를 활성화할 수 있는지 여부에 대한 정보를 포함하여 선택한 데이터 세트와 관련된 세부 정보가 표시됩니다.

사용할 데이터 세트를 확인하고 선택한 후에는 **[!UICONTROL 완료]**&#x200B;를 선택합니다.

![데이터 집합 선택](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-dataset.png)

데이터 세트를 선택하면 [!DNL Profile] 토글을 선택하여 [!DNL Profile]에 대한 데이터 세트를 사용하도록 설정합니다.

![기존 프로필](../../../../images/tutorials/dataflow/cloud-storage/streaming/existing-profile.png)

### 표준 필드 매핑

데이터 집합과 스키마가 설정되면 데이터에 대한 매핑 필드를 수동으로 구성할 수 있는 **[!UICONTROL 표준 필드 매핑]** 인터페이스가 나타납니다.

>[!TIP]
>
>Platform은 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../../../data-prep/ui/mapping.md)를 참조하십시오.

원본 데이터가 매핑되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![매핑](../../../../images/tutorials/dataflow/cloud-storage/streaming/mapping.png)

## 데이터 흐름 세부 정보

**[!UICONTROL 데이터 흐름 세부 정보]** 단계가 표시되어 새 데이터 흐름의 이름을 지정하고 간단한 설명을 제공할 수 있습니다.

데이터 흐름의 값을 입력하고 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![데이터 흐름-세부 정보](../../../../images/tutorials/dataflow/cloud-storage/streaming/dataflow-detail.png)

### 검토

새 데이터 흐름을 만들기 전에 검토할 수 있는 **[!UICONTROL 검토]** 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

- **[!UICONTROL 연결]**: 사용 중인 스트리밍 클라우드 저장소 원본과 관련된 계정 이름, 원본 유형 및 기타 정보를 표시합니다.
- **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 데이터 흐름에 사용 중인 대상 데이터 집합 및 스키마를 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 선택하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![검토](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 데이터 흐름 모니터링 및 삭제

스트리밍 클라우드 스토리지 데이터 흐름이 생성되면 이를 통해 수집되는 데이터를 모니터링할 수 있습니다. 스트리밍 데이터 흐름 모니터링 및 삭제에 대한 자세한 내용은 [스트리밍 데이터 흐름 모니터링](../../monitor-streaming.md)에 대한 자습서를 참조하십시오.

## 다음 단계

이 자습서에 따라 클라우드 스토리지 소스에서 데이터를 스트리밍하기 위한 데이터 흐름을 만들었습니다. 이제 [!DNL Real-Time Customer Profile] 및 [!DNL Data Science Workspace]과(와) 같은 다운스트림 플랫폼 서비스에서 수신 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [[!DNL Real-Time Customer Profile] 개요](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)