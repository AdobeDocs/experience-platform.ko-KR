---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;API;api;
title: Adobe Experience Platform 세그멘테이션 서비스 개발자 가이드
topic: guide
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] API 개발자 가이드

[!DNL Adobe Experience Platform Segmentation Service] 세그먼트를 만들고 데이터에서 대상 [!DNL Adobe Experience Platform] 을 생성할 수 [!DNL Real-time Customer Profile] 있습니다.

API는 세그먼트 작업을 프로그래밍 방식으로 관리할 수 있도록 해주는 여러 끝점을 제공합니다 [!DNL Segmentation Service] [!DNL Experience Platform]. 이 개요 문서에서는 이러한 각 끝점에 대한 높은 수준의 소개를 제공하며 관련 끝점 안내서에 대한 링크를 통해 자세히 알아보십시오. 개별 종단점 안내선을 읽기 전에 필요한 헤더, 샘플 API 호출 읽기 등에 대한 [자세한 내용은 시작 안내서](./getting-started.md) 를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [세그멘테이션 서비스 API 참조를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml).

## 내보내기 작업

내보내기 작업은 대상 세그먼트 멤버를 데이터 세트로 유지하는 데 사용되는 비동기 프로세스입니다. 끝점을 사용하여 모든 내보내기 작업을 검색하거나, 새 내보내기 작업을 만들거나, 특정 내보내기 작업의 세부 정보를 검색하거나, 특정 내보내기 작업을 취소할 수 있습니다. `/export/jobs`

이 끝점 사용에 대한 자세한 내용은 [내보내기 작업 끝점 안내서를 참조하십시오](./export-jobs.md).

## 미리 보기 및 예측

미리 보기에서는 세그먼트 정의에 대한 페이지로 구분된 프로필 목록을 제공하므로 결과를 예상과 비교할 수 있습니다. 종단점을 사용하여 `/preview` 새 미리 보기 작업을 만들거나 특정 미리 보기 작업의 결과를 조회할 수 있습니다.

예상 대상 크기, 신뢰 구간 및 오류 표준 편차와 같은 세그먼트 정의에 대한 통계 정보를 제공합니다. 종단점을 사용하여 `/estimate` 세그먼트 정의의 예상 값을 볼 수 있습니다.

이러한 끝점 사용에 대한 자세한 내용은 미리 보기 및 [예측 끝점 안내서를 참조하십시오](./previews-and-estimates.md).

## 일정

일정은 하루에 한 번 일괄 처리 세그먼테이션 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. 종단점을 사용하여 예약 목록을 검색하고, 새 일정을 만들거나, 특정 일정에 대한 세부 정보를 검색하고, 특정 일정을 업데이트하거나, 특정 일정을 삭제할 수 있습니다. `/config/schedules`

이 끝점 사용에 대한 자세한 내용은 [예약 끝점 안내서를 참조하십시오](./schedules.md).

## 세그먼트 정의

세그먼트 정의는 대상 세그먼트의 일부가 될 프로파일을 정의합니다. 끝점을 사용하여 세그먼트 정의를 관리할 수 `/segment/definitions` 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 정의 끝점 안내서를 참조하십시오](./segment-definitions.md).

## 세그먼트 작업

세그먼트 작업은 이전에 설정한 세그먼트 정의를 처리하여 대상 세그먼트를 생성합니다. 끝점을 사용하여 세그먼트 `/segment/jobs` 작업을 관리할 수 있습니다.

이 끝점 사용에 대한 자세한 내용은 [세그먼트 작업 끝점 안내서를 참조하십시오](./segment-jobs.md).

## 세그먼트 검색

세그먼트 검색은 다양한 데이터 소스에 포함된 필드를 검색하고 거의 실시간으로 반환하는 데 사용됩니다. 세그먼트 검색 작업을 시작하려면 [검색 끝점 안내서를 참조하십시오](segment-search.md)

## 다음 단계

API를 [!DNL Segmentation Service] 시작하려면 다양한 끝점 안내서에서 서비스의 다양한 끝점에 대한 호출을 수행하는 방법에 대한 자세한 단계를 검토하십시오. UI를 사용하여 세그먼트 작업에 대한 자세한 내용은 [!DNL Platform] 세그멘테이션 사용자 [안내서를 참조하십시오](../ui/overview.md).