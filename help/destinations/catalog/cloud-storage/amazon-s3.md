---
keywords: Amazon S3;S3 대상;s3;amazon s3
title: Amazon S3 연결
description: Amazon 웹 서비스(AWS) S3 스토리지에 대한 라이브 아웃바운드 연결을 생성하여 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 S3 버킷으로 주기적으로 내보냅니다.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 49a59e5b081243679f5d94b03a63d30df22cdc6a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# [!DNL Amazon S3] 연결  {#s3-connection}

## 개요 {#overview}

[!DNL Amazon Web Services](AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 데이터 또는 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예:이메일 주소, 전화 번호, 성)을  [대상 활성화 워크플로의 속성 선택 화면에서 선택합니다](../../ui/activate-destinations.md#select-attributes).

![Amazon S3 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 연결 대상 {#connect-destination}

[!DNL Amazon S3]를 포함하여 클라우드 스토리지 대상에 연결하는 방법에 대한 지침은 [클라우드 스토리지 대상 워크플로우 ](./workflow.md)을 참조하십시오.

[!DNL Amazon S3] 대상의 경우 대상 만들기 작업 과정에 다음 정보를 입력합니다.

* **[!DNL Amazon S3]액세스 키 및  [!DNL Amazon S3] 비밀 키**:에서  [!DNL Amazon S3]쌍을 생성하여  `access key - secret access key` 플랫폼에 사용자 계정에 대한 액세스 권한을  [!DNL Amazon S3] 부여합니다. [Amazon 웹 서비스 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)에서 자세한 내용을 살펴보십시오.

>[!TIP]
>
>연결 대상 작업 과정에서는 내보낸 세그먼트 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 지침은 [매크로를 사용하여 저장소 위치](./workflow.md#use-macros)에 폴더를 만듭니다.

## 필수 [!DNL Amazon S3] 권한 {#required-s3-permission}

데이터를 [!DNL Amazon S3] 저장소 위치에 성공적으로 연결하고 내보내려면 [!DNL Amazon S3]에서 [!DNL Platform]에 대한 IAM(Identity and Access Management) 사용자를 만들고 다음 작업에 대한 권한을 할당합니다.

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


## 내보낸 데이터 {#exported-data}

[!DNL Amazon S3] 대상의 경우 [!DNL Platform]은 사용자가 제공한 저장 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.
