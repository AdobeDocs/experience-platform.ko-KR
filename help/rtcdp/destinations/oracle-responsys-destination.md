---
title: Oracle Responsys 대상
seo-title: Oracle Responsys 대상
description: Responsys는 이메일, 모바일, 디스플레이 및 소셜 간의 상호 작용을 개인화하기 위해 Oracle에서 제공하는 크로스채널 마케팅 캠페인을 위한 기업 이메일 마케팅 툴입니다.
seo-description: Responsys는 이메일, 모바일, 디스플레이 및 소셜 간의 상호 작용을 개인화하기 위해 Oracle에서 제공하는 크로스채널 마케팅 캠페인을 위한 기업 이메일 마케팅 툴입니다.
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# Oracle Responsys

## 개요

[Responsys는](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 이메일, 모바일, 디스플레이 및 소셜 간의 상호 작용을 개인화하기 위해 Oracle에서 제공하는 크로스채널 마케팅 캠페인을 위한 기업 이메일 마케팅 툴입니다.

세그먼트 데이터를 Oracle Responsys로 전송하려면 먼저 Adobe 실시간 고객 데이터 플랫폼의 대상에 [](#connect-destination) 연결한 다음 저장 위치에서 Oracle Responsys로 데이터 가져오기를 [](#import-data-into-responsys) 설정해야 합니다.

## 연결 대상 {#connect-destination}

1. 에서 **[!UICONTROL Connections > Destinations]** Oracle Responsys를 선택한 다음 **[!UICONTROL Connect destination]**&#x200B;선택합니다.

   ![Responsys에 연결](/help/rtcdp/destinations/assets/connect-oracle-responsys.png)

2. 이전에 클라우드 스토리지 대상에 대한 연결을 설정한 **[!UICONTROL Authentication]** 경우 기존 연결 중 하나를 선택하고 **[!UICONTROL Existing Account]** 선택합니다. 또는 새 연결을 **[!UICONTROL New Account]** 설정하도록 선택할 수 있습니다. 계정 인증 자격 증명을 입력하고 **[!UICONTROL Connect to destination]**&#x200B;선택합니다. Oracle Responsys의 경우 **[!UICONTROL SFTP with Password]** 와 중 하나를 선택할 수 **[!UICONTROL SFTP with SSH Key]**&#x200B;있습니다. 연결 유형에 따라 아래 정보를 입력하고 **[!UICONTROL Connect to destination]**&#x200B;선택합니다.

   연결의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 **[!UICONTROL SFTP with Password]** 합니다.
연결의 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 **[!UICONTROL SFTP with SSH Key]** 합니다.

   ![Responsys 정보 입력](/help/rtcdp/destinations/assets/responsys-authentication.png)

3. 단계에서 **[!UICONTROL Setup]** 아래 표시된 대로 대상에 대한 관련 정보를 입력합니다.
   * **[!UICONTROL Name]**:대상의 관련 이름을 선택합니다.
   * **[!UICONTROL Description]**:대상에 대한 설명을 입력합니다.
   * **[!UICONTROL Folder Path]**:실시간 CDP를 통해 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 스토리지 위치에 경로를 제공합니다.
   * **[!UICONTROL File Format]**:CSV ******또는** TAB_SEPARATED. 저장소 위치로 내보낼 파일 형식을 선택합니다.
   ![Responsys 기본 정보](/help/rtcdp/destinations/assets/responsys-basic-information.png)

4. 위의 필드를 채운 **[!UICONTROL Create destination]** 후 을 클릭합니다. 대상이 연결되었으며 세그먼트를 [대상에](/help/rtcdp/destinations/activate-destinations.md) 활성화할 수 있습니다.

## 대상 속성 {#destination-attributes}

세그먼트를 [Oracle Responsys 대상으로](/help/rtcdp/destinations/activate-destinations.md) 활성화할 때 [조합 스키마에서](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 마케팅 [대상의 내보낸 파일에서](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 대상 특성으로 사용할 스키마 필드 선택을 참조하십시오.

## Oracle Responsys로 데이터 가져오기 설정 {#import-data-into-responsys}

실시간 CDP를 Amazon S3 또는 SFTP 스토리지에 연결한 후 스토리지 위치에서 Oracle Responsys로 데이터 가져오기를 설정해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 Oracle Responsys [Help Center에서 연락처 또는 계정](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 가져오기를 참조하십시오.