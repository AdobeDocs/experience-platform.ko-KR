---
title: 쿼리 서비스의 증분 로드
description: 증분 로드 기능은 익명 블록 및 스냅샷 기능을 모두 사용하여 일치하는 데이터를 무시하면서 데이터 레이크에서 데이터 웨어하우스로 데이터를 이동하는 거의 실시간 솔루션을 제공합니다.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 쿼리 서비스의 증분 로드

증분 로드 디자인 패턴은 데이터를 관리하는 솔루션입니다. 이 패턴은 마지막 로드 실행 이후 생성 또는 수정된 데이터 집합에 있는 정보만 처리합니다.

증분 로드에서는 익명 블록 및 스냅샷과 같은 Adobe Experience Platform 쿼리 서비스에서 제공하는 다양한 기능을 사용합니다. 이 디자인 패턴은 소스에서 이미 처리된 데이터를 건너뛸 때 처리 효율성을 높입니다. 스트리밍 및 배치 데이터 처리와 함께 사용할 수 있습니다.

이 문서에서는 증분 처리를 위한 디자인 패턴을 만드는 일련의 지침을 제공합니다. 이러한 단계를 템플릿으로 사용하여 고유한 증분 데이터 로드 쿼리를 만들 수 있습니다.

## 시작하기

이 문서 전체에서 SQL 예를 보려면 익명 블록 및 스냅샷 기능을 이해해야 합니다. 을 읽는 것이 좋습니다 [샘플 익명 블록 쿼리](./anonymous-block.md) 설명서 및 [스냅샷 절](../sql/syntax.md#snapshot-clause) 설명서.

이 안내서에서 사용되는 모든 용어에 대한 지침은 [SQL 구문 안내서](../sql/syntax.md).

## 데이터 증분 로드

아래 단계에서는 스냅샷과 익명 블록 기능을 사용하여 데이터를 생성하고 점진적으로 로드하는 방법을 보여 줍니다. 디자인 패턴은 고유한 쿼리 시퀀스의 템플릿으로 사용할 수 있습니다.

1 만들기 `checkpoint_log` 데이터를 성공적으로 처리하는 데 사용되는 가장 최근 스냅샷을 추적하는 테이블입니다. 추적 테이블(`checkpoint_log` 이 예에서) 먼저 를 `null` 데이터 세트를 점진적으로 처리하기 위해 입니다.

```SQL
DROP TABLE IF EXISTS checkpoint_log;
CREATE TABLE  checkpoint_log AS
SELECT
   cast(NULL AS string) process_name,
   cast(NULL AS string) process_status,
   cast(NULL AS string) last_snapshot_id,
   cast(NULL AS TIMESTAMP) process_timestamp
   WHERE false;
```

2 `checkpoint_log` 증분 처리가 필요한 데이터 세트에 대해 빈 레코드가 하나 있는 표 `DIM_TABLE_ABC` 는 아래 예에서 처리할 데이터 세트입니다. 첫 번째 처리 시 `DIM_TABLE_ABC`, `last_snapshot_id` 는 다음과 같이 초기화됩니다. `null`. 이렇게 하면 처음 및 그 이후에 점진적으로 전체 데이터 세트를 처리할 수 있습니다.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

3, 초기화 `DIM_TABLE_ABC_Incremental` 처리된 출력을 포함합니다. `DIM_TABLE_ABC`. 의 익명 블록 **필수** 아래 SQL 예제의 실행 섹션은 1~4단계에 설명된 대로 순차적으로 실행되어 데이터를 점진적으로 처리합니다.

1. 설정 `from_snapshot_id` 처리 시작 위치를 나타냅니다. 다음 `from_snapshot_id` 이 예제에서 는 `checkpoint_log` 와 함께 사용할 표 `DIM_TABLE_ABC`. 초기 실행 시 스냅샷 ID가 `null` 는 전체 데이터 세트가 처리됨을 의미합니다.
2. 설정 `to_snapshot_id` 소스 테이블의 현재 스냅샷 ID(`DIM_TABLE_ABC`). 이 예제에서는 소스 테이블의 메타데이터 테이블에서 질의됩니다.
3. 를 사용하십시오 `CREATE` 만들 키워드 `DIM_TABLE_ABC_Incremenal` 를 대상 테이블로 사용하십시오. 대상 테이블은 소스 데이터 세트(`DIM_TABLE_ABC`). 이렇게 하면 다음 사이에 소스 테이블에서 처리된 데이터를 사용할 수 있습니다 `from_snapshot_id` 및 `to_snapshot_id`: 대상 테이블에 점진적으로 추가할 수 있습니다.
4. 업데이트 `checkpoint_log` 테이블 `to_snapshot_id` 에 대해 `DIM_TABLE_ABC` 성공적으로 처리되었습니다.
5. 익명 블록의 순차적 실행 쿼리가 실패하면 **옵션** 예외 섹션이 실행됩니다. 그러면 오류가 반환되고 프로세스가 종료됩니다.

>[!NOTE]
>
>다음 `history_meta('source table name')` 는 데이터 집합에 있는 사용 가능한 스냅샷에 액세스하는 데 사용되는 편리한 방법입니다.

```SQL
$$ BEGIN
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                ON a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    CREATE TABLE DIM_TABLE_ABC_Incremental AS
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
 
INSERT INTO
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

4 아래 익명 블록 예제의 증분 데이터 로드 논리를 사용하여 소스 데이터 집합의 새 데이터(가장 최근 타임스탬프 이후)를 처리하여 일반 케이던스의 대상 테이블에 추가할 수 있습니다. 이 예제에서 데이터는 `DIM_TABLE_ABC` 처리 및 추가됨 `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` 는 두 가지 모두 `DIM_TABLE_ABC_Incremental` 및 `SELECT history_meta('DIM_TABLE_ABC')`.

```SQL
$$ BEGIN
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                ON a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
INSERT INTO
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

이 논리를 테이블에 적용하여 증분 로드를 수행할 수 있습니다.

## 만료된 스냅샷

>[!IMPORTANT]
>
>스냅숏 메타데이터는 다음 후에 만료됩니다. **2개** 일 수. 만료된 스냅샷은 위에 제공된 스크립트의 논리를 무효화합니다.

만료된 스냅숏 ID 문제를 해결하려면 익명 블록의 시작 부분에 다음 명령을 삽입합니다. 다음 코드 행은 `@from_snapshot_id` 가능한 한 빨리 `snapshot_id` 메타데이터.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

전체 코드 블록은 다음과 같습니다.

```SQL
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

## 다음 단계

이 문서를 읽은 후에는 익명 블록 및 스냅숏 기능을 사용하여 증분 로드를 수행하는 방법을 더 잘 이해하고 이 논리를 고유한 특정 쿼리에 적용할 수 있어야 합니다. 쿼리 실행에 대한 일반적인 지침은 [쿼리 서비스에서 쿼리 실행에 대한 안내서](../best-practices/writing-queries.md).
