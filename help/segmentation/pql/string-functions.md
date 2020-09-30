---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;string functions;string;
solution: Experience Platform
title: 문자열 함수
topic: developer guide
description: PQL(프로필 쿼리 언어)은 문자열과 보다 간편하게 상호 작용하는 기능을 제공합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 6%

---


# 문자열 함수

[!DNL Profile Query Language] (PQL)은 문자열과 보다 간편하게 상호 작용하는 기능을 제공합니다. 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요를 참조하십시오](./overview.md).

## 좋아요

이 `like` 함수는 문자열이 지정된 패턴과 일치하는지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1} like {STRING_2}
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열과 일치하는 표현식. 표현식을 만드는 데 지원되는 두 가지 특수 문자가 있습니다. `%` 및 `_`. <ul><li>`%` 0개 이상의 문자를 나타내는 데 사용됩니다.</li><li>`_` 은 정확히 하나의 문자를 나타내는 데 사용됩니다.</li></ul> |

**예**

다음 PQL 쿼리는 &quot;es&quot; 패턴을 포함하는 모든 도시를 검색합니다.

```sql
city like "%es%"
```

## 다음으로 시작

이 `startsWith` 함수는 문자열이 지정된 하위 문자열로 시작되는지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열 내에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대소문자를 구분하는지 확인하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 사람의 이름이 &quot;Joe&quot;로 시작하는 경우 대/소문자 구분 없이 결정합니다.

```sql
person.name.startsWith("Joe")
```

## 다음으로 시작하지 않음

이 `doesNotStartWith` 함수를 사용하여 문자열이 지정된 하위 문자열로 시작하지 않는지 확인합니다.

**형식**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열 내에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대소문자를 구분하는지 확인하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 개인 이름이 &quot;Joe&quot;로 시작되지 않을 경우 대/소문자 구분 없이 결정합니다.

```sql
person.name.doesNotStartWith("Joe")
```

## 다음으로 끝남

이 `endsWith` 함수는 문자열이 지정된 하위 문자열로 끝났는지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열 내에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대소문자를 구분하는지 확인하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 사용자의 이메일 주소가 &quot;.com&quot;으로 끝나는 경우 대/소문자 구분 없이 결정합니다.

```sql
person.emailAddress.endsWith(".com")
```

## 다음으로 끝나지 않음

이 `doesNotEndWith` 함수는 문자열이 지정된 하위 문자열로 끝나지 않는지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열 내에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대소문자를 구분하는지 확인하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 사용자의 이메일 주소가 &quot;.com&quot;으로 끝나지 않을 경우 대/소문자 구분 없이 결정합니다.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## 다음 포함

이 `contains` 함수는 문자열에 지정된 하위 문자열이 포함되어 있는지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열 내에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대소문자를 구분하는지 확인하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 사용자의 이메일 주소에 &quot;2010@gm&quot; 문자열이 포함된 경우 대/소문자 구분 없이 결정합니다.

```sql
person.emailAddress.contains("2010@gm")
```

## 다음을 포함하지 않음

이 `doesNotContain` 함수는 문자열에 지정된 하위 문자열이 포함되어 있지 않은지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열 내에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대소문자를 구분하는지 확인하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 사용자의 이메일 주소에 &quot;2010@gm&quot; 문자열이 포함되어 있지 않으면 대/소문자 구분 없이 결정합니다.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 다음과 같음

이 `equals` 함수는 문자열이 지정된 문자열과 같은지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.equals({STRING_2})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열과 비교할 문자열. |

**예**

다음 PQL 쿼리는 개인 이름이 &quot;John&quot;인 경우 대/소문자 구분 없이 결정합니다.

```sql
person.name.equals("John")
```

## 같지 않음

이 `notEqualTo` 함수는 문자열이 지정된 문자열과 동일하지 않은지 확인하는 데 사용됩니다.

**형식**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 검사를 수행할 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열과 비교할 문자열. |

**예**

다음 PQL 쿼리는 개인 이름이 &quot;John&quot;이 아닌 경우 대/소문자 구분 없이 결정합니다.

```sql
person.name.notEqualTo("John")
```

## 일치

이 `matches` 함수는 문자열이 특정 정규 표현식과 일치하는지 확인하는 데 사용됩니다. 정규 표현식의 일치 패턴에 대한 자세한 내용은 [이 문서를](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) 참조하십시오.

**형식**

```sql
{STRING_1}.matches(STRING_2})
```

**예**

다음 PQL 쿼리는 사람의 이름이 &quot;John&quot;으로 시작하는 경우 대/소문자를 구분하지 않고 결정합니다.

```sql
person.name.matches("(?i)^John")
```

## 정규 표현식 그룹

이 `regexGroup` 함수는 제공된 정규 표현식을 기반으로 특정 정보를 추출하는 데 사용됩니다.

**형식**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**예**

다음 PQL 질의는 이메일 주소로부터 도메인 이름을 추출하는 데 사용됩니다.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## 다음 단계

이제 문자열 함수에 대해 학습했으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요를 참조하십시오](./overview.md).

