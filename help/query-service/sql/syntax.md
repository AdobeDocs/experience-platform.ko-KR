---
keywords: Experience Platform;home;popular topics;query service;Query service;sql syntax;sql;ctas;CTAS;Create table as select
solution: Experience Platform
title: SQL 구문
topic: syntax
description: 이 문서에서는 쿼리 서비스에서 지원하는 SQL 구문을 보여 줍니다.
translation-type: tm+mt
source-git-commit: c044194ed22b5e6fcd5e2e2102f3cd4eda45aa84
workflow-type: tm+mt
source-wordcount: '2067'
ht-degree: 1%

---


# SQL 구문

[!DNL Query Service] 은 문 및 기타 제한된 명령에 표준 ANSI SQL을 사용하는 기능을 `SELECT` 제공합니다. 이 문서에는 에서 지원하는 SQL 구문이 나와 [!DNL Query Service]있습니다.

## SELECT 쿼리 정의

다음 구문은 에서 지원하는 `SELECT` 쿼리를 정의합니다 [!DNL Query Service].

```sql
[ WITH with_query [, ...] ]
SELECT [ ALL | DISTINCT [( expression [, ...] ) ] ]
    [ * | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_element [, ...] ]
    [ HAVING condition [, ...] ]
    [ WINDOW window_name AS ( window_definition ) [, ...] ]
    [ { UNION | INTERSECT | EXCEPT | MINUS } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start ]
```

where can be one: `from_item`

```sql
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

다음 중 하나를 수행할 수 있습니다. `grouping_element`

```sql
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

과 같은 `with_query` 결과가 표시됩니다.

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE 절

SELECT 쿼리의 WHERE 절에 대/소문자를 구분하지 않고 일치시키기 위해 LIKE 대신 키 단어 ILIKE를 사용할 수 있습니다.

```sql
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE 및 ILIKE 절의 논리는 다음과 같습니다.
- ```WHERE condition LIKE pattern```, ```~~``` pattern과 같습니다.
- ```WHERE condition NOT LIKE pattern```, ```!~~``` pattern과 같습니다.
- ```WHERE condition ILIKE pattern```, 패턴 ```~~*``` 에 상응하는
- ```WHERE condition NOT ILIKE pattern```, 패턴 ```!~~*``` 에 상응하는


#### 예

```sql
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

&quot;A&quot; 또는 &quot;a&quot;에서 시작하는 이름을 가진 고객을 반환합니다.

## 연결

조인을 사용하는 `SELECT` 쿼리에는 다음 구문이 있습니다.

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## 결합, 교차 및 제외

두 개 이상의 테이블 `UNION`, `INTERSECT`및 `EXCEPT` 테이블에서 좋아요 행을 결합하거나 제외할 수 있습니다.

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 선택한 대로 표 만들기

다음 구문은 에서 지원하는 `CREATE TABLE AS SELECT` (CTAS) 쿼리를 정의합니다 [!DNL Query Service].

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false') ] AS (select_query)
```

여기서`target_schema_title` 는 XDM 스키마의 제목입니다. CTAS 쿼리를`rowvalidation` 통해 만든 새 데이터 세트에 대해 사용자가 새로 만든 데이터 세트에 대해 인제스트된 모든 새 배치의 행 수준 유효성 검사를 원하는지 여부를 지정하는 경우에만 이 절을 사용하십시오. 기본값은 &#39;true&#39;입니다.

and `select_query` `SELECT` is a statement, the syntax of is defined above in this document.


### 예

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

지정된 CTAS 쿼리에 유의하십시오.

1. 문은 `SELECT` 집계 함수 `COUNT`, `SUM`등과 같은 별칭이 `MIN`있어야 합니다.
2. 문은 괄호()와 함께 또는 없이 제공할 수 있습니다. `SELECT`

## 삽입

다음 구문은 에서 지원하는 `INSERT INTO` 쿼리를 정의합니다 [!DNL Query Service].

```sql
INSERT INTO table_name select_query
```

여기서 `select_query` 는 이 문서에 위에 정의된 `SELECT` 문입니다.

### 예

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

지정된 INSERT INTO 쿼리에 유의하십시오.

1. 문 `SELECT` 은 괄호()로 묶어서는 안 됩니다.
2. 문 결과의 스키마는 문에 정의된 테이블 `SELECT` 의 스키마를 `INSERT INTO` 따라야 합니다.

### 드롭 테이블

EXTERNAL 테이블이 아닌 경우 테이블을 삭제하고 파일 시스템에서 테이블과 연관된 디렉토리를 삭제합니다. 삭제할 테이블이 없으면 예외가 발생합니다.

```sql
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 매개 변수

