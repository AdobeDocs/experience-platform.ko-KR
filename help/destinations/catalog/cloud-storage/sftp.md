---
title: SFTP 연결
description: SFTP 서버에 대한 실시간 아웃바운드 연결을 생성하여 구분된 데이터 파일을 정기적으로 Adobe Experience Platform에서 내보냅니다.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 8%

---

# SFTP 연결

## 대상 변경 로그 {#changelog}

2023년 7월 Experience Platform 릴리스에서는 SFTP 대상이 아래에 나열된 새로운 기능을 제공합니다.

* [데이터 세트 내보내기 지원](/help/destinations/ui/export-datasets.md).
* 추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* [향상된 매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능.
* [내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## 개요 {#overview}

SFTP 서버에 대한 실시간 아웃바운드 연결을 생성하여 구분된 데이터 파일을 정기적으로 Adobe Experience Platform에서 내보냅니다.

>[!IMPORTANT]
>
> Experience Platform은 SFTP 서버로 데이터 내보내기를 지원하지만 데이터를 내보내는 데 권장되는 클라우드 스토리지 위치는 다음과 같습니다 [!DNL Amazon S3] 및 [!DNL Azure Blob].

## API 또는 UI를 통해 SFTP에 연결 {#connect-api-or-ui}

* Platform 사용자 인터페이스를 사용하여 SFTP 저장소 위치에 연결하려면 섹션을 참조하십시오 [대상에 연결](#connect) 및 [이 대상에 대상자 활성화](#activate) 아래요.
* SFTP 저장소 위치에 프로그래밍 방식으로 연결하려면 [흐름 서비스 API 튜토리얼을 사용하여 파일 기반 대상에 대한 대상자 활성화](../../api/activate-segments-file-based-destinations.md).

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

![대상 카탈로그에서 강조 표시된 SFTP 프로필 기반 내보내기 유형.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* 방법 [platform 사용자 인터페이스를 사용하여 데이터 세트 내보내기](/help/destinations/ui/export-datasets.md).
* 방법 [흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트 내보내기](/help/destinations/api/export-datasets.md).

## 내보낸 데이터의 파일 형식 {#file-format}

내보낼 때 *대상 데이터*, Platform은 `.csv`, `parquet`, 또는 `.json` 파일을 제공한 저장소 위치에 있습니다. 파일에 대한 자세한 내용은 [내보내기에 지원되는 파일 형식](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) audience activation 튜토리얼의 섹션.

내보낼 때 *데이터 세트*, Platform은 `.parquet` 또는 `.json` 파일을 제공한 저장소 위치에 있습니다. 파일에 대한 자세한 내용은 [데이터 세트 내보내기 성공 확인](../../ui/export-datasets.md#verify) 섹션 을 참조하십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 인증 정보 {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA 공개 키"
>abstract="필요한 경우 RSA 형식의 공개 키를 첨부하여 암호화를 내보낸 파일에 추가할 수 있습니다. 아래 설명서 링크에서 올바른 형식의 키 예를 봅니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="비공개 SSH 키"
>abstract="비공개 SSH 키는 RSA 포맷의 Base64로 인코딩된 문자열이어야 하며 암호로 보호되지 않아야 합니다."

을(를) 선택하는 경우 **[!UICONTROL 암호가 포함된 SFTP]** SFTP 위치에 연결하는 인증 유형:

![암호가 포함된 SFTP 대상 기본 인증.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL 도메인]**: SFTP 저장소 위치 주소;
* **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름
* **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용하는 포트
* **[!UICONTROL 암호]**: SFTP 저장소 위치에 로그인하기 위한 암호입니다.
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지입니다.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


을(를) 선택하는 경우 **[!UICONTROL SSH 키가 포함된 SFTP]** SFTP 위치에 연결하는 인증 유형:

![SFTP 대상 SSH 키 인증.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL 도메인]**: SFTP 계정의 IP 주소 또는 도메인 이름을 입력합니다
* **[!UICONTROL 포트]**: SFTP 저장소 위치에서 사용하는 포트
* **[!UICONTROL 사용자 이름]**: SFTP 저장소 위치에 로그인할 사용자 이름
* **[!UICONTROL SSH 키]**: SFTP 저장소 위치에 로그인하는 데 사용되는 개인 SSH 키입니다. 개인 키는 RSA 형식의 Base64 인코딩 문자열이어야 하며 암호로 보호되지 않아야 합니다.
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지입니다.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### 대상 세부 사항 {#destination-details}

SFTP 위치에 인증 연결을 설정한 후 대상에 대해 다음 정보를 제공합니다.

![SFTP 대상에 대한 대상 세부 사항 필드.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL 이름]**: Experience Platform 사용자 인터페이스에서 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 파일을 내보낼 SFTP 위치의 폴더 경로를 입력합니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 을(를) 선택할 때 [!UICONTROL CSV] 옵션을 사용하여 다음을 수행할 수도 있습니다. [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 대해 Experience Platform이 사용해야 하는 압축 유형을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜거나 끕니다. 매니페스트의 이름은 형식을 사용하여 지정합니다. `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 보기 [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 내보낸 파일을 생성했습니다.
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장되는 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 SFTP 저장소를 확인하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인하십시오.

## 허용 목록에 추가하다 IP 주소 {#ip-address-allow-list}

다음을 참조하십시오. [허용 목록에 추가하다 IP 주소](ip-address-allow-list.md) Adobe IP를 허용 목록에 추가하다에 추가해야 하는 경우 문서입니다.
