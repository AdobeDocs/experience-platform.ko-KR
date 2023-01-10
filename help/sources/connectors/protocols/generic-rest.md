---
keywords: Experience Platform;홈;인기 항목;일반 REST;일반 REST
solution: Experience Platform
title: 일반 REST API 소스 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Adobe Experience Platform에 일반 REST API를 연결하는 방법을 알아봅니다.
exl-id: e3449e33-7261-4aa2-bce9-5530eb4fcc68
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# (베타) [!DNL Generic REST API]

>[!NOTE]
>
>다음 [!DNL Generic REST API] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

Adobe Experience Platform을 사용하면 를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다 [!DNL Platform] 서비스. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

플랫폼은 다음을 포함한 프로토콜 응용 프로그램에서 데이터를 수집하도록 지원합니다 [!DNL Generic REST API].

다음 [!DNL Generic REST API] 소스를 사용하면 REST 기반 애플리케이션의 데이터를 플랫폼으로 가져올 수 있습니다. [!DNL Generic REST API] 에서는 기본 인증 및 OAuth 2 새로 고침 코드 기반 인증을 모두 지원합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

아래 설명서에서는 [!DNL Generic REST API] api를 사용하여 Platform에 소스를 전송하는 중입니다.

## Connect [!DNL Generic REST API] to [!DNL Platform] api 사용

- [Flow Service API를 사용하여 일반 REST API 기본 연결을 만듭니다](../../tutorials/api/create/protocols/generic-rest.md)
- [Flow Service API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [Flow Service API를 사용하여 프로토콜 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/protocols.md)
