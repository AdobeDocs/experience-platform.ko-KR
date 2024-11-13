---
title: 계정 프로필 통찰력
description: 계정 프로필 인사이트를 제공하는 SQL을 살펴보고 이러한 쿼리를 사용하여 고객 및 고객 경험을 추가로 살펴보는 사용자 지정 인사이트를 생성하십시오.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="B2P 버전" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: f9ef0e25dac1715bbb6d73db52d6368c543bf7ec
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# 계정 프로필 인사이트

[계정 프로필](../../rtcdp/accounts/account-profile-overview.md)은(는) 여러 마케팅 채널 및 조직 시스템을 포함하여 다양한 소스의 계정 정보를 통합하는 데 사용됩니다. 이러한 통합 보기를 통해 고객 계정을 포괄적으로 이해하고 B2B 마케팅 캠페인을 향상시킬 수 있습니다. 데이터 모델 분석을 통해 얻은 인사이트를 통해 Adobe Real-time Customer Data Platform B2B 데이터에 보다 쉽게 액세스하고, 이해할 수 있으며, 의사 결정에 영향을 줄 수 있습니다.

통찰력을 향상시키는 SQL에 액세스하여 B2B 데이터를 더 잘 이해하고, 사용자 지정이 가능한 자신만의 통찰력을 생성하여 고객 계정 정보를 더 자세히 살펴볼 수 있습니다. 기존 Real-Time CDP 데이터 모델 SQL을 영감으로 사용하여 원시 데이터를 새로운 실행 가능한 통찰력으로 변환하여 고유한 비즈니스 요구 사항에 맞는 쿼리를 만듭니다.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

