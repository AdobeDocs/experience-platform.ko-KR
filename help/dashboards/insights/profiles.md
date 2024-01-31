---
title: 프로필 인사이트
description: 프로필 인사이트를 제공하는 SQL을 살펴보고 이러한 쿼리를 사용하여 고객 및 고객 경험을 추가로 살펴보는 사용자 지정 인사이트를 생성하십시오.
source-git-commit: ee9ef2cf777c72fbd19cfccd80a37ea66591216d
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 1%

---

# 프로필 인사이트

데이터 모델 분석을 통해 얻은 인사이트를 통해 Adobe Real-time Customer Data Platform 데이터에 보다 쉽게 액세스하고, 이해할 수 있으며, 의사 결정에 영향을 줄 수 있습니다.

프로필을 구동하는 SQL에 액세스하여 프로필 인사이트를 파악한 다음 고유한 인사이트를 생성하여 프로필을 구성하는 고객 및 소비자 경험을 더욱 탐색합니다. 기존 Real-Time CDP 데이터 모델 SQL을 영감으로 사용하여 원시 데이터를 새로운 실행 가능한 통찰력으로 변환하여 고유한 비즈니스 요구 사항에 맞는 쿼리를 만듭니다.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI.  -->

다음 인사이트를 의 일부로 사용할 수 있습니다. [프로필 대시보드](../guides/profiles.md) 또는 사용자 지정 [사용자 정의 대시보드](../user-defined-dashboards.md). 다음을 참조하십시오. [사용자 지정 개요](../customize/overview.md) 대시보드 또는 를 사용자 지정하는 방법에 대한 지침 [새 위젯 만들기 및 편집](../customize/custom-widgets.md) 위젯 라이브러리 및 [사용자 정의 대시보드](../user-defined-dashboards.md#create-widget).

다음 인사이트를 의 일부로 사용할 수 있습니다. [프로필 대시보드](../guides/profiles.md) 또는 사용자 지정 대시보드.

## 병합 정책별 대상자 중복 {#audience-overlap-by-merge-policy}

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
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.date_key = '2024-01-10'
      AND ((qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1333234510
            AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1559754729)
            OR (qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment1=1559754729
                AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_segments.segment2=1333234510))
    UNION ALL SELECT sum(count_of_profiles) overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    LEFT JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1333234510
    UNION ALL SELECT 0 overlap_col1,
                      sum(count_of_profiles) overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_Id = qsaccel.profile_agg.adwh_dim_segments.segment_Id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_segments.segment_Id = 1559754729 ) a;
```

+++

다음을 참조하십시오. [병합 정책 위젯 설명서를 통한 대상 중복](../guides/profiles.md#audience-overlap-by-merge-policy) 를 참조하십시오.

## 대상 중복 보고서 {#audience-overlap-report}

이 통찰력에 의해 답변된 질문:

- 가장 겹치는 50명의 대상은 무엇입니까?
- 가장 중복이 적은 50명의 대상은 무엇입니까?
- 병합 정책별로 중복 패턴은 어떻게 변경됩니까?

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

다음을 참조하십시오. [대상 중복 보고서 위젯 설명서](../guides/profiles.md#audience-overlap-report) 를 참조하십시오.

## 대상자(수) {#audiences}

이 통찰력에 의해 답변된 질문:

- 주로 세그먼테이션에 사용되는 병합 정책은 무엇입니까?
- 병합 정책 간 대상 분포는 무엇입니까?
- 시간이 지남에 따라 특정 병합 정책에 대한 대상 수에 중요한 변화가 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT count(DISTINCT a.segment_id) count_of_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines a
  JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) b ON a.merge_policy_id= b.merge_policy_id
  AND a.date_key = b.last_process_date
  WHERE a.merge_policy_id= 2027892989;
```

+++

