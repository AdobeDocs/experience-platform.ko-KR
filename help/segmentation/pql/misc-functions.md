---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 기타 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# 기타 함수

다음 함수는 PQL(프로필 쿼리 언어)에 대한 기타 함수입니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 언어 [개요를](./overview.md)참조하십시오.

## Let

이 `let` 함수를 사용하면 나중에 쿼리에서 사용할 변수로 표현식을 저장할 수 있습니다.

**형식**

```sql
let {VARIABLE} = {EXPRESSION}
```

**예**

다음 PQL 질의는 합계가 $100보다 크고 $1000보다 적은 USD의 트랜잭션과 모든 제품 합계를 가져옵니다.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 다음 단계

이제 기타 기능에 대해 알았으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 [언어 개요를](./overview.md)참조하십시오.
