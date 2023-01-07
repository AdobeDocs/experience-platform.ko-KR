---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;sql 구문;sql;ctas;CTAS;선택할 대로 테이블 만들기
solution: Experience Platform
title: 쿼리 서비스의 SQL 구문
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 지원하는 SQL 구문을 보여줍니다.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 2%

---

# 쿼리 서비스의 SQL 구문

Adobe Experience Platform Query Service에서는 표준 ANSI SQL을 `SELECT` 문 및 기타 제한된 명령. 이 문서에서는 [!DNL Query Service].

## 쿼리 선택 {#select-queries}

다음 구문은 `SELECT` 에서 지원하는 쿼리 [!DNL Query Service]:

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

여기서 `from_item` 다음 옵션 중 하나일 수 있습니다.

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
[ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
```

```sql
with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
```

```sql
from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

및 `grouping_element` 다음 옵션 중 하나일 수 있습니다.

```sql
( )
```

```sql
expression
```

```sql
( expression [, ...] )
```

```sql
ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
CUBE ( { expression | ( expression [, ...] ) } [, ...] )
```

```sql
GROUPING SETS ( grouping_element [, ...] )
```

및 `with_query` is:

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

다음 하위 섹션에서는 위에 요약된 형식을 따를 경우 질의에서 사용할 수 있는 추가 조문에 대한 세부 정보를 제공합니다.

### SNAPSHOT 절

이 절은 스냅샷 ID를 기반으로 테이블의 데이터를 점진적으로 읽는 데 사용할 수 있습니다. 스냅샷 ID는 데이터가 기록될 때마다 데이터 레이크 테이블에 적용되는 긴 형식의 숫자로 표시되는 체크포인트 마커입니다. 다음 `SNAPSHOT` 절은 그 옆에 사용되는 테이블 관계에 첨부됩니다.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 예

```sql
SELECT * FROM Customers SNAPSHOT SINCE 123;

SELECT * FROM Customers SNAPSHOT AS OF 345;

SELECT * FROM Customers SNAPSHOT BETWEEN 123 AND 345;

SELECT * FROM Customers SNAPSHOT BETWEEN HEAD AND 123;

SELECT * FROM Customers SNAPSHOT BETWEEN 345 AND TAIL;

SELECT * FROM (SELECT id FROM CUSTOMERS BETWEEN 123 AND 345) C 

SELECT * FROM Customers SNAPSHOT SINCE 123 INNER JOIN Inventory AS OF 789 ON Customers.id = Inventory.id;
```

다음 사항에 주의하십시오. `SNAPSHOT` 절은 테이블 또는 테이블 별칭과 함께 작동하지만 하위 쿼리 또는 뷰의 맨 위에는 작동하지 않습니다. A `SNAPSHOT` 조항은 어느 곳에서나 작동합니다 `SELECT` 테이블의 쿼리를 적용할 수 있습니다.

또한 `HEAD` 및 `TAIL` 스냅샷 절에 대한 특수 오프셋 값으로 사용됩니다. 사용 `HEAD` 는 첫 번째 스냅샷 앞의 오프셋을 참조하고 `TAIL` 는 마지막 스냅샷 이후의 오프셋을 나타냅니다.

>[!NOTE]
>
>두 스냅샷 ID와 시작 스냅샷 간에 쿼리하는 경우, 선택적 대체 동작 플래그(`resolve_fallback_snapshot_on_failure`)가 설정되어 있습니다.
>
>- 옵션 대체 동작 플래그가 설정되어 있으면 Query Service에서 사용 가능한 가장 빠른 스냅샷을 선택하고 시작 스냅샷으로 설정한 다음 사용 가능한 가장 이른 스냅샷과 지정된 종료 스냅샷 사이에 데이터를 반환합니다. 이 데이터는 **포함** 사용 가능한 가장 이른 스냅샷의
>
>- 옵션 대체 동작 플래그가 설정되지 않으면 오류가 반환됩니다.


### WHERE 절

기본적으로 은 `WHERE` 에 대한 조항 `SELECT` 쿼리는 대/소문자를 구분합니다. 일치 항목을 대/소문자를 구분하지 않게 하려면 키워드를 사용할 수 있습니다 `ILIKE` 대신 `LIKE`.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE 및 ILIKE 절의 논리는 다음 표에 설명되어 있습니다.

| 절 | 연산자 |
| ------ | -------- |
| `WHERE condition LIKE pattern` | `~~` |
| `WHERE condition NOT LIKE pattern` | `!~~` |
| `WHERE condition ILIKE pattern` | `~~*` |
| `WHERE condition NOT ILIKE pattern` | `!~~*` |

**예**

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

이 쿼리는 &quot;A&quot; 또는 &quot;a&quot;에서 시작하는 이름을 사용하는 고객을 반환합니다.

### 가입

A `SELECT` 조인을 사용하는 쿼리에는 다음 구문이 있습니다.

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 결합, 교차 및 제외

다음 `UNION`, `INTERSECT`, 및 `EXCEPT` 절은 두 개 이상의 테이블에서 유사 행을 결합하거나 제외하는 데 사용됩니다.

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 선택할 때 테이블 만들기

다음 구문은 `CREATE TABLE AS SELECT` (CTAS) 쿼리:

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

| 매개 변수 | 설명 |
| ----- | ----- |
| `schema` | XDM 스키마의 제목입니다. CTAS 쿼리에서 만든 새 데이터 세트에 기존 XDM 스키마를 사용하려는 경우에만 이 절을 사용합니다. |
| `rowvalidation` | (선택 사항) 새로 생성된 데이터 세트에 대해 수집된 모든 새 배치의 행 수준 유효성 검사를 사용자가 원하는지 여부를 지정합니다. 기본값은 `true`입니다. |
| `select_query` | A `SELECT` 문. 의 구문 `SELECT` 쿼리는 [쿼리 섹션 선택](#select-queries). |

**예**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>다음 `SELECT` 문에는 다음과 같은 집계 함수에 대한 별칭이 있어야 합니다. `COUNT`, `SUM`, `MIN`등 또한 `SELECT` 문은 괄호를 사용하거나 사용하지 않고 제공할 수 있습니다(). 다음을 제공할 수 있습니다 `SNAPSHOT` 대상 테이블에 증분 델타를 읽는 절

## 삽입 위치

다음 `INSERT INTO` 명령은 다음과 같이 정의됩니다.

```sql
INSERT INTO table_name select_query
```

| 매개 변수 | 설명 |
| ----- | ----- |
| `table_name` | 쿼리를 삽입할 테이블의 이름입니다. |
| `select_query` | A `SELECT` 문. 의 구문 `SELECT` 쿼리는 [쿼리 섹션 선택](#select-queries). |

**예**

>[!NOTE]
>
>다음은 강의용으로 작성된 예입니다.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
> 다음 `SELECT` statement **필수가 아니어야 합니다.** 괄호로 묶습니다(). 또한 `SELECT` 문은 `INSERT INTO` 문. 다음을 제공할 수 있습니다 `SNAPSHOT` 대상 테이블에 증분 델타를 읽는 절

실제 XDM 스키마의 대부분의 필드는 루트 수준에서 찾을 수 없으며 SQL에서는 점 표기법을 사용할 수 없습니다. 중첩된 필드를 사용하여 사실적인 결과를 얻으려면 `INSERT INTO` 경로.

종료 `INSERT INTO` 중첩된 경로는 다음 구문을 사용합니다.

```sql
INSERT INTO [dataset]
SELECT struct([source field1] as [target field in schema],
[source field2] as [target field in schema],
[source field3] as [target field in schema]) [tenant name]
FROM [dataset]
```

**예**

```sql
INSERT INTO Customers SELECT struct(SupplierName as Supplier, City as SupplierCity, Country as SupplierCountry) _Adobe FROM OnlineCustomers;
```

## 테이블 놓기

다음 `DROP TABLE` 명령은 기존 테이블을 삭제하고 외부 테이블이 아닌 경우 파일 시스템에서 테이블과 연관된 디렉토리를 삭제합니다. 테이블이 없으면 예외가 발생합니다.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 값을 지정하면 테이블이 지정된 경우 예외가 throw되지 않습니다 **not** 존재 |

## 데이터베이스 만들기

다음 `CREATE DATABASE` 명령은 ADLS 데이터베이스를 만듭니다.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 데이터베이스 삭제

다음 `DROP DATABASE` 명령은 인스턴스에서 데이터베이스를 삭제합니다.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 값을 지정하면 데이터베이스가 지정하는 경우 예외가 발생하지 않습니다 **not** 존재 |

## 스키마 삭제

다음 `DROP SCHEMA` 명령은 기존 스키마를 삭제합니다.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 값을 지정하면 스키마에 예외가 throw되지 않습니다 **not** 존재 |
| `RESTRICT` | 모드에 대한 기본값입니다. 이 값을 지정하면 스키마가 지정된 경우에만 삭제됩니다 **does not** 표를 모두 포함합니다. |
| `CASCADE` | 이 값을 지정하면 스키마에 있는 모든 테이블과 함께 스키마가 삭제됩니다. |

## 보기 만들기

다음 구문은 `CREATE VIEW` 쿼리:

```sql
CREATE VIEW view_name AS select_query
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `view_name` | 만들 보기의 이름입니다. |
| `select_query` | A `SELECT` 문. 의 구문 `SELECT` 쿼리는 [쿼리 섹션 선택](#select-queries). |

**예**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

## 보기 삭제

다음 구문은 `DROP VIEW` 쿼리:

```sql
DROP VIEW [IF EXISTS] view_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 값이 지정된 경우 보기가 실행되는 경우 예외가 발생하지 않습니다 **not** 존재 |
| `view_name` | 삭제할 보기의 이름입니다. |

**예**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 익명 블록

익명 블록은 다음 두 섹션으로 구성됩니다. 실행 파일 및 예외 처리 섹션. 익명 블록에서는 실행 가능한 섹션이 필수입니다. 그러나 예외 처리 섹션은 선택 사항입니다.

다음 예에서는 함께 실행할 하나 이상의 구문을 사용하여 블록을 만드는 방법을 보여 줍니다.

```sql
BEGIN
  statementList
[EXCEPTION exceptionHandler]
END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

다음은 익명 블록을 사용하는 예입니다.

```sql
BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
END;
```

## 데이터 자산 조직

Adobe Experience Platform 데이터 레이크 내에서 데이터가 증가할 때 데이터 자산을 논리적으로 구성하는 것이 중요합니다. Query Service는 샌드박스 내의 데이터 자산을 논리적으로 그룹화할 수 있는 SQL 구문을 확장합니다. 이 조직 방법을 사용하면 물리적으로 이동할 필요 없이 스키마 간에 데이터 자산을 공유할 수 있습니다.

데이터를 논리적으로 구성할 수 있도록 표준 SQL 구문을 사용하는 다음 SQL 구문이 지원됩니다.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

다음 안내서를 참조하십시오. [데이터 자산의 논리 조직](../best-practices/organize-data-assets.md) 쿼리 서비스 모범 사례에 대한 자세한 설명을 참조하십시오.

## 테이블이 존재함

다음 `table_exists` SQL 명령은 현재 시스템에 테이블이 있는지 여부를 확인하는 데 사용됩니다. 이 명령은 부울 값을 반환합니다. `true` 만약 **does** 존재 및 `false` 테이블에서 **not** 존재

문을 실행하기 전에 테이블이 있는지 확인하여 `table_exists` 이 기능은 익명 블록을 작성하여 두 요소를 모두 포함하는 과정을 간소화합니다 `CREATE` 및 `INSERT INTO` 사용 사례

다음 구문은 `table_exists` 명령:

```SQL
$$
BEGIN

#Set mytableexist to true if the table already exists.
SET @mytableexist = SELECT table_exists('target_table_name');

#Create the table if it does not already exist (this is a one time operation).
CREATE TABLE IF NOT EXISTS target_table_name AS
  SELECT *
  FROM   profile_dim_date limit 10;

#Insert data only if the table already exists. Check if @mytableexist = 'true'
 INSERT INTO target_table_name           (
                     select *
                     from   profile_dim_date
                     WHERE  @mytableexist = 'true' limit 20
              ) ;
EXCEPTION
WHEN other THEN SELECT 'ERROR';

END $$; 
```

## 인라인 {#inline}

다음 `inline` 함수는 구조체 배열의 요소를 분리하고 값을 표로 생성합니다. 이 ID는 `SELECT` 목록 또는 `LATERAL VIEW`.

다음 `inline` 함수 **사용할 수 없음** 다른 생성기 기능이 있는 선택 목록에 배치됩니다.

기본적으로 생성되는 열의 이름은 &quot;col1&quot;, &quot;col2&quot; 등입니다. 표현식이 `NULL` 그러면 행이 생성되지 않습니다.

>[!TIP]
>
>열 이름은 `RENAME` 명령.

**예**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

이 예는 다음을 반환합니다.

```text
1  a Spark SQL
2  b Spark SQL
```

이 두 번째 예는 의 개념 및 적용을 더 보여줍니다 `inline` 함수 위에 있어야 합니다. 이 예제의 데이터 모델은 아래 이미지에 표시되어 있습니다.

![productListItems에 대한 스키마 다이어그램입니다.](../images/sql/productListItems.png)

**예**

```sql
select inline(productListItems) from source_dataset limit 10;
```

에서 가져온 값 `source_dataset` 대상 테이블을 채우는 데 사용됩니다.

| SKU | _경험 | 수량 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;)&quot;) | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;)&quot;) |  |  |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;)&quot;) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;)&quot;) | 3 | 12 |

## [!DNL Spark] SQL 명령

아래 하위 섹션에서는 Query Service에서 지원하는 Spark SQL 명령을 다룹니다.

### 설정

다음 `SET` 명령은 속성을 설정하고 기존 속성의 값을 반환하거나 기존 속성을 모두 나열합니다. 기존 속성 키에 값이 제공되면 이전 값이 재정의됩니다.

```sql
SET property_key = property_value
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `property_key` | 나열하거나 변경할 속성의 이름입니다. |
| `property_value` | 속성을 로 설정할 값입니다. |

설정에 대한 값을 반환하려면 `SET [property key]` 없이 `property_value`.

## [!DNL PostgreSQL] 명령

아래의 하위 섹션은 [!DNL PostgreSQL] 쿼리 서비스에서 지원하는 명령

### 테이블 분석

다음 `ANALYZE TABLE` 명령은 가속 저장소의 테이블에 대한 통계를 계산합니다. 통계는 가속화된 저장소의 지정된 테이블에 대해 실행된 CTAS 또는 ITAS 쿼리에서 계산됩니다.

**예**

```sql
ANALYZE TABLE <original_table_name>
```

다음은 를 사용한 후에 사용할 수 있는 통계 계산 목록입니다 `ANALYZE TABLE` 명령:-

| 계산된 값 | 설명 |
|---|---|
| `field` | 테이블에 있는 열의 이름입니다. |
| `data-type` | 각 열에 대해 허용되는 데이터 유형입니다. |
| `count` | 이 필드에 대해 null이 아닌 값을 포함하는 행 수입니다. |
| `distinct-count` | 이 필드에 대한 고유한 또는 개별 값의 수입니다. |
| `missing` | 이 필드에 대해 null 값이 있는 행 수입니다. |
| `max` | 분석된 테이블의 최대값입니다. |
| `min` | 분석된 테이블의 최소값입니다. |
| `mean` | 분석된 테이블의 평균 값입니다. |
| `stdev` | 분석된 테이블의 표준 편차. |

### 시작

다음 `BEGIN` 명령 또는 또는 `BEGIN WORK` 또는 `BEGIN TRANSACTION` 트랜잭션 블록을 시작합니다. begin 명령 후에 입력된 모든 문은 명시적 COMMIT 또는 ROLLBACK 명령이 제공될 때까지 단일 트랜잭션에서 실행됩니다. 이 명령은 다음과 같습니다 `START TRANSACTION`.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 닫기

다음 `CLOSE` 명령은 열려 있는 커서와 연결된 리소스를 해제합니다. 커서를 닫으면 후속 작업이 허용되지 않습니다. 커서가 더 이상 필요하지 않으면 닫아야 합니다.

```sql
CLOSE name
CLOSE ALL
```

If `CLOSE name` 이 사용됩니다. `name` 닫아야 하는 열린 커서의 이름을 나타냅니다. If `CLOSE ALL` 를 사용하면 열려 있는 모든 커서가 닫힙니다.

### 할당 취소

다음 `DEALLOCATE` 명령을 사용하면 이전에 준비한 SQL 문을 할당 취소할 수 있습니다. 준비된 문을 명시적으로 할당 취소하지 않으면 세션이 종료될 때 이 명령문은 할당 취소됩니다. 준비된 문에 대한 자세한 내용은 [PREPARE 명령](#prepare) 섹션을 참조하십시오.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

If `DEALLOCATE name` 이 사용됩니다. `name` 할당 취소해야 하는 준비된 문의 이름을 나타냅니다. If `DEALLOCATE ALL` 이(가) 사용되면, 준비된 모든 명령문은 할당이 취소됩니다.

### 선언

다음 `DECLARE` 명령을 사용하면 커서를 만들 수 있으며 커서는 큰 쿼리에서 적은 수의 행을 검색하는 데 사용할 수 있습니다. 커서를 만들면 `FETCH`.

```sql
DECLARE name CURSOR FOR query
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 만들 커서의 이름입니다. |
| `query` | A `SELECT` 또는 `VALUES` 커서에서 반환할 행을 제공하는 명령입니다. |

### 실행

다음 `EXECUTE` 명령은 이전에 준비한 문을 실행하는 데 사용됩니다. 준비된 문은 세션 기간 동안에만 존재하므로 준비된 문은 `PREPARE` 현재 세션에서 이전에 실행된 문입니다. 준비된 문을 사용하는 방법에 대한 자세한 내용은 [`PREPARE` 명령](#prepare) 섹션을 참조하십시오.

만약 `PREPARE` 일부 매개 변수를 지정한 문을 만든 명령문이므로 호환되는 매개 변수 집합을 `EXECUTE` 문. 이러한 매개 변수가 전달되지 않으면 오류가 발생합니다.

```sql
EXECUTE name [ ( parameter ) ]
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 실행할 준비된 문의 이름입니다. |
| `parameter` | 준비된 문에 대한 매개 변수의 실제 값입니다. 준비된 문을 만들 때 결정된 대로 이 매개 변수의 데이터 유형과 호환되는 값을 가져오는 표현식이어야 합니다.  준비된 문에 대해 여러 매개 변수가 있는 경우 쉼표로 구분됩니다. |

### 설명

다음 `EXPLAIN` 명령에는 제공된 문에 대한 실행 계획이 표시됩니다. 실행 계획에는 문에서 참조하는 테이블을 스캔하는 방법이 표시됩니다.  여러 테이블을 참조하면 각 입력 테이블에서 필요한 행을 함께 가져오는 데 사용되는 조인 알고리즘이 표시됩니다.

```sql
EXPLAIN statement
```

를 사용하십시오 `FORMAT` 키워드 `EXPLAIN` 명령의 형식을 정의합니다.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `FORMAT` | 를 사용하십시오 `FORMAT` 출력 형식을 지정하는 명령 사용 가능한 옵션은 다음과 같습니다 `TEXT` 또는 `JSON`. 텍스트가 아닌 출력에는 텍스트 출력 형식과 동일한 정보가 포함되어 있지만 프로그램이 구문 분석하기 쉽습니다. 이 매개 변수의 기본값은 입니다. `TEXT`. |
| `statement` | 임의 `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS`, 또는 `CREATE MATERIALIZED VIEW AS` 표시할 실행 계획 |

>[!IMPORTANT]
>
>모든 출력은 `SELECT` 문은 `EXPLAIN` 키워드. 그 진술의 다른 부작용들은 평상시처럼 발생한다.

**예**

다음 예는 단일 테이블의 단순 쿼리에 대한 계획을 보여줍니다 `integer` 열 및 10000 행:

```sql
EXPLAIN SELECT * FROM foo;
```

```console
                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo (dataSetId = "6307eb92f90c501e072f8457", dataSetName = "foo") [0,1000000242,6973776840203d3d,6e616c58206c6153,6c6c6f430a3d4d20,74696d674c746365]
(1 row)
```

### 가져오기

다음 `FETCH` 명령은 이전에 만든 커서를 사용하여 행을 검색합니다.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `num_of_rows` | 가져올 행 수입니다. |
| `cursor_name` | 정보를 검색할 커서의 이름입니다. |

### 준비 {#prepare}

다음 `PREPARE` 명령을 사용하면 준비된 문을 만들 수 있습니다. 준비된 문은 유사한 SQL 문을 템플릿 지정하는 데 사용할 수 있는 서버측 객체입니다.

준비된 문은 매개 변수를 사용할 수 있습니다. 이 매개 변수는 명령문이 실행될 때 명령문에 대체되는 값입니다. 매개 변수는 준비된 문을 사용할 때 $1, $2 등을 사용하여 position별로 참조됩니다.

매개변수 데이터 유형 목록을 지정할 수도 있습니다. 매개 변수의 데이터 유형이 나열되지 않으면 컨텍스트에서 유형을 유추할 수 있습니다.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 준비된 문의 이름입니다. |
| `data_type` | 준비된 문의 매개 변수의 데이터 유형입니다. 매개 변수의 데이터 유형이 나열되지 않으면 컨텍스트에서 유형을 유추할 수 있습니다. 여러 데이터 유형을 추가해야 하는 경우 쉼표로 구분된 목록에 추가할 수 있습니다. |

### 롤백

다음 `ROLLBACK` 명령은 현재 트랜잭션을 해제하고 트랜잭션에서 수행한 모든 업데이트를 삭제합니다.

```sql
ROLLBACK
ROLLBACK WORK
```

### 다음으로 선택

다음 `SELECT INTO` 새 테이블을 만들고 쿼리로 계산된 데이터로 채웁니다. 데이터는 일반적이므로 클라이언트에 반환되지 않습니다 `SELECT` 명령. 새 테이블의 열에는 `SELECT` 명령.

```sql
[ WITH [ RECURSIVE ] with_query [, ...] ]
SELECT [ ALL | DISTINCT [ ON ( expression [, ...] ) ] ]
    * | expression [ [ AS ] output_name ] [, ...]
    INTO [ TEMPORARY | TEMP | UNLOGGED ] [ TABLE ] new_table
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY expression [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
    [ FETCH { FIRST | NEXT } [ count ] { ROW | ROWS } ONLY ]
    [ FOR { UPDATE | SHARE } [ OF table_name [, ...] ] [ NOWAIT ] [...] ]
```

표준 SELECT 쿼리 매개 변수에 대한 자세한 내용은 [쿼리 섹션 선택](#select-queries). 이 섹션에는 `SELECT INTO` 명령.

| 매개 변수 | 설명 |
| ------ | ------ |
| `TEMPORARY` 또는 `TEMP` | 선택적 매개 변수입니다. 지정하면 생성된 테이블이 임시 테이블이 됩니다. |
| `UNLOGGED` | 선택적 매개 변수입니다. 지정되면 로 만들어지는 테이블은 기록되지 않은 테이블입니다. 기록되지 않은 테이블에 대한 자세한 내용은 [[!DNL PostgreSQL] 설명서](https://www.postgresql.org/docs/current/sql-createtable.html). |
| `new_table` | 만들 테이블의 이름입니다. |

**예**

다음 쿼리는 새 테이블을 만듭니다 `films_recent` 테이블의 최근 항목만 포함하는 `films`:

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 표시

다음 `SHOW` 명령은 런타임 매개 변수의 현재 설정을 표시합니다. 이러한 변수는 `SET` 문, 편집 `postgresql.conf` 구성 파일, `PGOPTIONS` Postgres 서버를 시작할 때 환경 변수(libpq 또는 libpq 기반 응용 프로그램을 사용하는 경우) 또는 명령줄 플래그를 통해 환경 변수를 사용할 수 있습니다.

```sql
SHOW name
SHOW ALL
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 정보를 지정할 런타임 매개 변수의 이름입니다. 런타임 매개 변수에 사용할 수 있는 값에는 다음 값이 포함됩니다.<br>`SERVER_VERSION`: 이 매개 변수는 서버의 버전 번호를 보여줍니다.<br>`SERVER_ENCODING`: 이 매개 변수는 서버측 문자 집합 인코딩을 보여줍니다.<br>`LC_COLLATE`: 이 매개 변수는 데이터 정렬(텍스트 순서)에 대한 데이터베이스의 로케일 설정을 보여 줍니다.<br>`LC_CTYPE`: 이 매개 변수는 문자 분류에 대한 데이터베이스의 로케일 설정을 보여 줍니다.<br>`IS_SUPERUSER`: 이 매개 변수는 현재 역할에 수퍼유저 권한이 있는지 여부를 표시합니다. |
| `ALL` | 설명이 있는 모든 구성 매개 변수의 값을 표시합니다. |

**예**

다음 쿼리는 매개 변수의 현재 설정을 보여 줍니다 `DateStyle`.

```sql
SHOW DateStyle;
```

```console
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 복사

다음 `COPY` 명령은 `SELECT` 쿼리를 지정한 위치에 쿼리합니다. 이 명령을 성공하려면 이 위치에 액세스할 수 있어야 합니다.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `query` | 복사할 쿼리 |
| `format_name` | 쿼리를 복사할 형식입니다. 다음 `format_name` 다음 중 하나일 수 있습니다. `parquet`, `csv`, 또는 `json`. 기본적으로 값은 입니다 `parquet`. |

>[!NOTE]
>
>전체 출력 경로가 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`

### ALTER TABLE {#alter-table}

다음 `ALTER TABLE` 명령을 사용하면 기본 또는 외래 키 제약 조건을 추가하거나 삭제하고 테이블에 열을 추가할 수 있습니다.


#### 제약 조건 추가 또는 삭제

다음 SQL 쿼리는 테이블에 제약 조건을 추가하거나 삭제하는 예를 보여줍니다.

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY IDENTITY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT IDENTITY ( column_name )
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `table_name` | 편집 중인 테이블의 이름입니다. |
| `column_name` | 제약 조건을 추가할 열의 이름입니다. |
| `referenced_table_name` | 외래 키가 참조하는 테이블의 이름입니다. |
| `primary_column_name` | 외래 키가 참조하는 열의 이름입니다. |


>[!NOTE]
>
>테이블 스키마는 고유해야 하며 여러 테이블 간에 공유되지 않아야 합니다. 또한 네임스페이스는 기본 키, 기본 ID 및 ID 제한에 필수입니다.

#### 기본 및 보조 ID 추가 또는 삭제

다음 `ALTER TABLE` 명령을 사용하면 SQL을 통해 직접 주 ID 테이블 열과 보조 ID 테이블 열 모두에 대한 제약 조건을 추가하거나 삭제할 수 있습니다.

다음 예에서는 제한을 추가하여 기본 ID와 보조 ID를 추가합니다.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

아래 예와 같이 제약 조건을 드롭하여 ID를 제거할 수도 있습니다.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

다음 문서를 참조하십시오. [ad hoc 데이터 세트에서 ID 설정](../data-governance/ad-hoc-schema-identities.md) 를 참조하십시오.

#### 열 추가

다음 SQL 쿼리는 테이블에 열을 추가하는 예를 보여줍니다.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### 지원되는 데이터 유형

다음 표에는 [!DNL Postgres SQL], XDM 및 [!DNL Accelerated Database Recovery] Azure SQL의 (ADR)입니다.

| — | PSQL 클라이언트 | XDM | ADR. | 설명 |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | -9,223,372,036,854,775,807부터 9,223,372,036,854,775,807까지의 큰 정수를 저장하는 데 사용되는 숫자 데이터 형식입니다. |
| 2 | `integer` | `int4` | `integer` | -2,147,483,648부터 2,147,483,647까지의 정수를 4바이트로 저장하는 데 사용되는 숫자 데이터 유형입니다. |
| 3 | `smallint` | `int2` | `smallint` | -32,768부터 215-1까지의 정수를 2바이트로 저장하는 데 사용되는 숫자 데이터 형식입니다. |
| 4 | `tinyint` | `int1` | `tinyint` | 0부터 255까지의 정수를 1바이트로 저장하는 데 사용되는 숫자 데이터 유형입니다. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | 변수 크기의 문자 데이터 유형입니다. `varchar` 열 데이터 항목의 크기가 상당히 다를 때 가장 잘 사용됩니다. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` 및 `FLOAT` 에 대한 유효한 동의어입니다. `DOUBLE PRECISION`. `double precision` 는 부동 소수점 데이터 유형입니다. 부동 소수점 값은 8바이트로 저장됩니다. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8` 의 유효한 동의어입니다. `double precision`.`double precision` 는 부동 소수점 데이터 유형입니다. 부동 소수점 값은 8바이트로 저장됩니다. |
| 8 | `date` | `date` | `date` | 다음 `date` 데이터 유형은 타임스탬프 정보가 없는 4바이트 저장된 달력 날짜 값입니다. 유효한 날짜 범위는 01-01-0001부터 12-31-9999까지입니다. |
| 9 | `datetime` | `datetime` | `datetime` | 달력 날짜 및 시간으로 표현되는 시간에 인스턴스를 저장하는 데 사용되는 데이터 유형입니다. `datetime` 에는 다음 큐레이터가 포함됩니다. 연도, 월, 일, 시간, 두 번째 및 분수입니다. A `datetime` 선언에는 해당 시퀀스에서 결합되는 이러한 시간 단위의 하위 집합이 포함될 수 있고 심지어 하나의 시간 단위만 포함할 수 있습니다. |
| 10 | `char(len)` | `string` | `char(len)` | 다음 `char(len)` 키워드는 항목이 고정 길이 문자임을 나타내는 데 사용됩니다. |

#### 스키마 추가

다음 SQL 쿼리는 데이터베이스/스키마에 테이블을 추가하는 예를 보여줍니다.

```sql
ALTER TABLE table_name ADD SCHEMA database_name.schema_name
```

>[!NOTE]
>
> ADLS 테이블 및 뷰를 DWH 데이터베이스/스키마에 추가할 수 없습니다.


#### 스키마 제거

다음 SQL 쿼리는 데이터베이스/스키마에서 테이블을 제거하는 예를 보여 줍니다.

```sql
ALTER TABLE table_name REMOVE SCHEMA database_name.schema_name
```

>[!NOTE]
>
> 물리적으로 연결된 DWH 데이터베이스/스키마에서 DWH 테이블 및 뷰를 제거할 수 없습니다.


**매개 변수**

| 매개 변수 | 설명 |
| ------ | ------ |
| `table_name` | 편집 중인 테이블의 이름입니다. |
| `column_name` | 추가할 열의 이름입니다. |
| `data_type` | 추가할 열의 데이터 유형입니다. 지원되는 데이터 유형에는 다음이 포함됩니다. bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar. |

### 기본 키 표시

다음 `SHOW PRIMARY KEYS` 명령은 지정된 데이터베이스에 대한 모든 기본 키 제약 조건을 나열합니다.

```sql
SHOW PRIMARY KEYS
```

```console
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```

### 외래 키 표시

다음 `SHOW FOREIGN KEYS` 명령은 지정된 데이터베이스에 대한 모든 외래 키 제약 조건을 나열합니다.

```sql
SHOW FOREIGN KEYS
```

```console
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```


### 데이터 그룹 표시

다음 `SHOW DATAGROUPS` 명령은 연결된 모든 데이터베이스의 테이블을 반환합니다. 각 데이터베이스에 대해 테이블에는 스키마, 그룹 유형, 하위 유형, 하위 이름 및 하위 ID가 포함됩니다.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Data Warehouse Table | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### 테이블에 대한 데이터 그룹 표시

다음 `SHOW DATAGROUPS FOR` &#39;table_name&#39; 명령은 매개 변수를 자식으로 포함하는 연결된 모든 데이터베이스의 테이블을 반환합니다. 각 데이터베이스에 대해 테이블에는 스키마, 그룹 유형, 하위 유형, 하위 이름 및 하위 ID가 포함됩니다.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**매개 변수**

- `table_name`: 연관된 데이터베이스를 찾을 테이블의 이름입니다.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Data Warehouse Table | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
