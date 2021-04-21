---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;데이터 중복 제거;데이터 중복 제거;home;popular topics;query service;data deduplication;deduplication
solution: Experience Platform
title: 쿼리 서비스의 데이터 중복 제거
topic-legacy: queries
type: Tutorial
description: 이 문서에서는 경험 이벤트, 구매 및 지표의 세 가지 일반적인 사용 사례를 중복 제거하는 하위 선택 및 전체 샘플 쿼리 예에 대해 설명합니다.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# [!DNL Query Service]의 데이터 중복 제거

Adobe Experience Platform [!DNL Query Service]은(는) 데이터 중복 제거를 지원합니다. 데이터 중복 제거는 계산에 있는 전체 행을 제거하거나 특정 필드 집합을 무시해야 하는 경우에 수행할 수 있습니다. 행에 있는 데이터의 일부만이 중복된 정보입니다.

일반적으로 데이터 중복 제거는 순서가 지정된 시간에 대해 윈도우에 있는 `ROW_NUMBER()` 함수를 사용하여 ID(또는 ID 쌍)를 표시하는 것으로, 중복이 감지된 횟수를 나타내는 새 필드를 반환합니다. 시간은 종종 [!DNL Experience Data Model](XDM) `timestamp` 필드를 사용하여 표현됩니다.

`ROW_NUMBER()` 값이 `1`이면 원래 인스턴스를 참조합니다. 일반적으로 사용할 인스턴스입니다. 이 작업은 대부분 하위 선택 영역 내에서 수행됩니다. 하위 선택 영역에서 데이터 중복 제거가 집계 수를 수행하는 것처럼 상위 수준 `SELECT`에서 수행됩니다.

데이터 중복 제거 사용 사례는 전체 또는 단일 사용자 또는 최종 사용자 ID로 제한될 수 있습니다. `identityMap`

이 문서에서는 다음과 같은 세 가지 일반적인 사용 사례를 위해 중복 제거를 수행하는 방법에 대해 설명합니다.경험 이벤트, 구매 및 지표.

각 예에는 전체 SQL 쿼리뿐만 아니라 범위, 창 키, 중복 제거 방법의 개요 등이 포함되어 있습니다.

## 경험 이벤트 {#experience-events}

경험 이벤트가 중복되는 경우 전체 행을 무시하려고 할 수 있습니다.

>[!CAUTION]
>
>Adobe Analytics Data Connector에서 생성된 데이터 세트를 포함하여 [!DNL Experience Platform]의 많은 데이터 세트에 이미 경험 이벤트 수준 데이터 중복 제거가 적용되어 있습니다. 따라서 이러한 수준의 중복 제거 기능을 다시 적용할 필요가 없으며 쿼리를 느리게 할 수 있습니다.
>
>데이터 세트의 소스를 파악하고 경험 이벤트 수준의 데이터 중복 제거가 이미 적용되었는지 아는 것이 중요합니다. 스트리밍되는 모든 데이터 세트(예: Adobe Target의 데이터 세트)의 경우, 이러한 데이터 소스에는 &quot;최소 한 번&quot; 데이터 소스가 있으므로 **는 경험-이벤트 수준 데이터 중복 제거를 적용해야 합니다.**

**범위:** 전역

**창 키:** `id`

### 데이터 중복 제거 예

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

중복 구매가 있는 경우, 경험 이벤트 행의 대부분을 유지하려고 하지만 구매에 연결된 필드(예: `commerce.orders` 지표)는 무시합니다. 구매에는 구매 ID에 대한 특수 필드가 포함되어 있습니다(예: `commerce.order.purchaseID`).

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### 데이터 중복 제거 예

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

### 전체 예

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

선택적 고유 ID를 사용하는 지표가 있고 해당 ID의 복사본이 표시되는 경우 해당 지표 값을 무시하고 나머지 경험 이벤트를 유지하려고 할 수 있습니다.

XDM에서 데이터 중복 제거에 사용할 수 있는 선택적 `id` 필드가 포함된 `Measure` 데이터 유형을 거의 모든 지표가 사용합니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id 및 Measure 개체 ID

### 데이터 중복 제거 예

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

이 문서에서는 쿼리 서비스 내에서 데이터 중복 제거를 수행하는 방법 및 데이터 중복 제거의 예를 설명합니다. 쿼리 서비스를 사용하여 쿼리를 작성할 때의 모범 사례를 보려면 [쿼리 작성 안내서](./writing-queries.md)를 참조하십시오.