- `IF EXISTS`:테이블이 없으면 아무 일도 일어나지 않습니다
- `TEMP`:임시 테이블

## 보기 만들기

다음 구문은 에서 지원하는 `CREATE VIEW` 쿼리를 정의합니다 [!DNL Query Service].

```sql
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

여기서 `view_name` 는 작성할 보기의 이름이며 이 문서 `select_query` 에서 구문이 정의된 `SELECT` 명령문입니다.

예:

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### 드롭 뷰

다음 구문은 에서 지원하는 `DROP VIEW` 쿼리를 정의합니다 [!DNL Query Service].

```sql
DROP VIEW [IF EXISTS] view_name
```

삭제할 뷰 `view_name` 의 이름은 어디입니까

예:

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## [!DNL Spark] SQL 명령

### SET

속성을 설정하거나, 기존 속성의 값을 반환하거나 모든 기존 속성을 나열합니다. 기존 속성 키에 대한 값이 제공되면 이전 값이 재정의됩니다.

```sql
SET property_key [ To | =] property_value
```

모든 설정에 대한 값을 반환하려면 을 사용합니다 `SHOW [setting name]`.

## PostgreSQL 명령

### 시작

이 명령을 구문 분석하여 완료된 명령을 클라이언트로 다시 보냅니다. 이것은 `START TRANSACTION` 명령과 동일합니다.

```sql
BEGIN [ TRANSACTION ]
```

#### 매개 변수

- `TRANSACTION`:선택적 키워드. 경청해, 아무런 조치 없이

### 닫기

`CLOSE` 열린 커서와 연관된 리소스를 비웁니다. 커서를 닫으면 후속 작업이 허용되지 않습니다. 커서가 더 이상 필요하지 않을 때는 닫혀야 한다.

```sql
CLOSE { name }
```

#### 매개 변수

- `name`:닫을 열린 커서의 이름입니다.

### 커밋

커밋 트랜잭션 문에 대한 응답으로 수행되는 작업 [!DNL Query Service] 은 없습니다.

```sql
COMMIT [ WORK | TRANSACTION ]
```

#### 매개 변수

- `WORK`
- `TRANSACTION`:선택적 키워드. 효과가 없습니다.

### 할당 취소

이전에 준비된 SQL 문 `DEALLOCATE` 을 할당 취소하는 데 사용합니다. 준비된 문을 명시적으로 할당 해제하지 않으면 세션이 종료될 때 지정 취소됩니다.

```sql
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 매개 변수

- `Prepare`:이 키워드는 무시됩니다.
- `name`:할당을 해제할 준비된 문의 이름입니다.
- `ALL`:준비된 모든 문을 할당 취소합니다.

### DECLARE

`DECLARE` 사용자는 더 큰 쿼리에서 한 번에 적은 수의 행을 검색하는 데 사용할 수 있는 커서를 만들 수 있습니다. 커서를 만든 후에는 행을 사용하여 가져옵니다 `FETCH`.

```sql
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 매개 변수

- `name`:만들 커서의 이름입니다.
- `WITH HOLD`:성공적으로 커밋된 트랜잭션 후에도 커서를 계속 사용할 수 있도록 지정합니다.
- `query`:커서로 반환할 행을 제공하는 `SELECT` 또는 `VALUES` 명령.

### 실행

`EXECUTE` 은 이전에 준비된 문을 실행하는 데 사용됩니다. 준비된 문은 세션 동안에만 존재하므로, 준비된 문은 현재 세션에서 이전에 실행된 `PREPARE` 문으로 만들어야 합니다.

문을 `PREPARE` 만든 문이 일부 매개 변수를 지정한 경우 호환되는 매개 변수 집합을 `EXECUTE` 문으로 전달해야 하며 그렇지 않으면 오류가 발생합니다. 준비된 문(함수와 달리)은 매개 변수의 유형이나 수를 기준으로 오버로드되지 않습니다. 준비된 문의 이름은 데이터베이스 세션 내에서 고유해야 합니다.

```sql
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 매개 변수

