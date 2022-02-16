---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;문제 해결 가이드;faq;문제 해결;
solution: Experience Platform
title: Query Service 문제 해결 안내서
topic-legacy: troubleshooting
description: 이 문서에서는 사용자가 발생하는 일반적인 오류 코드 및 가능한 원인에 대한 정보를 제공합니다.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: 03cd013e35872bcc30c68508d9418cb888d9e260
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 3%

---

# [!DNL Query Service] 문제 해결 안내서

이 문서에서는 Query Service에 대해 자주 묻는 질문에 대한 답변을 제공하며 Query Service를 사용할 때 자주 표시되는 오류 코드 목록을 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결은 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

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

### 시간대를 UTC 타임스탬프에서 및 로 변경하려면 어떻게 해야 합니까?

Adobe Experience Platform은 UTC(Coordinated Universal Time) 타임스탬프 형식으로 데이터를 유지합니다. UTC 형식의 예는 다음과 같습니다 `2021-12-22T19:52:05Z`

Query Service는 지정된 타임스탬프를 UTC 형식으로 변환하기 위한 기본 제공 SQL 함수를 지원합니다. 둘 다 `to_utc_timestamp()` 그리고 `from_utc_timestamp()` 메서드는 두 가지 매개 변수를 사용합니다. timestamp 및 timezone.

