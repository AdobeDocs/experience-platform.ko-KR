---
title: Oracle Furnar 대상
seo-title: Oracle Furnar 대상
description: Oracle Fura는 B2B 마케터 및 조직이 마케팅 캠페인 및 영업 리드 생성을 관리하는 데 도움이 되는 Oracle이 제공하는 마케팅 자동화를 위한 SaaS(서비스) 플랫폼입니다.
seo-description: Oracle Fura는 B2B 마케터 및 조직이 마케팅 캠페인 및 영업 리드 생성을 관리하는 데 도움이 되는 Oracle이 제공하는 마케팅 자동화를 위한 SaaS(서비스) 플랫폼입니다.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# [!DNL Oracle Eloqua]

## 개요

[Fura](https://www.oracle.com/marketingcloud/products/marketing-automation/) 는 B2B 마케터 및 조직이 마케팅 캠페인 및 영업 리드 생성을 관리하는 데 도움이 [!DNL Oracle] 되는 마케팅 자동화를 위한 서비스(SaaS) 플랫폼으로서 사용되는 소프트웨어입니다.

세그먼트 데이터 [!DNL Oracle Eloqua]를 전송하려면 먼저 Adobe 실시간 고객 데이터 Platform에서 대상을 [](#connect-destination) 연결한 [다음 스토리지 위치에서 (으)로 데이터 가져오기](#import-data-into-eloqua) 를 [!DNL Oracle Eloqua]설정해야 합니다.

## 대상에 연결 {#connect-destination}

1. [ **[!UICONTROL 연결]** ] > [대상 ****]에서 [!DNL Oracle Eloqua]선택한 다음 **[!UICONTROL Connect 대상을 선택합니다]**.

   ![Furnar에 연결](/help/rtcdp/destinations/assets/connect-oracle-eloqua.png)

2. 이전에 클라우드 스토리지 대상에 대한 연결을 **[!UICONTROL 설정한 경우 인증]** 단계에서 **[!UICONTROL 기존 계정을]** 선택하고 기존 연결 중 하나를 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 대상에 **[!UICONTROL 연결을 선택합니다]**. 예를 [!DNL Oracle Eloqua]들어 암호를 사용하는 **[!UICONTROL SFTP와 SSH 키를 사용하는]** SFTP 중에서 선택할 수 있습니다 ****. 연결 유형에 따라 아래 정보를 입력하고 대상에 **[!UICONTROL 연결을 선택합니다]**.

   암호 **[!UICONTROL 가]** 연결된 SFTP의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.
SSH 키 **** 연결이 있는 SFTP의 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

   ![Furnar 마법사 설정](/help/rtcdp/destinations/assets/eloqua-authentication.png)

3. 설정 **** 단계에서 아래와 같이 대상에 대한 관련 정보를 입력합니다.
   * **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
   * **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
   * **[!UICONTROL 폴더 경로]**: 실시간 CDP가 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장하는 스토리지 위치에 경로를 제공합니다.
   * **[!UICONTROL 파일 형식]**: **CSV** 또는 **TAB_DIPORTED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

   ![웅변가 기본 정보](/help/rtcdp/destinations/assets/eloqua-basic-information.png)

4. 위 필드 **[!UICONTROL 를 채운 후 대상]** 만들기를 클릭합니다. 이제 대상이 만들어지고 대상에 대한 세그먼트를 [활성화할](/help/rtcdp/destinations/activate-destinations.md) 수 있습니다.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](/help/rtcdp/destinations/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.

## 대상 속성 {#destination-attributes}

세그먼트를 대상에 [활성화할](/help/rtcdp/destinations/activate-destinations.md) 때 [!DNL Oracle Eloqua] 조합 스키마에서 고유 식별자를 선택하는 것이 [좋습니다](../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 [마케팅 대상의 내보낸 파일에서](/help/rtcdp/destinations/email-marketing-destinations.md#destination-attributes) 대상 속성으로 사용할 스키마 필드 선택을 참조하십시오.

## 내보낸 데이터 {#exported-data}

대상 [!DNL Oracle Eloqua] 의 경우 Adobe 실시간 CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 파일 또는 `.csv` 파일을 생성합니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상을](/help/rtcdp/destinations/activate-destinations.md#esp-and-cloud-storage) 참조하십시오.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Eloqua_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Eloqua_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 데이터 가져오기 설정 [!DNL Oracle Eloqua] {#import-data-into-eloqua}

실시간 CDP를 Amazon S3 또는 SFTP 스토리지에 연결한 후 스토리지 위치에서 (으)로 데이터 가져오기를 설정해야 합니다 [!DNL Oracle Eloqua]. 이 작업을 수행하는 방법에 대한 자세한 내용은 의 [연락처 또는 계정](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) 가져오기를 참조하십시오 [!DNL Oracle Eloqua Help Center].