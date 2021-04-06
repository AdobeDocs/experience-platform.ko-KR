---
keywords: Experience Platform;홈;인기 항목;csv;맵 csv;csv 파일;csv 파일을 xdm에 매핑;csv를 xdm;ui 안내서;매퍼;매핑;매핑 필드;매핑 기능;매핑 함수
solution: Experience Platform
title: 데이터 준비 매핑 함수
topic: 개요
description: 이 문서에서는 데이터 준비와 함께 사용되는 매핑 함수를 소개합니다.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
translation-type: tm+mt
source-git-commit: 21782ee74adfe97fa0a88f499d01393155691b29
workflow-type: tm+mt
source-wordcount: '3793'
ht-degree: 3%

---

# 데이터 준비 매핑 함수

데이터 준비 함수를 사용하여 소스 필드에 입력된 값을 기반으로 값을 계산하고 계산할 수 있습니다.

## 필드

필드 이름은 문자, 달러 기호(`$`) 또는 밑줄 문자(`_`)로 시작하는 유니코드 문자 및 자릿수의 무제한 길이 시퀀스로 모든 법적 식별자가 될 수 있습니다. 변수 이름은 대소문자를 구분합니다.

필드 이름이 이 규칙을 따르지 않으면 필드 이름은 `${}`으로 둘러싸야 합니다. 예를 들어 필드 이름이 &quot;이름&quot; 또는 &quot;이름&quot;인 경우 이름이 각각 `${First Name}` 또는 `${First.Name}`과 같이 둘러싸야 합니다.

또한 필드 이름이 다음 예약 키워드의 **임의의**&#x200B;인 경우 `${}`로 둘러싸야 합니다.

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

도트 표기법을 사용하여 하위 필드 내의 데이터에 액세스할 수 있습니다. 예를 들어 `name` 객체가 있는 경우 `firstName` 필드에 액세스하려면 `name.firstName`를 사용합니다.

## 함수 목록

다음 표는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 함수를 나열합니다.

