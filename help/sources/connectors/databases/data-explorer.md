---
keywords: Experience Platform;홈;인기 항목;Azure Data Explorer;azure 데이터 탐색기
solution: Experience Platform
title: Azure Data Explorer 원본 커넥터 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 Azure Data Explorer을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 869bd8bb-51e6-4e0c-a3ec-ff083dda5789
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# (베타) [!DNL Azure Data Explorer] 커넥터

>[!NOTE]
>
>[!DNL Azure Data Explorer] 커넥터가 베타에 있습니다. 베타 레이블이 지정된 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform은 [!DNL Microsoft], MySQL 및 [!DNL Azure] 같은 데이터베이스 공급자에 대한 기본 연결을 제공합니다. 이러한 시스템의 데이터를 [!DNL Platform]으로 가져올 수 있습니다.

관계형, NoSQL 또는 데이터 웨어하우스를 비롯한 다양한 유형의 타사 데이터베이스가 지원됩니다. 데이터베이스 공급자에 대한 지원에는 [!DNL Azure Data Explorer]이 포함됩니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역 특정 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류 또는 비성능이 발생할 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

>[!IMPORTANT]
>
>현재 [!DNL Azure Data Explorer] 소스 커넥터는 플랫폼에 동일한 영역 연결을 지원하지 않습니다. 즉, Azure 인스턴스가 플랫폼과 동일한 네트워크 영역을 사용하는 경우 플랫폼 소스에 대한 연결을 설정할 수 없습니다. 현재 교차 영역 연결만 지원됩니다. 자세한 내용은 Adobe 계정 관리자에게 문의하십시오.

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Azure Data Explorer]을 [!DNL Platform]에 연결하는 방법에 대한 정보를 제공합니다.

## API를 사용하여 [!DNL Azure Data Explorer]을 [!DNL Platform]에 연결

- [흐름 서비스 API를 사용하여 Azure Data Explorer 원본 연결 만들기](../../tutorials/api/create/databases/data-explorer.md)
- [Flow Service API를 사용하여 데이터베이스 시스템 살펴보기](../../tutorials/api/explore/database-nosql.md)
- [Flow Service API를 사용하여 데이터베이스에서 데이터 수집](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Azure Data Explorer]을 [!DNL Platform]에 연결

- [UI에서 Azure Data Explorer 원본 연결 만들기](../../tutorials/ui/create/databases/data-explorer.md)
- [UI에서 데이터베이스 연결에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/databases.md)
