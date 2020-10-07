---
keywords: Experience Platform;home;popular topics;Phoenix;phoenix
solution: Experience Platform
title: Phoenix 커넥터
topic: overview
description: 아래 설명서에서는 API 또는 사용자 인터페이스를 사용하여 Phoenix를 Platform에 연결하는 방법에 대한 정보를 제공합니다.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# (베타) [!DNL Phoenix] 커넥터

>[!NOTE]
>
>커넥터의 [!DNL Phoenix] 베타입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../home.md#terms-and-conditions) 참조하십시오.

Adobe Experience Platform은 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있도록 허용합니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등 다양한 소스의 데이터를 인제스트할 수 있습니다.

[!DNL Experience Platform] 타사 데이터베이스의 데이터 인제스트 지원을 제공합니다. [!DNL Platform] 관계형, NoSQL 또는 데이터 웨어하우스와 같은 다양한 유형의 데이터베이스에 연결할 수 있습니다. 데이터베이스 공급자에 대한 지원에는 다음이 포함됩니다 [!DNL Phoenix].

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

아래 설명서에서는 API 또는 사용자 인터페이스 [!DNL Phoenix] 를 [!DNL Platform] 사용하여 연결하는 방법에 대해 설명합니다.

## API [!DNL Phoenix] 를 [!DNL Platform] 사용하는 데 연결

- [Flow Service API를 사용하여 Phoenix 커넥터 만들기](../../tutorials/api/create/databases/phoenix.md)
- [Flow Service API를 사용하여 데이터베이스 시스템 살펴보기](../../tutorials/api/explore/database-nosql.md)
- [Flow Service API를 사용하여 데이터베이스에서 데이터 수집](../../tutorials/api/collect/database-nosql.md)

## UI [!DNL Phoenix] 를 [!DNL Platform] 사용하는 데 연결

- [UI에서 Phoenix 소스 커넥터 만들기](../../tutorials/ui/create/databases/phoenix.md)
- [UI에서 데이터베이스 커넥터에 대한 데이터 흐름 구성](../../tutorials/ui/dataflow/databases.md)