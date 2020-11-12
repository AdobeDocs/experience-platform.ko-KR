---
keywords: Experience Platform;home;popular topics;Azure Event Hubs;azure event hubs;Event Hubs;event hubs
solution: Experience Platform
title: Azure 이벤트 허브 커넥터
topic: overview
description: 아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 Azure 이벤트 허브를 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: e0a0b7fc28b8cc85c5140d3840e06e5c7078c307
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# (베타) Azure 이벤트 허브 커넥터

>[!NOTE]
>
>Azure 이벤트 허브 커넥터가 베타에 있습니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../home.md#terms-and-conditions) 참조하십시오.

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform]및 AWS와 같은 클라우드 제공업체를 위한 기본 연결을 [!DNL Azure]제공합니다. 이러한 시스템에서 얻은 데이터를 [!DNL Platform]

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 [!DNL Platform] 없이 고유한 데이터를 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공식 또는 구분 기호로 형식을 지정할 수 있습니다. 프로세스의 모든 단계는 소스 워크플로우에 통합됩니다. [!DNL Platform] 데이터를 [!DNL Azure Event Hubs] 실시간으로 가져올 수 있습니다.

## IP 주소 허용 목록

소스 커넥터를 사용하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 연결 [!DNL Azure Event Hubs] 을 [!DNL Platform]

아래 설명서에서는 API 또는 사용자 인터페이스 [!DNL Azure Event Hubs] 를 [!DNL Platform] 사용하여 연결하는 방법에 대해 설명합니다.

### API 사용

- [Flow Service API를 사용하여 Azure 이벤트 허브 커넥터 만들기](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Flow Service API를 사용하여 클라우드 스토리지 시스템 살펴보기](../../tutorials/api/explore/cloud-storage.md)
- [Flow Service API를 사용하여 클라우드 스토리지 데이터 수집](../../tutorials/api/collect/cloud-storage.md)

### UI 사용

- [UI에서 Azure 이벤트 허브 원본 커넥터 만들기](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [UI에서 클라우드 스토리지 커넥터에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)