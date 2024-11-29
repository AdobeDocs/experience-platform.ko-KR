---
title: Audiences 인사이트
description: 대상 인사이트를 제공하는 SQL을 살펴보고 이러한 쿼리를 사용하여 사용자 지정 인사이트를 생성하면 Adobe Experience Platform에서 대상 데이터를 추가로 탐색할 수 있습니다.
exl-id: 99624234-c4e1-44bb-9567-505bc0c4723e
source-git-commit: cce576c00823a0c02e4b639f0888a466a5af6a0c
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 3%

---

# Audiences 인사이트

데이터 모델 분석을 통해 얻은 인사이트를 통해 Adobe Real-Time CDP 데이터에 보다 쉽게 액세스하고, 이해할 수 있으며, 의사 결정에 영향을 줄 수 있습니다.

대상자를 지원하는 SQL에 액세스하여 대상자 인사이트를 파악한 다음 고유한 인사이트를 생성하여 대상자를 구성하는 ID 및 프로필을 추가로 살펴봅니다. 기존 Real-Time CDP 데이터 모델 SQL을 영감으로 사용하여 원시 데이터를 새로운 실행 가능한 통찰력으로 변환하여 고유한 비즈니스 요구 사항에 맞는 쿼리를 만듭니다.

PLatform UI를 통해 직접 인사이트의 SQL을 조정하는 방법에 대한 자세한 내용은 [SQL 보기 설명서](../view-sql.md)를 참조하십시오.

