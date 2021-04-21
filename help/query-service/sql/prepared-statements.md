---
keywords: Experience Platform;home;popular topics;query service;Query service;prepared statements;preparted;sql;
solution: Experience Platform
title: 쿼리 서비스의 준비된 문
topic-legacy: prepared statements
description: SQL에서 준비된 문은 비슷한 쿼리 또는 업데이트를 서식 파일에 사용합니다. Adobe Experience Platform 쿼리 서비스는 매개 변수화된 쿼리를 사용하여 준비된 문을 지원합니다.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 9%

---

# 준비된 설명

SQL에서 준비된 문은 유사한 쿼리 또는 업데이트를 템플릿 지정하는 데 사용됩니다. Adobe Experience Platform [!DNL Query Service]은 매개 변수가 있는 쿼리를 사용하여 준비된 문을 지원합니다. 더 이상 쿼리를 반복해서 분석할 필요가 없으므로 이 기능을 사용하여 성능을 최적화할 수 있습니다.

## 준비된 문 사용

준비된 문을 사용할 때 다음 구문이 지원됩니다.

- [준비](#prepare)
- [실행](#execute)
- [할당 취소](#deallocate)

### 준비된 문 {#prepare} 준비

이 SQL 쿼리는 `PLAN_NAME`으로 지정된 이름으로 작성된 SELECT 쿼리를 저장합니다. 실제 값 대신 `$1` 등의 변수를 사용할 수 있습니다. 이 준비된 문은 현재 세션 중에 저장됩니다. 계획 이름은 **대/소문자를 구분하지 않습니다.**

#### SQL 형식

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 샘플 SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 준비된 문 {#execute} 실행

이 SQL 쿼리는 이전에 만든 준비된 문을 사용합니다.

#### SQL 형식

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 샘플 SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 준비된 문 {#deallocate} 할당 취소

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

| ID | 이름 | lastname | 생년월일 | 이메일 | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 앙투안 | 두부아 | 1967-03-14 | example2@example.com | 파리 | 프랑스 |
| 10002년 | 교코 | sakura | 1999-11-26 | example3@example.com | 도쿄 | 일본 |
| 10003 | 린스 | 페터슨 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004년 | aasir | 야카 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005년 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

다음 준비된 문을 사용하여 이 SQL 쿼리를 매개 변수화할 수 있습니다.

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

이제 다음 호출을 사용하여 준비된 문을 실행할 수 있습니다.

```sql
EXECUTE getIdRange(10000, 10005);
```

이 메시지가 호출되면 이전과 동일한 결과가 표시됩니다.

| ID | 이름 | lastname | 생년월일 | 이메일 | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 앙투안 | 두부아 | 1967-03-14 | example2@example.com | 파리 | 프랑스 |
| 10002년 | 교코 | sakura | 1999-11-26 | example3@example.com | 도쿄 | 일본 |
| 10003 | 린스 | 페터슨 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004년 | aasir | 야카 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005년 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

준비된 명령문 사용을 완료한 후 다음 호출을 사용하여 명령문을 할당 취소할 수 있습니다.

```sql
DEALLOCATE getIdRange;
```
