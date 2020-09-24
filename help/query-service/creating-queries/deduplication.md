---
keywords: Experience Platform;home;popular topics;query service;Query service;data deduplication;deduplication;
solution: Experience Platform
title: 데이터 중복 제거
topic: queries
type: Tutorial
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---


# 데이터 중복 제거 [!DNL Query Service]

Adobe Experience Platform은 데이터 중복 제거 기능을 [!DNL Query Service] 지원합니다. 단, 데이터 중 일부만 중복되기 때문에 계산에서 전체 행을 제거하거나 특정 필드 집합을 무시할 수 있습니다. 중복 제거에 대한 일반적인 패턴은 ID 또는 ID 쌍에 대한 창 간 `ROW_NUMBER()` 함수를 주문된 시간(XDM [!DNL Experience Data Model] `timestamp` 필드)에 걸쳐 사용하여 중복이 감지된 횟수를 나타내는 새 필드를 반환하는 것입니다. 이 값 `1`이 원래 인스턴스를 참조하고, 대부분의 경우 사용할 인스턴스로, 다른 모든 인스턴스를 무시합니다. 이러한 작업은 대부분 하위 선택 영역에서 수행되며, 집계 수와 같이 더 높은 수준의 데이터 중복 제거 작업을 수행합니다. `SELECT`

## 사용 사례

데이터 중복 제거에 대한 일부 사용 사례는 날짜 범위 전체에 적용되며, 일부는 데이터 중복 제거의 단일 방문자 또는 최종 사용자 ID로 제한됩니다 `identityMap`.

이 문서에서는 세 가지 일반적인 사용 사례 중복을 제거하기 위한 하위 선택 및 전체 샘플 쿼리 예에 대해 간략하게 설명합니다.
- [ExperienceEvents](#experienceevents)
- [구매](#purchases)
- [지표](#metrics)

### ExperienceEvents {#experienceevents}

ExperienceEvents가 중복되는 경우 전체 행을 무시할 수 있습니다.

>[!CAUTION]
>
>Adobe Analytics 데이터 커넥터에서 생성된 데이터 세트를 [!DNL Experience Platform]포함하여 많은 DataSets가 이미 ExperienceEvent 수준 중복 제거가 적용되었습니다. 따라서 이러한 수준의 데이터 중복 제거 기능을 다시 적용하는 것은 불필요한 작업이므로 질의 속도가 느려질 수 있습니다. DataSets의 소스를 파악하고 ExperienceEvent 수준의 데이터 중복 제거가 이미 적용되었는지 파악하는 것이 중요합니다. 스트리밍되는 모든 DataSets(예: Adobe Target의 데이터 세트)의 경우, 해당 데이터 소스는 &#39;최소 한 번&#39; 의미 체계를 가지므로 ExperienceEvent 수준의 데이터 중복 제거를 적용해야 합니다.

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

중복 구매가 있는 경우 대부분의 ExperienceEvent 행을 유지하지만 구매와 연결된 필드(예: 지표)는 `commerce.orders` 무시합니다. 구매 시 구매 ID에 대한 특수 필드가 있습니다. 이 필드 `commerce.order.purchaseID`는

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

선택적 고유 ID를 사용하는 지표가 있고 해당 ID의 복제본이 나타나면 해당 지표 값을 무시하고 나머지 ExperienceEvent를 유지하려는 경우가 있습니다. XDM에서 거의 모든 지표는 데이터 중복 제거에 사용할 수 있는 선택적 필드가 포함된 데이터 유형을 `Measure` `id` 사용합니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id 및 Measure 개체 id

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
