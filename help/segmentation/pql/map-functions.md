---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 맵 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 맵 함수

PQL(Profile Query Language)은 맵과 보다 손쉽게 인터랙션할 수 있는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 언어 [개요를](./overview.md)참조하십시오.

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

다음 PQL 쿼리는 맵에 대한 모든 키를 `identityMap`가져옵니다.

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

다음 PQL 쿼리는 맵의 모든 값을 가져옵니다 `identityMap`.

```sql
identityMap.values()
```

## 다음 단계

맵 기능에 대해 알아보았으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 [언어 개요를](./overview.md)참조하십시오.
