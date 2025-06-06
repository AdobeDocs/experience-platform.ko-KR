---
keywords: Experience Platform;홈;자주 찾는 항목;쿼리 서비스;쿼리 서비스;데이터 중복 제거;중복 제거;
solution: Experience Platform
title: 쿼리 서비스의 데이터 중복 제거
type: Tutorial
description: 이 문서에서는 세 가지 일반적인 사용 사례 경험 이벤트, 구매 및 지표를 중복 제거하기 위한 하위 선택 및 전체 샘플 쿼리 예제에 대해 간략히 설명합니다.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# [!DNL Query Service]의 데이터 중복 제거

Adobe Experience Platform [!DNL Query Service]은(는) 데이터 중복 제거를 지원합니다. 데이터 중복 제거는 행에서 데이터의 일부만 중복 정보이므로 계산에서 전체 행을 제거하거나 특정 필드 세트를 무시해야 하는 경우 수행할 수 있습니다.

중복 제거는 일반적으로 순서가 지정된 시간에 따른 ID(또는 ID 쌍)에 대해 창에서 `ROW_NUMBER()` 함수를 사용하는 것과 관련이 있습니다. 이 함수는 중복이 감지된 횟수를 나타내는 새 필드를 반환합니다. 시간은 종종 [!DNL Experience Data Model] (XDM) `timestamp` 필드를 사용하여 표시됩니다.

`ROW_NUMBER()`의 값이 `1`인 경우 원래 인스턴스를 참조합니다. 일반적으로 이 인스턴스를 사용합니다. 이 작업은 집계 수를 수행하는 것처럼 상위 수준 `SELECT`에서 중복 제거가 수행되는 하위 선택 내에서 수행되는 경우가 가장 많습니다.

중복 제거 사용 사례는 전역이거나 `identityMap` 내의 단일 사용자 또는 최종 사용자 ID로 제한될 수 있습니다.

이 문서에서는 경험 이벤트, 구매 및 지표의 세 가지 일반적인 사용 사례에 대해 중복 제거를 수행하는 방법에 대해 간략하게 설명합니다.

각 예에는 범위, 창 키, 중복 제거 방법의 개요 및 전체 SQL 쿼리가 포함됩니다.

## 경험 이벤트 {#experience-events}

중복 경험 이벤트의 경우 전체 행을 무시할 수 있습니다.

>[!CAUTION]
>
>Adobe Analytics 데이터 커넥터에서 생성한 데이터 세트를 포함하여 [!DNL Experience Platform]의 많은 데이터 세트에 이미 경험 이벤트 수준 중복 제거가 적용되어 있습니다. 따라서 이 수준의 중복 제거를 다시 적용할 필요가 없으며 쿼리 속도가 느려집니다.
>
>데이터 세트의 소스를 이해하고 경험 이벤트 수준의 중복 제거가 이미 적용되었는지 아는 것이 중요합니다. 스트리밍되는 데이터 세트(예: Adobe Target의 데이터 세트)의 경우 해당 데이터 소스에는 &quot;최소 한 번 이상&quot; 의미 체계가 있으므로 **will**&#x200B;이(가) 경험 이벤트 수준 중복 제거를 적용해야 합니다.

**범위:** 전역

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

중복 구매가 있는 경우 [!DNL Experience Event] 행 대부분을 유지하지만 구매와 연결된 필드(예: `commerce.orders` 지표)는 무시할 수 있습니다. 구매에는 구매 ID(`commerce.order.purchaseID`)에 대한 특수 필드가 포함되어 있습니다.

XDM 내의 구매 ID에 대한 표준 의미 체계 필드이므로 방문자 범위 내에서 `purchaseID`을(를) 사용하는 것이 좋습니다. 방문자 범위는 쿼리가 글로벌 범위를 사용하는 것보다 빠르며 구매 ID가 여러 방문자 ID에 걸쳐 중복될 가능성이 낮으므로 중복 구매 데이터를 제거하는 데 권장됩니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

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
>원본 Analytics 데이터에 방문자 ID에 대한 중복 구매 ID가 있는 경우 **may**&#x200B;에서 모든 방문자에 대해 구매 ID 중복 계산을 실행해야 합니다. 구매 ID가 없는 경우 이 메서드를 사용하려면 쿼리를 가능한 한 빨리 유지하기 위해 이벤트 ID를 대신 사용하는 조건을 포함해야 합니다.

### 전체 예

아래 예제에서는 구매 ID가 없는 경우 조건 절을 사용하여 이벤트 ID를 사용합니다.

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

선택적 고유 ID를 사용하는 지표가 있고 해당 ID의 복제본이 표시되는 경우, 해당 지표 값을 무시하고 나머지 경험 이벤트를 유지할 수 있습니다.

XDM에서 거의 모든 지표는 중복 제거에 사용할 수 있는 선택적 `id` 필드가 포함된 `Measure` 데이터 형식을 사용합니다.

**범위:** 방문자

**창 키:** identityMap[$NAMESPACE].id 및 측정값 개체의 id

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

이 문서에서는 데이터 중복 제거의 예제를 제공하고 쿼리 서비스 내에서 데이터 중복 제거를 수행하는 방법에 대해 간략히 설명했습니다. 쿼리 서비스를 사용하여 쿼리를 작성하는 모범 사례에 대한 자세한 내용은 [쿼리 작성 안내서](../best-practices/writing-queries.md)를 참조하십시오.
