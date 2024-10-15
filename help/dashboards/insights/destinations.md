---
title: 대상 통찰력
description: 대상 통찰력을 제공하는 SQL을 살펴보고 이러한 쿼리를 사용하여 사용자 지정 통찰력을 생성하여 Adobe Experience Platform에서 데이터 활성화를 자세히 살펴보십시오.
exl-id: 762a9960-e7a5-4796-80c7-ef745157cc04
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1139'
ht-degree: 3%

---

# 대상 인사이트

데이터 모델 분석을 통해 얻은 인사이트를 통해 Adobe Real-time Customer Data Platform 데이터에 보다 쉽게 액세스하고, 이해할 수 있으며, 의사 결정에 영향을 줄 수 있습니다.

이를 구동하는 SQL에 액세스하여 대상 인사이트를 파악한 다음 고유한 인사이트를 생성하여 Adobe Experience Platform에서 대상 플랫폼으로의 데이터 활성화를 자세히 살펴봅니다. 기존 Real-Time CDP 데이터 모델 SQL을 영감으로 사용하여 원시 데이터를 새로운 실행 가능한 통찰력으로 변환하여 고유한 비즈니스 요구 사항에 맞는 쿼리를 만듭니다.

PLatform UI를 통해 직접 인사이트의 SQL을 조정하는 방법에 대한 자세한 내용은 [SQL 보기 설명서](../view-sql.md)를 참조하십시오.

