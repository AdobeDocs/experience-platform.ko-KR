---
keywords: Experience Platform;홈;인기 항목;일반 REST;일반 REST
solution: Experience Platform
title: 일반 REST API Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 일반 REST API를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# (Beta) [!DNL Generic REST API]

>[!NOTE]
>
>[!DNL Generic REST API] 원본이 Beta 버전입니다. 베타 레이블 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform에서는 [!DNL Generic REST API]을(를) 포함한 프로토콜 응용 프로그램에서 데이터를 수집할 수 있도록 지원합니다.

[!DNL Generic REST API] 소스를 사용하면 REST 기반 응용 프로그램의 데이터를 Experience Platform으로 가져올 수 있습니다. [!DNL Generic REST API]은(는) 기본 인증과 OAuth 2 새로 고침 코드 기반 인증을 모두 지원합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

아래 설명서에서는 API를 사용하여 [!DNL Generic REST API] 소스를 Experience Platform에 연결하는 방법에 대한 정보를 제공합니다.

## API를 사용하여 [!DNL Generic REST API]을(를) [!DNL Experience Platform]에 연결

- [흐름 서비스 API를 사용하여 일반 REST API 기본 연결 만들기](../../tutorials/api/create/protocols/generic-rest.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 프로토콜 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/protocols.md)
