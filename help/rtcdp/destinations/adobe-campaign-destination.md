---
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 세트입니다.
seo-description: Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 세트입니다.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Adobe Campaign

## 개요

Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 세트입니다. 자세한 [내용은 Adobe Campaign](https://docs.adobe.com/content/help/en/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) Classic 정보를 참조하십시오.

세그먼트 데이터를 Adobe Campaign으로 전송하려면 먼저 Adobe 실시간 고객 데이터 플랫폼에서 대상을 [](#connect-destination) 연결한 다음 스토리지 위치에서 Adobe Campaign으로 데이터 가져오기를 [](#import-data-into-campaign) 설정해야 합니다.

## 연결 대상 {#connect-destination}

1. 에서 **[!UICONTROL Connections > Destinations]** Adobe Campaign을 선택한 다음 **[!UICONTROL Connect destination]**&#x200B;선택합니다.

   ![Adobe 캠페인에 연결](/help/rtcdp/destinations/assets/connect-adobe-campaign.png)

1. Connect 대상 워크플로우에서 저장소 위치에 **[!UICONTROL Connection type]** 사용할 항목을 선택합니다. Adobe Campaign의 경우, **[!UICONTROL Amazon S3]**&#x200B;및 **[!UICONTROL SFTP with Password]** 을 선택할 수 **[!UICONTROL SFTP with SSH Key]**&#x200B;있습니다. 연결 유형에 따라 아래 정보를 입력한 다음 을 **[!UICONTROL Connect]**&#x200B;선택합니다.

   ![캠페인 설정 마법사](/help/rtcdp/destinations/assets/adobe-campaign-wizard.png)

   연결의 **[!UICONTROL Amazon S3]** 경우 액세스 키 ID 및 비밀 액세스 키를 제공해야 합니다.
연결의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 **[!UICONTROL SFTP with Password]** 합니다.
연결의 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 **[!UICONTROL SFTP with SSH Key]** 합니다.

   ![캠페인 정보 입력](/help/rtcdp/destinations/assets/adobe-campaign-step2.png)

1. 에서 **[!UICONTROL Basic Information]**&#x200B;아래 표시된 대로 대상에 대한 관련 정보를 입력합니다.
   * **[!UICONTROL Name]**:대상의 관련 이름을 선택합니다.
   * **[!UICONTROL Description]**:대상에 대한 설명을 입력합니다.
   * **[!UICONTROL Bucket Name]**:S3 *연결에*&#x200B;대해. S3 버킷의 위치를 입력하여 실시간 CDP를 통해 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 수 있습니다.
   * **[!UICONTROL Folder Path]**:실시간 CDP를 통해 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 스토리지 위치에 경로를 제공합니다.
   * **[!UICONTROL File Format]**:CSV ******또는** TAB_SEPARATED. 저장소 위치로 내보낼 파일 형식을 선택합니다.
   ![캠페인 기본 정보](/help/rtcdp/destinations/assets/adobe-campaign-basic-information.png)

1. 위의 필드를 채운 **[!UICONTROL Create]** 후 을 클릭합니다. 대상이 연결되었으며 세그먼트를 [대상에](/help/rtcdp/destinations/activate-destinations.md) 활성화할 수 있습니다.

## 대상 속성 {#destination-attributes}

세그먼트를 [Adobe Campaign 대상으로](/help/rtcdp/destinations/activate-destinations.md) 활성화할 때에는 [조합 스키마에서](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 마케팅 [대상의 내보낸 파일에서](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 대상 특성으로 사용할 스키마 필드 선택을 참조하십시오.


## Adobe Campaign으로 데이터 가져오기 설정 {#import-data-into-campaign}

실시간 CDP를 Amazon S3 또는 SFTP 스토리지에 연결한 후 스토리지 위치에서 Adobe Campaign으로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 Adobe [Campaign 도움말](https://docs.adobe.com/content/help/en/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 설명서의 데이터 가져오기를 참조하십시오.