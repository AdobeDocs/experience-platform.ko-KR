---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 준비된 설명
topic: prepared statements
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# 준비된 설명

SQL에서 준비된 문은 유사한 쿼리 또는 업데이트를 템플릿 지정하는 데 사용됩니다. Adobe Experience Platform 쿼리 서비스는 매개 변수화된 쿼리를 사용하여 준비된 문을 지원합니다. 더 이상 쿼리를 여러 번 다시 구문 분석할 필요가 없으므로 성능을 최적화하는 데 사용할 수 있습니다.

## 준비된 문 사용

준비된 문을 사용할 때 다음 구문이 지원됩니다.

- [준비](#prepare)
- [실행](#execute)
- [할당 취소](#deallocate)

### 준비된 설명 준비 {#prepare}

이 SQL 쿼리는 지정된 이름으로 작성된 SELECT 쿼리를 `PLAN_NAME`저장합니다. 실제 값 대신 와 같은 변수를 사용할 `$1` 수 있습니다. 이 준비된 문은 현재 세션 중에 저장됩니다. 플랜 이름은 대소문자를 구분하지 **않습니다** .

#### SQL 포맷

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### 샘플 SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### 준비된 문 실행 {#execute}

이 SQL 쿼리는 이전에 만든 준비된 문을 사용합니다.

#### SQL 포맷

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### 샘플 SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### 준비된 문 할당 취소 {#deallocate}

이 SQL 쿼리는 준비된 명명된 문을 삭제하는 데 사용됩니다.

#### SQL 포맷

```sql
DEALLOCATE {PLAN_NAME}
```

#### 샘플 SQL

```sql
DEALLOCATE test;
```

## 준비된 문을 사용하는 예제 흐름

처음에는 아래 SQL 쿼리와 같은 SQL 쿼리를 사용할 수 있습니다.

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

위의 SQL 쿼리는 다음 응답을 반환합니다.

| ID | 이름 | lastname | 생년월일 | 이메일 | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 앙투안 | 두부아 | 1967-03-14 | example2@example.com | 파리 | 프랑스 |
| 10002 | 교코 | 사쿠라 | 1999-11-26 | example3@example.com | 도쿄 | 일본 |
| 10003 | 린스 | 페터손 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004 | aasir | 관자 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

이 SQL 쿼리는 다음 준비 문을 사용하여 매개 변수화할 수 있습니다.

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

이제 준비된 문은 다음 호출을 사용하여 실행할 수 있습니다.

```sql
EXECUTE getIdRange(10000, 10005);
```

이 메시지가 호출되면 전과 정확히 동일한 결과가 표시됩니다.

| ID | 이름 | lastname | 생년월일 | 이메일 | city | country |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | 알렉산더 | 데이비스 | 1993-09-15 | example@example.com | 밴쿠버 | 캐나다 |
| 10001 | 앙투안 | 두부아 | 1967-03-14 | example2@example.com | 파리 | 프랑스 |
| 10002 | 교코 | 사쿠라 | 1999-11-26 | example3@example.com | 도쿄 | 일본 |
| 10003 | 린스 | 페터손 | 1982-06-03 | example4@example.com | 스톡홀름 | 스웨덴 |
| 10004 | aasir | 관자 | 1976-12-17 | example5@example.com | 나이로비 | 케냐 |
| 10005 | 페르난도 | 리오스 | 2002-07-30 | example6@example.com | 산티아고 | 칠레 |

준비된 문 사용을 완료한 후 다음 호출을 사용하여 문을 할당 취소할 수 있습니다.

```sql
DEALLOCATE getIdRange;
```
