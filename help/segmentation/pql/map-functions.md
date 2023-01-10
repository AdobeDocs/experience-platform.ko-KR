---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;맵 함수;맵;
solution: Experience Platform
title: PQL 맵 함수
description: PQL(프로필 쿼리 언어)은 맵과 보다 쉽게 상호 작용할 수 있도록 기능을 제공합니다.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---

# 맵 함수

[!DNL Profile Query Language] (PQL) 은 맵과 보다 쉽게 상호 작용할 수 있는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 가져오기

다음 `get` 함수는 지정된 키에 대한 맵 값을 검색하는 데 사용됩니다.

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

다음 `keys` 함수는 지정된 맵에 대한 모든 키를 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.keys()
```

**예**

다음 PQL 쿼리는 맵의 모든 키를 가져옵니다 `identityMap`.

```sql
identityMap.keys()
```

## 값

다음 `values` 함수는 지정된 맵의 모든 값을 검색하는 데 사용됩니다.

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

맵 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md).
