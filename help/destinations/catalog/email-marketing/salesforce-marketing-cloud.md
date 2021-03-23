---
keywords: 전자 메일;전자 메일;전자 메일 대상;전자 메일 대상;salesforce;salesforce 대상
title: Salesforce Marketing Cloud 연결
seo-description: Salesforce Marketing Cloud은 방문자와 고객이 경험을 개인화할 수 있도록 여정을 구축하고 사용자 정의할 수 있도록 하는 이전 ExactTarget으로 알려진 디지털 마케팅 패키지입니다.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---


# [!DNL Salesforce Marketing Cloud] 연결

## 개요 {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) 는 방문자 및 고객이 자신의 경험을 개인화할 수 있도록 여정을 구축하고 사용자 정의할 수 있도록 해주는 이전 ExactTarget으로 알려진 디지털 마케팅 패키지입니다.

세그먼트 데이터를 [!DNL Salesforce Marketing Cloud]에 보내려면 먼저 [Platform에서 대상](#connect-destination)을 연결한 다음 [스토리지 위치에서 ](#import-data-into-salesforce)로 데이터 가져오기[!DNL Salesforce Marketing Cloud]를 설정해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;에서 [!DNL Salesforce Marketing Cloud]를 선택한 다음 **[!UICONTROL Configure]**&#x200B;을 선택합니다.

![Salesforce에 연결](../../assets/catalog/email-marketing/salesforce/catalog.png)

**[!UICONTROL Account]** 단계에서 이전에 클라우드 스토리지 대상에 대한 연결을 설정한 경우 **[!UICONTROL Existing Account]**&#x200B;을 선택하고 기존 연결 중 하나를 선택합니다. 또는 **[!UICONTROL New Account]**&#x200B;을 선택하여 새 연결을 설정할 수 있습니다. 계정 인증 자격 증명을 입력하고 **[!UICONTROL Connect to destination]**&#x200B;을 선택합니다. [!DNL Salesforce Marketing Cloud]의 경우 **[!UICONTROL SFTP with Password]**&#x200B;과 **[!UICONTROL SFTP with SSH Key]** 중에서 선택할 수 있습니다.

![Connect Salesforce Marketing Cloud 계정](../../assets/catalog/email-marketing/salesforce/connection-type.png)

연결 유형에 따라 아래 정보를 입력하고 **[!UICONTROL Configure]**&#x200B;을 선택합니다.

- **[!UICONTROL SFTP with Password]** 연결의 경우 [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] 및 [!UICONTROL Password]를 제공해야 합니다.
- **[!UICONTROL SFTP with SSH Key]** 연결의 경우 [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] 및 [!UICONTROL SSH Key]를 제공해야 합니다.

원하는 경우, RSA 형식 공개 키를 첨부하여 PGP/GPG를 사용하여 암호화를 **[!UICONTROL Key]** 섹션 아래의 내보낸 파일에 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩 문자열로 작성해야 합니다.

![Salesforce 정보 입력](../../assets/catalog/email-marketing/salesforce/account-info.png)

**[!UICONTROL Authentication]** 단계에서 아래와 같이 대상에 대한 관련 정보를 입력합니다.
- **[!UICONTROL Name]**:대상의 관련 이름을 선택합니다.
- **[!UICONTROL Description]**:대상에 대한 설명을 입력합니다.
- **[!UICONTROL Folder Path]**:Platform에서 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장할 스토리지 위치에 경로를 제공합니다.
- **[!UICONTROL File Format]**: **CSV** 또는  **TAB_DIPORTED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.
- **[!UICONTROL Marketing actions]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

![Salesforce 기본 정보](../../assets/catalog/email-marketing/salesforce/basic-information.png)

위의 필드를 채운 후 **[!UICONTROL Create destination]**&#x200B;을 클릭합니다. 이제 대상이 연결되었으며 [세그먼트](../../ui/activate-destinations.md)를 대상에 활성화할 수 있습니다.

## 세그먼트 활성화 {#activate-segments}

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../../ui/activate-destinations.md)에 활성화를 참조하십시오.

## 대상 특성 {#destination-attributes}

[세그먼트](../../ui/activate-destinations.md)를 [!DNL Salesforce Marketing Cloud] 대상에 활성화할 경우 Adobe은 [union schema](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유한 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 [내보낸 파일에서 대상 특성으로 사용할 스키마 필드 선택](./overview.md#destination-attributes)을 참조하십시오.

## 내보낸 데이터 {#exported-data}

[!DNL Salesforce Marketing Cloud] 대상의 경우 Platform은 사용자가 제공한 저장 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.

## 데이터 가져오기를 [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}에 설정

[!DNL Platform]을(를) SFTP 저장소에 연결한 후 저장소 위치에서 [!DNL Salesforce Marketing Cloud]으로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 [!DNL Salesforce Help Center]의 파일](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5)에서 구독자를 Marketing Cloud으로 가져오기를 참조하십시오.[