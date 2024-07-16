---
title: Pega 프로필 커넥터
description: Adobe Experience Platform의 Amazon S3용 Pega Profile Connector를 사용하여 전체 또는 증분, 또는 둘 다 프로필 데이터를 Amazon S3 클라우드 스토리지로 내보냅니다. Pega 고객 의사 결정 허브에서 Amazon S3 스토리지에서 주기적으로 프로필 데이터를 가져오기 위해 고객 프로필 Designer에서 데이터 작업을 예약할 수 있습니다.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 4%

---

# Pega 프로필 커넥터

## 개요 {#overview}

Adobe Experience Platform의 [!DNL Pega Profile Connector]을(를) 사용하여 [!DNL Amazon Web Services](AWS) S3 저장소에 대한 실시간 아웃바운드 연결을 생성하여 프로필 데이터를 CSV 파일로 Adobe Experience Platform에서 고유한 S3 버킷으로 정기적으로 내보냅니다. [!DNL Pega Customer Decision Hub]에서는 S3 스토리지에서 이 프로필 데이터를 가져와서 [!DNL Pega Customer Decision Hub] 프로필을 업데이트하도록 데이터 작업을 예약할 수 있습니다

이 커넥터는 프로필 데이터의 초기 내보내기를 설정하는 데 도움이 되며 새 프로필을 [!DNL Pega Customer Decision Hub]에 주기적으로 동기화하는 데 도움이 됩니다.  Customer Decision Hub에 최신 데이터가 있으면 차후 최상의 조치 결정을 위해 고객 기반을 더 낫고 업데이트된 보기로 확인할 수 있습니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 Pegasystem에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 Pega에게 직접 [여기](mailto:support@pega.com)로 문의하십시오.

## 사용 사례

[!DNL Pega Profile Connector] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 사용 사례 1

마케터는 처음에 Adobe Experience Platform에서 로드된 프로필 데이터로 [!DNL Pega Customer Decision Hub]을(를) 설정하려고 합니다. 이는 초기 전체 로드 후 일정에 따라 델타 로드 가 이어집니다.

### 사용 사례 2

마케터는 지속적으로 고객 프로필에 대한 페가 통찰력을 향상시키는 Adobe Experience Platform의 최신 프로필 데이터를 [!DNL Pega Customer Decision Hub]에서 사용할 수 있기를 원합니다.

## 전제 조건 {#prerequisites}

이 대상을 사용하여 Adobe Experience Platform에서 데이터를 내보내고 [!DNL Pega Customer Decision Hub](으)로 프로필을 가져오려면 먼저 다음 전제 조건을 완료하십시오.

* 데이터 파일 내보내기 및 가져오기에 사용할 [!DNL Amazon S3] 버킷 및 폴더 경로를 구성하십시오.
* [!DNL Amazon S3] 액세스 키와 [!DNL Amazon S3] 비밀 키를 구성하십시오. [!DNL Amazon S3]에서 `access key - secret access key` 쌍을 생성하여 [!DNL Amazon S3] 계정에 플랫폼 액세스 권한을 부여하십시오.
* 데이터를 [!DNL Amazon S3] 저장소 위치에 연결하고 내보내려면 [!DNL Amazon S3]에서 [!DNL Platform]에 대한 IAM(Identity and Access Management) 사용자를 만들고 `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts` 등의 권한을 할당합니다
* [!DNL Pega Customer Decision Hub] 인스턴스가 8.8 버전 이상으로 업그레이드되었는지 확인하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Pega Customer Decision Hub]은(는) 아래 표에 설명된 사용자 지정 사용자 ID의 활성화를 지원합니다. 자세한 내용은 [ID](/help/identity-service/features/namespaces.md)를 참조하세요.

| 대상 ID | 설명 |
|---|---|
| *고객 ID* | [!DNL Pega Customer Decision Hub] 및 Adobe Experience Platform에서 프로필을 고유하게 식별하는 공통 사용자 식별자 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: [!DNL Amazon S3]에서 `access key - secret access key` 쌍을 생성하여 [!DNL Amazon S3] 계정에 Adobe Experience Platform 액세스 권한을 부여합니다. 자세한 내용은 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)를 참조하세요.

### 대상 세부 정보 입력 {#destination-details}

[!DNL Amazon S3]에 대한 인증 연결을 설정한 후 대상에 대해 다음 정보를 제공하십시오.

![Pega 프로필 커넥터 대상 세부 사항에 대해 완료된 필드를 표시하는 UI 화면 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

대상에 대한 세부 정보를 구성하려면 필수 필드를 입력하고 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력하십시오.
* **[!UICONTROL 버킷 이름]**: 이 대상에서 사용할 [!DNL Amazon S3] 버킷의 이름을 입력하십시오.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력하십시오.
* **[!UICONTROL 압축 유형]**: 압축 유형을 GZIP 또는 없음으로 선택합니다.

>[!TIP]
>
>대상 연결 워크플로우에서 내보낸 대상 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 자세한 내용은 [매크로를 사용하여 저장소 위치에 폴더를 만드세요](/help/destinations/catalog/cloud-storage/overview.md#use-macros).

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

**[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 특성 및 ID 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 일괄 처리 대상 활성화 UI 자습서에서 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 참조하십시오.

## 데이터 내보내기 유효성 검사 {#exported-data}

[!DNL Pega Profile Connector] 대상의 경우 [!DNL Platform]은(는) 제공한 Amazon S3 저장소 위치에 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 대상 활성화 자습서에서 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

S3에서 프로필 데이터를 성공적으로 가져오면 [!DNL Pega Customer] 프로필 데이터 저장소에 데이터가 삽입됩니다. 가져온 고객 프로필 데이터는 다음 그림과 같이 [!DNL Pega Customer Profile Designer]에서 확인할 수 있습니다.
![고객 프로필 Designer에서 Adobe 프로필 데이터의 유효성을 검사할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

[!DNL Pega Customer Decision Hub]에서 데이터 관리자는 다음 그림과 같이 S3에서 주기적으로 프로필 데이터를 가져오도록 [!DNL Customer Profile Designer]의 데이터 작업을 구성할 수 있습니다. [!DNL Amazon S3]에서 프로필 데이터를 가져오도록 데이터 작업을 구성하는 방법에 대한 자세한 내용은 [추가 리소스](#additional-resources)를 참조하세요.
고객 프로필 Designer에서 데이터 작업을 구성하기 위한 ![UI 화면의 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 추가 리소스 {#additional-resources}

[!DNL Pega Customer Decision Hub]에서 [데이터 가져오기 작업](https://academy.pega.com/topic/import-data-jobs/v1)을 참조하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
