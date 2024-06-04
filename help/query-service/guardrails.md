---
keywords: Experience Platform;쿼리;쿼리 서비스;문제 해결;보호 기능;지침;제한;
title: 쿼리 서비스 보호
description: 이 문서에서는 쿼리 사용을 최적화하는 데 도움이 되는 쿼리 서비스 데이터의 사용 제한에 대한 정보를 제공합니다.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---

# 쿼리 서비스 보호

가드레일은 Adobe Experience Platform에서 데이터 및 시스템 사용, 성능 최적화 및 오류나 예기치 않은 결과의 회피를 안내하는 임계값입니다.
이 문서에서는 라이선스 권한과 관련하여 데이터를 쿼리할 때 시스템 성능을 최적화하는 데 도움이 되도록 쿼리 서비스 데이터에 대한 기본 사용 제한을 제공합니다.

>[!IMPORTANT]
>
>판매 주문에서 라이선스 권한을 확인하고 해당 권한을 확인하십시오. [제품 설명](https://helpx.adobe.com/legal/product-descriptions.html) 이 보호 기능 페이지 외에 실제 사용 제한에서도 사용할 수 있습니다.

## 전제 조건

이 문서를 계속하기 전에 주요 쿼리 서비스 정의 및 기능을 잘 이해해야 합니다. 아래에 설명되어 있습니다.

* **애드혹 쿼리**: 실행용 `SELECT` 쿼리의 결과가 나타나는 데이터를 탐색, 실험 및 검증하기 위한 쿼리 **저장되지 않음** 데이터 레이크에 있습니다.

* **일괄 쿼리**: 실행용 `INSERT TABLE AS SELECT` 및 `CREATE TABLE AS SELECT` 데이터를 정리, 셰이프, 조작 및 보강하는 쿼리입니다. 이 쿼리의 결과 **저장됨** 데이터 레이크에 있습니다. 이 기능의 소비량을 측정하기 위한 지표는 계산 시간입니다.

* **쿼리 서비스 사용자**: Customer Journey Analytics, Adobe Real-time Customer Data Platform 및/또는 Adobe Journey Optimizer에 대해 현재 라이선스 내에서 제공된 쿼리 서비스 사용자를 Data Distiller과 함께 사용할 수도 있습니다. 쿼리 서비스 사용자는 기능 간에 공유됩니다.

* **애드혹 사용자**: 애드혹 사용자는 애드혹 쿼리를 실행하는 사용자입니다.

* **일괄 처리 사용자**: 일괄 처리 사용자가 일괄 처리 쿼리를 실행하는 사용자입니다.

* **보고 API**: 데이터 가져오기 호출을 위한 API(내부 또는 외부). 확장 보고 데이터 모델은 Real-Time CDP 대시보드 데이터 모델과 같은 Adobe Experience Platform의 기본 보고 데이터 모델에서 파생됩니다.

아래 그림은 쿼리 서비스 기능이 현재 어떻게 패키지화되고 라이선스가 부여되는지 요약한 것입니다.

## 보호 유형

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

| 보호 유형 | 설명 |
|----------|---------|
| **성능 보호(소프트 제한)** | 성능 보호는 사용 사례의 범위와 관련된 사용 제한입니다. 성능 가드레일을 초과하면 성능 저하 및 지연이 발생할 수 있습니다. Adobe은 이러한 성능 저하의 원인이 아닙니다. 성능 가드레일을 지속적으로 초과하는 고객은 성능 저하를 방지하기 위해 추가 용량의 라이센스를 선택할 수 있습니다. |
| **시스템 시행 보호(하드 제한)** | 시스템에서 적용되는 가드레일은 Real-Time CDP UI 또는 API에 의해 적용됩니다. 이는 UI 및 API가 귀하를 차단하거나 오류를 반환하므로 초과할 수 없는 제한입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>이 문서에 설명된 기본 제한은 지속적으로 개선되고 있습니다. 업데이트를 정기적으로 확인하십시오.

## 기본 엔티티 성능 보호

아래 표는 특정 쿼리 패턴을 사용할 때 쿼리 실행에 권장되는 보호 제한 및 설명을 제공합니다.

**애드혹 쿼리**

| 가드레일 | 제한 | 제한 유형 | 설명 |
|---|---|---|---|
| 최대 실행 시간 | 10분 | 시스템 강제 보호 | 임시 SQL 쿼리의 최대 출력 시간을 정의합니다. 결과를 반환하는 시간 제한을 초과하면 오류 코드 오류가 53400. |
| 동시 쿼리 서비스 사용자 | <ul><li>애플리케이션 제품 설명에 지정된 대로.</li><li>+5(추가 Ad Hoc Query 사용자 추가 기능 팩을 구매할 때마다)</li></ul> | 시스템 강제 보호 | 특정 조직에 대해 동시에 세션을 만들 수 있는 사용자 수를 정의합니다. 동시성 한도를 초과하면 사용자는 `Session Limit Reached` 오류. |
| 쿼리 동시 실행 | <ul><li>애플리케이션 제품 설명에 지정된 대로.</li><li>+1(추가 Ad Hoc Query 사용자 추가 기능 SKU 팩을 구매할 때마다)</li></ul> | 시스템 강제 보호 | 특정 조직에 대해 동시에 실행할 수 있는 쿼리 수를 정의합니다. 동시 실행 제한을 초과하면 쿼리가 대기열에 추가됩니다. |
| 클라이언트 커넥터 및 결과 출력 제한 | 클라이언트 커넥터<ul><li>쿼리 UI(100행)</li><li>타사 클라이언트(50,000개)</li><li>[!DNL PostgresSQL] 클라이언트(50,000)</li></ul> | 시스템 강제 보호 | 쿼리 결과는 다음 수단을 통해 받을 수 있습니다.<ul><li>쿼리 서비스 UI</li><li>타사 클라이언트</li><li>[!DNL PostgresSQL] 클라이언트</li></ul>참고: 출력 카운트에 제한을 추가하면 결과가 더 빨리 반환될 수 있습니다. 예를 들어, `LIMIT 5`, `LIMIT 10`등. |
| 다음을 통해 반환된 결과 | 클라이언트 UI | N/A | 사용자가 결과를 사용할 수 있는 방법을 정의합니다. |

{style="table-layout:auto"}

**일괄 쿼리**

| **가드레일** | **제한** | **제한 유형** | **설명** |
|---|---|---|---|
| 최대 실행 시간 | 24시간 | 시스템 강제 보호 | 배치 SQL 쿼리의 최대 실행 시간을 정의합니다.<br>쿼리의 처리 시간은 처리할 데이터의 양과 쿼리 복잡도에 따라 다릅니다. |
| 스케줄링되지 않은 배치에 대한 동시작업 질의 서비스 사용자 | <ul><li>애플리케이션 제품 설명에 지정된 대로.</li><li>+5(추가 Ad Hoc Query 사용자 추가 기능 팩을 구매할 때마다)</li></ul> | 시스템 강제 보호 | 예약되지 않은 배치 쿼리(예: 대화형 모드의 CTAS/ITAS 쿼리)의 경우, 특정 조직에 대해 세션을 동시에 생성할 수 있는 사용자 수를 정의합니다. 동시성 한도를 초과하면 사용자는 `Session Limit Reached` 오류. |
| 예약된 배치에 대한 동시 쿼리 서비스 사용자 | 사용자 제한 없음 | N/A | 예약된 일괄 처리 쿼리는 비동기 작업이므로 사용자 제한이 없습니다. |
| 일괄 데이터 처리를 위한 계산 시간 | 고객의 Adobe Experience Platform 인텔리전스 쿼리 사용자 지정 SKU 판매 주문에 지정된 대로 | 성능 보호 | 이는 일괄 쿼리를 실행하여 데이터를 데이터 레이크에 스캔, 처리 및 다시 작성하는 데 허용되는 연간 계산 시간의 범위를 정의합니다. |
| 쿼리 동시 실행 | 지원됨 | N/A | 예약된 일괄 처리 쿼리는 비동기 작업이므로 동시 쿼리가 지원됩니다. |
| 클라이언트 커넥터 및 결과 출력 제한 | 클라이언트 커넥터<ul><li>쿼리 UI(행에 대한 상한 없음)</li><li>타사 클라이언트(행에 대한 상한 없음)</li><li>[!DNL PostgresSQL] 클라이언트(행에 대한 상한 없음)</li><li>REST API(행에 대한 상한 없음)</li></ul> | 시스템 강제 보호 | 쿼리 결과는 다음 방법을 사용하여 사용할 수 있습니다.<ul><li>파생 데이터 세트로 저장할 수 있음</li><li>기존 파생 데이터 세트에 삽입할 수 있습니다.</li></ul>참고: 쿼리 결과에는 레코드 개수 수에 대한 상한이 없습니다. |
| 다음을 통해 반환된 결과 | 데이터 세트 | N/A | 사용자가 결과를 사용할 수 있는 방법을 정의합니다. |

{style="table-layout:auto"}

## 쿼리 가속 저장소 {#query-accelerated-store}

아래 표는 쿼리 가속 저장소에 대한 권장 보호 제한 사항 및 설명을 제공합니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
|---|---|---|---|
| 쿼리 동시 실행 | 4 | 시스템 강제 보호 | 보고 API를 통해 집계된 데이터에 대한 쿼리(Real-Time CDP 데이터 모델과 같은 데이터 모델을 향상시키는 쿼리 포함)에 효율적으로 실행할 리소스가 있는지 확인하기 위해 보고 API는 각 쿼리에 동시 슬롯을 할당하여 리소스 사용률을 추적합니다. 시스템은 질의를 대기열에 넣고 동시성 슬롯을 사용할 수 있거나 캐시에서 처리될 수 있을 때까지 대기합니다. 지정된 시간에 최대 4개의 동시 쿼리 슬롯을 사용할 수 있습니다.<br>BI 도구를 통해 보고 API에 액세스하고 더 많은 동시성이 필요한 경우 BI 서버가 필요합니다. |

{style="table-layout:auto"}

## 다음 단계

이 문서를 읽은 후에는 사용 가능한 쿼리 패턴을 사용하여 쿼리 실행의 기본 제한을 더 잘 이해할 수 있어야 합니다.

쿼리 서비스에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [쿼리 서비스 API](./api/getting-started.md)
* [쿼리 서비스 UI](./ui/overview.md)

Real-Time CDP 제품 설명 문서의 기타 Experience Platform 서비스 보호, 종단 간 지연 정보 및 라이선스 정보에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Real-Time CDP 보호 기능](/help/rtcdp/guardrails/overview.md)
* [엔드 투 엔드 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) 다양한 Experience Platform 서비스용.
* [Real-time Customer Data Platform (B2C 에디션 - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)