다음을 참조하십시오. [대상 위젯 설명서](../guides/profiles.md#audiences) 를 참조하십시오.

## 대상 상태에 매핑된 대상자 {#audiences-mapped-to-destination-status}

이 통찰력에 의해 답변된 질문:

- 매핑된 대상과 매핑되지 않은 대상 간의 전체 대상자 분포는 어떻게 됩니까?
- 매핑된 대상자 수가 가장 많은 특정 대상은 무엇입니까?
- 매핑되지 않은 상태로 남아 있는 전체 대상의 비율은 얼마입니까?
- 매핑되지 않은 이러한 대상자 중 패턴이나 관련 트렌드가 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT COUNT(DISTINCT (y.segment_id)) AS count_mapped_segments,
        COUNT(DISTINCT (x.segment_id)) - COUNT(DISTINCT (y.segment_id)) AS count_unmapped_segments,
        COUNT(DISTINCT (x.segment_id)) AS total_segments
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines x
  LEFT JOIN qsaccel.profile_agg.adwh_dim_br_segment_destinations y ON x.segment_id = y.segment_id
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
    FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
    WHERE process_name = 'FACT_TABLES_PROCESSING'
      AND process_status = 'SUCCESSFUL'
    GROUP BY merge_policy_id) z ON x.merge_policy_id = z.merge_policy_id
  AND x.date_key = z.last_process_date
  WHERE x.merge_policy_id = 2027892989;
```

+++

다음을 참조하십시오. [대상 상태 위젯 설명서에 매핑된 대상자](../guides/profiles.md#audiences-mapped-to-destination-status) 를 참조하십시오.

## 대상자 크기 {#audiences-size}

이 통찰력에 의해 답변된 질문:

- 가장 큰 크기를 갖는 대상 세그먼트는 무엇입니까?
- 가장 많은 5명의 대상자는 어디입니까?
- 최상위 대상의 대상 크기 분포는 시간에 따라 어떻게 변경됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
        qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
        qsaccel.profile_agg.adwh_dim_segments.segment,
        qsaccel.profile_agg.adwh_dim_segments.segment_name,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.count_of_profiles)count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_segments ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.segment_id = qsaccel.profile_agg.adwh_dim_segments.segment_id
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id=adwh_dim_merge_policies.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key = '2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.merge_policy_id= 2027892989
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_segment_trendlines.date_key,
          qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
          qsaccel.profile_agg.adwh_dim_segments.segment,
          qsaccel.profile_agg.adwh_dim_segments.segment_name
  ORDER BY count_of_profiles DESC
  LIMIT 20;
```

+++

