---
solution: Experience Platform
title: PQL 개체 함수
description: Profile Query Language(PQL)는 개체와의 상호 작용을 더 간단하게 하는 기능을 제공합니다.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 9%

---

# 개체 함수

[!DNL Profile Query Language](PQL)에서는 개체와의 상호 작용을 더 간단하게 하는 기능을 제공합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## null임

`isNull` 함수는 개체 참조가 없는지 확인합니다.

**형식**

```sql
{OBJECT}.isNull()
```

**예**

다음 PQL 쿼리는 개인의 집 주소가 존재하지 않는지 확인합니다.

```sql
person.homeAddress.isNull()
```

## null이 아님

`isNotNull` 함수는 개체 참조가 있는지 확인합니다.

**형식**

```sql
{OBJECT}.isNotNull()
```

**예**

다음 PQL 쿼리는 개인의 집 주소가 존재하는지 확인합니다.

```sql
person.homeAddress.isNotNull()
```

## 다음 단계

개체 함수에 대해 배웠으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
