---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;filter functions;filter;
solution: Experience Platform
title: 필터 함수
topic: developer guide
description: 필터 함수는 PQL(Profile Query Language)의 배열 내에서 데이터를 필터링하는 데 사용됩니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 4%

---


# 필터 함수

필터 함수는 (PQL)의 어레이 내 데이터를 필터링하는 데 [!DNL Profile Query Language] 사용됩니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

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

## 위쪽 연산자

( `^` up) 연산자를 사용하면 필터 상단의 속성을 참조할 수 있습니다.

**형식**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 인수 | 설명 |
| -------- | ----------- |
| `{ARRAY}` | 필터링되는 배열. |
| `{FILTER_1}` | 필터링의 외부 레이어 |
| `{FILTER_2}` | 필터링의 내부 레이어 |
| `^{PROPERTY}` | 필터링되고 있는 속성입니다. 이 때문에 필터1 `^`을 기반으로 속성을 확인하고 있습니다. |

**예**

다음 PQL 쿼리는 &quot;PS&quot;와 같은 SKU의 제품 항목이 하나 이상 **있거나** 성이 여성인 사람이 있는 모든 이벤트를 가져옵니다.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 다음 단계

이제 필터 기능에 대해 알았으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
