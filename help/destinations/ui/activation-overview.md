---
keywords: 대상 활성화;데이터 활성화
title: 활성화 개요
type: Tutorial
description: Adobe Experience Platform의 대상을 다양한 유형의 대상으로 활성화하는 방법을 알아봅니다.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# 활성화 개요

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

Adobe Experience Platform은 다양한 대상을 지원합니다. 대상자 활성화 워크플로우는 대상자가 지원하는 대상자 데이터 유형과 데이터 내보내기 빈도에 따라 대상마다 다릅니다.

## 활성화 방법 {#activation-methods}

[대상을 구성](connect-destination.md)한 후 여러 가지 방법으로 대상을 활성화할 수 있습니다.

### 대상 카탈로그에서 대상 활성화

대상 카탈로그에서 대상자를 대상으로 활성화하는 방법에 대한 자세한 내용은 다음 안내서를 참조하십시오.

* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](activate-segment-streaming-destinations.md)
* [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](activate-streaming-profile-destinations.md)
* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](activate-batch-profile-destinations.md)

### [!UICONTROL 찾아보기] 페이지에서 대상자 활성화

**[!UICONTROL 찾아보기]** 페이지에서 데이터를 대상으로 활성화하려면 아래 단계를 따르십시오.

1. **[!UICONTROL 연결 > 대상]**(으)로 이동하여 **[!UICONTROL 찾아보기]** 탭을 선택합니다.

   ![탭 찾아보기](../assets/ui/activation-overview/browse-tab.png)

1. 세그먼트를 활성화하는 데 사용할 대상 연결을 찾고 [!UICONTROL 이름] 열에서 세 점을 선택한 다음 **[!UICONTROL 대상 활성화]**&#x200B;를 선택합니다.

   ![대상자 활성화 단추](../assets/ui/activation-overview/activate-segments.png)

1. 선택한 대상에 따라 **[!UICONTROL 세그먼트 선택]** 단계부터 아래 문서에 설명된 단계에 따라 활성화 워크플로를 완료합니다.

   * [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](activate-segment-streaming-destinations.md)
   * [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](activate-streaming-profile-destinations.md)
   * [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](activate-batch-profile-destinations.md)

### 대상 세부 사항 페이지에서 대상 활성화 {#activate-audience-details}

대상 세부 사항 페이지에서 대상을 대상으로 활성화할 수 있습니다. 자세한 내용은 [대상자 세부 정보](../../segmentation/ui/audience-portal.md#audience-details)를 참조하십시오.

선택한 대상에 따라 아래 문서에 설명된 단계에 따라 활성화 워크플로우를 완료합니다.

* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](activate-segment-streaming-destinations.md)
* [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](activate-streaming-profile-destinations.md)
* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](activate-batch-profile-destinations.md)
