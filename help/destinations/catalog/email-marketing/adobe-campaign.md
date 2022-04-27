---
keywords: 이메일;이메일;이메일;이메일 대상;adobe campaign;campaign
title: Adobe Campaign 연결
description: Adobe Campaign은 온라인과 오프라인 채널에서 모두 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 3%

---

# Adobe Campaign 연결

## 개요 {#overview}

Adobe Campaign은 온라인과 오프라인 채널에서 모두 캠페인을 개인화하고 전달할 수 있는 솔루션 집합입니다. 자세한 내용은 [Campaign Classic 시작](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 추가 정보.

세그먼트 데이터를 Adobe Campaign에 보내려면 먼저 해야 합니다 [대상 연결](#connect-destination) Adobe Experience Platform에서 [데이터 가져오기 설정](#import-data-into-campaign) 스토리지 위치에서 Adobe Campaign으로 이동합니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP 주소 허용 목록 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe에서 특정 IP 범위를 허용 목록에 추가하는 것을 권장합니다.

을(를) 참조하십시오. [클라우드 스토리지 대상에 대한 IP 주소 허용 목록](../cloud-storage/ip-address-allow-list.md) Adobe IP를 허용 목록에 추가해야 하는 경우

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

Adobe Campaign은 다음 연결 유형을 지원합니다.

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP와 암호]**
* **[!UICONTROL SSH 키가 있는 SFTP]**
* **[!UICONTROL Azure Blob]**

Adobe Campaign에 데이터를 전송하는 기본 방법은 [!DNL Amazon S3] 또는 [!DNL Azure Blob].

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* 대상 **[!UICONTROL Amazon S3]** 연결을 제공해야 합니다. [!UICONTROL 액세스 키 ID] 및 [!UICONTROL 비밀 액세스 키].
* 대상 **[!UICONTROL SFTP와 암호]** 연결, [!UICONTROL 도메인], [!UICONTROL 포트], [!UICONTROL 사용자 이름], 및 [!UICONTROL 암호].
* 대상 **[!UICONTROL SSH 키가 있는 SFTP]** 연결, [!UICONTROL 도메인], [!UICONTROL 포트], [!UICONTROL 사용자 이름], 및 [!UICONTROL SSH 키].
* 대상 **[!UICONTROL Azure Blob]** 연결 시 연결 문자열을 제공해야 합니다.
* 원할 경우 RSA 형식의 공개 키를 연결하여 PGP/GPG를 사용하여 암호화를 내보낸 파일에 추가할 수 있습니다. **[!UICONTROL 키]** 섹션을 참조하십시오. 공개 키는 [!DNL Base64] 인코딩된 문자열입니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: *S3 연결의 경우*. S3 버킷의 위치를 입력합니다. [!DNL Platform] 은 내보내기 데이터를 CSV 파일로 저장합니다.
* **[!UICONTROL 폴더 경로]**: 스토리지 위치에 경로를 입력합니다. [!DNL Platform] 은 내보내기 데이터를 CSV 파일로 저장합니다.
* **[!UICONTROL 컨테이너]**: *Blob 연결의 경우*. 폴더 경로가 있는 Blob을 포함하는 컨테이너입니다.
* **[!UICONTROL 파일 형식]**: 선택 **CSV** csv 파일을 저장소 위치로 내보내려면 를 클릭합니다.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.


자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 대상 속성 {#destination-attributes}

세그먼트를 이 대상에 활성화할 때, Adobe에서 고유 식별자를 선택할 것을 권장합니다 [조합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다. 자세한 내용은 [이메일을 마케팅 대상으로 대상을 활성화할 때 모범 사례에 대한 우수 사례입니다](overview.md#best-practices).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Adobe Campaign] 대상, [!DNL Platform] 만들기 `.csv` 파일을 입력한 저장 위치에 저장합니다. 파일에 대한 자세한 내용은 [세그먼트 활성화 확인](../../ui/activate-batch-profile-destinations.md#verify) 세그먼트 활성화 자습서에서 를 참조하십시오.

## Adobe Campaign으로 데이터 가져오기 설정 {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 주의 사항 [!DNL SFTP] 이 통합을 수행하는 동안 Adobe Campaign 계약에 따라 저장소 제한, 데이터베이스 저장소 제한 및 활성 프로필 제한.
>* 를 사용하여 Adobe Campaign에서 내보낸 세그먼트를 예약하고, 가져오고, 매핑해야 합니다 [!DNL Campaign] 워크플로우. 을(를) 참조하십시오. [반복 가져오기 설정](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) Adobe Campaign Classic 설명서 및 [데이터 관리 활동 기본 정보](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) Adobe Campaign Standard 설명서에서 확인하십시오.
>* Adobe Campaign에 데이터를 전송하는 기본 방법은 [!DNL Amazon S3] 또는 [!DNL Azure Blob].


연결 후 [!DNL Platform] 아래와 같이 [!DNL Amazon S3] 또는 [!DNL Azure Blob] 저장소 위치에서 Adobe Campaign으로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대한 자세한 내용은 다음 Adobe Campaign 설명서 페이지를 참조하십시오.
* [데이터 가져오기 및 내보내기 시작](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=ko) 및 [데이터 로드(파일)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) ( Adobe Campaign Classic 설명서)를 참조하십시오.
* [프로세스 및 데이터 관리 시작](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 및 [파일 로드](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) ( Adobe Campaign Standard 설명서)를 참조하십시오.
