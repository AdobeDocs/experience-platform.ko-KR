---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;API;home;popular topmentation;segmentation Service;api
title: 세그멘테이션 서비스 API 안내서
topic-legacy: guide
description: 개발자는 세그멘테이션 서비스 API를 사용하여 Adobe Experience Platform에서 세그멘테이션 작업을 프로그래밍 방식으로 관리할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 세그멘테이션 서비스 API 안내서

[!DNL Adobe Experience Platform Segmentation Service] 세그먼트를 작성하고 데이터 [!DNL Adobe Experience Platform] 에서 대상을 생성할 수  [!DNL Real-time Customer Profile] 있습니다.

[!DNL Segmentation Service] API는 [!DNL Experience Platform]에서 세그먼테이션 작업을 프로그래밍 방식으로 관리할 수 있는 여러 끝점을 제공합니다. 이 개요 문서에서는 이러한 각 끝점에 대한 높은 수준의 소개를 제공하며 자세한 내용은 해당 끝점에 연결된 안내선에 대한 링크를 제공합니다. 개별 끝점 안내선을 읽기 전에 필요한 머리글, 샘플 API 호출 읽기 등에 대한 자세한 내용은 [시작 안내서](./getting-started.md)를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [세그멘테이션 서비스 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)를 참조하십시오.

## 내보내기 작업

내보내기 작업은 대상 세그먼트 구성원을 데이터 세트로 유지하는 데 사용되는 비동기 프로세스입니다. `/export/jobs` 끝점을 사용하여 모든 내보내기 작업을 검색하거나, 새 내보내기 작업을 만들거나, 특정 내보내기 작업의 세부 정보를 검색하거나, 특정 내보내기 작업을 취소할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [내보내기 작업 끝점 안내서](./export-jobs.md)를 참조하십시오.

## 미리 보기 및 예측

미리 보기에서는 세그먼트 정의에 대한 페이지로 구분된 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다. `/preview` 끝점을 사용하여 새 미리 보기 작업을 만들거나 특정 미리 보기 작업의 결과를 조회할 수 있습니다.

추정은 예상 대상 크기, 신뢰 구간 및 오류 표준 편차 등 세그먼트 정의에 대한 통계 정보를 제공합니다. `/estimate` 끝점을 사용하여 세그먼트 정의의 예상 값을 볼 수 있습니다.

이러한 끝점 사용에 대한 자세한 내용은 [미리 보기 및 예상 끝점 안내서](./previews-and-estimates.md)를 참조하십시오.

## 예약

예약은 하루에 한 번 일괄 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. `/config/schedules` 끝점을 사용하여 일정 목록을 검색하고, 새 일정을 만들고, 특정 일정의 세부 정보를 검색하고, 특정 일정을 업데이트하거나, 특정 일정을 삭제할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [예약 끝점 안내서](./schedules.md)를 참조하십시오.

## 세그먼트 정의

세그먼트 정의는 대상 세그먼트의 일부가 될 프로파일을 정의합니다. `/segment/definitions` 끝점을 사용하여 세그먼트 정의를 관리할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서](./segment-definitions.md)를 참조하십시오.

## 세그먼트 작업

세그먼트 작업은 이전에 설정한 세그먼트 정의를 처리하여 대상 세그먼트를 생성합니다. `/segment/jobs` 끝점을 사용하여 세그먼트 작업을 관리할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서](./segment-jobs.md)를 참조하십시오.

## 세그먼트 검색

세그먼트 검색은 다양한 데이터 소스에 포함된 필드를 검색하고 거의 실시간으로 반환하는 데 사용됩니다. 세그먼트 검색 작업을 시작하려면 [검색 끝점 안내서](segment-search.md)를 참조하십시오.

## 다음 단계

[!DNL Segmentation Service] API를 시작하려면 다른 끝점 안내선을 검토하여 서비스의 다양한 끝점에 대한 호출을 수행하는 방법에 대한 자세한 단계를 검토하십시오. [!DNL Platform] UI를 사용하여 세그먼트 작업에 대한 자세한 내용은 [세그멘테이션 사용자 안내서](../ui/overview.md)를 참조하십시오.
