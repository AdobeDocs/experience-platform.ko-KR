---
title: Privacy Service API 안내서
description: Privacy Service API를 사용하여 지원되는 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 작업을 프로그래밍 방식으로 관리하는 방법을 알아봅니다.
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# [!DNL Privacy Service] API 안내서

Privacy Service API는 조직의 개인 정보 작업을 프로그래밍 방식으로 관리할 수 있도록 해주는 몇 가지 엔드포인트를 제공합니다. 이러한 엔드포인트는 아래에 요약되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 방문하여 을 참조하십시오. [시작 안내서](./getting-started.md) 필요한 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 제공합니다.

>[!NOTE]
>
>이 안내서에서는 [!DNL Privacy Service] API. UI 사용 방법에 대한 자세한 내용은 [Privacy Service UI 개요](../ui/overview.md).

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [Privacy Service API 참조](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## 개인 정보 작업

Privacy Service이 주체의 개인 데이터에 액세스하거나 삭제하라는 요청을 받으면 시스템이 해당 요청을 수행하기 위해 개인 정보 보호 작업을 만듭니다. 각 개인 정보 작업에는 데이터 주체와 관련된 ID 정보, 작업이 적용되는 Adobe Experience Cloud 제품에 대한 메타데이터 및 작업 처리 상태가 포함되어 있습니다.

다음 `/jobs` 엔드포인트를 사용하면 조직에 대한 개인 정보 작업을 만들고 검색할 수 있습니다. 이 종단점을 사용하는 방법에 대해 알아보려면 [개인 정보 보호 작업 엔드포인트 안내서](./privacy-jobs.md).

## 동의

특정 규정에서는 개인 데이터를 수집하기 전에 명시적인 고객 동의를 필요로 합니다. 다음 `/consent` 종단점을 사용하면 고객 동의 요청을 처리하고 개인 정보 보호 워크플로우에 통합할 수 있습니다. 자세한 내용은 [동의 끝점 안내서](./consent.md) 추가 정보

## 다음 단계

스키마 레지스트리 API를 사용하여 호출을 시작하려면 다음을 참조하십시오. [시작 안내서](./getting-started.md) 그런 다음 엔드포인트 가이드 중 하나를 선택하여 특정 엔드포인트를 사용하는 방법을 알아봅니다.
