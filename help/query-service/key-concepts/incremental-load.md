---
title: 쿼리 서비스의 증분 로드
description: 증분 로드 기능은 익명 블록 및 스냅샷 기능을 모두 사용하여 일치하는 데이터를 무시하면서 데이터 레이크에서 데이터 웨어하우스로 데이터를 이동하는 거의 실시간 솔루션을 제공합니다.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 65eeeb1df1d512c4cd6c67892905a63cc1cc4fc5
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 쿼리 서비스의 증분 로드

증분 로드 설계 패턴은 데이터 관리를 위한 솔루션입니다. 패턴은 마지막 로드 실행 이후 생성 또는 수정된 데이터 세트의 정보만 처리합니다.

증분 로드는 익명 블록 및 스냅샷과 같은 Adobe Experience Platform 쿼리 서비스에서 제공하는 다양한 기능을 사용합니다. 이러한 디자인 패턴은 소스에서 이미 처리된 데이터를 건너뛰므로 처리 효율성을 높입니다. 스트리밍과 일괄 데이터 처리 모두에서 사용할 수 있습니다.

이 문서에서는 증분 처리를 위한 디자인 패턴을 작성하는 일련의 지침을 제공합니다. 이러한 단계는 템플릿으로 사용하여 고유한 증분 데이터 로드 쿼리를 만들 수 있습니다.

## 시작하기

이 문서 전체에서 SQL 예제를 사용하려면 익명 블록 및 스냅샷 기능을 이해해야 합니다. [샘플 익명 블록 쿼리](./anonymous-block.md) 설명서 및 [스냅숏 절](../sql/syntax.md#snapshot-clause) 설명서를 읽는 것이 좋습니다.

이 안내서에서 사용되는 용어에 대한 자세한 내용은 [SQL 구문 안내서](../sql/syntax.md)를 참조하십시오.

## 증분 데이터 로드

아래 단계에서는 스냅샷 및 익명 블록 기능을 사용하여 데이터를 만들고 증분 로드하는 방법을 보여 줍니다. 디자인 패턴은 나만의 쿼리 시퀀스를 위한 템플릿으로 사용할 수 있습니다.

1. 데이터를 성공적으로 처리하는 데 사용된 최신 스냅숏을 추적하려면 `checkpoint_log` 테이블을 만드십시오. 데이터 집합을 증분 처리하려면 먼저 추적 테이블(`checkpoint_log`)을 `null`(으)로 초기화해야 합니다.

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

1. 증분 처리가 필요한 데이터 집합에 대해 하나의 빈 레코드로 `checkpoint_log` 테이블을 채웁니다. `DIM_TABLE_ABC`은(는) 아래 예에서 처리할 데이터 집합입니다. `DIM_TABLE_ABC`을(를) 처음 처리하는 경우 `last_snapshot_id`이(가) `null`(으)로 초기화됩니다. 이렇게 하면 전체 데이터 세트를 처음 처리할 때와 그 후에 증분 처리할 수 있습니다.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. `DIM_TABLE_ABC`에서 처리된 출력을 포함하도록 `DIM_TABLE_ABC_Incremental`을(를) 초기화합니다. 아래 SQL 예제의 **required** 실행 섹션에 있는 익명 블록은 1단계부터 4단계까지 설명된 대로 데이터를 점진적으로 처리하기 위해 순차적으로 실행됩니다.

   1. 처리가 시작되는 위치를 나타내는 `from_snapshot_id`을(를) 설정합니다. 이 예제의 `from_snapshot_id`은(는) `checkpoint_log` 테이블에서 `DIM_TABLE_ABC`과(와) 함께 사용하도록 쿼리되었습니다. 초기 실행 시 스냅숏 ID는 `null`입니다. 이는 전체 데이터 세트가 처리됨을 의미합니다.
   1. `to_snapshot_id`을(를) 원본 테이블(`DIM_TABLE_ABC`)의 현재 스냅숏 ID로 설정하십시오. 이 예제에서는 소스 테이블의 메타데이터 테이블에서 쿼리합니다.
   1. `CREATE` 키워드를 사용하여 `DIM_TABLE_ABC_Incremenal`을(를) 대상 테이블로 만드십시오. 대상 테이블은 원본 데이터 집합(`DIM_TABLE_ABC`)에서 처리된 데이터를 유지합니다. 이렇게 하면 `from_snapshot_id`과(와) `to_snapshot_id` 사이의 원본 테이블에서 처리된 데이터를 대상 테이블에 증분 추가할 수 있습니다.
   1. `DIM_TABLE_ABC`이(가) 성공적으로 처리한 원본 데이터의 `to_snapshot_id`(으)로 `checkpoint_log` 테이블을 업데이트하십시오.
   1. 익명 블록의 순차적으로 실행된 쿼리 중 하나라도 실패하면 **선택 사항** 예외 섹션이 실행됩니다. 오류를 반환하고 프로세스를 종료합니다.

   >[!NOTE]
   >
   >`history_meta('source table name')`은(는) 데이터 집합에서 사용 가능한 스냅숏에 액세스할 수 있는 편리한 방법입니다.

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

1. 아래 익명 블록 예제의 증분 데이터 로드 논리를 사용하여 (가장 최근 타임스탬프 이후) 소스 데이터 세트의 모든 새 데이터를 처리하고 정기적으로 대상 테이블에 추가할 수 있습니다. 이 예제에서는 `DIM_TABLE_ABC`에 대한 데이터 변경 내용이 처리되어 `DIM_TABLE_ABC_incremental`에 추가됩니다.

   >[!NOTE]
   >
   > `_ID`은(는) `DIM_TABLE_ABC_Incremental`과(와) `SELECT history_meta('DIM_TABLE_ABC')`의 기본 키입니다.

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

이 논리는 모든 테이블에 적용하여 증분 로드를 수행할 수 있습니다.

## 만료된 스냅샷

만료된 스냅샷 ID 문제를 해결하려면 익명 블록의 시작 부분에 다음 명령을 삽입합니다. 다음 코드 행은 메타데이터에서 사용 가능한 가장 빠른 `snapshot_id`을(를) 사용하여 `@from_snapshot_id`을(를) 재정의합니다.

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

이 문서를 읽으면 익명 블록 및 스냅샷 기능을 사용하여 증분 로드를 수행하는 방법을 더 잘 이해하고 이 논리를 고유한 특정 쿼리에 적용할 수 있습니다. 쿼리 실행에 대한 일반적인 지침은 [쿼리 서비스에서 쿼리 실행에 대한 안내서](../best-practices/writing-queries.md)를 참조하십시오.
