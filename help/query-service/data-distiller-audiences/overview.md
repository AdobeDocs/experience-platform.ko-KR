---
title: SQL을 사용하여 대상 작성
description: Adobe Experience Platform의 Data Distiller에서 SQL 대상 확장을 사용하여 SQL 명령을 사용하여 대상을 만들고, 관리하고, 게시하는 방법에 대해 알아봅니다. 이 안내서에서는 프로필 만들기, 업데이트 및 삭제, 데이터 기반 대상 정의 사용 등 대상 라이프사이클의 모든 측면을 다룹니다.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 9e16282f9f10733fac9f66022c521684f8267167
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 2%

---

# SQL을 사용하여 대상 작성

SQL 대상 확장을 사용하여 기존 차원 엔티티(예: 고객 속성 또는 제품 정보)를 포함하여 데이터 레이크의 데이터로 대상을 작성합니다.

이 SQL 확장을 사용하면 대상 세그먼트를 정의할 때 프로필에 원시 데이터가 필요하지 않으므로 대상을 만들 수 있는 기능이 향상됩니다. 이 방법을 사용하여 만든 대상은 Audience 작업 영역에 자동으로 등록되며, 여기에서 파일 기반 대상으로 추가 타깃팅할 수 있습니다.

![SQL 대상 확장 워크플로를 보여 주는 인포그래픽입니다. 단계에는 SQL 명령을 사용하여 Query Service로 대상을 빌드하고, Experience Platform UI에서 관리하며, 파일 기반 대상에서 활성화합니다.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

이 문서에서는 Adobe Experience Platform의 Data Distiller에서 SQL 대상 확장을 사용하여 SQL 명령을 사용하여 대상을 만들고, 관리하고, 게시하는 방법에 대해 설명합니다.

## Data Distiller의 고객 생성 라이프사이클 {#audience-creation-lifecycle}

다음 단계에 따라 대상자를 만들고, 관리하고, 활성화합니다. 생성된 대상은 &#39;대상 흐름&#39;에 원활하게 통합되므로 고객 전달을 위해 기본 대상에서 세그먼트를 작성하고 파일 기반 대상(예: CSV 업로드 또는 클라우드 스토리지 위치)을 타깃팅할 수 있습니다. &#39;대상 흐름&#39;은 대상을 만들고, 관리하고, 활성화하여 대상 간에 매끄러운 통합을 보장하는 전체 프로세스를 의미합니다.

&#39;대상 흐름&#39;의 일부로 다음 SQL 명령을 사용하여 Adobe Experience Platform에서 [만들기](#create-audience), [수정](#add-profiles-to-audience) 및 [삭제](#delete-audience)대상을 만듭니다.

### 대상자 만들기 {#create-audience}

`CREATE AUDIENCE AS SELECT` 명령을 사용하여 새 대상을 정의합니다. 만든 대상은 데이터 집합에 저장되고 Data Distiller의 [!UICONTROL 대상] 작업 영역에 등록됩니다.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title'])
AS (select_query)
```

**매개 변수**

다음 매개 변수를 사용하여 SQL 대상자 만들기 쿼리를 정의합니다.

| 매개변수 | 설명 |
|--------------------|------------------------------------------------------------------|
| `schema` | 선택 사항입니다. 쿼리로 만든 데이터 세트에 대한 XDM 스키마를 정의합니다. |
| `table_name` | 테이블 및 대상자의 이름입니다. |
| `primary_identity` | 대상자의 기본 ID 열을 지정합니다. |
| `identity_namespace` | ID 네임스페이스. 기존 네임스페이스를 사용하거나 새 네임스페이스를 만들 수 있습니다. 사용 가능한 네임스페이스를 보려면 `SHOW NAMESPACES` 명령을 사용하십시오. 새 네임스페이스를 만들려면 `CREATE NAMESPACE`을(를) 사용합니다. 예: `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | 대상을 정의하는 SELECT 문입니다. SELECT 쿼리의 구문은 [SELECT 쿼리](../sql/syntax.md#select-queries) 섹션에 있습니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>복잡한 데이터 구조에 더 많은 유연성을 제공하기 위해 대상을 정의할 때 보강된 속성을 중첩할 수 있습니다. 필요에 따라 대상자를 필터링하는 데 `orders`, `total_revenue`, `recency`, `frequency` 및 `monetization`과(와) 같은 보강된 특성을 사용할 수 있습니다.

**예:**

다음 예제에서는 SQL 대상자 만들기 쿼리를 구성하는 방법을 보여 줍니다.

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

이 예제에서 `userId` 열은 ID 열로 식별되고 적절한 네임스페이스(`lumaCrmId`)가 할당됩니다. 나머지 열(`orders`, `total_revenue`, `recency`, `frequency` 및 `monetization`)은 대상에 대한 추가 컨텍스트를 제공하는 보강된 특성입니다.

**제한 사항:**

대상 생성을 위해 SQL을 사용할 때 다음 제한 사항에 유의하십시오.

- 기본 ID 열 **must**&#x200B;은(는) 다른 특성 또는 범주 내에 중첩되지 않고 데이터 집합의 최상위 수준에 있어야 합니다.
- SQL 명령을 사용하여 생성된 외부 대상의 보존 기간은 30일입니다. 30일 후에는 이러한 대상이 자동으로 삭제되므로 대상 관리 전략을 계획하는 데 중요한 고려 사항이 됩니다.

### 기존 대상자에 프로필 추가 {#add-profiles-to-audience}

`INSERT INTO` 명령을 사용하여 기존 대상자에 프로필(또는 전체 대상자)을 추가하십시오.

```sql
INSERT INTO table_name
SELECT select_query
```

**매개 변수**

아래 표에서는 `INSERT INTO` 명령에 필요한 매개 변수에 대해 설명합니다.

| 매개변수 | 설명 |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | 대상자 만들기 명령의 일부로 만들어진 표의 이름입니다. |
| `select_query` | SELECT 문. SELECT 쿼리의 구문은 SELECT 쿼리 섹션에 있습니다. |

{style="table-layout:auto"}

**예:**

다음 예제에서는 `INSERT INTO` 명령을 사용하여 기존 대상자에 프로필을 추가하는 방법을 보여 줍니다.

```sql
INSERT INTO Audience aud_test
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### 대상 데이터 바꾸기(삽입: 덮어쓰기) {#replace-audience}

`INSERT OVERWRITE INTO` 명령을 사용하여 대상에 있는 모든 기존 프로필을 새 SQL 쿼리 결과로 바꿉니다. 이 명령은 한 단계에서 대상자의 콘텐츠를 완전히 새로 고칠 수 있도록 하여 동적 대상자 세그먼트를 관리하는 데 유용합니다.

>[!AVAILABILITY]
>
>`INSERT OVERWRITE INTO` 명령은 Data Distiller 고객만 사용할 수 있습니다. Data Distiller 추가 기능에 대한 자세한 내용은 Adobe 담당자에게 문의하십시오.

현재 대상자에 추가하는 [`INSERT INTO`](#add-profiles-to-audience)과(와) 달리 `INSERT OVERWRITE INTO`은(는) 기존 대상자 멤버를 모두 제거하고 쿼리에서 반환된 멤버만 삽입합니다. 이를 통해 자주 업데이트하거나 전체 업데이트가 필요한 대상자를 관리할 때 제어 기능과 유연성을 높일 수 있습니다.

다음 구문 템플릿을 사용하여 대상자를 새 프로필 세트로 덮어씁니다.

```sql
INSERT OVERWRITE INTO audience_name
SELECT select_query
```

**매개 변수**

아래 표에서는 `INSERT OVERWRITE INTO` 명령에 필요한 매개 변수에 대해 설명합니다.

| 매개변수 | 설명 |
|-----------|-------------|
| `audience_name` | `CREATE AUDIENCE` 명령을 사용하여 만든 대상자의 이름입니다. |
| `select_query` | 대상자에 포함할 프로필을 정의하는 `SELECT` 문입니다. |

**예:**

이 예제에서는 `audience_monthly_refresh` 대상자를 쿼리 결과로 완전히 덮어씁니다. 쿼리에서 반환되지 않은 모든 프로필은 대상에서 제거됩니다.

>[!NOTE]
>
>덮어쓰기 작업이 올바르게 작동하려면 대상과 연결된 일괄 업로드 하나만 있어야 합니다.

```sql
INSERT OVERWRITE INTO audience_monthly_refresh
SELECT user_id FROM latest_transaction_summary WHERE total_spend > 100;
```

#### 실시간 고객 프로필의 대상 덮어쓰기 동작

대상을 덮어쓰는 경우 실시간 고객 프로필은 다음 논리를 적용하여 프로필 멤버십을 업데이트합니다.

- 새 배치에만 나타나는 프로필은 입력된 것으로 표시됩니다.
- 이전 배치에만 있던 프로필은 종료됨으로 표시됩니다.
- 두 배치에 있는 프로필은 변경되지 않은 상태로 유지됩니다(아무 작업도 수행되지 않음).

이렇게 하면 대상 업데이트가 다운스트림 시스템 및 워크플로에 정확하게 반영됩니다.

**예제 시나리오**

대상 `A1`에 원래 다음이 포함된 경우:

| ID | 이름 |
|----|------|
| A | 잭 |
| B | John |
| C | 마사 |

그러면 덮어쓰기 쿼리는 다음을 반환합니다.

| ID | 이름 |
|----|------|
| A | 스튜어트 |
| C | 마사 |

그러면 업데이트된 대상자에 다음이 포함됩니다.

| ID | 이름 |
|----|------|
| A | 스튜어트 |
| C | 마사 |

프로필 B가 제거되고 프로필 A가 업데이트되며 프로필 C는 변경되지 않은 상태로 유지됩니다.

덮어쓰기 쿼리에 새 프로필이 포함된 경우:

| ID | 이름 |
|----|------|
| A | 스튜어트 |
| C | 마사 |
| D | 크리스 |

그러면 최종 대상자는 다음과 같습니다.

| ID | 이름 |
|----|------|
| A | 스튜어트 |
| C | 마사 |
| D | 크리스 |

### RFM 모델 대상 예 {#rfm-model-audience-example}

다음 예에서는 RFM(최신성, 빈도 및 수익화) 모델을 사용하여 대상자를 만드는 방법을 보여 줍니다. 이 예제는 최신성, 빈도 및 수익성 점수를 기반으로 고객을 분류하여 단골 고객, 신규 고객 및 고가치 고객과 같은 주요 그룹을 식별합니다.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

다음 쿼리는 RFM 대상에 대한 스키마를 만듭니다. 문은 `userId`, `days_since_last_purchase`, `orders`, `total_revenue` 등과 같은 고객 정보를 포함하는 필드를 설정합니다.

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

대상자를 만든 후 고객 데이터로 채우고 RFM 점수를 기반으로 프로필을 세그먼트화합니다. 아래 SQL 문은 `NTILE(4)` 함수를 사용하여 RFM(최신성, 빈도, 수익화) 점수를 기반으로 고객의 등급을 사분위수로 지정합니다. 이러한 점수는 고객을 &#39;핵심&#39;, &#39;충성도&#39;, &#39;고래&#39;의 6개 세그먼트로 분류합니다. 그런 다음 세그먼트화된 고객 데이터가 대상 `adls_rfm_profile` 테이블에 삽입됩니다.&quot;

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
```

### 대상자 삭제(대상자 삭제) {#delete-audience}

기존 대상자를 삭제하려면 `DROP AUDIENCE` 명령을 사용하십시오. 대상이 없는 경우 `IF EXISTS`을(를) 지정하지 않으면 예외가 발생합니다.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**매개 변수**

테이블에 `DROP AUDIENCE` 명령에 필요한 매개 변수가 포함되어 있습니다.

| 매개변수 | 설명 |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | 선택 사항입니다. 지정하면 테이블을 찾을 수 없는 경우 예외가 발생하지 않습니다. |
| `db_name` | 대상 데이터 세트를 정규화하는 데 사용되는 데이터 그룹을 지정합니다. |
| `table_name` | 대상자 만들기 명령의 일부로 만들어진 표의 이름입니다. |

{style="table-layout:auto"}

**예:**

다음 예에서는 DROP AUDIENCE 명령을 사용하여 대상을 삭제하는 방법을 보여 줍니다.

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### 자동 대상자 등록 및 가용성 {#registration-and-availability}

SQL 확장을 사용하여 만든 대상은 대상 작업 영역의 데이터 Distiller [!UICONTROL 원본]에 자동으로 등록됩니다. 등록되면 이러한 대상을 파일 기반 대상에서 타기팅할 수 있으므로 세그멘테이션 및 타기팅 전략이 향상됩니다. 이 프로세스에서는 추가적인 구성이 필요하지 않으므로 대상자 관리가 간소화됩니다. Experience Platform UI에서 대상을 보고, 관리하고, 만드는 방법에 대한 자세한 내용은 [대상 포털 개요](../../segmentation/ui/audience-portal.md)를 참조하십시오.

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![Adobe Experience Platform의 대상 작업 영역으로서, 데이터 Distiller 대상이 자동으로 게시되고 사용할 준비가 되었습니다.](../images/data-distiller/sql-audiences/audiences.png)

## 대상자를 대상으로 활성화 {#activate-audiences}

대상을 [!DNL Amazon S3], [!DNL SFTP] 또는 [!DNL Azure Blob]과(와) 같은 파일 기반 대상으로 타깃팅하여 활성화하십시오. 보강된 대상 속성을 필요에 따라 세분화하고 필터링할 수 있습니다.

![일괄 처리 및 스트리밍 옵션을 포함하여 공개 및 개인/사용자 지정 대상을 표시하는 Adobe Experience Platform 대상 유형의 순서도입니다.](../images/data-distiller/sql-audiences/destination-types.png)

## 기능 설명 {#faqs}

이 섹션에서는 Data Distiller에서 SQL을 사용하여 외부 대상을 만들고 관리하는 방법에 대한 FAQ를 설명합니다.

**질문**:

- 대상 생성은 플랫 데이터 세트에 대해서만 지원됩니까?

+++답변

현재 대상을 정의할 때 대상 만들기는 플랫(루트 수준) 속성으로 제한됩니다.

+++

- 대상을 만들면 단일 데이터 세트 또는 여러 데이터 세트가 발생합니까, 아니면 구성에 따라 달라집니까?

+++답변

대상과 데이터 세트 간에는 일대일 매핑이 있습니다.

+++

- 대상자 생성 중 생성된 데이터 세트가 프로필에 대해 표시됩니까?

+++답변

아니요. 대상자 생성 중에 생성된 데이터 세트는 프로필로 표시되지 않습니다.

+++

- 데이터 레이크에서 데이터 세트가 생성됩니까?

+++답변

예. 대상자와 연결된 데이터 세트는 데이터 레이크에 생성됩니다. 이 데이터 세트의 속성은 대상자 작성기 및 대상 플로우에서 보강된 속성으로 사용할 수 있습니다.

+++

- 대상의 속성이 엔터프라이즈 배치 파일 기반 대상으로 제한됩니까? (예 또는 아니요)

+++답변

아니요. 대상의 보강된 속성은 엔터프라이즈 배치 및 파일 기반 대상 모두에서 사용할 수 있습니다. &quot;다음 세그먼트 ID에는 이 대상에 대해 허용되지 않는 네임스페이스가 있습니다. e917f626-a038-42f7-944c-xyxyxix&quot;와 같은 오류가 발생하면 데이터 Distiller에서 새 세그먼트를 만들고 사용 가능한 대상에서 사용하십시오.

+++

- 데이터 Distiller 대상을 사용하는 대상의 대상을 만들 수 있습니까?

+++답변

예. 데이터 Distiller 대상을 사용하는 대상자 대상을 만들 수 있습니다.

+++

- 이러한 대상이 Adobe Journey Optimizer에 표시됩니까? 그렇지 않은 경우, 이 대상의 모든 구성원을 포함하는 새 대상을 규칙 빌더에서 만들면 어떻게 됩니까?

+++답변

Data Distiller 대상자는 Adobe Journey Optimizer에서도 사용할 수 있습니다. Adobe Journey Optimizer에서 Data Distiller 대상 을 사용하고 보강된 속성을 기준으로 결과를 필터링할 수 있습니다.

+++

- 데이터 Distiller 대상은 외부 대상이므로 30일마다 삭제됩니까?

+++답변

예. 데이터 Distiller 대상은 외부 대상이므로 30일마다 삭제됩니다.

+++

## 다음 단계

이 문서를 읽은 후에는 Data Distiller에서 SQL 대상 확장을 사용하여 SQL 명령을 사용하여 대상을 효과적으로 만들고, 관리하고, 게시하는 방법에 대해 알아보았습니다. 이제 고유한 비즈니스 요구 사항을 기반으로 대상 정의를 사용자 정의하고 다양한 대상에서 활성화하여 마케팅 전략 및 데이터 기반 결정을 최적화할 수 있습니다.

다음으로, 다음 설명서를 읽어 Experience Platform 대상자 관리 전략을 추가로 개발하고 최적화할 수 있습니다.

- **대상 평가 살펴보기**: Adobe Experience Platform의 [대상 평가 방법에 대해 알아보기](../../segmentation/home.md#evaluate-segments): 실시간 업데이트를 위한 스트리밍 세분화, 예약 또는 온디맨드 처리를 위한 일괄 세분화 및 Edge Network에서의 즉각적인 평가를 위한 에지 세분화.
- **대상과 통합**: Experience Platform 대상 UI를 사용하여 [주문형 파일을 일괄 대상으로 내보내기](../../destinations/ui/export-file-now.md)하는 방법에 대한 안내서를 읽어 보십시오.
- **대상 성능 검토**: SQL 정의 대상이 다양한 채널에서 어떻게 작동하는지 분석합니다. 데이터 인사이트를 사용하여 대상 정의 및 타깃팅 전략을 조정하고 개선합니다. [대상 인사이트](../../dashboards/insights/audiences.md)의 문서를 읽고 Adobe Real-Time CDP의 대상 인사이트에 대한 SQL 쿼리에 액세스하고 조정하는 방법을 알아보십시오. 그런 다음 대상 대시보드를 사용자 정의하여 이러한 인사이트를 효과적으로 시각화하고 사용하여 보다 나은 의사 결정을 위해 고유한 인사이트를 만들고 원시 데이터를 실행 가능한 정보로 변환할 수 있습니다.

