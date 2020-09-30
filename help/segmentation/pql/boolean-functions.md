---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;boolean functions;boolean;
solution: Experience Platform
title: 부울 함수
topic: developer guide
description: 부울 함수는 PQL(Profile Query Language)의 다양한 요소에 대해 부울 논리를 수행하는 데 사용됩니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 5%

---


# 부울 함수

부울 함수는 [!DNL Profile Query Language] (PQL)의 다른 요소에 대해 부울 논리를 수행하는 데 사용됩니다.  다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## And

이 `and` 함수는 논리 연결을 만드는 데 사용됩니다.

**형식**

```sql
{QUERY} and {QUERY}
```

**예**

다음 PQL 질의는 1985년 캐나다와 출생년으로 본국의 모든 사용자를 반환합니다.

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

다음 PQL 쿼리는 1985년 캐나다나 출생년으로 본국 내의 모든 사람을 반환합니다.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## 아님

( `not` 또는 `!`) 함수는 논리적 부정 생성을 위해 사용됩니다.

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

이 `if` 함수는 지정된 조건이 true인지 여부에 따라 표현식을 해결하는 데 사용됩니다.

**형식**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | 테스트 중인 부울 식입니다. |
| `{TRUE_EXPRESSION}` | true인 경우 값이 사용될 표현식 `{TEST_EXPRESSION}` 입니다. |
| `{FALSE_EXPRESSION}` | false일 경우 값을 사용할 표현식 `{TEST_EXPRESSION}` 입니다. |

**예**

다음 PQL 질의는 홈 국가가 캐나다인 `1` 경우, 그리고 해당 국가가 캐나다가 아닌 `2` 경우 이 값을 설정합니다.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## 다음 단계

부울 기능에 대해 알아냈으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).
