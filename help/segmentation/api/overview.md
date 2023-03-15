---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;API;API;
title: 세그먼테이션 서비스 API 안내서
description: 개발자는 세그멘테이션 서비스 API를 사용하여 Adobe Experience Platform의 세그멘테이션 작업을 프로그래밍 방식으로 관리할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 3%

---

# 세그먼테이션 서비스 API 안내서

[!DNL Adobe Experience Platform Segmentation Service] 에서 세그먼트를 작성하고 대상자를 생성할 수 있습니다. [!DNL Adobe Experience Platform] (으)로부터 [!DNL Real-Time Customer Profile] 데이터.

다음 [!DNL Segmentation Service] API는에서 세그멘테이션 작업을 프로그래밍 방식으로 관리할 수 있는 여러 끝점을 제공합니다 [!DNL Experience Platform]. 이 개요 문서에서는 이러한 각 엔드포인트에 대한 높은 수준의 소개를 제공하고 자세한 내용을 보려면 관련 엔드포인트 안내서에 대한 링크를 제공합니다. 개별 엔드포인트 안내서를 읽기 전에 [시작 안내서](./getting-started.md) 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 제공합니다.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [세그먼테이션 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/segmentation/).

<!-- ## Audiences

Audiences are a collection of people who share similar behaviors and/or characteristics. These can be generated either by using Platform or from external sources. You can use the `/audiences` endpoint to retrieve all audiences, create a new audience, retrieve details of a specific audience, update a specific audience, or delete a specific audience.

For more information on using this endpoint, please read the [audiences endpoint guide](./audiences.md). -->

## 내보내기 작업

내보내기 작업은 대상 세그먼트 구성원을 데이터 세트로 지속하는 데 사용되는 비동기 프로세스입니다. 다음을 사용할 수 있습니다. `/export/jobs` 모든 내보내기 작업을 검색하거나, 새 내보내기 작업을 생성하거나, 특정 내보내기 작업의 세부 정보를 검색하거나, 특정 내보내기 작업을 취소하기 위한 끝점입니다.

이 엔드포인트 사용에 대한 자세한 내용은 [내보내기 작업 엔드포인트 안내서](./export-jobs.md).

## 미리 보기 및 예상

미리 보기는 세그먼트 정의에 대해 페이지가 매겨진 자격 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다. 다음을 사용할 수 있습니다. `/preview` 새 미리보기 작업을 만들거나 특정 미리보기 작업의 결과를 조회하기 위한 끝점입니다.

예상치는 예상 대상 크기, 신뢰 구간 및 오류 표준 편차와 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 다음을 사용할 수 있습니다. `/estimate` 세그먼트 정의의 예상 값을 보기 위한 끝점입니다.

이러한 엔드포인트 사용에 대한 자세한 내용은 [미리 보기 및 예상 끝점 안내서](./previews-and-estimates.md).

## 일정

예약은 하루에 한 번 배치 세분화 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. 다음을 사용할 수 있습니다. `/config/schedules` 일정 목록을 검색하거나, 새 일정을 만들거나, 특정 일정의 세부 정보를 검색하거나, 특정 일정을 업데이트하거나, 특정 일정을 삭제하는 끝점입니다.

이 엔드포인트 사용에 대한 자세한 내용은 [일정 끝점 안내서](./schedules.md).

## 세그먼트 정의

세그먼트 정의는 대상 세그먼트에 포함될 프로필을 정의합니다. 다음을 사용할 수 있습니다. `/segment/definitions` 세그먼트 정의를 관리하기 위한 끝점입니다.

이 엔드포인트 사용에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서](./segment-definitions.md).

## 세그먼트 작업

세그먼트 작업은 이전에 설정한 세그먼트 정의를 처리하여 대상 세그먼트를 생성합니다. 다음을 사용할 수 있습니다. `/segment/jobs` 세그먼트 작업을 관리할 끝점입니다.

이 엔드포인트 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](./segment-jobs.md).

## 세그먼트 검색

세그먼트 검색은 다양한 데이터 소스에 걸쳐 포함된 필드를 검색하고 이를 실시간에 가깝게 반환하는 데 사용됩니다. 세그먼트 검색 작업을 시작하려면 다음을 참조하십시오 [검색 끝점 안내서](segment-search.md)

## 다음 단계

을(를) 시작하려면 [!DNL Segmentation Service] API에서 서비스의 다양한 끝점을 호출하는 방법에 대한 자세한 단계는 다양한 끝점 안내서를 검토하십시오. 를 사용하여 세그먼트 작업에 대해 자세히 알아보려면 [!DNL Platform] UI에서 다음을 참조하십시오. [세그먼테이션 사용 안내서](../ui/overview.md).
