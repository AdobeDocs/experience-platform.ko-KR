---
title: 피닉스 Source 개요
description: API 또는 사용자 인터페이스를 사용하여 Phoenix 계정을 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 45e6ef18-a0b7-4bb2-b099-b2a878e96637
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# [!DNL Phoenix]

>[!IMPORTANT]
>
>[!DNL Phoenix] 원본은 2025년 5월 말에 사용되지 않습니다. 또는 [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) 소스를 사용할 수도 있습니다.

Adobe Experience Platform 소스는 [[!DNL Phoenix]](https://phoenix.apache.org/index.html) 같은 타사 데이터베이스에서의 데이터 수집을 지원합니다. 이 문서에서는 [!DNL Flow Service] API 또는 Experience Platform 사용자 인터페이스를 통해 [!DNL Phoenix] 계정에 연결하기 전에 필수 구성 요소 정보를 제공합니다.

## IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

아래 설명서는 API 또는 Experience Platform 인터페이스를 사용하여 [!DNL Phoenix]을(를) 사용자에게 연결하는 방법에 대한 정보를 제공합니다.

## API를 사용하여 [!DNL Phoenix]을(를) Experience Platform에 연결

* [흐름 서비스 API를 사용하여 Phoenix 기본 연결 만들기](../../tutorials/api/create/databases/phoenix.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Phoenix]을(를) Experience Platform에 연결

* [Experience Platform 사용자 인터페이스를 사용하여  [!DNL Phoenix] 계정 연결](../../tutorials/ui/create/databases/phoenix.md)
* [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
