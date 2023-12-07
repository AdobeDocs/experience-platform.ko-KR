---
title: Azure Blob 연결
description: Azure Blob 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform에서 CSV 데이터 파일을 정기적으로 내보냅니다.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 7%

---

# [!DNL Azure Blob] 연결

## 대상 변경 로그 {#changelog}

2023년 7월 Experience Platform 릴리스에서는 [!DNL Azure Blob] 대상 은 아래에 나열된 새로운 기능을 제공합니다.

* [데이터 세트 내보내기 지원](/help/destinations/ui/export-datasets.md).
* 추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* [향상된 매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능.
* [내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 개요 {#overview}

[!DNL Azure Blob] (이하 &quot;&quot;라 한다) [!DNL Blob])는 클라우드를 위한 Microsoft의 개체 스토리지 솔루션입니다. 이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Blob] 대상 사용 [!DNL Platform] 사용자 인터페이스.

## 다음에 연결 [!UICONTROL Azure Blob] API 또는 UI를 통한 스토리지 {#connect-api-or-ui}

* 에 연결하려면 [!UICONTROL Azure Blob] 플랫폼 사용자 인터페이스를 사용한 저장소 위치에서 섹션을 읽습니다. [대상에 연결](#connect) 및 [이 대상에 대상자 활성화](#activate) 아래요.
* 에 연결하려면 [!UICONTROL Azure Blob] 저장소 위치를 프로그래밍 방식으로 읽고 [흐름 서비스 API 튜토리얼을 사용하여 파일 기반 대상에 대한 대상자 활성화](../../api/activate-segments-file-based-destinations.md).

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Blob] 대상, 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [대상에 대한 대상자 활성화](../../ui/activate-batch-profile-destinations.md).

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
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 의 프로필 속성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 멤버를 내보냅니다. [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. 자세한 내용 [배치 파일 기반 대상](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 지원되는 파일 형식 {#file-formats}

[!DNL Experience Platform] 은(는) 내보낼 다음 파일 형식을 지원합니다 [!DNL Azure Blob]:

* 쉼표로 구분된 값(CSV): 내보낸 데이터 파일에 대한 지원은 현재 쉼표로 구분된 값으로 제한됩니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="RSA 공개 키"
>abstract="필요한 경우 RSA 형식의 공개 키를 첨부하여 암호화를 내보낸 파일에 추가할 수 있습니다. 아래 설명서 링크에서 올바른 형식의 키 예를 봅니다."

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 연결 문자열]**: Blob 저장소의 데이터에 액세스하려면 연결 문자열이 필요합니다. 다음 [!DNL Blob] 연결 문자열 패턴은 다음으로 시작: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * 구성에 대한 자세한 내용은 [!DNL Blob] 연결 문자열입니다. 참조 [Azure 스토리지 계정에 대한 연결 문자열 구성](https://learn.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) Microsoft 설명서에서 확인할 수 있습니다.
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 컨테이너]**: 의 이름을 입력합니다. [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다.
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
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* 방법 [platform 사용자 인터페이스를 사용하여 데이터 세트 내보내기](/help/destinations/ui/export-datasets.md).
* 방법 [흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트 내보내기](/help/destinations/api/export-datasets.md).

## 내보낸 데이터 {#exported-data}

대상 [!DNL Azure Blob Storage] 대상, [!DNL Platform] 다음 항목을 만듭니다. `.csv` 파일을 제공한 저장소 위치에 있습니다. 파일에 대한 자세한 내용은 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) audience activation 튜토리얼에서 을 참조하십시오.