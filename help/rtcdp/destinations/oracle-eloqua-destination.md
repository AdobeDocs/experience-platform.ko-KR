---
title: Oracle Furnar 대상
seo-title: Oracle Furnar 대상
description: Oracle Fura는 B2B 마케터 및 조직이 마케팅 캠페인과 영업 리드 생성을 관리하는 데 도움이 되는 Oracle의 마케팅 자동화를 위한 SaaS(서비스) 플랫폼입니다.
seo-description: Oracle Fura는 B2B 마케터 및 조직이 마케팅 캠페인과 영업 리드 생성을 관리하는 데 도움이 되는 Oracle의 마케팅 자동화를 위한 SaaS(서비스) 플랫폼입니다.
translation-type: tm+mt
source-git-commit: fe56fe71c36e06f2eeed45436cb36b5a371d0484

---


# Oracle Furnar

## 개요

[Fura는](https://www.oracle.com/marketingcloud/products/marketing-automation/) B2B 마케터 및 조직이 마케팅 캠페인과 영업 리드 생성을 관리하는 데 도움이 되도록 Oracle에서 제공하는 마케팅 자동화를 위한 서비스(SaaS) 플랫폼으로서 소프트웨어입니다.

세그먼트 데이터를 Oracle Quala로 전송하려면 먼저 Adobe 실시간 고객 데이터 플랫폼에서 대상을 [](#connect-destination) 연결한 다음 저장 위치에서 Oracle Fura로 데이터 가져오기를 [](#import-data-into-eloqua) 설정해야 합니다.

## 대상에 연결 {#connect-destination}

1. 에서 Oracle **[!UICONTROL Connections > Destinations]** Furnar를 선택한 다음 **[!UICONTROL Connect destination]**&#x200B;선택합니다.

   ![Furnar에 연결](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. 인증 **단계에서** 이전에 클라우드 스토리지 대상에 대한 연결을 설정한 경우 기존 연결을 **[!UICONTROL Existing Account]** 선택하고 선택합니다. 또는 새 연결을 **[!UICONTROL New Account]** 설정하도록 선택할 수 있습니다. 계정 인증 자격 증명을 입력하고 **[!UICONTROL Connect to destination]**&#x200B;선택합니다. Oracle Fura의 경우, 암호를 사용하는 **SFTP와 SSH 키를** 사용하는 **SFTP를 선택할 수 있습니다**. 연결 유형에 따라 아래 정보를 입력하고 **[!UICONTROL Connect to destination]**&#x200B;선택합니다.

   암호 **연결이 있는 SFTP의** 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.
SSH **키 연결이 있는 SFTP의** 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

   ![Furnar 마법사 설정](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. 설정 **단계에서** 다음과 같이 대상에 대한 관련 정보를 입력합니다.
   * **이름**:대상의 관련 이름을 선택합니다.
   * **설명**:대상에 대한 설명을 입력합니다.
   * **폴더 경로**:실시간 CDP를 통해 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 스토리지 위치에 경로를 제공합니다.
   * **파일 형식**:CSV ******또는** TAB_SEPARATED. 저장소 위치로 내보낼 파일 형식을 선택합니다.
   ![Fura 기본 정보](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. 위의 **필드를 채운 후 대상** 만들기를 클릭합니다. 이제 대상이 생성되어 세그먼트를 [대상에](/help/rtcdp/destinations/activate-destinations.md) 활성화할 수 있습니다.

## 대상 속성

세그먼트를 [Oracle Fura 대상에](/help/rtcdp/destinations/activate-destinations.md) 활성화할 때 [조합 스키마에서](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 마케팅 [대상의 내보낸 파일에서](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 대상 특성으로 사용할 스키마 필드 선택을 참조하십시오.

## Oracle Fura로 데이터 가져오기 설정 {#import-data-into-eloqua}

Amazon S3 또는 SFTP 스토리지에 실시간 CDP를 연결한 후 스토리지 위치에서 Oracle Quala로 데이터 가져오기를 설정해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 Oracle [Fura Help Center에서 연락처 또는 계정](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 가져오기를 참조하십시오.