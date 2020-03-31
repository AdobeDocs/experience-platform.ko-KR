---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 비교 함수
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# 비교 함수

비교 함수는 서로 다른 표현식과 값을 비교하고, `true` 반환하거나 `false` 그에 따라 비교하는 데 사용됩니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 언어 [개요를](./overview.md)참조하십시오.

## 다음과 같음

(equals) `=` 함수는 한 값이나 표현식이 다른 값이나 표현식과 같은지 여부를 확인합니다.

**형식**

```sql
{EXPRESSION} = {VALUE}
```

**예**

다음 PQL 쿼리는 홈 주소 국가가 캐나다에 있는지 확인합니다.

```sql
homeAddress.countryISO = "CA"
```

## 같지 않음

같지 않음 `!=` 함수는 한 값 또는 표현식이 다른 값 또는 표현식과 **같지 않은지** 확인합니다.

**형식**

```sql
{EXPRESSION} != {VALUE}
```

**예**

다음 PQL 쿼리는 홈 주소 국가가 캐나다에 있지 않은지 확인합니다.

```sql
homeAddress.countryISO != "CA"
```

## 보다 큼

첫 `>` (보다 큼) 함수는 첫 번째 값이 두 번째 값보다 큰지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**예**

다음 PQL 질의는 생일이 1월 또는 2월에 해당되지 않는 사람을 정의합니다.

```sql
person.birthMonth > 2
```

## 크거나 같음

첫 `>=` (보다 크거나 같음) 함수는 첫 번째 값이 두 번째 값보다 크거나 같은지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**예**

다음 PQL 질의는 생일이 1월 또는 2월에 해당되지 않는 사람을 정의합니다.

```sql
person.birthMonth >= 3
```

## 미만

(보다 작음) `<` 비교 함수는 첫 번째 값이 두 번째 값보다 작은지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월에 생일을 맞는 사람을 정의합니다.

```sql
person.birthMonth < 2
```

## 작거나 같음

비교 `<=` (작거나 같음) 함수는 첫 번째 값이 두 번째 값보다 작거나 같은지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월 또는 2월 생일의 사람을 정의합니다.

```sql
person.birthMonth <= 2
```

## 다음 단계

이제 비교 기능에 대해 알아보았으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 프로필 쿼리 [언어 개요를](./overview.md)참조하십시오.
