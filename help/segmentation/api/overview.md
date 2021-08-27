---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;API;api;
title: Segmentation Service API 안내서
topic-legacy: guide
description: 세그먼테이션 서비스 API를 사용하여 개발자는 Adobe Experience Platform에서 세그먼테이션 작업을 프로그래밍 방식으로 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법을 알아보려면 이 안내서를 따르십시오.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Segmentation Service API 안내서

[!DNL Adobe Experience Platform Segmentation Service] 에서는 데이터를 통해 세그먼트를 작성하고 대상 [!DNL Adobe Experience Platform] 을 생성할 수  [!DNL Real-time Customer Profile] 있습니다.

[!DNL Segmentation Service] API는 [!DNL Experience Platform]에서 세분화 작업을 프로그래밍 방식으로 관리할 수 있도록 해주는 여러 끝점을 제공합니다. 이 개요 문서에서는 이러한 각 종단점에 대한 높은 수준의 소개와 세부 정보를 보려면 해당 관련 종단점 안내서에 대한 링크를 제공합니다. 개별 엔드포인트 안내서를 읽기 전에 필요한 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보는 [시작 안내서](./getting-started.md)를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [세그멘테이션 서비스 API 참조](https://www.adobe.io/experience-platform-apis/references/segmentation/)를 참조하십시오.

## 작업 내보내기

내보내기 작업은 대상 세그먼트 구성원을 데이터 세트에 유지하는 데 사용되는 비동기 프로세스입니다. `/export/jobs` 종단점을 사용하여 모든 내보내기 작업을 검색하거나, 새 내보내기 작업을 만들거나, 특정 내보내기 작업의 세부 사항을 검색하거나, 특정 내보내기 작업을 취소할 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [작업 끝점 내보내기 안내서](./export-jobs.md)를 참조하십시오.

## 미리 보기 및 예상

미리 보기는 세그먼트 정의에 대한 페이지 매김 프로필 목록을 제공하여 결과를 예상과 비교할 수 있도록 합니다. `/preview` 종단점을 사용하여 새 미리 보기 작업을 만들거나 특정 미리 보기 작업의 결과를 조회할 수 있습니다.

추정은 예상 대상 크기, 신뢰 구간 및 오류 표준 편차와 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. `/estimate` 종단점을 사용하여 세그먼트 정의의 견적을 볼 수 있습니다.

이러한 종단점 사용에 대한 자세한 내용은 [미리 보기 및 예상 종단점 안내서](./previews-and-estimates.md)를 참조하십시오.

## 스케줄러

예약은 하루에 한 번 배치 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. `/config/schedules` 종단점을 사용하여 일정 목록을 검색하거나, 새 일정을 만들거나, 특정 예약의 세부 정보를 검색하거나, 특정 일정을 업데이트하거나, 특정 일정을 삭제할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [엔드포인트 가이드](./schedules.md)를 참조하십시오.

## 세그먼트 정의

세그먼트 정의는 대상 세그먼트에 포함될 프로필을 정의합니다. `/segment/definitions` 종단점을 사용하여 세그먼트 정의를 관리할 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [세그먼트 정의 종단점 안내서](./segment-definitions.md)를 참조하십시오.

## 세그먼트 작업

세그먼트 작업은 대상 세그먼트를 생성하기 위해 이전에 설정한 세그먼트 정의를 처리합니다. `/segment/jobs` 종단점을 사용하여 세그먼트 작업을 관리할 수 있습니다.

이 종단점 사용에 대한 자세한 내용은 [세그먼트 작업 종단점 안내서](./segment-jobs.md)를 참조하십시오.

## 세그먼트 검색

세그먼트 검색은 다양한 데이터 소스에 포함된 필드를 검색하고 거의 실시간으로 반환하는 데 사용됩니다. 세그먼트 검색 작업을 시작하려면 [검색 끝점 안내서](segment-search.md)를 참조하십시오

## 다음 단계

[!DNL Segmentation Service] API를 시작하려면 다른 엔드포인트 안내서에서 서비스의 다양한 엔드포인트를 호출하는 방법에 대한 자세한 단계를 검토하십시오. [!DNL Platform] UI를 사용하여 세그먼트 작업에 대한 자세한 내용은 [세그먼테이션 사용 안내서](../ui/overview.md)를 참조하십시오.
