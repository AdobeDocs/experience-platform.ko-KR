---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;데이터 중복 제거;중복 제거;
solution: Experience Platform
title: Query Service의 데이터 중복 제거
type: Tutorial
description: 이 문서에서는 경험 이벤트, 구매 및 지표 등 세 가지 공통 사용 사례를 중복 제거하는 하위 선택 및 전체 샘플 쿼리 예에 대해 설명합니다.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 의 데이터 중복 제거 [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 데이터 중복 제거를 지원합니다. 데이터 중복 제거는 행의 데이터 부분만 중복 정보이므로 계산에서 전체 행을 제거하거나 특정 필드 집합을 무시해야 하는 경우 수행할 수 있습니다.

중복 제거에는 일반적으로 `ROW_NUMBER()` 지정된 시간에 ID(또는 한 쌍의 ID)를 위한 창에서 함수를 실행하고, 중복 감지 횟수를 나타내는 새 필드를 반환합니다. 시간은 [!DNL Experience Data Model] (XDM) `timestamp` 필드.

값이 `ROW_NUMBER()` is `1`는 원래 인스턴스를 참조합니다. 일반적으로 사용할 인스턴스입니다. 중복 제거가 상위 수준에서 수행되는 하위 선택 내에서 수행되는 경우가 많습니다 `SELECT` 합계 카운트를 수행하는 것처럼.

중복 제거 사용 사례는 글로벌 또는 단일 사용자 또는 `identityMap`.

다음 세 가지 일반적인 사용 사례에 대해 중복 제거를 수행하는 방법을 간략하게 설명합니다. 경험 이벤트, 구매 및 지표.

각 예에는 전체 SQL 쿼리뿐만 아니라 범위, 창 키, 중복 제거 방법의 개요 등이 포함됩니다.

## 경험 이벤트 {#experience-events}

중복된 경험 이벤트의 경우 전체 행을 무시할 수 있습니다.

>[!CAUTION]
>
>의 많은 데이터 세트 [!DNL Experience Platform]Adobe Analytics Data Connector에서 생성한 데이터를 포함하여 이미 경험 이벤트 수준 중복 제거가 적용되어 있습니다. 따라서 이 수준의 중복 제거를 다시 적용하는 것은 불필요하고 쿼리의 속도가 느려집니다.
>
>데이터 세트의 소스를 파악하고 Experience-Event 수준의 중복 제거가 이미 적용되었는지 확인하는 것이 중요합니다. 스트리밍되는 모든 데이터 세트(예: Adobe Target의 데이터 세트)에 대해 다음을 수행합니다 **will** 이러한 데이터 소스에는 &quot;최소 한 번&quot; 의미 체계가 있으므로 경험 이벤트 수준 중복 제거를 적용해야 합니다.

**범위:** 글로벌

**창 키:** `id`

### 중복 제거 예

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### 전체 예

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## 구매 {#purchases}

중복 구매가 있는 경우 대부분의 ID를 유지하려고 할 수 있습니다 [!DNL Experience Event] 행을 선택하되, 구매에 연결된 필드(예: `commerce.orders` 지표 참조). 구매에는 구매 ID에 대한 특수 필드( )가 포함되어 있습니다. `commerce.order.purchaseID`.

을 사용하는 것이 좋습니다 `purchaseID` 방문자 범위 내에서 XDM 내에서 구매 ID를 위한 표준 시맨틱 필드이므로 합니다. 쿼리는 전역 범위를 사용하는 것보다 빠르며 여러 방문자 ID에 구매 ID가 중복될 가능성이 낮으므로 중복 구매 데이터를 제거하는 데 방문자 범위를 사용하는 것이 좋습니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id 및 commerce.order.purchaseID

### 중복 제거 예

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

>[!NOTE]
>
>원래 Analytics 데이터에 방문자 ID에 걸쳐 중복 구매 ID가 있는 경우 **5월** 모든 방문자에 대해 구매 ID 중복 계산을 실행해야 합니다. 구매 ID가 없으면 이 메서드를 사용하려면 대신 이벤트 ID를 사용하여 쿼리를 가능한 한 빨리 유지하는 조건을 포함해야 합니다.

### 전체 예

아래 예제는 구매 ID가 없는 경우 조건 절을 사용하여 이벤트 ID를 사용합니다.

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## 지표 {#metrics}

선택적 고유 ID를 사용하는 지표가 있고 해당 ID의 복제본이 표시되면 해당 지표 값을 무시하고 나머지 경험 이벤트를 유지할 수 있습니다.

XDM에서 거의 모든 지표는 `Measure` 선택 사항을 포함하는 데이터 유형 `id` 중복 제거에 사용할 수 있는 필드입니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE]측정값 개체의 .id 및 id

### 중복 제거 예

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### 전체 예

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## 다음 단계

이 문서에서는 데이터 중복 제거의 예를 제공하고 Query Service 내에서 데이터 중복 제거를 수행하는 방법에 대해 간략하게 설명합니다. Query Service를 사용하여 쿼리를 작성할 때의 모범 사례를 더 알아보려면 [쿼리 작성 안내서](../best-practices/writing-queries.md).
