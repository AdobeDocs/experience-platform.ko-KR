---
keywords: 대상 삭제, 대상 삭제 방법, 대상 삭제
title: 대상 삭제
type: Tutorial
description: 이 자습서에는 Adobe Experience Platform UI에서 기존 대상을 삭제하는 단계가 나열되어 있습니다
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 대상 삭제 {#delete-destinations}

## 개요 {#overview}

Adobe Experience Platform 사용자 인터페이스에서 대상에 대한 기존 연결을 삭제할 수 있습니다.

대상을 삭제하면 해당 대상에 대한 기존 데이터 흐름이 모두 제거됩니다. 삭제한 대상에 활성화된 모든 대상은 데이터 흐름이 삭제되기 전에 매핑되지 않습니다.

[!DNL Platform] [!DNL UI]에서 대상을 삭제할 수 있는 방법에는 두 가지가 있습니다. 다음과 같은 작업을 수행할 수 있습니다.

* [[!UICONTROL 찾아보기] 탭에서 대상 삭제](#delete-browse-tab)
* [대상 세부 사항 페이지에서 대상 삭제](#delete-destination-details-page)

## 찾아보기 탭에서 대상 삭제{#delete-browse-tab}

[!UICONTROL 찾아보기] 탭에서 대상을 삭제하려면 아래 단계를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 모음에서 **[!UICONTROL 대상]**&#x200B;을 선택합니다. 기존 대상을 보려면 상단 헤더에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.

   ![대상 찾아보기](../assets/ui/delete-destinations/browse-destinations.png)

2. 왼쪽 상단의 필터 아이콘 ![Filter-icon](../assets/ui/delete-destinations/filter.png)을(를) 선택하여 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상의 목록을 제공합니다. 목록에서 두 개 이상의 대상을 선택하여 선택한 대상과 연관된 데이터 흐름의 필터링된 선택을 확인할 수 있습니다.

   ![대상 필터링](../assets/ui/delete-destinations/filter-destinations.png)

3. 기존 대상 연결을 제거하려면 이름 열에서 ![추가 단추](../assets/ui/delete-destinations/more-icon.png) 단추를 선택한 다음 ![삭제 단추](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL 삭제]**를 선택하십시오.
   ![대상 삭제](../assets/ui/delete-destinations/delete-destinations.png)

4. 대상 연결 제거를 확인하려면 **[!UICONTROL 삭제]**&#x200B;를 선택하십시오.

   ![대상 삭제 확인](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## 대상 세부 사항 페이지에서 대상 삭제{#delete-destination-details-page}

대상 세부 사항 페이지에서 대상을 삭제하려면 아래 단계를 따르십시오.

1. [Experience Platform UI](https://platform.adobe.com/)에 로그인하고 왼쪽 탐색 모음에서 **[!UICONTROL 대상]**&#x200B;을 선택합니다. 기존 대상을 보려면 상단 헤더에서 **[!UICONTROL 찾아보기]**&#x200B;를 선택하십시오.

   ![대상 찾아보기](../assets/ui/delete-destinations/browse-destinations.png)

2. 왼쪽 상단의 필터 아이콘 ![Filter-icon](../assets/ui/delete-destinations/filter.png)을(를) 선택하여 정렬 패널을 시작합니다. 정렬 패널에서는 모든 대상의 목록을 제공합니다. 목록에서 두 개 이상의 대상을 선택하여 선택한 대상과 연관된 데이터 흐름의 필터링된 선택을 확인할 수 있습니다.

   ![대상 필터링](../assets/ui/delete-destinations/filter-destinations.png)

3. 삭제하려는 대상의 이름을 선택합니다.

   ![대상 선택](../assets/ui/delete-destinations/delete-destination-select.png)

   * 대상에 기존 데이터 흐름이 있는 경우 [!UICONTROL 데이터 흐름 실행] 탭으로 이동합니다.

     ![데이터 흐름 실행 탭](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 대상에 기존 데이터 흐름이 없는 경우 대상 활성화를 시작할 수 있는 빈 페이지로 이동합니다.

     ![대상 세부 정보](../assets/ui/delete-destinations/destination-details-empty.png)

4. 오른쪽 레일에서 **[!UICONTROL 삭제]**&#x200B;를 선택합니다.

   ![대상 삭제](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 확인 대화 상자에서 **[!UICONTROL 삭제]**&#x200B;를 선택하여 대상을 제거합니다.

   ![대상 삭제 확인](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >서버 로드에 따라 [!DNL Platform]에서 대상을 삭제하는 데 몇 분 정도 걸릴 수 있습니다.
