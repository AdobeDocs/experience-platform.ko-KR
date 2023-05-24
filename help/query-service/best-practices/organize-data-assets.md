---
title: Query Service의 데이터 자산 조직에 대한 우수 사례
description: 이 문서에서는 쿼리 서비스에서 쉽게 사용할 수 있도록 데이터를 구성하는 논리적 방법에 대해 설명합니다.
exl-id: 12d6af99-035a-4f80-b7c0-c6413aa50697
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# Query Service에서 데이터 자산 구성

이 문서에서는 Adobe Experience Platform 쿼리 서비스와 함께 사용할 데이터 세트, 보기 및 임시 테이블을 포함한 데이터 에셋을 구성하기 위한 모범 사례에 대한 지침을 제공합니다. 데이터 구성 방법과 이 정보에 액세스, 업데이트 및 삭제하는 방법에 대한 정보를 다룹니다.

플랫폼 내에서 데이터 자산을 논리적으로 구성하는 것이 중요합니다 [!DNL Data Lake] 자라면서 Query Service는 샌드박스 내에서 데이터 자산을 논리적으로 그룹화할 수 있도록 SQL 구문을 확장합니다. 이 조직 방법을 사용하면 물리적으로 이동할 필요 없이 스키마 간에 데이터 자산을 공유할 수 있습니다.

## 시작하기

이 문서를 계속하기 전에 다음을 잘 이해해야 합니다. [쿼리 서비스](../home.md) 기능 및 다음을 읽었습니다. [사용자 인터페이스 안내서](../ui/user-guide.md).

## 쿼리 서비스에서 데이터 구성

다음 예제에서는 표준 SQL 구문을 사용하여 데이터를 논리적으로 구성하기 위해 Adobe Experience Platform 쿼리 서비스를 통해 사용할 수 있는 구문을 보여 줍니다. 먼저 데이터 포인트의 컨테이너 역할을 할 데이터베이스를 만들어야 합니다. 데이터베이스에는 하나 이상의 스키마가 포함될 수 있으며 각 스키마에는 데이터 에셋(데이터 세트, 보기, 임시 테이블 등)에 대한 하나 이상의 참조가 있을 수 있습니다. 이러한 참조에는 데이터 세트 간의 관계 또는 연결이 포함됩니다.

다음을 참조하십시오. [쿼리 편집기 사용 안내서](../ui/user-guide.md) 쿼리 서비스 UI를 사용하여 SQL 쿼리를 만드는 방법에 대한 자세한 지침을 제공합니다.

샌드박스에서 데이터 세트를 논리적으로 구성하는 다음 SQL 구문이 지원됩니다.

```SQL
CREATE DATABASE databaseA;
CREATE SCHEMA databaseA.schema1;
CREATE table t1 ...;
CREATE view v1 ...;
ALTER TABLE t1 ADD PRIMARY KEY (c1) NOT ENFORCED;
ALTER TABLE t2 ADD FOREIGN KEY (c1) REFERENCES t1(c1) NOT ENFORCED;
```

예제(간결성을 위해 약간 잘림)에서는 다음과 같은 방법을 보여 줍니다. `databaseA` 스키마 포함 `schema1`.

## 데이터 에셋을 스키마에 연결

데이터 자산의 컨테이너 역할을 하는 스키마가 만들어지면 표준 SQL ALTER TABLE 구문을 사용하여 각 데이터 세트를 데이터베이스의 하나 이상의 스키마와 연결할 수 있습니다.

다음 예제에서는 를 추가합니다 `dataset1`, `dataset2`, `dataset3` 및 `v1` (으)로 `databaseA.schema1` 이전 예에서 생성된 컨테이너입니다.

```SQL
ALTER TABLE dataset1 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset2 SET SCHEMA databaseA.schema1;
 
ALTER TABLE dataset3 SET SCHEMA databaseA.schema1;
 
ALTER VIEW v1  SET SCHEMA databaseA.schema1;
```

## 데이터 컨테이너에서 데이터 에셋에 액세스

