---
keywords: Experience Platform;홈;인기 있는 주제
title: Adobe Workfront 소스
description: Adobe Workfront은 한 곳에서 전체 작업 수명 주기를 관리하는 데 도움이 되는 마케팅 작업 관리 애플리케이션입니다. Workfront에는 조직에서 작업 흐름을 더 잘 이해하고 최적화하는 데 사용할 수 있는 보고 및 분석 도구가 포함되어 있습니다.
source-git-commit: 99741a3be4d50d1a812e945483c9ed1577a0a999
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 1%

---

# Adobe Workfront 소스

Adobe Workfront은 한 곳에서 전체 작업 수명 주기를 관리하는 데 도움이 되는 마케팅 작업 관리 애플리케이션입니다. Workfront에는 조직에서 작업 흐름을 더 잘 이해하고 최적화하는 데 사용할 수 있는 보고 및 분석 도구가 포함되어 있습니다.

Adobe Experience Platform 소스 카탈로그와 Workfront 통합을 통해 Workfront 데이터를 Experience Platform으로 가져오고 다음과 같은 사용 사례를 수행할 수 있습니다.

* 작업 레코드를 타사 데이터와 결합합니다.
* 작업 레코드에 내역 및 시계열 분석을 적용합니다.
* 다음과 같은 타사 비즈니스 인텔리전스 도구를 통해 작업 기록에 액세스 [!DNL PowerBI].
* 표준 SQL을 사용하여 작업 데이터를 쿼리합니다.

다음 작업 항목 및 해당 속성은 Workfront 소스를 통해 Experience Platform에 포함할 수 있습니다.

* 포트폴리오
* 프로그램
* 프로젝트
* 작업
* 작업(문제)
* 사용자

Workfront 소스는 이러한 속성에 대한 모든 새로운 업데이트를 스트리밍하고 최대 1년의 내역 변경 이벤트 를 다시 채웁니다. Workfront 데이터가 Platform 데이터 세트에 업로드되면 [쿼리 서비스](../../../query-service/home.md) 및 기타 도구를 사용하여 작업 관련 데이터를 필요에 따라 다른 데이터 세트와 추가로 분석하거나 결합할 수 있습니다.

## UI를 사용하여 Platform에 Workfront 연결

Workfront 데이터를 Platform으로 가져오는 방법에 대한 자세한 지침은 [Workfront 데이터를 플랫폼으로 가져오기 위한 소스 연결 만들기](../../tutorials/ui/create/adobe-applications/workfront.md).