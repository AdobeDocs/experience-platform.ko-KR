---
keywords: Experience Platform;home;popular topics;query service;Query service;prepared statements;prepared;sql;
solution: Experience Platform
title: 준비된 설명
topic: prepared statements
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 8%

---


# 준비된 설명

SQL에서는 유사한 쿼리 또는 업데이트를 템플릿 지정하는 데 준비된 문을 사용합니다. Adobe Experience Platform은 매개 변수화된 쿼리를 사용하여 준비된 문을 [!DNL Query Service] 지원합니다. 더 이상 쿼리를 반복해서 분석할 필요가 없으므로 이 기능을 사용하여 성능을 최적화할 수 있습니다.

## 준비된 문 사용

준비된 문을 사용할 때 다음 구문이 지원됩니다.

- [준비](#prepare)
- [실행](#execute)
- [할당 취소](#deallocate)

### 준비된 설명 준비 {#prepare}

이 SQL 쿼리는 지정된 이름으로 작성된 SELECT 쿼리를 저장합니다 `PLAN_NAME`. 실제 값 대신 변수 `$1` 등 변수를 사용할 수 있습니다. 이 준비된 문은 현재 세션 중에 저장됩니다. 플랜 이름은 대소문자를 구분하지 **않습니다** .

#### SQL 형식

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 샘플 SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 준비된 문 실행 {#execute}

이 SQL 쿼리는 이전에 생성된 준비된 문을 사용합니다.

#### SQL 형식

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 샘플 SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 준비된 문 할당 취소 {#deallocate}

이 SQL 쿼리는 준비된 명명된 문을 삭제하는 데 사용됩니다.

#### SQL 형식

```sql
DEALLOCATE {PLAN_NAME}
```

#### 샘플 SQL

```sql
DEALLOCATE test;
```

## 준비된 문을 사용한 흐름 예

처음에 SQL 쿼리를 사용할 수 있습니다(예: 아래 쿼리).

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

위의 SQL 쿼리는 다음 응답을 반환합니다.

| ID | 이름 | lastname | 생년월일 | 이메일 | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | antoine | 두부아 | 1967-03-14 | example2@example.com | Paris | 교구 |
| 10002 | 파리 | 사쿠라 | 1999-11-26 | stabilexample3@example.com | 도쿄 | 일본 |
| 10003 | 린스 | 페터슨 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004 | aasir | 야카 | 1976-12-17 | 이 | 나이로비 | 케냐 |
| 10005 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

다음 준비된 문을 사용하여 이 SQL 쿼리를 매개 변수화할 수 있습니다.

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

이제 다음 호출을 사용하여 준비된 문을 실행할 수 있습니다.

```sql
EXECUTE getIdRange(10000, 10005);
```

이 메시지가 호출되면 이전과 동일한 결과가 표시됩니다.

| ID | 이름 | lastname | 앙금 날짜 | 이메일 | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | 앙example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 이 | 두부아 | 1967-03-14 | example2@example.com | 생년월일 | 프랑스 |
| 10002 | 파리 | 이름 | 1999-11-26 | 프랑스 | 도쿄 | 일본 |
| 10003 | 린스 | 페터슨 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004 | aasir | 야카 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005 | 페르난도 | 프랑스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

준비된 명령문 사용을 완료한 후 다음 호출을 사용하여 명령문을 할당 취소할 수 있습니다.

```sql
DEALLOCATE getIdRange;
```
