---
solution: Experience Platform
title: PQL 맵 함수
description: Profile Query Language(PQL)는 맵과의 상호 작용을 용이하게 하는 기능을 제공합니다.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# 맵 함수

[!DNL Profile Query Language](PQL)은(는) 맵과의 상호 작용을 더 쉽게 하는 함수를 제공합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 다운로드

`get` 함수는 특정 키에 대한 맵 값을 개체로 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.get({STRING})
```

**예**

다음 PQL 쿼리는 키 `example@example.com`에 대한 ID 맵의 값을 가져옵니다.

```sql
identityMap.get("example@example.com")
```

## 키

`keys` 함수는 특정 맵의 모든 키를 배열 또는 목록으로 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.keys()
```

**예**

다음 PQL 쿼리는 맵 `identityMap`에 대한 모든 키를 가져옵니다.

```sql
identityMap.keys()
```

## 값

`values` 함수는 특정 맵의 모든 값을 배열 또는 목록으로 검색하는 데 사용됩니다.

**형식**

```sql
{MAP}.values()
```

**예**

다음 PQL 쿼리는 맵 `identityMap`의 모든 값을 가져옵니다.

```sql
identityMap.values()
```

## 다음 단계

맵 함수에 대해 배웠으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
