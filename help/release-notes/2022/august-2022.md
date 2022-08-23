---
title: Adobe Experience Platform 릴리스 노트 - 2022년 8월
description: Adobe Experience Platform에 대한 2022년 8월 릴리스 노트입니다.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 14%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 8월 24일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 준비](#data-prep)
- [소스](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 경고가 있는 레코드 수집 지원 | 이제 데이터 준비에서 경고(중요하지 않은 오류)를 필드에 현지화하고 나머지 행을 수집할 수 있습니다. 이제 모든 매퍼 변환 오류는 경고 및 부분적으로 수집된 행으로 보고되며, 경고 메시지가 표시됩니다.  경고 및 진단 세부 정보가 있는 레코드에서도 모니터링이 지원됩니다. 경고가 있는 레코드의 일부 섭취는 현재 스트리밍 데이터만 사용할 수 있습니다. 다음 문서를 검토하십시오. [경고가 있는 레코드 수집](../../sources/tutorials/ui/monitor-streaming.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

에 대해 자세히 알아보려면 [!DNL Data Prep]를 참조하고 [[!DNL Data Prep] 개요](../../data-prep/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 소스에 대한 지역 간 지원 | 이제 모든 지역(미국, 영국 또는 싱가포르)에서 보고서 세트를 수집할 수 있습니다. 보고서 세트는 소스 연결을 만들고 있는 Experience Platform 샌드박스 인스턴스와 동일한 조직에 매핑되어야 합니다. 자세한 내용은 [UI에서 Adobe Analytics 소스 연결 만들기](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