- `name`:실행할 준비된 문의 이름입니다.
- `parameter`:준비된 문에 대한 매개 변수의 실제 값. 준비된 문을 만들 때 결정된 대로 이 매개 변수의 데이터 유형과 호환되는 값을 제공하는 표현식이어야 합니다.

### 설명

이 명령은 PostgreSQL 계획자가 제공된 문에 대해 생성하는 실행 계획을 표시합니다. 실행 계획은 명령문에서 참조하는 테이블이 일반 순차적 스캔, 색인 스캔 등으로 스캔되는 방식을 보여주며, 여러 테이블이 참조되는 경우 각 입력 테이블에서 필요한 행을 가져오는 데 사용되는 조인 알고리즘을 보여줍니다.

디스플레이의 가장 중요한 부분은 예상 명세서 실행 비용이며, 이것이 명령문을 실행하는 데 걸리는 시간(임의적이지만 일반적인 평균 디스크 페이지 페치된 비용 단위로 측정됨)에 대한 계획자의 추측입니다. 실제로 두 개의 숫자가 표시됩니다.첫 번째 행을 반환하기 전의 시작 비용과 모든 행을 반환하는 총 비용. 대부분의 질의에서 총 비용은 중요한 것이지만 EXISTS의 하위 쿼리와 같은 컨텍스트에서는 계획자가 최소 총 비용 대신 가장 작은 시작 비용을 선택합니다(왜냐하면 실행자가 한 행을 가져온 후 중단되기 때문). 또한 절을 사용하여 반환할 행 수를 제한하는 경우 플래너는 종단점 비용 간의 적절한 보간을 만들어 어느 계획이 가장 저렴한지 추정합니다. `LIMIT`

이 `ANALYZE` 옵션을 사용하면 계획된 뿐 아니라 명령문이 실행됩니다. 그런 다음 각 계획 노드 내에 소요된 총 경과 시간(밀리초)과 반환된 총 행 수를 비롯하여 실제 실행 시간 통계가 디스플레이에 추가됩니다. 이는 계획가의 평가가 사실과 유사한지를 보는 데 유용합니다.

```sql
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 매개 변수

- `ANALYZE`:명령을 수행하고 실제 실행 시간과 기타 통계를 표시합니다. 이 매개 변수의 기본값은 `FALSE`입니다.
- `FORMAT`:TEXT, XML, JSON 또는 YAML일 수 있는 출력 형식을 지정합니다. 텍스트가 아닌 출력에는 텍스트 출력 형식과 동일한 정보가 포함되지만 프로그램에서 쉽게 구문 분석할 수 있습니다. 이 매개 변수의 기본값은 `TEXT`입니다.
- `statement`:당신이 보고 싶은 실행 계획 `SELECT`의 모든, `INSERT``UPDATE`, `DELETE`, `VALUES`, 또는 `EXECUTE``DECLARE``CREATE TABLE AS``CREATE MATERIALIZED VIEW AS` 진술서.

>[!IMPORTANT]
>
>옵션이 사용될 때 문이 실제로 `ANALYZE` 실행된다는 점을 명심하십시오. 반환되는 출력을 `EXPLAIN` 삭제하지만 명령문의 다른 `SELECT` 부작용은 평소대로 발생합니다.

#### 예

단일 열 및 1000개의 행이 있는 테이블에 간단한 `integer` 쿼리에 대한 계획을 표시하려면:

```sql
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### FETCH

`FETCH` 이전에 만든 커서를 사용하여 행을 검색합니다.

커서에는 연결된 위치가 있으며 이 위치는 에 의해 사용됩니다 `FETCH`. 커서 위치는 쿼리 결과의 첫 번째 행, 결과의 특정 행 또는 결과의 마지막 행 뒤에 올 수 있습니다. 만들어진 커서는 첫 번째 행 앞에 배치됩니다. 일부 행을 가져온 후 커서는 가장 최근에 검색된 행에 배치됩니다. 사용 가능한 행 끝에서 `FETCH` 실행하면 커서가 마지막 행 뒤에 남아 있습니다. 그러한 행이 없으면 빈 결과가 반환되고 첫 번째 행 앞 또는 마지막 행 뒤에 커서가 적절하게 배치됩니다.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 매개 변수

