---
keywords: 대상 연결;대상 연결;대상 연결 방법
title: 새 대상 연결 만들기
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform에서 대상에 연결하는 단계를 보여줍니다
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 729c0724c7af88bb69c9d68a45d58c3575c90828
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 새 대상 연결 만들기

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

## 개요 {#overview}

대상 데이터를 대상에 보내려면 먼저 대상 플랫폼에 연결을 설정해야 합니다. 이 문서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 새 대상을 설정하는 방법을 보여 줍니다.

## 새 대상 연결 만들기 {#setup}

1. 이동 **[!UICONTROL 연결]** > **[!UICONTROL 대상]**, 을(를) 선택하고 을(를) 선택합니다. **[!UICONTROL 카탈로그]** 탭.

   ![카탈로그 페이지](../assets/ui/connect-destinations/catalog.png)

1. 대상에 대한 기존 연결이 있는지 여부에 따라 다음 중 하나를 볼 수 있습니다 **[!UICONTROL 설정]** 또는 **[!UICONTROL 세그먼트 활성화]** 단추를 클릭합니다. 차이점에 대한 자세한 정보 **[!UICONTROL 세그먼트 활성화]** 및 **[!UICONTROL 설정]**&#x200B;를 참조하려면 [카탈로그](../ui/destinations-workspace.md#catalog) 대상 작업 공간 설명서의 섹션을 참조하십시오.

   다음 중 하나를 선택합니다 **[!UICONTROL 설정]** 또는 **[!UICONTROL 세그먼트 활성화]**&#x200B;사용할 수 있는 버튼에 따라 다릅니다.

   ![카탈로그 페이지](../assets/ui/connect-destinations/set-up.png)

   ![세그먼트 활성화](../assets/ui/connect-destinations/activate-segments.png)

1. 선택한 경우 **[!UICONTROL 설정]**&#x200B;를 눌러 다음 단계로 이동합니다.

   선택한 경우 **[!UICONTROL 세그먼트 활성화]**&#x200B;기존 대상 연결 목록을 볼 수 있습니다.

   선택 **[!UICONTROL 새 대상 구성]**.

   ![새 대상 구성](../assets/ui/connect-destinations/configure-new-destination.png)

1. 대상 플랫폼 연결 세부 정보를 입력한 다음 을 선택합니다 **[!UICONTROL 대상에 연결]**.

   >[!NOTE]
   >
   >아래 이미지는 일러스트레이션용으로만 사용됩니다. 대상 연결 세부 사항은 대상에 따라 다릅니다. 대상에 대한 연결 세부 정보에 대한 자세한 내용은 **연결 매개 변수** 각 섹션에 [대상 카탈로그](../catalog/overview.md) 페이지(예: [Google 고객 일치](..//catalog/advertising/google-customer-match.md#parameters)).

   ![대상에 연결](../assets/ui/connect-destinations/connect-destination.png)

1. (선택 사항) 가입하려는 대상 데이터 흐름 경고를 선택합니다. 데이터 흐름을 만들 때 경고를 구독하면 흐름 실행 상태, 성공 또는 실패와 관련된 경고 메시지를 받을 수 있습니다. 자세한 내용은 [컨텍스트 내 대상 경고 구독](alerts.md) 대상 데이터 흐름 경고에 대한 자세한 정보.

   ![컨텍스트 내 대상 경고 구독 옵션을 보여주는 UI 이미지](../assets/ui/connect-destinations/subscribe-to-alerts.png)

1. **[!UICONTROL 다음]**&#x200B;을 선택합니다.

   ![대상에 연결](../assets/ui/connect-destinations/next.png)

1. 대상으로 내보내려는 데이터에 적용할 수 있는 마케팅 작업을 선택합니다. 마케팅 작업은 대상으로 데이터를 내보낼 의도를 나타냅니다. Adobe 정의 마케팅 작업에서 선택하거나 고유한 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../data-governance/policies/overview.md) 페이지.

   ![마케팅 작업 선택](../assets/ui/connect-destinations/governance.png)

1. 선택 **[!UICONTROL 저장 및 종료]** 대상 구성을 저장하려면 **[!UICONTROL 다음]** 대상 데이터로 진행합니다 [활성화 흐름](activation-overview.md).