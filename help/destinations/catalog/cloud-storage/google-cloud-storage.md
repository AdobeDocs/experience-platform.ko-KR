---
title: (베타) Google 클라우드 스토리지 연결
description: Google 클라우드 스토리지에 연결하고 세그먼트를 활성화하거나 데이터 세트를 내보내는 방법을 알아봅니다.
source-git-commit: 97a39e12d916e4fbd048c0fb9ddfa9bdfa10d438
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---

# (베타) [!DNL Google Cloud Storage] 연결

>[!IMPORTANT]
>
>이 대상은 현재 베타에 있으며 제한된 수의 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 [!DNL Google Cloud Storage] 연결되면 Adobe 담당자에게 연락하여 [!DNL Organization ID].

## 개요 {#overview}

에 대한 라이브 아웃바운드 연결을 만듭니다. [!DNL Google Cloud Storage] 를 통해 Adobe Experience Platform의 데이터 파일을 고유한 버킷으로 주기적으로 내보냅니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 세그먼트의 프로필 속성 선택 화면에서 선택한 대로 해당 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다 [대상 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 연결 필수 구성 요소 설정 [!DNL Google Cloud Storage] account {#prerequisites}

Platform을 [!DNL Google Cloud Storage]를 사용하려면 먼저 상호 운용성을 설정해야 합니다. [!DNL Google Cloud Storage] 계정이 필요합니다. 상호 운용성 설정에 액세스하려면 [!DNL Google Cloud Platform] 을(를) 선택합니다. **[!UICONTROL 설정]** 에서 **[!UICONTROL 클라우드 스토리지]** 옵션을 선택합니다.

![클라우드 스토리지 및 설정이 강조 표시된 Google Cloud Platform 대시보드 .](/help/sources/images/tutorials/create/google-cloud-storage/nav.png)

다음 **[!UICONTROL 설정]** 페이지가 나타납니다. 여기에서 [!DNL Google] 프로젝트 ID 및 세부 정보 [!DNL Google Cloud Storage] 계정이 필요합니다. 상호 운용성 설정에 액세스하려면 **[!UICONTROL 상호 운용성]** 상단 헤더에서

![Google Cloud Platform 대시보드에 강조 표시된 상호 운용성 탭입니다.](/help/sources/images/tutorials/create/google-cloud-storage/project-access.png)

다음 **[!UICONTROL 상호 운용성]** 페이지에는 인증, 액세스 키 및 서비스 계정과 연결된 기본 프로젝트에 대한 정보가 들어 있습니다. 서비스 계정에 대한 새 액세스 키 ID와 비밀 액세스 키를 생성하려면 **[!UICONTROL 서비스 계정 키 만들기]**.

![Google Cloud Platform 대시보드에 강조 표시된 서비스 계정 컨트롤 키 만들기](/help/sources/images/tutorials/create/google-cloud-storage/interoperability.png)

새로 생성된 액세스 키 ID와 비밀 액세스 키를 사용하여 [!DNL Google Cloud Storage] Platform에 계정을 설정합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](/help/destinations/ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 입력합니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 액세스 키 ID]**: 인증을 위해 사용되는 61자의 영숫자 문자열입니다 [!DNL Google Cloud Storage] Platform에 계정을 설정합니다. 이 값을 가져오는 방법에 대한 자세한 내용은 [전제 조건](#prerequisites) 섹션에 있는 마지막 항목이 될 필요가 없습니다.
* **[!UICONTROL 비밀 액세스 키]**: 인증을 위해 사용되는 40자의 base64로 인코딩된 문자열입니다 [!DNL Google Cloud Storage] Platform에 계정을 설정합니다. 이 값을 가져오는 방법에 대한 자세한 내용은 [전제 조건](#prerequisites) 섹션에 있는 마지막 항목이 될 필요가 없습니다.
* **[!UICONTROL 암호화 키]**: 선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64-encoded] 문자열. 아래 설명서 링크에서 올바른 형식의 base64로 인코딩된 키의 예를 봅니다. 중간 부분은 간결성을 위해 짧게 되어 있다.

   ![UI에서 올바르게 포맷된 및 base64로 암호화된 PGP 키의 예를 보여주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

이러한 값에 대한 자세한 내용은 [Google 클라우드 스토리지 HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서. 고유한 액세스 키 ID 및 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 소스 개요](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 버킷 이름]**: 이름 입력 [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷입니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스트할 대상 폴더의 경로를 입력합니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 예약

에서 **[!UICONTROL 예약]** 단계를 수행하여 다음을 수행할 수 있습니다. [내보내기 스케줄 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 에 대해 [!DNL Google Cloud Storage] 대상 및 [내보낸 파일의 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 특성 및 ID 매핑 {#map}

에서 **[!UICONTROL 매핑]** 단계: 프로파일에 대해 내보낼 속성 및 id 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 친숙한 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 배치 대상 활성화 UI 자습서에서 를 참조하십시오.

## (베타) 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 집합 내보내기를 지원합니다. 데이터 집합 내보내기를 설정하는 방법에 대한 자세한 내용은 [데이터 세트 내보내기 자습서](/help/destinations/ui/export-datasets.md).

## 성공적인 데이터 내보내기의 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Google Cloud Storage] 버킷하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.
