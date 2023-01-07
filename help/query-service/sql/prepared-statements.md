---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;준비된 문;준비된;sql;
solution: Experience Platform
title: 쿼리 서비스의 준비된 문
description: SQL에서 준비된 문은 유사한 쿼리 또는 업데이트를 서식 지정하는 데 사용됩니다. Adobe Experience Platform 쿼리 서비스는 매개 변수가 있는 쿼리를 사용하여 준비된 문을 지원합니다.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 11%

---

# 준비된 설명

SQL에서 준비된 문은 유사한 쿼리 또는 업데이트를 템플릿화하는 데 사용됩니다. Adobe Experience Platform [!DNL Query Service] 매개 변수화된 쿼리를 사용하여 준비된 문을 지원합니다. 이렇게 하면 더 이상 쿼리를 반복적으로 재구문 분석할 필요가 없으므로 성능을 최적화할 수 있습니다.

## 준비된 문 사용

준비된 구문을 사용할 때 다음 구문이 지원됩니다.

- [준비](#prepare)
- [실행](#execute)
- [할당 취소](#deallocate)

### 준비된 설명 준비 {#prepare}

이 SQL 쿼리는 이름이 `PLAN_NAME`. 다음과 같은 변수를 사용할 수 있습니다. `$1` 실제 값 대신. 이 준비된 문은 현재 세션 중에 저장됩니다. 계획 이름은 다음과 같습니다 **not** 대/소문자를 구분합니다.

#### SQL 형식

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 샘플 SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 준비된 문 실행 {#execute}

이 SQL 쿼리는 이전에 만들어진 준비된 문을 사용합니다.

#### SQL 형식

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 샘플 SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 준비된 문 할당 취소 {#deallocate}

이 SQL 쿼리는 명명된 준비된 문을 삭제하는 데 사용됩니다.

#### SQL 형식

```sql
DEALLOCATE {PLAN_NAME}
```

#### 샘플 SQL

```sql
DEALLOCATE test;
```

## 준비된 문을 사용한 흐름 예

처음에는 다음과 같은 SQL 쿼리를 사용할 수 있습니다.

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

위의 SQL 쿼리는 다음 응답을 반환합니다.

| ID | 이름 | lastname | 생일 | 이메일 | city | 국가 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 앙투안 | 두부아 | 1967-03-14 | example2@example.com | 파리 | 프랑스 |
| 10002 | 교코 | 사쿠라 | 1999-11-26 | example3@example.com | 도쿄 | 일본 |
| 10003 | 리누스 | 페터슨 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004 | 아사르 | 허타카 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

다음 준비 문을 사용하여 이 SQL 쿼리를 매개 변수화할 수 있습니다.

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

이제 다음 호출을 사용하여 준비된 문을 실행할 수 있습니다.

```sql
EXECUTE getIdRange(10000, 10005);
```

이 메서드가 호출되면 이전과 정확히 동일한 결과가 표시됩니다.

| ID | 이름 | lastname | 생일 | 이메일 | city | 국가 |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 앙투안 | 두부아 | 1967-03-14 | example2@example.com | 파리 | 프랑스 |
| 10002 | 교코 | 사쿠라 | 1999-11-26 | example3@example.com | 도쿄 | 일본 |
| 10003 | 리누스 | 페터슨 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004 | 아사르 | 허타카 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

준비된 명령문 사용을 완료한 후 다음 호출을 사용하여 명령문을 할당 취소할 수 있습니다.

```sql
DEALLOCATE getIdRange;
```
