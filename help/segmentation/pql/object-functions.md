---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;개체 기능;개체
solution: Experience Platform
title: PQL 개체 함수
topic-legacy: developer guide
description: PQL(프로파일 쿼리 언어)은 개체와의 상호 작용을 단순화하는 기능을 제공합니다.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---

# 객체 함수

[!DNL Profile Query Language] (PQL)은 개체와의 상호 작용을 단순화하는 기능을 제공합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)에서 확인할 수 있습니다.

## null임

`isNull` 함수는 개체 참조가 있는지 확인합니다.

**형식**

```sql
{OBJECT}.isNull()
```

**예**

다음 PQL 쿼리는 개인의 홈 주소가 존재하지 않는지 확인합니다.

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

다음 PQL 쿼리는 개인의 홈 주소가 있는지 확인합니다.

```sql
person.homeAddress.isNotNull()
```

## 다음 단계

이제 개체 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md)를 참조하십시오.