다음 인사이트는 모두 [대상 대시보드](../guides/destinations.md) 또는 사용자 지정 [사용자 정의 대시보드](../standard-dashboards.md)의 일부로 사용할 수 있습니다. 위젯 라이브러리 및 [사용자 정의 대시보드](../standard-dashboards.md#create-widget)에서 대시보드를 사용자 정의하거나 [새 위젯을 만들고 편집](../customize/custom-widgets.md)하는 방법에 대한 지침은 [사용자 정의 개요](../customize/overview.md)를 참조하세요.

## 활성화된 대상자 {#activated-audiences}

이 통찰력에 의해 답변된 질문:

- 특정 대상으로 필터링된 활성화된 총 대상자 수는 얼마입니까?
- 각 대상별로 활성화된 대상자 수는 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT
  COUNT(segment_id) AS Activated_Audiences_Count
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
  (
    SELECT
      MAX(process_date)
    FROM
      qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE
      process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
  ) BETWEEN start_date AND end_date
  AND destination_id = 1458738325;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [활성화된 대상 위젯 설명서](../guides/destinations.md#activated-audiences)를 참조하십시오.

## 모든 대상에 대해 활성화된 대상자 {#activated-audiences-across-all-destinations}

이 통찰력에 의해 답변된 질문:

- 모든 대상에서 활성화된 대상은 몇 명입니까?
- 활성화된 총 대상자 수는 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT count(segment_id) AS Activated_Audiences_Count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE
    (SELECT MAX(process_date)
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) BETWEEN start_date AND end_date;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [모든 대상 위젯에서 활성화된 대상 설명서](../guides/destinations.md#activated-audiences-across-all-destinations)를 참조하십시오.

## 대상 플랫폼별 활성 대상 {#active-destinations-by-destination-platform}

이 통찰력에 의해 답변된 질문:

- 활성화된 대상이 몇 개입니까?
- 대상 플랫폼별 활성 대상 분류는 무엇입니까?
- 각 대상 플랫폼별로 분류된 활성 대상 수는 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT destination_platform_name AS Destination_Platform_Name,
       COUNT(destination_id) AS Active_Destinations_Count
  FROM qsaccel.profile_agg.adwh_dim_destination a
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination_platform b ON a.destination_platform_id = b.destination_platform_id
  WHERE destination_status='enabled'
  GROUP BY destination_platform_name
  ORDER BY Active_Destinations_Count DESC
  LIMIT 20;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [대상 플랫폼 위젯 설명서별 활성 대상](../guides/destinations.md#active-destinations-by-destination-platform)을 참조하십시오.

## 대상자 크기 트렌드 {#audience-size-trend}

이 통찰력에 의해 답변된 질문:

- 대상에 매핑된 대상자의 예외 항목을 포함하여 시간이 지남에 따라 대상자 크기가 어떻게 변경됩니까?
- 지정된 30일, 90일 및 12개월 동안 대상별 대상 크기의 전반적인 트렌드를 어떻게 찾을 수 있습니까?
- 이메일 마케팅 캠페인과 관련된 스파이크 등 크기에 기여하는 대상자의 주요 특성은 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT d.destination_name,
        d.destination,
        d.destination_id,
        b.segment_name,
        b.segment,
        c.segment_id,
        a.date_key,
        sum(a.count_of_profiles) AS profile_count
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations c ON a.segment_id = c.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination d ON c.destination_id = d.destination_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) f ON a.merge_policy_id = f.merge_policy_id
  WHERE a.date_key >= dateadd(DAY, -30-1, f.last_process_date)
    AND d.destination_id = -1275507046
    AND c.segment_id = -1452100519
  GROUP BY d.destination_name,
          d.destination,
          d.destination_id,
          b.segment_name,
          b.segment,
          c.segment_id,
          a.date_key;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 크기 트렌드 위젯 설명서](../guides/destinations.md#audience-size-trend)를 참조하세요.

## 공통 대상자 {#common-audiences}

이 통찰력에 의해 답변된 질문:

- 두 개의 서로 다른 대상 간에 공통되는 대상은 무엇입니까?
- 서로 다른 두 대상 간의 각 공통 대상에는 몇 개의 프로필이 있습니까?
- 두 대상이 매핑되는 가장 큰 대상은 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT k.destination_name1,
       k.destination_1,
       k.destination_id1,
       k.destination_name2,
       k.destination_2,
       k.destination_id2,
       b.segment_name,
       b.segment,
       b.segment_id,
       sum(a.count_of_profiles) AS profile_count
  FROM
    (SELECT i.destination_name AS destination_name1,
            i.destination AS destination_1,
            i.destination_id AS destination_id1,
            j.destination_name AS destination_name2,
            j.destination AS destination_2,
            j.destination_id AS destination_id2,
            i.segment_id
     FROM
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=1458738325) AS i
     INNER JOIN
       (SELECT b.destination_name,
               b.destination,
               b.destination_id,
               a.segment_id
        FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
        INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id=b.destination_id
        WHERE b.destination_id=-635802802) AS j ON i.segment_id=j.segment_id) AS k
  INNER JOIN qsaccel.profile_agg.adwh_fact_profile_by_segment a ON a.segment_id = k.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON b.segment_id = k.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) c ON a.merge_policy_id = c.merge_policy_id
  WHERE a.date_key = c.last_process_date
  GROUP BY k.destination_name1,
           k.destination_1,
           k.destination_id1,
           k.destination_name2,
           k.destination_2,
           k.destination_id2,
           b.segment_name,
           b.segment,
           b.segment_id
  ORDER BY profile_count DESC
  LIMIT 20;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [일반 대상 위젯 설명서](../guides/destinations.md#common-audiences)를 참조하세요.

## 대상 상태 {#destination-status}

이 통찰력에 의해 답변된 질문:

- 사용할 수 있는 총 대상 수는 얼마입니까?
- 비활성화된 총 대상 수는 얼마입니까?
- 활성화 대상과 비활성화 대상 사이의 비율 분할은 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT COUNT(CASE
                 WHEN destination_status='enabled' THEN 1
             END) AS count_of_active_destinations,
       COUNT(CASE
                 WHEN destination_status='disabled' THEN 1
             END) AS count_of_inactive_destinations
FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 상태 위젯 설명서](../guides/destinations.md#destination-status)를 참조하세요.

## 대상 개수 {#destinations-count}

이 통찰력에 의해 답변된 질문:

- 현재 구성된 대상은 몇 개입니까?
- 시간이 지남에 따라 총 대상 수가 어떻게 변경됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT count(destination_id) AS total_number_of_destinations
  FROM qsaccel.profile_agg.adwh_dim_destination;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [대상 수 위젯 설명서](../guides/destinations.md#destinations-count)를 참조하세요.

## 매핑된 대상자 상태 {#mapped-audience-health}

이 통찰력에 의해 답변된 질문:

- 지난 30일 동안 중요한 변형이 있는 대상에 매핑된 대상자를 선택하십시오.
- 매핑된 대상자의 최신 크기는 얼마입니까? 그리고 지난 달 동안 변경되었습니까?
- 지난 달의 크기 변경 심각도를 기반으로 대상에 매핑된 모든 대상을 나열하려면 어떻게 합니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT destination_name,
        SEGMENT,
        segment_id,
        segment_name,
        avg_profile_count,
        latest_profile_count,
        stddev_profile_count,
        profile_count_z_factor
  FROM
    (SELECT b.destination_name,
            f.segment_id,
            c.segment_name,
            c.segment,
            f.avg_profile_count,
            f.latest_profile_count,
            f.stddev_profile_count,
            CASE
                WHEN stddev_profile_count = 0 THEN 0 ELSE(f.latest_profile_count - f.avg_profile_count)/f.stddev_profile_count
            END AS profile_count_z_factor
    FROM
      (SELECT segment_id,
              avg(profile_count) AS avg_profile_count,
              sum(CASE
                      WHEN last_process_date = date_key THEN profile_count
                      ELSE 0
                  END) AS latest_profile_count,
              stdevp(profile_count) AS stddev_profile_count
        FROM
          (SELECT x.date_key,
                  x.segment_id,
                  d.last_process_date,
                  sum(x.count_of_profiles) AS profile_count
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
          INNER JOIN
            (SELECT MAX(process_date) last_process_date,
                    merge_policy_id
              FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
              WHERE process_name = 'FACT_TABLES_PROCESSING'
                AND process_status = 'SUCCESSFUL'
              GROUP BY merge_policy_id) d ON x.merge_policy_id = d.merge_policy_id
          WHERE x.date_key >= dateadd (DAY, -30, d.last_process_date)
          GROUP BY x.date_key,
                    x.segment_id,
                    d.last_process_date) AS t
        GROUP BY segment_id) AS f
    INNER JOIN qsaccel.profile_agg.adwh_dim_segments c ON f.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations a ON a.segment_id = c.segment_id
    INNER JOIN qsaccel.profile_agg.adwh_dim_destination b ON a.destination_id = b.destination_id
    WHERE b.destination_id = 1458738325) AS m
  WHERE abs(m.profile_count_z_factor) >= 1
  ORDER BY m.latest_profile_count DESC
  LIMIT 20;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [매핑된 대상자 상태 위젯 설명서](../guides/destinations.md#mapped-audience-health)를 참조하십시오.

## 매핑된 대상자 {#mapped-audiences}

이 통찰력에 의해 답변된 질문:

- 몇 개의 대상이 특정 대상에 매핑됩니까?
- 시간이 지남에 따라 매핑된 대상자의 수는 어떻게 변경되었습니까?
- 두 대상을 비교하여 각 대상에 매핑된 대상자 중첩을 볼 수 있는 곳은 어디입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT COUNT(segment_id) AS mapped_audiences_count
FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations
WHERE destination_id = 1458738325;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [매핑된 대상자 위젯 설명서](../guides/destinations.md#mapped-audiences)를 참조하십시오.

<!-- Commented out until the Jan release as the SQL IS MISSING:
## Mapped audiences by identity {#mapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are mapped to a destination?
- What is the count of identities for audiences mapped to a destination?
- Which audiences have the highest count of identities mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Mapped audiences by identity widget documentation](../guides/destinations.md#mapped-audiences-by-identity) for information on the appearance and functionality of this insight.
-->

## 가장 많이 사용하는 대상 {#most-used-destinations}

이 통찰력에 의해 답변된 질문:

- 가장 많이 사용하는 목적지는 어디입니까?
- 얼마나 많은 대상이 각 대상에 매핑되며, 최다 항목에서 최다 항목순으로 정렬됩니까?
- 대상에 대한 대상의 매핑은 한 스냅샷에서 다른 스냅샷으로 어떻게 변경됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_destination.destination_name,
       qsaccel.profile_agg.adwh_dim_destination.destination_id,
       qsaccel.profile_agg.adwh_dim_destination.destination,
       count(DISTINCT qsaccel.profile_agg.adwh_dim_br_segment_destinations.segment_id) segment_count
  FROM qsaccel.profile_agg.adwh_dim_destination
  JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations ON qsaccel.profile_agg.adwh_dim_destination.destination_id = qsaccel.profile_agg.adwh_dim_br_segment_destinations.destination_id
  WHERE qsaccel.profile_agg.adwh_dim_destination.destination_name IS NOT NULL
  GROUP BY qsaccel.profile_agg.adwh_dim_destination.destination_name,
           qsaccel.profile_agg.adwh_dim_destination.destination,
           qsaccel.profile_agg.adwh_dim_destination.destination_id
  ORDER BY segment_count DESC
  LIMIT 20;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [가장 많이 사용된 대상 위젯 설명서](../guides/destinations.md#most-used-destinations)를 참조하세요.

## 최근 활성화된 대상자 {#recently-activated-audiences}

이 통찰력에 의해 답변된 질문:

- 대상이 가장 최근에 활성화된 대상은 무엇입니까?
- 마지막으로 업데이트된 날짜별로 정렬된 모든 대상 목록을 찾으려면 어떻게 해야 합니까?
- 가장 최근의 활성화를 기준으로 두 대상을 비교하려면 어떻게 해야 합니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT
  segment_name,
  segment,
  destination_name,
  a.create_time create_time
FROM
  qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id = b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id = c.destination_id
ORDER BY
  create_time DESC,
  segment
LIMIT
  20;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [최근에 활성화된 대상 위젯 설명서](../guides/destinations.md#recently-activated-audiences)를 참조하십시오.

## 대상별로 최근 활성화된 대상자 {#recently-activated-audiences-by-destination}

이 통찰력에 의해 답변된 질문:

- 특정 대상에 대해 활성화된 대상은 무엇입니까?
- 가장 최근에서 가장 최근까지 특정 대상자에 의해 활성화된 대상자 목록을 어떻게 찾을 수 있습니까?
- 특정 대상에 대해 활성화된 날짜까지 대상자 목록을 찾으려면 어떻게 해야 합니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT c.destination_name,
       c.destination,
       c.destination_id,
       b.segment_name,
       b.segment,
       b.segment_id,
       a.create_time activated
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations a
  INNER JOIN qsaccel.profile_agg.adwh_dim_segments b ON a.segment_id=b.segment_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_destination c ON a.destination_id=c.destination_id
  WHERE c.destination_id=-1275507046
  ORDER BY a.create_time DESC,
           a.segment_id
  LIMIT 20;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [최근 활성화된 대상 위젯별 설명서](../guides/destinations.md#recently-activated-audiences-by-destination)를 참조하십시오.

## 최근에 생성된 대상 {#recently-created-destinations}

이 통찰력에 의해 답변된 질문:

- 가장 최근에 생성된 대상은 무엇입니까?
- 생성된 날짜가 포함된 대상 목록은 어떻게 찾을 수 있습니까?
- 최근에 어떤 새 대상이 생성되었습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT DISTINCT
  destination,
  destination_name,
  create_time
FROM
  qsaccel.profile_agg.adwh_dim_destination
WHERE
  destination_status = 'enabled'
ORDER BY
  create_time DESC
LIMIT
  20;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [최근에 만든 대상 위젯 설명서](../guides/destinations.md#recently-created-destinations)를 참조하십시오.

<!-- Commented out until the Jan release as SQL MISSING FROM WIKI:

## Unmapped audiences by identity {#unmapped-audiences-by-identity}

Questions answered by this insight:

- How do I find a list of audiences that are not mapped to a destination?
- What is the count of identities for audiences that are not mapped to a destination?
- Which audiences have the highest count of identities not mapped to a particular destination?

+++Select to reveal the SQL that generates this insight

```sql
```

+++

See the [Unmapped audiences by identity widget documentation](../guides/destinations.md#unmapped-audiences-by-identity) for information on the appearance and functionality of this insight.

-->

## 다음 단계 {#next-steps}

이제 이 문서를 읽고 대시보드 인사이트를 생성하는 SQL과 이 분석이 해결하는 일반적인 질문을 이해합니다. 이제 이러한 SQL 쿼리를 편집하고 반복하여 고유한 인사이트를 생성할 수 있습니다.

PLatform UI를 통해 직접 인사이트의 SQL을 조정하는 방법에 대한 자세한 내용은 [SQL 보기 설명서](../view-sql.md)를 참조하십시오.

[프로필](./profiles.md), [계정 프로필](./account-profiles.md) 및 [대상](./audiences.md) 대시보드에 대한 인사이트를 생성하는 SQL을 읽고 이해할 수도 있습니다.
