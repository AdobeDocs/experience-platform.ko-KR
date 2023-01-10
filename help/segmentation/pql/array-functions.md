---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;배열 함수;배열;
solution: Experience Platform
title: 어레이, 목록 및 PQL 함수 설정
description: PQL(프로필 쿼리 언어)은 배열, 목록 및 문자열과 보다 쉽게 상호 작용할 수 있는 기능을 제공합니다.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 5%

---

# 배열, 목록 및 설정 함수

[!DNL Profile Query Language] (PQL) 은 어레이, 목록 및 문자열과 보다 쉽게 상호 작용할 수 있는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## in

다음 `in` 함수가 배열 또는 목록의 구성원인지 여부를 확인하는 데 사용됩니다.

**형식**

```sql
{VALUE} in {ARRAY}
```

**예**

다음 PQL 질의는 3월, 6월 또는 9월에 생일이 있는 사람을 정의합니다.

```sql
person.birthMonth in [3, 6, 9]
```

## 아님

다음 `notIn` 함수는 항목이 배열 또는 목록의 멤버가 아닌지 확인하는 데 사용됩니다.

>[!NOTE]
>
>다음 `notIn` 함수 *또한* 두 값이 모두 null인지 확인합니다. 따라서, 그 결과는 `in` 함수 위에 있어야 합니다.

**형식**

```sql
{VALUE} notIn {ARRAY}
```

**예**

다음 PQL 질의는 3월, 6월 또는 9월에 없는 생일이 있는 사람을 정의합니다.

```sql
person.birthMonth notIn [3, 6, 9]
```

## 교차

다음 `intersects` 두 배열이나 목록에 하나 이상의 공통 멤버가 있는지 확인하는 데 사용되는 함수입니다.

**형식**

```sql
{ARRAY}.intersects({ARRAY})
```

**예**

다음 PQL 쿼리는 빨간색, 파란색 또는 녹색 중 하나 이상의 색상을 포함하는 사람을 정의합니다.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## 교차

다음 `intersection` 두 개의 배열 또는 목록의 공통 멤버를 결정하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.intersection({ARRAY})
```

**예**

다음 PQL 쿼리는 개인 1과 개인 2가 모두 빨간색, 파란색 및 녹색의 즐겨찾는 색상을 사용하는지 여부를 정의합니다.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## 하위 집합

다음 `subsetOf` 함수는 특정 배열(배열 A)이 다른 배열(배열 B)의 하위 집합인지 여부를 확인하는 데 사용됩니다. 즉, 배열 A의 모든 요소는 배열 B의 요소입니다.

**형식**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**예**

다음 PQL 쿼리는 즐겨찾는 도시를 모두 방문한 사용자를 정의합니다.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## 의 상위 집합

다음 `supersetOf` 함수는 특정 배열(배열 A)이 다른 배열(배열 B)의 상위 집합인지 여부를 확인하는 데 사용됩니다. 즉, 해당 배열 A에 배열 B의 모든 요소가 포함됩니다.

**형식**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**예**

다음 PQL 질의은 초밥과 피자를 적어도 한 번 먹은 사람을 정의한 것입니다.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## 포함

다음 `includes` 함수는 배열 또는 목록에 지정된 항목이 포함되어 있는지 여부를 확인하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.includes({ITEM})
```

**예**

다음 PQL 쿼리는 즐겨찾는 색상이 빨간색인 사람을 정의합니다.

```sql
person.favoriteColors.includes("red")
```

## 고유

다음 `distinct` 함수는 배열 또는 목록에서 중복 값을 제거하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.distinct()
```

**예**

다음 PQL 쿼리는 둘 이상의 저장소에 주문을 한 사용자를 지정합니다.

```sql
person.orders.storeId.distinct().count() > 1
```

## 그룹화 기준

다음 `groupBy` 함수는 배열 또는 목록의 값을 표현식의 값에 따라 그룹으로 분할하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 그룹화할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 반환된 배열 또는 목록의 각 항목을 매핑하는 식입니다. |

**예**

다음 PQL 질의는 주문이 배치된 모든 주문을 그룹화합니다.

```sql
orders.groupBy(storeId)
```

## 필터

다음 `filter` 함수는 표현식을 기반으로 배열이나 목록을 필터링하는 데 사용됩니다.

**형식**

```sql
{ARRAY}.filter({EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 필터링할 배열 또는 목록입니다. |
| `{EXPRESSION}` | 필터링할 식입니다. |

**예**

다음 PQL 쿼리는 21세 이상의 모든 사용자를 정의합니다.

```sql
person.filter(age >= 21)
```

## 맵

다음 `map` 함수는 지정된 배열의 각 항목에 표현식을 적용하여 새 배열을 만드는 데 사용됩니다.

**형식**

```sql
array.map(expression)
```

**예**

다음 PQL 쿼리는 새 숫자 배열을 만들고 원래 숫자의 값을 제곱합니다.

```sql
numbers.map(square)
```

## 첫 번째 `n` 어레이 {#first-n}

다음 `topN` 함수는 `N` 지정된 숫자 식을 기반으로 오름차순으로 정렬하는 경우 배열의 항목이 표시됩니다.

**형식**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{ARRAY}` | 정렬할 배열 또는 목록입니다. |
| `{VALUE}` | 배열이나 목록을 정렬할 속성입니다. |
| `{AMOUNT}` | 반환할 항목 수입니다. |

**예**

다음 PQL 쿼리는 가격이 가장 높은 상위 5개 주문을 반환합니다.

```sql
orders.topN(price, 5)
```

## 마지막 `n` 어레이

다음 `bottomN` 함수는 `N` 지정된 숫자 식을 기반으로 오름차순으로 정렬하는 경우 배열의 항목이 표시됩니다.

**형식**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| 인수 | 설명 |
| --------- | ----------- | 
| `{ARRAY}` | 정렬할 배열 또는 목록입니다. |
| `{VALUE}` | 배열이나 목록을 정렬할 속성입니다. |
| `{AMOUNT}` | 반환할 항목 수입니다. |

**예**

다음 PQL 쿼리는 가장 낮은 가격으로 상위 5개 주문을 반환합니다.

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

다음 PQL 쿼리는 가격이 가장 높은 상위 5개 주문 중 첫 번째 주문을 반환합니다. 에 대한 추가 정보 `topN` 함수는 [첫 번째 `n` 어레이](#first-n) 섹션을 참조하십시오.

```sql
orders.topN(price, 5).head()
```

## 다음 단계

이제 어레이, 목록 및 설정 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md).
