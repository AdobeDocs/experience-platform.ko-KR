---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 매핑 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---


# 매핑 함수

[!DNL Profile Query Language] (PQL)은 맵과의 상호 작용을 용이하게 하는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).

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
