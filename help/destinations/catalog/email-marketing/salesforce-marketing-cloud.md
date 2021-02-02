---
keywords: 전자 메일;전자 메일;전자 메일 대상;전자 메일 대상;salesforce;salesforce 대상
title: Salesforce Marketing Cloud
seo-title: Salesforce Marketing Cloud
description: Salesforce Marketing Cloud은 방문자와 고객이 경험을 개인화할 수 있도록 여정을 구축하고 사용자 정의할 수 있도록 하는 이전 ExactTarget으로 알려진 디지털 마케팅 패키지입니다.
seo-description: Salesforce Marketing Cloud은 방문자와 고객이 경험을 개인화할 수 있도록 여정을 구축하고 사용자 정의할 수 있도록 하는 이전 ExactTarget으로 알려진 디지털 마케팅 패키지입니다.
translation-type: tm+mt
source-git-commit: 7aadb4b7e7c36b659490d155ad4cfa7ef0a24306
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud]

## 개요

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 는 방문자 및 고객이 자신의 경험을 개인화할 수 있도록 여정을 구축하고 사용자 정의할 수 있도록 해주는 이전 ExactTarget으로 알려진 디지털 마케팅 패키지입니다.

세그먼트 데이터를 [!DNL Salesforce Marketing Cloud]에 보내려면 먼저 [Platform에서 대상](#connect-destination)을 연결한 다음 [스토리지 위치에서 ](#import-data-into-salesforce)로 데이터 가져오기[!DNL Salesforce Marketing Cloud]를 설정해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;에서 [!DNL Salesforce Marketing Cloud]를 선택한 다음 **[!UICONTROL 연결 대상]**&#x200B;을 선택합니다.

![Salesforce에 연결](../../assets/catalog/email-marketing/salesforce/catalog.png)

**[!UICONTROL 인증]** 단계에서 이전에 클라우드 저장소 대상에 대한 연결을 설정한 경우 **[!UICONTROL 기존 계정]**&#x200B;을 선택하고 기존 연결 중 하나를 선택합니다. 또는 **[!UICONTROL 새 계정]**&#x200B;을 선택하여 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 **[!UICONTROL 대상에 연결]**&#x200B;을 선택합니다. [!DNL Salesforce Marketing Cloud]의 경우 **[!UICONTROL 암호]**&#x200B;가 있는 SFTP와 SSH 키&#x200B;]**이(가) 있는**[!UICONTROL  SFTP 중에서 선택할 수 있습니다. 연결 유형에 따라 아래 정보를 입력하고 **[!UICONTROL 대상에 연결]**&#x200B;을 선택합니다.

암호&#x200B;]**연결이 있는**[!UICONTROL  SFTP의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.

**[!UICONTROL SFTP에서 SSH 키]** 연결을 사용하려면 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

![Salesforce 정보 입력](../../assets/catalog/email-marketing/salesforce/account-info.png)

**[!UICONTROL 설정]** 단계에서 아래 표시된 대로 대상에 대한 관련 정보를 입력합니다.
- **[!UICONTROL 이름]**:대상의 관련 이름을 선택합니다.
- **[!UICONTROL 설명]**:대상에 대한 설명을 입력합니다.
- **[!UICONTROL 폴더 경로]**:Platform에서 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 스토리지 위치에 경로를 제공합니다.
- **[!UICONTROL 파일 형식]**: **[!UICONTROL CSV]** 또는  **[!UICONTROL TAB_DIPORTED]**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

![Salesforce 기본 정보](../../assets/catalog/email-marketing/salesforce/basic-information.png)

위의 필드를 채운 후 **[!UICONTROL 대상 만들기]**&#x200B;를 클릭합니다. 이제 대상이 연결되었으며 [세그먼트](../../ui/activate-destinations.md)를 대상에 활성화할 수 있습니다.

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md)에 활성화를 참조하십시오.

## 대상 특성 {#destination-attributes}

[세그먼트](../../ui/activate-destinations.md)를 [!DNL Salesforce Marketing Cloud] 대상으로 활성화하는 경우 [union schema](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유한 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 이메일 마케팅 대상의 내보낸 파일](./overview.md#destination-attributes)에서 대상 특성으로 사용할 스키마 필드 선택을 참조하십시오.[

## 내보낸 데이터 {#exported-data}

[!DNL Salesforce Marketing Cloud] 대상의 경우 Platform은 사용자가 제공한 저장 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.

## 데이터 가져오기를 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}에 설정

플랫폼을 [!DNL Amazon S3] 또는 SFTP 스토리지에 연결한 후 저장소 위치에서 [!DNL Salesforce Marketing Cloud]로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 [!DNL Salesforce Help Center]의 파일](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5)에서 구독자를 Marketing Cloud으로 가져오기를 참조하십시오.[