| 매개 변수 | 설명 |
|---|---|
| 타임스탬프 | 타임스탬프는 UTC 형식 또는 간단한 형식으로 쓸 수 있습니다 `{year-month-day}` 형식 지정 시간을 제공하지 않으면 기본값은 지정된 날의 아침에 자정입니다. |
| 표준 시간대 | 시간대는 `{continent/city})` 형식 지정 이 코드에 있는 대로 인식된 시간대 코드 중 하나여야 합니다. [공용 도메인 TZ 데이터베이스](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### UTC 타임스탬프로 변환

다음 `to_utc_timestamp()` 메서드는 지정된 매개 변수를 해석하고 변환합니다 **로컬 시간대의 타임스탬프로** UTC 형식입니다. 예를 들어, 서울의 시간대는 대한민국 UTC/GMT +9시간입니다. 날짜 전용 타임스탬프를 제공하여 메서드는 오전 자정 기본값을 사용합니다. 타임스탬프 및 시간대는 해당 지역의 시간에서 로컬 지역의 UTC 타임스탬프로 변환됩니다.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

쿼리가 사용자의 현지 시간에 타임스탬프를 반환합니다. 이 경우 서울 전날인 3시 3분이 9시간 앞입니다.

```
2021-08-30 15:00:00
```

다른 예로, 주어진 타임스탬프가 `2021-07-14 12:40:00.0` 대상 `Asia/Seoul` 시간대, 반환된 UTC 타임스탬프는 `2021-07-14 03:40:00.0`

Query Service UI에 제공된 콘솔 출력은 사람이 읽을 수 있는 형식입니다.

```
8/30/2021, 3:00 PM
```

### UTC 타임스탬프에서 변환

다음 `from_utc_timestamp()` 메서드는 지정된 매개 변수를 해석합니다 **로컬 시간대의 타임스탬프에서** 및 은 UTC 형식으로 원하는 영역의 상응하는 타임스탬프를 제공합니다. 아래 예에서 시간은 사용자의 로컬 시간대에서 오후 2시 40분입니다. 변수로 전달된 Seoul 시간대 는 로컬 시간보다 9시간 앞서 있습니다.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

쿼리는 매개 변수로 전달된 시간대의 UTC 형식 타임스탬프를 반환합니다. 결과는 쿼리를 실행한 시간대보다 9시간 빠릅니다.

```
8/31/2021, 11:40 PM
```

### 시계열 데이터를 필터링하려면 어떻게 해야 합니까?

시계열 데이터를 사용하여 쿼리할 때는 가능한 한 빨리 타임스탬프 필터를 사용하여 보다 정확한 분석을 해야 합니다.

>[!NOTE]
>
> 날짜 문자열 **반드시** 형식을 사용해야 합니다. `yyyy-mm-ddTHH24:MM:SS`.

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

와일드카드를 사용하여 행의 모든 데이터를 가져올 수 없습니다. 쿼리 서비스는 **열 형식 저장소** 기존 행 기반 스토어 시스템 대신

### 사용해야 합니까 `NOT IN` 내 SQL 쿼리에서?

다음 `NOT IN` 연산자는 다른 테이블이나 SQL 문에서 찾을 수 없는 행을 검색하는 데 종종 사용됩니다. 이 연산자는 성능 속도를 저하할 수 있으며 비교 중인 열이 수락되면 예기치 않은 결과를 반환할 수 있습니다 `NOT NULL`또는 레코드 수가 많습니다.

를 사용하는 대신 `NOT IN`, 다음 중 하나를 사용할 수 있습니다. `NOT EXISTS` 또는 `LEFT OUTER JOIN`.

예를 들어 다음 테이블을 생성한 경우

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

를 사용하는 경우 `NOT EXISTS` 연산자인 경우 `NOT IN` 다음 쿼리를 사용하여 연산자 사용:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

또는, `LEFT OUTER JOIN` 연산자를 사용할 경우 `NOT IN` 다음 쿼리를 사용하여 연산자 사용:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

### 올바른 사용 방법은 무엇입니까? `OR` 및 `UNION` 연산자?

### 을 올바로 사용합니까? `CAST` 연산자를 사용하여 SQL 쿼리에서 내 타임스탬프를 변환하시겠습니까?

를 사용할 때 `CAST` 연산자를 사용하여 타임스탬프를 변환하려면 날짜를 모두 포함해야 합니다 **및** 시간

예를 들어, 아래와 같이 시간 구성 요소가 없으면 오류가 발생합니다.

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

의 올바른 사용 `CAST` 연산자는 다음과 같습니다.

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

### 쿼리 결과를 CSV 파일로 다운로드하려면 어떻게 해야 합니까?

Query Service가 직접 제공하는 기능이 아닙니다. 그러나 [!DNL PostgreSQL] 데이터베이스 서버에 연결하는 데 사용되는 클라이언트에 기능이 있습니다. SELECT 쿼리의 응답을 CSV 파일로 작성하고 다운로드할 수 있습니다. 이 프로세스에 대한 설명을 보려면 사용 중인 유틸리티 또는 타사 도구의 설명서를 참조하십시오.

## REST API 오류

| HTTP 상태 코드 | 설명 | 가능한 원인 |
| ---------------- | ----------- | --------------- |
| 400 | 잘못된 요청 | 잘못된 쿼리 또는 잘못된 쿼리 |
| 401년 | 인증 실패 | 잘못된 인증 토큰 |
| 500 | 내부 서버 오류 | 내부 시스템 장애 |

## PostgreSQL API 오류

| 오류 코드 | 연결 상태 | 설명 | 가능한 원인 |
| ---------- | ---------------- | ----------- | -------------- |
| **08P01** | 해당 없음 | 지원되지 않는 메시지 유형 | 지원되지 않는 메시지 유형 |
| **28P01** | 시작 - 인증 | 잘못된 암호 | 잘못된 인증 토큰 |
| **28000** | 시작 - 인증 | 잘못된 인증 유형 | 권한 부여 형식이 잘못되었습니다. 반드시 `AuthenticationCleartextPassword`. |
| **42P12** | 시작 - 인증 | 테이블을 찾을 수 없습니다. | 사용할 테이블을 찾을 수 없습니다. |
| **42601** | 쿼리 | 구문 오류 | 명령 또는 구문 오류가 잘못되었습니다. |
| **42P01** | 쿼리 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다 |
| **42P07** | 쿼리 | 테이블이 존재함 | 이름이 같은 테이블이 이미 있습니다(CREATE TABLE). |
| **53400** | 쿼리 | LIMIT가 최대값을 초과합니다. | 사용자가 100,000보다 큰 LIMIT 절을 지정했습니다. |
| **53400** | 쿼리 | 문 시간 초과 | 제출된 라이브 명령문은 최대 10분 이상 걸렸습니다 |
| **58000** | 쿼리 | 시스템 오류 | 내부 시스템 장애 |
| **0A000** | 쿼리/명령 | 지원되지 않음 | 쿼리/명령의 기능/기능은 지원되지 않습니다 |
| **42501** | 테이블 쿼리 삭제 | 쿼리 서비스에서 만들지 않은 테이블 삭제 | 삭제되는 테이블이 `CREATE TABLE` statement |
| **42501** | 테이블 쿼리 삭제 | 인증된 사용자가 만들지 않은 테이블 | 삭제되는 테이블은 현재 로그인한 사용자가 만들지 않았습니다 |
| **42P01** | 테이블 쿼리 삭제 | 테이블을 찾을 수 없음 | 쿼리에 지정된 테이블을 찾을 수 없습니다 |
| **42P12** | 테이블 쿼리 삭제 | 에 대한 테이블을 찾을 수 없습니다. `dbName`: 확인 `dbName` | 현재 데이터베이스에 테이블이 없습니다. |
