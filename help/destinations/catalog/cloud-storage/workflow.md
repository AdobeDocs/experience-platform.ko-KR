---
keywords: cloud storage destination;cloud storage
title: 클라우드 스토리지 대상 워크플로우
seo-title: 클라우드 스토리지 대상 워크플로우
type: Tutorial
description: 클라우드 스토리지 위치에 연결하는 지침
seo-description: 클라우드 스토리지 위치에 연결하는 지침
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---


# 클라우드 스토리지 대상을 만드는 워크플로우

## 개요

이 페이지에서는 실시간 고객 데이터 플랫폼의 클라우드 스토리지 위치에 연결하는 방법을 설명합니다.

[ **[!UICONTROL 연결]** ] > **[!UICONTROL 대상]**]에서 원하는 클라우드 스토리지 대상을 선택한 다음 구성을 **[!UICONTROL 선택합니다]**.

![클라우드 스토리지 대상에 연결](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 **[!UICONTROL 의 차이에 대한 자세한]****[!UICONTROL 내용은 대상 작업 공간 설명서의]**&#x200B;카탈로그 [섹션을](../../ui/destinations-workspace.md#catalog) 참조하십시오.

이전에 클라우드 스토리지 대상에 대한 연결을 **[!UICONTROL 설정한 경우 인증]** 단계에서 기존 계정 **[!UICONTROL 을]** 선택하고 기존 연결을 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 클라우드 스토리지 대상에 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 대상에 **[!UICONTROL 연결을 선택합니다]**. RSA 형식 공개 키를 연결하여 내보낸 파일에 암호화를 추가할 수도 있습니다. 이 공개 키는 Base64 인코딩 문자열로 **작성해야** 합니다.

인증 단계에서 입력한 자격 증명에 대한 자세한 내용은 [Amazon S3](./amazon-s3.md)[[!DNL Amazon Kinesis]](./amazon-kinesis.md) 대상, 대상, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) 대상 및 [SFTP](./sftp.md) 대상을 **** 참조하십시오.

>[!NOTE]
>
>실시간 CDP는 인증 프로세스의 자격 증명 확인을 지원하며 클라우드 스토리지 위치에 잘못된 자격 증명을 입력하는 경우 오류 메시지를 표시합니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

![클라우드 스토리지 대상에 연결 - 인증 단계](../../assets/catalog/cloud-storage/workflow/destination-account.png)

설정 **** 단계 **[!UICONTROL 에서]** 활성화 과정 **[!UICONTROL 에 대한 이름]** 및설명을입력합니다.

또한 이 단계에서는 이 대상에 **[!UICONTROL 적용되어야 하는 모든]** 마케팅 사용 사례를 선택할 수 있습니다. 마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](../../../rtcdp/privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](../../../data-governance/policies/overview.md#core-actions).

Amazon S3 대상의 경우, 파일이 배달될 클라우드 스토리지 대상에 **[!UICONTROL 버킷 이름]** 및 **[!UICONTROL 폴더 경로]** 를 삽입합니다. 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

![Amazon S3 클라우드 스토리지 대상에 연결 - 인증 단계](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

SFTP 대상의 경우 파일이 배달될 **[!UICONTROL 폴더 경로를]** 삽입합니다. 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

![SFTP 클라우드 저장소 대상에 연결 - 인증 단계](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

대상의 경우 [!DNL Amazon Kinesis] 계정에 있는 기존 데이터 스트림의 이름을 [!DNL Amazon Kinesis] 입력합니다. 실시간 CDP는 데이터를 이 스트림으로 내보냅니다. 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

![Kinesis 클라우드 스토리지 대상에 연결 - 인증 단계](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

대상의 경우 [!DNL Azure Event Hubs] 계정에 있는 기존 데이터 스트림의 이름을 [!DNL Amazon Event Hubs] 입력합니다. 실시간 CDP는 데이터를 이 스트림으로 내보냅니다. 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

![이벤트 허브 클라우드 스토리지 대상에 연결 - 인증 단계](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

이제 대상이 만들어집니다. 나중에 세그먼트 **[!UICONTROL 를]** 활성화하려면 저장 및 종료를 **[!UICONTROL 선택하거나]** 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 두 경우 모두, 나머지 워크플로우에서 데이터 [를 내보내기 위해 다음 섹션, 세그먼트](#activate-segments)활성화를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](../../ui/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.