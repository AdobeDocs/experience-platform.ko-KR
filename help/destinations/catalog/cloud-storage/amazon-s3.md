---
keywords: Amazon S3;S3 destination;s3;amazon s3
title: Amazon S3 대상
seo-title: Amazon S3 대상
description: Amazon 웹 서비스(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.
seo-description: Amazon 웹 서비스(AWS) S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.
translation-type: tm+mt
source-git-commit: f2fdc3b75d275698a4b1e4c8969b1b840429c919
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# [!DNL Amazon S3] 대상

## 개요

AWS) [!DNL Amazon Web Services] S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 Adobe Experience Platform에서 탭으로 구분된 또는 CSV 데이터 파일을 사용자 자신의 S3 버킷으로 주기적으로 내보냅니다.

## 내보내기 유형 {#export-type}

**프로필 기반** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예:이메일 주소, 전화 번호, 성)을 [대상 활성화 워크플로우의 속성 선택 화면에서 선택한 대로 선택합니다](../../ui/activate-destinations.md#select-attributes).

![Amazon S3 프로필 기반 내보내기 유형](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## 연결 대상 {#connect-destination}

클라우드 [스토리지 대상 워크플로우 ](./workflow.md) 에서 클라우드 스토리지 대상에 연결하는 방법에 대한 지침을 참조하십시오 [!DNL Amazon S3].

대상에 대해 [!DNL Amazon S3] 대상 만들기 워크플로우에서 다음 정보를 입력합니다.

* **[!DNL Amazon S3]액세스 키 및 [!DNL Amazon S3] 비밀 키**:이 [!DNL Amazon S3]에서 `access key - secret access key` 쌍을 생성하여 계정에 대한 실시간 CDP 액세스 권한을 [!DNL Amazon S3] 부여합니다. 자세한 내용은 [Amazon 웹 서비스 문서를 참조하십시오](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

>[!IMPORTANT]
>
>실시간 CDP는 내보내기 파일이 전달되는 버킷 객체에 대한 `write` 권한이 필요합니다.

## 내보낸 데이터 {#exported-data}

대상에 대해 [!DNL Amazon S3] 실시간 CDP는 사용자가 제공한 스토리지 위치에 탭으로 구분된 `.txt` 또는 `.csv` 파일을 생성합니다. 파일에 대한 자세한 내용은 세그먼트 활성화 자습서에서 [이메일 마케팅 대상 및 클라우드 스토리지 대상을](../../ui/activate-destinations.md#esp-and-cloud-storage) 참조하십시오.
