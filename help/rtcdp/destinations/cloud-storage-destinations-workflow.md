---
title: 클라우드 스토리지 대상 워크플로우
seo-title: 클라우드 스토리지 대상 워크플로우
description: 클라우드 스토리지 위치에 연결하는 지침
seo-description: 클라우드 스토리지 위치에 연결하는 지침
translation-type: tm+mt
source-git-commit: 37c51435ce8330dbd61857bda408df03ff21a491
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# 클라우드 스토리지 대상을 만드는 워크플로우

## 개요

이 페이지에서는 Adobe 실시간 고객 데이터 플랫폼의 클라우드 스토리지 위치에 연결하는 방법을 설명합니다.

1. [ **[!UICONTROL 연결] > [대상]**]에서 원하는 클라우드 저장소 대상을 선택한 다음 **[!UICONTROL Connect 대상을 선택합니다]**.

   ![클라우드 스토리지 대상에 연결](/help/rtcdp/destinations/assets/connect-cloud-destination.png)

2. 이전에 클라우드 스토리지 대상에 대한 연결을 **[!UICONTROL 설정한 경우 인증]** 단계에서 기존 계정 **[!UICONTROL 을]** 선택하고 기존 연결을 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 클라우드 스토리지 대상에 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 대상에 **[!UICONTROL 연결을 선택합니다]**. <br> Amazon [S3](/help/rtcdp/destinations/amazon-s3-destination.md) 대상, [Amazon Kinesis](/help/rtcdp/destinations/amazon-kinesis-destination.md) 대상, [Azure 이벤트 허브](/help/rtcdp/destinations/azure-event-hubs-destination.md) 대상 및 SFTP 대상 [](/help/rtcdp/destinations/sftp-destination.md) **** 에서 Facebook 인증 단계에서 자격 증명 입력에 대한 자세한 내용을 보려면 Amazon S3 대상을 참조하십시오.

   >[!NOTE]
   >
   >Adobe 실시간 CDP는 인증 프로세스의 자격 증명 확인을 지원하며 클라우드 스토리지 위치에 잘못된 자격 증명을 입력하는 경우 오류 메시지를 표시합니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![클라우드 스토리지 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/cloud-destinations-authentication-step.png)

3. 설정 **** 단계 **[!UICONTROL 에서]** 활성화 과정 **[!UICONTROL 에 대한 이름]** 및설명을입력합니다. <br>
Amazon S3 대상의 경우, 파일이 배달될 클라우드 스토리지 대상에 **[!UICONTROL 버킷 이름]** 및 **[!UICONTROL 폴더 경로를]** 삽입합니다. 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

   ![Amazon S3 클라우드 스토리지 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/cloud-destinations-setup-step.png)

   SFTP 대상의 경우 파일이 배달될 **[!UICONTROL 폴더 경로를]** 삽입합니다.

   ![SFTP 클라우드 저장소 대상에 연결 - 인증 단계](/help/rtcdp/destinations/assets/sftp-destinations-setup-step.png)

4. 이제 대상이 만들어집니다. 나중에 세그먼트 **[!UICONTROL 를]** 활성화하려면 저장 및 종료를 **[!UICONTROL 선택하거나]** 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 두 경우 모두, 나머지 워크플로우에서 데이터 [를 내보내기 위해 다음 섹션, 세그먼트](#activate-segments)활성화를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](/help/rtcdp/destinations/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.