---
solution: Experience Platform
title: PQL 기타 함수
description: 다음 함수는 Profile Query Language(PQL)에 대한 기타 함수입니다.
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# 기타 함수

다음 함수는 [!DNL Profile Query Language](PQL)에 대한 기타 함수입니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## Let

`let` 함수를 사용하면 나중에 쿼리에서 사용할 변수로 식을 저장할 수 있습니다.

**형식**

```sql
let {VARIABLE} = {EXPRESSION}
```

**예**

다음 PQL 쿼리는 합계액이 $100보다 크고 $1000보다 작은 USD 단위의 트랜잭션과 함께 제품 합계의 모든 합계를 가져옵니다.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## 다음 단계

이제 기타 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
