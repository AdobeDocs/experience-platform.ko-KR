---
title: 쿼리 서비스의 익명 블록
description: 익명 블록은 Adobe Experience Platform 쿼리 서비스에서 지원하는 SQL 구문이므로 쿼리 시퀀스를 효율적으로 실행할 수 있습니다
exl-id: ec497475-9d2b-43aa-bcf4-75a430590496
source-git-commit: d3ea7ee751962bb507c91e1afea0da35da60a66d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 쿼리 서비스의 익명 블록

Adobe Experience Platform 쿼리 서비스는 익명 블록을 지원합니다. 익명 블록 기능을 사용하면 시퀀스로 실행되는 하나 이상의 SQL 문을 체인할 수 있습니다. 예외 처리 옵션도 허용합니다.

익명 블록 기능은 작업 또는 쿼리 시퀀스를 수행하는 효율적인 방법입니다. 블록 내의 쿼리 체인은 템플릿으로 저장될 수 있으며 특정 시간 또는 간격으로 실행되도록 예약할 수 있습니다. 이러한 쿼리는 새 데이터 세트를 만들기 위해 데이터를 쓰고 추가하는 데 사용할 수 있으며, 일반적으로 종속성이 있는 곳에서 사용됩니다.

>[!IMPORTANT]
>
>익명 블록을 사용하여 쿼리를 예약하는 것은 현재 [!DNL Query Service] API. 다음 문서를 참조하십시오. [api를 통한 쿼리 예약에 대한 전체 지침](../api/scheduled-queries.md).

이 표에서는 블록의 주 섹션을 설명합니다. 실행 및 예외 처리를 참조하십시오. 섹션은 키워드로 정의됩니다 `BEGIN`, `END`, 및 `EXCEPTION`.

| 섹션에 있는 마지막 항목이 될 필요가 없습니다 | 설명 |
|---|---|
| 실행 | 실행 가능한 섹션은 키워드로 시작됩니다 `BEGIN` 및 은 키워드로 끝납니다 `END`. 에 포함된 모든 문 집합 `BEGIN` 및 `END` 키워드는 순서대로 실행되며, 시퀀스의 이전 쿼리가 완료될 때까지 후속 쿼리가 실행되지 않습니다. |
| 예외 처리 | 선택적 예외 처리 섹션은 키워드로 시작됩니다 `EXCEPTION`. 실행 섹션의 SQL 문이 실패할 경우 예외를 catch 및 처리할 코드가 포함되어 있습니다. 쿼리가 실패하면 전체 블록이 중지됩니다. |

블록은 실행 가능한 문이므로 다른 블록 내에서 중첩될 수 있습니다.

>[!NOTE]
>
> 더 작은 데이터 세트에서 쿼리를 테스트하고 예상대로 작동하는지 확인하는 것이 좋습니다. 쿼리에 구문 오류가 있으면 예외가 발생하고 전체 블록이 중단됩니다. 쿼리의 무결성을 확인했으면 해당 쿼리의 체인을 시작할 수 있습니다. 이렇게 하면 블록이 작동하기 전에 예상대로 작동됩니다.

## 익명 블록 쿼리 샘플

다음 쿼리는 SQL 문 체인의 예를 보여줍니다. 자세한 내용은 [쿼리 서비스의 SQL 구문](../sql/syntax.md) 사용된 SQL 구문에 대한 자세한 내용은 문서를 참조하십시오.

```SQL
$$ BEGIN
    CREATE TABLE ADLS_TABLE_A AS SELECT * FROM ADLS_TABLE_1....;
    ....
    CREATE TABLE ADLS_TABLE_D AS SELECT * FROM ADLS_TABLE_C....; 
    EXCEPTION WHEN OTHER THEN SET @ret = SELECT 'ERROR';
END
$$;
```

아래 예에서는 `SET` 의 결과를 유지합니다. `SELECT` 지정된 로컬 변수에 있는 쿼리입니다. 변수 범위가 익명 블록으로 지정됩니다.

스냅샷 ID는 로컬 변수(`@current_sid`). 그런 다음 다음 다음 다음 쿼리에서 동일한 데이터 세트/테이블의 스냅샷을 기반으로 결과를 반환합니다.

데이터베이스 스냅숏은 SQL Server 데이터베이스의 읽기 전용 정적 보기입니다. 추가 정보 [스냅샷 절에 대한 정보](../sql/syntax.md#SNAPSHOT-clause) sql 구문 설명서를 참조하십시오.

```SQL
$$ BEGIN                                             
  SET @current_sid = SELECT parent_id  FROM (SELECT history_meta('your_table_name')) WHERE  is_current = true;
  CREATE temp table abcd_temp_table AS SELECT count(1) FROM your_table_name  SNAPSHOT SINCE @current_sid;                                                                                           
END
$$;
```

## 다음 단계

이 문서를 읽으면 이제 익명 블록과 블록의 구조를 명확하게 이해할 수 있습니다. [쿼리 실행에 대한 자세한 정보](../best-practices/writing-queries.md)쿼리 서비스에서 쿼리 실행에 대한 안내서를 참조하십시오.

또한 다음 내용을 읽어야 합니다 [증분 로드 디자인 패턴에 익명 블록 사용 방법](./incremental-load.md) 쿼리 효율성을 높입니다.
