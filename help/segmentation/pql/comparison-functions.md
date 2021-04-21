---
keywords: Experience Platform;홈;인기 항목;세그멘테이션;세그멘테이션 서비스;pql;PQL;프로필 쿼리 언어;비교 함수;비교;비교;
solution: Experience Platform
title: PQL 비교 함수
topic-legacy: developer guide
description: 비교 함수는 서로 다른 표현식과 값을 비교하고 그에 따라 "true" 또는 "false"를 반환하는 데 사용됩니다.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 9%

---

# 비교 함수

비교 함수는 서로 다른 표현식과 값을 비교하기 위해 사용되며 그에 따라 `true` 또는 `false`을 반환합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)에서 확인할 수 있습니다.

## 다음과 같음

`=`(같음) 함수는 한 값 또는 표현식이 다른 값 또는 표현식과 같은지 여부를 확인합니다.

**형식**

```sql
{EXPRESSION} = {VALUE}
```

**예**

다음 PQL 쿼리는 홈 주소 국가가 캐나다인지 확인합니다.

```sql
homeAddress.countryISO = "CA"
```

## 같지 않음

`!=`(같지 않음) 함수는 한 값 또는 표현식이 다른 값 또는 표현식과 동일한지 **not**&#x200B;인지 확인합니다.

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

`>`(보다 큼) 함수는 첫 번째 값이 두 번째 값보다 큰지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월 또는 2월에 생일을 맞지 않는 사람을 정의합니다.

```sql
person.birthMonth > 2
```

## 크거나 같음

`>=`(보다 크거나 같음) 함수는 첫 번째 값이 두 번째 값보다 크거나 같은지 확인하는 데 사용됩니다.

**형식**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월 또는 2월에 생일을 맞지 않는 사람을 정의합니다.

```sql
person.birthMonth >= 3
```

## 보다 작음

`<`(보다 작음) 비교 함수를 사용하여 첫 번째 값이 두 번째 값보다 작은지 확인합니다.

**형식**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월에 생일을 사용하는 사람을 정의합니다.

```sql
person.birthMonth < 2
```

## 작거나 같음

`<=`(작거나 같음) 비교 함수를 사용하여 첫 번째 값이 두 번째 값보다 작거나 같은지 확인합니다.

**형식**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 1월 또는 2월에 생일을 사용하는 사람을 정의합니다.

```sql
person.birthMonth <= 2
```

## 다음 단계

이제 비교 기능에 대해 배웠으므로 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 기능에 대한 자세한 내용은 [프로필 쿼리 언어 개요](./overview.md)를 참조하십시오.
