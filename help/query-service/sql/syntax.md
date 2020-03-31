---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: SQL 구문
topic: syntax
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce

---


# SQL 구문

쿼리 서비스는 `SELECT` 문 및 기타 제한된 명령에 표준 ANSI SQL을 사용하는 기능을 제공합니다. 이 문서에서는 쿼리 서비스에서 지원하는 SQL 구문을 보여 줍니다.

## SELECT 쿼리 정의

다음 구문은 쿼리 서비스에서 지원하는 `SELECT` 쿼리를 정의합니다.

```
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

```
table_name [ * ] [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    [ LATERAL ] ( select ) [ AS ] alias [ ( column_alias [, ...] ) ]
    with_query_name [ [ AS ] alias [ ( column_alias [, ...] ) ] ]
    from_item [ NATURAL ] join_type from_item [ ON join_condition | USING ( join_column [, ...] ) ]
```

다음 중 하나가 될 수 있습니다. `grouping_element`

```
( )
    expression
    ( expression [, ...] )
    ROLLUP ( { expression | ( expression [, ...] ) } [, ...] )
    CUBE ( { expression | ( expression [, ...] ) } [, ...] )
    GROUPING SETS ( grouping_element [, ...] )
```

과 `with_query` 는 다음과 같습니다.

```
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
 
TABLE [ ONLY ] table_name [ * ]
```

### WHERE ILIKE 절

LIKE 대신 ILIKE 키 단어를 사용하여 SELECT 쿼리의 WHERE 절에 대/소문자를 구분하지 않고 일치시킬 수 있습니다.

```
    [ WHERE condition { LIKE | ILIKE | NOT LIKE | NOT ILIKE } pattern ]
```

LIKE 및 ILIKE 절의 논리는 다음과 같습니다.
- ```WHERE condition LIKE pattern```, ```~~``` 은 pattern과 같습니다.
- ```WHERE condition NOT LIKE pattern```, ```!~~``` 은 pattern과 같습니다.
- ```WHERE condition ILIKE pattern```, ```~~*``` pattern
- ```WHERE condition NOT ILIKE pattern```, ```!~~*``` pattern


#### 예

```
SELECT * FROM Customers
WHERE CustomerName ILIKE 'a%';
```

&quot;A&quot; 또는 &quot;a&quot;에서 시작하는 이름으로 고객을 반환합니다.

## 연결

조인을 사용하는 `SELECT` 쿼리에는 다음 구문이 있습니다.

```
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```


## 결합, 교차 및 제외

두 개 이상의 테이블에서 좋아요 행을 결합하거나 제외하는 `UNION`데, `INTERSECT`및 `EXCEPT` 절이 지원됩니다.

```
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

## 선택할 때 표 만들기

다음 구문은 쿼리 서비스에서 지원하는 `CREATE TABLE AS SELECT` (CTAS) 쿼리를 정의합니다.

```
CREATE TABLE table_name [ WITH (schema='target_schema_title') ] AS (select_query)
```

여기서 `target_schema_title` 는 XDM 스키마의 제목입니다. CTAS 쿼리에서 만든 새 데이터 세트에 대해 기존 XDM 스키마를 사용하려는 경우에만 이 절을 사용하십시오.

and `select_query` is a `SELECT` statement, the syntax is defined above in this document.


### 예

```
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
CREATE TABLE Chairs WITH (schema='target schema title') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)
```

지정된 CTAS 쿼리의 경우:

1. 명령문에는 `SELECT` , `COUNT``SUM``MIN`및 기타 집계 함수에 대한 별칭이 있어야 합니다.
2. 이 `SELECT` 문은 괄호()와 함께 제공되거나 괄호 없이 제공될 수 있습니다.

## 삽입

다음 구문은 쿼리 서비스에서 지원하는 `INSERT INTO` 쿼리를 정의합니다.

```
INSERT INTO table_name select_query
```

여기서 `select_query` 는 `SELECT` 문이며 이 문서의 구문은 위에 정의되어 있습니다.

### 예

```
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;
```

지정된 INSERT INTO 쿼리에 유의하십시오.

1. 문은 괄호()로 묶으면 안 `SELECT` 됩니다.
2. 문 결과의 스키마는 문에 정의된 테이블의 스키마와 일치해야 합니다. `SELECT` `INSERT INTO`

### 드롭 테이블

테이블을 삭제하고 EXTERNAL 테이블이 아닌 경우 파일 시스템에서 테이블과 연결된 디렉토리를 삭제합니다. 삭제할 테이블이 없으면 예외가 발생합니다.

```
DROP [TEMP] TABLE [IF EXISTS] [db_name.]table_name
```

### 매개 변수

- `IF EXISTS`:테이블이 없으면 아무 일도 발생하지 않습니다
- `TEMP`:임시 테이블

## 보기 만들기

다음 구문은 쿼리 서비스에서 지원하는 `CREATE VIEW` 쿼리를 정의합니다.

```
CREATE [ OR REPLACE ] VIEW view_name AS select_query
```

여기서 `view_name` 는 만들 보기의 이름이며 `select_query` 이 `SELECT` 문서의 구문은 위에 정의되어 있습니다.

예:

```
CREATE VIEW V1 AS SELECT color, type FROM Inventory
CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

### 드롭 뷰

다음 구문은 쿼리 서비스에서 지원하는 `DROP VIEW` 쿼리를 정의합니다.

```
DROP VIEW [IF EXISTS] view_name
```

삭제할 `view_name` 보기의 이름은 어디입니까?

예:

```
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## Spark SQL 명령

### SET

속성을 설정하거나, 기존 속성의 값을 반환하거나, 모든 기존 속성을 나열합니다. 기존 속성 키에 대한 값이 제공되면 이전 값은 재정의됩니다.

```
SET property_key [ To | =] property_value
```

모든 설정에 대한 값을 반환하려면 을 `SHOW [setting name]`사용합니다.

## PostgreSQL 명령

### 시작

이 명령은 구문 분석되고 완료된 명령이 클라이언트로 다시 전송됩니다. 이는 `START TRANSACTION` 명령과 동일합니다.

```
BEGIN [ TRANSACTION ]
```

#### 매개 변수

- `TRANSACTION`:선택적 키워드. 듣고 있어, 어떤 행동도 취하지 않아.

### 닫기

`CLOSE` 열려 있는 커서와 연결된 리소스를 비웁니다. 커서를 닫으면 후속 작업이 허용되지 않습니다. 더 이상 필요하지 않은 커서는 닫아야 합니다.

```
CLOSE { name }
```

#### 매개 변수

- `name`:닫을 열린 커서의 이름입니다.

### 커밋

커밋 트랜잭션 문에 대한 응답으로 쿼리 서비스에서 작업이 수행되지 않습니다.

```
COMMIT [ WORK | TRANSACTION ]
```

#### 매개 변수

- `WORK`
- `TRANSACTION`:선택적 키워드. 효과가 없습니다.

### 할당 취소

이전에 준비된 SQL 문을 `DEALLOCATE` 할당 해제하는 데 사용합니다. 준비된 문을 명시적으로 할당 해제하지 않으면 세션이 종료될 때 할당 취소됩니다.

```
DEALLOCATE [ PREPARE ] { name | ALL }
```

#### 매개 변수

- `Prepare`:이 키워드는 무시됩니다.
- `name`:할당 해제할 준비된 문의 이름입니다.
- `ALL`:준비된 모든 문을 할당 취소합니다.

### DECLARE

`DECLARE` 사용자는 더 큰 쿼리에서 한 번에 적은 수의 행을 검색하는 데 사용할 수 있는 커서를 만들 수 있습니다. 커서가 만들어지면, 에서 를 사용하여 행을 가져옵니다 `FETCH`.

```
DECLARE name CURSOR [ WITH  HOLD ] FOR query
```

#### 매개 변수

- `name`:만들 커서의 이름입니다.
- `WITH HOLD`:성공적으로 커밋된 트랜잭션 후에도 커서를 계속 사용할 수 있도록 지정합니다.
- `query`:커서로 반환할 행을 제공하는 `SELECT` 또는 `VALUES` 명령.

### 실행

`EXECUTE` 는 이전에 준비된 문을 실행하는 데 사용됩니다. 준비된 문은 세션 기간 동안에만 존재하므로, 준비된 문은 현재 세션에서 이전에 실행된 `PREPARE` 문으로 만들어졌어야 합니다.

문을 만든 `PREPARE` 문이 일부 매개 변수를 지정한 경우 호환되는 매개 변수 집합을 `EXECUTE` 문으로 전달해야 합니다. 그렇지 않으면 오류가 발생합니다. 준비된 문(함수와 달리)은 매개 변수의 유형 또는 수에 따라 오버로드되지 않습니다. 준비된 문의 이름은 데이터베이스 세션 내에서 고유해야 합니다.

```
EXECUTE name [ ( parameter [, ...] ) ]
```

#### 매개 변수

- `name`:실행할 준비된 문의 이름입니다.
- `parameter`:준비된 문에 대한 매개 변수의 실제 값입니다. 준비된 문을 만들 때 결정된 대로 이 매개 변수의 데이터 유형과 호환되는 값을 제공하는 표현식이어야 합니다.

### 설명

이 명령은 PostgreSQL 계획자가 제공된 문에 대해 생성하는 실행 계획을 표시합니다. 실행 계획은 문에서 참조하는 테이블을 검색하는 방법을 보여줍니다. 일반 순차적 스캔, 색인 스캔 등을 통해 여러 테이블이 참조되면 각 입력 테이블에서 필요한 행을 가져오는 데 사용되는 조인 알고리즘이 사용됩니다.

디스플레이의 가장 중요한 부분은 예상 명세서 실행 비용이며, 이 비용은 계획자의 추측으로 명세서 실행에 소요되는 시간입니다(임의의, 하지만 일반적인 평균 디스크 페이지 페치인 비용 단위로 측정됨). 실제로 두 개의 숫자가 표시됩니다.첫 번째 행을 반환하기 전의 시작 비용과 모든 행을 반환하는 총 비용. 대부분의 질의에서 총 비용은 중요하지만 EXISTS의 하위 쿼리와 같은 컨텍스트에서는 계획자가 최소 총 비용 대신 최소 시작 비용을 선택합니다(어쨌든 한 행을 가져온 후 중지되기 때문). 또한 `LIMIT` 절을 사용하여 반환할 행 수를 제한하는 경우 계획자는 종단점 비용 간의 적절한 보간을 만들어 어떤 계획이 가장 저렴한지 추정합니다.

이 `ANALYZE` 옵션을 선택하면 명령문이 실행되며 계획되었을 뿐만 아니라 그런 다음 각 계획 노드 내에 소요된 총 경과 시간(밀리초)과 반환된 총 행 수를 포함하여 실제 런타임 통계가 표시에 추가됩니다. 이것은 계획자의 추정이 사실과 가까운지 보는 데 유용합니다.

```
EXPLAIN [ ( option [, ...] ) ] statement
EXPLAIN [ ANALYZE ] statement

where option can be one of:
    ANALYZE [ boolean ]
    TYPE VALIDATE
    FORMAT { TEXT | JSON }
```

#### 매개 변수

- `ANALYZE`:명령을 실행하고 실제 실행 시간과 기타 통계를 표시합니다. 이 매개 변수의 기본값은 `FALSE`입니다.
- `FORMAT`:TEXT, XML, JSON 또는 YAML의 출력 형식을 지정합니다. 텍스트가 아닌 출력에는 텍스트 출력 형식과 동일한 정보가 포함되지만 프로그램에서 쉽게 구문 분석할 수 있습니다. 이 매개 변수의 기본값은 `TEXT`입니다.
- `statement`:모든 `SELECT`것, `INSERT``UPDATE`, `DELETE`그 실행 계획, `VALUES`즉, 당신이 보고 싶어하는 실행 계획을 가진 모든 것, `EXECUTE`그, `DECLARE``CREATE TABLE AS``CREATE MATERIALIZED VIEW AS` 모든 것, 또는 진술들.

> [!IMPORTANT] 이 `ANALYZE` 옵션이 사용될 때 문이 실제로 실행된다는 점을 염두에 두십시오. 어떤 결과물도 `EXPLAIN` 폐기하더라도 명령문의 다른 `SELECT` 부작용은 평소대로 발생합니다.

#### 예

단일 `integer` 열과 10000개의 행이 있는 테이블에 간단한 쿼리에 대한 계획을 표시하려면:

```
EXPLAIN SELECT * FROM foo;

                       QUERY PLAN
---------------------------------------------------------
 Seq Scan on foo  (cost=0.00..155.00 rows=10000 width=4)
(1 row)
```

### 가져오기

`FETCH` 이전에 만든 커서를 사용하여 행을 검색합니다.

커서에는 에 사용되는 연결된 위치가 `FETCH`있습니다. 커서 위치는 쿼리 결과의 첫 번째 행, 결과의 특정 행 또는 결과의 마지막 행 이후일 수 있습니다. 만든 후에는 첫 번째 행 앞에 커서가 배치됩니다. 일부 행을 가져온 후 커서는 가장 최근에 검색된 행에 배치됩니다. 사용 가능한 행 끝에서부터 `FETCH` 실행되면 커서가 마지막 행 뒤에 남아 있습니다. 해당 행이 없으면 빈 결과가 반환되고 첫 번째 행 앞 또는 마지막 행 뒤에 커서가 그대로 유지됩니다.

```
FETCH num_of_rows [ IN | FROM ] cursor_name
```

#### 매개 변수

- `num_of_rows`:가져올 행 수 또는 위치의 수를 결정하는 부호 있는 정수 상수.
- `cursor_name`:열린 커서의 이름입니다.

### 준비

`PREPARE` 준비된 문을 만듭니다. 준비된 문은 성능을 최적화하는 데 사용할 수 있는 서버측 객체입니다. 문이 실행되면 지정된 문이 구문 분석, 분석 및 다시 작성됩니다. `PREPARE` 이후에 `EXECUTE` 명령이 실행되면 준비된 문이 계획되고 실행됩니다. 이 노동력 분할은 반복적인 구문 분석 작업을 방지하며 실행 계획은 제공된 특정 매개 변수 값에 따라 달라지도록 합니다.

준비된 문은 매개 변수, 명령문을 실행할 때 명령문으로 대체되는 값을 사용할 수 있습니다. 준비된 문을 만들 때는 $1, $2 등을 사용하여 위치별 매개 변수를 참조하십시오. 매개 변수 데이터 유형의 해당 목록을 선택적으로 지정할 수 있습니다. 매개 변수의 데이터 유형이 지정되지 않았거나 알 수 없는 것으로 선언되면 가능한 경우 매개 변수가 처음 참조되는 컨텍스트에서 유형이 유추됩니다. 문을 실행할 때 `EXECUTE` 문에서 이러한 매개 변수에 대한 실제 값을 지정합니다.

준비된 문은 현재 데이터베이스 세션 동안 지속됩니다. 세션이 종료되면 준비된 명령문은 잊어버리므로 다시 사용하기 전에 다시 만들어야 합니다. 또한 여러 동시 데이터베이스 클라이언트에서 하나의 준비된 문을 사용할 수 없음을 의미합니다. 그러나 각 클라이언트는 자체 준비된 문을 만들어 사용할 수 있습니다. 준비된 문은 `DEALLOCATE` 명령을 사용하여 수동으로 정리할 수 있습니다.

준비된 문은 여러 유사한 문을 실행하는 데 단일 세션을 사용하는 경우 가장 큰 성능 이점을 얻을 수 있습니다. 성능 차이는 특히 쿼리가 많은 테이블의 조인을 포함하거나 여러 규칙의 적용을 필요로 하는 경우와 같이 명령문을 계획하거나 다시 쓰는 것이 복잡한 경우 중요합니다. 이 문이 상대적으로 간단하게 계획 및 다시 작성되지만 실행하기에는 상대적으로 비용이 많이 드는 경우 준비된 명령문의 성능 이점이 눈에 띄지 않습니다.

```
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

#### 매개 변수

- `name`:준비된 이 특정 문에 지정된 임의의 이름입니다. 단일 세션 내에서 고유해야 하며 이후에 이전에 준비된 문을 실행하거나 할당을 취소하는 데 사용됩니다.
- `data-type`:준비된 문에 대한 매개 변수의 데이터 유형입니다. 특정 매개 변수의 데이터 유형이 지정되지 않았거나 알 수 없는 것으로 지정된 경우 매개 변수가 처음 참조되는 컨텍스트에서 유추됩니다. 준비된 문 자체의 매개 변수를 참조하려면 $1, $2 등을 사용합니다.


### ROLLBACK

`ROLLBACK` 현재 트랜잭션을 롤백하고 트랜잭션에서 수행한 모든 업데이트를 삭제합니다.

```
ROLLBACK [ WORK ]
```

#### 매개 변수

- `WORK`

### 다음으로 선택

`SELECT INTO` 새 테이블을 만들고 쿼리를 통해 계산된 데이터로 채웁니다. 데이터는 일반 데이터이므로 클라이언트로 반환되지 않습니다 `SELECT`. 새 표의 열에는 테이블의 출력 열과 연관된 이름 및 데이터 유형이 `SELECT`있습니다.

```
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

- `TEMPORARAY` 또는 `TEMP`지정한 경우 테이블이 임시 테이블로 생성됩니다.
- `UNLOGGED:` 지정된 경우 테이블이 기록되지 않은 테이블로 만들어집니다.
- `new_table` 생성할 테이블의 이름(선택적으로 스키마 적격)입니다.

#### 예

표에서 최근 항목만 `films_recent` 포함하는 새 표를 `films`만듭니다.

```
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 표시

`SHOW` 런타임 매개 변수의 현재 설정을 표시합니다. 이러한 변수는 postgresql.conf 구성 파일을 편집하거나, 환경적 변수(libpq 또는 libpq 기반 응용 프로그램을 사용하는 경우)를 통해 또는, Postgres 서버를 시작할 때 명령줄 플래그를 통해 설정할 수 있습니다. `SET` `PGOPTIONS`

```
SHOW name
```

#### 매개 변수

- `name`:
   - `SERVER_VERSION`:서버의 버전 번호를 표시합니다.
   - `SERVER_ENCODING`:서버측 문자 집합 인코딩을 표시합니다. 현재 이 매개 변수는 데이터베이스 생성 시 인코딩이 결정되므로 표시할 수 있지만 설정할 수는 없습니다.
   - `LC_COLLATE`:데이터 정렬(텍스트 순서)에 대한 데이터베이스의 로케일 설정을 표시합니다. 현재 이 매개 변수는 데이터베이스 생성 시 설정되므로 표시할 수 있지만 설정할 수는 없습니다.
   - `LC_CTYPE`:문자 분류에 대한 데이터베이스의 로케일 설정을 표시합니다. 현재 이 매개 변수는 데이터베이스 생성 시 설정되므로 표시할 수 있지만 설정할 수는 없습니다.
      `IS_SUPERUSER`:현재 역할에 수퍼유저 권한이 있는 경우 True입니다.
- `ALL`:모든 구성 매개 변수의 값을 설명과 함께 표시합니다.

#### 예

매개 변수의 현재 설정 표시 `DateStyle`

```
SHOW DateStyle;
 DateStyle
-----------
 ISO, MDY
(1 row)
```

### 트랜잭션 시작

이 명령은 구문 분석하여 완료된 명령을 다시 클라이언트로 전송합니다. 이는 `BEGIN` 명령과 동일합니다.

```
START TRANSACTION [ transaction_mode [, ...] ]

where transaction_mode is one of:

    ISOLATION LEVEL { SERIALIZABLE | REPEATABLE READ | READ COMMITTED | READ UNCOMMITTED }
    READ WRITE | READ ONLY
```
