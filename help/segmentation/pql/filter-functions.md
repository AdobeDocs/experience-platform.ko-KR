---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;필터 기능;필터
solution: Experience Platform
title: PQL 필터 함수
topic-legacy: developer guide
description: 필터 함수는 PQL(프로필 쿼리 언어)의 배열 내에서 데이터를 필터링하는 데 사용됩니다.
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 4%

---

# 필터 함수

필터 함수는 [!DNL Profile Query Language](PQL)의 배열 내에서 데이터를 필터링하는 데 사용됩니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)에서 확인할 수 있습니다.

## 필터

`[]` (필터) 함수를 사용하면 필터를 배열에 적용하고 지정된 조건과 일치하는 배열의 하위 집합을 반환합니다.

**형식**

```sql
{ARRAY}[filter]
```

**예**

다음 PQL 쿼리는 SKU가 &quot;PS&quot;와 같은 제품 항목이 하나 이상 있는 모든 이벤트를 가져옵니다.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Up 연산자

`^`(up) 연산자를 사용하면 필터 상단의 속성을 참조할 수 있습니다.

**형식**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| 인수 | 설명 |
| -------- | ----------- |
| `{ARRAY}` | 필터링되는 배열입니다. |
| `{FILTER_1}` | 필터링의 외부 레이어입니다. |
| `{FILTER_2}` | 필터링의 내부 레이어 |
| `^{PROPERTY}` | 필터링되고 있는 속성입니다. `^` 때문에 filter1을 기반으로 속성을 확인하고 있습니다. |

**예**

다음 PQL 쿼리는 &quot;PS&quot; **또는**&#x200B;에 성이 여성인 사람이 있는 제품 항목이 하나 이상 있는 모든 이벤트를 가져옵니다.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## 다음 단계

이제 필터 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md)를 참조하십시오.
