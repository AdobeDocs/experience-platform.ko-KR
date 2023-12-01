---
title: 쿼리 서비스의 익명 블록
description: 익명 블록은 Adobe Experience Platform 쿼리 서비스에서 지원하는 SQL 구문으로, 쿼리 시퀀스를 효율적으로 실행할 수 있습니다
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: b7de5d3b2ceba27f5e86d48078be484dcb6f7c4b
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# 쿼리 서비스의 익명 블록

Adobe Experience Platform 쿼리 서비스는 익명 블록을 지원합니다. 익명 블록 기능을 사용하면 순서대로 실행되는 하나 이상의 SQL 문을 연결할 수 있습니다. 또한 예외 처리 옵션을 사용할 수 있습니다.

익명 블록 기능은 일련의 작업 또는 쿼리를 수행하는 효율적인 방법입니다. 블록 내의 쿼리 체인을 템플릿으로 저장하고 특정 시간 또는 간격으로 실행되도록 예약할 수 있습니다. 이러한 쿼리는 데이터를 작성하고 추가하여 새 데이터 세트를 만들 수 있으며 일반적으로 종속성이 있는 곳에서 사용됩니다.

>[!IMPORTANT]
>
>현재 익명 블록을 사용하여 쿼리를 예약하는 것은 [!DNL Query Service] API. 다음 설명서를 참조하십시오. [api를 통한 쿼리 예약에 대한 전체 지침](../api/scheduled-queries.md).

이 표에서는 블록의 주요 섹션인 실행 및 예외 처리에 대한 분류를 제공합니다. 섹션은 키워드로 정의됩니다 `BEGIN`, `END`, 및 `EXCEPTION`.

| 섹션에 있는 마지막 항목이 될 필요가 없습니다 | 설명 |
|---|---|
| 실행 | 실행 가능한 섹션은 키워드로 시작합니다 `BEGIN` 키워드로 끝남 `END`. 내에 포함된 모든 문 세트 `BEGIN` 및 `END` 키워드는 순서대로 실행되며 시퀀스의 이전 쿼리가 완료될 때까지 후속 쿼리가 실행되지 않습니다. |
| 예외 처리 | 선택적 예외 처리 섹션은 키워드로 시작합니다 `EXCEPTION`. 실행 섹션의 SQL 문이 실패할 경우 예외를 catch하고 처리하는 코드가 포함되어 있습니다. 쿼리 중 하나라도 실패하면 전체 블록이 중지됩니다. |

블록은 실행 가능한 문이며 따라서 다른 블록 내에 중첩될 수 있다는 점에 주목할 필요가 있다.

>[!NOTE]
>
> 쿼리를 더 작은 데이터 세트에서 테스트하고 예상대로 작동하는지 확인하는 것이 좋습니다. 쿼리에 구문 오류가 있으면 예외가 throw되고 전체 블록이 중단됩니다. 쿼리의 무결성을 확인하면 쿼리를 연결할 수 있습니다. 이렇게 하면 블록을 작동시키기 전에 블록이 예상대로 작동하는지 확인할 수 있습니다.

## 샘플 익명 블록 쿼리

다음 쿼리는 SQL 문 체인의 예를 보여 줍니다. 다음을 참조하십시오. [쿼리 서비스의 SQL 구문](../sql/syntax.md) 사용된 SQL 구문에 대한 자세한 내용은 을 참조하십시오.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

아래 예에서는 `SET` 의 결과를 유지합니다. `SELECT` 지정한 로컬 변수에서 쿼리합니다. 변수의 범위가 익명 블록으로 지정됩니다.

스냅샷 ID는 로컬 변수(`@current_sid`). 그런 다음 다음 쿼리에서 동일한 데이터 세트/테이블의 SNAPSHOT을 기반으로 결과를 반환하는 데 사용됩니다.

데이터베이스 스냅숏은 SQL Server 데이터베이스의 읽기 전용 정적 보기입니다. 더 보기 [snapshot 절에 대한 정보](../sql/syntax.md#SNAPSHOT-clause) sql 구문 설명서를 참조하십시오.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 타사 클라이언트가 있는 익명 블록 {#third-party-clients}

특정 타사 클라이언트는 스크립트의 일부가 단일 문으로 처리되어야 함을 나타내기 위해 SQL 블록 전후에 별도의 식별자가 필요할 수 있습니다. 서드파티 클라이언트에서 쿼리 서비스를 사용할 때 오류 메시지가 표시되는 경우 SQL 블록 사용과 관련된 서드파티 클라이언트의 설명서를 참조하십시오.

예를 들어, **DbVisualizer** 를 사용하려면 구분 기호가 줄의 유일한 텍스트여야 합니다. DbVisualizer에서 시작 식별자의 기본값은 입니다. `--/` 최종 식별자의 경우 다음과 같습니다. `/`. DbVisualizer의 익명 블록의 예는 아래에 나와 있습니다.

```SQL
--/
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....;
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
/
```

특히 DbVisualizer의 경우 UI에 &quot;[!DNL Execute the complete buffer as one SQL statement]&quot;. 다음을 참조하십시오. [DbVisualizer 설명서](https://confluence.dbvis.com/display/UG120/Executing+Complex+Statements#ExecutingComplexStatements-UsingExecuteBuffer) 추가 정보.

## 다음 단계

이제 이 문서를 읽고 익명 블록과 그 구성 방법을 명확하게 이해할 수 있습니다. 다음을 읽으십시오. [쿼리 실행 안내서](../best-practices/writing-queries.md) 쿼리 작성에 대한 자세한 내용을 참조하십시오.

다음 내용도 읽어 보십시오. [증분 로드 디자인 패턴에 익명 블록을 사용하는 방법](./incremental-load.md) 쿼리 효율성을 높입니다.
