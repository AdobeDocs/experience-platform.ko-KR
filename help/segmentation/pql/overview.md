---
keywords: Experience Platform;홈;인기 항목;PQL;프로필 쿼리 언어
solution: Experience Platform
title: PQL(프로파일 쿼리 언어) 개요
topic: developer guide
description: 이 안내서에서는 서식 지침을 다루는 PQL에 대한 일반적인 개요와 PQL 표현식 예를 제공합니다.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---


# [!DNL Profile Query Language] (PQL) 개요

[!DNL Profile Query Language] (PQL)은  [!DNL Experience Data Model] (XDM) 호환 쿼리 언어로서, 데이터에 대한 세그멘테이션 쿼리의 정의 및 실행을 지원하기 위해  [!DNL Real-time Customer Profile] 설계되었습니다.

이 안내서에서는 서식 지침을 다루는 PQL에 대한 일반적인 개요와 PQL 표현식 예를 제공합니다.

## PQL 쿼리 서식 지정

PQL 쿼리에는 다음 서명이 있습니다.

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

입력 매개 변수는 부울 또는 문자열 등의 간단한 프리미티브 유형이거나 객체, 배열 또는 맵과 같은 보다 복잡한 유형이 될 수 있습니다.

PQL 표현식의 본문 내에서 입력 매개 변수를 참조하는 방법에는 세 가지가 있습니다.

### 첫 번째 매개 변수에 대한 암시적 참조

아래 예에서 첫 번째 매개 변수는 항상 컨텍스트에 있으므로 속성 참조(`homeAddress`)를 직접 해당 매개 변수에 지정할 수 있습니다.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 첫 번째 매개 변수에 대한 명시적 참조

아래 예에서 `$1`은 첫 번째 매개 변수를 참조합니다. 따라서 `$2`은 두 번째 매개 변수 등을 참조합니다.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 람다 표기법을 사용하여 명명된 변수의 사용

아래 예에서 `Profile`은 쿼리 작성자가 선택할 수 있는 변수 이름입니다.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL 리터럴

PQL은 다음과 같은 문자 유형을 지원합니다.

| 리터럴 | 정의 | 예 |
| ------- | ---------- | ------- |
| 문자열 | 큰따옴표로 둘러싸인 문자로 구성된 데이터 유형입니다. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| 부울 | true 또는 false인 데이터 유형입니다. | `true`, `false` |
| 정수 | 정수를 나타내는 데이터 유형입니다. 양수, 음수 또는 0일 수 있습니다. | `-201`,  `0`  `412` |
| 이중 | 실수를 나타내는 데이터 유형입니다. 양수, 음수 또는 0일 수 있습니다. | `-51.24`,  `3.14`  `0.6942058` |
| 날짜 | 연도, 월 및 일을 정수 매개 변수로 기준으로 날짜를 만드는 데 사용할 수 있는 데이터 유형입니다. 이 형식은 `date(year, month, day)`로 지정됩니다. | `date(2020, 3, 14)` |
| 배열 | 다른 리터럴 값의 그룹으로 구성되는 데이터 유형입니다. 여러 값을 구분하기 위해 대괄호를 그룹화하고 쉼표를 사용합니다.<br> **참고: 배열** 내의 항목의 속성에 직접 액세스할 수는 없습니다. 따라서 배열 내에서 속성에 액세스해야 하는 경우 지원되는 메서드는 `select X from array where X.item = ...`입니다. <br> PQL은 프로필 `xEvent` 에 연결된 경험 이벤트 배열을 참조하기 위해 단어를 예약합니다. | `[1, 4, 7]`,  `["US", "CA"]` |
| 상대 시간 참조 | 타임스탬프 및 시간 간격 참조를 구성하는 데 사용할 수 있는 예약된 단어 <ul><li>이제, 오늘, 어제, 내일</li><li>마지막, 다음</li><li>이전, 이후,</li><li>밀리초, 초, 분, 시간, 일, 주, 월, 연도, 년, 10년, 세기/세기, 밀레니엄/밀레니아</li></ul> | `X.timestamp occurs before today`,  `X.timestamp occurs last month`  `X.timestamp occurs <= 3 days before now` |


## PQL 함수

다음 표는 추가 설명서로 연결되는 링크를 비롯하여 지원되는 PQL 함수의 여러 카테고리에 대해 간략하게 설명합니다.

| 카테고리 | 정의 |
| -------- | ---------- |
| 부울 | PQL 내에서 부울 대수를 구현하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [부울 함수 문서](./boolean-functions.md)에서 확인할 수 있습니다. |
| 비교 | 다른 PQL 요소 간을 비교하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [비교 함수 문서](./comparison-functions.md)에서 확인할 수 있습니다. |
| 배열, 목록 및 세트 | 배열, 목록 및 세트와 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [array, list 및 set functions 문서](./array-functions.md)에서 확인할 수 있습니다. |
| 맵 | 맵과 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [맵 함수 문서](./map-functions.md)에서 확인할 수 있습니다. |
| 문자열 | 문자열과 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [문자열 함수 문서](./string-functions.md)에서 확인할 수 있습니다. |
| 개체 | 개체와 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [개체 함수 문서](./object-functions.md)에서 확인할 수 있습니다. |
| 산술 | PQL 요소에서 기본 산술을 수행하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [산술 함수 문서](./arithmetic-functions.md)에서 확인할 수 있습니다. |
| 집계 | 배열의 결과를 하나의 결과로 결합하는 데 사용됩니다. 집계 함수에 대한 자세한 내용은 [집계 함수 문서](./aggregation-functions.md)에서 확인할 수 있습니다. |
| 날짜 및 시간 | date, time 및 datetime 객체와 함께 사용됩니다. 이러한 함수에 대한 자세한 내용은 [date/time functions 문서](./datetime-functions.md)에서 확인할 수 있습니다. |
| 필터 | 배열 내의 데이터를 필터링하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [필터 함수 문서](./filter-functions.md)에서 확인할 수 있습니다. |
| 논리적 한정 기호 | 배열 내의 조건을 구현하는 데 사용됩니다. 자세한 내용은 [논리적 수량자 문서](./logical-quantifiers.md)에서 확인할 수 있습니다. |
| 기타 | 위의 카테고리에 맞지 않는 함수는 [기타 함수 문서](./misc-functions.md)에서 찾을 수 있습니다. |

## 다음 단계

이제 [!DNL Profile Query Language]을 사용하는 방법을 알았으므로 세그먼트를 만들고 수정할 때 PQL을 사용할 수 있습니다. 세그멘테이션에 대한 자세한 내용은 [세그멘테이션 개요](../home.md)를 참조하십시오.