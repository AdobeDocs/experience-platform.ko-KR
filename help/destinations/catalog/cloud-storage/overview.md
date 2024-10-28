---
keywords: 클라우드 스토리지 대상;클라우드 스토리지
title: 클라우드 스토리지 대상 개요
description: Adobe Experience Platform은 대상을 Amazon S3, AWS Kinesis, Azure Event Hubs 또는 SFTP 클라우드 스토리지 위치에 데이터 파일로 전달할 수 있습니다.
exl-id: d29f0a6e-b323-4f78-bbd0-dee2f1e0fedb
source-git-commit: 2e21e62de624c5e7e9fac4d36dbf41b46198062a
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 5%

---

# 클라우드 스토리지 대상 개요 {#cloud-storage-destinations}

## 개요 {#overview}

Adobe Experience Platform은 대상을 클라우드 스토리지 위치에 데이터 파일로 제공할 수 있습니다. 이렇게 하면 [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage Gen2], [!DNL Data Landing Zone], [!DNL Google Cloud Storage] 및 SFTP에 대한 CSV 파일을 통해 대상자와 해당 프로필 속성을 내부 시스템으로 보낼 수 있습니다. [!DNL Amazon Kinesis] 및 [!DNL Azure Event Hubs] 대상의 경우 데이터가 Experience Platform 밖으로 [!DNL JSON] 형식으로 스트리밍됩니다.

![Adobe 클라우드 저장소 대상](../../assets/catalog/cloud-storage/cloud-storage-destinations.png)

## 지원되는 클라우드 스토리지 대상 {#supported-destinations}

Adobe Experience Platform은 다음 클라우드 스토리지 대상으로 데이터 내보내기를 지원합니다.

* [Amazon Kinesis 연결](amazon-kinesis.md)
* [Amazon S3 연결](amazon-s3.md)
* [Azure Blob 연결](azure-blob.md)
* [Azure Data Lake Storage Gen2](adls-gen2.md)
* [Azure 이벤트 허브 연결](azure-event-hubs.md)
* [데이터 랜딩 구역](data-landing-zone.md)
* [Google 클라우드 스토리지](google-cloud-storage.md)
* [SFTP 연결](sftp.md)

## 새 클라우드 스토리지 대상에 연결 {#connect-destination}

캠페인을 위해 대상을 클라우드 스토리지 대상으로 보내려면 먼저 플랫폼에서 대상에 연결해야 합니다. 새 대상 설정에 대한 자세한 내용은 [대상 만들기 자습서](../../ui/connect-destination.md)를 참조하십시오.


## 매크로를 사용하여 스토리지 위치에 폴더 만들기 {#use-macros}

>[!NOTE]
>
> 이 섹션에서 설명하는 기능은 모든 클라우드 스토리지 대상에 사용할 수 있습니다. 그러나 [Amazon S3](amazon-s3.md) 대상은 현재 `%SEGMENT_ID%` 및 `%SEGMENT_NAME%` 매크로만 지원합니다.

저장소 위치의 대상 파일별로 사용자 지정 폴더를 만들려면 폴더 경로 입력 필드의 매크로를 사용할 수 있습니다. 아래와 같이 입력 필드의 끝에 매크로를 삽입합니다.

![매크로를 사용하여 저장소에 폴더를 만드는 방법](../../assets/catalog/cloud-storage/workflow/macros-folder-path.png)

아래 예제에서는 ID가 `25768be6-ebd5-45cc-8913-12fb3f348615`인 샘플 대상 `Luxury Audience`을(를) 참조합니다.

**매크로 1:`%SEGMENT_NAME%`**

입력: `acme/campaigns/2021/%SEGMENT_NAME%`
저장소 위치의 폴더 경로: `acme/campaigns/2021/Luxury Audience`

**매크로 2:`%SEGMENT_ID%`**

입력: `acme/campaigns/2021/%SEGMENT_ID%`
저장소 위치의 폴더 경로: `acme/campaigns/2021/25768be6-ebd5-45cc-8913-12fb3f348615`

**매크로 3:`%SEGMENT_NAME%/%SEGMENT_ID%`**

입력: `acme/campaigns/2021/%SEGMENT_NAME%/%SEGMENT_ID%`
저장소 위치의 폴더 경로: `acme/campaigns/2021/Luxury Audience/25768be6-ebd5-45cc-8913-12fb3f348615`

**추가 매크로**

위의 예제와 유사하게 추가 매크로를 사용하여 폴더 위치에 사용자 지정 폴더 구조를 만들 수 있습니다.

* `%DATETIME%` 또는 `%TIMESTAMP%`을(를) 통해 파일의 내보내기 시간을 기준으로 사용자 지정 폴더 이름을 추가할 수 있습니다. 첫 번째 매크로의 형식은 `MMDDYYYY_HHMMSS`이고 두 번째 매크로의 UNIX 10자리 형식입니다.
* 대상 데이터 흐름의 이름을 기반으로 사용자 지정 폴더를 추가하려면 `%DESTINATION_NAME%`.

## 데이터 내보내기 유형 {#export-type}

클라우드 스토리지 대상은 다음 내보내기 유형을 지원합니다.
* **프로필 기반 내보내기**. 즉, 대상의 개인에 대한 세부 정보를 내보내고 있습니다. 이러한 세부 사항은 개인화에 필요하며 속성, 이벤트, 대상 멤버십 등을 포함할 수 있습니다.
* **데이터 집합 내보내기**. 이 기능을 사용하면 전체 데이터 세트를 클라우드 스토리지 대상으로 내보낼 수 있습니다. 기능에 대해 [자세히 읽어보세요](/help/destinations/ui/export-datasets.md).

## 다음 단계 {#next-steps}

사용할 [지원되는 클라우드 대상 중 하나](#supported-destinations)를 선택한 후 [대상에 연결 자습서](/help/destinations/ui/connect-destination.md)를 읽고 대상에 연결하는 방법을 알아보십시오. 그런 다음 파일 기반 대상으로 활성화 자습서를 읽고 클라우드 저장소 대상으로 [데이터 내보내기](/help/destinations/ui/activate-batch-profile-destinations.md)를 시작하는 방법을 알아보십시오.