### 문자열 함수 {#string}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | 지정된 문자열을 연결합니다. | <ul><li>문자열:연결할 문자열입니다.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | regex를 기반으로 문자열을 분할하고 부분 배열을 반환합니다. 선택적으로 regex를 포함하여 문자열을 분할할 수 있습니다. 기본적으로 분할은 &quot;,&quot;로 확인됩니다. `\`에서 이스케이프해야 하는 **구분 기호**&#x200B;는 다음과 같습니다.`+, ?, ^, |, ., [, (, {, ), *, $, \` 구분 기호로 여러 문자를 포함하는 경우 구분 기호는 다중 문자 구분 기호로 처리됩니다. | <ul><li>문자열:**필수** 분할해야 하는 문자열입니다.</li><li>REGEX:*선택적* 문자열을 분할하는 데 사용할 수 있는 정규 표현식.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot;) | `["Hi,", "there"]` |
| instant | 하위 문자열의 위치/인덱스를 반환합니다. | <ul><li>입력:**필수** 검색되는 문자열입니다.</li><li>하위 문자열:**필수** 문자열 내에서 검색되는 하위 문자열입니다.</li><li>START_POSITION:*선택적* 문자열에서 찾을 위치의 위치입니다.</li><li>발생:*선택 사항* 시작 위치에서 찾을 n번째 항목입니다. 기본적으로 1입니다. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| 교체 | 원래 문자열에 있는 경우 검색 문자열을 대체합니다. | <ul><li>입력:**필수** 입력 문자열입니다.</li><li>TO_FIND:**필수** 입력 내에서 찾을 문자열입니다.</li><li>TO_REPLACE:**필수** &quot;TO_FIND&quot; 내의 값을 대체할 문자열입니다.</li></ul> | replacestor(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;문자열 재테스트&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 대체 테스트입니다.&quot; |
| substr | 주어진 길이의 하위 문자열을 반환합니다. | <ul><li>입력:**필수** 입력 문자열입니다.</li><li>START_INDEX:**필수** 하위 문자열이 시작되는 입력 문자열의 인덱스입니다.</li><li>길이:**필수** 하위 문자열의 길이입니다.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;하위 문자열 테스트입니다&quot;, 7, 8) | &quot; 하위 항목&quot; |
| lcase /<br>lcase | 문자열을 소문자로 변환합니다. | <ul><li>입력:**필수** 소문자로 변환할 문자열입니다.</li></ul> | lower(INPUT) | lower(&quot;HeLlO&quot;)<br>lcase(&quot;HeLlO&quot;) | &quot;hello&quot; |
| upper /<br>uase | 문자열을 대문자로 변환합니다. | <ul><li>입력:**필수** 대문자로 변환할 문자열입니다.</li></ul> | upper(INPUT) | upper(&quot;HeLlO&quot;)<br>uase(&quot;HeLlO&quot;) | &quot;HELLO&quot; |
| split | 구분 기호로 입력 문자열을 분할합니다. 다음 구분 문자 **에**&#x200B;을(를) `\`로 이스케이프해야 합니다.`\`. 여러 구분 기호를 포함하는 경우 문자열이 문자열에 있는 구분 기호의 **임의의**&#x200B;에서 분할됩니다. | <ul><li>입력:**필수** 분할할 입력 문자열입니다.</li><li>구분 기호:**필수** 입력 내용을 분할하는 데 사용되는 문자열입니다.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | 구분 기호를 사용하여 개체 목록을 연결합니다. | <ul><li>구분 기호:**필수** 개체에 연결하는 데 사용할 문자열입니다.</li><li>개체:**필수** 연결할 문자열 배열입니다.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | 문자열의 왼쪽 끝에 지정된 문자열을 넣습니다. | <ul><li>입력:**필수** 채워질 문자열입니다. 이 문자열은 null일 수 있습니다.</li><li>카운트:**필수** 채울 문자열의 크기입니다.</li><li>패딩:**필수** 입력 내용을 패딩하는 문자열입니다. null 또는 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | lpad(입력, 카운트, 패딩) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzygybat&quot; |
| rpad | 지정된 다른 문자열을 사용하여 문자열의 오른쪽에 패드를 넣습니다. | <ul><li>입력:**필수** 채워질 문자열입니다. 이 문자열은 null일 수 있습니다.</li><li>카운트:**필수** 채울 문자열의 크기입니다.</li><li>패딩:**필수** 입력 내용을 패딩하는 문자열입니다. null 또는 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | rpad(입력, 카운트, 패딩) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | 지정된 문자열의 첫 번째 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열:**필수** 첫 번째 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트:**필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자입니다.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | 지정된 문자열의 마지막 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열:**필수** 마지막 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트:**필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자입니다.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| 트리밍 | 문자열 시작 부분에서 공백을 제거합니다. | <ul><li>문자열:**필수** 공백을 제거할 문자열입니다.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| 트리밍 | 문자열 끝에서 공백을 제거합니다. | <ul><li>문자열:**필수** 공백을 제거할 문자열입니다.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | 문자열의 시작 부분과 끝 부분에서 공백을 제거합니다. | <ul><li>문자열:**필수** 공백을 제거할 문자열입니다.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 다음과 같음 | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분합니다. | <ul><li>STRING1:**필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2:**필수** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equals( &#x200B;STRING2) | &quot;string1&quot;&#x200B;을 참조하십시오.같음(&quot;&#x200B;STRING1&quot;) | false |
| equalsIgnoreCase | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 **대/소문자를 구분하지 않습니다.** | <ul><li>STRING1:**필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2:**필수** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;&#x200B;을 참조하십시오.equalsIgnoreCase(&quot;&#x200B;STRING1)) | true |

{style=&quot;table-layout:auto&quot;}

### 정규 표현식 함수

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | 정규 표현식을 기반으로 입력 문자열에서 그룹을 추출합니다. | <ul><li>문자열:**필수** 그룹을 추출하는 문자열입니다.</li><li>REGEX:**필수** 그룹을 일치시킬 정규 표현식.</li></ul> | extract_regex(STRING, REGEX) | extract_regex(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;)) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | 문자열이 입력된 정규 표현식과 일치하는지 확인합니다. | <ul><li>문자열:**필수** 검사 중인 문자열이 정규 표현식과 일치합니다.</li><li>REGEX:**필수** 비교할 일반 표현식.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### 해시 함수 {#hashing}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | SHA-1(보안 해시 알고리즘 1)을 사용하여 입력을 받고 해시 값을 생성합니다. | <ul><li>입력:**필수** 해시할 일반 텍스트입니다.</li><li>문자 세트:*선택적* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | 입력 내용을 가져와 보안 해시 알고리즘 256(SHA-256)을 사용하여 해시 값을 생성합니다. | <ul><li>입력:**필수** 해시할 일반 텍스트입니다.</li><li>문자 세트:*선택적* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha256(입력, 문자 집합) | sha256(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 입력 내용을 가져와 보안 해시 알고리즘 512(SHA-512)를 사용하여 해시 값을 생성합니다. | <ul><li>입력:**필수** 해시할 일반 텍스트입니다.</li><li>문자 세트:*선택적* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha512(입력, 문자 집합) | sha512(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b3b8c9c2163c21ef 708bf11b4232bb21d2a8704ada2cdcd7b367dd078dd a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | MD5를 사용하여 입력을 받고 해시 값을 생성합니다. | <ul><li>입력:**필수** 해시할 일반 텍스트입니다.</li><li>문자 세트:*선택적* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다. </li></ul> | md5(입력, 문자 세트) | md5(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | 입력은 CRC(순환 중복 검사) 알고리즘을 사용하여 32비트 순환 코드를 생성합니다. | <ul><li>입력:**필수** 해시할 일반 텍스트입니다.</li><li>문자 세트:*선택적* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | crc32(입력, 문자 집합) | crc32(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL 함수 {#url}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_protocol | 지정된 URL에서 프로토콜을 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL:**필수** 프로토콜을 추출해야 하는 URL입니다.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 지정된 URL의 호스트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL:**필수** 호스트를 추출해야 하는 URL입니다.</li></ul> | get_url_host&#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 지정된 URL의 포트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL:**필수** 포트를 추출해야 하는 URL입니다.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 지정된 URL의 경로를 반환합니다. 기본적으로 전체 경로가 반환됩니다. | <ul><li>URL:**필수** 경로를 추출해야 하는 URL입니다.</li><li>FULL_PATH:*선택적* 전체 경로가 반환되는지 여부를 결정하는 부울 값입니다. false로 설정하면 경로의 끝만 반환됩니다.</li></ul> | get_url_&#x200B;path(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | 지정된 URL의 쿼리 문자열을 반환합니다. | <ul><li>URL:**필수** 쿼리 문자열을 가져오려는 URL입니다.</li><li>앵커:**필수** 쿼리 문자열에서 앵커로 수행할 작업을 결정합니다. 다음 3개 값 중 하나일 수 있습니다.&quot;retain&quot;, &quot;remove&quot; 또는 &quot;append&quot;를 클릭합니다.<br><br>값이 &quot;retain&quot;이면 반환된 값에 앵커가 추가됩니다.<br>값이 &quot;remove&quot;이면 반환된 값에서 앵커가 제거됩니다.<br>값이 &quot;append&quot;이면 앵커가 별도의 값으로 반환됩니다.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str(&quot;foo://example.com:8042//over/there?name=&#x200B;을) ferrete#nose를 &#x200B;), &quot;rette&quot;<br>get_url_str(&quot;foo://example.com:8042을 사용하여 //?name=을을, &quot;제거&quot;))&lt;get_url_url을 get_url이_이 될 수 있습니다. #noes&quot;, &quot;append&quot;)<br> | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### 날짜 및 시간 함수 {#date-and-time}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오. `date` 함수에 대한 자세한 내용은 [date 함수 안내서](./dates.md)에서 확인할 수 있습니다.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | 현재 시간을 검색합니다. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 현재 Unix 시간을 검색합니다. |  | timestamp() | timestamp() | 1571850624571 |
| format | 지정된 형식에 따라 입력 날짜를 지정합니다. | <ul><li>날짜:**필수** 형식을 지정할 ZundedDateTime 개체로서 입력 날짜입니다.</li><li>형식:**필수** 날짜를 변경할 형식입니다.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | <ul><li>타임스탬프:**필수** 형식을 지정할 타임스탬프입니다. 밀리초 단위로 기록됩니다.</li><li>형식:**필수** 타임스탬프를 변경할 형식입니다.</li></ul> | 형식&#x200B;(타임스탬프, 형식) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;2019년 10월 23일 11:24&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 객체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜:**필수** 날짜를 나타내는 문자열입니다.</li><li>형식:**필수** 날짜 형식을 나타내는 문자열입니다.</li><li>DEFAULT_DATE:**필수** 제공된 날짜가 null인 경우 반환된 기본 날짜입니다.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 객체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜:**필수** 날짜를 나타내는 문자열입니다.</li><li>형식:**필수** 날짜 형식을 나타내는 문자열입니다.</li></ul> | date(날짜, 형식) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 객체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜:**필수** 날짜를 나타내는 문자열입니다.</li></ul> | date(날짜) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | 날짜의 부분을 검색합니다. 다음 구성 요소 값이 지원됩니다.<br><br>&quot;연도&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;분기&quot;<br>&quot;q&quot;<br>&quot;월&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;&lt;a11&quot; 1/>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;평일&quot;<br>&quot;dw&quot;&lt;20/>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br> &quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot;<br><br><br><br> | <ul><li>구성 요소:**필수** 날짜 부분을 나타내는 문자열입니다. </li><li>날짜:**필수** 날짜(표준 형식)입니다.</li></ul> | date_&#x200B;part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17&quot;) | 10 |
| set_date_part | 지정된 날짜의 구성 요소를 대체합니다. 다음 구성 요소가 허용됩니다.<br><br>&quot;연도&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;월&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;일&quot;<br>&quot;dd&quot;<br><br>&quot;시간&quot;<br>&quot;hh&quot;<br><br> minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br> | <ul><li>구성 요소:**필수** 날짜 부분을 나타내는 문자열입니다. </li><li>값:**필수** 지정된 날짜에 구성 요소에 대해 설정할 값입니다.</li><li>날짜:**필수** 날짜(표준 형식)입니다.</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | 부품으로부터 날짜를 만듭니다. make_timestamp를 사용하여 이 함수를 유도할 수도 있습니다. | <ul><li>연도:**필수** 연도(4자리 숫자)</li><li>월:**필수** 월입니다. 허용되는 값은 1~12입니다.</li><li>일:**필수**&#x200B;일 허용되는 값은 1~31입니다.</li><li>시간:**필수** 시간입니다. 허용되는 값은 0~23입니다.</li><li>분:**필수** 분수입니다. 허용되는 값은 0~59입니다.</li><li>나노초:**필수** 나노초 값입니다. 허용되는 값은 0에서 999999999.</li><li>시간대:**필수** 날짜 시간에 대한 시간대입니다.</li></ul> | make_date_&#x200B;time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, 나노초, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;미국/로스앤젤레스&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | 시간대의 날짜를 UTC의 날짜로 변환합니다. | <ul><li>날짜:**필수** 변환하려는 날짜입니다.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | 한 시간대에서 다른 시간대로 날짜를 변환합니다. | <ul><li>날짜:**필수** 변환하려는 날짜입니다.</li><li>영역:**필수** 날짜를 변환할 시간대입니다.</li></ul> | zone_date_to_zone &#x200B;(날짜, 영역) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### 계층 - 개체 {#objects}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | 입력 크기를 반환합니다. | <ul><li>입력:**필수** 크기를 찾으려는 개체입니다.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | 객체가 비어 있는지 여부를 확인합니다. | <ul><li>입력:**필수** 확인하려는 개체가 비어 있습니다.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | 개체 목록을 만듭니다. | <ul><li>입력:**필수** 키 및 배열 쌍의 그룹입니다.</li></ul> | array_to_object(INPUT) | 샘플 필요 | 샘플 필요 |
| to_object | 주어진 평면 키/값 쌍을 기반으로 객체를 만듭니다. | <ul><li>입력:**필수** 키/값 쌍의 일반 목록입니다.</li></ul> | to_object(INPUT) | to_&#x200B;object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 입력 문자열에서 객체를 만듭니다. | <ul><li>문자열:**필수** 개체를 만들기 위해 파싱되는 문자열입니다.</li><li>VALUE_DELIMITER:*선택적* 값과 필드를 구분하는 구분 기호입니다. 기본 구분 기호는 `:`입니다.</li><li>FIELD_DELIMITER:*선택적* 필드 값 쌍을 구분하는 구분 기호입니다. 기본 구분 기호는 `,`입니다.</li></ul> | str_to_&#x200B;object(문자열, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | 전화 - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | 개체가 소스 데이터 내에 있는지 확인합니다. | <ul><li>입력:**필수** 소스 데이터 내에 있는 경우 확인할 경로입니다.</li></ul> | is_set(INPUT) | is_set(&quot;evars.evar.field1&quot;) | true |
| 무효 | 특성 값을 `null`으로 설정합니다. 이 옵션은 필드를 대상 스키마에 복사하지 않으려는 경우에 사용해야 합니다. |  | untrue() | untrue() | `null` |