다음 인사이트는 모두 [대상 대시보드](../guides/audiences.md) 또는 사용자 지정 [사용자 정의 대시보드](../standard-dashboards.md)의 일부로 사용할 수 있습니다. 위젯 라이브러리 및 [사용자 정의 대시보드](../standard-dashboards.md#create-widget)에서 대시보드를 사용자 정의하거나 [새 위젯을 만들고 편집](../customize/custom-widgets.md)하는 방법에 대한 지침은 [사용자 정의 개요](../customize/overview.md)를 참조하세요.

다음 인사이트는 모두 [대상 대시보드](../guides/audiences.md) 또는 사용자 지정 대시보드의 일부로 사용할 수 있습니다.

## 대상자 오버랩 보고서 {#audience-overlap-report}

이 통찰력에 의해 답변된 질문:

- 필터링된 특정 대상의 상위 50개 겹치는 대상은 무엇입니까?
- 필터링된 특정 대상자 중 가장 겹치지 않는 50명의 대상자는 무엇입니까?
- 필터링된 다른 대상에 대해 겹치는 패턴이 어떻게 변경됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT source_segment_name,
        source_segment_id,
        overlap_segment_name,
        overlap_segment_id,
        max(source_segment_audience_count) source_segment_audience_count,
        max(overlap_segment_audience_count) overlap_segment_audience_count,
        max(overlap_audience_count) overlap_audience_count,
        CASE
            WHEN (max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) > 0 THEN (cast(max(overlap_audience_count) AS DECIMAL(18, 2)) / cast((max(source_segment_audience_count) + max(overlap_segment_audience_count) - max(overlap_audience_count)) AS DECIMAL(18, 2))) * 100::DECIMAL(9, 2)
            ELSE 100.00
        END overlapping_percentage
  FROM
    (SELECT adwh_fact_profile_overlap_of_segments.Segment1 source_segment_id,
            adwh_fact_profile_overlap_of_segments.Segment2 overlap_segment_id,
            Sum(count_of_overlap) overlap_audience_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment2 ,
              qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.Segment1) a
  INNER JOIN
    (SELECT sum(count_of_profiles) source_segment_audience_count,
            adwh_dim_segments.segment_name source_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment1
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_dim_segments.segment_id = qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) b ON a.source_segment_id = b.segment1
  INNER JOIN
    (SELECT sum(count_of_profiles) overlap_segment_audience_count,
            adwh_dim_segments.segment_name overlap_segment_name,
            adwh_fact_profile_by_segment_trendlines.merge_policy_id,
            adwh_fact_profile_by_segment_trendlines.segment_Id segment2
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON adwh_dim_segments.segment_id = adwh_fact_profile_by_segment_trendlines.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    GROUP BY qsaccel.profile_agg.adwh_dim_segments.segment_name,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id,
              qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id) c ON a.overlap_segment_id = c.segment2
  GROUP BY source_segment_name,
          source_segment_id,
          overlap_segment_name,
          overlap_segment_id
  ORDER BY overlapping_percentage DESC
  LIMIT 5;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 중복 보고서 위젯 설명서](../guides/audiences.md#audience-overlap-report)를 참조하십시오.

## 대상자 오버랩 {#audience-overlap}

이 통찰력에 의해 답변된 질문:

- 두 대상에 공통되는 프로필은 무엇입니까?
- 중복은 참여 또는 전환율에 어떤 영향을 줍니까?
- 겹치는 세그먼트에 맞게 마케팅 전략을 어떻게 조정할 수 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            sum(count_of_overlap)Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1870062812
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=2080256533)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=2080256533
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1870062812))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1870062812
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1133248113
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 2080256533 ) a;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 중복 위젯 설명서](../guides/audiences.md#audience-overlap)를 참조하십시오.

## 대상자 크기 변경 트렌드 {#audience-size-change-trend}

이 통찰력에 의해 답변된 질문:

- 지난 30일, 90일 또는 12개월 내에 대상자 크기가 상당히 증가하거나 감소했습니까?
- 특정 기간 동안 대상 크기는 어떻게 변경됩니까?
- 지난 12개월 동안 탐지된 급감이나 급감의 이상현상이나 반복되는 패턴이 있었습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT date_key,
      Profiles_added
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                                ORDER BY date_key))Profiles_added
    FROM
      (SELECT date_key,
              sum(x.count_of_profiles)count_of_profiles,
              row_number() OVER (
                                  ORDER BY date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
        INNER JOIN
          (SELECT MAX(process_date) last_process_date,
                  merge_policy_id
          FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
          WHERE process_name = 'FACT_TABLES_PROCESSING'
            AND process_status = 'SUCCESSFUL'
          GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
        WHERE segment_id = 1333234510
          AND x.date_key >= dateadd(DAY, -30 -1, y.last_process_date)
        GROUP BY x.date_key) a)b
  WHERE rn_num > 1;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 크기 변경 트렌드 위젯 설명서](../guides/audiences.md#audience-size-change-trend)를 참조하세요.

## ID별 대상자 크기 트렌드 {#audience-size-trend-by-identity}

이 통찰력에 의해 답변된 질문:

- 내 대상이 지속적으로 성장하고, 안정되고, 변동을 경험하고 있습니까?
- 시간이 지남에 따라 대상자 증가율이 급증하거나 감소하는 특정 정체성이 있습니까?
- 시간이 지남에 따라 나의 정체성 성장에는 어떤 이상이 있는가?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT sum(count_of_profiles) AS identities,
        date_key
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  INNER JOIN qsaccel.profile_agg.adwh_dim_namespaces z ON x.namespace_id = z.namespace_id
  AND x.merge_policy_id = z.merge_policy_id
  WHERE x.date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
    AND z.namespace_description = 'crmid'
  GROUP BY date_key;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [ID 위젯 설명서별 대상 크기 트렌드](../guides/audiences.md#audience-size-trend-by-identity)를 참조하십시오.

## 대상자 크기 트렌드 {#audience-size-trend}

이 통찰력에 의해 답변된 질문:

- 예외 항목을 포함하여 시간이 지남에 따라 대상 크기가 어떻게 변경됩니까?
- 30일, 90일 및 12개월 동안 대상 크기의 전반적인 트렌드를 어떻게 찾을 수 있습니까?
- 규모에 기여하는 대상의 주요 특성은 무엇입니까? 예를 들어 이메일 마케팅 캠페인으로 인한 스파이크가 있습니다.

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT date_key,
        sum(count_of_profiles) AS audience_size
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -30, y.last_process_date)
    AND x.segment_id = 1333234510
  GROUP BY date_key,
          segment_id;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 크기 트렌드 위젯 설명서](../guides/audiences.md#audience-size-trend)를 참조하세요.

## 대상자 크기 {#audience-size}

이 통찰력에 의해 답변된 질문:

- 현재 대상자 총 규모는 얼마입니까?
- 현재 대상 크기는 이전 기간 또는 특정 대상과 어떻게 비교됩니까?
- 최근 마케팅 캠페인이 대상자 크기에 미치는 영향은 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT
  sum(
    qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles
  ) count_of_profiles
FROM
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
WHERE
  qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = -1323307941
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 1914917902
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-12';
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [대상 크기 위젯 설명서](../guides/audiences.md#audience-size)를 참조하세요.

## 고객 AI 점수 분포 {#customer-ai-distribution-of-scores}

이 통찰력에 의해 답변된 질문:

- 선택한 대상자로 필터링된 내 고객 AI 모델의 각 버킷에 대한 채점 분포는 무엇입니까?
- 특정 대상에 대한 높음, 중간, 낮음의 점수 분포는 얼마입니까?
- 관심 있는 다양한 대상자에 의한 채점 분포의 분류는 무엇인가?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT b.model_name,
      b.model_type,
      c.segment_name,
      c.segment_id,
      CASE
        WHEN score >= 0
          AND score < 25 THEN 'LOW'
        WHEN score >= 25
          AND score < 75 THEN 'MEDIUM'
        WHEN score >= 75
          AND score <= 100 THEN 'HIGH'
        END bucket_name,
      CASE
        WHEN score >= 0
          AND score < 5 THEN '02.50'
        WHEN score >= 5
          AND score < 10 THEN '07.50'
        WHEN score >= 10
          AND score < 15 THEN '12.50'
        WHEN score >= 15
          AND score < 20 THEN '17.50'
        WHEN score >= 20
          AND score < 25 THEN '22.50'
        WHEN score >= 25
          AND score < 30 THEN '27.50'
        WHEN score >= 30
          AND score < 35 THEN '32.50'
        WHEN score >= 35
          AND score < 40 THEN '37.50'
        WHEN score >= 40
          AND score < 45 THEN '42.50'
        WHEN score >= 45
          AND score < 50 THEN '47.50'
        WHEN score >= 50
          AND score < 55 THEN '52.50'
        WHEN score >= 55
          AND score < 60 THEN '57.50'
        WHEN score >= 60
          AND score < 65 THEN '62.50'
        WHEN score >= 65
          AND score < 70 THEN '67.50'
        WHEN score >= 70
          AND score < 75 THEN '72.50'
        WHEN score >= 75
          AND score < 80 THEN '77.50'
        WHEN score >= 80
          AND score < 85 THEN '82.50'
        WHEN score >= 85
          AND score < 90 THEN '87.50'
        WHEN score >= 90
          AND score < 95 THEN '92.50'
        WHEN score >= 95
          AND score <= 100 THEN '97.50'
        END score_bins,
      Sum(CASE
            WHEN score >= 0
              AND score < 25 THEN count_of_profiles
            WHEN score >= 25
              AND score < 75 THEN count_of_profiles
            WHEN score >= 75
              AND score <= 100 THEN count_of_profiles
        END) count_of_profiles
   FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
          JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
     AND a.model_id = b.model_id
          JOIN qsaccel.profile_agg.adwh_dim_segments c ON a.segment_id = c.segment_id
   WHERE a.merge_policy_id = 1133248113
     AND a.model_id = 1829081696
     AND a.segment_id = 1870062812
     AND score_date =
         (SELECT MAX(score_date)
          FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
          WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
             b.model_type,
             c.segment_name,
             c.segment_id,
             CASE
               WHEN score >= 0
                 AND score < 25 THEN 'LOW'
               WHEN score >= 25
                 AND score < 75 THEN 'MEDIUM'
               WHEN score >= 75
                 AND score <= 100 THEN 'HIGH'
               END,
             CASE
               WHEN score >= 0
                 AND score < 5 THEN '02.50'
               WHEN score >= 5
                 AND score < 10 THEN '07.50'
               WHEN score >= 10
                 AND score < 15 THEN '12.50'
               WHEN score >= 15
                 AND score < 20 THEN '17.50'
               WHEN score >= 20
                 AND score < 25 THEN '22.50'
               WHEN score >= 25
                 AND score < 30 THEN '27.50'
               WHEN score >= 30
                 AND score < 35 THEN '32.50'
               WHEN score >= 35
                 AND score < 40 THEN '37.50'
               WHEN score >= 40
                 AND score < 45 THEN '42.50'
               WHEN score >= 45
                 AND score < 50 THEN '47.50'
               WHEN score >= 50
                 AND score < 55 THEN '52.50'
               WHEN score >= 55
                 AND score < 60 THEN '57.50'
               WHEN score >= 60
                 AND score < 65 THEN '62.50'
               WHEN score >= 65
                 AND score < 70 THEN '67.50'
               WHEN score >= 70
                 AND score < 75 THEN '72.50'
               WHEN score >= 75
                 AND score < 80 THEN '77.50'
               WHEN score >= 80
                 AND score < 85 THEN '82.50'
               WHEN score >= 85
                 AND score < 90 THEN '87.50'
               WHEN score >= 90
                 AND score < 95 THEN '92.50'
               WHEN score >= 95
                 AND score <= 100 THEN '97.50'
               END;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [점수 위젯 설명서의 고객 AI 배포](../guides/audiences.md#customer-ai-distribution-of-scores)를 참조하십시오.

## 고객 AI 점수 요약 {#customer-ai-scoring-summary}

이 통찰력에 의해 답변된 질문:

- 특정 대상에 대한 각 고객 AI 모델의 채점 요약은 무엇입니까?
- 다양한 대상에 대해 내 고객 AI 성향 점수는 어떻게 변경됩니까?
- 내 채점 요약은 대상 개요의 다른 KPI와 어떻게 비교합니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT model_name,
         model_type,
         segment_name,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  JOIN QSAccel.profile_agg.adwh_dim_segments c ON a.segment_id=c.segment_id
  WHERE a.merge_policy_id=1133248113
    AND a.model_id =1829081696
    AND a.segment_id=1870062812
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_by_segment_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           segment_name,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [Customer AI 채점 요약 위젯 설명서](../guides/audiences.md#customer-ai-scoring-summary)를 참조하십시오.

## ID 중첩 {#identity-overlap}

이 통찰력에 의해 답변된 질문:

- 필터링된 대상에 대해 [!UICONTROL ID 유형 A]과(와) [!UICONTROL ID 유형 B] 간의 일반적인 교집합은 무엇입니까?
- 특정 ID 유형의 중복을 기반으로 고객 대상을 세분화하여 타깃팅된 마케팅 전략을 향상하려면 어떻게 해야 합니까?
- 교차하는 영역 내에서 캠페인 성과를 평가함으로써 얻을 수 있는 통찰력은 무엇입니까?
- 이러한 통찰력을 기반으로 향후 마케팅 노력을 최적화하려면 어떻게 해야 합니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        Sum(overlap_count) Overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace_by_segment.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 1709997014
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('crmid',
                                                                                          'email')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
    LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'email'
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10' ) a;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [ID 중복 위젯 설명서](../guides/audiences.md#identity-overlap)를 참조하세요.

## ID별 프로필 {#profiles-by-identity}

이 통찰력에 의해 답변된 질문:

- 선택한 대상에 대한 총 프로필 수 내에서 가장 높은 비율을 갖는 ID 유형은 무엇입니까?
- 선택한 대상에 대해 ID 유형 간에 큰 차이가 있습니까?
- 대상자별 ID 유형의 전체 분포는 무엇입니까?
- 다양한 대상에 대한 ID 수에 중요한 차이점이나 예외 항목이 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.segment_id = 1333234510
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.merge_policy_id = 1709997014
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_and_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

이 인사이트의 모양과 기능에 대한 자세한 내용은 [ID 위젯 설명서별 프로필](../guides/audiences.md#profiles-by-identity)을 참조하십시오.

## 예약된 활성화 {#scheduled-activations}

이 통찰력에 의해 답변된 질문:

- 특정 플랫폼에서 특정 대상에 대해 가장 성과가 좋은 활성화의 시작 및 종료 날짜는 무엇입니까?
- 특정 대상의 예약된 활성화에 가장 많이 사용된 플랫폼은 무엇입니까?
- 플랫폼 사용에서 특정 대상에 대한 활성화 전략의 우선순위 지정 또는 다양화에 대한 결정을 안내할 수 있는 패턴이 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT p.destination_platform ,
       p.destination_platform_name AS platform ,
       d.destination_name ,
       d.destination ,
       br.start_date ,
       CASE
           WHEN br.end_date = '9999-12-31' THEN 'Ongoing'
           ELSE br.end_date
       END AS end_date
  FROM qsaccel.profile_agg.adwh_dim_br_segment_destinations br
  JOIN qsaccel.profile_agg.adwh_dim_destination d ON br.destination_id = d.destination_id
  JOIN qsaccel.profile_agg.adwh_dim_destination_platform p ON d.destination_platform_id = p.destination_platform_id
  JOIN
    (SELECT MAX(process_date) AS last_process_date
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL' ) lpd ON lpd.last_process_date BETWEEN br.start_date AND br.end_date
  AND br.segment_id = 1333234510;
```

+++

이 인사이트의 모양 및 기능에 대한 자세한 내용은 [예약된 활성화 위젯 설명서](../guides/audiences.md#scheduled-activations)를 참조하십시오.

## 다음 단계

이제 이 문서를 읽고 대시보드 인사이트를 생성하는 SQL과 이 분석이 해결하는 일반적인 질문을 이해합니다. 이제 SQL을 편집하고 반복하여 고유한 인사이트를 생성할 수 있습니다.

PLatform UI를 통해 직접 인사이트의 SQL을 조정하는 방법에 대한 자세한 내용은 [SQL 보기 설명서](../view-sql.md)를 참조하십시오.

[프로필](./profiles.md), [계정 프로필](./account-profiles.md) 및 [대상](./destinations.md) 대시보드에 대한 인사이트를 생성하는 SQL을 읽고 이해할 수도 있습니다.
