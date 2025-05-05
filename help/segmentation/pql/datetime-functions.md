---
solution: Experience Platform
title: PQL 날짜 및 시간 함수
description: 날짜 및 시간 함수는 Profile Query Language(PQL) 내의 값에 대한 날짜 및 시간 작업을 수행하는 데 사용됩니다.
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 2%

---

# 날짜 및 시간 함수

날짜 및 시간 함수는 [!DNL Profile Query Language] (PQL) 내의 값에 대한 날짜 및 시간 작업을 수행하는 데 사용됩니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 이번 달

`currentMonth` 함수는 현재 월을 정수로 반환합니다.

**형식**

```sql
currentMonth()
```

**예**

다음 PQL 쿼리는 개인의 출생 월이 현재 월인지 확인합니다.

```sql
person.birthMonth = currentMonth()
```

## 월 가져오기

`getMonth` 함수는 지정된 타임스탬프를 기반으로 월을 정수로 반환합니다.

**형식**

```sql
{TIMESTAMP}.getMonth()
```

**예**

다음 PQL 쿼리는 개인의 생년월이 6월인지 확인합니다.

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

다음 PQL 쿼리는 제품이 올해 판매되었는지 확인합니다.

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

다음 PQL 쿼리는 개인의 출생연도가 1991, 1992, 1993, 1994 또는 1995년인지 확인합니다.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## 현재 날짜

`currentDayOfMonth` 함수는 달의 현재 요일을 정수로 반환합니다.

**형식**

```sql
currentDayOfMonth()
```

**예**

다음 PQL 쿼리는 개인의 생일이 해당 월의 현재 날짜와 일치하는지 확인합니다.

```sql
person.birthDay = currentDayOfMonth()
```

## 날짜 가져오기

`getDayOfMonth` 함수는 지정된 타임스탬프를 기반으로 일을 정수로 반환합니다.

**형식**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**예**

다음 PQL 쿼리는 항목이 그 달의 첫 15일 이내에 판매되었는지 확인합니다.

```sql
product.sale.getDayOfMonth() <= 15
```

## 발생

`occurs` 함수는 특정 타임스탬프 함수를 고정된 기간(부울)과 비교합니다.

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
| `{COMPARISON}` | 비교 연산자. 다음 연산자 중 하나가 될 수 있습니다. `>`, `>=`, `<`, `<=`, `=`, `!=`. 비교 함수에 대한 자세한 내용은 [비교 함수 문서](./comparison-functions.md)를 참조하십시오. |
| `{INTEGER}` | 음수가 아닌 정수. |
| `{TIME_UNIT}` | 시간 단위입니다. 다음 단어 중 하나가 될 수 있습니다. `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | 날짜를 비교할 시기를 설명하는 전치사. `before`, `after`, `from` 단어 중 하나일 수 있습니다. |
| `{TIME}` | 타임스탬프 리터럴(`today`, `now`, `yesterday`, `tomorrow`), 상대 시간 단위(`this`, `last` 또는 `next` 중 하나, 뒤에 시간 단위) 또는 타임스탬프 특성일 수 있습니다. |

>[!NOTE]
>
>`on` 단어 사용은 선택 사항입니다. `timestamp occurs on date(2019,12,31)`과(와) 같은 일부 조합의 가독성을 향상시킬 수 있습니다.

**예**

다음 PQL 쿼리는 항목이 지난 주에 판매되었는지 확인합니다.

```sql
product.saleDate occurs last week
```

다음 PQL 쿼리는 2015년 1월 8일부터 2017년 7월 1일 사이에 항목이 판매되었는지 확인합니다.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## 지금

`now`은(는) PQL 실행의 타임스탬프를 나타내는 예약어입니다.

**예**

다음 PQL 쿼리는 항목이 정확히 3시간 전에 판매되었는지 확인합니다.

```sql
product.saleDate occurs = 3 hours before now
```

## 오늘

`today`은(는) PQL 실행 날짜의 타임스탬프를 나타내는 예약어입니다.

**예**

다음 PQL 쿼리는 개인의 생일이 3일 전인지 확인합니다.

```sql
person.birthday occurs = 3 days before today
```

## 다음 단계

이제 날짜 및 시간 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
