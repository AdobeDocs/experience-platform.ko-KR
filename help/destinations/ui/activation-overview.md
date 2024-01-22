---
keywords: 대상 활성화;데이터 활성화
title: 활성화 개요
type: Tutorial
description: Adobe Experience Platform의 대상을 다양한 유형의 대상으로 활성화하는 방법을 알아봅니다.
exl-id: 987af401-2d93-45b4-a8f9-191e6058e4da
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 1%

---

# 활성화 개요

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

Adobe Experience Platform은 다양한 대상을 지원합니다. 대상자 활성화 워크플로우는 대상자가 지원하는 대상자 데이터 유형과 데이터 내보내기 빈도에 따라 대상마다 다릅니다.

## 활성화 방법 {#activation-methods}

이후 [대상 구성](connect-destination.md), 다음과 같은 여러 가지 방법으로 대상을 활성화할 수 있습니다.

### 대상 카탈로그에서 대상 활성화

대상 카탈로그에서 대상자를 대상으로 활성화하는 방법에 대한 자세한 내용은 다음 안내서를 참조하십시오.

* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](activate-segment-streaming-destinations.md)
* [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](activate-streaming-profile-destinations.md)
* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](activate-batch-profile-destinations.md)

### 에서 대상자 활성화 [!UICONTROL 찾아보기] 페이지

다음 단계에 따라 다음 위치에서 대상에 데이터를 활성화합니다. **[!UICONTROL 찾아보기]** 페이지를 가리키도록 업데이트하는 중입니다.

1. 다음으로 이동 **[!UICONTROL 연결 > 대상]**&#x200B;을(를) 클릭하고 **[!UICONTROL 찾아보기]** 탭.

   ![찾아보기 탭](../assets/ui/activation-overview/browse-tab.png)

1. 세그먼트를 활성화하는 데 사용할 대상 연결을 찾은 다음, [!UICONTROL 이름] 열을 선택한 다음 **[!UICONTROL 대상자 활성화]**.

   ![대상자 활성화 버튼](../assets/ui/activation-overview/activate-segments.png)

1. 선택한 대상에 따라 다음 문서에서 설명하는 단계를 따릅니다. **[!UICONTROL 세그먼트 선택]** 단계, 활성화 워크플로를 완료하려면

   * [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](activate-segment-streaming-destinations.md)
   * [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](activate-streaming-profile-destinations.md)
   * [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](activate-batch-profile-destinations.md)

### 대상 세부 사항 페이지에서 대상 활성화 {#activate-audience-details}

대상 세부 사항 페이지에서 대상을 대상으로 활성화할 수 있습니다. 다음을 참조하십시오 [대상자 세부 정보](../../segmentation/ui/overview.md#audience-details) 추가 정보.

선택한 대상에 따라 아래 문서에 설명된 단계에 따라 활성화 워크플로우를 완료합니다.

* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](activate-segment-streaming-destinations.md)
* [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](activate-streaming-profile-destinations.md)
* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](activate-batch-profile-destinations.md)
