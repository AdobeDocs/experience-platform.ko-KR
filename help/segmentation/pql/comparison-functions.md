---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;비교 함수;비교;
solution: Experience Platform
title: PQL 비교 함수
description: 비교 함수는 다른 표현식과 값 간을 비교하고 그에 따라 "true" 또는 "false"를 반환하는 데 사용됩니다.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 비교 함수

비교 함수는 다른 표현식과 값 간을 비교하고, `true` 또는 `false` 따라서, 다른 PQL 기능에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md).

## 다음과 같음

다음 `=` (equals) 함수는 한 값 또는 표현식이 다른 값 또는 표현식과 같은지 여부를 확인합니다.

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

다음 `!=` (같지 않음) 함수는 값 또는 표현식이 있는지 여부를 확인합니다 **not** 다른 값 또는 표현식과 같음.

**형식**

```sql
{EXPRESSION} != {VALUE}
```

**예**

다음 PQL 쿼리는 홈 주소 국가가 캐나다에 없는지 확인합니다.

```sql
homeAddress.countryISO != "CA"
```

## 보다 큼

다음 `>` (보다 큼) 함수는 첫 번째 값이 두 번째 값보다 커야 하는지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**예**

다음 PQL 질의는 생일이 1월이나 2월에 해당되지 않는 사람을 정의합니다.

```sql
person.birthMonth > 2
```

## 크거나 같음

다음 `>=` (크거나 같음) 함수는 첫 번째 값이 두 번째 값보다 크거나 같은지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**예**

다음 PQL 질의는 생일이 1월이나 2월에 해당되지 않는 사람을 정의합니다.

```sql
person.birthMonth >= 3
```

## 미만

다음 `<` (보다 작음) 비교 함수를 사용하여 첫 번째 값이 두 번째 값보다 작은지 확인합니다.

**형식**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월에 생일이 속하는 사람을 정의합니다.

```sql
person.birthMonth < 2
```

## 작거나 같음

다음 `<=` (작거나 같음) 비교 함수를 사용하여 첫 번째 값이 두 번째 값보다 작거나 같은지 확인합니다.

**형식**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**예**

다음 PQL 질의는 생일이 1월 또는 2월인 사용자를 정의합니다.

```sql
person.birthMonth <= 2
```

## 다음 단계

이제 비교 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md).
