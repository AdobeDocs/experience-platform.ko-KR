---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개체 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 개체 함수

PQL(Profile Query Language)은 개체와의 상호 작용을 간소화하는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 언어 [개요를](./overview.md)참조하십시오.

## Is null

이 `isNull` 함수는 객체 참조가 존재하지 않는지 여부를 결정합니다.

**형식**

```sql
{OBJECT}.isNull()
```

**예**

다음 PQL 쿼리는 개인의 홈 주소가 없는지 확인합니다.

```sql
person.homeAddress.isNull()
```

## null이 아님

이 `isNotNull` 함수는 객체 참조가 있는지 여부를 결정합니다.

**형식**

```sql
{OBJECT}.isNotNull()
```

**예**

다음 PQL 쿼리는 개인의 홈 주소가 있는지 확인합니다.

```sql
person.homeAddress.isNotNull()
```

## 다음 단계

이제 개체 기능에 대해 학습했으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 [언어 개요를](./overview.md)참조하십시오.