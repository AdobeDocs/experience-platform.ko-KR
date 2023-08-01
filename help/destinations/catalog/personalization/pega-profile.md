---
title: Pega 프로필 커넥터
description: Adobe Experience Platform의 Amazon S3용 Pega Profile Connector를 사용하여 전체 또는 증분, 또는 둘 다 프로필 데이터를 Amazon S3 클라우드 스토리지로 내보냅니다. Pega 고객 의사 결정 허브에서 고객 프로필 디자이너에서 데이터 작업을 예약하여 Amazon S3 스토리지에서 정기적으로 프로필 데이터를 가져올 수 있습니다.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 2%

---

# Pega 프로필 커넥터

## 개요 {#overview}

사용 [!DNL Pega Profile Connector] Adobe Experience Platform에서 의 실시간 아웃바운드 연결을 [!DNL Amazon Web Services] (AWS) 프로필 데이터를 Adobe Experience Platform의 CSV 파일로 정기적으로 자체 S3 버킷으로 내보내는 S3 스토리지입니다. [!DNL Pega Customer Decision Hub]에서는 S3 스토리지에서 이 프로필 데이터를 가져와서 [!DNL Pega Customer Decision Hub] 프로필을 업데이트하도록 데이터 작업을 예약할 수 있습니다

이 커넥터는 프로필 데이터의 초기 내보내기를 설정하는 데 도움이 되며 새 프로필을에 정기적으로 동기화하는 데에도 도움이 됩니다 [!DNL Pega Customer Decision Hub].  Customer Decision Hub에 최신 데이터가 있으면 차후 최상의 조치 결정을 위해 고객 기반을 더 낫고 업데이트된 보기로 확인할 수 있습니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 Pegasystem에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 페가에게 직접 문의하시기 바랍니다 [여기](mailto:support@pega.com).

## 사용 사례

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Pega Profile Connector] 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 사용 사례 1

마케터는 처음에 를 설정하려고 합니다. [!DNL Pega Customer Decision Hub] Adobe Experience Platform에서 로드된 프로필 데이터로 이는 초기 전체 로드 후 일정에 따라 델타 로드 가 이어집니다.

### 사용 사례 2

마케터는에서 사용할 수 있는 Adobe Experience Platform의 최신 프로필 데이터를 원합니다. [!DNL Pega Customer Decision Hub] 이를 통해 고객 프로필에 대한 페가의 통찰력이 지속적으로 향상됩니다.

## 사전 요구 사항 {#prerequisites}

이 대상을 사용하여 Adobe Experience Platform에서 데이터를 내보내고 프로필을 로 가져오기 전에 [!DNL Pega Customer Decision Hub]를 설치한 후 다음 사전 요구 사항을 완료하십시오.

* 구성 [!DNL Amazon S3] 데이터 파일 내보내기 및 가져오기에 사용할 버킷 및 폴더 경로입니다.
* 구성 [!DNL Amazon S3] 액세스 키 및 [!DNL Amazon S3] 비밀 키: [!DNL Amazon S3], 생성 `access key - secret access key` 쌍으로 플랫폼에 액세스 권한 부여 [!DNL Amazon S3] 계정입니다.
* 에 데이터를 성공적으로 연결하고 내보내려면 [!DNL Amazon S3] 스토리지 위치에서 IAM(Identity and Access Management) 사용자를 [!DNL Platform] 위치: [!DNL Amazon S3] 및 다음과 같은 권한 할당 `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* 다음을 확인하십시오. [!DNL Pega Customer Decision Hub] 인스턴스가 8.8 버전 이상으로 업그레이드되었습니다.

## 지원되는 ID {#supported-identities}

[!DNL Pega Customer Decision Hub] 는 아래 표에 설명된 사용자 지정 사용자 ID의 활성화를 지원합니다. 자세한 내용은 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 |
|---|---|
| *고객 ID* | 에서 프로필을 고유하게 식별하는 공통 사용자 식별자 [!DNL Pega Customer Decision Hub] 및 Adobe Experience Platform |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: 위치 [!DNL Amazon S3], 생성 `access key - secret access key` 쌍으로 Adobe Experience Platform에 액세스 권한 부여 [!DNL Amazon S3] 계정입니다. 다음에서 자세히 알아보기 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 대상 세부 정보 입력 {#destination-details}

에 인증 연결 설정 후 [!DNL Amazon S3]에 대상에 대해 다음 정보를 제공합니다.

![Pega 프로필 커넥터 대상 세부 사항에 대해 완료된 필드를 표시하는 UI 화면 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

대상에 대한 세부 정보를 구성하려면 필수 필드를 입력한 다음 을(를) 선택합니다 **[!UICONTROL 다음]**. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: 의 이름을 입력합니다. [!DNL Amazon S3] 이 대상에서 사용할 버킷.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 압축 유형]**: 압축 유형을 GZIP 또는 없음으로 선택합니다.

>[!TIP]
>
>대상 연결 워크플로우에서 내보낸 대상 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 읽기 [매크로를 사용하여 저장소 위치에 폴더를 만듭니다.](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 설명서를 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 속성 및 ID 매핑 {#map}

다음에서 **[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 속성 및 id 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 배치 대상 활성화 UI 튜토리얼에서 다음을 수행합니다.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상 [!DNL Pega Profile Connector] 대상, [!DNL Platform] 다음 항목을 만듭니다. `.csv` 제공한 Amazon S3 저장소 위치의 파일입니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) audience activation 튜토리얼에서 을 참조하십시오.

S3에서 프로필 데이터를 성공적으로 가져오면 데이터가 [!DNL Pega Customer] 프로필 데이터 저장소입니다. 가져온 고객 프로필 데이터는에서 확인할 수 있습니다. [!DNL Pega Customer Profile Designer] 다음 그림과 같이 을 참조하십시오.
![고객 프로필 디자이너에서 Adobe 프로필 데이터의 유효성을 검사할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

위치 [!DNL Pega Customer Decision Hub], 데이터 관리자는에서 데이터 작업을 구성할 수 있습니다. [!DNL Customer Profile Designer] 다음 그림과 같이 S3에서 주기적으로 프로필 데이터를 가져옵니다. 다음을 참조하십시오. [추가 리소스](#additional-resources) 프로필 데이터를 가져오도록 데이터 작업을 구성하는 방법에 대한 자세한 내용 [!DNL Amazon S3].
![고객 프로필 디자이너에서 데이터 작업을 구성하는 UI 화면의 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 추가 리소스 {#additional-resources}

다음을 참조하십시오 [데이터 가져오기 작업](https://academy.pega.com/topic/import-data-jobs/v1) 위치: [!DNL Pega Customer Decision Hub].

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