다음 인사이트는 모두 [계정 프로필 대시보드](../guides/account-profiles.md) 또는 [사용자 지정 대시보드](../standard-dashboards.md)의 일부로 사용할 수 있습니다. 위젯 라이브러리 및 [사용자 정의 대시보드](../standard-dashboards.md#create-widget)에서 대시보드를 사용자 정의하거나 [새 위젯을 만들고 편집](../customize/custom-widgets.md)하는 방법에 대한 지침은 [사용자 정의 개요](../customize/overview.md)를 참조하세요.

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

## 업종별 신규 계정 {#accounts-by-industry}

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

## 유형별 새 계정 {#accounts-by-type}

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

## 기회 추가됨 {#opportunities-added}

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

## 개인 역할별 새로운 기회 {#opportunities-by-person-role}

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

## 매출액별 새로운 기회 {#opportunities-by-revenue}

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

## 상태 및 단계별 새로운 기회 {#opportunities-by-status-and-stage}

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

## 획득한 새로운 영업 기회 {#opportunities-won}

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

## 계정당 고객 개요 {#customers-per-account-overview}

>[!NOTE]
>
>[!UICONTROL 계정당 고객 개요] 차트에는 [!UICONTROL 계정당 고객 세부 정보], [!UICONTROL 계정당 기회 개요] 및 [!UICONTROL 계정당 기회 세부 정보]의 세 가지 드릴스루 인사이트가 포함됩니다. 이러한 드릴스루는 카테고리(예: 직접 및 간접 고객)와 범위(예: 고객 및 기회 수 범위)별로 고객 및 기회 수를 분류하여 보다 세분화된 통찰력을 제공합니다. 이러한 차트는 사용자가 설정했을 수 있는 글로벌 날짜 필터의 영향을 받지 않습니다.

이 통찰력에 의해 답변된 질문:

- 직간접 고객 유무에 따른 계좌의 분포는 어떠한가?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH LatestDate AS (SELECT MAX(inserted_date) AS max_inserted_date FROM adwh_b2b_account_person_association),
     CategorizedData AS (
         SELECT CASE 
                    WHEN is_direct = 'true' AND person_count = 0 THEN 'Accounts without Direct Customers' 
                    WHEN is_direct = 'false' AND person_count = 0 THEN 'Accounts without Indirect Customers' 
                    WHEN is_direct = 'true' AND person_count > 0 THEN 'Accounts with Direct Customers' 
                    WHEN is_direct = 'false' AND person_count > 0 THEN 'Accounts with Indirect Customers' 
                END AS Account_Category, 
                account_count 
         FROM adwh_b2b_account_person_association 
         WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
     ),
     AggregatedData AS (
         SELECT Account_Category, SUM(account_count) AS Accounts 
         FROM CategorizedData 
         GROUP BY Account_Category
     ),
     AllCategories AS (
         SELECT 'Accounts without Direct Customers' AS Account_Category 
         UNION ALL SELECT 'Accounts without Indirect Customers' 
         UNION ALL SELECT 'Accounts with Direct Customers' 
         UNION ALL SELECT 'Accounts with Indirect Customers'
     )
SELECT ac.Account_Category AS Account_Category, COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad ON ac.Account_Category = ad.Account_Category 
ORDER BY ac.Account_Category;
```

+++

## 계정당 고객 세부 정보 {#customers-per-account-detail}

>[!NOTE]
>
>이 인사이트는 글로벌 날짜 필터의 영향을 받지 않습니다.

이 통찰력에 의해 답변된 질문:

- 직접 또는 간접 고객 범위가 다른 계정은 몇 개입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH customer_ranges AS (
    SELECT 'Direct Customer' AS customer_type, '1-10 Customers' AS person_range 
    UNION ALL
    SELECT 'Direct Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '1000+ Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1-10 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1000+ Customers'
)
SELECT 
    cr.customer_type, 
    cr.person_range, 
    COALESCE(SUM(ap.account_count), 0) AS Accounts
FROM customer_ranges cr
LEFT JOIN (
    SELECT 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END AS customer_type,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END AS person_range,
        SUM(account_count) AS account_count
    FROM adwh_b2b_account_person_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_person_association) 
    GROUP BY 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END
) ap ON cr.customer_type = ap.customer_type AND cr.person_range = ap.person_range
GROUP BY cr.customer_type, cr.person_range
ORDER BY cr.customer_type, 
    CASE cr.person_range 
        WHEN '1-10 Customers' THEN 1 
        WHEN '11-100 Customers' THEN 2 
        WHEN '101-1000 Customers' THEN 3 
        WHEN '1000+ Customers' THEN 4 
    END;
```

+++

## 계정당 영업 기회 개요 {#opportunities-per-account-overview}

>[!NOTE]
>
>이 인사이트는 글로벌 날짜 필터의 영향을 받지 않습니다.

이 통찰력에 의해 답변된 질문:

- 관련 영업 기회가 있는지 여부에 따른 계정 분포는 무엇입니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH LatestDate AS (
    SELECT MAX(inserted_date) AS max_inserted_date 
    FROM adwh_b2b_account_opportunity_association
),
CategorizedData AS (
    SELECT 
        CASE 
            WHEN opportunity_count = 0 THEN 'Accounts without Opportunities'
            WHEN opportunity_count > 0 THEN 'Accounts with Opportunities'
        END AS Opportunity_Category, 
        account_count 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
),
AggregatedData AS (
    SELECT 
        Opportunity_Category,
        SUM(account_count) AS Accounts 
    FROM CategorizedData 
    GROUP BY Opportunity_Category
),
AllCategories AS (
    SELECT 'Accounts without Opportunities' AS Opportunity_Category 
    UNION ALL 
    SELECT 'Accounts with Opportunities'
)
SELECT 
    ac.Opportunity_Category AS Opportunity_Category, 
    COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad 
    ON ac.Opportunity_Category = ad.Opportunity_Category 
ORDER BY ac.Opportunity_Category;
```

+++

## 계정당 영업 기회 세부 정보 {#opportunities-per-account-detail}

>[!NOTE]
>
>이 인사이트는 글로벌 날짜 필터의 영향을 받지 않습니다.

이 통찰력에 의해 답변된 질문:

- 몇 개의 고객이 서로 다른 범위의 연계 기회를 가지고 있습니까?

+++이 통찰력을 생성하는 SQL을 표시하려면 선택합니다.

```sql
WITH opportunity_ranges AS (
    SELECT '1-10 Opportunities' AS opportunity_range 
    UNION ALL 
    SELECT '11-50 Opportunities' 
    UNION ALL 
    SELECT '51-100 Opportunities' 
    UNION ALL 
    SELECT '100+ Opportunities'
)
SELECT opportunity_ranges.opportunity_range AS OPPORTUNITIES, 
       COALESCE(SUM(accounts.total_accounts), 0) AS ACCOUNTS 
FROM opportunity_ranges 
LEFT JOIN (
    SELECT 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END AS opportunity_range, 
        SUM(account_count) AS total_accounts 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_opportunity_association) 
      AND opportunity_count > 0 
    GROUP BY 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END
) AS accounts ON opportunity_ranges.opportunity_range = accounts.opportunity_range 
GROUP BY opportunity_ranges.opportunity_range 
ORDER BY CASE opportunity_ranges.opportunity_range 
            WHEN '1-10 Opportunities' THEN 1 
            WHEN '11-50 Opportunities' THEN 2 
            WHEN '51-100 Opportunities' THEN 3 
            WHEN '100+ Opportunities' THEN 4 
        END;
```

+++

## 다음 단계

이제 이 문서를 읽고 계정 프로필 대시보드 인사이트를 생성하는 SQL과 이 분석이 해결하는 일반적인 질문을 이해합니다. 이제 SQL을 편집하고 반복하여 고유한 인사이트를 생성할 수 있습니다. SQL로 사용자 지정 인사이트를 생성하는 방법에 대해 알아보려면 [Query Pro 모드 개요](../sql-insights-query-pro-mode/overview.md)를 참조하세요.

[프로필](./profiles.md), [대상](./audiences.md) 및 [대상](./destinations.md) 대시보드에 대한 인사이트를 생성하는 SQL을 읽고 이해할 수도 있습니다.
