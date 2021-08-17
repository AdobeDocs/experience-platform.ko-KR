---
keywords: 이메일;이메일;이메일;이메일 대상;adobe campaign;campaign
title: Adobe Campaign 연결
description: Adobe Campaign은 온라인과 오프라인 채널에서 모두 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---

# Adobe Campaign 연결

## 개요 {#overview}

Adobe Campaign은 온라인과 오프라인 채널에서 모두 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다. 자세한 내용은 [Campaign Classic 시작](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html)을 참조하십시오.

세그먼트 데이터를 Adobe Campaign에 보내려면 먼저 [Adobe Experience Platform에서 대상](#connect-destination)을 연결한 다음, [저장소 위치에서 Adobe Campaign으로 데이터 가져오기](#import-data-into-campaign)를 설정해야 합니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 이메일 주소, 전화번호, 성). 대상 활성화  **[!UICONTROL 워크플로우]** 의 속성 선택 단계에서 선택한  [대로](../../ui/activate-batch-profile-destinations.md#select-attributes).

## IP 주소 허용 목록 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe에서 특정 IP 범위를 허용 목록에 추가하는 것을 권장합니다.

허용 목록에 Adobe IP를 추가해야 하는 경우 클라우드 저장소 대상에 대한 [IP 주소 허용 목록](../cloud-storage/ip-address-allow-list.md)을 참조하십시오.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

Adobe Campaign은 다음 연결 유형을 지원합니다.

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP와 암호]**
* **[!UICONTROL SSH 키가 있는 SFTP]**
* **[!UICONTROL Azure Blob]**

Adobe Campaign에 데이터를 전송하는 기본 방법은 [!DNL Amazon S3] 또는 [!DNL Azure Blob]을 통해 입니다.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL Amazon S3]** 연결의 경우 [!UICONTROL 액세스 키 ID] 및 [!UICONTROL 비밀 액세스 키]를 제공해야 합니다.
* 암호&#x200B;]**연결이 있는**[!UICONTROL  SFTP의 경우 [!UICONTROL 도메인], [!UICONTROL 포트], [!UICONTROL 사용자 이름] 및 [!UICONTROL 암호]를 제공해야 합니다.
* SSH 키&#x200B;]**연결이 있는**[!UICONTROL  SFTP의 경우 [!UICONTROL 도메인], [!UICONTROL 포트], [!UICONTROL 사용자 이름] 및 [!UICONTROL SSH 키]를 제공해야 합니다.
* **[!UICONTROL Azure Blob]** 연결의 경우 연결 문자열을 제공해야 합니다.
* 원할 경우 RSA 형식의 공개 키를 첨부하여 **[!UICONTROL 키]** 섹션 아래의 내보낸 파일에 PGP/GPG를 사용한 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩 문자열로 기록해야 합니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**:  *S3 연결*. S3 버킷의 위치를 입력합니다. 여기서 [!DNL Platform]은 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로 전달합니다.
* **[!UICONTROL 폴더 경로]**: 내보내기 데이터를 CSV 또는 탭으로 구분된 파일로  [!DNL Platform] 저장할 저장소 위치의 경로를 제공합니다.
* **[!UICONTROL 컨테이너]**:  *Blob 연결*&#x200B;의 경우 폴더 경로가 있는 Blob을 포함하는 컨테이너입니다.
* **[!UICONTROL 파일 형식]**:  **** CSV 또는  **TAB_DISTINGUISHED**. 저장소 위치로 내보낼 파일 형식을 선택합니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 대상 속성 {#destination-attributes}

세그먼트를 이 대상에 활성화할 때 [결합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다. 자세한 내용은 [이메일을 마케팅 대상으로 대상을 활성화할 때 모범 사례를 참조하십시오](overview.md#best-practices).

## 내보낸 데이터 {#exported-data}

[!DNL Adobe Campaign] 대상의 경우 [!DNL Platform]은 사용자가 제공한 저장소 위치에 탭으로 구분된 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [세그먼트 활성화 확인](../../ui/activate-batch-profile-destinations.md#verify) 을 참조하십시오.

## Adobe Campaign으로 데이터 가져오기 설정 {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 이 통합을 수행하는 동안 Adobe Campaign 계약에 따라 [!DNL SFTP] 저장소 제한, 데이터베이스 저장소 제한 및 활성 프로필 제한을 기억하십시오.
>* [!DNL Campaign] 워크플로우를 사용하여 Adobe Campaign에서 내보낸 세그먼트를 예약하고, 가져오고, 매핑해야 합니다. Adobe Campaign Classic 설명서에서 [반복 가져오기 설정](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) 및 Adobe Campaign Standard 설명서에서 [데이터 관리 활동 정보](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html)를 참조하십시오.
>* Adobe Campaign에 데이터를 전송하는 기본 방법은 [!DNL Amazon S3] 또는 [!DNL Azure Blob]을 통해 입니다.


[!DNL Platform]을 [!DNL Amazon S3] 또는 [!DNL Azure Blob] 저장소에 연결한 후 저장소 위치에서 Adobe Campaign으로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 다음 Adobe Campaign 설명서 페이지를 참조하십시오.
* [Adobe Campaign Classic 설명서에서 데이터 가져오기 및 ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=ko) 내보내기,  [데이터 로드(파일)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) 를 시작합니다.
* [Adobe Campaign Standard 설명서에서 프로세스 및 데이터 ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 관리  [및 ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) 파일 로드 를 시작합니다.
