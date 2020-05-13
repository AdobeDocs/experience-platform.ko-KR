---
title: 클라우드 스토리지 대상
seo-title: 클라우드 스토리지 대상
description: Adobe 실시간 CDP는 세그먼트를 데이터 파일로 Amazon S3, AWS Kinesis, Azure 이벤트 허브 또는 SFTP 클라우드 스토리지 위치에 전달할 수 있습니다.
seo-description: Adobe 실시간 CDP는 세그먼트를 데이터 파일로 Amazon S3, AWS Kinesis, Azure 이벤트 허브 또는 SFTP 클라우드 스토리지 위치에 전달할 수 있습니다.
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# 클라우드 스토리지 대상 {#cloud-storage-destinations}

Adobe 실시간 CDP를 사용하면 세그먼트를 데이터 파일로 클라우드 스토리지 위치에 전달할 수 있습니다. 이렇게 하면 Amazon S3 및 SFTP에 대해 CSV 또는 탭으로 구분된 파일을 통해 대상과 프로필 속성을 내부 시스템으로 보낼 수 있습니다. AWS Kinesis 및 Azure 이벤트 허브 대상의 경우 데이터는 JSON 형식으로 경험 플랫폼에서 스트리밍됩니다.

![Adobe Cloud 스토리지 대상](/help/rtcdp/destinations/assets/cloud-storage-destinations.png)

클라우드 스토리지 대상에 연결하는 방법에 대한 자세한 내용은 클라우드 스토리지 [대상을 만드는 워크플로우를 참조하십시오](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md).

## 데이터 내보내기 유형

**프로필 기반 내보내기** - 대상 내 개인에 대한 세부 정보를 내보냅니다. 이러한 세부 사항은 개인화에 필요하며 속성, 이벤트, 세그먼트 멤버십 등을 포함할 수 있습니다.

## 사용 가능한 클라우드 스토리지 대상

* [Amazon S3 대상](/help/rtcdp/destinations/amazon-s3-destination.md)
* [SFTP 대상](/help/rtcdp/destinations/sftp-destination.md)

## 사용 가능한 클라우드 스토리지 스트리밍 대상

* [Amazon Kinesis 대상](/help/rtcdp/destinations/amazon-kinesis-destination.md)
* [Azure EventHub 대상](/help/rtcdp/destinations/azure-event-hubs-destination.md)