---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;object functions;object;
solution: Experience Platform
title: 개체 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 5%

---


# 개체 함수

[!DNL Profile Query Language] (PQL)은 개체와의 상호 작용을 단순화하는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## null임

이 `isNull` 함수는 개체 참조가 있는지 확인합니다.

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

이 `isNotNull` 함수는 개체 참조가 있는지 확인합니다.

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

이제 개체 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).