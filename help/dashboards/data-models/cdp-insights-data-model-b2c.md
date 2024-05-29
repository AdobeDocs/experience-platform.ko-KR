---
title: Real-time Customer Data Platform Insights 데이터 모델 B2C 에디션
description: Real-time Customer Data Platform Insights 데이터 모델(B2C 버전)과 함께 SQL 쿼리를 사용하여 마케팅 및 KPI 사용 사례에 맞게 고유한 Real-Time CDP 보고서를 사용자 지정하는 방법을 알아봅니다.
badgeB2B: label="B2B 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 61bc7f23-9f79-4c75-a515-85dd9dda2d02
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Real-time Customer Data Platform Insights 데이터 모델 B2C 에디션

를 위한 Real-time Customer Data Platform 통찰력 데이터 모델 [B2C 버전](../../rtcdp/overview.md#rtcdp-b2c) 다양한 프로필, 대상 및 세그멘테이션 위젯에 대한 통찰력을 제공하는 데이터 모델 및 SQL을 표시합니다. 이러한 SQL 쿼리 템플릿을 사용자 정의하여 마케팅 및 주요 성능 지표(KPI) 사용 사례에 대한 Real-Time CDP 보고서를 만들 수 있습니다. 그런 다음 이러한 인사이트를 사용자 정의 대시보드에 대한 사용자 정의 위젯으로 사용할 수 있습니다. 자세한 내용은 쿼리 가속 스토어 보고 인사이트 설명서 를 참조하십시오 [가속화된 스토어 데이터 및 사용자 정의 대시보드와 함께 사용하기 위해 쿼리 서비스를 통해 보고 인사이트 데이터 모델을 구축하는 방법](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md).

>[!NOTE]
>
>&quot;세그먼트&quot;라는 용어가 Adobe Experience Platform 시스템에서 &quot;대상&quot;으로 업데이트되었습니다. 세그먼트에 대한 일부 참조는 파일 경로 및 데이터 세트 이름 지정 규칙에 계속 사용됩니다.

## 전제 조건

이 안내서를 사용하려면 다음을 이해할 수 있어야 합니다 [사용자 정의 대시보드 기능](../user-defined-dashboards.md). 이 안내서를 계속하기 전에 설명서를 읽어 보십시오.

## Real-Time CDP 인사이트 보고서 및 사용 사례

Real-Time CDP 보고에서는 프로필 데이터와 대상 및 대상과의 관계에 대한 통찰력을 제공합니다. 다양한 일반적인 마케팅 활용 사례에 답변할 수 있도록 다양한 스타 스키마 모델을 개발하였으며, 각 데이터 모델은 여러 활용 사례를 지원할 수 있다.

>[!IMPORTANT]
>
>Real-Time CDP 보고에 사용된 데이터는 선택한 병합 정책 및 가장 최근 일별 스냅샷에서 정확합니다.

### 프로필 모델 {#profile-model}

프로필 모델은 다음 세 개의 데이터 세트로 구성됩니다.

- `adwh_dim_date`
- `adwh_fact_profile`
- `adwh_dim_merge_policies`

아래 이미지에는 각 데이터 세트의 관련 데이터 필드가 포함되어 있습니다.

![프로필 모델의 ERD입니다.](../images/cdp-insights/profile-model.png)

#### 프로필 개수 사용 사례 {#profile-count}

에 사용되는 논리 [!UICONTROL 프로필 개수] 위젯은 스냅숏을 만들 때 프로필 저장소 내에 있는 병합된 프로필의 총 수를 반환합니다. 다음을 참조하십시오. [[!UICONTROL 프로필 개수] 위젯 설명서](../guides/profiles.md#profile-count) 추가 정보.

다음을 생성하는 SQL [!UICONTROL 프로필 개수] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

```sql
SELECT qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name,
       sum(qsaccel.profile_agg.adwh_fact_profile.count_of_profiles) CNT
  FROM qsaccel.profile_agg.adwh_fact_profile
  LEFT OUTER JOIN qsaccel.profile_agg.adwh_dim_merge_policies ON qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_id=adwh_fact_profile.merge_policy_id
  WHERE qsaccel.profile_agg.adwh_fact_profile.date_key='2024-01-10'
    AND qsaccel.profile_agg.adwh_fact_profile.merge_policy_id = 2027892989
  GROUP BY qsaccel.profile_agg.adwh_dim_merge_policies.merge_policy_name;
```

+++

#### 단일 ID 프로필 사용 사례 {#single-identity-profiles}

에 사용되는 논리 [!UICONTROL 단일 ID 프로필] 위젯에서는 ID를 생성하는 한 가지 유형의 ID만 있는 조직 프로필 수를 제공합니다. 다음을 참조하십시오. [[!UICONTROL 단일 ID 프로필] 위젯 설명서](../guides/profiles.md#single-identity-profiles) 추가 정보.

다음을 생성하는 SQL [!UICONTROL 단일 ID 프로필] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

### 네임스페이스 모델 {#namespace-model}

네임스페이스 모델은 다음 데이터 세트로 구성됩니다.

- `adwh_dim_date`
- `adwh_fact_profile_by_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_namespaces`

아래 이미지에는 각 데이터 세트의 관련 데이터 필드가 포함되어 있습니다.

![네임스페이스 모델의 ERD입니다.](../images/cdp-insights/namespace-model.png)

#### ID별 프로필 사용 사례 {#profiles-by-identity}

다음 [!UICONTROL ID별 프로필] 위젯은 프로필 스토어에 있는 병합된 모든 프로필의 id 분류를 표시합니다. 다음을 참조하십시오. [[!UICONTROL ID별 프로필] 위젯 설명서](../guides/profiles.md#profiles-by-identity) 추가 정보.

다음을 생성하는 SQL [!UICONTROL ID별 프로필] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

#### ID 사용 사례별 단일 ID 프로필 {#single-identity-profiles-by-identity}

에 사용되는 논리 [!UICONTROL ID별 단일 ID 프로필] 위젯은 하나의 고유 식별자로만 식별되는 총 프로필 수를 보여 줍니다. 다음을 참조하십시오. [ID 위젯 설명서별 단일 ID 프로필](../guides/profiles.md#single-identity-profiles-by-identity) 추가 정보.

다음을 생성하는 SQL [!UICONTROL ID별 단일 ID 프로필] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

### 대상 모델 {#audience-model}

대상 모델은 다음 데이터 세트로 구성됩니다.

- `adwh_dim_date`
- `adwh_fact_profile_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

아래 이미지에는 각 데이터 세트의 관련 데이터 필드가 포함되어 있습니다.

![대상 모델의 ERD.](../images/cdp-insights/audience-model.png)

#### 대상자 크기 사용 사례 {#audience-size}

에 사용되는 논리 [!UICONTROL 대상 크기] 위젯은 가장 최근의 스냅샷 시점에 선택한 대상 내에서 병합된 프로필의 총 수를 반환합니다. 다음을 참조하십시오. [[!UICONTROL 대상 크기] 위젯 설명서](../guides/audiences.md#audience-size) 추가 정보.

다음을 생성하는 SQL [!UICONTROL 대상 크기] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

#### 대상자 크기 변경 트렌드 사용 사례 {#audience-size-change-trend}

에 사용되는 논리 [!UICONTROL 대상자 크기 변경 트렌드] 위젯은 가장 최근의 일별 스냅샷 간 주어진 대상자에 대해 자격이 있는 총 프로필 수의 차이에 대한 선 그래프 일러스트레이션을 제공합니다. 다음을 참조하십시오. [[!UICONTROL 대상자 크기 변경 트렌드] 위젯 설명서](../guides/audiences.md#audience-size-change-trend) 추가 정보.

다음을 생성하는 SQL [!UICONTROL 대상자 크기 변경 트렌드] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

#### 가장 많이 사용되는 대상 사용 사례 {#most-used-destinations}

에 사용되는 논리 [!UICONTROL 가장 많이 사용한 대상] 위젯은 매핑된 대상자 수에 따라 조직에서 가장 많이 사용하는 대상을 나열합니다. 이 순위는 어떤 대상이 활용되고 있는지에 대한 통찰력을 제공하는 동시에 활용도가 낮을 수 있는 대상을 잠재적으로 보여 줍니다. 다음에서 설명서를 참조하십시오. [[!UICONTROL 가장 많이 사용한 대상] 위젯](../guides/destinations.md#most-used-destinations) 추가 정보.

다음을 생성하는 SQL [!UICONTROL 가장 많이 사용한 대상] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

#### 최근에 활성화된 대상자 사용 사례 {#recently-activated-audiences}

에 대한 논리 [!UICONTROL 최근에 활성화된 대상자] 위젯은 대상에 가장 최근에 매핑된 대상자의 목록을 제공합니다. 이 목록은 시스템에서 사용 중인 대상 및 대상의 스냅샷을 제공하며 잘못된 매핑을 해결하는 데 도움이 됩니다. 다음을 참조하십시오. [[!UICONTROL 최근에 활성화된 대상자] 위젯 설명서](../guides/destinations.md#recently-activated-audiences) 추가 정보.

다음을 생성하는 SQL [!UICONTROL 최근에 활성화된 대상자] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

### 네임스페이스-대상 모델 {#namespace-audience-model}

네임스페이스-대상 모델은 다음 데이터 세트로 구성됩니다.

- `adwh_dim_date`
- `adwh_dim_namespaces`
- `adwh_fact_profile_by_segment_and_namespace`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

아래 이미지에는 각 데이터 세트의 관련 데이터 필드가 포함되어 있습니다.

![네임스페이스-대상 모델의 ERD입니다.](../images/cdp-insights/namespace-audience-model.png)

#### 대상자 사용 사례에 대한 ID별 프로필 {#audience-profiles-by-identity}

에 사용되는 논리 [!UICONTROL ID별 프로필] 위젯은 지정된 대상자에 대해 프로필 스토어에 있는 모든 병합된 프로필에서 id의 분류를 제공합니다. 다음을 참조하십시오. [[!UICONTROL ID별 프로필] 위젯 설명서](../guides/audiences.md#profiles-by-identity) 추가 정보.

다음을 생성하는 SQL [!UICONTROL ID별 프로필] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

### 네임스페이스 모델 겹치기

중첩 네임스페이스 모델은 다음 데이터 세트로 구성됩니다.

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace`
- `adwh_dim_merge_policies`

아래 이미지에는 각 데이터 세트의 관련 데이터 필드가 포함되어 있습니다.

![중첩 네임스페이스 모델의 ERD입니다.](../images/cdp-insights/overlap-namespace-model.png)

#### ID 중복(프로필) 사용 사례 {#profiles-identity-overlap}

에 사용되는 논리 [!UICONTROL ID 중복] 위젯은 의 프로필 중복을 표시합니다. **프로필 저장소** 선택한 두 id가 포함됩니다. 자세한 내용은 [[!UICONTROL ID 중복] 의 위젯 섹션 [!UICONTROL 프로필] 대시보드 설명서](../guides/profiles.md#identity-overlap).

다음을 생성하는 SQL [!UICONTROL ID 중복] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

### 대상 모델별 Overlap Namespace {#overlap-namespace-by-audience-model}

대상 모델별 중복 네임스페이스는 다음 데이터 세트로 구성됩니다.

- `adwh_dim_date`
- `adwh_dim_overlap_namespaces`
- `adwh_fact_profile_overlap_of_namespace_by_segment`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

아래 이미지에는 각 데이터 세트의 관련 데이터 필드가 포함되어 있습니다.

![대상 모델별 오버랩 네임스페이스의 ERD입니다.](../images/cdp-insights/overlap-namespace-by-audience-model.png)

#### ID 중복(대상) 사용 사례 {#audiences-identity-overlap}

에 사용되는 논리 [!UICONTROL 대상] 대시보드 [!UICONTROL ID 중복] 위젯은 특정 대상자에 대해 선택한 두 개의 id가 포함된 프로필의 겹침을 보여 줍니다. 자세한 내용은 [[!UICONTROL ID 중복] 의 위젯 섹션 [!UICONTROL 대상] 대시보드 설명서](../guides/audiences.md#identity-overlap).

다음을 생성하는 SQL [!UICONTROL ID 중복] 위젯은 아래의 축소 가능한 섹션에 표시됩니다.

+++SQL 쿼리

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

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### Overlap Namespace-Audience model {#overlap-namespace-audience-model}

The overlap namespace-audience model is comprised of the following datasets: 

- `adwh_fact_profile_overlap_by_namespace_and_segment`
- `adwh_dim_date`
- `adwh_dim_namespace`
- `adwh_dim_overlap_namespaces`
- `adwh_dim_merge_policies`
- `adwh_dim_segments`
- `adwh_dim_br_segment_destinations`
- `adwh_dim_destination`
- `adwh_dim_destination_platform`

![An ERD of the overlap namespace-audience model.](../images/cdp-insights/overlap-namespace-audience-model.png) -->

<!-- What insights are gathered from this particular data model? -->

<!-- Commented out as Anil wanted to add something but did not provide information yet:
### AI model {#ai-model}

The AI model is comprised of the following datasets: 

- `adwh_fact_profile_ai_models`
- `adwh_dim_date`
- `adwh_dim_merge_policies`
- `adwh_dim_ai_models`

![An ERD of the AI model.](./images/cdp-insights/ai-model.png) -->

<!-- What insights are gathered from this particular data model? -->

