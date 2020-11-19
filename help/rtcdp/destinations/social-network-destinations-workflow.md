---
keywords: Facebook;facebook;Social network;Social Network;social network authentication;Social network authentication
title: 소셜 네트워크 대상 워크플로우
type: Tutorial
seo-title: 소셜 네트워크 대상 워크플로우
description: 소셜 네트워크 및 계정에 연결하는 지침
seo-description: 소셜 네트워크 및 계정에 연결하는 지침
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---


# 소셜 네트워크 대상 인증 워크플로 {#social-network-destinations-workflow}

## 소셜 네트워크 대상을 만드는 워크플로

이 자습서는 예를 [!DNL Facebook] 들어 사용하지만 제품에 한 번 더 추가되면 실시간 고객 데이터 플랫폼의 워크플로우는 모든 소셜 네트워크 대상에 대해 동일합니다.

1. 대상 **** > **[!UICONTROL 카탈로그]**&#x200B;에서 **[!UICONTROL Social]** 카테고리로스크롤합니다. 원하는 소셜 네트워크 대상을 선택한 다음 구성을 **[!UICONTROL 선택합니다]**.

   ![소셜 네트워크 대상에 연결](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

   >[!NOTE]
   >
   >이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 **[!UICONTROL 의 차이에 대한 자세한]****[!UICONTROL 내용은 대상 작업 공간 설명서의]**&#x200B;카탈로그 [섹션을](/help/rtcdp/destinations/destinations-workspace.md#catalog) 참조하십시오.

2. 이전에 소셜 네트워크 대상에 대한 연결을 **설정한 경우 인증** 단계에서 기존 계정 **[!UICONTROL 을]** 선택하고 기존 연결을 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 소셜 네트워크 대상에 대한 새 연결을 설정할 수 있습니다. 대상에 **[!UICONTROL 연결을]** 선택하면 선택한 소셜 네트워크 대상으로 로그인하여 소셜 네트워크 광고 계정에 Adobe Experience Cloud을 연결합니다.

   >[!NOTE]
   >
   >Adobe 실시간 CDP는 인증 프로세스의 자격 증명 유효성 검사를 지원하고 소셜 네트워크 계정 ID에 잘못된 자격 증명을 입력한 경우 오류 메시지를 표시합니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![소셜 네트워크 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 자격 증명이 확인되고 Adobe Experience Cloud이 소셜 네트워크에 연결되면 **[!UICONTROL 다음]** 을 선택하여 **[!UICONTROL 설정]** 단계를 진행할 수 있습니다.

   ![자격 증명 확인됨](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 설정 **[!UICONTROL 단계에서]** [!UICONTROL 이름] 과 [!UICONTROL 활성화] 과정에 대한 설명 [!UICONTROL 을 입력하고 소셜 네트워크 및 계정의] 계정 ID를 입력합니다. <br> 또한 이 단계에서는 이 대상에 **[!UICONTROL 적용되어야 하는 모든]** 마케팅 사용 사례를 선택할 수 있습니다. 마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](/help/rtcdp/privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](/help/data-governance/policies/overview.md#core-actions). <br> 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

   >[!IMPORTANT]
   >
   > * 소셜 네트워크 *대상에 대해 기본적으로 단일 ID 개인화* 마케팅 사용 사례가 선택되므로 제거할 수 없습니다.
   > * 대상 [!DNL Facebook] 을 참조하십시오. **[!UICONTROL 계정 ID가]** 귀하의 [!DNL Facebook Ad Account ID]것입니다. 이 ID는 [!DNL Facebook Ads Manager] 아래 표시된 대로 ID에 접두사를 `act_` 붙입니다.


   ![소셜 네트워크 대상에 연결 - 설정 단계](/help/rtcdp/destinations/assets/social-networks-setup-step.png)

5. 이제 대상이 만들어집니다. 나중에 세그먼트 **[!UICONTROL 를]** 활성화하려면 저장 및 종료를 **[!UICONTROL 선택하거나]** 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 다음 섹션, 소셜 네트워크에 세그먼트 [활성화](#activate-segments), 나머지 작업 과정을 참조하십시오.

## 소셜 네트워크에 세그먼트 활성화 {#activate-segments}

소셜 네트워크에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).