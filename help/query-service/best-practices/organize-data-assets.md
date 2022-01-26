---
title: Query Service의 데이터 자산 조직에 대한 우수 사례
description: 이 문서에서는 Query Service를 사용하여 편리하게 데이터를 구성할 수 있는 논리적 방법을 간략하게 설명합니다.
source-git-commit: ed9fa7b83f9e1c974bc74e9dde018a87823954ee
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 0%

---

# Query Service에서 데이터 자산 구성

이 문서에서는 Adobe Experience Platform Query Service에서 사용할 데이터 세트, 보기 및 임시 테이블을 포함한 데이터 자산을 구성하는 모범 사례에 대한 지침을 제공합니다. 이 섹션에서는 데이터를 구성하는 방법과 이 정보에 액세스, 업데이트 및 삭제하는 방법에 대한 정보를 다룹니다.

플랫폼 내에서 데이터 자산을 논리적으로 구성하는 것이 중요합니다 [!DNL Data Lake] 성장하면서 Query Service는 샌드박스 내의 데이터 자산을 논리적으로 그룹화할 수 있는 SQL 구문을 확장합니다. 이 조직 방법을 사용하면 물리적으로 이동할 필요 없이 스키마 간에 데이터 자산을 공유할 수 있습니다.

## 시작하기

이 문서를 계속 진행하기 전에 다음을 잘 이해해야 합니다 [쿼리 서비스](../home.md) 기능 및 [사용자 인터페이스 안내서](../ui/user-guide.md).

## Query Service에서 데이터 구성

다음 예제에서는 Adobe Experience Platform Query Service를 통해 표준 SQL 구문을 사용하여 데이터를 논리적으로 구성하는 데 사용할 수 있는 구문을 보여줍니다. 먼저 데이터 포인트에 대한 컨테이너 역할을 하는 데이터베이스를 만들어야 합니다. 데이터베이스에는 하나 이상의 스키마가 포함될 수 있으며 각 스키마에는 데이터 자산(데이터 세트, 보기, 임시 테이블 등)에 대한 하나 이상의 참조가 있을 수 있습니다. 이러한 참조에는 데이터 세트 간의 관계나 연결이 포함됩니다.

자세한 내용은 [쿼리 편집기 사용 안내서](../ui/user-guide.md) query Service UI를 사용하여 SQL 쿼리를 만드는 방법에 대한 자세한 지침은

샌드박스에서 데이터 세트를 논리적으로 구성하는 다음 SQL 구문이 지원됩니다.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

이 예(간결성을 위해 약간 잘림)는 `databaseA` 스키마 포함 `schema1`.

## 데이터 자산을 스키마에 연결

데이터 자산의 컨테이너 역할을 하는 스키마가 만들어지면 표준 SQL ALTER TABLE 구문을 사용하여 각 데이터 세트를 데이터베이스의 하나 이상의 스키마와 연결할 수 있습니다.

다음 예는 를 추가합니다 `dataset1`, `dataset2`, `dataset3` 및 `v1` 변환 후 `databaseA.schema1` 이전 예에서 생성된 컨테이너입니다.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## 데이터 컨테이너에서 데이터 자산에 액세스

데이터베이스 이름을 적절히 검증함으로써 [!DNL PostgreSQL] 클라이언트는 SHOW 키워드를 사용하여 만든 데이터 구조에 연결할 수 있습니다. SHOW 키워드에 대한 자세한 내용은 [SQL 구문 설명서에 섹션 표시](../sql/syntax.md#show).

&quot;all&quot;은 샌드박스의 모든 데이터베이스 및 스키마 컨테이너를 포함하는 기본 데이터베이스 이름입니다. 만들 때 [!DNL PostgreSQL] 를 사용하여 연결 `dbname="all"`, 액세스 권한 **임의** 데이터를 논리적으로 구성하도록 만든 데이터베이스 및 스키마.

모든 데이터베이스 목록 `dbname="all"` 사용 가능한 데이터베이스 세 개를 표시합니다.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

모든 스키마 나열 `dbname="all"` 샌드박스의 모든 데이터베이스와 관련된 세 가지 스키마를 표시합니다.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

만들 때 [!DNL PostgreSQL] 를 사용하여 연결 `dbname="databaseA"`아래 예와 같이 특정 데이터베이스와 연결된 모든 스키마에 액세스할 수 있습니다.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
 

SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
```

점 표기법을 사용하면 선택한 데이터베이스에 연결된 특정 스키마와 연결된 모든 테이블에 액세스할 수 있습니다. 연결 `DBNAME = databaseA.schema1;`, 특정 스키마와 연결된 모든 테이블(`schema1`)가 표시됩니다. 이 항목에서는 어떤 데이터 세트에 어느 테이블이 포함되어 있는지 설명합니다.

```sql
SHOW DATABASES;
  
name     
---------
databaseA


SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1


SHOW tables;
name       | type
----------------------
dataset1| table
dataset2| table
dataset3| table
```

## 데이터 컨테이너에서 데이터 자산 업데이트 또는 제거

IMS 조직(또는 샌드박스)의 데이터 자산 양이 증가하면 데이터 컨테이너에서 데이터 자산을 업데이트하거나 제거해야 합니다. 점 표기법을 사용하여 적절한 데이터베이스 및 스키마 이름을 참조하여 개별 자산을 조직 컨테이너에서 제거할 수 있습니다. 표 및 보기(`t1` 및 `v1` 각각 추가됨) `databaseA.schema1` 첫 번째 예에서 는 다음 예제의 구문을 사용하여 제거됩니다.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 데이터 자산 제거

다음 [테이블 놓기](../sql/syntax.md#drop-table) 함수는 [!DNL Data Lake] ims 조직에 있는 모든 데이터베이스에 테이블에 대한 단일 참조가 있는 경우.

```sql
DROP TABLE databaseA.schema2.t1;
```

### 데이터 자산 컨테이너 제거

표준 SQL 함수를 사용하여 데이터베이스와 스키마를 모두 제거할 수도 있습니다.

#### 데이터베이스 제거

데이터베이스와 연결된 데이터 자산에 대한 다른 참조가 있는 경우 데이터베이스를 제거하려고 할 때 함수에 오류가 발생합니다.

```sql
DROP DATABASE databaseA;
```

#### 스키마 제거

스키마를 제거할 때 다음 세 가지 중요한 고려 사항이 있습니다.

- 스키마를 제거해도 테이블, 보기 또는 임시 테이블과 같은 데이터 자산은 물리적으로 삭제되지 않습니다.
- 대상 스키마에서 참조되는 데이터 자산이 있고 모드가 RESTRICT인 경우 예외가 발생합니다.
- 대상 스키마에서 참조되는 데이터 자산이 있고 모드가 CASCADE인 경우, 시스템은 스키마 컨테이너에서 참조하는 모든 데이터 자산을 제거한 다음 스키마 컨테이너를 삭제합니다.

```sql
DROP SCHEMA databaseA.schema2;
```

## 다음 단계

이제 이 문서를 읽은 후 Adobe Experience Platform Query Service에서 사용할 데이터 자산의 조직 및 구조에 대한 우수 사례를 더 잘 이해할 수 있습니다. 정보를 읽어 Query Service 우수 사례에 대해 계속 학습하는 것이 좋습니다 [데이터 중복 제거 설명서](./deduplication.md).
