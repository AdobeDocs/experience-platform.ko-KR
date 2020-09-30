---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: 매핑 함수
topic: developer guide
description: PQL(프로필 쿼리 언어)은 맵과의 상호 작용을 용이하게 하는 기능을 제공합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---


# 매핑 함수

[!DNL Profile Query Language] (PQL)은 맵과의 상호 작용을 용이하게 하는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## 가져오기

이 `get` 함수는 지정된 키에 대한 맵 값을 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.get({STRING})
```

**예**

다음 PQL 쿼리는 키에 대한 ID 맵의 값을 가져옵니다 `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## 키

이 `keys` 함수는 지정된 맵에 대한 모든 키를 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.keys()
```

**예**

다음 PQL 쿼리는 맵에 대한 모든 키를 가져옵니다 `identityMap`.

```sql
identityMap.keys()
```

## 값

이 `values` 함수는 지정된 맵의 모든 값을 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.values()
```

**예**

다음 PQL 쿼리는 맵에 대한 모든 값을 가져옵니다 `identityMap`.

```sql
identityMap.values()
```

## 다음 단계

맵 기능에 대해 알아냈으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
