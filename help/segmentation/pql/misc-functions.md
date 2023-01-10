---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;기타 함수;기타;
solution: Experience Platform
title: PQL 기타 함수
description: 다음 함수는 PQL(프로필 쿼리 언어)에 대한 기타 기능입니다.
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# 기타 함수

다음 함수는 [!DNL Profile Query Language] (PQL). 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## Let

다음 `let` 함수를 사용하면 표현식을 변수로 저장하여 나중에 쿼리에서 사용할 수 있습니다.

**형식**

```sql
let {VARIABLE} = {EXPRESSION}
```

**예**

다음 PQL 쿼리는 합계가 $100보다 크고 $1000보다 작은 USD의 트랜잭션과 함께 모든 제품 합계를 가져옵니다.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 다음 단계

이제 기타 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md).
