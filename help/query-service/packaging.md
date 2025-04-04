---
title: 쿼리 서비스 패키징
description: 다음 문서에서는 쿼리 서비스에 사용할 수 있는 기능 및 제품의 패키지 구성에 대해 간략히 설명하고 애드혹 쿼리와 배치 쿼리의 차이점을 조명합니다.
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# 쿼리 서비스 패키징

이 문서에서는 쿼리 서비스에서 사용할 수 있는 다양한 유형의 패키징 및 쿼리 실행 기능에 대해 간략히 설명합니다.

Adobe Experience Platform 쿼리 서비스는 실행할 수 있는 쿼리 패턴에 따라 다음 두 가지 기능으로 나눌 수 있습니다.

- **임시 쿼리**&#x200B;는 확인, 유효성 검사, 실험 등을 위해 수집된 데이터 세트를 탐색하는 데 사용되는 SQL 쿼리입니다. 이러한 쿼리는 Experience Platform 데이터 레이크에 데이터를 다시 쓰지 않습니다.
- **일괄 처리 쿼리**&#x200B;는 수집된 데이터 세트의 수집 후 처리를 수행하는 데 사용되는 SQL 쿼리입니다. 이러한 쿼리는 데이터를 정리, 셰이프, 조작 및 강화하고, 그 결과를 Experience Platform 데이터 레이크에 다시 기록합니다. 이러한 쿼리는 배치 작업으로 예약, 관리 및 모니터링할 수 있습니다.

쿼리 서비스 기능은 다음 제품 및 추가 기능과 함께 패키지됩니다.

- **Experience Platform 기반 응용 프로그램**(Adobe Real-Time Customer Data Platform, Adobe Customer Journey Analytics 및 Adobe Journey Optimizer): 애드 혹 쿼리를 실행하기 위한 쿼리 서비스 액세스는 Experience Platform 기반 응용 프로그램의 모든 변형 및 계층에서 처음부터 제공됩니다.
- **[!DNL Data Distiller]**(Adobe Real-Time CDP, Customer Journey Analytics 및 Adobe Journey Optimizer과 함께 구입할 수 있는 추가 기능 패키지): 일괄 처리 쿼리를 실행하기 위한 쿼리 서비스 액세스 권한은 [!DNL Data Distiller]과(와) 함께 제공됩니다.

## 권한 {#entitlements}

다음 표에서는 패키지화 방법을 기반으로 하는 주요 쿼리 서비스 권한에 대해 설명합니다.

