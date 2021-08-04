---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;문제 해결 가이드;faq;문제 해결;
solution: Experience Platform
title: Query Service 문제 해결 안내서
topic-legacy: troubleshooting
description: 이 문서에서는 사용자가 발생하는 일반적인 오류 코드 및 가능한 원인에 대한 정보를 제공합니다.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 2b118228473a5f07ab7e2c744b799f33a4c44c98
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 6%

---

# [!DNL Query Service] 문제 해결 안내서

이 문서에서는 Query Service에 대해 자주 묻는 질문에 대한 답변을 제공하며 Query Service를 사용할 때 자주 표시되는 오류 코드 목록을 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

## 자주 묻는 질문

다음은 Query Service에 대해 자주 묻는 질문에 대한 답변 목록입니다.

### 쿼리의 메타데이터만 가져오려면 어떻게 해야 합니까?

쿼리의 메타데이터만 가져오려면 다음과 같이 0행을 반환하는 쿼리를 실행할 수 있습니다.

```sql
SELECT * FROM <table> WHERE 1=0
```

이 쿼리는 지정된 테이블에 대한 메타데이터만 반환합니다.

### CTAS(Create Table as Select) 쿼리를 구체화하지 않고 빠르게 반복하려면 어떻게 해야 합니까?

임시 테이블을 만들어 사용할 수 있도록 구체화하기 전에 쿼리를 빠르게 반복 및 실험할 수 있습니다. 임시 테이블을 사용하여 쿼리가 작동하는지 확인할 수도 있습니다.

예를 들어 임시 테이블을 만들 수 있습니다.

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

그런 다음 임시 테이블을 다음과 같이 사용할 수 있습니다.

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

### 시계열 데이터를 필터링하려면 어떻게 해야 합니까?

시계열 데이터를 사용하여 쿼리할 때는 가능한 한 빨리 타임스탬프 필터를 사용하여 보다 정확한 분석을 해야 합니다.

타임스탬프 필터 사용의 예는 다음과 같습니다.

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

### 와일드카드를 사용해야 합니까? 예: * 를 사용하여 데이터 세트에서 모든 행을 가져와야 합니까?

와일드카드를 사용하여 행의 모든 데이터를 가져올 수 없습니다. Query Service는 기존 행 기반 저장소 시스템이 아니라 **열 형식 저장소**&#x200B;로 처리되어야 하기 때문입니다.

## REST API 오류

| HTTP 상태 코드 | 설명 | 가능한 원인 |
| ---------------- | ----------- | --------------- |
| 400 | 잘못된 요청 | 잘못된 쿼리 또는 잘못된 쿼리 |
| 401년 | 인증 실패 | 잘못된 인증 토큰 |
| 500 | 내부 서버 오류 | 내부 시스템 장애 |

## PostgreSQL API 오류

| 오류 코드 | 연결 상태 | 설명 | 가능한 원인 |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | N/A | 지원되지 않는 메시지 유형 | 지원되지 않는 메시지 유형 |
| **28P01** | 시작 - 인증 | 잘못된 암호 | 잘못된 인증 토큰 |
| **28000** | 시작 - 인증 | 잘못된 인증 유형 | 권한 부여 형식이 잘못되었습니다. `AuthenticationCleartextPassword`이어야 합니다. |
| **42P12** | 시작 - 인증 | 테이블을 찾을 수 없습니다. | 사용할 테이블을 찾을 수 없습니다. |
| **42601** | 쿼리 | 구문 오류 | 명령 또는 구문 오류가 잘못되었습니다. |
| **42P01** | 쿼리 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다 |
| **42P07** | 쿼리 | 테이블이 존재함 | 이름이 같은 테이블이 이미 있습니다(CREATE TABLE). |
| **53400** | 쿼리 | LIMIT가 최대값을 초과합니다. | 사용자가 100,000보다 큰 LIMIT 절을 지정했습니다. |
| **53400** | 쿼리 | 문 시간 초과 | 제출된 라이브 명령문은 최대 10분 이상 걸렸습니다 |
| **58000** | 쿼리 | 시스템 오류 | 내부 시스템 장애 |
| **0A000** | 쿼리/명령 | 지원되지 않음 | 쿼리/명령의 기능/기능은 지원되지 않습니다 |
| **42501** | 테이블 쿼리 삭제 | 쿼리 서비스에서 만들지 않은 테이블 삭제 | 삭제되는 테이블이 `CREATE TABLE` 문을 사용하여 쿼리 서비스에서 만들지 않았습니다 |
| **42501** | 테이블 쿼리 삭제 | 인증된 사용자가 만들지 않은 테이블 | 삭제되는 테이블은 현재 로그인한 사용자가 만들지 않았습니다 |
| **42P01** | 테이블 쿼리 삭제 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다 |
| **42P12** | 테이블 쿼리 삭제 | `dbName`에 대한 테이블을 찾을 수 없습니다. `dbName` 확인 | 현재 데이터베이스에 테이블이 없습니다. |
