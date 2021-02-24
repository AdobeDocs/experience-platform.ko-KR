---
keywords: Facebook;Facebook;소셜 네트워크;소셜 네트워크;소셜 네트워크 인증;소셜 네트워크 인증;Facebook;facebook;Social network authentication;Social network authentication
title: 소셜 네트워크 대상 만들기
type: 튜토리얼
description: Adobe Experience Platform에서 소셜 네트워크 및 계정에 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 19e38faa84d365682e97c2ec1c6352d127c0ac29
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---


# 소셜 네트워크 대상 {#social-network-destinations-workflow} 만들기

이 자습서에서는 [!DNL Facebook]을(를) 예로 사용하지만 Adobe Experience Platform 워크플로우는 모든 소셜 네트워크 대상에 대해 동일합니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;에서 **[!UICONTROL 소셜]** 범주로 스크롤합니다. 원하는 소셜 네트워크 대상을 선택한 다음 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![소셜 네트워크 대상에 연결](../../assets/catalog/social/workflow/catalog.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시될 수 있습니다. **[!UICONTROL 활성화]**&#x200B;와 **[!UICONTROL 구성]**&#x200B;의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.

**인증** 단계에서 소셜 네트워크 대상에 대한 연결을 이전에 설정한 경우 **[!UICONTROL 기존 계정]**&#x200B;을 선택하고 기존 연결을 선택합니다. 또는 **[!UICONTROL 새 계정]**&#x200B;을 선택하여 소셜 네트워크 대상에 대한 새 연결을 설정할 수 있습니다. **[!UICONTROL 대상에 연결]**&#x200B;을 선택하면 선택한 소셜 네트워크 대상으로 이동하여 로그인하고 Adobe Experience Cloud을 소셜 네트워크 광고 계정에 연결합니다.

>[!NOTE]
>
>플랫폼은 인증 프로세스의 자격 증명 유효성 검사를 지원하고 소셜 네트워크 계정 ID에 잘못된 자격 증명을 입력하는 경우 오류 메시지를 표시합니다. 이렇게 하면 자격 증명이 잘못된 작업 흐름을 완료하지 못합니다.

![소셜 네트워크 대상에 연결 - 인증 단계](../../assets/catalog/social/workflow/pre-connect.png)

자격 증명이 확인되고 Adobe Experience Cloud이 소셜 네트워크에 연결되면 **[!UICONTROL 다음]**&#x200B;을 선택하여 **[!UICONTROL 설정]** 단계로 진행할 수 있습니다.

![자격 증명 확인](../../assets/catalog/social/workflow/post-connect.png)

**[!UICONTROL 설정]** 단계에서 활성화 플로우에 [!UICONTROL 이름] 및 [!UICONTROL 설명]을 입력하고 소셜 네트워크 광고 계정의 [!UICONTROL 계정 ID]을 입력합니다.

>[!IMPORTANT]
>
> [!DNL Facebook] 대상의 경우 **[!UICONTROL 계정 ID]**&#x200B;는 [!DNL Facebook Ad Account ID]입니다. 이 ID는 [!DNL Facebook Ads Manager]에서 찾을 수 있습니다. 아래 표시된 대로 ID에 `act_`을(를) 접두어로 지정합니다.

![소셜 네트워크 대상에 연결 - 설정 단계](../../assets/catalog/social/workflow/setup.png)

>[!IMPORTANT]
>
> [!DNL LinkedIn] 대상의 경우 **[!UICONTROL 계정 ID]**&#x200B;는 [!DNL LinkedIn Campaign Manager Account ID]입니다. 이 ID는 [!DNL LinkedIn Campaign Manager]에서 찾을 수 있습니다.

또한 이 단계에서 이 대상에 적용할 **[!UICONTROL 마케팅 작업]**&#x200B;을 선택할 수 있습니다. 마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

위의 필드를 채운 후 **[!UICONTROL 대상 만들기]**&#x200B;를 선택합니다.

이제 대상이 만들어집니다. 나중에 세그먼트를 활성화하려면 **[!UICONTROL 저장 및 종료]**&#x200B;을 선택하고, **[!UICONTROL 다음]**&#x200B;을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 이 두 경우 모두 워크플로우의 나머지 부분에 대해서는 다음 섹션 [소셜 네트워크에 세그먼트 활성화](#activate-segments)를 참조하십시오.

## 세그먼트를 소셜 네트워크에 활성화 {#activate-segments}

소셜 네트워크에 세그먼트를 활성화하는 방법에 대한 지침은 [대상에 데이터 활성화](../../ui/activate-destinations.md)를 참조하십시오.