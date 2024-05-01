---
title: 계정 프로필 통찰력
description: 계정 프로필 인사이트를 제공하는 SQL을 살펴보고 이러한 쿼리를 사용하여 고객 및 고객 경험을 추가로 살펴보는 사용자 지정 인사이트를 생성하십시오.
badgeB2B: label="B2B 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: b7875128592b17044b068d8064de082bf00a8309
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# 계정 프로필 인사이트

[계정 프로필](../../rtcdp/accounts/account-profile-overview.md) 은 여러 마케팅 채널 및 조직 시스템을 포함하여 다양한 소스의 계정 정보를 통합하는 데 사용됩니다. 이러한 통합 보기를 통해 고객 계정을 포괄적으로 이해하고 B2B 마케팅 캠페인을 향상시킬 수 있습니다. 데이터 모델 분석을 통해 얻은 인사이트를 통해 Adobe Real-time Customer Data Platform B2B 데이터에 보다 쉽게 액세스하고, 이해할 수 있으며, 의사 결정에 영향을 줄 수 있습니다.

통찰력을 향상시키는 SQL에 액세스하여 B2B 데이터를 더 잘 이해하고, 사용자 지정이 가능한 자신만의 통찰력을 생성하여 고객 계정 정보를 더 자세히 살펴볼 수 있습니다. 기존 Real-Time CDP 데이터 모델 SQL을 영감으로 사용하여 원시 데이터를 새로운 실행 가능한 통찰력으로 변환하여 고유한 비즈니스 요구 사항에 맞는 쿼리를 만듭니다.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

다음 인사이트를 의 일부로 사용할 수 있습니다. [계정 프로필 대시보드](../guides/account-profiles.md) 또는 [사용자 지정 대시보드](../user-defined-dashboards.md). 다음을 참조하십시오. [사용자 지정 개요](../customize/overview.md) 대시보드 또는 를 사용자 지정하는 방법에 대한 지침 [새 위젯 만들기 및 편집](../customize/custom-widgets.md) 위젯 라이브러리 및 [사용자 정의 대시보드](../user-defined-dashboards.md#create-widget).

## 계정 프로필 추가됨 {#account-profiles-added}

이 통찰력에 의해 답변된 질문:

- 지정된 기간 동안 얼마나 많은 계정 프로필이 추가되었습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## 업종별 계정 {#accounts-by-industry}

이 통찰력에 의해 답변된 질문:

- 계정 프로필이 속하는 상위 5개 산업은 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## 유형별 계정 {#accounts-by-type}

이 통찰력에 의해 답변된 질문:

- 유형별 계정 수는 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## 영업 기회 추가됨 {#opportunities-added}

이 통찰력에 의해 답변된 질문:

- 주어진 기간 동안 몇 개의 기회가 추가되었습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## 개인 역할별 기회 {#opportunities-by-person-role}

이 통찰력에 의해 답변된 질문:

- 기회에서 다양한 역할의 상대적 크기와 수는 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## 매출액별 영업 기회 {#opportunities-by-revenue}

이 통찰력에 의해 답변된 질문:

- 매출(USD)로 순위가 매겨진 상위 20개 기회는 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## 상태 및 단계별 영업 기회 {#opportunities-by-status-and-stage}

이 통찰력에 의해 답변된 질문:

- 어떤 오픈 기회가 있으며 판매 또는 마케팅 단계의 어느 단계에 있습니까?
- 마감된 영업 기회는 무엇이며, 영업 또는 마케팅 단계의 어느 단계에 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## 성공한 영업 기회 {#opportunities-won}

이 통찰력에 의해 답변된 질문:

- 정상적으로 종료되거나 완료된 영업 기회의 수는 얼마입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## 성공한 영업 기회(선 그래프) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

이 통찰력에 의해 답변된 질문:

- 주어진 기간 동안 성공적으로 마감되거나 최종 확정(원)된 기회는 몇 개입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## 다음 단계

이제 이 문서를 읽고 계정 프로필 대시보드 인사이트를 생성하는 SQL과 이 분석이 해결하는 일반적인 질문을 이해합니다. 이제 SQL을 편집하고 반복하여 고유한 인사이트를 생성할 수 있습니다.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

다음에 대한 인사이트를 생성하는 SQL을 읽고 이해할 수도 있습니다. [프로필](./profiles.md), [대상](./audiences.md), 및 [대상](./destinations.md) 대시보드.
