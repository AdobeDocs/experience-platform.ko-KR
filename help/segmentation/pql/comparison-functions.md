---
solution: Experience Platform
title: PQL 비교 함수
description: 비교 함수는 다른 표현식과 값을 비교하는 데 사용되며, 그에 따라 "true" 또는 "false"를 반환합니다.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 7%

---

# 비교 함수

비교 함수는 다른 표현식과 값을 비교하는 데 사용되며 그에 따라 `true` 또는 `false`을(를) 반환합니다. 다른 PQL 함수에 대한 자세한 내용은 [[!DNL Profile Query Language] 개요](./overview.md)를 참조하세요.

## 같음

`=`(equals) 함수는 하나의 값 또는 식이 다른 값 또는 식과 같은지 확인합니다.

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

`!=`(같지 않음) 함수는 하나의 값 또는 식이 다른 값 또는 식과 **같지 않음**&#x200B;인지 확인합니다.

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

`>`(큼) 함수는 첫 번째 값이 두 번째 값보다 큰지 확인하는 데 사용합니다.

**형식**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 생일이 1월이나 2월이 아닌 사람을 정의합니다.

```sql
person.birthMonth > 2
```

## 보다 크거나 같음

`>=`(크거나 같음) 함수는 첫 번째 값이 두 번째 값보다 크거나 같은지 확인하는 데 사용합니다.

**형식**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 생일이 1월이나 2월이 아닌 사람을 정의합니다.

```sql
person.birthMonth >= 3
```

## 보다 작음

`<`(작음) 비교 함수는 첫 번째 값이 두 번째 값보다 작은지 확인하는 데 사용합니다.

**형식**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 생일이 1월인 사람을 정의합니다.

```sql
person.birthMonth < 2
```

## 보다 작거나 같음

`<=`(작거나 같음) 비교 함수는 첫 번째 값이 두 번째 값보다 작거나 같은지 확인하는 데 사용합니다.

**형식**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**예**

다음 PQL 쿼리는 생일이 1월 또는 2월인 사람을 정의합니다.

```sql
person.birthMonth <= 2
```

## 다음 단계

비교 함수에 대해 배웠으므로 이제 PQL 쿼리 내에서 사용할 수 있습니다. 다른 PQL 함수에 대한 자세한 내용은 [Profile Query Language 개요](./overview.md)를 참조하십시오.