| 쿼리 서비스 권한 | Experience Platform 기반 애플리케이션 패키지 | [!DNL Data Distiller]&#x200B;(으)로 패키지됨 |
|---|---|---|
| 쿼리 패턴 지원됨 | 애드혹 쿼리 전용 | 일괄 처리 쿼리 |
| 지원되는 사용 사례 | <ul><li>탐험&#x200B;</li><li>데이터 검색 &#x200B;</li><li>데이터 유효성 검사</li><li>실험</li></ul> | <ul><li>청소</li><li>모양 지정</li><li>조작</li><li>강화</li></ul> |
| 지원되는 의미 체계 | <ul><li>쿼리 선택</li></ul> | <ul><li>CTAS 및 ITAS 쿼리</li></ul> |
| 최대 실행 시간 | 10분 | 24시간 |
| 라이선스 지표 | **사용자 동시성 쿼리**: <ul><li>동시 사용자 1명(Real-Time CDP, Adobe Journey Optimizer&#x200B;)</li><li>동시 사용자 5명(Customer Journey Analytics&#x200B;)</li></ul> **동시성 쿼리**: <ul><li>동시 실행 쿼리 1개(모든 애플리케이션)&#x200B;</li></ul> **추가 임시 쿼리 사용자 팩 추가 기능**&#x200B;을 구입하여 인증된 임시 쿼리 권한을 늘릴 수 있습니다. <ul><li>+팩당 추가 동시 사용자 5명</li><li>+1개의 추가 동시 실행 쿼리/팩</li></ul> | **시간 계산**: <ul><li>변수(애플리케이션 권한에 따라 범위 지정)</li></ul> **시간 계산**&#x200B;은 일괄 처리 쿼리가 실행될 때 쿼리 서비스 엔진에서 데이터를 읽고 처리하고 데이터 레이크에 다시 쓰는 데 걸린 시간을 측정한 것입니다. <br>Data Distiller SKU를 사용하면 추가 사용자 및 쿼리 동시성을 얻을 수 있습니다. 이 동시성은 임시 쿼리를 실행하는 데 사용할 수 있습니다.  Data Distiller SKU에는 <br>이(가) 포함되어 있습니다.<ul><li>+5명의 추가 동시 사용자</li><li>+1개의 추가 동시 실행 쿼리</li></ul> |
| 가속화된 쿼리 및 보고 사용 | 아니요 | 예 - 동시 가속 쿼리를 사용하면 가속 저장소에서 데이터를 읽고 대시보드 내에 표시할 수 있습니다. 가속화된 저장소에 보고 모델 및 데이터 세트를 저장할 수 있는 전용 자격 부여 항목도 제공됩니다. |
| 데이터 레이크 스토리지 용량 | 전체 스토리지 권한은 플랫폼 기반 애플리케이션 라이센스에 따라 달라집니다. 예를 들어 Real-Time CDP, AJO, CJA 등이 있습니다. | 예 - 7일 데이터 만료일 이후에도 Data Distiller 사용 사례에 대한 원시 및 파생 데이터 세트를 유지할 수 있는 추가 스토리지 권한이 제공됩니다.<br>데이터 레이크 저장소 용량은 테라바이트(TB) 단위로 측정되며 구입한 컴퓨팅 시간에 따라 다릅니다. 자세한 내용은 제품 설명을 확인하십시오. |
| 데이터 내보내기 허용 | 총 내보내기 권한은 플랫폼 기반 애플리케이션 라이선스에 따라 다릅니다. 예를 들어 Real-Time CDP, AJO, CJA 등이 있습니다. | 예 - Data Distiller을 사용하여 생성된 파생 데이터 세트를 내보낼 수 있는 추가 내보내기 권한이 제공됩니다.<br>연간 데이터 내보내기 허용량은 테라바이트(TB)로 측정되며 구입한 컴퓨팅 시간에 따라 다릅니다. 자세한 내용은 제품 설명을 확인하십시오. |
| 쿼리 실행 인터페이스 | <ul><li>쿼리 서비스 UI</li><li>타사 클라이언트 UI</li><li>[!DNL PostgresSQL] 클라이언트 UI</li></ul> | <ul><li>쿼리 서비스 UI </li><li>타사 클라이언트 UI</li><li>[!DNL PostgresSQL] 클라이언트 UI</li><li>REST API</li></ul> |
| 다음을 통해 반환된 쿼리 결과 | 클라이언트 UI | 데이터 레이크에 저장된 파생된 데이터 세트 |
| 결과 제한 | <ul><li>쿼리 서비스 UI - 출력 행 수는 [UI 설정으로 구성](./ui/user-guide.md#result-count)할 수 있습니다. 행 수는 50~500개 사이입니다.</li><li>타사 클라이언트 - 50,000개</li><li>[!DNL PostgresSQL] 클라이언트 - 50,000</li></ul> | CTAS 및 ITAS 쿼리는 쿼리 출력이 파생 데이터 세트에 저장되므로 성공 메시지만 생성합니다. |
| 데이터 세트 용량 읽기 | 예 | 예 |
| 데이터 세트 용량 쓰기 | 아니요 | 예 |
| 예약 용량 | 아니요 | 예 |
| 용량 모니터링 | 예 | 예 |
| 쿼리 경고 설정 용량 | 아니요 | 예 |

{style="table-layout:auto"}

## 액세스 제어 {#access-control}

Experience Platform에 대한 액세스 제어는 제품 프로필이 사용 권한 및 샌드박스를 사용자와 연결하는 [Adobe Admin Console](https://adminconsole.adobe.com/)을 통해 관리됩니다. 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 참조하십시오.

제품 프로필 권한 액세스 요청에 대한 자세한 지침은 [제품 프로필에 대한 권한 관리](../access-control/ui/permissions.md) 및 [제품 프로필에 대한 사용자 관리](../access-control/ui/users.md) 문서를 참조하십시오

### 관련 쿼리 서비스 권한 {#query-service-permissions}

쿼리 서비스를 사용하려면 Admin Console 내에서 **[!DNL Manage Queries]** 권한을 사용하도록 설정해야 합니다. 이 권한을 사용하면 임시 및 일괄 쿼리를 실행할 수 있습니다.

다음 표에서는 [!DNL Manage Queries] 권한의 효과를 간략히 설명합니다.

| 사용 권한 | 함수 |
|---|---|
| [!DNL Manage Queries]&#x200B;(데이터 쓰기 권한 없음) | 애드혹 쿼리 실행에 대한 액세스 권한 제공 |
| [!DNL Manage Queries]&#x200B;(데이터 쓰기 권한 있음) | 일괄 처리 쿼리 실행에 대한 액세스 권한 제공 |

{style="table-layout:auto"}

### 관련 SQL Insights 권한 {#sql-insights-permissions}

대시보드 내에 Data Distiller [SQL Insights](./data-distiller/sql-insights/overview.md)를 만들려면 Admin Console 내에서 다음 권한 **을(를) 활성화해야**&#x200B;합니다.

| 사용 권한 | 함수 |
|---|---|
| [!DNL View Custom Dashboard] | 사용자 정의 대시보드에 대한 보기 액세스 권한 제공 |
| [!DNL Manage Custom Dashboard] | 사용자 정의 대시보드에 대한 액세스 관리 제공 |

{style="table-layout:auto"}

## 샌드박스 지원 {#sandbox-support}

샌드박스는 Experience Platform의 단일 인스턴스 내에 있는 가상 파티션입니다. 각 Experience Platform 인스턴스는 여러 프로덕션 및 비프로덕션 샌드박스를 지원하며, 각 샌드박스는 Experience Platform 리소스의 자체 라이브러리를 유지 관리합니다. 비프로덕션 샌드박스를 사용하면 프로덕션 샌드박스에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 수행할 수 있습니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../sandboxes/home.md)를 참조하십시오. 모든 Query Service 권한은 모든 샌드박스에서 공유됩니다.

## 다음 단계

이 문서를 읽으면 Query Service에서 사용할 수 있는 다양한 패키징 유형 및 쿼리 실행 기능을 더 잘 이해할 수 있습니다. 잘 알려진 업계 사용 사례와 같은 쿼리 서비스에 대한 자세한 내용은 [사용 사례 설명서](./use-cases/abandoned-browse.md)를 참조하세요. 자세한 내용은 [쿼리 서비스 개요](./home.md)를 참조하세요.

