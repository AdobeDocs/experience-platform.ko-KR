---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;pql;PQL;프로필 쿼리 언어;산술 함수;산술 함수;
solution: Experience Platform
title: PAL 산술 함수
description: 산술 함수는 프로필 쿼리 언어(PQL)의 값에 대한 기본 계산을 수행하는 데 사용됩니다.
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 5%

---

# 산술 함수

산술 함수는 의 값에 대한 기본 계산을 수행하는 데 사용됩니다. [!DNL Profile Query Language] (PQL). 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에

다음 `+` (추가) 함수는 두 인수 표현식의 합계를 찾는 데 사용합니다.

**형식**

```sql
{NUMBER} + {NUMBER}
```

**예**

다음 PQL 쿼리는 두 가지 다른 제품의 가격을 합합니다.

```sql
product1.price + product2.price
```

## 곱하기

다음 `*` (곱하기) 함수는 두 인수 표현식의 곱을 찾는 데 사용된다.

**형식**

```sql
{NUMBER} * {NUMBER}
```

**예**

다음 PQL 쿼리는 재고의 제품과 제품의 가격을 찾아 제품의 총 값을 찾습니다.

```sql
product.inventory * product.price
```

## 빼기

다음 `-` (빼기) 함수는 두 인수 표현식의 차이를 구하는 데 사용합니다.

**형식**

```sql
{NUMBER} - {NUMBER}
```

**예**

다음 PQL 쿼리는 두 가지 다른 제품 간의 가격 차이를 찾습니다.

```sql
product1.price - product2.price
```

## 나누기

다음 `/` (나눗셈) 함수는 두 인수 표현식의 몫을 구하는 데 사용된다.

**형식**

```sql
{NUMBER} / {NUMBER}
```

**예**

다음 PQL 쿼리는 품목당 평균 비용을 보기 위해 판매된 총 제품과 벌어들인 총 금액 사이의 몫을 구합니다.

```sql
totalProduct.price / totalProduct.sold
```

## 나머지

다음 `%` (modulo/remainder) 함수는 두 인수 표현식을 나눈 후 나머지를 구하는 데 사용된다.

**형식**

```sql
{NUMBER} % {NUMBER}
```

**예**

다음 PQL 쿼리는 개인의 연령을 5로 나눌 수 있는지 확인합니다.

```sql
person.age % 5 = 0
```

## 다음 단계

산술 함수에 대해 배웠으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 다음을 참조하십시오. [프로필 쿼리 언어 개요](./overview.md).
