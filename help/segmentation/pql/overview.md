---
keywords: Experience Platform;home;popular topics;PQL;pql;profile query language
solution: Experience Platform
title: PQL(프로필 쿼리 언어) 개요
topic: developer guide
description: 이 안내서에서는 서식 지침을 다루는 PQL에 대한 일반적인 개요와 PQL 표현식 예를 제공합니다.
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 2%

---


# [!DNL Profile Query Language] (PQL) 개요

[!DNL Profile Query Language] (PQL)은 [!DNL Experience Data Model] (XDM) 호환 쿼리 언어로서, [!DNL Real-time Customer Profile] 데이터에 대한 세그멘테이션 쿼리의 정의 및 실행을 지원하도록 설계되었습니다.

이 안내서에서는 서식 지침을 다루는 PQL에 대한 일반적인 개요와 PQL 표현식 예를 제공합니다.

## PQL 쿼리 서식

PQL 질의에는 다음 서명이 있습니다.

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

입력 매개 변수는 부울 또는 문자열과 같은 간단한 원시 유형이거나 오브젝트, 배열 또는 맵과 같은 보다 복잡한 유형일 수 있습니다.

PQL 표현식 본문 내의 입력 매개 변수를 참조하는 방법에는 세 가지가 있습니다.

### 첫 번째 매개 변수에 대한 암시적 참조

아래 예에서 첫 번째 매개 변수는 항상 컨텍스트에 있으므로 속성 참조(`homeAddress`)를 직접 해당 매개 변수에 지정할 수 있습니다.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 첫 번째 매개 변수에 대한 명시적 참조

아래 예에서 첫 번째 매개 변수를 `$1` 참조합니다. 따라서 두 번째 매개 변수 등을 `$2` 참조합니다.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 람다 표기법을 사용하여 명명된 변수의 사용

아래 예에서 변수 이름 `Profile` 은 쿼리 작성자가 선택할 수 있습니다.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL 리터럴

PQL은 다음과 같은 문자 유형을 지원합니다.

| 리터럴 | 정의 | 예 |
| ------- | ---------- | ------- |
| 문자열 | 큰 따옴표로 둘러싸인 문자로 구성된 데이터 형식입니다. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| 부울 | true 또는 false인 데이터 형식입니다. | `true`, `false` |
| 정수 | 정수를 나타내는 데이터 형식입니다. 양수, 음수 또는 0일 수 있습니다. | `-201`, `0`, `412` |
| 이중 | 모든 실수를 나타내는 데이터 유형입니다. 양수, 음수 또는 0일 수 있습니다. | `-51.24`, `3.14`, `0.6942058` |
| 날짜 | 연도, 월 및 일을 정수 매개 변수로 기준으로 날짜를 만드는 데 사용할 수 있는 데이터 유형입니다. It is formatted as `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | 다른 리터럴 값의 그룹으로 구성된 데이터 유형입니다. 대괄호를 사용하여 그룹화하고 쉼표를 사용하여 여러 값 간에 구분합니다. <br> **참고:** 배열 내에서 항목의 속성에 직접 액세스할 수는 없습니다. 따라서 배열 내에서 속성에 액세스해야 하는 경우 지원되는 방법이 됩니다 `select X from array where X.item = ...`. <br> PQL은 프로파일에 연결된 경험 이벤트 `xEvent` 의 배열을 참조하기 위해 단어를 예약합니다. | `[1, 4, 7]`, `["US", "CA"]` |
| 상대 시간 참조 | 타임스탬프 및 시간 간격 참조를 구성하는 데 사용할 수 있는 예약된 단어 <ul><li>지금, 어제, 내일</li><li>this, last, next</li><li>before, after, from</li><li>밀리초, 초, 분, 시간, 일, 주, 월, 년, 년, 10년, 세기/세기, 밀레니엄/밀리</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL 함수

다음 표에서는 추가 설명서에 대한 링크를 포함하여 지원되는 PQL 기능의 다양한 범주에 대해 개괄적으로 설명합니다.

| 카테고리 | 정의 |
| -------- | ---------- |
| 부울 | PQL 내에서 부울 대수를 구현하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [부울 함수 문서에서 확인할 수 있습니다](./boolean-functions.md). |
| 비교 | 서로 다른 PQL 요소 간을 비교하는 데 사용됩니다. 이러한 기능에 대한 자세한 내용은 [비교 함수 문서에서 확인할 수 있습니다](./comparison-functions.md). |
| 배열, 목록 및 설정 | 배열, 목록 및 세트와 상호 작용하는 데 사용됩니다. 이러한 기능에 대한 자세한 내용은 [배열, 목록 및 집합 함수 문서에서 확인할 수 있습니다](./array-functions.md). |
| 맵 | 맵과 상호 작용하는 데 사용됩니다. 이러한 기능에 대한 자세한 내용은 [지도 함수 문서에서 확인할 수 있습니다](./map-functions.md). |
| 문자열 | 문자열과 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [문자열 함수 문서에서 확인할 수 있습니다](./string-functions.md). |
| 개체 | 개체와 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [개체 함수 문서에서 확인할 수 있습니다](./object-functions.md). |
| 산술 | PQL 요소에서 기본 산술을 수행하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [산술 함수 문서에서 확인할 수 있습니다](./arithmetic-functions.md) |
| 집계 | 배열의 결과를 하나의 결과로 결합하는 데 사용됩니다. 집계 기능에 대한 자세한 내용은 [집계 함수 문서에서 확인할 수 있습니다](./aggregation-functions.md). |
| 날짜 및 시간 | date, time 및 datetime 개체와 함께 사용됩니다. 이러한 기능에 대한 자세한 내용은 [날짜/시간 함수 문서에서 확인할 수 있습니다](./datetime-functions.md). |
| 필터 | 배열 내의 데이터를 필터링하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [필터 함수 문서에서 확인할 수 있습니다](./filter-functions.md). |
| 논리적 수량자 | 배열 내의 조건을 구현하는 데 사용됩니다. 자세한 내용은 [논리적 수량자 문서에서 확인할 수 있습니다](./logical-quantifiers.md). |
| 기타 | 위의 카테고리에 맞지 않는 함수는 기타 [함수 문서에서 찾을 수 있습니다](./misc-functions.md). |

## 다음 단계

이제 세그먼트 작성 및 수정 시 PQL [!DNL Profile Query Language]을 사용할 수 있습니다. 세그멘테이션에 대한 자세한 내용은 [세그멘테이션 개요를 참조하십시오](../home.md).