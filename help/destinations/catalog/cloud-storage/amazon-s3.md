---
title: Amazon S3 연결
description: Amazon Web Services(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform의 CSV 데이터 파일을 정기적으로 자체 S3 버킷으로 내보냅니다.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 17%

---

# [!DNL Amazon S3] 연결 {#s3-connection}

## 대상 변경 로그 {#changelog}

+++ 변경 로그 보기


| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 1월 | 기능 및 설명서 업데이트 | 이제 Amazon S3 대상 커넥터가 새로운 가정된 역할 인증 유형을 지원합니다. 자세한 내용은 [인증 섹션](#assumed-role-authentication)을 참조하세요. |
| 2023년 7월 | 기능 및 설명서 업데이트 | 2023년 7월 Experience Platform 릴리스를 통해 [!DNL Amazon S3] 대상은 아래 나열된 새로운 기능을 제공합니다. <br><ul><li>[데이터 집합 내보내기 지원](/help/destinations/ui/export-datasets.md)</li><li>추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>[향상된 매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능.</li><li>[내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## API 또는 UI를 통해 [!DNL Amazon S3] 저장소에 연결합니다. {#connect-api-or-ui}

* 플랫폼 사용자 인터페이스를 사용하여 [!DNL Amazon S3] 저장소 위치에 연결하려면 아래의 [대상에 연결](#connect) 및 [이 대상에 대상 활성화](#activate) 섹션을 참조하십시오.
* 프로그래밍 방식으로 [!DNL Amazon S3] 저장소 위치에 연결하려면 Flow Service API 자습서를 사용하여 파일 기반 대상에 대해 [대상자를 활성화하는 방법](../../api/activate-segments-file-based-destinations.md)에 대한 안내서를 읽어 보십시오.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ 덧신 | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](../../ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

![UU에서 강조 표시된 Amazon S3 프로필 기반 내보내기 유형.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 데이터 세트 내보내기 {#export-datasets}

이 대상은 데이터 세트 내보내기를 지원합니다. 데이터 세트 내보내기 설정 방법에 대한 자세한 내용은 튜토리얼을 참조하십시오.

* [플랫폼 사용자 인터페이스를 사용하여 데이터 세트를 내보내는 방법](/help/destinations/ui/export-datasets.md).
* 흐름 서비스 API를 사용하여 프로그래밍 방식으로 데이터 세트를 [내보내는 방법](/help/destinations/api/export-datasets.md).

## 내보낸 데이터의 파일 형식 {#file-format}

*대상 데이터*&#x200B;를 내보낼 때 Platform은 사용자가 제공한 저장소 위치에 `.csv`, `parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 대상 활성화 자습서에서 [내보내기에 지원되는 파일 형식](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) 섹션을 참조하십시오.

*데이터 세트*&#x200B;를 내보낼 때 Platform은 사용자가 제공한 저장소 위치에 `.parquet` 또는 `.json` 파일을 만듭니다. 파일에 대한 자세한 내용은 데이터 세트 내보내기 자습서에서 [데이터 세트 내보내기에 성공했는지 확인](../../ui/export-datasets.md#verify) 섹션을 참조하십시오.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 공개 키"
>abstract="필요한 경우 RSA 형식의 공개 키를 첨부하여 암호화를 내보낸 파일에 추가할 수 있습니다. 아래 설명서 링크에서 올바른 형식의 키 예를 봅니다."

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오. Amazon S3 대상은 두 가지 인증 방법을 지원합니다.

* 액세스 키 및 비밀 키 인증
* 가정된 역할 인증

#### 액세스 키 및 비밀 키 인증

Experience Platform이 데이터를 Amazon S3 속성으로 내보내도록 Amazon S3 액세스 키 및 비밀 키를 입력하려는 경우 이 인증 방법을 사용하십시오.

![액세스 키 및 비밀 키 인증을 선택할 때 필요한 필드의 이미지입니다.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: [!DNL Amazon S3]에서 `access key - secret access key` 쌍을 생성하여 [!DNL Amazon S3] 계정에 플랫폼 액세스 권한을 부여합니다. 자세한 내용은 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)를 참조하세요.
* **[!UICONTROL 암호화 키]**: 필요한 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지입니다.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 가정된 역할 {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="가정된 역할 인증"
>abstract="Adobe와 계정 키 및 비밀 키를 공유하지 않으려면 이 인증 유형을 사용합니다. 대신 Experience Platform은 역할 기반 액세스를 사용하여 Amazon S3 위치에 연결됩니다. Adobe 사용자를 위해 AWS에서 생성한 역할의 ARN을 붙여넣습니다. 패턴은 `arn:aws:iam::800873819705:role/destinations-role-customer`와 유사합니다. "

![가정된 역할 인증을 선택할 때 필요한 필드의 이미지](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Adobe와 계정 키 및 비밀 키를 공유하지 않으려면 이 인증 유형을 사용합니다. 대신 Experience Platform은 역할 기반 액세스를 사용하여 Amazon S3 위치에 연결합니다.

이렇게 하려면 AWS 콘솔에서 Amazon S3 버킷에 쓸 수 있는 [올바른 필수 권한](#required-s3-permission)이 있는 Adobe의 가설 사용자를 만들어야 합니다. Adobe 계정 **[!UICONTROL 670664943635]**&#x200B;을(를) 사용하여 AWS에서 **[!UICONTROL 신뢰할 수 있는 엔터티]**&#x200B;을(를) 만듭니다. 자세한 내용은 [역할 만들기에 대한 AWS 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html)를 참조하세요.

* **[!DNL Role]**: Adobe 사용자에 대해 AWS에서 만든 역할의 ARN을 붙여 넣습니다. 패턴은 `arn:aws:iam::800873819705:role/destinations-role-customer`과(와) 유사합니다.
* **[!UICONTROL 암호화 키]**: 필요한 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="버킷 이름"
>abstract="이름은 3~63자 사이여야 합니다. 글자나 숫자로 시작하고 끝나야 합니다. 소문자, 숫자 또는 하이픈( - )만 포함해야 합니다. 형식은 IP 주소(예: 192.100.1.1)로 지정하면 안 됩니다."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="폴더 경로"
>abstract="A-Z, a-z, 0-9 문자만 포함해야 하며 특수 문자(예: `/!-_.'()"^[]+$%.*"`)를 포함할 수 있습니다. 대상자 파일별로 폴더를 만들려면 매크로(예: `/%SEGMENT_NAME%` 또는 `/%SEGMENT_ID%` 또는 `/%SEGMENT_NAME%/%SEGMENT_ID%`)를 텍스트 필드에 삽입합니다. 매크로는 폴더 경로 끝에만 삽입할 수 있습니다. 설명서의 매크로 예 보기"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=ko-KR#use-macros" text="매크로를 사용하여 스토리지 위치에 폴더 만들기"

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력하십시오.
* **[!UICONTROL 버킷 이름]**: 이 대상에서 사용할 [!DNL Amazon S3] 버킷의 이름을 입력하십시오.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력하십시오.
* **[!UICONTROL 파일 형식]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택하십시오. [!UICONTROL CSV] 옵션을 선택할 때 [파일 서식 옵션을 구성](../../ui/batch-destinations-file-formatting-options.md)할 수도 있습니다.
* Experience Platform **[!UICONTROL 압축 형식]**: 내보낸 파일에 사용할 압축 형식을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜십시오. 매니페스트의 이름은 `manifest-<<destinationId>>-<<dataflowRunId>>.json` 형식을 사용하여 지정합니다. [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)을(를) 봅니다. 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: 내보낸 파일을 생성한 [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장된 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

>[!TIP]
>
>대상 연결 워크플로우에서 내보낸 대상 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 자세한 내용은 [매크로를 사용하여 저장소 위치에 폴더를 만드세요](overview.md#use-macros).

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

### 필요한 [!DNL Amazon S3] 권한 {#required-s3-permission}

데이터를 [!DNL Amazon S3] 저장소 위치에 연결하고 내보내려면 [!DNL Amazon S3]에서 [!DNL Platform]에 대한 IAM(Identity and Access Management) 사용자를 만들고 다음 작업에 대한 권한을 할당하십시오.

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상자 활성화에 대한 지침은 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](../../ui/activate-batch-profile-destinations.md)를 참조하십시오.

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Amazon S3] 저장소를 확인하고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인하십시오.

## 허용 목록에 추가하다 IP 주소 {#ip-address-allow-list}

허용 목록에 추가하다 Adobe IP를 허용 목록에 추가하다에 추가해야 하는 경우 [IP 주소](ip-address-allow-list.md) 문서를 참조하십시오.