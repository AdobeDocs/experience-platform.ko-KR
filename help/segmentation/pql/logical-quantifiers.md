---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;논리 수량;논리 수량;
solution: Experience Platform
title: PQL 논리 수량
description: 논리 수량자는 PQL(프로필 쿼리 언어)에서 배열이 있는 조건을 어설션하는 데 사용할 수 있습니다.
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 4%

---

# 논리 수량 함수

논리 정량자를 사용하여 [!DNL Profile Query Language] (PQL). 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 존재함

다음 `exists` 함수는 제공된 조건을 충족하는 경우, 배열에 항목의 존재를 결정합니다.

**형식**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 인수 | 설명 |
| ---------- | ----------- |
| `{VARIABLE}` | 변수의 이름입니다. |
| `{EXPRESSION}` | 확인 중인 배열입니다. |
| `{CONDITION}` | 반환된 배열의 값을 필터링하는 선택적 표현식입니다. |

**예**

다음 PQL 쿼리는 가격이 $50보다 높거나 SKU가 &quot;PS&quot;인 모든 이벤트를 가져옵니다.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 모든 경우에

다음 `forall` 함수는 지정된 모든 조건을 충족하는 배열의 모든 항목을 결정합니다.

**형식**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 인수 | 설명 |
| ---------- | ----------- |
| `{VARIABLE}` | 변수의 이름입니다. |
| `{EXPRESSION}` | 확인 중인 배열입니다. |
| `{CONDITION}` | 반환된 배열의 값을 필터링하는 선택적 표현식입니다. |

**예**

다음 PQL 쿼리는 가격이 $50보다 크고 SKU &quot;PS&quot;를 포함하는 모든 이벤트를 가져옵니다.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 다음 단계

이제 논리 수량자에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md).
