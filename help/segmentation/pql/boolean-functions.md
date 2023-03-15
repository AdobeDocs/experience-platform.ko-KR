---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼테이션;세그먼테이션 서비스;pql;PQL;프로필 쿼리 언어;부울 함수;부울;
solution: Experience Platform
title: PQL 부울 함수
description: 부울 함수를 사용하여 PQL(프로필 쿼리 언어)의 다른 요소에 대해 부울 논리를 수행합니다.
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# 부울 함수

부울 함수는 의 다른 요소에 대해 부울 로직을 수행하는 데 사용됩니다. [!DNL Profile Query Language] (PQL).  다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 및

다음 `and` 함수는 논리 결합을 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} and {QUERY}
```

**예**

다음 PQL 쿼리는 본국이 1985년의 캐나다와 출생년도인 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 또는

다음 `or` 함수는 논리적 분리를 만드는 데 사용됩니다.

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

다음 `not` (또는 `!`) 함수는 논리 부정을 만드는 데 사용됩니다.

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

다음 `if` 함수는 지정된 조건이 true인지에 따라 표현식을 확인하는 데 사용합니다.

**형식**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 테스트 중인 부울 표현식입니다. |
| `{TRUE_EXPRESSION}` | 다음 경우에 사용될 값을 가진 표현식 `{TEST_EXPRESSION}` true입니다. |
| `{FALSE_EXPRESSION}` | 다음 경우에 사용될 값을 가진 표현식 `{TEST_EXPRESSION}` false입니다. |

**예**

다음 PQL 쿼리는 값을 로 설정합니다. `1` 본국이 캐나다인 경우 `2` 본국이 캐나다가 아닌 경우.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 다음 단계

이제 부울 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 다음을 참조하십시오. [프로필 쿼리 언어 개요](./overview.md).
