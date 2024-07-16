---
solution: Experience Platform
title: PQL 집계 함수
description: 집계 함수는 Profile Query Language(PQL) 배열 내에서 여러 값을 함께 그룹화하여 단일 요약 값을 구성하는 데 사용됩니다.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 6%

---

# 집계 함수

집계 함수는 [!DNL Profile Query Language](PQL) 배열 내에서 여러 값을 함께 그룹화하여 단일 요약 값을 구성하는 데 사용됩니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 횟수

`count` 함수는 특정 배열의 요소 수를 반환합니다.

**형식**

```sql
{ARRAY}.count()
```

**예**

다음 PQL 쿼리는 배열의 주문 수를 반환합니다.

```sql
orders.count()
```

## 합계

`sum` 함수는 배열에서 선택한 모든 값의 합계를 반환합니다.

**형식**

```sql
{ARRAY}.sum()
```

**예**

다음 PQL 쿼리는 모든 주문 가격의 합계를 반환합니다.

```sql
orders.sum(order.price)
```

## 평균

`average` 함수는 배열에서 선택한 모든 값의 산술 평균을 반환합니다.

**형식**

```sql
{ARRAY}.average()
```

**예**

다음 PQL 쿼리는 모든 주문의 평균 가격을 반환합니다.

```sql
orders.average(order.price)
```

## 최소

`min` 함수는 배열에서 선택한 모든 값 중 가장 작은 값을 반환합니다.

**형식**

```sql
{ARRAY}.min()
```

**예**

다음 PQL 쿼리는 모든 주문의 최저 가격을 반환합니다.

```sql
orders.min(order.price)
```

## 최대

`max` 함수는 배열에서 선택한 모든 값 중 가장 큰 값을 반환합니다.

**형식**

```sql
{ARRAY}.max()
```

**예**

다음 PQL 쿼리는 모든 주문의 가장 높은 가격을 반환합니다.

```sql
orders.max(order.price)
```

## 다음 단계

집계 함수에 대해 배웠으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
