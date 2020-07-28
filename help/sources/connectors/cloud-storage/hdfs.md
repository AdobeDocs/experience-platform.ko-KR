---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: HDFS 커넥터
topic: overview
translation-type: tm+mt
source-git-commit: 340f5d0611e9e9eb4676018ee10c8a8aa08dbb2d
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# (베타) [!DNL Apache] HDFS 커넥터

>[!NOTE]
>Apache HDFS 커넥터가 베타 버전입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../home.md#terms-and-conditions) 참조하십시오.

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform]및 [!DNL Azure]와 같은 클라우드 제공업체를 위한 기본 연결을 제공하므로 이러한 시스템에서 데이터를 가져올 수 있습니다. 인제스트된 데이터는 JSON, 쪽모이 세공된 데이터 또는 구분 기호로 형식을 지정할 수 있습니다. 클라우드 스토리지 공급자에 대한 지원에는 HDFS가 [!DNL Apache] 포함됩니다.

## IP 주소 허용 목록

소스 커넥터를 사용하기 전에 다음 IP 주소를 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다.

### 미국 동부 지역

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### 서유럽 지역

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### 오스트레일리아 동부

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Apache] HDFS를 연결하는 방법에 [!DNL Platform] 대한 정보를 제공합니다.

## API [!DNL Apache] 를 [!DNL Platform] 사용하여 HDFS 연결

- [Flow Service API를 사용하여 HDFS 커넥터 만들기](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Flow Service API를 사용하여 클라우드 스토리지 시스템 살펴보기](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 데이터 수집](../../tutorials/api/collect/cloud-storage.md)

## UI [!DNL Apache] 를 [!DNL Platform] 사용하여 HDFS 연결

- [UI에서 Apache HDFS 소스 커넥터 만들기](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [UI에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/batch/cloud-storage.md)