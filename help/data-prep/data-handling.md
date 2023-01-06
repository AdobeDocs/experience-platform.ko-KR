---
keywords: Experience Platform;홈;인기 항목;csv 매핑;csv 파일 매핑;csv 파일을 xdm에 매핑;csv를 xdm에 매핑;ui 안내서;맵;매핑;데이터 준비;데이터 준비;데이터 준비
solution: Experience Platform
title: 데이터 준비를 사용하여 데이터 형식 처리
description: 이 문서에서는 데이터 준비에서 다양한 데이터 유형을 처리하는 방법에 대해 간략하게 설명합니다.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# 데이터 준비를 사용하여 데이터 형식 처리

데이터 준비에서는 Adobe Experience Platform에 수집된 다양한 데이터 형식을 주로 처리할 수 있습니다. 이 문서에서는 데이터 준비로 다양한 데이터 형식을 처리하는 방법을 간략하게 설명합니다.

## 부울 {#booleans}

소스 유형이 문자열이고 대상 유형이 부울인 경우, 데이터 준비에서 자동으로 값을 구문 분석하고 소스 값을 부울로 변환할 수 있습니다.

값 `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`, 및 `TRUE` 자동으로 구문 분석되어 `true`.

값 `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`, 및 `FALSE` 자동으로 구문 분석되어 `false`.

## 날짜 {#dates}

데이터 준비에서는 날짜 함수를 문자열 및 datetime 개체로 지원합니다.

### 날짜 함수 형식

날짜 함수는 문자열 및 datetime 개체를 ISO 8601 형식의 ZoneDateTime 개체로 변환합니다.

**형식**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATE}` | 필수 여부. 날짜를 나타내는 문자열입니다. |
| `{FORMAT}` | 선택 사항입니다. 소스 날짜 형식을 나타내는 문자열입니다. 문자열 서식에 대한 자세한 내용은 [날짜/시간 형식 문자열 섹션](#format). |
| `{DEFAULT_DATE}` | 선택 사항입니다. 제공된 날짜가 null인 경우 반환되는 기본 날짜입니다. |

예: 표현식 `date(orderDate, "yyyy-MM-dd")` 은 `orderDate` &quot;2020년 12월 31일&quot;의 값을 &quot;2020-12-31&quot;의 datetime 값으로 가져옵니다.

### 날짜 함수 전환

수신 데이터의 문자열 필드가 XDM(Experience Data Model)을 사용하여 스키마의 날짜 필드에 매핑되는 경우 날짜 형식이 명시적으로 언급되어야 합니다. 명시적으로 언급되지 않은 경우 데이터 준비에서는 입력 데이터를 다음 형식으로 일치시켜 변환합니다. 일치하는 형식이 발견되면 후속 형식 평가가 중지됩니다.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> 데이터 준비에서는 문자열을 가능한 한 날짜로 변환하려고 합니다. 하지만 이러한 전환은 바람직하지 않은 결과를 초래할 수 있습니다. 예를 들어 문자열 값 &quot;12112020&quot;은 &quot;MmDyyyy&quot; 패턴과 일치하지만 사용자가 날짜를 &quot;ddMMyyyy&quot; 패턴으로 읽으려고 했을 수 있습니다. 따라서 사용자는 문자열의 날짜 형식을 명시적으로 언급해야 합니다.

### 날짜/시간 형식 문자열 {#format}

다음 표는 형식 문자열에 대해 정의된 패턴 문자를 보여줍니다. 문자는 대/소문자를 구분합니다.

| 기호 | 의미 | 프레젠테이션 | 예 |
| ------ | ------- | ------------ | ------- |
| G | 시대 | 텍스트 | AD; 아노 도미니 A |
| Y | 연도, ISO 주 기반 | 숫자 | 1996; 96 |
| y | 연도 | 숫자 | 2004; 04 |
| M/L | 월(연 기준) | 숫자/텍스트 | 7. 07; 7월 7월 J |
| w | 주(해당 연도) | 숫자 | 27 |
| W | 해당 월의 주 | 숫자 | 3 |
| D | 일(한 해 기준) | 숫자 | 189 |
| d | 날짜(월 기준) | 숫자 | 10 |
| F | 한 달에 요일 | 숫자 | 2 |
| E | 요일 이름 | 텍스트 | 화요일; 화 |
| u | 요일(숫자). 1은 월요일을, 7은 일요일을 나타냅니다. | 숫자 | 1 |
| a | 오전/오후 마커 | 텍스트 | PM |
| H | 시간(0-23) | 숫자 | 0 |
| k | 시간(1-24) | 숫자 | 24 |
| K | 오전/오후 시간(0-11) | 숫자 | 0 |
| h | 오전/오후 시간(1-12) | 숫자 | 12 |
| m | 시간(분) | 숫자 | 38 |
| s | 분 중 두 번째 | 숫자 | 44 |
| S | 밀리초 | 숫자 | 245 |
| z | 시간대 | 일반 시간대 | 태평양 표준시 PST; GMT-08:00 |
| Z | 시간대 | RFC 822 시간대 | -0800 |
| X | 시간대 | ISO 8601 시간대 | -08; -0800; -08:00 |
| V | 시간대 ID | 텍스트 | 미국/로스앤젤레스 |
| O | 시간대 오프셋 | 텍스트 | GMT+8 |
| Q/q | 사분기 | 숫자/텍스트 | 3. 03; 3분기; 3분기 |

## 지도 {#maps}

맵은 현재 다음에서 지원되지 않습니다. [!DNL Data Prep].
