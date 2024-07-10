---
keywords: 이메일;이메일;이메일;이메일 대상;adobe campaign;campaign
title: Adobe Campaign 연결
description: Adobe Campaign은 모든 온라인 및 오프라인 채널에서 캠페인을 개인화하고 전달하는 데 도움이 되는 솔루션 세트입니다.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 4%

---

# Adobe Campaign 연결

## 개요 {#overview}

Adobe Campaign은 모든 온라인 및 오프라인 채널에서 캠페인을 개인화하고 전달하는 데 도움이 되는 솔루션 세트입니다. 다음을 참조하십시오 [Campaign Classic 시작](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) 추가 정보.

대상 데이터를 Adobe Campaign으로 전송하려면 먼저 다음을 수행해야 합니다 [대상 연결](#connect-destination) Adobe Experience Platform에서 [데이터 가져오기 설정](#import-data-into-campaign) 스토리지 위치에서 Adobe Campaign으로.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ 덧신 | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 허용 목록에 추가하다 IP 주소 {#allow-list}

SFTP 저장소를 사용하여 이메일 마케팅 대상을 설정할 때 Adobe은 특정 IP 범위를 허용 목록에 추가하다에 추가할 것을 권장합니다.

을(를) 참조하십시오 [허용 목록에 추가하다 SFTP 대상의 IP 주소](../cloud-storage/ip-address-allow-list.md) Adobe IP를 허용 목록에 추가하다에 추가해야 하는 경우

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

Adobe Campaign은 다음 연결 유형을 지원합니다.

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL 암호가 포함된 SFTP]**
* **[!UICONTROL SSH 키가 포함된 SFTP]**
* **[!UICONTROL Azure Blob]**

Adobe Campaign에 데이터를 보내는 기본 방법은 [!DNL Amazon S3] 또는 [!DNL Azure Blob].

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* 대상 **[!UICONTROL Amazon]** 연결, 다음을 제공해야 합니다. [!UICONTROL 액세스 키 ID] 및 [!UICONTROL 비밀 액세스 키].
* 대상 **[!UICONTROL 암호가 포함된 SFTP]** 연결, 다음을 제공해야 합니다. [!UICONTROL 도메인], [!UICONTROL 포트], [!UICONTROL 사용자 이름], 및 [!UICONTROL 암호].
* 대상 **[!UICONTROL SSH 키가 포함된 SFTP]** 연결, 다음을 제공해야 합니다. [!UICONTROL 도메인], [!UICONTROL 포트], [!UICONTROL 사용자 이름], 및 [!UICONTROL SSH 키].
* 대상 **[!UICONTROL Azure Blob]** 연결 - 연결 문자열을 제공해야 합니다.
* 원할 경우 RSA 형식의 공개 키를 첨부하여 PGP/GPG를 사용한 암호화를 내보낸 파일에 추가할 수 있습니다. **[!UICONTROL 키]** 섹션. 공개 키는 다음으로 작성되어야 합니다. [!DNL Base64] 인코딩된 문자열입니다.
* **[!UICONTROL 이름]**: 대상의 관련 이름을 선택합니다.
* **[!UICONTROL 설명]**: 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: *S3 연결용*. S3 버킷의 위치를 입력하십시오. [!DNL Platform] 은 내보내기 데이터를 CSV 파일로 저장합니다.
* **[!UICONTROL 폴더 경로]**: 저장소 위치의 경로를 제공합니다. 여기서 [!DNL Platform] 은 내보내기 데이터를 CSV 파일로 저장합니다.
* **[!UICONTROL 컨테이너]**: *Blob 연결의 경우*. 폴더 경로가 있는 Blob을 보유하는 컨테이너입니다.
* **[!UICONTROL 파일 형식]**: 선택 **CSV** csv 파일을 저장소 위치로 내보냅니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}


다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 대상 속성 {#destination-attributes}

이 대상에 대한 대상을 활성화할 때 Adobe은에서 고유 식별자를 선택할 것을 권장합니다. [유니온 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다. 자세한 내용은 다음을 참조하십시오. [이메일 마케팅 대상으로 대상자를 활성화할 때의 모범 사례](overview.md#best-practices).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Adobe Campaign] 대상, [!DNL Platform] 다음 항목을 만듭니다. `.csv` 파일을 제공한 저장소 위치에 있습니다. 파일에 대한 자세한 내용은 [대상자 활성화 확인](../../ui/activate-batch-profile-destinations.md#verify) audience activation 튜토리얼의 섹션.

## Adobe Campaign으로 데이터 가져오기 설정 {#import-data-into-campaign}

>[!IMPORTANT]
>
>* 다음 사항에 주의하십시오. [!DNL SFTP] 이 통합을 수행하는 동안 Adobe Campaign 계약에 따라 스토리지 제한, 데이터베이스 스토리지 제한 및 활성 프로필 제한을 실시합니다.
>* 다음을 사용하여 Adobe Campaign에서 내보낸 세그먼트를 예약하고, 가져오고, 매핑해야 합니다. [!DNL Campaign] 워크플로. 을(를) 참조하십시오 [반복 가져오기 설정](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) Adobe Campaign Classic 설명서 및 [데이터 관리 활동 기본 정보](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) Adobe Campaign Standard 설명서에서 확인할 수 있습니다.
>* Adobe Campaign에 데이터를 보내는 기본 방법은 [!DNL Amazon S3] 또는 [!DNL Azure Blob].

연결 후 [!DNL Platform] (으)로 [!DNL Amazon S3] 또는 [!DNL Azure Blob] 스토리지: 스토리지 위치에서 Adobe Campaign으로 데이터 가져오기를 설정해야 합니다. 이를 수행하는 방법에 대해 알아보려면 다음 Adobe Campaign 설명서 페이지를 참조하십시오.
* [데이터 가져오기 및 내보내기 시작](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=ko) 및 [데이터 로드 중(파일)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) Adobe Campaign Classic 설명서에서 확인할 수 있습니다.
* [프로세스 및 데이터 관리 시작](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) 및 [파일 로드](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) Adobe Campaign Standard 설명서에서 확인할 수 있습니다.
