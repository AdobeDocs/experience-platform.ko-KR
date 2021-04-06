---
keywords: 대상 삭제
title: 대상 삭제
type: 튜토리얼
description: 이 자습서는 Adobe Experience Platform UI에서 기존 대상을 삭제하는 단계를 나열합니다
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
translation-type: tm+mt
source-git-commit: 07869d63f395bbab6c49a3976051facdf94d43b7
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 대상 삭제 {#delete-destinations}

## 개요 {#overview}

Adobe Experience Platform 사용자 인터페이스에서 대상에 대한 기존 연결을 삭제할 수 있습니다.

대상을 삭제하면 기존 데이터 흐름이 해당 대상으로 제거됩니다. 삭제한 대상에 대해 활성화된 모든 세그먼트는 데이터 흐름 삭제 전에 매핑되지 않습니다.

[!DNL Platform] [!DNL UI]에서 대상을 삭제할 수 있는 방법에는 두 가지가 있습니다. 다음을 수행할 수 있습니다.

* [탭에서 대상  [!UICONTROL Browse] 삭제](#delete-browse-tab)
* [대상 세부 사항 페이지에서 대상 삭제](#delete-destination-details-page)

## 찾아보기 탭{#delete-browse-tab}에서 대상 삭제

[!UICONTROL Browse] 탭에서 대상을 삭제하려면 아래 절차를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 막대에서 **[!UICONTROL Destinations]**&#x200B;를 선택합니다. 기존 대상을 보려면 상단 헤더에서 **[!UICONTROL Browse]**&#x200B;을 선택합니다.

   ![검색 대상](../assets/ui/delete-destinations/browse-destinations.png)

2. 정렬 패널을 시작하려면 왼쪽 상단에 있는 필터 아이콘 ![필터 아이콘](../assets/ui/delete-destinations/filter.png)을 선택합니다. 정렬 패널은 모든 대상 목록을 제공합니다. 목록에서 대상을 두 개 이상 선택하여 선택한 대상과 연결된 데이터 흐름 필터링된 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/delete-destinations/filter-destinations.png)

3. 기존 대상을 제거하려면 **[!UICONTROL Platform]** 열에서 ![삭제 단추](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]** 단추를 선택합니다.
   ![대상 삭제](../assets/ui/delete-destinations/delete-destinations.png)

4. **[!UICONTROL Delete]**&#x200B;을 선택하여 대상 제거를 확인합니다.

   ![대상 삭제 확인](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## 대상 세부 사항 페이지에서 대상 삭제{#delete-destination-details-page}

대상 세부 사항 페이지에서 대상을 삭제하려면 아래 절차를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 막대에서 **[!UICONTROL Destinations]**&#x200B;를 선택합니다. 기존 대상을 보려면 상단 헤더에서 **[!UICONTROL Browse]**&#x200B;을 선택합니다.

   ![검색 대상](../assets/ui/delete-destinations/browse-destinations.png)

2. 정렬 패널을 시작하려면 왼쪽 상단에 있는 필터 아이콘 ![필터 아이콘](../assets/ui/delete-destinations/filter.png)을 선택합니다. 정렬 패널은 모든 대상 목록을 제공합니다. 목록에서 대상을 두 개 이상 선택하여 선택한 대상과 연결된 데이터 흐름 필터링된 선택을 볼 수 있습니다.

   ![필터 대상](../assets/ui/delete-destinations/filter-destinations.png)

3. 삭제할 대상의 이름을 선택합니다.

   ![대상 선택](../assets/ui/delete-destinations/delete-destination-select.png)

   * 대상에 기존 데이터 흐름이 있는 경우 [!UICONTROL Dataflow runs] 탭으로 이동합니다.

      ![Dataflow 실행 탭](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 대상에 기존 데이터 플로우가 없는 경우 대상 활성화를 시작할 수 있는 빈 페이지로 이동합니다.

      ![대상 세부 사항](../assets/ui/delete-destinations/destination-details-empty.png)


4. 오른쪽 레일에서 **[!UICONTROL Delete]**&#x200B;을 선택합니다.

   ![대상 삭제](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 확인 대화 상자에서 **[!UICONTROL Delete]**&#x200B;을 선택하여 대상을 제거합니다.

   ![대상 삭제 확인](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >서버 로드에 따라 [!DNL Platform]이 대상을 삭제하는 데 몇 분 정도 걸릴 수 있습니다.
