---
description: Destination SDK을 사용하려면 파트너 회사가 이 문서에 나열된 사전 요구 사항을 충족해야 합니다.
title: 통합 사전 요구 사항
exl-id: 031af9f1-ce18-4056-bd53-199ce8b56be5
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 통합 사전 요구 사항

Destination SDK을 사용하려면 아래 섹션에 나열된 기술 및 파트너십 사전 요구 사항을 충족하는지 확인하십시오.

## 스트리밍 대상을 위한 기술/API 사전 요구 사항 {#streaming-prerequisites}

1. Adobe Experience Platform에 다음 유형의 데이터를 전달할 수 있는 REST API 엔드포인트가 있습니다.
   * 대상자 멤버십 정보;
   * 프로필 신원 정보;
   * (선택 사항) 프로필 강화를 위한 추가 속성입니다.
2. REST API 끝점은 기본, 전달자 토큰 또는 OAuth 2.0 인증 프로토콜을 지원합니다.
3. (선택 사항) 프로그래밍 방식 메타데이터 관리를 위한 API 또는 API 엔드포인트 만들기/업데이트/삭제가 제공됩니다.

## 일괄 처리 대상을 위한 기술 사전 요구 사항 {#batch-prerequisites}

1. 에 호스팅된 대상 위치가 있습니다. [!DNL Amazon S3], [!DNL Azure Blob], [!DNL Azure Data Lake Storage], [!DNL SFTP], [!DNL Google Cloud], 또는 비공개 [!DNL Data Landing Zone]: Experience Platform 외부로 내보낸 파일을 받을 수 있습니다.
2. 대상 플랫폼은 를 통해 구성된 형식의 파일을 수집할 수 있습니다. [파일 서식 옵션](functionality/destination-server/file-formatting.md) 배치 대상 Destination SDK
3. (선택 사항) 대상자 만들기/검색/업데이트/삭제가 있습니다([!DNL CRUD]) 프로그래밍 방식의 메타데이터 관리를 위한 API 또는 API 엔드포인트.

## 파트너십 사전 요구 사항 {#partnership-prerequisites}

Destination SDK을 사용하려는 ISV(Independent Software Vendor) 또는 SI(System Integrator)인 경우 [액세스 섹션을 가져오는 중](overview.md#get-access).