다음을 참조하십시오. [대상 크기 위젯 설명서](../guides/profiles.md#audiences-size) 를 참조하십시오.

## 고객 AI 점수 분배 {#customer-ai-distribution-of-scores}

이 통찰력에 의해 답변된 질문:

- 각 고객 AI 모델에 대한 버킷 간 점수 분포는 무엇입니까?
- 고, 중, 저점수별 점수의 분포는 어떠한가?
- 병합 정책별 채점 분포의 분류는 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT b.model_name,
     b.model_type,
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
  FROM qsaccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN qsaccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id = b.merge_policy_id
  AND a.model_id = b.model_id
  WHERE a.merge_policy_id = 2027892989
    AND a.model_id = 1829081696
    AND score_date =
      (SELECT Max(score_date)
       FROM qsaccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id = a.model_id) GROUP  BY b.model_name,
          model_type,
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

다음을 참조하십시오. [점수 위젯 설명서의 고객 AI 배포](../guides/profiles.md#customer-ai-distribution-of-scores) 를 참조하십시오.

## Customer AI 점수 요약 {#customer-ai-scoring-summary}

이 통찰력에 의해 답변된 질문:

- 각 고객 AI 모델에 대한 점수 요약은 무엇입니까?
- 다양한 대상에 대해 내 고객 AI 성향 점수는 어떻게 변경됩니까?
- 프로필 개요에서 다른 KPI와 비교하여 채점 요약은 어떻게 변경됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT model_name,
         model_type,
         CASE
             WHEN score BETWEEN 0 AND 24 THEN 'LOW'
             WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
             WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
         END score_buckets,
         sum(count_of_profiles) count_of_profiles
  FROM QSAccel.profile_agg.adwh_fact_profile_ai_models a
  JOIN QSAccel.profile_agg.adwh_dim_ai_models b ON a.merge_policy_id=b.merge_policy_id
  AND a.model_id=b.model_id
  WHERE a.merge_policy_id=2027892989
    AND a.model_id =1829081696
    AND score_date=
      (SELECT max(score_date)
       FROM QSAccel.profile_agg.adwh_fact_profile_ai_models d
       WHERE d.model_id=a.model_id)
  GROUP BY model_name,
           model_type,
           CASE
               WHEN score BETWEEN 0 AND 24 THEN 'LOW'
               WHEN score BETWEEN 25 AND 74 THEN 'MEDIUM'
               WHEN score BETWEEN 75 AND 100 THEN 'HIGH'
           END;
```

+++

다음을 참조하십시오. [Customer AI 점수 요약 위젯 설명서](../guides/profiles.md#customer-ai-scoring-summary) 를 참조하십시오.

## ID 중첩 {#identity-overlap}

이 통찰력에 의해 답변된 질문:

- 어떤 게 공통적인 교차점이죠 [!UICONTROL ID 유형 A] 및 [!UICONTROL ID 유형 B]?
- 특정 ID 유형의 중복을 기반으로 고객 대상을 세분화하여 타깃팅된 마케팅 전략을 향상하려면 어떻게 해야 합니까?
- 교차하는 영역 내에서 캠페인 성과를 평가함으로써 얻을 수 있는 통찰력은 무엇입니까?
- 이 캠페인 성과 인사이트를 사용하여 향후 마케팅 노력을 최적화하는 방법은 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT Sum(overlap_col1) overlap_col1,
        Sum(overlap_col2) overlap_col2,
        coalesce(Sum(overlap_count), 0) overlap_count
  FROM
    (SELECT 0 overlap_col1,
            0 overlap_col2,
            Sum(count_of_profiles) overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace
    WHERE qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_fact_profile_overlap_of_namespace.overlap_id IN
        (SELECT a.overlap_id
          FROM
            (SELECT qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id overlap_id,
                    count(*) cnt_num
            FROM qsaccel.profile_agg.adwh_dim_overlap_namespaces
            WHERE qsaccel.profile_agg.adwh_dim_overlap_namespaces.merge_policy_id = 2027892989
              AND qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_namespaces in ('avid',
                                                                                          'crmid')
            GROUP BY qsaccel.profile_agg.adwh_dim_overlap_namespaces.overlap_id)a
          WHERE a.cnt_num>1 )
    UNION ALL SELECT count_of_profiles overlap_col1,
                      0 overlap_col2,
                      0 overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'avid'
    UNION ALL SELECT 0 overlap_col1,
                      count_of_profiles overlap_col2,
                      0 Overlap_count
    FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
    JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
    WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
      AND qsaccel.profile_agg.adwh_dim_namespaces.namespace_description = 'crmid' )a;
```

+++

다음을 참조하십시오. [ID 중복 위젯 설명서](../guides/profiles.md#identity-overlap) 를 참조하십시오.

## 프로필 개수 {#profile-count}

이 통찰력에 의해 답변된 질문:

- Adobe Real-time Customer Data Platform의 전체 프로필 수는 얼마입니까?
- 병합 정책을 기반으로 프로필이 배포되는 방법은 무엇입니까?
- 프로필 수가 가장 많은 병합 정책은 무엇입니까?

이러한 통찰력을 생성하는 SQl은 다음과 같습니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

이 인사이트의 모양과 기능에 대한 전체 정보는 [프로필 개수 위젯 안내서](https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count).

다음을 참조하십시오. [프로필 개수 위젯 설명서](../guides/profiles.md#profile-count) 를 참조하십시오.

## 프로필 개수 변경 {#profile-count-change}

이 통찰력에 의해 답변된 질문:

- 전체 프로필 수 변경의 트렌드는 무엇입니까?
- 프로필 수가 크게 증가 또는 감소한 원인은 무엇입니까?
- 프로필 개수 변경을 유도하는 특정 병합 정책이 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT (sum(count_of_profiles) - sum(count_of_profiles_days_ago)) profiles_added
  FROM
    (SELECT sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) count_of_profiles,
            0 count_of_profiles_days_ago
    FROM qsaccel.profile_agg.adwh_fact_profile
    WHERE qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
      AND qsaccel.profile_agg.adwh_fact_profile.date_key = '2024-01-10'
    UNION ALL SELECT 0 count_of_profiles,
                      CASE
                          WHEN sum(cntondatediff) =0 THEN sum(cntmin)
                          ELSE sum(cntondatediff)
                      END AS count_of_profiles_days_ago
    FROM
      (SELECT coalesce(sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles), 0) cntondatediff,
              0 cntmin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =dateadd(DAY, - 30, '2024-01-10')
        UNION ALL SELECT 0 cntondatediff,
                        sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) countMin
        FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key =
            (SELECT min(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) col
            FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
            WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id =2027892989
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >= dateadd(DAY, - 30, '2024-01-10')
              AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles IS NOT NULL) )b) a;
```

+++

다음을 참조하십시오. [프로필 개수 변경 위젯 설명서](../guides/profiles.md#profile-count-change) 를 참조하십시오.

## 프로필 개수 변경 트렌드 {#profile-count-change-trend}

이 통찰력에 의해 답변된 질문:

- 병합 정책을 기준으로 지난 12개월 동안 프로필 개수 변경의 전체 트렌드는 무엇입니까?
- 지난 30일 이내에 주의가 필요한 프로필 개수 변경에 특정 패턴이나 변동이 있습니까?
- 지난 90일 동안의 프로필 수는 전체 추세와 비교하여 어떻게 변경됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

다음을 참조하십시오. [프로필 개수 변경 트렌드 위젯 설명서](../guides/profiles.md#profile-count-change-trend) 를 참조하십시오.

## 프로필 개수 트렌드 {#profile-count-trend}

이 통찰력에 의해 답변된 질문:

- 지난 30일 동안의 병합 정책을 기반으로 하는 프로필 수의 전반적인 트렌드는 무엇입니까?
- 이 트렌드를 기반으로 장기 트렌드(예: 90일 및 12개월)와 어떻게 비교합니까?
- 지정된 기간(30일, 90일 및 12개월) 동안 프로필 수 증감에 가장 큰 기여를 하는 병합 정책은 무엇입니까?
- 30일 기간 내에 특정 이벤트 또는 기간과 상호 작용하는 프로필 수에 특정 스파이크나 드롭이 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT date_key,
       sum(count_of_profiles) AS count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines x
  INNER JOIN
    (SELECT MAX(process_date) last_process_date,
            merge_policy_id
     FROM qsaccel.profile_agg.adwh_lkup_process_delta_log
     WHERE process_name = 'FACT_TABLES_PROCESSING'
       AND process_status = 'SUCCESSFUL'
     GROUP BY merge_policy_id) y ON x.merge_policy_id = y.merge_policy_id
  WHERE date_key >= dateadd(DAY, -365, y.last_process_date)
    AND x.merge_policy_id = 2027892989
  GROUP BY date_key;
```

+++

다음을 참조하십시오. [프로필 개수 트렌드 위젯 설명서](../guides/profiles.md#profile-count-trend) 를 참조하십시오.

## ID별 프로필 {#profiles-by-identity}

이 통찰력에 의해 답변된 질문:

- 전체 프로필 수 중에서 어떤 ID 유형이 더 높은 비율을 차지합니까?
- 정체성 유형 간에 상당한 차이가 있습니까?
- ID 유형의 전체 분포는 무엇입니까?
- ID 수에 중요한 차이점이나 예외 항목이 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
  ORDER BY count_of_profiles DESC;
```

+++

다음을 참조하십시오. [ID 위젯 설명서별 프로필](../guides/profiles.md#profiles-by-identity) 를 참조하십시오.

## 프로필 개수 변경 트렌드 {#profiles-count-change-trend}

이 통찰력에 의해 답변된 질문:

- 병합 정책을 기반으로 지난 12개월 동안 프로필 수 변경의 전반적인 트렌드는 무엇입니까?
- 지난 30일 동안 주의가 필요한 프로필 수의 변화에 특정 패턴 또는 변동이 있습니까?
- 지난 90일 동안의 프로필 개수 변경은 전체 추세와 어떻게 비교됩니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT date_key,
         profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            (count_of_profiles-lag(count_of_profiles, 1, 0) over(
                                                            ORDER BY date_key))profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (
                              ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key) rn_num
      FROM qsaccel.profile_agg.adwh_fact_profile_by_trendlines
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key >=dateadd(DAY, - 30 -1, '2024-01-10')
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_trendlines.date_key)a)b
  WHERE rn_num > 1;
```

+++

다음을 참조하십시오. [프로필 개수 변경 트렌드 위젯 설명서](../guides/profiles.md#profiles-count-change-trend) 를 참조하십시오.

## ID별 프로필 개수 변경 트렌드 {#profiles-count-change-trend-by-identity}

이 통찰력에 의해 답변된 질문:

- 지난 12개월 동안 다른 ID에서 프로필 수가 변경된 전반적인 트렌드는 무엇입니까?
- 지난 30일 이내에 중요한 변경 사항을 보여주는 특정 ID 트렌드가 있습니까?
- 특정 ID에 대한 30일, 90일 및 12개월 트렌드를 비교할 때 프로필 수의 변경 사항은 어떻게 다릅니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT date_key,
        namespace_description,
        profiles_count_change
  FROM
    (SELECT rn_num,
            date_key,
            namespace_description,
            (count_of_profiles - lag(count_of_profiles, 1, 0) over(PARTITION BY namespace_description
                                                                  ORDER BY date_key)) profiles_count_change
    FROM
      (SELECT qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
              qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
              sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_profiles) count_of_profiles,
              row_number() OVER (PARTITION BY qsaccel.profile_agg.adwh_dim_namespaces.namespace_description
                                  ORDER BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key) rn_num
        FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
        LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
        AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
        WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id= -1042977439
          AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key >= dateadd(DAY, - 30 -1, '2024-01-10')
        GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
                adwh_dim_namespaces.namespace_description)a)b
  WHERE rn_num > 1;
```

+++

다음을 참조하십시오. [ID 위젯 설명서별 프로필 수 변경 트렌드](../guides/profiles.md#profiles-count-change-trend-by-identity) 를 참조하십시오.

## 단일 ID 프로필 {#single-identity-profiles}

이 통찰력에 의해 답변된 질문:

- 내 고객 ID 데이터가 일관되게 단일 ID로 표시됩니까?
- 단일 ID 유형만 있는 프로필로 구성된 사용자 베이스의 비율은 얼마입니까?
- 단일 ID 유형만 있는 프로필 중 이러한 프로필의 완성도는 어떻게 영향을 줍니까?
- 가장 일반적인 ID 유형과 단일 ID 프로필 수 간에 상관 관계가 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Single_Identity_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

다음을 참조하십시오. [단일 ID 프로필 위젯 설명서](../guides/profiles.md#single-identity-profiles) 를 참조하십시오.

## ID별 단일 ID 프로필 {#single-identity-profiles-by-identity}

이 통찰력에 의해 답변된 질문:

- 단일 ID(예: 이메일 또는 전화번호)로 등록한 고유 고객은 몇 명입니까?
- 이메일 또는 전화번호와 같은 다양한 ID 유형 간에 단일 ID 프로필의 분포는 무엇입니까?
- 단일 ID 프로필 내에 새로운 ID 패턴 또는 이동이 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_namespaces.namespace_description,
        sum(qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.count_of_Single_Identity_profiles) count_of_Single_Identity_profiles
  FROM qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_namespaces ON qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.namespace_id = qsaccel.profile_agg.adwh_dim_namespaces.namespace_id
  AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = qsaccel.profile_agg.adwh_dim_namespaces.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id = 2027892989
    AND qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key = '2024-01-10'
  GROUP BY qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.date_key,
          qsaccel.profile_agg.adwh_fact_profile_by_namespace_trendlines.merge_policy_id,
          qsaccel.profile_agg.adwh_dim_namespaces.namespace_description;
```

+++

다음을 참조하십시오. [ID 위젯 설명서별 단일 ID 프로필](../guides/profiles.md#single-identity-profiles-by-identity) 를 참조하십시오.

## 분할되지 않은 프로필 {#unsegmented-profiles}

이 통찰력에 의해 답변된 질문:

- 대상자에 포함되지 않는 프로필은 몇 개입니까?
- 세분화되지 않은 프로필로 표현되는 대상자 비율은 얼마입니까?
- 병합 정책이 세그먼트화되지 않은 프로필 수에 기여합니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_Orphan_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

다음을 참조하십시오. [세분화되지 않은 프로필 위젯 설명서](../guides/profiles.md#unsegmented-profiles) 를 참조하십시오.

## 다음 단계

이제 이 문서를 읽고 대시보드 인사이트를 생성하는 SQL과 이 분석이 해결하는 일반적인 질문을 이해합니다. 이제 SQL을 편집하고 반복하여 고유한 인사이트를 생성할 수 있습니다.

<!-- This link will go in during the January release.
See the [View SQL documentation]() for more information on how to adapt your insights' SQL directly through the PLatform UI. -->

다음에 대한 인사이트를 생성하는 SQL을 읽고 이해할 수도 있습니다. [대상](./audiences.md) 및 [대상](./destinations.md) 대시보드.
