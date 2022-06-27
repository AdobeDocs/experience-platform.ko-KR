---
keywords: 활성화 편집, 대상 편집, 대상 편집
title: 활성화 데이터 흐름 편집
type: Tutorial
description: Adobe Experience Platform의 기존 활성화 데이터 플로우를 편집하려면 이 문서의 단계를 따르십시오.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 활성화 데이터 흐름 편집 {#edit-activation-flows}

Adobe Experience Platform에서는 내보낸 세그먼트 및 프로필 속성, 내보내기 빈도, 활성화 데이터 데이터 흐름이 활성화 또는 비활성화되었는지 여부 등과 같은 기존 활성화 데이터 흐름의 다양한 구성 요소를 대상으로 편집할 수 있습니다.

## 데이터 흐름 편집 {#edit-dataflows}

기존 활성화 데이터 흐름을 편집하려면 아래 절차를 따르십시오.

1. 에 로그인합니다. [Experience Platform UI](https://platform.adobe.com/) 을(를) 선택합니다. **[!UICONTROL 대상]** 왼쪽 탐색 막대에서 을 클릭합니다. 선택 **[!UICONTROL 찾아보기]** 기존 대상 데이터 흐름을 보려면 상단 헤더에서 클릭하십시오.

   ![찾아보기 대상](../assets/ui/edit-activation/browse-destinations.png)

2. 필터 아이콘을 선택합니다 ![Filter-icon](../assets/ui/edit-activation/filter.png) 왼쪽 상단에서 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상 목록을 제공합니다. 목록에서 둘 이상의 대상을 선택하여 선택한 대상과 연관된 필터링된 데이터 흐름 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/edit-activation/filter-destinations.png)

3. 편집할 대상 데이터 흐름의 이름을 선택합니다.

   ![대상 선택](../assets/ui/edit-activation/destination-select.png)

4. 다음 **[!UICONTROL 데이터 흐름 실행]** 사용 가능한 컨트롤을 보여주는 대상 페이지가 나타납니다. 이때 대상 데이터 흐름의 여러 구성 요소를 편집할 수 있습니다.

   * 선택 **[!UICONTROL 세그먼트 활성화]** 오른쪽 레일에서 를 클릭하여 대상에 전송할 세그먼트 또는 프로필 속성을 변경합니다. 이 작업을 수행하면 활성화 워크플로우로 이동합니다. 활성화 워크플로우는 대상 유형에 따라 다릅니다. 자세한 내용은 다음 안내서를 참조하십시오.
      * [세그먼트 스트리밍 대상에 대상 데이터 활성화](./activate-segment-streaming-destinations.md) (예: Facebook 또는 Twitter);
      * [대상자 데이터를 묶음 프로필 기반 대상으로 활성화](./activate-batch-profile-destinations.md) (예: Amazon S3 또는 Oracle Eloqua);
      * [스트리밍 프로필 기반 대상으로 대상 데이터 활성화](./activate-streaming-profile-destinations.md) (예: HTTP API 또는 Amazon Kinesis)
   * 또한 대상 데이터 흐름 이름 및 설명을 편집할 수 있습니다.
   * 를 사용할 수 있습니다 **[!UICONTROL 활성화됨]/[!UICONTROL 비활성화됨]** 모든 데이터 내보내기를 대상으로 시작 및 일시 중지로 전환합니다.

   ![대상 세부 사항](../assets/ui/edit-activation/destination-details.png)

## 다음 단계 {#next-steps}

이 자습서를 따라 다음을 성공적으로 사용했습니다. **[!UICONTROL 대상]** 기존 대상 데이터 흐름을 업데이트하는 작업 공간입니다.

대상에 대한 자세한 내용은 [대상 개요](../catalog/overview.md).
