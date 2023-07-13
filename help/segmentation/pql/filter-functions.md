---
solution: Experience Platform
title: PQL 필터 함수
description: 필터 함수는 PQL(프로필 쿼리 언어)에서 배열 내의 데이터를 필터링하는 데 사용됩니다.
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 4%

---

# 필터 함수

필터 함수는 의 배열 내에서 데이터를 필터링하는 데 사용됩니다. [!DNL Profile Query Language] (PQL). 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 필터

다음 `[]` (filter) 함수를 사용하면 필터에 적용하고 지정된 조건과 일치하는 배열의 하위 집합을 반환할 수 있습니다.

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

다음 `^` (위쪽) 연산자를 사용하면 필터 상위 수준의 속성을 참조할 수 있습니다.

**형식**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 인수 | 설명 |
| -------- | ----------- |
| `{ARRAY}` | 필터링되는 배열입니다. |
| `{FILTER_1}` | 필터링의 외부 레이어입니다. |
| `{FILTER_2}` | 필터링의 내부 레이어 |
| `^{PROPERTY}` | 필터링 중인 속성입니다. (으)로 인해 `^`, filter1을 기반으로 속성을 확인하고 있습니다. |

**예**

다음 PQL 쿼리는 SKU가 &quot;PS&quot;와 동일한 하나 이상의 제품 항목이 있는 모든 이벤트를 가져옵니다. **또는** 성별이 여성인 사람이 있다.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 다음 단계

이제 필터 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 다음을 참조하십시오. [프로필 쿼리 언어 개요](./overview.md).
