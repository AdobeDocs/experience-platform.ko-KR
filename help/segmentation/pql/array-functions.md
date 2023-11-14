---
solution: Experience Platform
title: PQL 함수 배열, 목록 및 설정
description: PQL(프로필 쿼리 언어)은 배열, 목록 및 문자열과 보다 쉽게 상호 작용할 수 있도록 하는 기능을 제공합니다.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 5%

---

# 배열, 목록 및 집합 함수

[!DNL Profile Query Language] (PQL)은 배열, 목록 및 문자열과 보다 쉽게 상호 작용할 수 있도록 함수를 제공합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 위치

다음 `in` 함수는 항목이 배열의 멤버인지 또는 목록의 멤버인지 확인하는 데 사용합니다.

**형식**

```sql
{VALUE} in {ARRAY}
```

**예**

다음 PQL 쿼리는 3월, 6월, 9월에 생일이 있는 사람을 정의합니다.

```sql
person.birthMonth in [3, 6, 9]
```

## 다음에 없음

다음 `notIn` 함수는 항목이 배열의 멤버인지 또는 목록의 멤버가 아닌지 확인하는 데 사용합니다.

>[!NOTE]
>
>다음 `notIn` 함수 *또한* 두 값 모두 null이 되지 않도록 합니다. 따라서 결과는 의 정확한 부정이 아닙니다. `in` 함수.

**형식**

```sql
{VALUE} notIn {ARRAY}
```

**예**

다음 PQL 쿼리는 생일이 3월, 6월, 9월이 아닌 사람을 정의합니다.

```sql
person.birthMonth notIn [3, 6, 9]
```

## 교차

다음 `intersects` 함수는 두 배열 또는 목록에 최소 하나 이상의 공통 멤버가 있는지 확인하는 데 사용합니다.

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

다음 `intersection` 함수는 두 배열 또는 목록의 공통 멤버를 결정하는 데 사용합니다.

**형식**

```sql
{ARRAY}.intersection({ARRAY})
```

**예**

다음 PQL 쿼리는 개인 1과 개인 2가 모두 빨강, 파랑 및 녹색으로 즐겨 찾는 색상을 가지고 있는지 여부를 정의합니다.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 하위 집합

다음 `subsetOf` 함수는 특정 배열(배열 A)이 다른 배열(배열 B)의 하위 집합인지 확인하는 데 사용됩니다. 즉, 배열 A의 모든 요소는 배열 B의 요소이다.

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

다음 `supersetOf` 함수는 특정 배열(배열 A)이 다른 배열(배열 B)의 상위 집합인지 확인하는 데 사용됩니다. 즉, 배열 A는 배열 B의 모든 요소를 포함합니다.

**형식**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**예**

다음 PQL 쿼리는 스시와 피자를 한 번 이상 먹은 사람을 정의합니다.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 포함

다음 `includes` 함수는 배열 또는 목록에 지정된 항목이 포함되어 있는지 확인하는 데 사용합니다.

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

다음 `distinct` 함수는 배열 또는 목록에서 중복 값을 제거하는 데 사용합니다.

**형식**

```sql
{ARRAY}.distinct()
```

**예**

다음 PQL 쿼리는 두 개 이상의 스토어에서 주문한 사람을 지정합니다.

```sql
person.orders.storeId.distinct().count() > 1
```

## 그룹화 기준

다음 `groupBy` 함수는 식 값을 기준으로 배열 또는 목록의 값을 그룹으로 분할하는 데 사용합니다.

**형식**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 그룹화할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 반환된 배열 또는 목록의 각 항목을 매핑하는 표현식입니다. |

**예**

다음 PQL 쿼리는 주문이 배치된 모든 주문을 그룹화합니다.

```sql
orders.groupBy(storeId)
```

## 필터

다음 `filter` 함수는 표현식을 기반으로 배열 또는 목록을 필터링하는 데 사용합니다.

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

다음 `map` 함수는 특정 배열의 각 항목에 식을 적용하여 새 배열을 만드는 데 사용됩니다.

**형식**

```sql
array.map(expression)
```

**예**

다음 PQL 쿼리는 새로운 숫자 배열을 생성하고 원래 숫자 값을 제곱합니다.

```sql
numbers.map(square)
```

## 첫 번째 `n` 배열에서 {#first-n}

다음 `topN` 함수는 다음을 반환하는 데 사용됩니다. `N` 배열의 항목이 지정된 수식에 따라 오름차순으로 정렬됩니다.

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

## 마지막 `n` 배열에서

다음 `bottomN` 함수는 마지막 반환에 사용됩니다. `N` 배열의 항목이 지정된 수식에 따라 오름차순으로 정렬됩니다.

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

다음 `head` 함수는 배열 또는 목록의 첫 번째 항목을 반환하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.head()
```

**예**

다음 PQL 쿼리는 가격이 가장 높은 상위 5개 주문 중 첫 번째 주문을 반환합니다. 에 대한 추가 정보 `topN` 함수는에서 찾을 수 있습니다. [첫 번째 `n` 배열에서](#first-n) 섹션.

```sql
orders.topN(price, 5).head()
```

## 다음 단계

이제 배열, 목록 및 집합 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 다음을 참조하십시오. [프로필 쿼리 언어 개요](./overview.md).
