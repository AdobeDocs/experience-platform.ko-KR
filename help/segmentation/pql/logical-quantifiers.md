---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: 논리적 수량자
topic: developer guide
description: 논리 정량자는 PQL(프로필 쿼리 언어)에서 배열이 있는 조건을 표시하는 데 사용할 수 있습니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 5%

---


# 논리적 수량 함수

논리 정량자는 (PQL)에서 배열이 있는 조건을 [!DNL Profile Query Language] 확인하는 데 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## 존재함

이 `exists` 함수는 제공된 조건을 충족하는 경우 배열에 항목의 존재를 결정합니다.

**형식**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 인수 | 설명 |
| ---------- | ----------- |
| `{VARIABLE}` | 변수의 이름입니다. |
| `{EXPRESSION}` | 검사 중인 배열입니다. |
| `{CONDITION}` | 반환된 배열의 값을 필터링하는 선택적 표현식. |

**예**

다음 PQL 쿼리는 가격이 50달러 이상이거나 SKU가 &quot;PS&quot;인 모든 이벤트를 가져옵니다.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 모든 사용자에게

이 `forall` 함수는 지정된 모든 조건을 충족하는 배열의 모든 항목을 결정합니다.

**형식**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| 인수 | 설명 |
| ---------- | ----------- |
| `{VARIABLE}` | 변수의 이름입니다. |
| `{EXPRESSION}` | 검사 중인 배열입니다. |
| `{CONDITION}` | 반환된 배열의 값을 필터링하는 선택적 표현식. |

**예**

다음 PQL 쿼리는 가격이 $50보다 크고 SKU가 &quot;PS&quot;인 모든 이벤트를 가져옵니다.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## 다음 단계

이제 논리 정량자에 대해 학습했으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
