---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 중복 제거
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 쿼리 서비스의 데이터 중복 제거

Adobe Experience Platform Query Service는 계산에 있는 전체 행을 제거하거나 특정 필드 집합을 무시해야 하는 경우 데이터 중복 제거를 지원합니다. 이는 행의 데이터의 일부만 복제되기 때문입니다. 중복 제거에 대한 일반적인 패턴은 ID 또는 ID 쌍에 대한 창 간 `ROW_NUMBER()` 함수를 주문 시간(XDM(Experience Data Model) `timestamp` 필드 사용)에 따라 사용하여 중복이 감지된 횟수를 나타내는 새 필드를 반환하는 것입니다. 이 값이 `1`인 경우, 원래 인스턴스를 참조하며, 대부분의 경우 사용할 인스턴스로 다른 인스턴스는 무시합니다. 이 작업은 대부분 하위 선택 영역에서 수행됩니다. 하위 선택 영역에서 집계 수를 수행하는 `SELECT` 것과 같이 데이터 중복 제거가 더 높은 수준에서 수행됩니다.

## 사용 사례

데이터 중복 제거에 대한 일부 사용 사례는 날짜 범위에서 전역적이며, 어떤 경우는 `identityMap`데이터 중복 제거의 단일 방문자 또는 최종 사용자 ID로 제한됩니다.

이 문서에서는 세 가지 일반적인 사용 사례 중복을 제거하기 위한 하위 선택 및 전체 샘플 쿼리 예에 대해 설명합니다.
- [ExperienceEvents](#experienceevents)
- [구매](#purchases)
- [지표](#metrics)

### ExperienceEvents {#experienceevents}

ExperienceEvents가 중복되는 경우 전체 행을 무시할 수 있습니다.

>[!CAUTION] Adobe Analytics Data Connector를 비롯한 경험 플랫폼의 많은 DataSet은 이미 ExperienceEvent 수준 중복 제거가 적용되었습니다. 따라서 이러한 수준의 데이터 중복 제거 기능을 다시 적용할 필요가 없으며 쿼리 속도가 느려집니다. DataSets의 소스를 파악하고 ExperienceEvent 수준의 중복 제거가 이미 적용되었는지 아는 것이 중요합니다. 스트리밍되는 모든 DataSet(예: Adobe Target의 데이터 세트)의 경우 ExperienceEvent 수준 중복 제거를 적용해야 합니다. 그 이유는 데이터 소스에 &#39;최소 한 번&#39; 의미 체계가 있기 때문입니다.

**범위:** 글로벌

**창 키:** id

#### 하위 선택

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### 전체 예

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

### 구매 {#purchases}

중복 구매가 있는 경우 대부분의 ExperienceEvent 행을 유지하지만 구매와 연결된 필드(예: `commerce.orders` 지표)는 무시합니다. 구매 시 구매 ID에 대한 특수 필드가 있습니다. 이 필드는 `commerce.order.purchaseID`다음과 같습니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### 하위 선택

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

#### 전체 예

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

### 지표 {#metrics}

선택적 고유 ID를 사용하는 지표가 있고 해당 ID의 복사본이 표시되는 경우 해당 지표 값을 무시하고 나머지 ExperienceEvent를 유지하려고 할 수 있습니다. XDM에서 거의 모든 지표는 데이터 중복 제거에 사용할 수 있는 선택적 필드가 포함된 `Measure` `id` 데이터 유형을 사용합니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id 및 Measure 개체 ID

#### 하위 선택

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

#### 전체 예

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
