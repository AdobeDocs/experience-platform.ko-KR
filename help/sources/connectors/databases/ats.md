---
keywords: Experience Platform;홈;인기 항목;Azure 테이블 저장소;azure 테이블 저장소;ATS;ats
solution: Experience Platform
title: Azure 테이블 저장소 원본 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 Azure 테이블 저장소를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 096e01b1-7e95-4e30-87de-d0976f8b438a
source-git-commit: 5821f9304a37c1a03d17f0113d09548799662a2e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# (베타) [!DNL Azure Table Storage] 커넥터

>[!NOTE]
>
>[!DNL Azure Table Storage] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 를 참조하십시오.

Adobe Experience Platform을 사용하면 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 에서는 타사 데이터베이스에서 데이터를 수집하기 위한 지원을 제공합니다. [!DNL Platform] 관계형, NoSQL 또는 데이터 웨어하우스와 같은 다양한 유형의 데이터베이스에 연결할 수 있습니다. 데이터베이스 공급자에 대한 지원에는 [!DNL Azure Table Storage]이 포함됩니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Azure Table Storage] 소스 커넥터는 현재 플랫폼에 대한 동일한 영역 연결을 지원하지 않습니다. 즉, Azure 인스턴스가 플랫폼과 동일한 네트워크 영역을 사용하는 경우 플랫폼 원본에 대한 연결을 설정할 수 없습니다. 현재는 교차 영역 연결만 지원됩니다. 자세한 내용은 Adobe 계정 관리자에게 문의하십시오.

아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Azure Table Storage]을 [!DNL Platform]에 연결하는 방법에 대해 설명합니다.

## API를 사용하여 [!DNL Azure Table Storage]을 [!DNL Platform]에 연결

- [Flow Service API를 사용하여 Azure 테이블 저장소 기본 연결을 만듭니다](../../tutorials/api/create/databases/ats.md)
- [Flow Service API를 사용하여 데이터베이스 소스의 데이터 구조 및 컨텐츠를 탐색합니다](../../tutorials/api/explore/database-nosql.md)
- [Flow Service API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Azure Table Storage]을 [!DNL Platform]에 연결

- [UI에서 Azure 테이블 저장소 소스 연결 만들기](../../tutorials/ui/create/databases/ats.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
