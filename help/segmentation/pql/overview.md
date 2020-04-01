---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PQL(프로필 쿼리 언어) 개요
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# PQL(프로필 쿼리 언어) 개요

PQL(Profile Query Language)은 XDM(Experience Data Model) 호환 쿼리 언어로, 실시간 고객 프로필 데이터에 대한 세그멘테이션 쿼리의 정의 및 실행을 지원하도록 설계되었습니다.

이 안내서에서는 서식 지침을 다루는 PQL에 대한 일반적인 개요와 PQL 표현식 예를 제공합니다.

## PQL 쿼리 서식

PQL 쿼리에는 다음 서명이 있습니다.

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

입력 매개 변수는 부울 또는 문자열과 같은 간단한 프리미티브이거나 오브젝트, 배열 또는 맵과 같은 복잡한 유형일 수 있습니다.

PQL 표현식 본문 내에서 입력 매개 변수를 참조하는 **세 가지** 방법이 있습니다.

### 첫 번째 매개 변수에 대한 암시적 참조

아래 예에서 첫 번째 매개 변수가 항상 컨텍스트에 있기 때문에 속성 참조(`homeAddress`)를 직접 만들 수 있습니다.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### 첫 번째 매개 변수에 대한 명시적 참조

아래 예에서는 `$1` 첫 번째 매개 변수를 참조합니다. 따라서 두 번째 매개 변수 `$2` 등을 참조합니다.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### 람다 표기법을 사용하여 명명된 변수의 사용

아래 예에서 변수 이름은 쿼리 작성자가 선택할 수 `Profile` 있습니다.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL 리터럴

PQL은 다음과 같은 문자 유형을 지원합니다.

| 리터럴 | 정의 | 예 |
| ------- | ---------- | ------- |
| 문자열 | 큰따옴표로 둘러싸인 문자로 구성된 데이터 유형입니다. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| 부울 | true 또는 false인 데이터 유형입니다. | `true`, `false` |
| 정수 | 정수를 나타내는 데이터 유형입니다. 양수, 음수 또는 0일 수 있습니다. | `-201`, `0`, `412` |
| 이중 | 모든 실수를 나타내는 데이터 유형입니다. 양수, 음수 또는 0일 수 있습니다. | `-51.24`, `3.14`, `0.6942058` |
| 날짜 | 연도, 월 및 일을 정수 매개 변수로 기준으로 날짜를 만드는 데 사용할 수 있는 데이터 유형입니다. 형식이 `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | 다른 리터럴 값의 그룹으로 구성된 데이터 유형입니다. 대괄호를 사용하여 그룹화하고 쉼표를 사용하여 여러 값 간에 구분합니다. <br> **참고:** 배열 내에서 항목의 속성에 직접 액세스할 수는 없습니다. 따라서 배열 내에서 속성에 액세스해야 하는 경우 지원되는 방법이 `select X from array where X.item = ...`됩니다. <br> PQL은 프로파일에 연결된 경험 이벤트 배열을 `xEvent` 참조하는 단어를 예약합니다. | `[1, 4, 7]`, `["US", "CA"]` |
| 상대적 시간 참조 | 타임스탬프 및 시간 간격 참조를 구성하는 데 사용할 수 있는 예약어입니다. <ul><li>오늘, 어제, 내일</li><li>this, last, next</li><li>before, after, from</li><li>밀리초(초), 초, 분, 시간, 시간, 일, 주, 월, 년, 10년, 세기/세기, 밀레니엄/밀리</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL 함수

다음 표에서는 자세한 내용을 보려면 추가 설명서에 대한 링크를 포함하여 지원되는 PQL 함수의 여러 범주에 대해 간략하게 설명합니다.

| 카테고리 | 정의 |
| -------- | ---------- |
| 부울 | PQL 내에서 부울 대수를 구현하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [부울 함수 문서에서](./boolean-functions.md)확인할 수 있습니다. |
| 비교 | 서로 다른 PQL 요소 간에 비교하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [비교 함수 문서에서](./comparison-functions.md)확인할 수 있습니다. |
| 배열, 목록 및 설정 | 배열, 목록 및 세트와 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [배열, 목록 및 집합 함수 문서에서](./array-functions.md)확인할 수 있습니다. |
| 맵 | 맵과 상호 작용하는 데 사용됩니다. 이러한 기능에 대한 자세한 내용은 [지도 함수 문서에서](./map-functions.md)확인할 수 있습니다. |
| 문자열 | 문자열과 상호 작용하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [문자열 함수 문서에서](./string-functions.md)확인할 수 있습니다. |
| 산술 | PQL 요소에서 기본 산술을 수행하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [산술 함수 문서에서 확인할 수 있습니다](./arithmetic-functions.md) |
| 집계 | 배열의 결과를 하나의 결과로 결합하는 데 사용됩니다. 집계 함수에 대한 자세한 내용은 [집계 함수 문서에서](./aggregation-functions.md)확인할 수 있습니다. |
| 날짜 및 시간 | date, time 및 datetime 개체와 함께 사용됩니다. 이러한 기능에 대한 자세한 내용은 [날짜/시간 함수 문서에서](./datetime-functions.md)확인할 수 있습니다. |
| 필터 | 배열 내에서 데이터를 필터링하는 데 사용됩니다. 이러한 함수에 대한 자세한 내용은 [필터 함수 문서에서](./filter-functions.md)확인할 수 있습니다. |
| 논리적 수량자 | 배열 내의 조건을 구현하는 데 사용됩니다. 자세한 내용은 [논리적 수량자 문서에서](./logical-quantifiers.md)찾을 수 있습니다. |
| 기타 | 위의 범주에 속하지 않는 함수는 [기타 함수 문서에서](./misc-functions.md)찾을 수 있습니다. |

## 다음 단계

프로필 쿼리 언어 사용 방법을 살펴보았으므로 세그먼트를 만들고 수정할 때 PQL을 사용할 수 있습니다. 세그멘테이션에 대한 자세한 내용은 [세그멘테이션 개요를](../home.md)참조하십시오.