---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;array functions;array;
solution: Experience Platform
title: 배열, 목록 및 집합 함수
topic: developer guide
description: PQL(프로필 쿼리 언어)은 배열, 목록 및 문자와의 상호 작용을 쉽게 하는 기능을 제공합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 5%

---


# 배열, 목록 및 집합 함수

[!DNL Profile Query Language] (PQL)은 배열, 목록 및 문자와의 상호 작용을 용이하게 하는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## 인

이 `in` 함수를 사용하여 항목이 배열 또는 목록의 구성원인지 확인합니다.

**형식**

```sql
{VALUE} in {ARRAY}
```

**예**

다음 PQL 질의는 3월, 6월 또는 9월에 생일을 기준으로 사람을 정의합니다.

```sql
person.birthMonth in [3, 6, 9]
```

## Not in

이 `notIn` 함수를 사용하여 항목이 배열 또는 목록의 구성원이 아닌지 확인합니다.

>[!NOTE]
>
>이 `notIn` 함수는 *또한* 두 값이 모두 null임을 보장합니다. 따라서 결과는 `in` 함수의 정확한 부정은 아닙니다.

**형식**

```sql
{VALUE} notIn {ARRAY}
```

**예**

다음 PQL 질의는 3월, 6월 또는 9월에 없는 생일을 가진 사람을 정의합니다.

```sql
person.birthMonth notIn [3, 6, 9]
```

## 교차점

이 `intersects` 함수를 사용하여 두 배열 또는 목록에 하나 이상의 공통 구성원이 있는지 확인합니다.

**형식**

```sql
{ARRAY}.intersects({ARRAY})
```

**예**

다음 PQL 쿼리는 즐겨찾기 색상이 하나 이상의 빨간색, 파란색 또는 녹색을 포함하는 사람을 정의합니다.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 교차

이 `intersection` 함수는 두 배열 또는 목록의 공통 멤버를 결정하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.intersection({ARRAY})
```

**예**

다음 PQL 질의는 사람 1과 사람 2가 모두 빨간색, 파란색 및 녹색의 즐겨찾는 색상을 사용하는지 여부를 정의합니다.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 하위 집합

이 `subsetOf` 함수를 사용하여 특정 배열(배열 A)이 다른 배열(배열 B)의 하위 집합인지 확인합니다. 즉, 어레이 A의 모든 요소는 배열 B의 요소입니다.

**형식**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**예**

다음 PQL 쿼리는 자주 사용하는 모든 도시를 방문한 사람을 정의합니다.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 상위 세트

이 `supersetOf` 함수를 사용하여 특정 배열(배열 A)이 다른 배열(배열 B)의 상위 집합인지 확인합니다. 즉, 해당 배열 A에는 배열 B의 모든 요소가 포함됩니다.

**형식**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**예**

다음 PQL 질의은 초밥과 피자를 최소한 한 번 먹은 사람을 정의합니다.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 포함

이 `includes` 함수는 배열 또는 목록에 지정된 항목이 포함되어 있는지 확인하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.includes({ITEM})
```

**예**

다음 PQL 쿼리는 자주 사용하는 색상이 빨간색을 포함하는 사람을 정의합니다.

```sql
person.favoriteColors.includes("red")
```

## 고유한

이 `distinct` 함수는 배열 또는 목록에서 중복 값을 제거하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.distinct()
```

**예**

다음 PQL 쿼리는 둘 이상의 스토어에서 주문을 제출한 사람을 지정합니다.

```sql
person.orders.storeId.distinct().count() > 1
```

## 그룹화 기준

이 `groupBy` 함수는 배열 또는 목록의 값을 표현식 값을 기준으로 그룹으로 분할하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 그룹화할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 반환된 배열 또는 목록의 각 항목을 매핑하는 식입니다. |

**예**

다음 PQL 쿼리는 주문을 저장하는 모든 주문을 그룹화합니다.

```sql
orders.groupBy(storeId)
```

## 필터

이 `filter` 함수는 식을 기반으로 배열 또는 목록을 필터링하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 필터링할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 필터링할 표현식입니다. |

**예**

다음 PQL 쿼리는 21세 이상의 모든 사람을 정의합니다.

```sql
person.filter(age >= 21)
```

## 맵

이 `map` 함수는 지정된 배열의 각 항목에 표현식을 적용하여 새 배열을 만드는 데 사용됩니다.

**형식**

```sql
array.map(expression)
```

**예**

다음 PQL 쿼리는 새 숫자 배열을 만들고 원래 숫자의 값을 제곱합니다.

```sql
numbers.map(square)
```

## 스토리지 `n` 의 첫 번째 {#first-n}

이 `topN` 함수는 지정된 숫자 표현식에 따라 오름차순으로 정렬할 때 배열의 첫 번째 `N` 항목을 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 정렬할 배열 또는 목록입니다. |
| `{VALUE}` | 배열 또는 목록을 정렬할 속성입니다. |
| `{AMOUNT}` | 반환할 항목 수입니다. |

**예**

다음 PQL 쿼리는 가장 높은 가격을 가진 상위 5개 주문을 반환합니다.

```sql
orders.topN(price, 5)
```

## 스토리지 `n` 의 마지막

이 `bottomN` 함수는 지정된 숫자 표현식에 따라 오름차순으로 정렬할 때 배열의 마지막 `N` 항목을 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 인수 | 설명 |
| --------- | ----------- | 
| `{ARRAY}` | 정렬할 배열 또는 목록입니다. |
| `{VALUE}` | 배열 또는 목록을 정렬할 속성입니다. |
| `{AMOUNT}` | 반환할 항목 수입니다. |

**예**

다음 PQL 쿼리는 가장 낮은 가격으로 상위 5개 주문을 반환합니다.

```sql
orders.bottomN(price, 5)
```

## 첫 번째 항목

이 `head` 함수는 배열 또는 목록의 첫 번째 항목을 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.head()
```

**예**

다음 PQL 쿼리는 가장 높은 가격을 가진 상위 5개 주문 중 첫 번째 주문을 반환합니다. 함수에 대한 자세한 내용은 `topN` array 섹션의 [첫 `n` 번째](#first-n) 섹션에서 찾을 수 있습니다.

```sql
orders.topN(price, 5).head()
```

## 다음 단계

배열, 목록 및 설정 기능에 대해 알고 있다면 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
