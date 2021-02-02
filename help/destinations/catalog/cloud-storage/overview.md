---
keywords: 클라우드 스토리지 대상;클라우드 스토리지
title: 클라우드 스토리지 대상
seo-title: 클라우드 스토리지 대상
description: 플랫폼은 세그먼트를 Amazon S3, AWS Kinesis, Azure 이벤트 허브 또는 SFTP 클라우드 스토리지 위치에 데이터 파일로 제공할 수 있습니다.
seo-description: 플랫폼은 세그먼트를 Amazon S3, AWS Kinesis, Azure 이벤트 허브 또는 SFTP 클라우드 스토리지 위치에 데이터 파일로 제공할 수 있습니다.
translation-type: tm+mt
source-git-commit: b348a5493b13112291dd8e9234d457ff8c694147
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---


# 클라우드 스토리지 대상 {#cloud-storage-destinations}

Adobe Experience Platform은 세그먼트를 데이터 파일로 클라우드 스토리지 위치에 전달할 수 있습니다. 이렇게 하면 [!DNL Amazon S3] 및 SFTP에 대해 CSV 또는 탭으로 구분된 파일을 통해 대상과 프로필 속성을 내부 시스템으로 보낼 수 있습니다. [!DNL AWS Kinesis] 및 [!DNL Azure Event Hubs] 대상의 경우 데이터는 JSON 형식의 Experience Platform에서 스트리밍됩니다.

![Adobe 클라우드 스토리지 대상](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

클라우드 스토리지 대상에 연결하는 방법에 대한 자세한 내용은 [클라우드 스토리지 대상 만들기 작업 과정](./workflow.md)을 참조하십시오.

## 데이터 내보내기 유형

**프로필 기반 내보내기**  - 대상 내 개인 정보를 내보냅니다. 이러한 세부 사항은 개인화에 필요하며 속성, 이벤트, 세그먼트 멤버십 등을 포함할 수 있습니다.

## 사용 가능한 클라우드 스토리지 대상

- [Amazon S3 대상](./amazon-s3.md)
- [Azure Blob 대상](./azure-blob.md)
- [SFTP 대상](./sftp.md)

## 사용 가능한 클라우드 스토리지 스트리밍 대상

- [Amazon Kinesis 대상](./amazon-kinesis.md)
- [Azure 이벤트 허브 대상](./azure-event-hubs.md)