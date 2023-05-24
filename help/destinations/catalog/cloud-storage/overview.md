---
keywords: 클라우드 스토리지 대상;클라우드 스토리지
title: 클라우드 스토리지 대상 개요
description: Adobe Experience Platform은 세그먼트를 Amazon S3, AWS Kinesis, Azure Event Hubs 또는 SFTP 클라우드 스토리지 위치에 데이터 파일로 전달할 수 있습니다.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 4a4c82cc4528fe07bbdb75ae9f795bdbab48c089
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 3%

---

# 클라우드 스토리지 대상 개요 {#cloud-storage-destinations}

## 개요 {#overview}

Adobe Experience Platform은 세그먼트를 클라우드 스토리지 위치에 데이터 파일로 제공할 수 있습니다. 이렇게 하면 대상 및 해당 프로필 속성을 의 CSV 파일을 통해 내부 시스템으로 전송할 수 있습니다. [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage]및 SFTP입니다. 대상 [!DNL Amazon Kinesis] 및 [!DNL Azure Event Hubs] 대상, 데이터가 Experience Platform에서 스트리밍됨 [!DNL JSON] 포맷.

![Adobe 클라우드 스토리지 대상](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 지원되는 클라우드 스토리지 대상 {#supported-destinations}

Adobe Experience Platform은 다음 클라우드 스토리지 대상을 지원합니다.

* [Amazon Kinesis 연결](amazon-kinesis.md)
* [Amazon S3 연결](amazon-s3.md)
* [Azure Blob 연결](azure-blob.md)
* [(베타) Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure 이벤트 허브 연결](azure-event-hubs.md)
* [(베타) 데이터 랜딩 영역](data-landing-zone.md)
* [(베타) Google 클라우드 스토리지](google-cloud-storage.md)
* [SFTP 연결](sftp.md)

## 새 클라우드 스토리지 대상에 연결 {#connect-destination}

캠페인을 위해 세그먼트를 클라우드 스토리지 대상으로 보내려면 먼저 플랫폼이 대상에 연결되어야 합니다. 다음을 참조하십시오. [대상 만들기 튜토리얼](../../ui/connect-destination.md) 새 대상 설정에 대한 자세한 정보.


## 매크로를 사용하여 스토리지 위치에 폴더 만들기 {#use-macros}

>[!NOTE]
>
> 이 섹션에서 설명하는 기능은 현재 다음에 대해 사용할 수 있습니다. [Amazon](amazon-s3.md) 대상만 해당.

저장소 위치의 세그먼트 파일별로 사용자 지정 폴더를 만들려면 폴더 경로 입력 필드의 매크로를 사용할 수 있습니다. 아래와 같이 입력 필드의 끝에 매크로를 삽입합니다.

![매크로를 사용하여 저장소에 폴더를 만드는 방법](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

아래 예제는 샘플 세그먼트를 참조합니다 `Luxury Audience` (ID 포함) `25768be6-ebd5-45cc-8913-12fb3f348615`.

**매크로 1:`%SEGMENT_NAME%`**

입력: `acme/campaigns/2021/%SEGMENT_NAME%`
저장소 위치의 폴더 경로: `acme/campaigns/2021/Luxury Audience`

**매크로 2:`%SEGMENT_ID%`**

입력: `acme/campaigns/2021/%SEGMENT_ID%`
저장소 위치의 폴더 경로: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**매크로 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

입력: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
저장소 위치의 폴더 경로: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

## 데이터 내보내기 유형 {#export-type}

클라우드 스토리지 대상 지원 **프로필 기반 내보내기**. 즉, 대상의 개인에 대한 세부 정보를 내보내고 있습니다. 이러한 세부 사항은 개인화에 필요하며 속성, 이벤트, 세그먼트 멤버십 등을 포함할 수 있습니다.