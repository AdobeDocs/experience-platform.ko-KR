---
keywords: Experience Platform;홈;인기 항목;Google PubSub;google pubsub
solution: Experience Platform
title: Google Pub하위 소스 커넥터 개요
topic: overview
description: API 또는 사용자 인터페이스를 사용하여 Google PubSub를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# (베타) [!DNL Google PubSub] 커넥터

>[!NOTE]
>
>[!DNL Google PubSub] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform은 [!DNL AWS], [!DNL Google Cloud Platform] 및 [!DNL Azure] 같은 클라우드 공급자에 대한 기본 연결을 제공하므로 다운스트림 서비스 및 대상에 사용할 수 있도록 이러한 시스템의 데이터를 Platform으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 포맷 또는 업로드 없이도 데이터를 플랫폼에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계가 소스 워크플로우에 통합됩니다. 플랫폼을 사용하면 실시간으로 [!DNL Azure Event Hubs]의 데이터를 가져올 수 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류 또는 비성능이 발생할 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 플랫폼에 [!DNL Google PubSub] 연결

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Google PubSub]을 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [Flow Service API를 사용하여 Google PubSub 소스 연결 만들기](../../tutorials/api/create/cloud-storage/google-pubsub.md)
- [Flow Service API를 사용하여 스트리밍 데이터 수집](../../tutorials/api/collect/streaming.md)

### UI 사용

- [UI에서 Google PubSub 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
- [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)