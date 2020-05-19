---
title: 소셜 네트워크 대상 워크플로우
seo-title: 소셜 네트워크 대상 워크플로우
description: 소셜 네트워크 및 계정에 연결하는 지침
seo-description: 소셜 네트워크 및 계정에 연결하는 지침
translation-type: tm+mt
source-git-commit: ab53e2efffed536e8028beabd64aee843d1eeee8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# 소셜 네트워크 대상 인증 워크플로 {#social-network-destinations-workflow}

## 소셜 네트워크 대상을 만드는 워크플로

이 자습서는 Facebook을 예로 사용하지만 제품에 한 번 더 추가되면 Adobe 실시간 고객 데이터 플랫폼의 워크플로우는 모든 소셜 네트워크 대상에 대해 동일합니다.

1. 대상 **[!UICONTROL > 카탈로그에서]****[!UICONTROL 소셜]** 카테고리로 스크롤합니다. 원하는 소셜 네트워크 대상을 선택한 다음 **[!UICONTROL 연결 대상을 선택합니다]**.

   ![소셜 네트워크 대상에 연결](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 이전에 소셜 네트워크 대상에 대한 연결을 **설정한 경우 인증** 단계에서 기존 계정 **[!UICONTROL 을]** 선택하고 기존 연결을 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 소셜 네트워크 대상에 대한 새 연결을 설정할 수 있습니다. 대상에 **[!UICONTROL 연결을]** 선택하면 선택한 소셜 네트워크 대상으로 이동하여 로그인하고 Adobe Experience Cloud를 소셜 네트워크 광고 계정에 연결합니다.

   >[!NOTE]
   >
   >Adobe 실시간 CDP는 인증 프로세스의 자격 증명 유효성 검사를 지원하고 소셜 네트워크 계정 ID에 잘못된 자격 증명을 입력한 경우 오류 메시지를 표시합니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![소셜 네트워크 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 자격 증명이 확인되고 Adobe Experience Cloud가 소셜 네트워크에 연결되면 **[!UICONTROL 다음]** 을 선택하여 **[!UICONTROL 설정]** 단계로 진행할 수 있습니다.

   ![자격 증명 확인됨](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 설정 **[!UICONTROL 단계에서]** **[!UICONTROL 이름]** 과 **[!UICONTROL 활성화]** 과정에 대한 설명 **[!UICONTROL 을 입력하고 소셜 네트워크 및 계정의]** 계정 ID를 입력합니다. 이 대상에 적용할 마케팅 사용 사례를 선택합니다. 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

   >[!IMPORTANT]
   >
   > Facebook 대상. **[!UICONTROL 계정 ID는]** Facebook 광고 계정 ID입니다. Facebook 광고 관리자에서 이 ID를 찾을 수 있습니다. 아래 표시된 대로 ID에 접두사를 `act_` 붙입니다.

   ![소셜 네트워크 대상에 연결 - 설정 단계](/help/rtcdp/destinations/assets/social-network-setup-step.png)

5. 이제 대상이 만들어집니다. 나중에 세그먼트 **[!UICONTROL 를]** 활성화하려면 저장 및 종료를 **[!UICONTROL 선택하거나]** 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 다음 섹션, 소셜 네트워크에 세그먼트 [활성화](#activate-segments), 나머지 작업 과정을 참조하십시오.

## 소셜 네트워크에 세그먼트 활성화 {#activate-segments}

소셜 네트워크에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).


<!--

// update IMPORTANT note in step 4 after marketing use cases are released for RTCDP

    >[!IMPORTANT]
    >
    > * The *Single Identity Personalization* marketing use case is selected by default for social network destinations and cannot be removed. 
    > * For Facebook destinations. **[!UICONTROL Account ID]** is your Facebook Ad Account ID. You can find this ID in the Facebook Ads Manager. Prefix the ID with `act_` as shown below: 

    ![Connect to social network destination - setup step](/help/rtcdp/destinations/assets/social-networks-setup-step.png)