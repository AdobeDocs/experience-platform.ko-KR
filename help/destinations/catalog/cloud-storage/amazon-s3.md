---
title: Amazon S3 연결
description: Amazon Web Services(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 생성하여 Adobe Experience Platform의 CSV 데이터 파일을 정기적으로 자체 S3 버킷으로 내보냅니다.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 17%

---

# [!DNL Amazon S3] 연결 {#s3-connection}

## 대상 변경 로그 {#changelog}

+++ 변경 로그 보기


| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2024년 1월 | 기능 및 설명서 업데이트 | 이제 Amazon S3 대상 커넥터가 새로운 가정된 역할 인증 유형을 지원합니다. 자세한 내용은 [인증 섹션](#assumed-role-authentication). |
| 2023년 7월 | 기능 및 설명서 업데이트 | 2023년 7월 Experience Platform 릴리스에서는 [!DNL Amazon S3] 대상 은 아래에 나열된 새로운 기능을 제공합니다. <br><ul><li>[데이터 세트 내보내기 지원](/help/destinations/ui/export-datasets.md)</li><li>추가 [파일 이름 지정 옵션](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>[향상된 매핑 단계](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)를 통해 내보낸 파일에서 사용자 정의 파일 헤더를 설정하는 기능.</li><li>[내보낸 CSV 데이터 파일의 형식을 사용자 지정하는 기능](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## 다음에 연결 [!DNL Amazon S3] API 또는 UI를 통한 스토리지 {#connect-api-or-ui}

* 에 연결하려면 [!DNL Amazon S3] 플랫폼 사용자 인터페이스를 사용한 저장소 위치에서 섹션을 읽습니다. [대상에 연결](#connect) 및 [이 대상에 대상자 활성화](#activate) 아래요.
* 에 연결하려면 [!DNL Amazon S3] 프로그래밍 방식으로 저장소 위치에서 방법 안내서를 참조하십시오. [흐름 서비스 API 튜토리얼을 사용하여 파일 기반 대상에 대상 활성화](../../api/activate-segments-file-based-destinations.md).

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

![Amazon S3 프로필 기반 내보내기 유형은 UU에서 강조 표시됩니다.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

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

### 대상으로 인증 {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA 공개 키"
>abstract="필요한 경우 RSA 형식의 공개 키를 첨부하여 암호화를 내보낸 파일에 추가할 수 있습니다. 아래 설명서 링크에서 올바른 형식의 키 예를 봅니다."

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**. Amazon S3 대상은 두 가지 인증 방법을 지원합니다.

* 액세스 키 및 비밀 키 인증
* 가정된 역할 인증

#### 액세스 키 및 비밀 키 인증

Experience Platform이 데이터를 Amazon S3 속성으로 내보내도록 Amazon S3 액세스 키 및 비밀 키를 입력하려는 경우 이 인증 방법을 사용하십시오.

![액세스 키 및 비밀 키 인증을 선택할 때 필요한 필드의 이미지.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]액세스 키** 및 **[!DNL Amazon S3]비밀 키**: 위치 [!DNL Amazon S3], 생성 `access key - secret access key` 쌍으로 플랫폼에 액세스 권한 부여 [!DNL Amazon S3] 계정입니다. 다음에서 자세히 알아보기 [Amazon Web Services 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

  ![UI에서 올바른 형식의 PGP 키의 예를 보여 주는 이미지입니다.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### 가정된 역할 {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="가정된 역할 인증"
>abstract="Adobe와 계정 키 및 비밀 키를 공유하지 않으려면 이 인증 유형을 사용합니다. 대신 Experience Platform은 역할 기반 액세스를 사용하여 Amazon S3 위치에 연결됩니다. Adobe 사용자를 위해 AWS에서 생성한 역할의 ARN을 붙여넣습니다. 패턴은 `arn:aws:iam::800873819705:role/destinations-role-customer`와 유사합니다. "

![가정된 역할 인증을 선택할 때의 필수 필드 이미지.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Adobe와 계정 키 및 비밀 키를 공유하지 않으려면 이 인증 유형을 사용합니다. 대신 Experience Platform은 역할 기반 액세스를 사용하여 Amazon S3 위치에 연결합니다.

이렇게 하려면 AWS 콘솔에서 를 사용하여 Adobe을 수행할 가정한 사용자를 만들어야 합니다. [권한 필수 권한](#required-s3-permission) Amazon S3 버킷에 쓸 수 있습니다. 만들기 **[!UICONTROL 신뢰할 수 있는 엔티티]** Adobe 계정이 있는 AWS에서 **[!UICONTROL 670664943635]**. 자세한 내용은 [역할 만들기에 대한 AWS 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**: Adobe 사용자를 위해 AWS에서 만든 역할의 ARN을 붙여넣습니다. 패턴은 과 유사합니다. `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL 암호화 키]**: 원할 경우 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 아래 이미지에서 올바른 형식의 암호화 키의 예를 봅니다.

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

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: 의 이름을 입력합니다. [!DNL Amazon S3] 이 대상에서 사용할 버킷.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.
* **[!UICONTROL 파일 유형]**: 내보낸 파일에 사용할 형식 Experience Platform을 선택합니다. 을(를) 선택할 때 [!UICONTROL CSV] 옵션을 사용하여 다음을 수행할 수도 있습니다. [파일 서식 옵션 구성](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL 압축 포맷]**: 내보낸 파일에 대해 Experience Platform이 사용해야 하는 압축 유형을 선택합니다.
* **[!UICONTROL 매니페스트 파일 포함]**: 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함된 매니페스트 JSON 파일을 내보내기에 포함하려면 이 옵션을 켜거나 끕니다. 매니페스트의 이름은 형식을 사용하여 지정합니다. `manifest-<<destinationId>>-<<dataflowRunId>>.json`. 보기 [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). 매니페스트 파일에는 다음 필드가 포함되어 있습니다.
   * `flowRunId`: [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 내보낸 파일을 생성했습니다.
   * `scheduledTime`: 파일을 내보낸 시간(UTC)입니다.
   * `exportResults.sinkPath`: 내보낸 파일이 저장되는 저장소 위치의 경로입니다.
   * `exportResults.name`: 내보낸 파일의 이름입니다.
   * `size`: 내보낸 파일의 크기(바이트)입니다.

>[!TIP]
>
>대상 연결 워크플로우에서 내보낸 대상 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 읽기 [매크로를 사용하여 저장소 위치에 폴더를 만듭니다.](overview.md#use-macros) 설명서를 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

### 필수 [!DNL Amazon S3] 권한 {#required-s3-permission}

에 데이터를 성공적으로 연결하고 내보내려면 [!DNL Amazon S3] 스토리지 위치에서 IAM(Identity and Access Management) 사용자를 [!DNL Platform] 위치: [!DNL Amazon S3] 및 다음 작업에 대한 권한을 할당할 수 있습니다.

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
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 성공적인 데이터 내보내기 유효성 검사 {#exported-data}

데이터를 성공적으로 내보냈는지 확인하려면 [!DNL Amazon S3] 저장소가 추가되고 내보낸 파일에 예상 프로필 모집단이 포함되어 있는지 확인합니다.

## 허용 목록에 추가하다 IP 주소 {#ip-address-allow-list}

다음을 참조하십시오. [허용 목록에 추가하다 IP 주소](ip-address-allow-list.md) Adobe IP를 허용 목록에 추가하다에 추가해야 하는 경우 문서입니다.