- `num_of_rows`:가져올 행 수 또는 위치의 수를 결정하는 정수 상수.
- `cursor_name`:열린 커서의 이름입니다.

### 준비

`PREPARE` 준비된 문을 만듭니다. 준비된 문은 성능을 최적화하는 데 사용할 수 있는 서버측 객체입니다. 문이 실행되면 지정된 문이 구문 분석, 분석 및 다시 작성됩니다. `PREPARE` 이후에 명령을 `EXECUTE` 실행하면 준비된 문이 계획되고 실행됩니다. 이 노무 부서는 반복 구문 분석 작업을 피하는 반면 실행 계획은 제공된 특정 매개 변수 값에 따라 달라지도록 합니다.

준비된 문은 매개 변수, 명령문을 실행할 때 명령문으로 대체되는 값을 사용할 수 있습니다. 준비된 문을 만들 때는 $1, $2 등을 사용하여 위치별 매개 변수를 참조하십시오. 매개 변수 데이터 유형의 해당 목록을 선택적으로 지정할 수 있습니다. 매개 변수의 데이터 유형이 지정되지 않았거나 알 수 없는 것으로 선언되면 가능한 경우 매개 변수가 처음 참조되는 컨텍스트에서 유형이 유추됩니다. 문을 실행할 때 문에서 이러한 매개 변수에 대한 실제 값을 `EXECUTE` 지정합니다.

준비된 문은 현재 데이터베이스 세션 동안 지속됩니다. 세션이 종료되면 준비된 문은 잊어버리므로 다시 사용하기 전에 다시 만들어야 합니다. 또한 여러 동시 데이터베이스 클라이언트에서 하나의 준비된 문을 사용할 수 없음을 의미합니다. 그러나 각 클라이언트는 자체 준비된 문을 만들어 사용할 수 있습니다. 준비된 문은 `DEALLOCATE` 명령을 사용하여 수동으로 정리할 수 있습니다.

준비된 문은 단일 세션을 사용하여 많은 유사 문을 실행하는 경우 잠재적으로 가장 큰 성능 이점을 제공합니다. 성능 차이는 쿼리가 많은 테이블의 조인을 포함하거나 여러 규칙의 적용을 필요로 하는 경우 등 명령문이 계획 또는 재작성하기가 복잡한 경우 특히 중요합니다. 이 문이 상대적으로 계획 및 재작성은 간단하지만 실행하기에 상대적으로 비싼 경우 준비된 문에 대한 성능 이점은 잘 보이지 않습니다.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 매개 변수

- `name`:이 준비된 특정 문에 지정된 임의의 이름입니다. 단일 세션 내에서 고유해야 하며 이후에 이전에 준비된 문을 실행하거나 할당을 취소하는 데 사용됩니다.
- `data-type`:준비된 문에 대한 매개 변수의 데이터 유형입니다. 특정 매개 변수의 데이터 유형이 지정되지 않았거나 알 수 없는 것으로 지정된 경우 매개 변수가 처음 참조되는 컨텍스트에서 유추됩니다. 준비된 문 자체의 매개 변수를 참조하려면 $1, $2 등을 사용합니다.


### ROLLBACK

`ROLLBACK` 현재 트랜잭션을 롤백하고 트랜잭션에서 수행한 모든 업데이트를 삭제합니다.

```sql
ROLLBACK [ WORK ]
```

#### 매개 변수

- `WORK`

### 선택

`SELECT INTO` 새 테이블을 만들고 쿼리를 통해 계산된 데이터로 채웁니다. 데이터는 일반 데이터이므로 클라이언트로 반환되지 않습니다 `SELECT`. 새 표의 열에는 해당 열의 출력 열과 연결된 이름 및 데이터 유형이 있습니다 `SELECT`.

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

#### 매개 변수

