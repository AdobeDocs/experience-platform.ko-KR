---
solution: Experience Platform
title: PQL 함수 배열, 목록 및 설정
description: Profile Query Language(PQL)는 배열, 목록 및 문자열과 보다 쉽게 상호 작용할 수 있도록 함수를 제공합니다.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 4%

---

# 배열, 목록 및 집합 함수

[!DNL Profile Query Language](PQL)에서는 배열, 목록 및 문자열과 보다 쉽게 상호 작용할 수 있도록 함수를 제공합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 안에 있음

`in` 함수는 항목이 배열의 멤버인지 또는 부울의 멤버인지 확인하는 데 사용합니다.

**형식**

```sql
{VALUE} in {ARRAY}
```

**예**

다음 PQL 쿼리는 3월, 6월 또는 9월에 생일이 있는 사람을 정의합니다.

```sql
person.birthMonth in [3, 6, 9]
```

## 안에 없음

`notIn` 함수는 항목이 배열의 멤버인지 또는 목록의 멤버가 아닌지 부울로 확인하는 데 사용합니다.

>[!NOTE]
>
>`notIn` 함수 *also*&#x200B;에서는 두 값 모두 null이 아닙니다. 따라서 결과는 `in` 함수에 대한 정확한 부정 결과가 아닙니다.

**형식**

```sql
{VALUE} notIn {ARRAY}
```

**예**

다음 PQL 쿼리는 생일이 3월, 6월 또는 9월이 아닌 사람을 정의합니다.

```sql
person.birthMonth notIn [3, 6, 9]
```

## 교차

`intersects` 함수는 두 배열 또는 목록에 부울로 최소 하나 이상의 공통 멤버가 있는지 확인하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.intersects({ARRAY})
```

**예**

다음 PQL 쿼리는 즐겨 찾는 색상에 빨간색, 파란색 또는 녹색 중 하나 이상이 포함된 사람을 정의합니다.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 교집합

`intersection` 함수는 두 배열 또는 목록의 공통 멤버를 목록으로 확인하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.intersection({ARRAY})
```

**예**

다음 PQL 쿼리는 개인 1과 개인 2가 모두 빨강, 파랑 및 녹색으로 즐겨 찾는 색상을 가지고 있는지 정의합니다.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 하위 집합

`subsetOf` 함수는 특정 배열(배열 A)이 다른 배열(배열 B)의 하위 집합인지 확인하는 데 사용됩니다. 즉, 배열 A의 모든 요소는 부울로서 배열 B의 요소이다.

**형식**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**예**

다음 PQL 쿼리는 즐겨 찾는 모든 도시를 방문한 사람들을 정의합니다.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 상위 집합

`supersetOf` 함수는 특정 배열(배열 A)이 다른 배열(배열 B)의 상위 집합인지 확인하는 데 사용합니다. 즉, 배열 A는 배열 B의 모든 요소를 부울로 포함합니다.

**형식**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**예**

다음 PQL 쿼리는 스시와 피자를 한 번 이상 먹은 사람을 정의합니다.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 다음을 포함

`includes` 함수는 배열 또는 목록에 지정된 항목이 부울로 포함되어 있는지 확인하는 데 사용합니다.

**형식**

```sql
{ARRAY}.includes({ITEM})
```

**예**

다음 PQL 쿼리는 즐겨 찾는 색상에 빨간색이 포함된 사람을 정의합니다.

```sql
person.favoriteColors.includes("red")
```

## 고유

`distinct` 함수는 배열 또는 목록에서 배열로 중복 값을 제거하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.distinct()
```

**예**

다음 PQL 쿼리는 둘 이상의 스토어에서 주문을 한 사람을 지정합니다.

```sql
person.orders.storeId.distinct().count() > 1
```

## 그룹화 기준

`groupBy` 함수는 그룹화 식의 고유한 값에서 배열 식의 분할인 배열로의 맵으로 식의 값을 기반으로 배열 또는 목록의 값을 그룹으로 분할하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 그룹화할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 반환된 배열 또는 목록의 각 항목을 매핑하는 표현식입니다. |

**예**

다음 PQL 쿼리는 주문이 배치된 저장소의 모든 주문을 그룹화합니다.

```sql
xEvent[type="order"].groupBy(storeId)
```

## 필터

`filter` 함수는 입력에 따라 배열 또는 목록으로 식을 기반으로 배열 또는 목록을 필터링하는 데 사용합니다.

**형식**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 필터링할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 필터링 기준 표현식. |

**예**

다음 PQL 쿼리는 21세 이상인 모든 사람을 정의합니다.

```sql
person.filter(age >= 21)
```

## 맵

`map` 함수는 특정 배열의 각 항목에 식을 배열로 적용하여 새 배열을 만드는 데 사용합니다.

**형식**

```sql
array.map(expression)
```

**예**

다음 PQL 쿼리는 새로운 숫자 배열을 만들고 원래 숫자 값을 제곱합니다.

```sql
numbers.map(square)
```

## 배열의 첫 `n` {#first-n}

`topN` 함수는 특정 수식을 배열로 기준으로 오름차순으로 정렬되는 경우 배열에서 첫 번째 `N` 항목을 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 정렬할 배열 또는 목록입니다. |
| `{VALUE}` | 배열 또는 목록을 정렬할 속성입니다. |
| `{AMOUNT}` | 반환할 항목의 수입니다. |

**예**

다음 PQL 쿼리는 가격이 가장 높은 상위 5개 주문을 반환합니다.

```sql
orders.topN(price, 5)
```

## 배열의 마지막 `n`

`bottomN` 함수는 특정 수식을 배열로 기준으로 오름차순으로 정렬되는 경우 배열에서 마지막 `N` 항목을 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 인수 | 설명 |
| --------- | ----------- | 
| `{ARRAY}` | 정렬할 배열 또는 목록입니다. |
| `{VALUE}` | 배열 또는 목록을 정렬할 속성입니다. |
| `{AMOUNT}` | 반환할 항목의 수입니다. |

**예**

다음 PQL 쿼리는 가격이 가장 낮은 상위 5개 주문을 반환합니다.

```sql
orders.bottomN(price, 5)
```

## 첫 번째 항목

`head` 함수는 배열 또는 목록의 첫 번째 항목을 개체로 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.head()
```

**예**

다음 PQL 쿼리는 가격이 가장 높은 상위 5개 주문 중 첫 번째 주문을 반환합니다. `topN` 함수에 대한 자세한 내용은 배열의 [첫 번째 `n`](#first-n) 섹션에서 찾을 수 있습니다.

```sql
orders.topN(price, 5).head()
```

## 다음 단계

이제 배열, 목록 및 집합 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
