---
keywords: Experience Platform;홈;인기 항목;Azure 이벤트 허브;azure 이벤트 허브;이벤트 허브;이벤트 허브;이벤트 허브
solution: Experience Platform
title: Azure 이벤트 허브 원본 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 Azure 이벤트 허브를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
translation-type: tm+mt
source-git-commit: 6dac267be93241bffb4eb5092a6e8da5093c63a6
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# [!DNL Azure Event Hubs] 커넥터

Adobe Experience Platform은 AWS, [!DNL Google Cloud Platform] 및 [!DNL Azure] 같은 클라우드 공급자에 대한 기본 연결을 제공합니다. 이러한 시스템의 데이터를 [!DNL Platform]으로 가져올 수 있습니다.

클라우드 스토리지 소스는 다운로드, 형식 지정 또는 업로드할 필요 없이 자신의 데이터를 [!DNL Platform]에 가져올 수 있습니다. 인제스트된 데이터는 XDM JSON, XDM 쪽모이 세공 마루 또는 구분된 형태로 포맷될 수 있습니다. 프로세스의 모든 단계가 소스 워크플로우에 통합됩니다. [!DNL Platform] 데이터를 실시간으로 가져올 수  [!DNL Azure Event Hubs] 있습니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류 또는 비성능이 발생할 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## [!DNL Azure Event Hubs]을(를) [!DNL Platform]에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Azure Event Hubs]을 [!DNL Platform]에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [흐름 서비스 API를 사용하여 Azure 이벤트 허브 원본 연결 만들기](../../tutorials/api/create/cloud-storage/eventhub.md)
- [Flow Service API를 사용하여 스트리밍 데이터 수집](../../tutorials/api/collect/streaming.md)

### UI 사용

- [UI에서 Azure 이벤트 허브 소스 연결 만들기](../../tutorials/ui/create/cloud-storage/eventhub.md)
- [UI에서 클라우드 스토리지 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
