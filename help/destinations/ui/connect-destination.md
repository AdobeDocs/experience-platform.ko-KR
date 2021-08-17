---
keywords: 대상 연결;대상 연결;대상 연결 방법
title: 새 대상 연결 만들기
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform에서 대상에 연결하는 단계를 보여줍니다
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# 새 대상 연결 만들기

## 개요 {#overview}

대상 데이터를 대상에 보내려면 먼저 대상 플랫폼에 연결을 설정해야 합니다. 이 문서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 새 대상을 설정하는 방법을 보여 줍니다.

## 새 대상 연결 만들기 {#setup}

### 대상 선택 {#select-destination}

1. **[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;으로 이동하고 **[!UICONTROL 카탈로그]** 탭을 선택합니다.

   ![카탈로그 페이지](../assets/ui/connect-destinations/catalog.png)

1. 대상에 대한 기존 연결이 있는지 여부에 따라 대상 카드에 **[!UICONTROL 구성]** 또는 **[!UICONTROL 활성화]** 단추가 표시됩니다. **[!UICONTROL Activate]** 및 **[!UICONTROL Configure]**&#x200B;의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오. 사용 가능한 단추에 따라 **[!UICONTROL 구성]** 또는 **[!UICONTROL 활성화]**&#x200B;를 선택합니다.

   ![카탈로그 페이지](../assets/ui/connect-destinations/set-up.png)

   ![세그먼트 활성화](../assets/ui/connect-destinations/activate-segments.png)

<!-- 1. If you selected **[!UICONTROL Set up]**, skip this step. If you selected **[!UICONTROL Activate segments]**, you can now see a list of the existing destination connections. Select **[!UICONTROL Configure new destination]**.

   ![Configure new destination](../assets/ui/connect-destinations/configure-new-destination.png) -->

### 계정 단계 {#account}

대상에 새 연결을 설정하려면 **[!UICONTROL 새 계정]**&#x200B;을 선택합니다. 또는 이전에 대상에 대한 연결을 설정한 경우 **[!UICONTROL 기존 계정]**&#x200B;을 선택하고 기존 연결을 선택합니다.

계정 단계에서 입력해야 하는 자격 증명은 대상 및 인증 유형에 따라 다릅니다.

* 클라우드 스토리지 대상의 경우 스토리지 위치에 연결하기 위해 Experience Platform이 자격 증명을 제공해야 합니다.

   ![클라우드 스토리지 대상의 계정 유형 선택](../assets/ui/connect-destinations/new-account-cloud-storage.png)

* facebook 및 기타 여러 소셜 및 광고 대상의 경우, **[!UICONTROL 새 계정]** 을 선택한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을 선택합니다. 대상 로그인 페이지로 이동하여 대상에 Experience Platform을 연결할 수 있습니다.

   ![소셜 대상에 대한 계정 유형 선택](../assets/ui/connect-destinations/new-account.png)

>[!IMPORTANT]
>
>이 단계에서 필요한 매개 변수에 대한 자세한 내용은 각 대상 카탈로그 페이지의 **[!UICONTROL 연결 매개 변수]** 섹션을 참조하십시오(예: [Azure Blob](../catalog/cloud-storage/azure-blob.md#parameters)에는 연결 문자열이 필요).

### 인증 단계 {#authentication}

대상 플랫폼 연결 세부 정보를 입력한 다음 **[!UICONTROL 대상 만들기]**&#x200B;를 선택합니다.

1. 대상으로 내보내려는 데이터에 적용할 수 있는 마케팅 작업을 선택합니다. 마케팅 작업은 대상으로 데이터를 내보낼 의도를 나타냅니다. Adobe 정의 마케팅 작업에서 선택하거나 고유한 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../data-governance/policies/overview.md) 페이지를 참조하십시오.

   >[!IMPORTANT]
   >
   >아래 이미지는 일러스트레이션용으로만 사용됩니다. 대상 연결 세부 사항은 대상에 따라 다릅니다. 대상에 대한 연결 세부 정보에 대한 자세한 내용은 각 [대상 카탈로그](../catalog/overview.md) 페이지의 **[!UICONTROL 연결 매개 변수]** 섹션을 참조하십시오(예: [Google Customer Match](../catalog/advertising/google-customer-match.md#parameters)).

   ![대상에 연결](../assets/ui/connect-destinations/connect-destination.png)

1. **[!UICONTROL 저장 및 종료]**&#x200B;를 선택하여 대상 구성을 저장하거나 **[!UICONTROL 다음]**&#x200B;을 선택하여 대상 데이터 [활성화 흐름](activation-overview.md)으로 진행합니다.