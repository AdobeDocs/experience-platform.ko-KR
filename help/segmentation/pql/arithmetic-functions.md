---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;산술 함수;산술;
solution: Experience Platform
title: PAL 산술 함수
description: 산술 함수는 PQL(프로필 쿼리 언어)의 값에 대한 기본 계산을 수행하는 데 사용됩니다.
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 산술 함수

산술 함수는 [!DNL Profile Query Language] (PQL). 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에

다음 `+` (추가) 함수는 두 인수 표현식의 합계를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} + {NUMBER}
```

**예**

다음 PQL 쿼리는 두 가지 서로 다른 제품의 가격을 합합니다.

```sql
product1.price + product2.price
```

## 곱하기

다음 `*` (곱하기) 함수는 두 인수 표현식의 제품을 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} * {NUMBER}
```

**예**

다음 PQL 질의에서는 재고 제품 및 제품 가격을 찾아 제품의 총값을 찾습니다.

```sql
product.inventory * product.price
```

## 빼기

다음 `-` (빼기) 함수는 두 인수 표현식의 차이를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} - {NUMBER}
```

**예**

다음 PQL 쿼리는 서로 다른 두 제품 간의 가격 차이를 찾습니다.

```sql
product1.price - product2.price
```

## 나누기

다음 `/` (division) 함수는 두 인수 표현식의 따옴표를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} / {NUMBER}
```

**예**

다음 PQL 질의는 판매된 총 제품과 총 획득된 금액 사이의 수량을 찾아 품목당 평균 원가를 확인합니다.

```sql
totalProduct.price / totalProduct.sold
```

## 나머지

다음 `%` (modulo/additional) 함수는 두 인수 표현식을 나눈 후 나머지를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} % {NUMBER}
```

**예**

다음 PQL 쿼리는 개인의 나이가 5명으로 나눌 수 있는지 확인합니다.

```sql
person.age % 5 = 0
```

## 다음 단계

이제 산술 함수에 대해 배웠으므로 PQL 쿼리 내에서 이 함수를 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md).
