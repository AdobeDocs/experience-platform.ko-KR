---
title: 클라우드 스토리지 대상 워크플로우
seo-title: 클라우드 스토리지 대상 워크플로우
description: 클라우드 스토리지 위치에 연결하는 지침
seo-description: 클라우드 스토리지 위치에 연결하는 지침
translation-type: tm+mt
source-git-commit: c4f1c0a6ef4d16e5fe763826016d56506fdca5dc

---


# 클라우드 스토리지 대상을 만드는 워크플로우

## 개요

이 페이지에서는 Adobe 실시간 고객 데이터 플랫폼의 클라우드 스토리지 위치에 연결하는 방법을 설명합니다.

1. 에서 **[!UICONTROL Connections > Destinations]**&#x200B;원하는 클라우드 스토리지 대상을 선택한 다음 **[!UICONTROL Connect destination]**&#x200B;을 선택합니다.

   ![클라우드 스토리지 대상에 연결](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

1. 인증 **단계에서** 이전에 클라우드 스토리지 대상에 대한 연결을 설정한 경우 기존 연결을 **[!UICONTROL Existing Account]** 선택하고 선택합니다. 또는 클라우드 스토리지 대상에 대한 새 연결을 **[!UICONTROL New Account]** 설정하도록 선택할 수 있습니다. 계정 인증 자격 증명을 입력하고 **[!UICONTROL Connect to destination]**&#x200B;선택합니다. 인증 [단계의 자격 증명 입력에 대한 자세한 내용은 Amazon S3 대상](/help/rtcdp/destinations/amazon-s3-destination.md) 및 [SFTP 대상을](/help/rtcdp/destinations/sftp-destination.md) **** 참조하십시오.

   >[!NOTE]
   >
   >Adobe Real-time CDP는 인증 프로세스의 자격 증명 확인을 지원하며 클라우드 스토리지 위치에 잘못된 자격 증명을 입력하면 오류 메시지가 표시됩니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![클라우드 스토리지 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

1. 단계에서 활성화 흐름에 대해 a **[!UICONTROL Setup]** 및 **[!UICONTROL Name]** **[!UICONTROL Description]** a를 입력합니다. <br>
Amazon S3 대상의 경우, 파일이 배달될 클라우드 스토리지 대상에 **[!UICONTROL Bucket name]** 및 **[!UICONTROL Folder path]** 를 삽입합니다. 위의 필드를 채운 **[!UICONTROL Create Destination]** 후 선택합니다.

   ![Amazon S3 클라우드 스토리지 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)



   <br>SFTP 대상의 경우 **[!UICONTROL Folder path]**

   ![SFTP 클라우드 저장소 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

1. 이제 대상이 만들어집니다. 나중에 세그먼트를 활성화할지 **[!UICONTROL Save & Exit]** 또는 워크플로우를 계속하기 위해 선택하고 활성화할 세그먼트를 선택할 **[!UICONTROL Next]** 수 있습니다. 두 경우 모두, 나머지 워크플로우에서 [데이터를 내보낼 다음 섹션인 세그먼트](#activate-segments)활성화를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 프로필과 세그먼트를 대상에](/help/rtcdp/destinations/activate-destinations.md) 활성화를 참조하십시오.