---
title: Google 클라우드 스토리지 연결
description: Google Cloud Storage에 연결하고 대상을 활성화하거나 데이터 세트를 내보내는 방법에 대해 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---

# [!DNL Google Cloud Storage] 연결

## 개요 {#overview}

에 대한 실시간 아웃바운드 연결 만들기 [!DNL Google Cloud Storage] Adobe Experience Platform의 데이터 파일을 정기적으로 고유한 버킷으로 내보냅니다.

## 다음에 연결 [!DNL Google Cloud Storage] API 또는 UI를 통한 스토리지 {#connect-api-or-ui}

* 에 연결하려면 [!DNL Google Cloud Storage] 플랫폼 사용자 인터페이스를 사용한 저장소 위치에서 섹션을 읽습니다. [대상에 연결](#connect) 및 [이 대상에 대상자 활성화](#activate) 아래요.
* 에 연결하려면 [!DNL Google Cloud Storage] 저장소 위치를 프로그래밍 방식으로 읽고 [흐름 서비스 API 튜토리얼을 사용하여 파일 기반 대상에 대한 대상자 활성화](../../api/activate-segments-file-based-destinations.md).

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 연결을 위한 필수 구성 요소 설정 [!DNL Google Cloud Storage] account {#prerequisites}

플랫폼을 연결하려면 다음을 수행하십시오. [!DNL Google Cloud Storage], 먼저 상호 운용성을 활성화해야 합니다. [!DNL Google Cloud Storage] 계정입니다. 상호 운용성 설정에 액세스하려면 [!DNL Google Cloud Platform] 및 선택 **[!UICONTROL 설정]** 다음에서 **[!UICONTROL 클라우드 스토리지]** 옵션을 선택합니다.

![클라우드 스토리지 및 설정이 강조 표시된 Google 클라우드 플랫폼 대시보드.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

다음 **[!UICONTROL 설정]** 페이지가 나타납니다. 여기에서 다음에 대한 정보를 볼 수 있습니다. [!DNL Google] 프로젝트 ID 및 세부 정보 [!DNL Google Cloud Storage] 계정입니다. 상호 운용성 설정에 액세스하려면 다음을 선택합니다 **[!UICONTROL 상호 운용성]** 맨 위 머리글에서

![Google Cloud Platform 대시보드에서 강조 표시된 상호 운용성 탭입니다.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

다음 **[!UICONTROL 상호 운용성]** 페이지에는 서비스 계정과 연결된 인증, 액세스 키 및 기본 프로젝트에 대한 정보가 포함되어 있습니다. 서비스 계정에 대한 새 액세스 키 ID와 비밀 액세스 키를 생성하려면 다음을 선택합니다. **[!UICONTROL 서비스 계정에 대한 키 만들기]**.

![Google Cloud Platform 대시보드에서 강조 표시된 서비스 계정 컨트롤에 대한 키 만들기 를 참조하십시오.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

새로 생성된 액세스 키 ID 및 비밀 액세스 키를 사용하여 [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](/help/destinations/ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 액세스 키 ID]**: 인증을 위해 사용되는 61자 영숫자 문자열입니다. [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다. 이 값을 얻는 방법에 대한 자세한 내용은 [전제 조건](#prerequisites) 위의 섹션.
* **[!UICONTROL 비밀 액세스 키]**: 인증에 사용되는 40자의 base64로 인코딩된 문자열 [!DNL Google Cloud Storage] 계정을 플랫폼에 추가합니다. 이 값을 얻는 방법에 대한 자세한 내용은 [전제 조건](#prerequisites) 위의 섹션.
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

이러한 값에 대한 자세한 내용은 [Google 클라우드 스토리지 HMAC 키](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 가이드. 자신의 액세스 키 ID 및 비밀 액세스 키를 생성하는 방법에 대한 단계는 [[!DNL Google Cloud Storage] 소스 개요](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 버킷 이름]**: 의 이름을 입력합니다. [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 을(를) 선택할 때 [!UICONTROL CSV] 옵션을 사용하여 다음을 수행할 수도 있습니다. [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 대해 Experience Platform이 사용해야 하는 압축 유형을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜거나 끕니다. 매니페스트의 이름은 형식을 사용하여 지정합니다. `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 보기 [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 내보낸 파일을 생성했습니다.
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장되는 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 예약

다음에서 **[!UICONTROL 예약]** 단계, 다음을 수행할 수 있습니다. [내보내기 일정 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) 에 대한 [!DNL Google Cloud Storage] 대상 및 다음을 수행할 수도 있습니다. [내보낸 파일의 이름 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### 속성 및 ID 매핑 {#map}

다음에서 **[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 속성 및 id 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) 배치 대상 활성화 UI 튜토리얼에서 다음을 수행합니다.

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* 방법 [platform 사용자 인터페이스를 사용하여 데이터 세트 내보내기](/help/destinations/ui/export-datasets.md).
* 방법 [흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트 내보내기](/help/destinations/api/export-datasets.md).

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Google Cloud Storage] 버킷 을 만들고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.
