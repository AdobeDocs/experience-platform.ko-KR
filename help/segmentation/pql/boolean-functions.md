---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 부울 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# 부울 함수

부울 함수는 PQL(Profile Query Language)의 다양한 요소에 대해 부울 논리를 수행하는 데 사용됩니다.  다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 언어 [개요를](./overview.md)참조하십시오.

## And

이 `and` 함수는 논리적 접속사를 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} and {QUERY}
```

**예**

다음 PQL 쿼리는 1985년 캐나다와 출생년으로 본국의 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 또는

이 `or` 함수는 논리적 분리를 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} or {QUERY}
```

**예**

다음 PQL 쿼리는 1985년 캐나다 또는 출생년으로 본국의 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 아님

( `not` 또는 `!`) 함수는 논리적 부정을 만드는 데 사용됩니다.

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

이 `if` 함수는 지정된 조건이 true인지 여부에 따라 표현식을 확인하는 데 사용됩니다.

**형식**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 테스트할 부울 식입니다. |
| `{TRUE_EXPRESSION}` | true인 경우 값이 사용될 `{TEST_EXPRESSION}` 표현식입니다. |
| `{FALSE_EXPRESSION}` | false일 경우 값을 사용할 `{TEST_EXPRESSION}` 표현식. |

**예**

다음 PQL 쿼리는 홈 국가가 캐나다인 `1` 것과 `2` 국가가 캐나다가 아닌 경우 이 값을 설정합니다.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 다음 단계

이제 부울 함수에 대해 학습했으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 [언어 개요를](./overview.md)참조하십시오.
