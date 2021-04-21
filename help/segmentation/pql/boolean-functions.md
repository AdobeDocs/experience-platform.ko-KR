---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;부울 함수;Boolean
solution: Experience Platform
title: PQL 부울 함수
topic-legacy: developer guide
description: 부울 함수는 PQL(프로파일 쿼리 언어)의 다른 요소에 대해 부울 논리를 수행하는 데 사용됩니다.
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 5%

---

# 부울 함수

부울 함수는 [!DNL Profile Query Language](PQL)의 다른 요소에 대해 부울 논리를 수행하는 데 사용됩니다.  다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)에서 확인할 수 있습니다.

## 그리고

`and` 함수는 논리 연결을 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} and {QUERY}
```

**예**

다음 PQL 쿼리는 1985년 캐나다와 출생년으로 본국에 있는 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## 또는

`or` 함수는 논리적 분리를 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} or {QUERY}
```

**예**

다음 PQL 쿼리는 1985년 캐나다나 출생년으로 본국에 있는 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 아님

`not`(또는 `!`) 함수를 사용하여 논리적 부정을 만듭니다.

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

`if` 함수는 지정된 조건이 true인지 여부에 따라 표현식을 해결하는 데 사용됩니다.

**형식**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 테스트할 부울 표현식입니다. |
| `{TRUE_EXPRESSION}` | `{TEST_EXPRESSION}`이(가) true인 경우 값이 사용될 표현식입니다. |
| `{FALSE_EXPRESSION}` | `{TEST_EXPRESSION}`이(가) false인 경우 값을 사용할 표현식입니다. |

**예**

다음 PQL 쿼리는 홈 국가가 캐나다인 경우 `1` 값을 설정하고, 홈 국가가 캐나다가 아닌 경우에는 `2` 값을 설정합니다.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 다음 단계

이제 부울 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md)를 참조하십시오.
