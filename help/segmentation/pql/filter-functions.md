---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 필터 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 필터 함수

필터 함수는 PQL(프로필 쿼리 언어)의 배열 내에서 데이터를 필터링하는 데 사용됩니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 언어 [개요를](./overview.md)참조하십시오.

## 필터

( `[]` filter) 함수를 사용하면 필터를 배열에 적용하고 지정된 조건과 일치하는 배열의 하위 집합을 반환할 수 있습니다.

**형식**

```sql
{ARRAY}[filter]
```

**예**

다음 PQL 쿼리는 SKU가 &quot;PS&quot;인 제품 항목이 하나 이상 있는 모든 이벤트를 가져옵니다.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up 연산자

( `^` up) 연산자를 사용하면 필터 상단의 속성을 참조할 수 있습니다.

**형식**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 인수 | 설명 |
| -------- | ----------- |
| `{ARRAY}` | 필터링되는 배열입니다. |
| `{FILTER_1}` | 필터링의 외부 레이어 |
| `{FILTER_2}` | 필터링의 내부 레이어 |
| `^{PROPERTY}` | 필터링되고 있는 속성입니다. 이 `^`때문에 filter1을 기반으로 속성을 확인하고 있습니다. |

**예**

다음 PQL 쿼리는 SKU가 &quot;PS&quot;와 같은 제품 항목을 하나 이상 **포함하거나** 성별을 가진 사람을 포함하는 모든 이벤트를 가져옵니다.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 다음 단계

이제 필터 기능에 대해 알았으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 [언어 개요를](./overview.md)참조하십시오.
