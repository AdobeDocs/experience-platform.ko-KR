---
title: 클라우드 스토리지 대상 워크플로우
seo-title: 클라우드 스토리지 대상 워크플로우
description: 클라우드 스토리지 위치에 연결하는 지침
seo-description: 클라우드 스토리지 위치에 연결하는 지침
translation-type: tm+mt
source-git-commit: 225f18bd0d092bdae7b4cc99c278e850be9cfd56

---


# 클라우드 스토리지 대상을 만드는 워크플로우

## 개요

이 페이지에서는 Adobe 실시간 고객 데이터 플랫폼의 클라우드 스토리지 위치에 연결하는 방법을 설명합니다.

1. [ **[!UICONTROL 연결] > [대상]**]에서 원하는 클라우드 저장소 대상을 선택한 다음 [연결 대상] **[!UICONTROL 을]**&#x200B;선택합니다.

   ![클라우드 스토리지 대상에 연결](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. 인증 **단계에서** 이전에 클라우드 스토리지 대상에 대한 연결을 설정한 경우 기존 계정을 **[!UICONTROL 선택하고]** 기존 연결을 선택합니다. 또는 새 계정을 선택하여 **[!UICONTROL 클라우드]** 스토리지 대상에 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 대상에 **[!UICONTROL 연결을]**&#x200B;선택합니다.

   >[!NOTE]
   >
   >Adobe Real-time CDP는 인증 프로세스의 자격 증명 확인을 지원하며 클라우드 스토리지 위치에 잘못된 자격 증명을 입력하면 오류 메시지가 표시됩니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![클라우드 스토리지 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 설정 **[!UICONTROL 단계에서]** 활성화 **[!UICONTROL 흐름에 대한 이름]** 및 **[!UICONTROL 대상을]** 입력하고 **[!UICONTROL 클라우드 스토리지 대상에]** 파일을 전달할 폴더 경로를 삽입합니다. 위의 **[!UICONTROL 필드를]** 채운 후 대상 만들기를 선택합니다.

   ![클라우드 스토리지 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

4. 이제 대상이 만들어집니다. 나중에 세그먼트를 **[!UICONTROL 활성화하거나]** 다음을 선택하여 워크플로우를 **[!UICONTROL 계속하고 활성화할 세그먼트를 선택할 수]** 있습니다. 두 경우 모두 다음 섹션인 [세그먼트](#activate-segments)활성화를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 프로필과 세그먼트를 대상에](/help/rtcdp/destinations/activate-destinations.md) 활성화를 참조하십시오.