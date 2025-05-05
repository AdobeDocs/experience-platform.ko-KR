---
solution: Experience Platform
title: PQL 부울 함수
description: 부울 함수는 Profile Query Language(PQL)의 다른 요소에 대해 부울 로직을 수행하는 데 사용됩니다.
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 4%

---

# 부울 함수

부울 함수를 사용하여 [!DNL Profile Query Language] (PQL)의 다른 요소에 대해 부울 논리를 수행합니다.  다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 및

`and` 함수는 논리 결합을 부울로 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} and {QUERY}
```

**예**

다음 PQL 쿼리는 캐나다 및 1985년의 출생연도로 본국이 있는 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 또는

`or` 함수를 사용하여 논리 분리를 부울로 만듭니다.

**형식**

```sql
{QUERY} or {QUERY}
```

**예**

다음 PQL 쿼리는 본국이 캐나다 또는 1985년의 출생년도인 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 아님

`not`(또는 `!`) 함수는 논리 부정을 만드는 데 사용됩니다.

**형식**

```sql
not ({QUERY})
!({QUERY})
```

**예**

다음 PQL 쿼리는 본국이 없는 모든 사람을 캐나다로 반환합니다.

```sql
not (homeAddress.countryISO = "CA")
```

## If

`if` 함수는 지정된 조건이 부울로서 true인지에 따라 식을 확인하는 데 사용됩니다.

**형식**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 테스트 중인 부울 표현식입니다. |
| `{TRUE_EXPRESSION}` | `{TEST_EXPRESSION}`이(가) true인 경우 값이 사용되는 식입니다. |
| `{FALSE_EXPRESSION}` | `{TEST_EXPRESSION}`이(가) false인 경우 값이 사용되는 식입니다. |

**예**

다음 PQL 쿼리는 홈 국가가 캐나다인 경우 값을 `1`(으)로 설정하고, 홈 국가가 캐나다가 아닌 경우 값을 `2`(으)로 설정합니다.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 다음 단계

이제 부울 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
