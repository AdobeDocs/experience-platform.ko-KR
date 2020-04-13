---
title: 소셜 네트워크 대상 워크플로우
seo-title: 소셜 네트워크 대상 워크플로우
description: 소셜 네트워크 및 계정에 연결하는 지침
seo-description: 소셜 네트워크 및 계정에 연결하는 지침
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (베타) 소셜 네트워크 대상 인증 워크플로 {#social-network-destinations-workflow}


>[!IMPORTANT]
>
>Adobe Real-time CDP에서 소셜 네트워크 대상을 생성하는 워크플로우는 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

## 클라우드 스토리지 대상을 만드는 워크플로우

이 자습서는 Facebook을 예로 사용하지만 Adobe 실시간 고객 데이터 플랫폼의 워크플로우는 제품에 한 번 더 추가되면 모든 소셜 네트워크 대상에 대해 동일합니다.

1. 에서 **[!UICONTROL Connections > Destinations]**&#x200B;카테고리로 스크롤합니다 **[!UICONTROL Social]** . 원하는 소셜 네트워크 대상을 선택한 다음 **[!UICONTROL Connect destination]**&#x200B;을 선택합니다.

   ![소셜 네트워크 대상에 연결](/help/rtcdp/destinations/assets/facebook-catalog-view.png)

2. 인증 **단계에서** 이전에 소셜 네트워크 대상에 대한 연결을 설정한 경우 기존 연결을 **[!UICONTROL Existing Account]** 선택하고 선택합니다. 또는 소셜 네트워크 대상에 대한 새 연결을 **[!UICONTROL New Account]** 설정하도록 선택할 수 있습니다. 선택하면 선택한 소셜 네트워크 대상으로 **[!UICONTROL Connect to destination]** 이동하여 로그인하고 Adobe Experience Cloud를 소셜 네트워크 광고 계정에 연결합니다.

   >[!NOTE]
   >
   >Adobe Real-time CDP는 인증 프로세스의 자격 증명 확인을 지원하며, 소셜 네트워크 계정 ID에 잘못된 자격 증명을 입력하면 오류 메시지가 표시됩니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![소셜 네트워크 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/facebook-pre-connect-view.png)

3. 자격 증명이 확인되고 Adobe Experience Cloud가 소셜 네트워크에 연결되면 이 **[!UICONTROL Next]** 단계를 진행하도록 선택할 수 있습니다 **[!UICONTROL Setup]** .

   ![자격 증명 확인됨](/help/rtcdp/destinations/assets/facebook-post-connection-view.png)

4. 단계에서 활성화 **[!UICONTROL Setup]** 흐름에 **[!UICONTROL Name]** 대한 a 및 a를 입력하고 소셜 네트워크 및 **[!UICONTROL Description]** **[!UICONTROL Account ID]** 계정의 정보를 입력합니다. 위의 필드를 채운 **[!UICONTROL Create Destination]** 후 선택합니다.

   >[!IMPORTANT]
   >
   >Facebook 대상. **[!UICONTROL Account ID]** Facebook 광고 계정 ID입니다. 이 ID는 Facebook 광고 관리자에서 찾을 수 있습니다. 아래 `act_` 표시된 대로 ID에 접두사를 붙입니다.

   ![소셜 네트워크 대상에 연결 - 설정 단계](/help/rtcdp/destinations/assets/social-network-step.png)

5. 이제 대상이 만들어집니다. 나중에 세그먼트를 활성화할지 **[!UICONTROL Save & Exit]** 또는 워크플로우를 계속하기 위해 선택하고 활성화할 세그먼트를 선택할 **[!UICONTROL Next]** 수 있습니다. 두 경우 모두 워크플로우의 나머지 부분에 [대해 다음 섹션인 소셜 네트워크에](#activate-segments)세그먼트 활성화를 참조하십시오.

## 소셜 네트워크에 세그먼트 활성화 {#activate-segments}

소셜 네트워크에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).