데이터베이스 이름을 적절히 지정하여 다음을 수행합니다. [!DNL PostgreSQL] 클라이언트는 SHOW 키워드를 사용하여 만든 데이터 구조에 연결할 수 있습니다. SHOW 키워드에 대한 자세한 내용은 [SQL 구문 설명서에 섹션 표시](../sql/syntax.md#show).

&quot;all&quot;은 샌드박스의 모든 데이터베이스 및 스키마 컨테이너를 포함하는 기본 데이터베이스 이름입니다. 다음을 수행하는 경우 [!DNL PostgreSQL] 을 사용한 연결 `dbname="all"`, 다음에 액세스할 수 있습니다 **임의** 데이터를 논리적으로 구성하기 위해 만든 데이터베이스와 스키마.

아래에 모든 데이터베이스 나열 `dbname="all"` 사용 가능한 데이터베이스 세 개를 표시합니다.

```sql
SHOW DATABASES;
  
name     
---------
databaseA
databaseB
databaseC
```

아래에 모든 스키마 나열 `dbname="all"` 샌드박스의 모든 데이터베이스와 관련된 세 개의 스키마를 표시합니다.

```SQL
SHOW SCHEMAS;
  
database       | schema
----------------------
databaseA      | schema1
databaseA      | schema2
databaseB      | schema3
```

다음을 수행하는 경우 [!DNL PostgreSQL] 을 사용한 연결 `dbname="databaseA"`에서는 아래 예와 같이 특정 데이터베이스와 연관된 모든 스키마에 액세스할 수 있습니다.

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

점 표기법을 사용하면 선택한 데이터베이스에 연결된 특정 스키마와 연결된 모든 테이블에 액세스할 수 있습니다. 에 연결하여 `DBNAME = databaseA.schema1;`, 특정 스키마와 연결된 모든 테이블(`schema1`)이 표시됩니다. 이렇게 하면 테이블이 포함된 데이터 세트에 대한 정보가 제공됩니다.

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

조직(또는 샌드박스)의 데이터 에셋 양이 증가함에 따라 데이터 컨테이너에서 데이터 에셋을 업데이트하거나 제거해야 합니다. 점 표기법을 사용하여 적절한 데이터베이스 및 스키마 이름을 참조하여 조직 컨테이너에서 개별 자산을 제거할 수 있습니다. 테이블 및 뷰(`t1` 및 `v1` )가에 추가됨 `databaseA.schema1` 첫 번째 예에서 는 다음 예의 구문을 사용하여 제거됩니다.

```sql
ALTER TABLE databaseA.schema2.t1 REMOVE SCHEMA databaseA.schema2;
ALTER VIEW databaseA.schema2.v1 REMOVE SCHEMA databaseA.schema2;
```

### 데이터 자산 제거

다음 [테이블 놓기](../sql/syntax.md#drop-table) 함수는에서 데이터 자산을 물리적으로 만 제거합니다. [!DNL Data Lake] 테이블에 대한 단일 참조가 조직의 모든 데이터베이스에 있는 경우.

```sql
DROP TABLE databaseA.schema2.t1;
```

### 데이터 자산 컨테이너 제거

표준 SQL 함수를 사용하여 데이터베이스와 스키마를 모두 제거할 수도 있습니다.

#### 데이터베이스 제거

데이터베이스와 연결된 데이터 자산에 대한 다른 참조가 있는 경우 함수는 데이터베이스를 제거하려고 할 때 오류를 발생시킵니다.

```sql
DROP DATABASE databaseA;
```

#### 스키마 제거

스키마를 제거할 때 다음과 같은 세 가지 중요 고려 사항이 있습니다.

- 스키마를 제거해도 테이블, 뷰 또는 임시 테이블과 같은 데이터 자산은 실제로 삭제되지 않습니다.
- 대상 스키마에서 참조되는 데이터 에셋이 있고 모드가 RESTRICT인 경우 예외가 발생합니다.
- 대상 스키마에서 참조되는 데이터 에셋이 있고 모드가 CASCADE인 경우 시스템은 스키마 컨테이너에 의해 참조되는 모든 데이터 에셋을 제거한 다음 스키마 컨테이너를 삭제합니다.

```sql
DROP SCHEMA databaseA.schema2;
```

## 다음 단계

이 문서를 읽으면 이제 Adobe Experience Platform 쿼리 서비스와 함께 사용할 데이터 자산의 구성 및 구조에 대한 모범 사례를 더 잘 이해할 수 있습니다. 다음을 읽음으로써 쿼리 서비스 모범 사례에 대해 계속 학습하는 것이 좋습니다. [데이터 중복 제거 설명서](../essential-concepts/deduplication.md).
