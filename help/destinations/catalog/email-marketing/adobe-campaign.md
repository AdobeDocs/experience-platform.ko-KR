---
keywords: 이메일;이메일;이메일;이메일 대상;adobe campaign;campaign;email;email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign은 온라인과 오프라인 등 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다.
seo-description: Adobe Campaign은 온라인과 오프라인 등 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다.
translation-type: tm+mt
source-git-commit: cf2d76799c03a2ea0414aedd83b35f3ce2ca3cb5
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 1%

---


# Adobe Campaign

## 개요

Adobe Campaign은 온라인과 오프라인 등 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다. 자세한 내용은 [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 정보를 참조하십시오.

세그먼트 데이터를 Adobe Campaign으로 전송하려면 먼저 Adobe Experience Platform에서 대상](#connect-destination)을 연결한 다음 [저장소 위치에서 Adobe Campaign으로 데이터 가져오기](#import-data-into-campaign)를 설정해야 합니다.[

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;에서 Adobe Campaign을 선택한 다음 **[!UICONTROL 연결 대상]**&#x200B;을 선택합니다.

![adobe campaign에 연결](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Connect 대상 작업 과정에서 저장소 위치에 대한 **[!UICONTROL 연결 유형]**&#x200B;을 선택합니다. Adobe Campaign의 경우 **[!UICONTROL Amazon S3]**, **[!UICONTROL 암호가 있는 SFTP]**, **[!UICONTROL SFTP 및**[!UICONTROL  SSH 키가 있는 SFTP ]**및 Azure Blob]** 중에서 선택할 수 있습니다. 연결 유형에 따라 아래 정보를 입력한 다음 **[!UICONTROL Connect]**&#x200B;를 선택합니다.

![캠페인 설정 마법사](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- **[!UICONTROL Amazon S3]** 연결의 경우 액세스 키 ID 및 비밀 액세스 키를 제공해야 합니다.
- 암호&#x200B;]**연결이 있는**[!UICONTROL  SFTP의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.
- **[!UICONTROL SFTP에서 SSH 키]** 연결을 사용하려면 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.
- **[!UICONTROL Azure Blob]** 연결의 경우 연결 문자열을 제공해야 합니다.

선택적으로 RSA 형식 공개 키를 첨부하여 **[!UICONTROL 키]** 섹션 아래의 내보낸 파일에 PGP/GPG를 사용하여 암호화를 추가할 수 있습니다. 이 공개 키 **는 Base64 인코딩 문자열로 기록되어야 합니다.**

![캠페인 정보 입력](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

**[!UICONTROL 기본 정보]**&#x200B;에서 아래와 같이 대상에 대한 관련 정보를 입력합니다.
- **[!UICONTROL 이름]**:대상의 관련 이름을 선택합니다.
- **[!UICONTROL 설명]**:대상에 대한 설명을 입력합니다.
- **[!UICONTROL 버킷 이름]**: *S3 연결을 참조하십시오*. S3 버킷 위치를 입력하여 Platform에서 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장합니다.
- **[!UICONTROL 폴더 경로]**:Platform에서 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 스토리지 위치에 경로를 제공합니다.
- **[!UICONTROL 컨테이너]**: *Blob 연결의 경우*. 폴더 경로가 있는 Blob가 들어 있는 컨테이너입니다.
- **[!UICONTROL 파일 형식]**: **CSV** 또는  **TAB_DIPORTED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

![캠페인 기본 정보](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

위의 필드를 채운 후 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 이제 대상이 연결되었으며 [세그먼트](../../ui/activate-destinations.md)를 대상에 활성화할 수 있습니다.

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md)에 활성화를 참조하십시오.

## 대상 특성 {#destination-attributes}

[세그먼트](../../ui/activate-destinations.md)를 Adobe Campaign 대상에 활성화하는 경우 [공용 스키마](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유한 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 마케팅 대상 문서에서 내보낸 파일](./overview.md#destination-attributes)에서 대상 특성으로 사용할 스키마 필드 선택을 참조하십시오.[

## 내보낸 데이터 {#exported-data}

[!DNL Adobe Campaign] 대상의 경우 Platform은 사용자가 제공한 저장 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.

## Adobe Campaign {#import-data-into-campaign}에 데이터 가져오기 설정

>[!IMPORTANT]
>
>- 이 통합을 수행하는 동안 Adobe Campaign 계약에 따라 SFTP 저장소 제한, 데이터베이스 저장소 제한 및 활성 프로필 제한에 주의하십시오.
>- [!DNL Campaign] 워크플로우를 사용하여 Adobe Campaign에서 내보낸 세그먼트를 예약, 가져오기 및 매핑해야 합니다. Adobe Campaign 설명서에서 [반복 가져오기](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) 설정을 참조하십시오.



플랫폼을 [!DNL Amazon S3] 또는 SFTP 스토리지에 연결한 후 저장소 위치에서 Adobe Campaign으로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 Adobe Campaign 설명서의 [데이터 가져오기](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html)를 참조하십시오.