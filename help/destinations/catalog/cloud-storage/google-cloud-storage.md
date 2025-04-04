---
title: Google 클라우드 스토리지 연결
description: Google Cloud Storage에 연결하고 대상을 활성화하거나 데이터 세트를 내보내는 방법에 대해 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 2%

---

# [!DNL Google Cloud Storage] 연결

## 개요 {#overview}

[!DNL Google Cloud Storage]에 대한 실시간 아웃바운드 연결을 생성하여 정기적으로 Adobe Experience Platform의 데이터 파일을 고유한 버킷으로 내보냅니다.

## API 또는 UI를 통해 [!DNL Google Cloud Storage] 저장소에 연결합니다. {#connect-api-or-ui}

* Experience Platform 사용자 인터페이스를 사용하여 [!DNL Google Cloud Storage] 저장소 위치에 연결하려면 아래의 [대상에 연결](#connect) 및 [이 대상에 대상 활성화](#activate) 섹션을 참조하십시오.
* 프로그래밍 방식으로 [!DNL Google Cloud Storage] 저장소 위치에 연결하려면 흐름 서비스 API 자습서를 사용하여 [파일 기반 대상에 대상 활성화](../../api/activate-segments-file-based-destinations.md)를 읽어 보십시오.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* [Experience Platform 사용자 인터페이스를 사용하여 데이터 세트를 내보내는 방법](/help/destinations/ui/export-datasets.md).
* 흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트를 [내보내는 방법](/help/destinations/api/export-datasets.md).

## 내보낸 데이터의 파일 형식 {#file-format}

*대상 데이터*&#x200B;를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 `.csv`, `parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 대상 활성화 자습서에서 [내보내기에 지원되는 파일 형식](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) 섹션을 참조하십시오.

*데이터 세트*&#x200B;를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 `.parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 데이터 세트 내보내기 자습서에서 [데이터 세트 내보내기에 성공했는지 확인](../../ui/export-datasets.md#verify) 섹션을 참조하십시오.

## [!DNL Google Cloud Storage] 계정에 연결하기 위한 필수 구성 요소 설정 {#prerequisites}

Experience Platform을 [!DNL Google Cloud Storage]에 연결하려면 먼저 [!DNL Google Cloud Storage] 계정에 대해 상호 운용성을 사용하도록 설정해야 합니다. 상호 운용성 설정에 액세스하려면 [!DNL Google Cloud Platform]을(를) 열고 탐색 패널의 **[!UICONTROL 클라우드 저장소]** 옵션에서 **[!UICONTROL 설정]**&#x200B;을(를) 선택하십시오.

클라우드 저장소 및 설정이 강조 표시된 ![Google 클라우드 플랫폼 대시보드.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

**[!UICONTROL 설정]** 페이지가 나타납니다. 여기에서 [!DNL Google] 프로젝트 ID에 대한 정보와 [!DNL Google Cloud Storage] 계정에 대한 세부 정보를 볼 수 있습니다. 상호 운용성 설정에 액세스하려면 상단 헤더에서 **[!UICONTROL 상호 운용성]**&#x200B;을 선택하십시오.

![Google Cloud Platform 대시보드에 강조 표시된 상호 운용성 탭입니다.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

**[!UICONTROL 상호 운용성]** 페이지에는 서비스 계정과 연결된 인증, 액세스 키 및 기본 프로젝트에 대한 정보가 포함되어 있습니다. 서비스 계정에 대한 새 액세스 키 ID와 비밀 액세스 키를 생성하려면 **[!UICONTROL 서비스 계정에 대한 키 만들기]**&#x200B;를 선택하십시오.

![Google Cloud Platform 대시보드에 강조 표시된 서비스 계정 컨트롤에 대한 키를 만듭니다.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

새로 생성된 액세스 키 ID 및 비밀 액세스 키를 사용하여 [!DNL Google Cloud Storage] 계정을 Experience Platform에 연결할 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](/help/destinations/ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL 액세스 키 ID]**: Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 61자 영숫자 문자열입니다. 이 값을 얻는 방법에 대한 자세한 내용은 위의 [필수 구성 요소](#prerequisites) 섹션을 참조하십시오.
* **[!UICONTROL 비밀 액세스 키]**: Experience Platform에 [!DNL Google Cloud Storage] 계정을 인증하는 데 사용되는 40자의 base64로 인코딩된 문자열입니다. 이 값을 얻는 방법에 대한 자세한 내용은 위의 [필수 구성 요소](#prerequisites) 섹션을 참조하십시오.
* **[!UICONTROL 암호화 키]**: 필요한 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

이러한 값에 대한 자세한 내용은 [Google Cloud Storage HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 안내서를 참조하십시오. 자신의 액세스 키 ID와 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 소스 개요](/help/sources/connectors/cloud-storage/google-cloud-storage.md)를 참조하세요.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 버킷 이름]**: 이 대상에서 사용할 [!DNL Google Cloud Storage] 버킷의 이름을 입력하십시오.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력하십시오.
* **[!UICONTROL 파일 형식]**: 내보낸 파일에 Experience Platform에서 사용할 형식을 선택하십시오. [!UICONTROL CSV] 옵션을 선택할 때 [파일 서식 옵션을 구성](../../ui/batch-destinations-file-formatting-options.md)할 수도 있습니다.
* **[!UICONTROL 압축 형식]**: Experience Platform에서 내보낸 파일에 사용할 압축 형식을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜십시오. 매니페스트의 이름은 `manifest-<<destinationId>>-<<dataflowRunId>>.json` 형식을 사용하여 지정합니다. [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)을(를) 봅니다. 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: 내보낸 파일을 생성한 [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장된 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

### 필요한 [!DNL Google Cloud Storage] 권한 {#required-google-cloud-storage-permission}

데이터를 [!DNL Google Cloud Storage] 저장소 위치에 연결하고 내보내려면 버킷에 대해 다음 [!DNL Google Cloud Storage] 권한이 필요합니다.

* `orgpolicy.policy.get`
* `resourcemanager.projects.get`
* `resourcemanager.projects.list`
* `storage.managedFolders.create`
* `storage.multipartUploads.abort`
* `storage.multipartUploads.create`
* `storage.multipartUploads.listParts`
* `storage.objects.create`
* `storage.objects.list`

[!DNL Google Cloud Storage]의 [액세스 제어 및 권한](https://cloud.google.com/storage/docs/access-control/iam-permissions)에 대해 자세히 알아보세요.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 일정 조정

**[!UICONTROL 예약]** 단계에서 [!DNL Google Cloud Storage] 대상에 대해 [내보내기 일정을 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)할 수 있으며 [내보낸 파일의 이름을 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)할 수도 있습니다.

### 속성 및 ID 매핑 {#map}

**[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 특성 및 ID 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 일괄 처리 대상 활성화 UI 자습서에서 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 참조하십시오.

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Google Cloud Storage] 버킷을 확인하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인하십시오.

## 허용 목록에 추가하다 IP 주소 {#ip-address-allow-list}

허용 목록에 추가하다 Adobe IP를 허용 목록에 추가하다에 추가해야 하는 경우 [IP 주소](ip-address-allow-list.md) 문서를 참조하십시오.