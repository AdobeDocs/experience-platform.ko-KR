---
keywords: email;Email;e-mail;email destinations;adobe campaign;campaign
title: Adobe Campaign
seo-title: Adobe Campaign
description: Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다.
seo-description: Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 1%

---


# Adobe Campaign

## 개요

Adobe Campaign은 온라인과 오프라인의 모든 채널에서 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다. 자세한 [내용은 Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 정보를 참조하십시오.

세그먼트 데이터를 Adobe Campaign으로 전송하려면 먼저 실시간 고객 데이터 플랫폼에서 대상 [을](#connect-destination) 연결한 다음 스토리지 위치에서 Adobe Campaign으로 데이터 가져오기 [를](#import-data-into-campaign) 설정해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예:이메일 주소, 전화 번호, 성)을 [대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 선택합니다](../../ui/activate-destinations.md#select-attributes).

## 연결 대상 {#connect-destination}

[ **[!UICONTROL 연결]** ] > [대상 **[!UICONTROL 에서]** Adobe Campaign을 선택한 다음 **[!UICONTROL 연결 대상을 선택합니다]**.

![adobe campaign에 연결](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Connect 대상 작업 과정에서 저장소 위치에 대한 **[!UICONTROL 연결 유형을]** 선택합니다. Adobe Campaign의 경우, **[!UICONTROL Amazon S3]**, **[!UICONTROL 암호를 사용하는 SFTP]** 및 **[!UICONTROL SSH 키를 사용하는]** SFTP 중에서 선택할 수 있습니다. 연결 유형에 따라 아래 정보를 입력한 다음 **[!UICONTROL Connect를 선택합니다]**.

![캠페인 설정 마법사](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- **[!UICONTROL Amazon S3]** 연결의 경우 액세스 키 ID와 비밀 액세스 키를 제공해야 합니다.
- 암호 **[!UICONTROL 가]** 연결된 SFTP의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.
- SSH 키 **** 연결이 있는 SFTP의 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

선택적으로 RSA 형식 공개 키를 연결하여 **[!UICONTROL 키]** 섹션 아래의 내보낸 파일에 PGP/GPG를 사용하여 암호화를 추가할 수 있습니다. 이 공개 키는 Base64 인코딩 문자열로 **작성해야** 합니다.

![캠페인 정보 입력](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

기본 **[!UICONTROL 정보에서]**&#x200B;아래와 같이 대상에 대한 관련 정보를 입력합니다.
- **[!UICONTROL 이름]**:대상의 관련 이름을 선택합니다.
- **[!UICONTROL 설명]**:대상에 대한 설명을 입력합니다.
- **[!UICONTROL 버킷 이름]**: *S3 연결을 참조하십시오*. 실시간 CDP가 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장하는 S3 버킷의 위치를 입력합니다.
- **[!UICONTROL 폴더 경로]**:실시간 CDP가 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 저장하는 스토리지 위치에 경로를 제공합니다.
- **[!UICONTROL 파일 형식]**: **CSV** 또는 **TAB_DIPORTED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

![캠페인 기본 정보](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

위의 필드를 **[!UICONTROL 채운]** 후 만들기를 클릭합니다. 대상이 연결되었으며 대상에 대한 세그먼트를 [활성화할](../../ui/activate-destinations.md) 수 있습니다.

## 세그먼트 활성화 {#activate-segments}

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](../../ui/activate-destinations.md) 프로필 및 세그먼트 활성화를 참조하십시오.

## 대상 속성 {#destination-attributes}

세그먼트를 Adobe Campaign 대상에 [활성화할](../../ui/activate-destinations.md) 때 [조합 스키마에서 고유 식별자를 선택하는 것이 좋습니다](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 [이메일 마케팅 대상 문서에서 내보낸 파일에서](./overview.md#destination-attributes) 대상 속성으로 사용할 스키마 필드 선택을 참조하십시오.

## 내보낸 데이터 {#exported-data}

대상에 대해 [!DNL Adobe Campaign] 실시간 CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 생성합니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상을](../../ui/activate-destinations.md#esp-and-cloud-storage) 참조하십시오.

## Adobe Campaign으로 데이터 가져오기 설정 {#import-data-into-campaign}

>[!IMPORTANT]
>
>- 이 통합을 수행하는 동안 Adobe Campaign 계약에 따라 SFTP 저장소 제한, 데이터베이스 저장소 제한 및 활성 프로필 제한에 주의하십시오.
>- 워크플로우를 사용하여 Adobe Campaign에서 내보낸 세그먼트를 예약, 가져오기 및 매핑해야 [!DNL Campaign] 합니다. Adobe Campaign [문서에서 반복 가져오기](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows) 설정을 참조하십시오.



실시간 CDP를 사용자 [!DNL Amazon S3] 또는 SFTP 스토리지에 연결한 후 스토리지 위치에서 Adobe Campaign으로 데이터 가져오기를 설정해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 Adobe Campaign 설명서의 [데이터](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) 가져오기를 참조하십시오.