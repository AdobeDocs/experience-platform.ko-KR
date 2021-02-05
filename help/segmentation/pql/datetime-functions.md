---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;날짜 및 시간 함수;datetime 함수;date;time
solution: Experience Platform
title: PQL 날짜 및 시간 함수
topic: developer guide
description: 날짜 및 시간 함수는 PQL(프로필 쿼리 언어) 내의 값에 대한 날짜 및 시간 작업을 수행하는 데 사용됩니다.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 4%

---


# 날짜 및 시간 함수

날짜 및 시간 함수는 [!DNL Profile Query Language](PQL) 내의 값에 대한 날짜 및 시간 작업을 수행하는 데 사용됩니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)에서 확인할 수 있습니다.

## 현재 달

`currentMonth` 함수는 현재 월을 정수로 반환합니다.

**형식**

```sql
currentMonth()
```

**예**

다음 PQL 쿼리는 개인의 생년월일이 현재 월인지 확인합니다.

```sql
person.birthMonth = currentMonth()
```

## 월 다운로드

`getMonth` 함수는 지정된 타임스탬프를 기반으로 월을 정수로 반환합니다.

**형식**

```sql
{TIMESTAMP}.getMonth()
```

**예**

다음 PQL 쿼리는 개인의 생년월일이 6월인지 확인합니다.

```sql
person.birthdate.getMonth() = 6
```

## 올해

`currentYear` 함수는 현재 연도를 정수로 반환합니다.

**형식**

```sql
currentYear()
```

**예**

다음 PQL 쿼리는 제품이 현재 연도에 판매되었는지 확인합니다.

```sql
product.saleYear = currentYear()
```

## 연도 가져오기

`getYear` 함수는 지정된 타임스탬프를 기반으로 연도를 정수로 반환합니다.

**형식**

```sql
{TIMESTAMP}.getYear()
```

**예**

다음 PQL 쿼리는 1991년, 1992년, 1993년, 1994년 또는 1995년에 출생한 사람의 연도를 확인합니다.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 현재 날짜

`currentDayOfMonth` 함수는 현재 날짜를 정수로 반환합니다.

**형식**

```sql
currentDayOfMonth()
```

**예**

다음 PQL 쿼리는 개인의 생년월일이 해당 월의 현재 요일과 일치하는지 확인합니다.

```sql
person.birthDay = currentDayOfMonth()
```

## 월 기준 가져오기

`getDayOfMonth` 함수는 지정된 타임스탬프를 기반으로 날짜를 정수로 반환합니다.

**형식**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**예**

다음 PQL 쿼리는 해당 제품이 해당 월의 첫 15일 이내에 판매되었는지 확인합니다.

```sql
product.sale.getDayOfMonth() <= 15
```

## 발생

`occurs` 함수는 지정된 타임스탬프 함수를 고정 기간과 비교합니다.

**형식**

`occurs` 함수는 다음 형식을 사용하여 작성할 수 있습니다.

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| 인수 | 설명 |
| --------- | ----------- |
| `{COMPARISON}` | 비교 연산자입니다. 다음 연산자 중 하나일 수 있습니다.`>`, `>=`, `<`, `<=`, `=`, `!=` 비교 함수에 대한 자세한 내용은 [비교 함수 문서](./comparison-functions.md)에서 확인할 수 있습니다. |
| `{INTEGER}` | 음수가 아닌 정수입니다. |
| `{TIME_UNIT}` | 시간 단위 다음 단어 중 하나일 수 있습니다.`millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia``month(s)` |
| `{DIRECTION}` | 날짜를 비교할 시기를 설명하는 사전 위치입니다. 다음 단어 중 하나일 수 있습니다.`before`, `after`, `from`. |
| `{TIME}` | 타임스탬프 리터럴(`today`, `now`, `yesterday`, `tomorrow`), 상대 시간 단위(`this` 중 하나, `last` 또는 `next` 뒤에 시간 단위) 또는 timestamp 특성이 될 수 있습니다. |

>[!NOTE]
>
>단어 `on`의 사용은 선택 사항입니다. `timestamp occurs on date(2019,12,31)`과 같은 일부 조합의 가독성을 높이기 위해 필요합니다.

**예**

다음 PQL 쿼리는 지난 주에 항목이 판매되었는지 확인합니다.

```sql
product.saleDate occurs last week
```

다음 PQL 쿼리는 2015년 1월 8일부터 2017년 7월 1일 사이에 항목이 판매되었는지 확인합니다.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 바로 지금입니다

`now` PQL 실행의 타임스탬프를 나타내는 예약된 단어입니다.

**예**

다음 PQL 쿼리는 항목이 정확히 3시간 전에 판매되었는지 확인합니다.

```sql
product.saleDate occurs = 3 hours before now
```

## 오늘

`today` 는 PQL 실행 시작일의 타임스탬프를 나타내는 예약된 단어입니다.

**예**

다음 PQL 쿼리는 개인의 생일이 3일 전인지 확인합니다.

```sql
person.birthday occurs = 3 days before today
```

## 다음 단계

날짜 및 시간 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md)를 참조하십시오.
