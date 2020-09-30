---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;aggregation functions;aggregation;
solution: Experience Platform
title: 집계 함수
topic: developer guide
description: '집계 함수는 PQL(Profile Query Language) 배열 내에서 여러 값을 함께 그룹화하여 단일 요약 값을 구성하는 데 사용됩니다. '
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 6%

---


# 집계 함수

집계 함수는 PQL(Againing Array) [!DNL Profile Query Language] 배열에서 여러 값을 함께 그룹화하여 단일 요약 값을 구성하는 데 사용됩니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## 카운트

이 `count` 함수는 지정된 배열 내의 요소 수를 반환합니다.

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

이 `sum` 함수는 배열 내에서 선택한 모든 값의 합계를 반환합니다.

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

이 `average` 함수는 배열 내에서 선택한 모든 값의 산술 평균을 반환합니다.

**형식**

```sql
{ARRAY}.average()
```

**예**

다음 PQL 쿼리는 모든 주문의 평균 가격을 반환합니다.

```sql
orders.average(order.price)
```

## 최소값

이 `min` 함수는 배열 내에서 선택한 모든 값 중 가장 작은 값을 반환합니다.

**형식**

```sql
{ARRAY}.min()
```

**예**

다음 PQL 쿼리는 모든 주문의 가장 낮은 가격을 반환합니다.

```sql
orders.min(order.price)
```

## 최대값

이 `max` 함수는 배열 내에서 선택한 모든 값 중 가장 큰 값을 반환합니다.

**형식**

```sql
{ARRAY}.max()
```

**예**

다음 PQL 쿼리는 모든 주문의 최고 가격을 반환합니다.

```sql
orders.max(order.price)
```

## 다음 단계

이제 집계 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
