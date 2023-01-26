---
title: Pega 프로필 커넥터
description: Adobe Experience Platform의 Amazon S3용 Pega Profile Connector를 사용하여 프로필 데이터를 Amazon S3 클라우드 저장소로 전체 또는 증분 또는 둘 다 내보냅니다. Pega Customer Decision Hub에서 고객 프로필 디자이너에 데이터 작업을 예약하여 Amazon S3 스토리지에서 프로필 데이터를 주기적으로 가져올 수 있습니다.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 1%

---


# Pega 프로필 커넥터

## 개요 {#overview}

를 사용하십시오 [!DNL Pega Profile Connector] Adobe Experience Platform에서 를 통해 [!DNL Amazon Web Services] (AWS) S3 저장소를 사용하여 Adobe Experience Platform의 프로필 데이터를 CSV 파일로 주기적으로의 S3 버킷으로 내보냅니다. in [!DNL Pega Customer Decision Hub]로 지정하는 경우 데이터 작업을 예약하여 S3 저장소에서 이 프로필 데이터를 가져와 업데이트할 수 있습니다 [!DNL Pega Customer Decision Hub] 프로필 참조.

이 커넥터는 프로필 데이터의 초기 내보내기를 설정하는 데 도움이 되며 새 프로필을 주기적으로 동기화하는 데 도움이 됩니다 [!DNL Pega Customer Decision Hub].  Customer Decisioning Hub에 최신 데이터가 있으면 다음으로 좋은 작업 의사 결정을 위한 고객 기반의 보다 나아지고 업데이트된 보기가 제공됩니다.

>[!IMPORTANT]
>
>이 설명서 페이지는 Pegasystems에서 만들었습니다. 문의 사항이나 업데이트 요청이 있으면 Pega에 직접 문의하십시오 [여기](mailto:support@pega.com).

## 사용 사례

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Pega Profile Connector] 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 1

마케터가 처음에 [!DNL Pega Customer Decision Hub] (Adobe Experience Platform에서 로드한 프로필 데이터 포함). 이것은 예약된 기준으로 델타 로드가 뒤따르는 초기 전체 로드입니다.

### 사용 사례 2

마케터는 Adobe Experience Platform에서 사용할 수 있는 최신 프로필 데이터를 원합니다. [!DNL Pega Customer Decision Hub] 는 지속적으로 고객 프로필에 대한 Pega 인사이트를 향상시킵니다.

## 전제 조건 {#prerequisites}

이 대상을 사용하여 Adobe Experience Platform에서 데이터를 내보내고 프로필을 로 가져올 수 있습니다. [!DNL Pega Customer Decision Hub], 다음 전제 조건을 완료했는지 확인합니다.

* 구성 [!DNL Amazon S3] 버킷 및 데이터 파일을 내보내고 가져오는 데 사용할 폴더 경로입니다.
* 구성 [!DNL Amazon S3] 액세스 키 및 [!DNL Amazon S3] 암호 키: in [!DNL Amazon S3], 생성 `access key - secret access key` 플랫폼에 대한 액세스 권한을 부여하기 위한 쌍 [!DNL Amazon S3] 계정이 필요합니다.
* 데이터를 성공적으로 연결하고 로 내보내려면 [!DNL Amazon S3] 저장소 위치, [!DNL Platform] in [!DNL Amazon S3] 및 과 같은 권한 할당 `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* 다음 사항을 확인하십시오. [!DNL Pega Customer Decision Hub] 인스턴스가 8.8 버전 이상으로 업그레이드되었습니다.

## 지원되는 ID {#supported-identities}

[!DNL Pega Customer Decision Hub] 은 아래 표에 설명된 사용자 지정 사용자 ID의 활성화를 지원합니다. 자세한 내용은 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 |
|---|---|
| *CustomerID* | 에서 프로필을 고유하게 식별하는 일반 사용자 식별자입니다 [!DNL Pega Customer Decision Hub] 및 Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 전자 메일 주소, 전화 번호, 성)을 선택한 대로 [대상 활성화 워크플로우](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 다운스트림 플랫폼으로 3, 6, 8, 12 또는 24시간 단위로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 입력합니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 필요한 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**.

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: in [!DNL Amazon S3], 생성 `access key - secret access key` Adobe Experience Platform 액세스 권한을 부여하려면 쌍을 따르십시오 [!DNL Amazon S3] 계정이 필요합니다. 자세한 내용은 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### 대상 세부 사항 채우기 {#destination-details}

인증 연결을 설정한 후 [!DNL Amazon S3]를 채울 경우 대상에 대해 다음 정보를 제공합니다.

![Pega 프로필 커넥터 대상 세부 사항에 대해 완료된 필드를 보여주는 UI 화면의 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

대상에 대한 세부 사항을 구성하려면 필수 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 다음]**. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: 이름 입력 [!DNL Amazon S3] 이 대상에서 사용할 버킷입니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 압축 유형]**: 압축 유형을 GZIP 또는 NONE으로 선택합니다.

>[!TIP]
>
>연결 대상 워크플로우에서 내보낸 세그먼트 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 읽기 [매크로를 사용하여 저장소 위치에 폴더를 만듭니다](/help/destinations/catalog/cloud-storage/overview.md#use-macros) 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 특성 및 ID 매핑 {#map}

에서 **[!UICONTROL 매핑]** 단계: 프로파일에 대해 내보낼 속성 및 id 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 친숙한 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 배치 대상 활성화 UI 자습서에서 를 참조하십시오.

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상 [!DNL Pega Profile Connector] 대상, [!DNL Platform] 만들기 `.csv` 제공한 Amazon S3 저장소 위치에 있는 파일입니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../../ui/activate-batch-profile-destinations.md) 세그먼트 활성화 자습서에서 를 참조하십시오.

S3에서 프로필 데이터를 성공적으로 가져오면 [!DNL Pega Customer] 프로필 데이터 저장소. 가져온 고객 프로필 데이터는에서 확인할 수 있습니다. [!DNL Pega Customer Profile Designer] 다음 그림과 같이,
![고객 프로필 디자이너에서 Adobe 프로필 데이터의 유효성을 확인할 수 있는 UI 화면의 이미지입니다](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

in [!DNL Pega Customer Decision Hub], 데이터 관리자는에서 데이터 작업을 구성할 수 있습니다. [!DNL Customer Profile Designer] 다음 그림과 같이 프로필 데이터를 S3에서 주기적으로 가져오려면 다음을 수행하십시오. 자세한 내용은 [추가 리소스](#additional-resources) 에서 프로필 데이터를 가져오도록 데이터 작업을 구성하는 방법에 대한 자세한 정보 [!DNL Amazon S3].
![고객 프로필 디자이너에서 데이터 작업을 구성하기 위한 UI 화면의 이미지](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## 추가 리소스 {#additional-resources}

자세한 내용은 [데이터 가져오기 작업](https://academy.pega.com/topic/import-data-jobs/v1) in [!DNL Pega Customer Decision Hub].

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).



