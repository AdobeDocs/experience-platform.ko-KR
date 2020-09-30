---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;arithmetic functions;arithmetic;
solution: Experience Platform
title: 산술 함수
topic: developer guide
description: 산술 함수는 PQL(프로필 쿼리 언어)에서 값에 대한 기본 계산을 수행하는 데 사용됩니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 5%

---


# 산술 함수

산술 함수는 (PQL)의 값에 대한 기본 계산을 수행하는 데 [!DNL Profile Query Language] 사용됩니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에

(adding) `+` 함수는 두 인수 표현식의 합을 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} + {NUMBER}
```

**예**

다음 PQL 쿼리는 두 개의 서로 다른 제품의 가격을 합산합니다.

```sql
product1.price + product2.price
```

## 곱하기

(곱하기) `*` 함수는 두 인수 표현식의 제품을 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} * {NUMBER}
```

**예**

다음 PQL 질의는 재고 제품 및 제품 가격을 검색하여 제품의 총값을 찾습니다.

```sql
product.inventory * product.price
```

## 빼기

( `-` 빼기) 함수는 두 인수 표현식의 차이를 찾는 데 사용됩니다.

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

(division) `/` 함수는 두 인수 표현식의 인용 값을 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} / {NUMBER}
```

**예**

다음 PQL 질의는 총 판매된 제품과 총 획득 금액 간의 견적을 검색하여 품목당 평균 비용을 확인합니다.

```sql
totalProduct.price / totalProduct.sold
```

## 나머지

두 인수 `%` 표현식을 나눈 후 나머지 함수를 찾는 데 (모듈과 나머지) 함수를 사용합니다.

**형식**

```sql
{NUMBER} % {NUMBER}
```

**예**

다음 PQL 쿼리는 개인의 나이가 5명으로 구분되어 있는지 확인합니다.

```sql
person.age % 5 = 0
```

## 다음 단계

이제 산술 함수에 대해 학습했으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
