---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;sql 구문;sql;ctas;CTAS;선택 항목으로 테이블 만들기
solution: Experience Platform
title: 쿼리 서비스의 SQL 구문
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 지원하는 SQL 구문에 대해 자세히 설명합니다.
exl-id: 2bd4cc20-e663-4aaa-8862-a51fde1596cc
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '4291'
ht-degree: 2%

---

# 쿼리 서비스의 SQL 구문

Adobe Experience Platform 쿼리 서비스에서 `SELECT` 문 및 기타 제한된 명령에 표준 ANSI SQL을 사용할 수 있습니다. 이 문서에서는 [!DNL Query Service]에서 지원하는 SQL 구문을 다룹니다.

## 쿼리 선택 {#select-queries}

다음 구문은 [!DNL Query Service]에서 지원하는 `SELECT` 쿼리를 정의합니다.

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

아래 탭 섹션에서는 FROM, GROUP 및 WITH 키워드에 사용할 수 있는 옵션을 제공합니다.

>[!BEGINTABS]

>[!TAB `from_item`]

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

>[!TAB `grouping_element`]

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

>[!TAB `with_query`]

```sql
 with_query_name [ ( column_name [, ...] ) ] AS ( select | values )
```

>[!ENDTABS]

다음 하위 섹션은 위에 요약된 형식을 따르는 경우 쿼리에 사용할 수 있는 추가 조항에 대한 세부 정보를 제공합니다.

### SNAPSHOT 절

이 절을 사용하여 스냅숏 ID를 기반으로 테이블의 데이터를 증분 읽는 데 사용할 수 있습니다. 스냅샷 ID는 데이터가 기록될 때마다 데이터 레이크 테이블에 적용되는 긴 유형 번호로 표시되는 체크포인트 마커입니다. `SNAPSHOT` 절은 옆에 사용되는 테이블 관계에 연결됩니다.

```sql
    [ SNAPSHOT { SINCE start_snapshot_id | AS OF end_snapshot_id | BETWEEN start_snapshot_id AND end_snapshot_id } ]
```

#### 예

```sql
SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT AS OF end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN start_snapshot_id AND end_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN HEAD AND start_snapshot_id;

SELECT * FROM table_to_be_queried SNAPSHOT BETWEEN end_snapshot_id AND TAIL;

SELECT * FROM (SELECT id FROM table_to_be_queried BETWEEN start_snapshot_id AND end_snapshot_id) C 

(SELECT * FROM table_to_be_queried SNAPSHOT SINCE start_snapshot_id) a
  INNER JOIN 
(SELECT * from table_to_be_joined SNAPSHOT AS OF your_chosen_snapshot_id) b 
  ON a.id = b.id;
```

아래 표에서는 SNAPSHOT 절 내의 각 구문 옵션의 의미를 설명합니다.

| 구문 | 의미 |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------|
| `SINCE start_snapshot_id` | 지정된 스냅샷 ID(제외)에서 시작하는 데이터를 읽습니다. |
| `AS OF end_snapshot_id` | 지정된 스냅샷 ID(포함)에 있는 그대로 데이터를 읽습니다. |
| `BETWEEN start_snapshot_id AND end_snapshot_id` | 지정된 시작 및 끝 스냅숏 ID 사이에서 데이터를 읽습니다. `start_snapshot_id`을(를) 제외하고 `end_snapshot_id`을(를) 포함합니다. |
| `BETWEEN HEAD AND start_snapshot_id` | 첫 번째 스냅숏 앞의 데이터를 지정된 시작 스냅숏 ID(포함)로 읽습니다. 참고: `start_snapshot_id`에 있는 행만 반환합니다. |
| `BETWEEN end_snapshot_id AND TAIL` | 지정된 `end-snapshot_id` 바로 뒤에서 데이터 집합 끝(스냅숏 ID 제외)까지 데이터를 읽습니다. 즉, `end_snapshot_id`이(가) 데이터 집합의 마지막 스냅숏인 경우 마지막 스냅숏 이후에 스냅숏이 없으므로 쿼리에서 0개의 행을 반환합니다. |
| `SINCE start_snapshot_id INNER JOIN table_to_be_joined AS OF your_chosen_snapshot_id ON table_to_be_queried.id = table_to_be_joined.id` | `table_to_be_queried`에서 지정한 스냅숏 ID로 시작하는 데이터를 읽고 `your_chosen_snapshot_id`에서와 같이 `table_to_be_joined`의 데이터와 결합합니다. 조인은 조인되는 두 테이블의 ID 열에서 일치하는 ID를 기반으로 합니다. |

`SNAPSHOT` 절은 테이블 또는 테이블 별칭과 함께 작동하지만 하위 쿼리 또는 뷰 위에서는 작동하지 않습니다. `SNAPSHOT` 절은 테이블의 `SELECT` 쿼리를 적용할 수 있는 모든 위치에서 작동합니다.

또한 스냅숏 절의 특수 오프셋 값으로 `HEAD` 및 `TAIL`을(를) 사용할 수 있습니다. `HEAD`을(를) 사용하면 첫 번째 스냅숏 앞의 오프셋이 사용되고, `TAIL`은(는) 마지막 스냅숏 뒤의 오프셋이 사용됩니다.

>[!NOTE]
>
>두 스냅숏 ID 간에 쿼리하는 경우 시작 스냅숏이 만료되고 선택적 대체 동작 플래그(`resolve_fallback_snapshot_on_failure`)가 설정된 경우 다음 두 가지 시나리오가 발생할 수 있습니다.
>
>- 선택적 대체 동작 플래그를 설정하면 쿼리 서비스가 사용 가능한 가장 이른 스냅샷을 선택하고 이를 시작 스냅샷으로 설정한 다음 가장 이른 스냅샷과 지정된 종료 스냅샷 사이에 데이터를 반환합니다. 이 데이터는 사용 가능한 가장 빠른 스냅숏의 **포함**&#x200B;입니다.

### WHERE 절

기본적으로 `SELECT` 쿼리에서 `WHERE` 절에 의해 생성된 일치 항목은 대/소문자를 구분합니다. 일치하는 항목을 대/소문자를 구분하지 않게 하려면 `LIKE` 대신 `ILIKE` 키워드를 사용할 수 있습니다.

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

이 쿼리는 &quot;A&quot; 또는 &quot;a&quot;로 시작하는 이름을 가진 고객을 반환합니다.

### 가입

조인을 사용하는 `SELECT` 쿼리에 다음 구문이 있습니다.

```sql
SELECT statement
FROM statement
[JOIN | INNER JOIN | LEFT JOIN | LEFT OUTER JOIN | RIGHT JOIN | RIGHT OUTER JOIN | FULL JOIN | FULL OUTER JOIN]
ON join condition
```

### 결합, 교차 및 제외

`UNION`, `INTERSECT` 및 `EXCEPT` 절은 둘 이상의 테이블에서 유사 행을 조합하거나 제외하는 데 사용됩니다.

```sql
SELECT statement 1
[UNION | UNION ALL | UNION DISTINCT | INTERSECT | EXCEPT | MINUS]
SELECT statement 2
```

### 선택 항목으로 표 만들기 {#create-table-as-select}

