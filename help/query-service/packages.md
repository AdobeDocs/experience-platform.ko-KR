---
title: 쿼리 서비스 패키지
description: 다음 문서에서는 Query Service에 사용할 수 있는 기능 및 제품 패키지에 대해 간략하게 설명하고 Ad Hoc 쿼리와 배치 질의 간의 차이점을 설명합니다.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 3%

---

# 쿼리 서비스 패키지

이 문서에서는 Query Service에서 사용할 수 있는 다양한 유형의 패키징 및 쿼리 실행 기능에 대해 설명합니다.

Adobe Experience Platform 쿼리 서비스는 실행할 수 있는 쿼리 패턴을 기반으로 두 가지 기능으로 분할할 수 있습니다.

- **애드혹 쿼리** 확인, 유효성 검사, 실험 등을 위해 수집된 데이터 집합을 탐색하는 데 사용되는 SQL 쿼리입니다. 이러한 쿼리는 Platform 데이터 레이크에 데이터를 다시 쓰지 않습니다.
- **일괄 처리 쿼리** 수집된 데이터 세트의 수집 후 처리를 수행하는 데 사용되는 SQL 쿼리입니다. 이러한 쿼리는 데이터를 정리, 모양, 조작 및 보강하며 그 결과를 Platform 데이터 레이크에 다시 기록합니다. 이러한 쿼리는 일괄 작업으로 예약, 관리 및 모니터링할 수 있습니다.

Query Service 기능은 다음 제품 및 추가 기능과 함께 패키지되어 있습니다.

- **플랫폼 기반 애플리케이션** (Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics 및 Adobe Journey Optimizer): Ad Hoc 쿼리를 실행하기 위한 Query Service 액세스는 플랫폼 기반 응용 프로그램의 모든 변형 및 계층을 통해 처음부터 제공됩니다.
- **[!DNL Data Distiller]** (Adobe Real-Time CDP, Customer Journey Analytics 및 Adobe Journey Optimizer과 함께 구입할 수 있는 추가 기능 패키지): 배치 쿼리를 실행하기 위한 쿼리 서비스 액세스 권한은 [!DNL Data Distiller].

다음 표에서는 패키지 방식에 따라 주요 Query Service 권한에 대해 설명합니다.

