---
keywords: Experience Platform;홈;인기 있는 주제;
title: (베타) Adobe Workfront 소스
description: Adobe Workfront은 업무의 전체 라이프사이클을 한 곳에서 관리할 수 있도록 도와주는 마케팅 작업 관리 애플리케이션입니다. Workfront에는 조직의 작업 흐름을 더 잘 이해하고 최적화하는 데 사용할 수 있는 보고 및 분석 도구가 포함되어 있습니다.
exl-id: ea714278-d84d-4929-9a34-81fc5fb70871
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# (베타) Adobe Workfront 소스

>[!NOTE]
>
>Adobe Workfront 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블이 지정된 커넥터 사용에 대한 자세한 정보를 제공합니다.

Adobe Workfront은 업무의 전체 라이프사이클을 한 곳에서 관리할 수 있도록 도와주는 마케팅 작업 관리 애플리케이션입니다. Workfront에는 조직의 작업 흐름을 더 잘 이해하고 최적화하는 데 사용할 수 있는 보고 및 분석 도구가 포함되어 있습니다.

Adobe Experience Platform 소스 카탈로그와 Workfront을 통합하면 Workfront 데이터를 Experience Platform 상태로 전환하고 다음과 같은 사용 사례를 수행할 수 있습니다.

* 작업 기록을 서드파티 데이터와 결합합니다.
* 작업 레코드에 이전 및 시계열 분석을 적용합니다.
* 다음과 같은 타사 비즈니스 인텔리전스 도구를 통해 작업 기록에 액세스 [!DNL PowerBI].
* 표준 SQL을 사용하여 작업 데이터 쿼리

다음 작업 항목과 해당 속성은 Workfront 소스를 통해 Experience Platform에 포함할 수 있습니다.

* 포트폴리오
* 프로그램
* 프로젝트
* 작업
* 운영 작업(문제)
* 사용자

Workfront 소스는 이러한 속성에 대한 모든 새 업데이트를 스트리밍하고 최대 1년의 내역 변경 이벤트를 다시 채웁니다. Workfront 데이터가 플랫폼 데이터 세트에 있으면 다음을 활용할 수 있습니다. [쿼리 서비스](../../../query-service/home.md) 필요에 따라 작업 관련 데이터를 더 자세히 분석하거나 다른 데이터 세트와 연결할 수 있는 기타 도구입니다.

## UI를 사용하여 Workfront을 플랫폼에 연결

Workfront 데이터를 플랫폼으로 가져오는 방법에 대한 자세한 지침은 의 안내서를 참조하십시오. [소스 연결을 생성하여 Workfront 데이터를 플랫폼으로 가져오기](../../tutorials/ui/create/adobe-applications/workfront.md).
