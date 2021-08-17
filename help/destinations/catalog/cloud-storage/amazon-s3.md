---
keywords: Amazon S3;S3 대상;s3;amazon s3
title: Amazon S3 연결
description: AWS(Amazon Web Services) S3 스토리지에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭 구분 또는 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# [!DNL Amazon S3] 연결 {#s3-connection}

## 개요 {#overview}

[!DNL Amazon Web Services] (AWS) S3 스토리지에 대한 라이브 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭 구분 또는 CSV 데이터 파일을 고유한 S3 버킷으로 주기적으로 내보냅니다.

## 내보내기 유형 {#export-type}

**프로필 기반**  - 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다(예: 대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 이메일 주소,  [전화 번호, 성)](../../ui/activate-destinations.md#select-attributes).

![Amazon S3 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!DNL Amazon S3]액세스** 키 및  **[!DNL Amazon S3]암호 키**: 에서  [!DNL Amazon S3]쌍을  `access key - secret access key` 생성하여 계정에 대한 플랫폼 액세스 권한을  [!DNL Amazon S3] 부여합니다. 자세한 내용은 [Amazon 웹 서비스 설명서](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)를 참조하십시오.
* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 버킷 이름]**: 이 대상에서 사용할  [!DNL Amazon S3] 버킷의 이름을 입력합니다.
* **[!UICONTROL 폴더 경로]**: 내보낸 파일을 호스팅할 대상 폴더의 경로를 입력합니다.

선택적으로 RSA 형식의 공개 키를 첨부하여 내보낸 파일에 암호화를 추가할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩 문자열로 기록해야 합니다.

>[!TIP]
>
>연결 대상 워크플로우에서 내보낸 세그먼트 파일당 Amazon S3 저장소에 사용자 지정 폴더를 만들 수 있습니다. 자세한 내용은 [매크로를 사용하여 저장소 위치에 폴더를 만듭니다](overview.md#use-macros).

### 필요한 [!DNL Amazon S3] 권한 {#required-s3-permission}

데이터를 [!DNL Amazon S3] 저장소 위치에 성공적으로 연결하고 내보내려면 [!DNL Amazon S3]에서 [!DNL Platform]에 대한 IAM(Identity and Access Management) 사용자를 만들고 다음 작업에 대한 권한을 지정하십시오.

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

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상 세그먼트 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

[!DNL Amazon S3] 대상의 경우 [!DNL Platform]은 사용자가 제공한 저장소 위치에 탭으로 구분된 `.csv` 파일을 만듭니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상](../../ui/activate-destinations.md#esp-and-cloud-storage)을 참조하십시오.
