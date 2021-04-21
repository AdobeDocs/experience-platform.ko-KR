---
keywords: Experience Platform;홈;인기 항목;클라우드 저장소 커넥터;클라우드 저장소;;home;popular topics;cloud storage
solution: Experience Platform
title: UI에서 클라우드 스토리지 스트리밍 커넥터에 대한 데이터 흐름 구성
topic-legacy: overview
type: Tutorial
description: 데이터 흐름(Dataflow)은 소스에서 플랫폼 데이터 집합으로 데이터를 검색하고 인제스트하는 예약된 작업입니다. 이 자습서에서는 클라우드 저장소 기본 커넥터를 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.
exl-id: 75deead6-ef3c-48be-aed2-c43d1f432178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 1%

---

# UI에서 클라우드 스토리지 스트리밍 연결에 대한 데이터 흐름 구성

데이터 흐름(Dataflow)은 소스의 데이터를 검색하여 [!DNL Platform] 데이터 세트로 인제스트하는 예약된 작업입니다. 이 자습서에서는 클라우드 저장소 기본 커넥터를 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):고객 경험 데이터를  [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 튜토리얼을 사용하려면 이미 클라우드 스토리지 커넥터를 제작해야 합니다. UI에서 다른 클라우드 스토리지 커넥터를 만들기 위한 자습서 목록은 [소스 커넥터 개요](../../../../home.md)에서 찾을 수 있습니다.

## 데이터 선택

클라우드 스토리지 커넥터를 만든 후 데이터를 스트림할 스트림을 선택할 수 있도록 *데이터* 선택 단계가 표시됩니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## 데이터 필드를 XDM 스키마에 매핑

소스 데이터를 [!DNL Platform] 데이터 세트에 매핑하기 위한 대화형 인터페이스를 제공하는 **[!UICONTROL Mapping]** 단계가 나타납니다.

수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 집합을 사용하거나 새 데이터 집합을 만들 수 있습니다.

**기존 데이터 세트 사용**

데이터를 기존 데이터 세트에 인제스트하려면 **[!UICONTROL Use existing dataset]**&#x200B;을 선택한 다음 데이터 세트 아이콘을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

**[!UICONTROL Select dataset]** 대화 상자가 나타납니다. 사용할 데이터 세트를 찾아 선택한 다음 **[!UICONTROL Continue]**&#x200B;을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**새 데이터 세트 사용**

데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL Create new dataset]**&#x200B;을 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 그런 다음 드롭다운 아래에서 사용할 스키마를 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## 데이터 흐름 이름 지정

**[!UICONTROL Dataflow detail]** 단계가 나타나 새 데이터 흐름 이름을 지정하고 간단한 설명을 제공할 수 있습니다.

데이터 흐름 값을 입력하고 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### 데이터 흐름 검토

**[!UICONTROL Review]** 단계가 나타나 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

- **[!UICONTROL Source details]**:소스 유형과 소스에 대한 기타 관련 세부 사항을 표시합니다.
- **[!UICONTROL Target details]**:데이터 세트가 준수하는 스키마를 포함하여 원본 데이터를 수집할 데이터 집합을 표시합니다.

데이터 흐름을 검토했으면 **[!UICONTROL Finish]**&#x200B;을(를) 클릭하고 데이터 흐름을 만들 시간을 잠시 기다립니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 데이터 흐름 모니터링 및 삭제

클라우드 스토리지 데이터 플로우가 생성되면 이를 통해 인제스트되는 데이터를 모니터링할 수 있습니다. 데이터 흐름 모니터링 및 삭제에 대한 자세한 내용은 [데이터 흐름 모니터링](../../../../../ingestion/quality/monitor-data-ingestion.md)에서 자습서를 참조하십시오.

## 다음 단계

이 튜토리얼을 따라 데이터 흐름을 만들어 외부 클라우드 스토리지에서 데이터를 가져오고 데이터 집합 모니터링에 대한 통찰력을 얻었습니다. 이제 [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace] 등의 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)

## 부록

다음 섹션에서는 소스 커넥터 작업에 대한 추가 정보를 제공합니다.

### 데이터 흐름 비활성화

데이터 흐름을 만들면 즉시 활성 상태가 되어 지정된 일정에 따라 데이터를 인제스트합니다. 아래 지침에 따라 언제든지 활성 데이터 흐름을 비활성화할 수 있습니다.

**[!UICONTROL Sources]** 작업 영역에서 **[!UICONTROL Browse]** 탭을 클릭합니다. 그런 다음 비활성화할 활성 데이터 프롤에 연결된 연결 이름을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

**[!UICONTROL Source activity]** 페이지가 나타납니다. 목록에서 활성 데이터 흐름을 선택하여 화면 오른쪽의 **[!UICONTROL Properties]** 열을 엽니다. 이 열에는 **[!UICONTROL Enabled]** 전환 단추가 있습니다. 토글을 클릭하여 데이터 흐름을 비활성화합니다. 데이터 흐름을 비활성화한 후 동일한 전환을 사용하여 데이터 흐름을 다시 활성화할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### [!DNL Profile] 모집단용 인바운드 데이터 활성화

소스 커넥터의 인바운드 데이터를 사용하여 [!DNL Real-time Customer Profile] 데이터를 누름 및 채울 수 있습니다. [!DNL Real-time Customer Profile] 데이터를 채우는 방법에 대한 자세한 내용은 [프로필 채우기](../../profile.md)에 대한 자습서를 참조하십시오.