{style=&quot;table-layout:auto&quot;}

### 계층 - 배열 {#arrays}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| 코알스 | 지정된 배열에서 null이 아닌 첫 번째 객체를 반환합니다. | <ul><li>입력:**필수** null이 아닌 첫 번째 개체를 찾을 배열입니다.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, 첫 번째, null, &quot;두 번째&quot;) | &quot;first&quot; |
| first | 지정된 배열의 첫 번째 요소를 검색합니다. | <ul><li>입력:**필수** 의 첫 번째 요소를 찾을 배열입니다.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | 지정된 배열의 마지막 요소를 검색합니다. | <ul><li>입력:**필수** 의 마지막 요소를 찾을 배열입니다.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 배열 끝에 요소를 추가합니다. | <ul><li>배열:**필수** 요소를 추가할 배열입니다.</li><li>값:배열에 추가할 요소입니다.</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | add_to_array([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_array | 배열을 서로 결합합니다. | <ul><li>배열:**필수** 요소를 추가할 배열입니다.</li><li>값:상위 배열에 추가할 배열입니다.</li></ul> | join_array&#x200B;(ARRAY, VALUES) | join_arrays([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | 입력 목록을 가져와서 배열로 변환합니다. | <ul><li>INCLUDE_NULL:**필수** 응답 배열에 null을 포함할지 여부를 나타내는 부울 값입니다.</li><li>값:**필수** 배열로 변환할 요소입니다.</li></ul> | to_&#x200B;array(INCLUDE_NULL, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

{style=&quot;table-layout:auto&quot;}

### 논리 연산자 {#logical-operators}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decode | 키와 배열 형태로 분리된 키 값 쌍 목록이 지정된 경우 키가 있으면 값을 반환하고 배열에 있는 경우 기본값을 반환합니다. | <ul><li>키:**필수** 일치할 키입니다.</li><li>OPTIONS:**필수** 키/값 쌍의 분리된 배열입니다. 선택적으로 기본값을 끝에 배치할 수 있습니다.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 지정된 stateCode가 &quot;ca&quot;, &quot;California&quot;인 경우.<br>주어진 stateCode가 &quot;pa&quot;, &quot;Pennsylvania&quot;인 경우<br>stateCode가 다음과 일치하지 않는 경우 &quot;N/A&quot;. |
| iif | 주어진 부울 표현식을 평가하고 결과를 기준으로 지정된 값을 반환합니다. | <ul><li>표현식:**필수** 평가 중인 부울 식입니다.</li><li>TRUE_VALUE:**필수** 표현식이 true로 평가되는 경우 반환되는 값입니다.</li><li>FALSE_VALUE:**필수** 표현식이 false로 평가되는 경우 반환되는 값입니다.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### 집계 {#aggregation}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | 지정된 인수의 최소 개수를 반환합니다. 자연스러운 순서를 사용합니다. | <ul><li>OPTIONS:**필수** 서로 비교할 수 있는 하나 이상의 객체입니다.</li></ul> | min(OPTIONS) | 최소(3, 1, 4) | 1 |
| max | 주어진 인수의 최대값을 반환합니다. 자연스러운 순서를 사용합니다. | <ul><li>OPTIONS:**필수** 서로 비교할 수 있는 하나 이상의 객체입니다.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### 전환 입력 {#type-conversions}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | 문자열을 BigInteger로 변환합니다. | <ul><li>문자열:**필수** BigInteger로 변환할 문자열입니다.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 문자열을 Double로 변환합니다. | <ul><li>문자열:**필수** Double로 변환할 문자열입니다.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 문자열을 Float로 변환합니다. | <ul><li>문자열:**필수** float로 변환할 문자열입니다.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 문자열을 정수로 변환합니다. | <ul><li>문자열:**필수** 정수로 변환할 문자열입니다.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON 함수 {#json}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | 지정된 문자열에서 JSON 콘텐츠를 역직렬화합니다. | <ul><li>문자열:**필수** 역직렬화할 JSON 문자열입니다.</li></ul> | json_to_object&#x200B;(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; :&quot;Doe&quot;}) | JSON을 나타내는 객체입니다. |

{style=&quot;table-layout:auto&quot;}

### 특수 작업 {#special-operations}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | 의사 임의 ID를 생성합니다. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### 사용자 에이전트 함수 {#user-agent}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | 사용자 에이전트 문자열에서 운영 체제 이름을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_&#x200B;name(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 사용자 에이전트 문자열에서 운영 체제의 주 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 사용자 에이전트 문자열에서 운영 체제의 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 사용자 에이전트 문자열에서 운영 체제의 이름과 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 사용자 에이전트 문자열에서 에이전트 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 사용자 에이전트 문자열에서 에이전트 이름 및 주 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 사용자 에이전트 문자열에서 에이전트 이름을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_&#x200B;name(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 사용자 에이전트 문자열에서 장치 클래스를 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, 예: Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 전화 |

{style=&quot;table-layout:auto&quot;}
