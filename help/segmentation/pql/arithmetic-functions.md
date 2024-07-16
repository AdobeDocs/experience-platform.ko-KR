---
solution: Experience Platform
title: PAL 산술 함수
description: 산술 함수는 Profile Query Language(PQL)의 값에 대한 기본 계산을 수행하는 데 사용됩니다.
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 4%

---

# 산술 함수

산술 함수는 [!DNL Profile Query Language](PQL)의 값에 대한 기본 계산을 수행하는 데 사용됩니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 이벤트가 복제되지 않도록 하면서 현재 이벤트 변수에

`+`(추가) 함수는 두 인수 표현식의 합계를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} + {NUMBER}
```

**예**

다음 PQL 쿼리는 두 가지 다른 제품의 가격을 합계합니다.

```sql
product1.price + product2.price
```

## 곱하기

`*`(곱하기) 함수는 두 인수 표현식의 곱을 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} * {NUMBER}
```

**예**

다음 PQL 쿼리는 재고 및 제품 가격의 제품을 찾아 제품의 총 값을 찾습니다.

```sql
product.inventory * product.price
```

## 빼기

`-`(빼기) 함수는 두 인수 표현식의 차이를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} - {NUMBER}
```

**예**

다음 PQL 쿼리는 서로 다른 두 제품 간의 가격 차이를 확인합니다.

```sql
product1.price - product2.price
```

## 나누기

`/`(나눗셈) 함수는 두 인수 표현식의 몫을 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} / {NUMBER}
```

**예**

다음 PQL 쿼리는 항목당 평균 비용을 보기 위해 판매된 총 제품과 벌어들인 총 금액 사이의 몫을 구합니다.

```sql
totalProduct.price / totalProduct.sold
```

## 나머지

`%`(modulo/remainder) 함수는 두 인수 표현식을 나눈 후 나머지를 찾는 데 사용됩니다.

**형식**

```sql
{NUMBER} % {NUMBER}
```

**예**

다음 PQL 쿼리는 개인의 나이를 5로 나눌 수 있는지 확인합니다.

```sql
person.age % 5 = 0
```

## 다음 단계

산술 함수에 대해 배웠으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
