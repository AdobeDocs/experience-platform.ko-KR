---
title: Azure Data Lake Storage Gen2 연결
description: Azure Data Lake Storage Gen2에 연결하여 대상자를 활성화하고 데이터 세트를 내보내는 방법을 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: d265a02d-c901-4b39-8714-fe9ecdbb5bb1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 2%

---

# [!DNL Azure Data Lake Storage Gen2] 연결

## 개요 {#overview}

[[!DNL Azure Data Lake Storage Gen2]](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)&#x200B;([!DNL ADLS Gen2]) 데이터 레이크에 대한 실시간 아웃바운드 연결을 만들어 정기적으로 Experience Platform에서 데이터 파일을 내보내는 방법에 대해 알아보려면 이 페이지를 참조하십시오.

## API 또는 UI를 통해 [!DNL ADLS Gen2] 저장소에 연결합니다. {#connect-api-or-ui}

* Experience Platform 사용자 인터페이스를 사용하여 [!DNL ADLS Gen2] 저장소 위치에 연결하려면 아래의 [대상에 연결](#connect) 및 [이 대상에 대상 활성화](#activate) 섹션을 참조하십시오.
* 프로그래밍 방식으로 [!DNL ADLS Gen2] 저장소 위치에 연결하려면 흐름 서비스 API 자습서를 사용하여 [파일 기반 대상에 대상 활성화](../../api/activate-segments-file-based-destinations.md)를 읽어 보십시오.

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
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 적용 가능한 스키마 필드(예: PPID)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* [Experience Platform 사용자 인터페이스를 사용하여 데이터 세트를 내보내는 방법](/help/destinations/ui/export-datasets.md).
* 흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트를 [내보내는 방법](/help/destinations/api/export-datasets.md).

## 내보낸 데이터의 파일 형식 {#file-format}

*대상 데이터*&#x200B;를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 `.csv`, `parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 대상 활성화 자습서에서 [내보내기에 지원되는 파일 형식](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) 섹션을 참조하십시오.

*데이터 세트*&#x200B;를 내보낼 때 Experience Platform은 사용자가 제공한 저장소 위치에 `.parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 데이터 세트 내보내기 자습서에서 [데이터 세트 내보내기에 성공했는지 확인](../../ui/export-datasets.md#verify) 섹션을 참조하십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](/help/destinations/ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL URL]**: [!DNL Azure Data Lake Storage Gen2]의 끝점입니다. 끝점 패턴은 `abfss://<container>@<accountname>.dfs.core.windows.net`입니다.
* **[!UICONTROL 테넌트]**: 응용 프로그램이 포함된 테넌트 정보입니다.
* **[!UICONTROL 서비스 사용자 ID]**: 응용 프로그램의 클라이언트 ID입니다.
* **[!UICONTROL 서비스 사용자 키]**: 응용 프로그램의 키입니다.
* **[!UICONTROL 암호화 키]**: 필요한 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
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

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 일정 조정 {#scheduling}

**[!UICONTROL 예약]** 단계에서 [!DNL Azure Data Lake Storage Gen2] 대상에 대해 [내보내기 일정을 설정](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling)할 수 있으며 [내보낸 파일의 이름을 구성](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)할 수도 있습니다.

### 속성 및 ID 매핑 {#map}

**[!UICONTROL 매핑]** 단계에서는 프로필에 내보낼 특성 및 ID 필드를 선택할 수 있습니다. 내보낸 파일의 헤더를 원하는 이름으로 변경하도록 선택할 수도 있습니다. 자세한 내용은 일괄 처리 대상 활성화 UI 자습서에서 [매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 참조하십시오.

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Azure Data Lake Storage Gen2] 저장소를 확인하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인하십시오.
