---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 쿼리 작성
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 쿼리 서비스에서 쿼리 실행에 대한 일반 지침

이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 쿼리를 작성할 때 알아야 할 중요한 세부 사항을 자세히 설명합니다.

쿼리 서비스에 사용되는 SQL 구문에 대한 자세한 내용은 SQL [구문 설명서를](../sql/syntax.md)참조하십시오.

## 쿼리 실행 모델

Adobe Experience Platform Query Service에는 두 가지 쿼리 실행 모델이 있습니다.인터랙티브한 요소와 비인터랙티브한 기능을 제공합니다. 대화형 실행은 비즈니스 인텔리전스 도구에서 쿼리 개발 및 보고서 생성에 사용되는 반면, 비대화형 실행은 데이터 처리 워크플로의 일부로서 더 큰 작업과 운영 쿼리에 사용됩니다.

### 대화형 쿼리 실행

쿼리는 쿼리 서비스 UI 또는 연결된 클라이언트를 [통해](../clients/overview.md)제출함으로써 대화식으로 실행할 수 있습니다. 연결된 클라이언트를 통해 쿼리 서비스를 실행할 때 제출된 쿼리가 반환되거나 시간 초과될 때까지 클라이언트와 쿼리 서비스 간에 활성 세션이 실행됩니다.

대화형 쿼리 실행에는 다음과 같은 제한이 있습니다.

| 매개 변수 | 제한 사항 |
| --------- | ---------- |
| 쿼리 시간 초과 | 10분 |
| 반환되는 최대 행 수 | 50,000 |
| 최대 동시 쿼리 | 5 |

>[!NOTE] 최대 행 제한을 무시하려면 쿼리에 `LIMIT 0` 포함하십시오. 쿼리 시간 초과(10분)는 여전히 적용됩니다.

기본적으로 대화형 쿼리의 결과는 클라이언트에 반환되며 지속되지 **않습니다** . 결과를 Experience Platform에서 데이터 집합으로 유지하려면 쿼리에 `CREATE TABLE AS SELECT` 구문을 사용해야 합니다.

### 비대화형 쿼리 실행

Query Service API를 통해 제출된 쿼리는 대화식으로 실행되지 않습니다. 비대화형 실행은 쿼리 서비스가 API 호출을 수신하고 쿼리를 수신한 순서대로 실행함을 의미합니다. 비대화형 쿼리는 항상 Experience Platform에서 새 데이터 세트를 생성하여 결과를 받거나 기존 데이터 세트에 새 행을 삽입하게 됩니다.

## 개체 내의 특정 필드에 액세스

쿼리의 개체 내 필드에 액세스하려면 점 표기법(`.`) 또는 대괄호 표기법(`[]`)을 사용할 수 있습니다. 다음 SQL 문은 점 표기법을 사용하여 `endUserIds` 개체를 `mcid` 개체 아래로 탐색합니다.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 분석 테이블의 이름입니다. |

다음 SQL 문은 대괄호 표기법을 사용하여 `endUserIds` 개체를 `mcid` 개체 아래로 탐색합니다.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 분석 테이블의 이름입니다. |

>[!NOTE] 각 표기법 유형은 동일한 결과를 반환하므로, 사용자가 선택하는 표기법은 사용자의 기본 설정에 따라 달라집니다.

위의 두 예제 쿼리 모두 단일 값이 아닌 분리된 개체를 반환합니다.

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

반환된 `endUserIds._experience.mcid` 객체에는 다음 매개 변수에 대한 해당 값이 포함됩니다.

- `id`
- `namespace`
- `primary`

열을 객체로만 선언하면 전체 객체를 문자열로 반환합니다. ID만 보려면 다음을 사용하십시오.

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 작은 따옴표, 큰 따옴표 및 작은 따옴표를 사용해야 하는 경우

이 섹션에서는 쿼리에서 작은 따옴표, 큰 따옴표 및 뒤에 따옴표를 사용하는 시기를 설명합니다.

### 작은 따옴표

텍스트 문자열을 만드는 데 단일 인용 부호(`'`)가 사용됩니다. 예를 들어 `SELECT` 문에서 이 값을 사용하여 결과의 정적 텍스트 값을 반환하고 `WHERE` 절에서 열의 컨텐츠를 평가할 수 있습니다.

다음 쿼리는 열에 대한 정적 텍스트 값(`'datasetA'`)을 선언합니다.

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

다음 쿼리는 WHERE 절에 단일 인용 부호 문자열(`'homepage'`)을 사용하여 특정 페이지에 대한 이벤트를 반환합니다.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### 큰따옴표

큰따옴표(`"`)는 공백이 있는 식별자를 선언하는 데 사용됩니다.

다음 쿼리는 한 열에 해당 식별자의 공백이 있을 때 지정된 열의 값을 반환하는 큰따옴표를 사용합니다.

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE] 큰 따옴표는 점 표기법 필드 액세스에는 사용할 **수 없습니다** .

### 인용 부호

뒤에 오는 따옴표는 도트 표기법 구문을 사용할 `` ` `` 때만 **** 예약된 열 이름을 escape하는 데 사용됩니다. 예를 들어 SQL에서 예약된 `order` 단어이므로 이 필드에 액세스하려면 뒤에 인용 부호를 사용해야 합니다 `commerce.order`.

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

후문도 숫자로 시작하는 필드에 액세스하는 데 사용됩니다. 예를 들어 필드에 액세스하려면 `30_day_value`역방향 따옴표 표기법을 사용해야 합니다.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

대괄호 표기법을 사용하는 경우에는 인용 부호가 **필요하지 않습니다** .

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## 다음 단계

이 문서를 읽음으로써 쿼리 서비스를 사용하여 쿼리를 작성할 때 몇 가지 중요한 고려 사항을 알게 되었습니다. SQL 구문을 사용하여 쿼리를 작성하는 방법에 대한 자세한 내용은 SQL 구문 [설명서를](../sql/syntax.md)참조하십시오.