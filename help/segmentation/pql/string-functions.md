---
solution: Experience Platform
title: PQL 문자열 함수
description: Profile Query Language(PQL)는 문자열과 상호 작용을 더 간단하게 하는 함수를 제공합니다.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 5%

---

# 문자열 함수

[!DNL Profile Query Language](PQL)에서는 문자열과의 상호 작용을 더 간단하게 하는 함수를 제공합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 좋아요

`like` 함수는 문자열이 지정된 패턴과 부울로 일치하는지 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1} like {STRING_2}
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열과 일치하는 표현식. 식을 만드는 데 지원되는 특수 문자 `%`과(와) `_`이(가) 있습니다. <ul><li>`%`은(는) 0개 이상의 문자를 나타내는 데 사용됩니다.</li><li>`_`은(는) 정확히 하나의 문자를 나타내는 데 사용됩니다.</li></ul> |

**예**

다음 PQL 쿼리는 &quot;es&quot; 패턴을 포함하는 모든 도시를 검색합니다.

```sql
city like "%es%"
```

## 다음으로 시작

`startsWith` 함수는 문자열이 지정된 하위 문자열로 부울로 시작하는지 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대/소문자를 구분하는지 여부를 결정하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 대/소문자 구분을 통해 개인의 이름이 &quot;Joe&quot;로 시작하는지 여부를 결정합니다.

```sql
person.name.startsWith("Joe")
```

## 다음으로 시작하지 않음

`doesNotStartWith` 함수는 문자열이 지정된 하위 문자열로 부울로 시작되지 않는지 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대/소문자를 구분하는지 여부를 결정하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 대소문자 구분을 통해 개인의 이름이 &quot;Joe&quot;로 시작되지 않는지 여부를 결정합니다.

```sql
person.name.doesNotStartWith("Joe")
```

## 다음으로 끝남

`endsWith` 함수는 문자열이 지정된 하위 문자열로 끝나는지 부울로 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대/소문자를 구분하는지 여부를 결정하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 대소문자 구분을 통해 개인의 이메일 주소가 &quot;.com&quot;으로 끝나는지 여부를 결정합니다.

```sql
person.emailAddress.endsWith(".com")
```

## 다음으로 끝나지 않음

`doesNotEndWith` 함수는 문자열이 지정된 하위 문자열(부울)로 끝나지 않은지 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대/소문자를 구분하는지 여부를 결정하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 대소문자 구분을 통해 개인의 이메일 주소가 &quot;.com&quot;으로 끝나지 않는 경우를 결정합니다.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## 다음 포함

`contains` 함수는 문자열에 지정된 하위 문자열이 부울로 포함되어 있는지 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대/소문자를 구분하는지 여부를 결정하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 대소문자 구분을 통해 개인의 이메일 주소에 문자열 &quot;2010@gm&quot;이 포함되어 있는지 여부를 결정합니다.

```sql
person.emailAddress.contains("2010@gm")
```

## 포함하지 않음

`doesNotContain` 함수는 문자열에 지정된 하위 문자열이 부울로 포함되어 있지 않은지 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열에서 검색할 문자열입니다. |
| `{BOOLEAN}` | 검사가 대/소문자를 구분하는지 여부를 결정하는 선택적 매개 변수입니다. 기본적으로 true로 설정됩니다. |

**예**

다음 PQL 쿼리는 대소문자 구분을 통해 개인의 이메일 주소에 문자열 &quot;2010@gm&quot;이 포함되어 있지 않은지 결정합니다.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## 같음

`equals` 함수는 문자열이 지정된 문자열과 같은지 부울로 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.equals({STRING_2})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열과 비교할 문자열입니다. |

**예**

다음 PQL 쿼리는 대/소문자 구분을 통해 개인의 이름이 &quot;John&quot;인지 여부를 결정합니다.

```sql
person.name.equals("John")
```

## 다음과 같지 않음

`notEqualTo` 함수는 문자열이 지정된 문자열과 같지 않은지 부울로 확인하는 데 사용합니다.

**형식**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| 인수 | 설명 |
| --------- | ----------- |
| `{STRING_1}` | 확인을 수행하는 문자열입니다. |
| `{STRING_2}` | 첫 번째 문자열과 비교할 문자열입니다. |

**예**

다음 PQL 쿼리는 대소문자 구분을 통해 개인의 이름이 &quot;John&quot;이 아님을 확인합니다.

```sql
person.name.notEqualTo("John")
```

## 일치

`matches` 함수는 문자열이 특정 정규 표현식과 일치하는지 확인하는 데 사용합니다. 부울로 사용되는 정규 표현식의 패턴 일치에 대한 자세한 내용은 [이 문서](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html)을 참조하십시오.

**형식**

```sql
{STRING_1}.matches(STRING_2})
```

**예**

다음 PQL 쿼리는 대/소문자를 구분하지 않고 개인 이름이 &quot;John&quot;으로 시작하는지 여부를 결정합니다.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>`\w`과(와) 같은 정규 표현식 함수를 사용하는 경우 **반드시** 백슬래시 문자를 이스케이프 처리합니다. 따라서 `\w`만 쓰는 대신 추가 백슬래시를 포함하고 `\\w`을(를) 써야 합니다.

## 정규 표현식 그룹

`regexGroup` 함수는 문자열로 제공되는 정규 표현식을 기반으로 특정 정보를 추출하는 데 사용합니다.

**형식**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**예**

다음 PQL 쿼리는 이메일 주소에서 도메인 이름을 추출하는 데 사용됩니다.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>`\w`과(와) 같은 정규 표현식 함수를 사용하는 경우 **반드시** 백슬래시 문자를 이스케이프 처리합니다. 따라서 `\w`만 쓰는 대신 추가 백슬래시를 포함하고 `\\w`을(를) 써야 합니다.

## 다음 단계

이제 문자열 함수에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