- `TEMPORARAY` 또는 `TEMP`지정한 경우 테이블이 임시 테이블로 만들어집니다.
- `UNLOGGED:` 지정된 경우 테이블이 기록되지 않은 테이블로 생성됩니다.
- `new_table` 생성할 테이블의 이름(선택적으로 스키마 적격)입니다.

#### 예

표에서 최근 항목만 `films_recent` 으로 구성된 새 표를 만듭니다 `films`.

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 표시

`SHOW` 런타임 매개 변수의 현재 설정을 표시합니다. 이러한 변수는 `SET` 명령문을 사용하여, postgresql.conf 구성 파일을 편집하거나, `PGOPTIONS` 환경 변수를 통해(libpq 또는 libpq 기반 응용 프로그램을 사용하는 경우) 또는 postgres 서버를 시작할 때 명령줄 플래그를 통해 설정할 수 있습니다.

```sql
SHOW name
```

#### 매개 변수

- `name`:
   - `SERVER_VERSION`:서버의 버전 번호를 표시합니다.
   - `SERVER_ENCODING`:서버측 문자 집합 인코딩을 표시합니다. 현재 이 매개 변수는 데이터베이스 생성 시 인코딩이 결정되므로 표시되지만 설정할 수는 없습니다.
   - `LC_COLLATE`:데이터 정렬(텍스트 순서)에 대한 데이터베이스의 로케일 설정을 표시합니다. 현재 이 매개 변수는 데이터베이스 생성 시간에 설정되므로 표시할 수 있지만 설정할 수는 없습니다.
   - `LC_CTYPE`:문자 분류에 대한 데이터베이스의 로케일 설정을 표시합니다. 현재 이 매개 변수는 데이터베이스 생성 시간에 설정되므로 표시할 수 있지만 설정할 수는 없습니다.
      `IS_SUPERUSER`:현재 역할에 수퍼유저 권한이 있는 경우 True입니다.
- `ALL`:모든 구성 매개 변수의 값을 설명과 함께 표시합니다.

#### 예

매개 변수의 현재 설정 표시 `DateStyle`

```sql
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 트랜잭션 시작

이 명령은 구문 분석하여 완료된 명령을 다시 클라이언트로 전송합니다. 이것은 `BEGIN` 명령과 동일합니다.

```sql
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```

### 복사

이 명령은 SELECT 쿼리의 출력을 지정된 위치에 덤프합니다. 이 명령이 성공하려면 사용자가 이 위치에 액세스할 수 있어야 합니다.

```sql
COPY  query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']

where 'format_name' is be one of:
    'parquet', 'csv', 'json'

'parquet' is the default format.
```

>[!NOTE]
>
>전체 출력 경로가 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`


### ALTER

이 명령은 테이블에 기본 또는 외래 키 제약 조건을 추가하거나 삭제하는 데 도움이 됩니다.

```sql
Alter TABLE table_name ADD ( column_name Primary key Namespace 'namespace')

Alter TABLE table_name ADD ( column_name Foreign key references referenced_table_name Namespace 'namespace')

Alter TABLE table_name DROP ( column_name Primary key)

Alter TABLE table_name DROP ( column_name Foreign key)
```

>[!NOTE]
>테이블 스키마는 고유해야 하며 여러 테이블 간에 공유되어서는 안 됩니다. 또한 네임스페이스는 필수입니다.


### 기본 키 표시

이 명령은 지정된 데이터베이스에 대한 모든 기본 키 제약 조건을 나열합니다.

```sql
SHOW PRIMARY KEYS
    tableName | columnName    | datatype | namespace
------------------+----------------------+----------+-----------
 table_name_1 | column_name1  | text     | "ECID"
 table_name_2 | column_name2  | text     | "AAID"
```


### 외래 키 표시

이 명령은 지정된 데이터베이스에 대한 모든 외래 키 제약 조건을 나열합니다.

```sql
SHOW FOREIGN KEYS
    tableName   |     columnName      | datatype | referencedTableName | referencedColumnName | namespace 
------------------+---------------------+----------+---------------------+----------------------+-----------
 table_name_1   | column_name1        | text     | table_name_3        | column_name3         |  "ECID"
 table_name_2   | column_name2        | text     | table_name_4        | column_name4         |  "AAID"
```