다음 구문은 `CREATE TABLE AS SELECT`(CTAS) 쿼리를 정의합니다.

```sql
CREATE TABLE table_name [ WITH (schema='target_schema_title', rowvalidation='false', label='PROFILE') ] AS (select_query)
```

| 매개 변수 | 설명 |
| ----- | ----- |
| `schema` | XDM 스키마의 제목입니다. CTAS 쿼리로 만든 새 데이터 세트에 기존 XDM 스키마를 사용하려는 경우에만 이 절을 사용합니다. |
| `rowvalidation` | (선택 사항) 사용자가 새로 만든 데이터 세트에 대해 수집된 모든 새 일괄 처리의 행 수준 유효성 검사를 원하는지 여부를 지정합니다. 기본값은 `true`입니다. |
| `label` | CTAS 쿼리로 데이터 세트를 만들 때 값이 `profile`인 이 레이블을 사용하여 데이터 세트에 프로필이 활성화되도록 레이블을 지정합니다. 즉, 데이터 세트가 생성될 때 프로필에 대해 자동으로 표시됩니다. `label` 사용에 대한 자세한 내용은 파생 특성 확장 문서를 참조하십시오. |
| `select_query` | `SELECT` 문입니다. `SELECT` 쿼리의 구문은 [SELECT 쿼리 섹션](#select-queries)에 있습니다. |

**예**

```sql
CREATE TABLE Chairs AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs WITH (schema='target schema title', label='PROFILE') AS (SELECT color, count(*) AS no_of_chairs FROM Inventory i WHERE i.type=="chair" GROUP BY i.color)

CREATE TABLE Chairs AS (SELECT color FROM Inventory SNAPSHOT SINCE 123)
```

>[!NOTE]
>
>`SELECT` 문에는 `COUNT`, `SUM`, `MIN` 등의 집계 함수에 대한 별칭이 있어야 합니다. 또한 `SELECT` 문에는 괄호()를 사용하거나 사용하지 않을 수 있습니다. 대상 테이블에 증분 델타를 읽을 수 있는 `SNAPSHOT` 절을 제공할 수 있습니다.

## 에 삽입

`INSERT INTO` 명령은 다음과 같이 정의됩니다.

```sql
INSERT INTO table_name select_query
```

| 매개 변수 | 설명 |
| ----- | ----- |
| `table_name` | 쿼리를 삽입할 테이블의 이름입니다. |
| `select_query` | `SELECT` 문입니다. `SELECT` 쿼리의 구문은 [SELECT 쿼리 섹션](#select-queries)에 있습니다. |

**예**

>[!NOTE]
>
>다음은 교육적 목적으로 구성된 사례입니다.

```sql
INSERT INTO Customers SELECT SupplierName, City, Country FROM OnlineCustomers;

INSERT INTO Customers AS (SELECT * from OnlineCustomers SNAPSHOT AS OF 345)
```

>[!INFO]
> 
>**not**&#x200B;은(는) `SELECT` 문을 괄호()로 묶지 마십시오. 또한 `SELECT` 문 결과의 스키마는 `INSERT INTO` 문에 정의된 테이블의 스키마를 준수해야 합니다. 대상 테이블에 증분 델타를 읽을 수 있는 `SNAPSHOT` 절을 제공할 수 있습니다.

실제 XDM 스키마의 대부분의 필드는 루트 수준에서 찾을 수 없으며 SQL에서는 점 표기법을 사용할 수 없습니다. 중첩된 필드를 사용하여 실제 결과를 얻으려면 `INSERT INTO` 경로에 각 필드를 매핑해야 합니다.

중첩된 경로를 `INSERT INTO`하려면 다음 구문을 사용하십시오.

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

`DROP TABLE` 명령은 기존 테이블을 삭제하고 외부 테이블이 아닌 경우 해당 테이블과 연결된 디렉터리를 파일 시스템에서 삭제합니다. 테이블이 없으면 예외가 발생합니다.

```sql
DROP TABLE [IF EXISTS] [db_name.]table_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 항목을 지정하면 테이블이 **not**&#x200B;인 경우 예외가 throw되지 않습니다. |

## 데이터베이스 만들기

`CREATE DATABASE` 명령은 ADLS(Azure Data Lake Storage) 데이터베이스를 만듭니다.

```sql
CREATE DATABASE [IF NOT EXISTS] db_name
```

## 데이터베이스 삭제

`DROP DATABASE` 명령은 인스턴스에서 데이터베이스를 삭제합니다.

```sql
DROP DATABASE [IF EXISTS] db_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 항목을 지정하면 데이터베이스가 **not**&#x200B;인 경우 예외가 throw되지 않습니다. |

## 스키마 삭제

`DROP SCHEMA` 명령이 기존 스키마를 삭제합니다.

```sql
DROP SCHEMA [IF EXISTS] db_name.schema_name [ RESTRICT | CASCADE]
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 매개 변수를 지정하고 스키마가 **not**&#x200B;인 경우 예외가 throw되지 않습니다. |
| `RESTRICT` | 모드의 기본값입니다. 지정하면 스키마에 테이블이 포함되지 않은 **경우**&#x200B;에만 스키마가 삭제됩니다. |
| `CASCADE` | 지정하면 스키마가 스키마에 있는 모든 테이블과 함께 삭제됩니다. |

## 보기 만들기 {#create-view}

SQL 보기는 SQL 문의 결과 집합을 기반으로 하는 가상 테이블입니다. `CREATE VIEW` 문으로 보기를 만들고 이름을 지정하십시오. 그런 다음 해당 이름을 사용하여 쿼리 결과를 다시 참조할 수 있습니다. 이렇게 하면 복잡한 쿼리를 더 쉽게 재사용할 수 있습니다.

다음 구문은 데이터 집합에 대한 `CREATE VIEW` 쿼리를 정의합니다. 이 데이터 세트는 ADLS 또는 가속화된 스토어 데이터 세트일 수 있습니다.

```sql
CREATE VIEW view_name AS select_query
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `view_name` | 생성할 보기의 이름입니다. |
| `select_query` | `SELECT` 문입니다. `SELECT` 쿼리의 구문은 [SELECT 쿼리 섹션](#select-queries)에 있습니다. |

**예**

```sql
CREATE VIEW V1 AS SELECT color, type FROM Inventory

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory
```

다음 구문은 데이터베이스 및 스키마의 컨텍스트에서 보기를 만드는 `CREATE VIEW` 쿼리를 정의합니다.

**예**

```sql
CREATE VIEW db_name.schema_name.view_name AS select_query
CREATE OR REPLACE VIEW db_name.schema_name.view_name AS select_query
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `db_name` | 데이터베이스의 이름입니다. |
| `schema_name` | 스키마의 이름입니다. |
| `view_name` | 생성할 보기의 이름입니다. |
| `select_query` | `SELECT` 문입니다. `SELECT` 쿼리의 구문은 [SELECT 쿼리 섹션](#select-queries)에 있습니다. |

**예**

```sql
CREATE VIEW <dbV1 AS SELECT color, type FROM Inventory;

CREATE OR REPLACE VIEW V1 AS SELECT model, version FROM Inventory;
```

## 보기 표시

다음 쿼리는 보기 목록을 보여 줍니다.

```sql
SHOW VIEWS;
```

```console
 Db Name  | Schema Name | Name  | Id       |  Dataset Dependencies | Views Dependencies | TYPE
----------------------------------------------------------------------------------------------
 qsaccel  | profile_agg | view1 | view_id1 | dwh_dataset1          |                    | DWH
          |             | view2 | view_id2 | adls_dataset          | adls_views         | ADLS
(2 rows)
```

## 놓기 보기

다음 구문은 `DROP VIEW` 쿼리를 정의합니다.

```sql
DROP VIEW [IF EXISTS] view_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `IF EXISTS` | 이 항목을 지정하면 보기가 **not**&#x200B;인 경우 예외가 throw되지 않습니다. |
| `view_name` | 삭제할 보기의 이름입니다. |

**예**

```sql
DROP VIEW v1
DROP VIEW IF EXISTS v1
```

## 익명 블록 {#anonymous-block}

익명 블록은 실행 섹션과 예외 처리 섹션의 두 섹션으로 구성됩니다. 익명 블록에서는 실행 가능 섹션이 필수입니다. 그러나 예외 처리 섹션은 선택 사항입니다.

다음 예에서는 함께 실행할 하나 이상의 문으로 블록을 만드는 방법을 보여 줍니다.

```sql
$$BEGIN
  statementList
[EXCEPTION exceptionHandler]
$$END

exceptionHandler:
      WHEN OTHER
      THEN statementList

statementList:
    : (statement (';')) +
```

다음은 익명 블록을 사용하는 예제입니다.

```sql
$$BEGIN
   SET @v_snapshot_from = select parent_id  from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_snapshot_to = select snapshot_id from (select history_meta('email_tracking_experience_event_dataset') ) tab where is_current;
   SET @v_log_id = select now();
   CREATE TABLE tracking_email_id_incrementally
     AS SELECT _id AS id FROM email_tracking_experience_event_dataset SNAPSHOT BETWEEN @v_snapshot_from AND @v_snapshot_to;

EXCEPTION
  WHEN OTHER THEN
    DROP TABLE IF EXISTS tracking_email_id_incrementally;
    SELECT 'ERROR';
$$END;
```

### 익명 블록의 조건문 {#conditional-anonymous-block-statements}

IF-THEN-ELSE 컨트롤 구조를 사용하면 조건이 TRUE로 평가될 때 문 목록을 조건부로 실행할 수 있습니다. 이 제어 구조는 익명 블록 내에서만 적용할 수 있습니다. 이 구조를 독립 실행형 명령으로 사용하면 구문 오류(&quot;익명 블록 외부의 잘못된 명령&quot;)가 발생합니다.

아래의 코드 조각은 익명 블록의 IF-THEN-ELSE 조건문에 대한 올바른 형식을 보여 줍니다.

```javascript
IF booleanExpression THEN
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSEIF booleanExpression THEN 
   List of statements;
ELSE
   List of statements;
END IF
```

**예**

다음 예제에서는 `SELECT 200;`을(를) 실행합니다.

```sql
$$BEGIN
    SET @V = SELECT 2;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;   

 END$$;
```

이 구조는 `raise_error();`과(와) 함께 사용하여 사용자 지정 오류 메시지를 반환할 수 있습니다. 아래에 표시된 코드 블록은 &quot;사용자 지정 오류 메시지&quot;로 익명 블록을 종료합니다.

**예**

```sql
$$BEGIN
    SET @V = SELECT 5;
    SELECT @V;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT 200;
    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT raise_error('custom error message');
    END IF;   

 END$$;
```

#### 중첩된 IF 문

중첩된 IF 문은 익명 블록 내에서 지원됩니다.

**예**

```sql
$$BEGIN
    SET @V = SELECT 1;
    IF @V = 1 THEN
       SELECT 100;
       IF @V > 0 THEN
         SELECT 1000;
       END IF;   
    END IF;   

 END$$; 
```

#### 예외 블록

예외 블록은 익명 블록 내에서 지원됩니다.

**예**

```sql
$$BEGIN
    SET @V = SELECT 2;
    IF @V = 1 THEN
       SELECT 100;
    ELSEIF @V = 2 THEN
       SELECT raise_error(concat('custom-error for v= ', '@V' ));

    ELSEIF @V = 3 THEN
       SELECT 300;
    ELSE    
       SELECT 'DEFAULT';
    END IF;  
EXCEPTION WHEN OTHER THEN 
  SELECT 'THERE WAS AN ERROR';    
 END$$;
```

### JSON으로 자동 {#auto-to-json}

쿼리 서비스는 대화형 SELECT 쿼리의 최상위 복잡한 필드를 JSON 문자열로 반환하기 위한 선택적 세션 수준 설정을 지원합니다. `auto_to_json` 설정을 사용하면 복잡한 필드의 데이터를 JSON으로 반환한 다음 표준 라이브러리를 사용하여 JSON 개체로 구문 분석할 수 있습니다.

복잡한 필드가 포함된 SELECT 쿼리를 실행하기 전에 기능 플래그 `auto_to_json`을(를) true로 설정하십시오.

```sql
set auto_to_json=true; 
```

#### `auto_to_json` 플래그를 설정하기 전에

다음 표에서는 `auto_to_json` 설정을 적용하기 전의 예제 쿼리 결과를 제공합니다. 복잡한 필드가 있는 테이블을 타겟팅하는 동일한 SELECT 쿼리(아래 참조)가 두 시나리오에서 사용되었습니다.

```sql
SELECT * FROM TABLE_WITH_COMPLEX_FIELDS LIMIT 2;
```

결과는 다음과 같습니다.

```console
                _id                |                                _experience                                 | application  |                   commerce                   | dataSource |                               device                               |                       endUserIDs                       |                                                                                                environment                                                                                                |                     identityMap                     |                              placeContext                               |   receivedTimestamp   |       timestamp       | userActivityRegion |                                         web                                          | _adcstageforpqs
-----------------------------------+----------------------------------------------------------------------------+--------------+----------------------------------------------+------------+--------------------------------------------------------------------+--------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------------------------+-------------------------------------------------------------------------+-----------------------+-----------------------+--------------------+--------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE080007B35-E6CE00000000000,"(AAID)",t)")")  | ("(en-US,f,f,t,1.6,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",490,1125)",xo.net,64.3.235.13)     | [AAID -> "{(31892EE080007B35-E6CE00000000000,t)}"]  | ("("(34.01,-84.0)",lawrenceville,US,524,30043,ga)",600)                 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Search Results,"(1.0)")","(http://www.google.com/search?ie=UTF-8&q=,internal)") |
 31892EE15DE00000-401B92664FF48AE8 | ("("("(1,1)","(1,1)")","(-209479095,4085488201,-2105158467,2189808829)")") | (background) | (NULL,"(USD,NULL)",NULL,NULL,NULL,NULL,NULL) | (475341)   | (32,768,1024,205202,https://ns.adobe.com/xdm/external/deviceatlas) | ("("(31892EE100007BF3-215FE00000000001,"(AAID)",t)")") | ("(en-US,f,f,t,1.5,"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7",768,556)",ntt.net,219.165.108.145) | [AAID -> "{(31892EE100007BF3-215FE00000000001,t)}"] | ("("(34.989999999999995,138.42)",shizuoka,JP,392005,420-0812,22)",-240) | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | (UT1)              | ("(f,Home - JJEsquire,"(1.0)")","(NULL,typed_bookmarked)")                           |
(2 rows)  
```

#### `auto_to_json` 플래그 설정 후

다음 표는 결과 데이터 세트에 대한 `auto_to_json` 설정의 결과 차이점을 보여 줍니다. 두 시나리오 모두에서 동일한 SELECT 쿼리가 사용되었습니다.

```console
                _id                |   receivedTimestamp   |       timestamp       |                                                                                                                   _experience                                                                                                                   |           application            |             commerce             |    dataSource    |                                                                  device                                                                   |                                                   endUserIDs                                                   |                                                                                                                                                                                           environment                                                                                                                                                                                            |                             identityMap                              |                                                                                            placeContext                                                                                            |      userActivityRegion      |                                                                                     web                                                                                      | _adcstageforpqs
-----------------------------------+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------+----------------------------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------
 31892EE15DE00000-401D52664FF48A52 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE080007B35-E6CE00000000000","namespace":{"code":"AAID"},"primary":true}}}  | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.6","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":490,"viewportWidth":1125},"domain":"xo.net","ipV4":"64.3.235.13"}     | {"AAID":[{"id":"31892EE080007B35-E6CE00000000000","primary":true}]}  | {"geo":{"_schema":{"latitude":34.01,"longitude":-84.0},"city":"lawrenceville","countryCode":"US","dmaID":524,"postalCode":"30043","stateProvince":"ga"},"localTimezoneOffset":600}                 | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Search Results","pageViews":{"value":1.0}},"webReferrer":{"URL":"http://www.google.com/search?ie=UTF-8&q=","type":"internal"}} |
 31892EE15DE00000-401B92664FF48AE8 | 2022-09-02 19:47:14.0 | 2022-09-02 19:47:14.0 | {"analytics":{"customDimensions":{"eVars":{"eVar1":"1","eVar2":"1"},"props":{"prop1":"1","prop2":"1"}},"environment":{"browserID":-209479095,"browserIDStr":"4085488201","operatingSystemID":-2105158467,"operatingSystemIDStr":"2189808829"}}} | {"userPerspective":"background"} | {"order":{"currencyCode":"USD"}} | {"_id":"475341"} | {"colorDepth":32,"screenHeight":768,"screenWidth":1024,"typeID":"205202","typeIDService":"https://ns.adobe.com/xdm/external/deviceatlas"} | {"_experience":{"aaid":{"id":"31892EE100007BF3-215FE00000000001","namespace":{"code":"AAID"},"primary":true}}} | {"browserDetails":{"acceptLanguage":"en-US","cookiesEnabled":false,"javaEnabled":false,"javaScriptEnabled":true,"javaScriptVersion":"1.5","userAgent":"Mozilla/5.0 (iPhone; U; CPU iPhone OS 4_1 like Mac OS X; ja-jp) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8B117 Safari/6531.22.7","viewportHeight":768,"viewportWidth":556},"domain":"ntt.net","ipV4":"219.165.108.145"} | {"AAID":[{"id":"31892EE100007BF3-215FE00000000001","primary":true}]} | {"geo":{"_schema":{"latitude":34.989999999999995,"longitude":138.42},"city":"shizuoka","countryCode":"JP","dmaID":392005,"postalCode":"420-0812","stateProvince":"22"},"localTimezoneOffset":-240} | {"dataCenterLocation":"UT1"} | {"webPageDetails":{"isHomePage":false,"name":"Home - JJEsquire","pageViews":{"value":1.0}},"webReferrer":{"type":"typed_bookmarked"}}                                        |
(2 rows)
```

### 실패 시 대체 스냅샷 해결 {#resolve-fallback-snapshot-on-failure}

`resolve_fallback_snapshot_on_failure` 옵션은 만료된 스냅숏 ID 문제를 해결하는 데 사용됩니다. 스냅샷 메타데이터는 2일 후에 만료되며 만료된 스냅샷은 스크립트 논리를 무효화할 수 있습니다. 이는 익명 블록을 사용할 때 문제가 될 수 있습니다.

이전 스냅숏 ID로 스냅숏을 재정의하려면 `resolve_fallback_snapshot_on_failure` 옵션을 true로 설정하십시오.

```sql
SET resolve_fallback_snapshot_on_failure=true;
```

다음 코드 행은 메타데이터에서 사용 가능한 가장 빠른 `snapshot_id`을(를) 사용하여 `@from_snapshot_id`을(를) 재정의합니다.

```sql
$$ BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);

Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
END
$$;
```


## 데이터 자산 조직

Adobe Experience Platform 데이터 레이크 내에서 데이터 자산이 커짐에 따라 이를 논리적으로 구성하는 것이 중요합니다. Query Service는 샌드박스 내에서 데이터 자산을 논리적으로 그룹화할 수 있도록 SQL 구문을 확장합니다. 이 조직 방법을 사용하면 물리적으로 이동할 필요 없이 스키마 간에 데이터 자산을 공유할 수 있습니다.

표준 SQL 구문을 사용하는 다음 SQL 구문이 지원되므로 데이터를 논리적으로 구성할 수 있습니다.

```SQL
CREATE DATABASE dg1;
CREATE SCHEMA dg1.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

쿼리 서비스 모범 사례에 대한 자세한 설명은 [데이터 자산의 논리 조직](../best-practices/organize-data-assets.md) 안내서를 참조하세요.

## 테이블이 있습니다.

`table_exists` SQL 명령을 사용하여 현재 시스템에 테이블이 있는지 확인합니다. 이 명령은 테이블 **does**&#x200B;이(가) 있는 경우 `true`, 테이블이 **does**&#x200B;이(가) 없는 경우 `false` 부울 값을 반환합니다.

`table_exists` 기능을 사용하면 문을 실행하기 전에 테이블이 있는지 확인하여 `CREATE` 및 `INSERT INTO` 사용 사례를 모두 다루는 익명 블록 쓰기 프로세스를 단순화할 수 있습니다.

다음 구문은 `table_exists` 명령을 정의합니다.

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

`inline` 함수는 구조체 배열의 요소를 분리하고 값을 테이블로 생성합니다. `SELECT` 목록 또는 `LATERAL VIEW`에만 배치할 수 있습니다.

다른 생성기 함수가 있는 선택 목록에 `inline` 함수 **을(를) 배치할 수 없습니다**.

기본적으로 생성된 열의 이름은 &quot;col1&quot;, &quot;col2&quot; 등으로 지정됩니다. 식이 `NULL`이면 행이 생성되지 않습니다.

>[!TIP]
>
>열 이름은 `RENAME` 명령을 사용하여 이름을 바꿀 수 있습니다.

**예**

```sql
> SELECT inline(array(struct(1, 'a'), struct(2, 'b'))), 'Spark SQL';
```

이 예제는 다음을 반환합니다.

```text
1  a Spark SQL
2  b Spark SQL
```

이 두 번째 예에서는 `inline` 함수의 개념과 적용을 추가로 보여 줍니다. 아래 그림에는 예제의 데이터 모델이 나와 있습니다.

![productListItems에 대한 스키마 다이어그램입니다.](../images/sql/productListItems.png)

**예**

```sql
select inline(productListItems) from source_dataset limit 10;
```

`source_dataset`에서 가져온 값은 대상 테이블을 채우는 데 사용됩니다.

| SKU | 경험(_E) | 수량 | priceTotal |
|---------------------|-----------------------------------|----------|--------------|
| product-id-1 | (&quot;(&quot;(&quot;(A,pass,B,NULL)&quot;)&quot;) | 5 | 10.5 |
| product-id-5 | (&quot;(&quot;(&quot;(A, pass, B,NULL)&quot;)&quot;) |          |              |
| product-id-2 | (&quot;(&quot;(&quot;(AF, C, D,NULL)&quot;)&quot;)) | 6 | 40 |
| product-id-4 | (&quot;(&quot;(BM, pass, NA,NULL)&quot;)&quot;) | 3 | 12 |

## 설정

`SET` 명령은 속성을 설정하고 기존 속성 값을 반환하거나 기존 속성을 모두 나열합니다. 기존 속성 키에 대한 값이 제공되면 이전 값이 재정의됩니다.

```sql
SET property_key = property_value
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `property_key` | 나열하거나 변경할 속성의 이름입니다. |
| `property_value` | 속성을 설정할 값입니다. |

모든 설정에 대한 값을 반환하려면 `property_value` 없이 `SET [property key]`을(를) 사용합니다.

## [!DNL PostgreSQL]개 명령

아래의 하위 섹션은 쿼리 서비스에서 지원하는 [!DNL PostgreSQL] 명령을 다룹니다.

### 테이블 분석 {#analyze-table}

`ANALYZE TABLE` 명령은 명명된 테이블에 대한 분포 분석 및 통계 계산을 수행합니다. `ANALYZE TABLE`의 사용은 데이터 세트가 [가속화된 저장소](#compute-statistics-accelerated-store) 또는 [데이터 레이크](#compute-statistics-data-lake)에 저장되어 있는지 여부에 따라 달라집니다. 사용 방법에 대한 자세한 내용은 해당 섹션 을 참조하십시오.

#### 가속 스토어의 통계 계산 {#compute-statistics-accelerated-store}

`ANALYZE TABLE` 명령은 가속화된 저장소의 테이블에 대한 통계를 계산합니다. 통계는 가속화된 저장소의 주어진 테이블에 대해 실행된 CTAS 또는 ITAS 쿼리에 대해 계산됩니다.

**예**

```sql
ANALYZE TABLE <original_table_name>
```

다음은 `ANALYZE TABLE` 명령을 사용한 후 사용할 수 있는 통계 계산 목록입니다.

| 계산된 값 | 설명 |
|---|---|
| `field` | 테이블에 있는 열의 이름입니다. |
| `data-type` | 각 열에 허용되는 데이터 유형입니다. |
| `count` | 이 필드에 대해 null이 아닌 값이 포함된 행 수입니다. |
| `distinct-count` | 이 필드에 대한 고유하거나 고유한 값의 수입니다. |
| `missing` | 이 필드에 대해 null 값이 있는 행 수입니다. |
| `max` | 분석된 테이블의 최대값입니다. |
| `min` | 분석된 테이블의 최소값. |
| `mean` | 분석된 테이블의 평균 값입니다. |
| `stdev` | 분석된 테이블의 표준 편차입니다. |

#### 데이터 레이크의 통계 계산 {#compute-statistics-data-lake}

이제 `COMPUTE STATISTICS` SQL 명령을 사용하여 [!DNL Azure Data Lake Storage](ADLS) 데이터 세트에 대한 열 수준 통계를 계산할 수 있습니다. 전체 데이터 세트, 데이터 세트의 하위 집합, 모든 열 또는 열의 하위 집합에 대한 열 통계를 계산합니다.

`COMPUTE STATISTICS`이(가) `ANALYZE TABLE` 명령을 확장합니다. 그러나 `COMPUTE STATISTICS`, `FILTERCONTEXT` 및 `FOR COLUMNS` 명령은 가속화된 저장소 테이블에서 지원되지 않습니다. `ANALYZE TABLE` 명령에 대한 이러한 확장은 현재 ADLS 테이블에서만 지원됩니다.

**예**

```sql
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-04-01 00:00:00') and timestamp <= to_timestamp('2023-04-05 00:00:00')) COMPUTE STATISTICS  FOR COLUMNS (commerce, id, timestamp);
```

`FILTER CONTEXT` 명령은 제공된 필터 조건을 기반으로 데이터 집합 하위 집합에 대한 통계를 계산합니다. `FOR COLUMNS` 명령은 분석할 특정 열을 대상으로 합니다.

>[!NOTE]
>
>`Statistics ID` 및 생성된 통계는 각 세션에 대해서만 유효하며 다른 PSQL 세션에서 액세스할 수 없습니다.<br><br>제한 사항:<ul><li>배열 또는 맵 데이터 유형에 대해서는 통계 생성이 지원되지 않습니다.</li><li>계산된 통계는 세션 간에 **지속되지 않습니다**.</li></ul><br><br>옵션:<br><ul><li>`skip_stats_for_complex_datatypes`</li></ul><br>기본적으로 플래그는 true로 설정됩니다. 따라서 지원되지 않는 데이터 형식에 대한 통계가 요청되면 오류가 발생하지 않지만 지원되지 않는 데이터 형식이 있는 필드는 자동으로 건너뜁니다.<br>지원되지 않는 데이터 형식에 대한 통계가 요청될 때 오류에 대한 알림을 사용하도록 설정하려면 `SET skip_stats_for_complex_datatypes = false`을(를) 사용하십시오.

콘솔 출력이 아래와 같이 표시됩니다.

```console
|     Statistics ID      | 
| ---------------------- |
| adc_geometric_stats_1  |
(1 row)
```

그런 다음 `Statistics ID`을(를) 참조하여 계산된 통계를 직접 쿼리할 수 있습니다. 출력을 전체적으로 보려면 아래 예제 문과 같이 `Statistics ID` 또는 별칭 이름을 사용합니다. 이 기능에 대한 자세한 내용은 [별칭 이름 설명서](../key-concepts/dataset-statistics.md#alias-name)를 참조하세요.

```sql
-- This statement gets the statistics generated for `alias adc_geometric_stats_1`.
SELECT * FROM adc_geometric_stats_1;
```

`SHOW STATISTICS` 명령을 사용하여 세션에서 생성된 모든 임시 통계에 대한 메타데이터를 표시합니다. 이 명령은 통계 분석의 범위를 구체화하는 데 도움이 될 수 있습니다.

```sql
SHOW STATISTICS;
```

SHOW STATISTICS의 출력 예는 아래에 나와 있습니다.

```console
      statsId         |   tableName   | columnSet |         filterContext       |      timestamp
----------------------+---------------+-----------+-----------------------------+--------------------
adc_geometric_stats_1 | adc_geometric |   (age)   |                             | 25/06/2023 09:22:26
demo_table_stats_1    |  demo_table   |    (*)    |       ((age > 25))          | 25/06/2023 12:50:26
age_stats             | castedtitanic |   (age)   | ((age > 25) AND (age < 40)) | 25/06/2023 09:22:26
```

자세한 내용은 [데이터 집합 통계 설명서](../key-concepts/dataset-statistics.md)를 참조하세요.

#### 테이블 샘플 {#tablesample}

Adobe Experience Platform 쿼리 서비스는 대략적인 쿼리 처리 기능의 일부로 샘플 데이터 세트를 제공합니다.

데이터 집합 샘플은 데이터 집합에 대한 집계 작업에 대해 정확한 답변이 필요하지 않을 때 사용하는 것이 가장 좋습니다. 대략적인 답변을 반환하기 위해 대략적인 쿼리를 발행하여 큰 데이터 세트에 대해 보다 효율적인 탐색 쿼리를 수행하려면 `TABLESAMPLE` 기능을 사용하십시오.

샘플 데이터 세트는 원본의 레코드 비율만 사용하여 기존 [!DNL Azure Data Lake Storage](ADLS) 데이터 세트의 균일한 무작위 샘플로 만들어집니다. 데이터 집합 샘플 기능이 `ANALYZE TABLE` 명령을 `TABLESAMPLE` 및 `SAMPLERATE` SQL 명령으로 확장합니다.

아래 예에서 1행은 표의 5% 샘플을 계산하는 방법을 보여줍니다. 두 번째 행은 표 내의 데이터에 대한 필터링된 보기에서 5% 샘플을 계산하는 방법을 보여 줍니다.

**예**

```sql {line-numbers="true"}
ANALYZE TABLE tableName TABLESAMPLE SAMPLERATE 5;
ANALYZE TABLE tableName FILTERCONTEXT (timestamp >= to_timestamp('2023-01-01')) TABLESAMPLE SAMPLERATE 5:
```

자세한 내용은 [데이터 집합 샘플 설명서](../key-concepts/dataset-samples.md)를 참조하세요.

### 시작

`BEGIN` 명령 또는 `BEGIN WORK` 또는 `BEGIN TRANSACTION` 명령은 트랜잭션 블록을 시작합니다. begin 명령 뒤에 입력된 모든 문은 명시적 COMMIT 또는 ROLLBACK 명령이 제공될 때까지 단일 트랜잭션에서 실행됩니다. 이 명령은 `START TRANSACTION`과(와) 동일합니다.

```sql
BEGIN
BEGIN WORK
BEGIN TRANSACTION
```

### 닫기

`CLOSE` 명령을 사용하면 열린 커서와 관련된 리소스를 사용할 수 있습니다. 커서를 닫으면 후속 작업이 허용되지 않습니다. 더 이상 필요하지 않은 경우 커서를 닫아야 합니다.

```sql
CLOSE name
CLOSE ALL
```

`CLOSE name`을(를) 사용하는 경우 `name`은(는) 닫아야 하는 열린 커서의 이름을 나타냅니다. `CLOSE ALL`을(를) 사용하면 열려 있는 모든 커서가 닫힙니다.

### 할당 해제

이전에 준비한 SQL 문의 할당을 취소하려면 `DEALLOCATE` 명령을 사용합니다. 준비된 문의 할당을 명시적으로 취소하지 않은 경우 세션이 종료되면 이 문의 할당이 취소됩니다. 준비된 문에 대한 자세한 내용은 [PREPARE 명령](#prepare) 섹션에 있습니다.

```sql
DEALLOCATE name
DEALLOCATE ALL
```

`DEALLOCATE name`을(를) 사용하는 경우 `name`은(는) 할당 해제해야 하는 준비된 문의 이름을 나타냅니다. `DEALLOCATE ALL`을(를) 사용하면 준비된 문이 모두 할당 해제됩니다.

### DECLARE

`DECLARE` 명령을 사용하면 큰 쿼리에서 적은 수의 행을 검색하는 데 사용할 수 있는 커서를 만들 수 있습니다. 커서가 만들어지면 `FETCH`을(를) 사용하여 커서에서 행을 가져옵니다.

```sql
DECLARE name CURSOR FOR query
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 생성할 커서의 이름입니다. |
| `query` | 커서가 반환할 행을 제공하는 `SELECT` 또는 `VALUES` 명령입니다. |

### 실행

`EXECUTE` 명령은 이전에 준비한 문을 실행하는 데 사용됩니다. 준비된 문은 세션 중에만 있으므로 준비된 문은 현재 세션에서 이전에 실행된 `PREPARE` 문으로 생성되어야 합니다. 준비된 문을 사용하는 방법에 대한 자세한 내용은 [`PREPARE` 명령](#prepare) 섹션에 있습니다.

문을 만든 `PREPARE` 문에서 일부 매개 변수를 지정한 경우 호환 가능한 매개 변수 집합을 `EXECUTE` 문에 전달해야 합니다. 이러한 매개 변수가 전달되지 않으면 오류가 발생합니다.

```sql
EXECUTE name [ ( parameter ) ]
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 실행할 준비된 문의 이름입니다. |
| `parameter` | 준비된 문에 대한 매개 변수의 실제 값. 준비된 문이 생성될 때 결정된 대로 이 매개 변수의 데이터 유형과 호환되는 값을 산출하는 표현식이어야 합니다. 준비된 문에 여러 매개 변수가 있는 경우 쉼표로 구분됩니다. |

### 설명

`EXPLAIN` 명령은 제공된 문의 실행 계획을 표시합니다. 실행 계획에는 명령문에서 참조하는 테이블을 검사하는 방법이 표시됩니다. 여러 테이블이 참조되는 경우 각 입력 테이블에서 필요한 행을 통합하는 데 사용되는 조인 알고리즘을 보여 줍니다.

```sql
EXPLAIN statement
```

응답 형식을 정의하려면 `EXPLAIN` 명령과 함께 `FORMAT` 키워드를 사용합니다.

```sql
EXPLAIN FORMAT { TEXT | JSON } statement
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `FORMAT` | `FORMAT` 명령을 사용하여 출력 형식을 지정하십시오. 사용 가능한 옵션은 `TEXT` 또는 `JSON`입니다. 텍스트가 아닌 출력에는 텍스트 출력 형식과 동일한 정보가 포함되어 있지만 프로그램이 더 쉽게 구문 분석할 수 있습니다. 이 매개 변수의 기본값은 `TEXT`입니다. |
| `statement` | 실행 계획을 보려는 모든 `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `VALUES`, `EXECUTE`, `DECLARE`, `CREATE TABLE AS` 또는 `CREATE MATERIALIZED VIEW AS` 문입니다. |

>[!IMPORTANT]
>
>`SELECT` 문이 반환할 수 있는 출력은 `EXPLAIN` 키워드로 실행할 때 무시됩니다. 그 진술의 다른 부작용들은 평소와 같이 발생한다.

**예**

다음 예제에서는 단일 `integer` 열과 10000 행이 있는 테이블의 단순 쿼리에 대한 계획을 보여 줍니다.

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

`FETCH` 명령은 이전에 만든 커서를 사용하여 행을 검색합니다.

```sql
FETCH num_of_rows [ IN | FROM ] cursor_name
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `num_of_rows` | 가져올 행 수입니다. |
| `cursor_name` | 정보를 검색하는 커서의 이름입니다. |

### 준비 {#prepare}

`PREPARE` 명령을 사용하면 준비된 문을 만들 수 있습니다. 준비된 문은 유사한 SQL 문을 템플릿화하는 데 사용할 수 있는 서버측 개체입니다.

준비된 문은 실행 시 문에 대체되는 값인 매개 변수를 사용할 수 있습니다. 매개 변수는 준비된 문을 사용할 때 $1, $2 등을 사용하여 위치별로 참조됩니다.

선택적으로 매개 변수 데이터 유형 목록을 지정할 수 있습니다. 매개 변수의 데이터 유형이 나열되지 않으면 해당 유형을 컨텍스트에서 유추할 수 있습니다.

```sql
PREPARE name [ ( data_type [, ...] ) ] AS SELECT
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 준비된 문의 이름입니다. |
| `data_type` | 준비된 문 매개 변수의 데이터 형식입니다. 매개 변수의 데이터 유형이 나열되지 않으면 해당 유형을 컨텍스트에서 유추할 수 있습니다. 여러 데이터 유형을 추가해야 하는 경우 쉼표로 구분된 목록으로 추가할 수 있습니다. |

### 롤백

`ROLLBACK` 명령은 현재 트랜잭션을 취소하고 트랜잭션에서 수행한 모든 업데이트를 삭제합니다.

```sql
ROLLBACK
ROLLBACK WORK
```

### 다음으로 선택

`SELECT INTO` 명령은 새 테이블을 만들고 쿼리에 의해 계산된 데이터로 채웁니다. 일반 `SELECT` 명령을 사용하므로 데이터가 클라이언트에 반환되지 않습니다. 새 테이블의 열에는 `SELECT` 명령의 출력 열과 연결된 이름 및 데이터 형식이 있습니다.

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

표준 SELECT 쿼리 매개 변수에 대한 자세한 내용은 [SELECT 쿼리 섹션](#select-queries)에 있습니다. 이 섹션에는 `SELECT INTO` 명령에 배타적인 매개 변수만 나열됩니다.

| 매개 변수 | 설명 |
| ------ | ------ |
| `TEMPORARY` 또는 `TEMP` | 선택적 매개 변수. 매개변수를 지정하면 생성된 테이블이 임시 테이블이 됩니다. |
| `UNLOGGED` | 선택적 매개 변수. 매개 변수를 지정하면 작성된 테이블이 기록되지 않은 테이블입니다. 기록되지 않은 테이블에 대한 자세한 내용은 [[!DNL PostgreSQL] 설명서](https://www.postgresql.org/docs/current/sql-createtable.html)를 참조하세요. |
| `new_table` | 생성할 테이블의 이름입니다. |

**예**

다음 쿼리는 `films` 테이블의 최근 항목으로만 구성된 새 테이블 `films_recent`을(를) 만듭니다.

```sql
SELECT * INTO films_recent FROM films WHERE date_prod >= '2002-01-01';
```

### 표시

`SHOW` 명령은 런타임 매개 변수의 현재 설정을 표시합니다. 이러한 변수는 `SET` 문을 사용하여, `postgresql.conf` 구성 파일을 편집하거나, `PGOPTIONS` 환경 변수(libpq 또는 libpq 기반 응용 프로그램을 사용하는 경우)를 통해 또는 Postgres 서버를 시작할 때 명령줄 플래그를 통해 설정할 수 있습니다.

```sql
SHOW name
SHOW ALL
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `name` | 정보를 보려는 런타임 매개 변수의 이름입니다. 런타임 매개 변수에 사용할 수 있는 값에는 다음 값이 포함됩니다. <br>`SERVER_VERSION`: 이 매개 변수는 서버의 버전 번호를 표시합니다.<br>`SERVER_ENCODING`: 이 매개 변수는 서버측 문자 집합 인코딩을 보여 줍니다.<br>`LC_COLLATE`: 이 매개 변수는 데이터 정렬(텍스트 순서 지정)에 대한 데이터베이스의 로캘 설정을 보여 줍니다.<br>`LC_CTYPE`: 이 매개 변수는 문자 분류에 대한 데이터베이스의 로케일 설정을 보여 줍니다.<br>`IS_SUPERUSER`: 이 매개 변수는 현재 역할에 수퍼유저 권한이 있는지 여부를 표시합니다. |
| `ALL` | 모든 구성 매개 변수의 값을 설명과 함께 표시합니다. |

**예**

다음 쿼리는 `DateStyle` 매개 변수의 현재 설정을 보여 줍니다.

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

`COPY` 명령은 `SELECT` 쿼리의 출력을 지정된 위치에 복제합니다. 이 명령을 수행하려면 사용자에게 이 위치에 대한 액세스 권한이 있어야 합니다.

```sql
COPY query
    TO '%scratch_space%/folder_location'
    [  WITH FORMAT 'format_name']
```

| 매개 변수 | 설명 |
| ------ | ------ |
| `query` | 복사할 쿼리입니다. |
| `format_name` | 쿼리를 복사할 형식입니다. `format_name`은(는) `parquet`, `csv` 또는 `json` 중 하나일 수 있습니다. 기본적으로 값은 `parquet`입니다. |

>[!NOTE]
>
>전체 출력 경로는 `adl://<ADLS_URI>/users/<USER_ID>/acp_foundation_queryService/folder_location/<QUERY_ID>`입니다.

### 테이블 변경 {#alter-table}

`ALTER TABLE` 명령을 사용하면 기본 또는 외래 키 제약 조건을 추가하거나 삭제하고 테이블에 열을 추가할 수 있습니다.

#### 제한 추가 또는 삭제

다음 SQL 쿼리는 테이블에 제약 조건을 추가하거나 삭제하는 예를 보여 줍니다. 기본 키 및 외래 키 제약 조건은 쉼표로 구분된 값이 있는 여러 열에 추가할 수 있습니다. 아래 예에 표시된 것처럼 둘 이상의 열 이름 값을 전달하여 복합 키를 만들 수 있습니다.

**기본 키 또는 복합 키 정의**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT PRIMARY KEY ( column_name1, column_name2 ) NAMESPACE namespace
```

**하나 이상의 키를 기준으로 테이블 간의 관계를 정의합니다**

```sql
ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name ) REFERENCES referenced_table_name ( primary_column_name )

ALTER TABLE table_name ADD CONSTRAINT FOREIGN KEY ( column_name1, column_name2 ) REFERENCES referenced_table_name ( primary_column_name1, primary_column_name2 )
```

**ID 열 정의**

```sql
ALTER TABLE table_name ADD CONSTRAINT PRIMARY IDENTITY ( column_name ) NAMESPACE namespace

ALTER TABLE table_name ADD CONSTRAINT IDENTITY ( column_name ) NAMESPACE namespace
```

**제약 조건/관계/ID 삭제**

```sql
ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT PRIMARY KEY ( column_name1, column_name2 )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name )

ALTER TABLE table_name DROP CONSTRAINT FOREIGN KEY ( column_name1, column_name2 )

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
>테이블 스키마는 고유해야 하며 여러 테이블 간에 공유되지 않아야 합니다. 또한 기본 키, 기본 ID 및 ID 제약 조건에는 네임스페이스가 필수입니다.

#### 기본 및 보조 ID 추가 또는 삭제

기본 및 보조 ID 테이블 열 모두에 대한 제약 조건을 추가하거나 삭제하려면 `ALTER TABLE` 명령을 사용합니다.

다음 예제에서는 제약 조건을 추가하여 기본 ID와 보조 ID를 추가합니다.

```sql
ALTER TABLE t1 ADD CONSTRAINT PRIMARY IDENTITY (id) NAMESPACE 'IDFA';
ALTER TABLE t1 ADD CONSTRAINT IDENTITY(id) NAMESPACE 'IDFA';
```

아래 예와 같이 제한을 드롭하여 ID를 제거할 수도 있습니다.

```sql
ALTER TABLE t1 DROP CONSTRAINT PRIMARY IDENTITY (c1) ;
ALTER TABLE t1 DROP CONSTRAINT IDENTITY (c1) ;
```

자세한 내용은 [임시 데이터 세트에서 ID 설정](../data-governance/ad-hoc-schema-identities.md)에 대한 문서를 참조하십시오.

#### 열 추가

다음 SQL 쿼리는 테이블에 열을 추가하는 예를 보여 줍니다.

```sql
ALTER TABLE table_name ADD COLUMN column_name data_type

ALTER TABLE table_name ADD COLUMN column_name_1 data_type1, column_name_2 data_type2 
```

##### 지원되는 데이터 유형

다음 표는 Azure SQL에서 [!DNL Postgres SQL], XDM 및 [!DNL Accelerated Database Recovery](ADR)이 있는 테이블에 열을 추가하는 데 허용되는 데이터 형식을 나열합니다.

| — | PSQL 클라이언트 | XDM | ADR | 설명 |
|---|---|---|---|---|
| 1 | `bigint` | `int8` | `bigint` | -9,223,372,036,854,775,807부터 9,223,372,036,854,775,807까지의 큰 정수를 8바이트로 저장하는 데 사용되는 숫자 데이터 형식입니다. |
| 2 | `integer` | `int4` | `integer` | -2,147,483,648 - 2,147,483,647 범위의 정수를 4바이트로 저장하는 데 사용되는 숫자 데이터 형식입니다. |
| 3 | `smallint` | `int2` | `smallint` | -32,768 ~ 215-1 32,767 범위의 정수를 2바이트로 저장하는 데 사용되는 숫자 데이터 형식입니다. |
| 4 | `tinyint` | `int1` | `tinyint` | 0에서 255 사이의 정수를 1바이트에 저장하는 데 사용되는 숫자 데이터 형식입니다. |
| 5 | `varchar(len)` | `string` | `varchar(len)` | 변수 크기의 문자 데이터 유형입니다. `varchar`은(는) 열 데이터 항목의 크기가 상당히 다를 때 가장 적합합니다. |
| 6 | `double` | `float8` | `double precision` | `FLOAT8` 및 `FLOAT`은(는) `DOUBLE PRECISION`에 대해 올바른 동의어입니다. `double precision`은(는) 부동 소수점 데이터 형식입니다. 부동 소수점 값은 8바이트로 저장됩니다. |
| 7 | `double precision` | `float8` | `double precision` | `FLOAT8`은(는) `double precision`의 올바른 동의어입니다.`double precision`은(는) 부동 소수점 데이터 형식입니다. 부동 소수점 값은 8바이트로 저장됩니다. |
| 8 | `date` | `date` | `date` | `date` 데이터 형식은 타임스탬프 정보가 없는 4바이트로 저장된 달력 날짜 값입니다. 유효한 날짜 범위는 01-01-0001부터 12-31-9999까지입니다. |
| 9 | `datetime` | `datetime` | `datetime` | 달력 날짜 및 시간으로 표현된 인스턴트 인 타임을 저장하는 데 사용되는 데이터 유형입니다. `datetime`에는 연도, 월, 일, 시간, 초 및 분수의 한정자가 포함됩니다. `datetime` 선언에는 해당 시퀀스에서 연결되는 시간 단위의 하위 집합이 포함될 수 있으며 단일 시간 단위만 포함할 수도 있습니다. |
| 10 | `char(len)` | `string` | `char(len)` | `char(len)` 키워드는 항목의 길이가 고정된 문자를 나타내는 데 사용됩니다. |

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
| `data_type` | 추가하려는 열의 데이터 유형입니다. 지원되는 데이터 유형은 bigint, char, string, date, datetime, double, double precision, integer, smallint, tinyint, varchar입니다. |

### 기본 키 표시

`SHOW PRIMARY KEYS` 명령은 지정된 데이터베이스에 대한 모든 기본 키 제약 조건을 나열합니다.

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

`SHOW FOREIGN KEYS` 명령은 지정된 데이터베이스에 대한 모든 외래 키 제약 조건을 나열합니다.

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

`SHOW DATAGROUPS` 명령은 연결된 모든 데이터베이스의 테이블을 반환합니다. 각 데이터베이스에 대해 테이블에는 스키마, 그룹 유형, 하위 유형, 하위 이름 및 하위 ID가 포함됩니다.

```sql
SHOW DATAGROUPS
```

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                       |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   adls_db     | adls_scheema      | ADLS      | Data Lake Table      | adls_table1                                        | 6149ff6e45cfa318a76ba6d3
   adls_db     | adls_scheema      | ADLS      | Accelerated Store | _table_demo1                                       | 22df56cf-0790-4034-bd54-d26d55ca6b21
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view1                                         | c2e7ddac-d41c-40c5-a7dd-acd41c80c5e9
   adls_db     | adls_scheema      | ADLS      | View                 | adls_view4                                         | b280c564-df7e-405f-80c5-64df7ea05fc3
```


### 테이블에 대한 데이터 그룹 표시

`SHOW DATAGROUPS FOR 'table_name'` 명령은 매개 변수를 자식 값으로 포함하는 연결된 모든 데이터베이스의 테이블을 반환합니다. 각 데이터베이스에 대해 테이블에는 스키마, 그룹 유형, 하위 유형, 하위 이름 및 하위 ID가 포함됩니다.

```sql
SHOW DATAGROUPS FOR 'table_name'
```

**매개 변수**

- `table_name`: 연결된 데이터베이스를 찾을 테이블의 이름입니다.

```console
   Database   |      Schema       | GroupType |      ChildType       |                     ChildName                      |               ChildId
  -------------+-------------------+-----------+----------------------+----------------------------------------------------+--------------------------------------
   dwh_db_demo | schema2           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   dwh_db_demo | schema1           | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
   qsaccel     | profile_aggs      | QSACCEL   | Accelerated Store | _table_demo2                                       | d270f704-0a65-4f0f-b3e6-cb535eb0c8ce
```
