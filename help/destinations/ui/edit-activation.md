---
keywords: 활성화 편집, 대상 편집, 대상 편집
title: 활성화 데이터 흐름 편집
type: Tutorial
description: 이 문서의 단계에 따라 Adobe Experience Platform에서 기존 활성화 데이터 흐름을 편집합니다.
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 활성화 데이터 흐름 편집 {#edit-activation-flows}

Adobe Experience Platform에서 내보낸 대상 및 프로필 속성, 내보내기 빈도, 활성화 데이터 흐름의 활성화 여부 등과 같은 대상에 대한 기존 활성화 데이터 흐름의 다양한 구성 요소를 편집할 수 있습니다.

## 데이터 흐름 편집 {#edit-dataflows}

기존 활성화 데이터 흐름을 편집하려면 아래 단계를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 모음에서 **[!UICONTROL 대상]**&#x200B;을 선택합니다. 기존 대상 데이터 흐름을 보려면 상단 헤더에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.

   ![대상 찾아보기](../assets/ui/edit-activation/browse-destinations.png)

2. 왼쪽 상단의 필터 아이콘 ![Filter-icon](../assets/ui/edit-activation/filter.png)을(를) 선택하여 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상의 목록을 제공합니다. 목록에서 두 개 이상의 대상을 선택하여 선택한 대상과 연관된 데이터 흐름의 필터링된 선택을 확인할 수 있습니다.

   ![대상 필터링](../assets/ui/edit-activation/filter-destinations.png)

3. 편집할 대상 데이터 흐름의 이름을 선택합니다.

   ![대상 선택](../assets/ui/edit-activation/destination-select.png)

4. 대상에 대한 **[!UICONTROL 데이터 흐름 실행]** 페이지가 나타나고 사용 가능한 컨트롤이 표시됩니다. 이 시점에서 대상 데이터 흐름의 여러 구성 요소를 편집할 수 있습니다.

   * 대상으로 보낼 대상 또는 프로필 특성을 변경하려면 오른쪽 레일에서 **[!UICONTROL 대상 활성화]**&#x200B;를 선택하십시오. 이 작업을 수행하면 대상 유형에 따라 달라지는 활성화 워크플로우로 이동합니다. 자세한 내용은 다음 안내서를 참조하십시오.
      * [대상 스트리밍 대상으로 대상 데이터 활성화](./activate-segment-streaming-destinations.md)(예: Facebook 또는 Twitter);
      * [대상자 데이터를 프로필 기반 대상으로 활성화](./activate-batch-profile-destinations.md)(예: Amazon S3 또는 Oracle Eloqua);
      * [대상 데이터를 스트리밍 프로필 기반 대상으로 활성화](./activate-streaming-profile-destinations.md)(예: HTTP API 또는 Amazon Kinesis).

   * 또한 대상 데이터 흐름 이름 및 설명을 편집할 수 있습니다.
   * **[!UICONTROL 사용]/[!UICONTROL 사용 안 함]** 전환을 사용하여 대상으로 모든 데이터 내보내기를 시작하고 일시 중지할 수 있습니다.

   ![대상 세부 정보](../assets/ui/edit-activation/destination-details.png)

## 다음 단계 {#next-steps}

이 자습서에 따라 **[!UICONTROL 대상]** 작업 영역을 사용하여 기존 대상 데이터 흐름을 업데이트했습니다.

대상에 대한 자세한 내용은 [대상 개요](../catalog/overview.md)를 참조하세요.
