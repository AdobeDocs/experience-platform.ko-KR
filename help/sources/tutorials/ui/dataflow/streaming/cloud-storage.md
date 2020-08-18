---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 클라우드 스토리지 스트리밍 커넥터에 대한 데이터 흐름 구성
topic: overview
translation-type: tm+mt
source-git-commit: 6bd5dc5a68fb2814ab99d43b34f90aa7e50aa463
workflow-type: tm+mt
source-wordcount: '667'
ht-degree: 0%

---


# UI에서 클라우드 스토리지 스트리밍 커넥터에 대한 데이터 흐름 구성

데이터 흐름(Dataflow)은 소스에서 데이터 세트로 데이터를 검색하고 인제스트하는 예약된 [!DNL Platform] 작업입니다. 이 자습서에서는 클라우드 스토리지 기반 커넥터를 사용하여 새 데이터 흐름을 구성하는 절차를 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

- [[!DNL Experience Data Model] (XDM) 시스템](../../../../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
   - [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   - [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
- [[!DNL 실시간 고객 프로필]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

또한 이 자습서에서는 클라우드 스토리지 커넥터를 이미 만들어야 합니다. UI에서 다른 클라우드 스토리지 커넥터를 만들기 위한 자습서 목록은 [소스 커넥터 개요에 있습니다](../../../../home.md).

## 데이터 선택

클라우드 스토리지 커넥터를 만든 후 *데이터* 선택 단계가 나타나며 데이터를 스트림할 스트림을 선택할 수 있는 인터페이스를 제공합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-data.png)

## 데이터 필드를 XDM 스키마에 매핑

소스 데이터를 데이터 세트에 매핑하기 위한 대화형 인터페이스를 제공하는 **[!UICONTROL 매핑]** 단계가 [!DNL Platform] 나타납니다.

수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

**기존 데이터 세트 사용**

데이터를 기존 데이터 세트에 인제스트하려면 기존 데이터 세트 ****&#x200B;사용을 선택한 다음 데이터 세트 아이콘을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-existing-data.png)

데이터 **[!UICONTROL 세트]** 선택 대화 상자가 나타납니다. 사용할 데이터 세트를 찾아 선택한 다음 **[!UICONTROL 계속을 클릭합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/select-existing-data.png)

**새 데이터 집합 사용**

데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL 새 데이터 세트]** 만들기를 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 그런 다음 드롭다운 아래에서 사용할 스키마를 선택합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/use-new-dataset.png)

## 데이터 흐름 이름 지정

데이터 **[!UICONTROL 흐름 세부]** 정보 단계가 나타나므로 새 데이터 흐름 이름에 대한 간단한 설명을 제공할 수 있습니다.

데이터 흐름 값을 제공하고 [다음]을 **[!UICONTROL 클릭합니다]**.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/name-your-dataflow.png)

### 데이터 흐름 검토

[ **[!UICONTROL 검토]** ] 단계가 표시되어 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

- **[!UICONTROL 소스 세부 정보]**:소스에 대한 소스 유형 및 기타 관련 세부 사항을 표시합니다.
- **[!UICONTROL Target 세부 정보]**:데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집되고 있는 데이터 세트를 표시합니다.

데이터 흐름을 검토한 후에는 [ **[!UICONTROL 마침]** ]을 클릭하고 데이터 흐름 만들기를 잠시 기다립니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/review.png)

## 데이터 흐름 모니터링 및 삭제

클라우드 스토리지 데이터 프롤이 생성되면 이를 통해 인제스트되는 데이터를 모니터링할 수 있습니다. 데이터 흐름 모니터링 및 삭제에 대한 자세한 내용은 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오](../../../../../ingestion/quality/monitor-data-flows.md).

## 다음 단계

이 튜토리얼을 따라 외부 클라우드 스토리지에서 데이터를 가져오는 데이터 흐름을 성공적으로 생성했으며 데이터 세트 모니터링에 대한 통찰력을 얻을 수 있었습니다. 이제 및 같은 다운스트림 [!DNL Platform] 서비스에서 들어오는 데이터를 사용할 수 [!DNL Real-time Customer Profile] 있습니다 [!DNL Data Science Workspace]. 자세한 내용은 다음 문서를 참조하십시오.

- [[!DNL Real-time Customer Profile] 개요](../../../../../profile/home.md)
- [[!DNL Data Science Workspace] 개요](../../../../../data-science-workspace/home.md)

## 부록

다음 섹션에서는 소스 커넥터 작업에 대한 추가 정보를 제공합니다.

### 데이터 흐름 비활성화

데이터 흐름 생성은 즉시 활성화되고 주어진 일정에 따라 데이터를 인제스트합니다. 아래 지침에 따라 언제든지 활성 데이터 흐름을 비활성화할 수 있습니다.

소스 **[!UICONTROL 작업]** 공간 내에서 **[!UICONTROL 찾아보기]** 탭을 클릭합니다. 그런 다음 비활성화할 활성 데이터 프롤과 연결된 연결 이름을 클릭합니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/browse.png)

소스 **[!UICONTROL 활동]** 페이지가 나타납니다. 목록에서 활성 데이터 흐름을 선택하여 화면 오른쪽의 **[!UICONTROL 속성]** 열을 엽니다. 이 열에는 활성화된 전환 단추가 **[!UICONTROL 포함되어]** 있습니다. 토글을 클릭하여 데이터 흐름을 비활성화합니다. 데이터 흐름을 비활성화한 후 동일한 전환을 사용하여 다시 활성화할 수 있습니다.

![](../../../../images/tutorials/dataflow/cloud-storage/streaming/disable-source.png)

### 모집단 [!DNL Profile] 에 대한 인바운드 데이터 활성화

소스 커넥터의 인바운드 데이터를 [!DNL Real-time Customer Profile] 데이터 누락을 위해 사용할 수 있습니다. 데이터 채우기에 대한 자세한 내용은 [!DNL Real-time Customer Profile] 프로필 모집단 [에 대한 자습서를 참조하십시오](../../profile.md).
