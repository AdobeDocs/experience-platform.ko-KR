---
keywords: email;Email;e-mail;email destinations;oracle responsys destination
title: Oracle Responsys 대상
seo-title: Oracle Responsys 대상
description: Respondsys는 Oracle이 이메일, 모바일, 디스플레이 및 소셜 간의 인터랙션을 개인화하기 위해 제공하는 크로스채널 마케팅 캠페인을 위한 기업 이메일 마케팅 툴입니다.
seo-description: Respondsys는 Oracle이 이메일, 모바일, 디스플레이 및 소셜 간의 인터랙션을 개인화하기 위해 제공하는 크로스채널 마케팅 캠페인을 위한 기업 이메일 마케팅 툴입니다.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 0%

---


# [!DNL Oracle Responsys]

## 개요

[Respondsys](https://www.oracle.com/marketingcloud/products/cross-channel-orchestration/) 는 이메일, 모바일, 디스플레이 및 소셜 간의 인터랙션을 개인화하도록 [!DNL Oracle] 하는 크로스채널 마케팅 캠페인을 위한 기업 이메일 마케팅 툴입니다.

세그먼트 데이터를 대상 [!DNL Oracle Responsys]으로 전송하려면 먼저 실시간 고객 데이터 [플랫폼에서 대상에](#connect-destination) [연결한 다음 스토리지 위치에서 다음](#import-data-into-responsys) 위치로 데이터 가져오기를 [!DNL Oracle Responsys]설정해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예:이메일 주소, 전화 번호, 성)을 [대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

[ **[!UICONTROL 연결]** ] > [대상 ****]에서 [!DNL Oracle Responsys]선택한 다음 **[!UICONTROL Connect 대상을 선택합니다]**.

![Responsys에 연결](../../assets/catalog/email-marketing/oracle-responsys/catalog.png)

이전에 클라우드 스토리지 대상에 대한 연결을 **[!UICONTROL 설정한 경우 인증]** 단계에서 **[!UICONTROL 기존 계정을]** 선택하고 기존 연결 중 하나를 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 대상에 **[!UICONTROL 연결을 선택합니다]**. 예를 [!DNL Oracle Responsys]들어 암호를 사용하는 **[!UICONTROL SFTP와 SSH 키를 사용하는]** SFTP 중에서 선택할 수 있습니다 ****. 연결 유형에 따라 아래 정보를 입력하고 대상에 **[!UICONTROL 연결을 선택합니다]**.

암호 **[!UICONTROL 가]** 연결된 SFTP의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.

SSH 키 **** 연결이 있는 SFTP의 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

![Responsys 정보 입력](../../assets/catalog/email-marketing/oracle-responsys/account-info.png)

설정 **** 단계에서 아래와 같이 대상에 대한 관련 정보를 입력합니다.
- **[!UICONTROL 이름]**:대상의 관련 이름을 선택합니다.
- **[!UICONTROL 설명]**:대상에 대한 설명을 입력합니다.
- **[!UICONTROL 폴더 경로]**:실시간 CDP가 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장하는 스토리지 위치에 경로를 제공합니다.
- **[!UICONTROL 파일 형식]**: **CSV** 또는 **TAB_DIPORTED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

![Responsys 기본 정보](../../assets/catalog/email-marketing/oracle-responsys/basic-information.png)

위 필드 **[!UICONTROL 를 채운 후 대상]** 만들기를 클릭합니다. 대상이 연결되었으며 대상에 대한 세그먼트를 [활성화할](../../ui/activate-destinations.md) 수 있습니다.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](../../ui/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.

## 대상 속성 {#destination-attributes}

세그먼트를 대상에 [활성화할](../../ui/activate-destinations.md) 때 [!DNL Oracle Responsys] 조합 스키마에서 고유 식별자를 선택하는 것이 [좋습니다](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 [마케팅 대상의 내보낸 파일에서](./overview.md#destination-attributes) 대상 속성으로 사용할 스키마 필드 선택을 참조하십시오.

## 내보낸 데이터 {#exported-data}

대상에 대해 [!DNL Oracle Responsys] 실시간 CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 생성합니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상을](../../ui/activate-destinations.md#esp-and-cloud-storage) 참조하십시오.

<!--

Expect a new file to be created in your storage location every day. The file format is:

`Oracle_Responsys_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

```
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Oracle_Responsys_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

The presence of these files in your storage location is confirmation of successful activation. To understand how the exported files are structured, you can [download a sample .csv file](/help/rtcdp/destinations/assets/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). This sample file includes the profile attributes `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, and `personalEmail.address`.

-->

## 데이터 가져오기 설정 [!DNL Oracle Responsys] {#import-data-into-responsys}

실시간 CDP를 사용자 [!DNL Amazon S3] 또는 SFTP 스토리지에 연결한 후 스토리지 위치에서 (으)로 데이터 가져오기를 설정해야 합니다 [!DNL Oracle Responsys]. 이 작업을 수행하는 방법에 대한 자세한 내용은 의 [연락처 또는 계정](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCEA/Connect_WizardUpload.htm) 가져오기를 참조하십시오 [!DNL Oracle Responsys Help Center].