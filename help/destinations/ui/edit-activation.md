---
keywords: 활성화 편집, 대상 편집, 대상 편집
title: 활성화 데이터 흐름 편집
type: Tutorial
description: 이 문서의 단계에 따라 Adobe Experience Platform에서 기존 활성화 데이터 흐름을 편집합니다.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 활성화 데이터 흐름 편집 {#edit-activation-flows}

Adobe Experience Platform에서 내보낸 세그먼트 및 프로필 속성, 내보내기 빈도, 활성화 데이터 흐름의 활성화 여부 등과 같은 대상에 대한 기존 활성화 데이터 흐름의 다양한 구성 요소를 편집할 수 있습니다.

## 데이터 흐름 편집 {#edit-dataflows}

기존 활성화 데이터 흐름을 편집하려면 아래 단계를 따르십시오.

1. 에 로그인합니다 [EXPERIENCE PLATFORM UI](https://platform.adobe.com/) 및 선택 **[!UICONTROL 대상]** 왼쪽 탐색 모음에서 을 클릭합니다. 선택 **[!UICONTROL 찾아보기]** 을 클릭하여 기존 대상 데이터 흐름을 확인하십시오.

   ![대상 찾아보기](../assets/ui/edit-activation/browse-destinations.png)

2. 필터 아이콘 선택 ![필터 아이콘](../assets/ui/edit-activation/filter.png) 왼쪽 상단에서 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상의 목록을 제공합니다. 목록에서 두 개 이상의 대상을 선택하여 선택한 대상과 연관된 데이터 흐름의 필터링된 선택을 확인할 수 있습니다.

   ![필터 대상](../assets/ui/edit-activation/filter-destinations.png)

3. 편집할 대상 데이터 흐름의 이름을 선택합니다.

   ![대상 선택](../assets/ui/edit-activation/destination-select.png)

4. 다음 **[!UICONTROL 데이터 흐름 실행]** 사용 가능한 컨트롤이 표시된 대상 페이지가 나타납니다. 이 시점에서 대상 데이터 흐름의 여러 구성 요소를 편집할 수 있습니다.

   * 선택 **[!UICONTROL 세그먼트 활성화]** 을 클릭하여 대상으로 전송할 세그먼트 또는 프로필 속성을 변경할 수 있습니다. 이 작업을 수행하면 대상 유형에 따라 달라지는 활성화 워크플로우로 이동합니다. 자세한 내용은 다음 안내서를 참조하십시오.
      * [대상자 데이터를 세그먼트 스트리밍 대상으로 활성화](./activate-segment-streaming-destinations.md) (예: Facebook 또는 Twitter);
      * [대상자 데이터를 프로필 기반 대상 일괄 처리로 활성화](./activate-batch-profile-destinations.md) (예: Amazon S3 또는 Oracle Eloqua);
      * [대상자 데이터를 스트리밍 프로필 기반 대상으로 활성화](./activate-streaming-profile-destinations.md) (예: HTTP API 또는 Amazon Kinesis).
   * 또한 대상 데이터 흐름 이름 및 설명을 편집할 수 있습니다.
   * 다음을 사용할 수 있습니다. **[!UICONTROL 활성화됨]/[!UICONTROL 비활성화됨]** 대상으로 모든 데이터 내보내기를 시작 및 일시 중지하려면 전환하십시오.

   ![대상 세부 사항](../assets/ui/edit-activation/destination-details.png)

## 다음 단계 {#next-steps}

이 자습서에 따라 **[!UICONTROL 대상]** 기존 대상 데이터 흐름을 업데이트할 작업 영역입니다.

대상에 대한 자세한 내용은 [대상 개요](../catalog/overview.md).