| 쿼리 서비스 자격 | 플랫폼 기반 응용 프로그램과 함께 패키지 | 패키지 [!DNL Data Distiller] |
|---|---|---|
| 지원되는 쿼리 패턴 | 애드혹 쿼리 전용 | 일괄 처리 쿼리 |
| 지원되는 사용 사례 | <ul><li>탐색 &#x200B;</li><li>데이터 &#x200B; 검색</li><li>데이터 유효성 검사</li><li>실험</li></ul> | <ul><li>클리닝</li><li>모양</li><li>조작</li><li>강화</li></ul> |
| 지원되는 의미 체계 | <ul><li>쿼리 선택</li></ul> | <ul><li>CTAS 및 ITAS 쿼리</li></ul> |
| 최대 실행 시간 | 10분 | 24시간 |
| 라이선스 지표 | **쿼리 사용자 동시성**: <ul><li>동시 사용자 1명(Real-Time CDP, Adobe Journey Optimizer &#x200B;)</li><li>5명의 동시 사용자(Customer Journey Analytics)&#x200B;</li></ul> **쿼리 동시성**: <ul><li>동시 실행 쿼리 1개(모든 &#x200B; 애플리케이션)</li></ul> **추가 애드혹 쿼리 사용자 팩 추가 기능** 고객의 승인된 ad hoc 쿼리 권한을 늘리기 위해 구입할 수 있습니다. <ul><li>팩당 추가 동시 사용자 5명</li><li>팩당 추가 동시 실행 쿼리 1개</li></ul> | **계산 시간**: <ul><li>변수(고객의 애플리케이션 권한에 따라 범위 지정)</li></ul> **계산 시간** 는 일괄 처리 쿼리가 실행될 때 Query Service 엔진이 데이터를 다시 읽고 처리하고 쓰는 데 걸리는 시간을 측정합니다. |
| 쿼리 실행 인터페이스 | <ul><li>쿼리 서비스 UI</li><li>타사 클라이언트 UI</li><li>[!DNL PostgresSQL] 클라이언트 UI</li></ul> | <ul><li>쿼리 UI </li><li>타사 클라이언트 UI</li><li>[!DNL PostgresSQL] 클라이언트 UI</li><li>REST API</li></ul> |
| 를 통해 반환된 쿼리 결과 | 클라이언트 UI | 데이터 레이크에 저장된 파생 데이터 세트 |
| 결과 제한 | <ul><li>쿼리 UI - 100개 행</li><li>타사 클라이언트 - 50,000</li><li>[!DNL PostgresSQL] 클라이언트 - 50,000</li></ul> | <ul><li>쿼리 UI(행에 대한 상한 제한 없음)</li><li>타사 클라이언트(행에 대한 상한 제한 없음)</li><li>[!DNL PostgresSQL] 클라이언트(행에 대한 상한값 없음)</li><li>REST API(행에 대한 상한값 없음)</li></ul> |
| 데이터 집합 용량 읽기 | 예 | 예 |
| 데이터 집합 용량 쓰기 | 아니요 | 예 |
| 예약 능력 | 아니요 | 예 |
| 용량 모니터링 | 예 | 예 |
| 쿼리 경고 설정 용량 | 아니요 | 예 |

{style=&quot;table-layout:auto&quot;}

## 액세스 제어

Experience Platform에 대한 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com/) 여기서 제품 프로필은 사용자와 권한 및 샌드박스를 연결합니다. 자세한 내용은 [액세스 제어 개요](../access-control/home.md) 추가 정보.

쿼리 서비스를 사용하려면 [!DNL Manage Queries] admin console 내에서 사용 권한을 활성화해야 합니다. 이 권한을 통해 사용자는 임시 및 배치 쿼리를 실행할 수 있습니다. 제품 프로필에 대한 액세스 요청에 대한 자세한 지침 [!DNL Manage Queries] 사용 권한은 [제품 프로필에 대한 권한 관리](../access-control/ui/permissions.md) 및 [제품 프로필의 사용자 관리](../access-control/ui/users.md) 문서.

를 구입한 후 [!DNL Data Distiller] 추가 기능, [!DNL Write Dataset] 권한을 부여해야 합니다. 이 사용 권한 [!DNL Data Distiller] 사용자가 배치 쿼리를 실행할 수 있습니다.

다음 표에서는 [!DNL Manage Queries] 권한:

| 사용 권한 | 함수 |
|---|---|
| [!DNL Manage Queries] (쓰기 데이터 권한 없음) | 임시 쿼리를 실행할 액세스 권한을 제공합니다. |
| [!DNL Manage Queries] (쓰기 데이터 권한 사용) | 배치 질의 실행에 대한 액세스 제공 |

{style=&quot;table-layout:auto&quot;}

## 샌드박스 지원

샌드박스는 단일 Experience Platform 인스턴스 내의 가상 파티션입니다. 각 Platform 인스턴스는 각각 고유한 Platform 리소스 라이브러리를 유지하는 여러 프로덕션 및 비프로덕션 샌드박스를 지원합니다. 비프로덕션 샌드박스를 사용하면 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 만들 수 있습니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md). 모든 쿼리 서비스 권한은 모든 샌드박스에서 공유됩니다

## 다음 단계

이 문서를 읽은 후에는 Query Service에서 사용할 수 있는 다양한 패키지 유형 및 쿼리 실행 기능을 더 잘 이해할 수 있어야 합니다. 알려진 업계 사용 사례와 같은 Query Service에 대한 자세한 내용은 [사용 사례 설명서](./use-cases/abandoned-browse.md). 일반적인 정보를 보려면 [쿼리 서비스 개요](./home.md).
