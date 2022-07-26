---
keywords: Experience Platform;홈;인기 항목;csv 매핑;csv 파일 매핑;csv 파일을 xdm에 매핑;csv를 xdm에 매핑;ui 안내서;맵;매핑;필드 매핑;매핑 함수;
solution: Experience Platform
title: 데이터 준비 매핑 함수
topic-legacy: overview
description: 이 문서에서는 데이터 준비에 사용되는 매핑 기능을 소개합니다.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 666286970d0cbbcd28f07c34e3f08ec9f4333b0c
workflow-type: tm+mt
source-wordcount: '4298'
ht-degree: 3%

---

# 데이터 준비 매핑 함수

데이터 준비 함수를 사용하여 소스 필드에 입력한 내용에 따라 값을 계산하고 계산할 수 있습니다.

## 필드

필드 이름은 유니코드 문자 및 자릿수의 무제한 길이 시퀀스로 문자, 달러 기호( )로 시작하는 모든 올바른 식별자가 될 수 있습니다`$`) 또는 밑줄 문자(`_`). 변수 이름은 대소문자를 구분합니다.

필드 이름이 이 규칙을 따르지 않는 경우 필드 이름을 `${}`. 따라서 예를 들어 필드 이름이 &quot;First Name&quot; 또는 &quot;First.Name&quot;인 경우 이름을 다음과 같이 래핑해야 합니다 `${First Name}` 또는 `${First.Name}` 각각 사용할 수 있습니다.

또한 필드 이름이 **임의** 다음 예약된 키워드 중에서 `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

점 표기법을 사용하여 하위 필드 내의 데이터에 액세스할 수 있습니다. 예를 들어 `name` 개체, 액세스 `firstName` 필드, `name.firstName`.

## 함수 목록

다음 표에는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 함수가 나열되어 있습니다.

### 문자열 함수 {#string}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 지정된 문자열을 연결합니다. | <ul><li>문자열: 연결할 문자열입니다.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | regex를 기반으로 문자열을 분할하고 부분 배열을 반환합니다. 선택적으로 regex를 포함하여 문자열을 분할할 수 있습니다. 기본적으로 분할은 &quot;,&quot;로 확인됩니다. 다음 구분 기호 **필요** 도망치다 `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` 여러 문자를 구분 기호로 포함하는 경우 구분 기호는 다중 문자 구분 기호로 처리됩니다. | <ul><li>문자열: **필수 여부** 분할해야 하는 문자열입니다.</li><li>REGEX: *선택 사항입니다* 문자열을 분할하는 데 사용할 수 있는 정규 표현식입니다.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| 인스턴스 | 하위 문자열의 위치/인덱스를 반환합니다. | <ul><li>입력: **필수 여부** 검색 중인 문자열입니다.</li><li>하위 문자열: **필수 여부** 문자열 내에서 검색되는 하위 문자열입니다.</li><li>START_POSITION: *선택 사항입니다* 문자열에서 찾기를 시작할 위치.</li><li>발생 횟수: *선택 사항입니다* 시작 위치에서 찾을 n번째 발생. 기본적으로 1입니다. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| 교체 | 원래 문자열에 있는 경우 검색 문자열을 바꿉니다. | <ul><li>입력: **필수 여부** 입력 문자열입니다.</li><li>TO_FIND: **필수 여부** 입력 내에서 찾을 문자열입니다.</li><li>TO_REPLACE: **필수 여부** &quot;TO_FIND&quot; 내의 값을 대체할 문자열입니다.</li></ul> | replacestor(INPUT, TO_FIND, TO_REPLACE) | replacestor(&quot;문자열 재테스트&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 바꾸기 테스트입니다.&quot; |
| substr | 지정된 길이의 하위 문자열을 반환합니다. | <ul><li>입력: **필수 여부** 입력 문자열입니다.</li><li>START_INDEX: **필수 여부** 하위 문자열이 시작되는 입력 문자열의 색인입니다.</li><li>길이: **필수 여부** 하위 문자열의 길이입니다.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot;subst&quot; |
| lower/lower<br>lcase | 문자열을 소문자로 변환. | <ul><li>입력: **필수 여부** 소문자로 변환됩니다.</li></ul> | lower(입력) | lower(&quot;HeO&quot;)<br>lcase(&quot;HeO&quot;) | &quot;hello&quot; |
| upper /<br>구루아제 | 문자열을 대문자로 변환. | <ul><li>입력: **필수 여부** 대문자로 변환할 문자열입니다.</li></ul> | upper(입력) | upper(&quot;HeO&quot;)<br>ucase(&quot;HeO&quot;) | &quot;HELLO&quot; |
| split | 구분 기호로 입력 문자열을 분할합니다. 다음 구분 기호 **요구 사항** 도망치다 `\`: `\`. 여러 구분 기호를 포함하는 경우 문자열이 다음 순서로 분할됩니다 **임의** 문자열에 있는 구분 기호로 묶습니다. | <ul><li>입력: **필수 여부** 분할할 입력 문자열입니다.</li><li>구분 기호: **필수 여부** 입력을 분할하는 데 사용되는 문자열입니다.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 가입 | 구분 기호를 사용하여 개체 목록을 연결합니다. | <ul><li>구분 기호: **필수 여부** 개체를 조인하는 데 사용할 문자열입니다.</li><li>개체: **필수 여부** 조인할 문자열의 배열입니다.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | 문자열의 왼쪽에 지정된 다른 문자열을 패드합니다. | <ul><li>입력: **필수 여부** 그 끈은 패딩될 것이다. 이 문자열은 null일 수 있습니다.</li><li>카운트: **필수 여부** 패딩할 문자열 크기입니다.</li><li>패딩: **필수 여부** 입력을 패딩하는 문자열입니다. null이거나 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | lpad(입력, 카운트, 패딩) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | 문자열의 오른쪽을 지정된 다른 문자열로 패드합니다. | <ul><li>입력: **필수 여부** 그 끈은 패딩될 것이다. 이 문자열은 null일 수 있습니다.</li><li>카운트: **필수 여부** 패딩할 문자열 크기입니다.</li><li>패딩: **필수 여부** 입력을 패딩하는 문자열입니다. null이거나 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | rpad(입력, 카운트, 패딩) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| 왼쪽 | 지정된 문자열의 첫 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열: **필수 여부** 에 대한 첫 번째 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트: **필수 여부**&#x200B;문자열에서 가져올 &quot;n&quot; 문자.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| 오른쪽 | 지정된 문자열의 마지막 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열: **필수 여부** 에 대한 마지막 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트: **필수 여부**&#x200B;문자열에서 가져올 &quot;n&quot; 문자.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | 문자열 시작 부분에서 공백을 제거합니다. | <ul><li>문자열: **필수 여부** 공백을 제거할 문자열입니다.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 문자열 끝에서 공백을 제거합니다. | <ul><li>문자열: **필수 여부** 공백을 제거할 문자열입니다.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | 문자열의 시작과 끝에서 공백을 제거합니다. | <ul><li>문자열: **필수 여부** 공백을 제거할 문자열입니다.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 다음과 같음 | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분합니다. | <ul><li>문자열1: **필수 여부** 비교할 첫 번째 문자열입니다.</li><li>문자열2: **필수 여부** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equals( &#x200B;문자열2) | &quot;string1&quot;&#x200B;을 참조하십시오.equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 **not** 대/소문자를 구분합니다. | <ul><li>문자열1: **필수 여부** 비교할 첫 번째 문자열입니다.</li><li>문자열2: **필수 여부** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;&#x200B;을 참조하십시오.equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### 정규 표현식 함수

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 정규 표현식을 기반으로 입력 문자열에서 그룹을 추출합니다. | <ul><li>문자열: **필수 여부** 그룹을 추출하는 문자열입니다.</li><li>REGEX: **필수 여부** 그룹을 일치시킬 정규 표현식입니다.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;()[^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | 문자열이 입력된 정규 표현식과 일치하는지 확인합니다. | <ul><li>문자열: **필수 여부** 확인하는 문자열이 정규 표현식과 일치합니다.</li><li>REGEX: **필수 여부** 비교하려는 정규 표현식입니다.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### 해시 함수 {#hashing}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 입력을 가져오고 SHA-1(보안 해시 알고리즘 1)을 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수 여부** 해시할 일반 텍스트입니다.</li><li>CHARSET: *선택 사항입니다* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha1(입력, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 48690840c5dfcce3c80 |
| sha256 | 입력을 가져오고 보안 해시 알고리즘 256(SHA-256)을 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수 여부** 해시할 일반 텍스트입니다.</li><li>CHARSET: *선택 사항입니다* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha256(입력, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21&#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 입력을 가져오고 보안 해시 알고리즘 512(SHA-512)를 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수 여부** 해시할 일반 텍스트입니다.</li><li>CHARSET: *선택 사항입니다* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha512(입력, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef708bf11b4232bb21d2a8704ada2cdcd7b367dd078a5c908cfe377aceb107a7f7f7a7f8f4f8a4f8f8f8a4f8f8f8a4f8f8f8a4f8a4f8f 68a8fd24d16 |
| md5 | 입력을 가져오고 MD5를 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수 여부** 해시할 일반 텍스트입니다.</li><li>CHARSET: *선택 사항입니다* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다. </li></ul> | md5(입력, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 입력을 받으면 CRC(순환 중복 검사) 알고리즘을 사용하여 32비트 순환 코드를 생성합니다. | <ul><li>입력: **필수 여부** 해시할 일반 텍스트입니다.</li><li>CHARSET: *선택 사항입니다* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | crc32(입력, 문자) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL 함수 {#url}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 지정된 URL에서 프로토콜을 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL: **필수 여부** 프로토콜을 추출해야 하는 URL입니다.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 주어진 URL의 호스트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL: **필수 여부** 호스트를 추출해야 하는 URL입니다.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 지정된 URL의 포트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL: **필수 여부** 포트를 추출해야 하는 URL입니다.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 지정된 URL의 경로를 반환합니다. 기본적으로 전체 경로가 반환됩니다. | <ul><li>URL: **필수 여부** 경로를 추출해야 하는 URL입니다.</li><li>FULL_PATH: *선택 사항입니다* 전체 경로가 반환되는지 여부를 결정하는 부울 값입니다. false로 설정하면 경로의 끝만 반환됩니다.</li></ul> | get_url_&#x200B;path(URL, FULL_PATH) | get_url_&#x200B;path(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | 쿼리 문자열 이름 및 쿼리 문자열 값의 맵으로 주어진 URL의 쿼리 문자열을 반환합니다. | <ul><li>URL: **필수 여부** 쿼리 문자열을 가져오려는 URL입니다.</li><li>앵커: **필수 여부** 쿼리 문자열의 앵커로 수행할 작업을 결정합니다. 다음 세 값 중 하나일 수 있습니다. &quot;keep&quot;, &quot;remove&quot; 또는 &quot;append&quot;.<br><br>값이 &quot;keep&quot;이면 앵커가 반환된 값에 연결됩니다.<br>값이 &quot;remove&quot;이면 반환된 값에서 앵커가 제거됩니다.<br>값이 &quot;append&quot;이면 앵커는 별도의 값으로 반환됩니다.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nos&quot;, &quot;retain&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com&#x200B;:8042/over/there?name=ferret#nos&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### 날짜 및 시간 함수 {#date-and-time}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오. 에 대한 추가 정보 `date` 함수는 [데이터 형식 처리 안내서](./data-handling.md#dates).

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 현재 시간을 검색합니다. |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | 현재 Unix 시간을 검색합니다. |  | timestamp() | timestamp() | 1571850624571 |
| 포맷 | 입력 날짜를 지정된 형식에 따라 형식을 지정합니다. | <ul><li>날짜: **필수 여부** 형식을 지정할 입력 날짜(ZoneDateTime 개체)입니다.</li><li>형식: **필수 여부** 날짜를 변경할 형식입니다.</li></ul> | format(날짜, 형식) | 형식(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | <ul><li>타임스탬프: **필수 여부** 포맷할 타임스탬프입니다. 밀리초 단위로 기록됩니다.</li><li>형식: **필수 여부** 타임스탬프를 만들려는 형식입니다.</li></ul> | DFORMAT(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| 날짜 | 날짜 문자열을 ZoneDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜: **필수 여부** 날짜를 나타내는 문자열입니다.</li><li>형식: **필수 여부** 소스 날짜 형식을 나타내는 문자열입니다.**참고:** 이 기능은 **not** 날짜 문자열을 변환하려는 형식을 나타냅니다. </li><li>DEFAULT_DATE: **필수 여부** 제공된 날짜가 null인 경우 기본 날짜가 반환됩니다.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| 날짜 | 날짜 문자열을 ZoneDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜: **필수 여부** 날짜를 나타내는 문자열입니다.</li><li>형식: **필수 여부** 소스 날짜 형식을 나타내는 문자열입니다.**참고:** 이 기능은 **not** 날짜 문자열을 변환하려는 형식을 나타냅니다. </li></ul> | date(날짜, 형식) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| 날짜 | 날짜 문자열을 ZoneDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜: **필수 여부** 날짜를 나타내는 문자열입니다.</li></ul> | date(날짜) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | 날짜의 부분을 검색합니다. 지원되는 구성 요소 값은 다음과 같습니다. <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;ms&quot;<br>&quot;ms&quot; | <ul><li>구성 요소: **필수 여부** 날짜의 부분을 나타내는 문자열입니다. </li><li>날짜: **필수 여부** 표준 형식으로 된 날짜입니다.</li></ul> | date_&#x200B;part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11&quot;:55:12형) | 10 |
| set_date_part | 지정된 날짜에서 구성 요소를 바꿉니다. 다음 구성 요소가 수락됩니다. <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>구성 요소: **필수 여부** 날짜의 부분을 나타내는 문자열입니다. </li><li>값: **필수 여부** 지정된 날짜에 대한 구성 요소에 대해 설정할 값입니다.</li><li>날짜: **필수 여부** 표준 형식으로 된 날짜입니다.</li></ul> | set_date_&#x200B;part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797형) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | 부품으로부터 날짜를 생성합니다. make_timestamp를 사용하여 이 함수를 유도할 수도 있습니다. | <ul><li>년: **필수 여부** 그 해는 네 자리 숫자로 기록되었다.</li><li>월: **필수 여부** 그 달. 허용되는 값은 1~12입니다.</li><li>일: **필수 여부** 오늘 허용되는 값은 1~31입니다.</li><li>시간: **필수 여부** 시간 허용되는 값은 0~23입니다.</li><li>분: **필수 여부** 분 허용되는 값은 0~59입니다.</li><li>나노초: **필수 여부** 나노 초 값입니다. 허용되는 값은 0에서 999999999.</li><li>시간대: **필수 여부** 날짜 시간 시간대.</li></ul> | make_date_&#x200B;time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 시간대의 날짜를 UTC의 날짜로 변환합니다. | <ul><li>날짜: **필수 여부** 변환하려는 날짜입니다.</li></ul> | zone_date_to_&#x200B;utc(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 날짜를 하나의 시간대에서 다른 시간대로 변환합니다. | <ul><li>날짜: **필수 여부** 변환하려는 날짜입니다.</li><li>영역: **필수 여부** 날짜를 변환하려는 시간대</li></ul> | zone_date_to_&#x200B;zone(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### 계층 - 객체 {#objects}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 개체가 비어 있는지 여부를 확인합니다. | <ul><li>입력: **필수 여부** 확인하려는 개체가 비어 있습니다.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | 개체 목록을 만듭니다. | <ul><li>입력: **필수 여부** 키 및 배열 쌍의 그룹입니다.</li></ul> | array_to_object(INPUT) | 샘플 필요 | 샘플 필요 |
| to_object | 제공된 플랫 키/값 쌍을 기반으로 개체를 만듭니다. | <ul><li>입력: **필수 여부** 키/값 쌍의 플랫 목록입니다.</li></ul> | to_object(INPUT) | to_&#x200B;object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 입력 문자열에서 개체를 만듭니다. | <ul><li>문자열: **필수 여부** 개체를 만들기 위해 구문 분석되는 문자열입니다.</li><li>VALUE_DELIMITER: *선택 사항입니다* 값과 필드를 구분하는 구분 기호입니다. 기본 구분 기호는 다음과 같습니다 `:`.</li><li>FIELD_DELIMITER: *선택 사항입니다* 필드 값 쌍을 구분하는 구분 기호입니다. 기본 구분 기호는 다음과 같습니다 `,`.</li></ul> | str_to_&#x200B;object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName=John,lastName=Doe,phone=123 456 7890&quot;, &quot;=&quot;, &quot;,&quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| contains_key | 개체가 소스 데이터 내에 있는지 확인합니다. **참고:** 이 함수는 사용되지 않는 `is_set()` 함수 위에 있어야 합니다. | <ul><li>입력: **필수 여부** 소스 데이터 내에 있는 경우 확인할 경로입니다.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| 무효 | 속성 값을 로 설정합니다. `null`. 대상 스키마에 필드를 복사하지 않으려는 경우 사용해야 합니다. |  | nothing() | nothing() | `null` |
| get_keys | 키/값 쌍을 구문 분석하고 모든 키를 반환합니다. | <ul><li>개체: **필수 여부** 키를 추출할 객체입니다.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;): &quot;오만과 편견&quot;, &quot;책2&quot; &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | 키/값 쌍을 구문 분석하고 지정된 키를 기반으로 문자열 값을 반환합니다. | <ul><li>문자열: **필수 여부** 구문 분석할 문자열입니다.</li><li>키: **필수 여부** 값을 추출해야 하는 키입니다.</li><li>VALUE_DELIMITER: **필수 여부** 필드와 값을 구분하는 구분 기호입니다. 다음의 경우 `null` 또는 빈 문자열이 제공되면 이 값은 `:`.</li><li>FIELD_DELIMITER: *선택 사항입니다* 필드 및 값 쌍을 구분하는 구분 기호입니다. 다음의 경우 `null` 또는 빈 문자열이 제공되면 이 값은 `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | 존 |

{style=&quot;table-layout:auto&quot;}

객체 복사 기능에 대한 자세한 내용은 섹션을 참조하십시오 [아래](#object-copy).

### 계층 - 배열 {#arrays}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | 지정된 배열에서 null이 아닌 첫 번째 개체를 반환합니다. | <ul><li>입력: **필수 여부** null이 아닌 첫 번째 개체를 찾을 배열입니다.</li></ul> | coalesce(입력) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| 첫 번째 | 지정된 배열의 첫 번째 요소를 검색합니다. | <ul><li>입력: **필수 여부** 의 첫 번째 요소를 찾을 배열입니다.</li></ul> | first(입력) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 마지막 | 지정된 배열의 마지막 요소를 검색합니다. | <ul><li>입력: **필수 여부** 의 마지막 요소를 찾을 배열입니다.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 배열 끝에 요소를 추가합니다. | <ul><li>어레이: **필수 여부** 요소를 추가할 배열입니다.</li><li>값: 배열에 추가할 요소입니다.</li></ul> | add_to_&#x200B;array(ARRAY, VALUES) | add_to_&#x200B; array([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | 배열을 서로 결합합니다. | <ul><li>어레이: **필수 여부** 요소를 추가할 배열입니다.</li><li>값: 상위 배열에 추가할 배열입니다.</li></ul> | join_&#x200B;arrays(ARRAY, VALUES) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | 입력 목록을 가져와 배열로 변환합니다. | <ul><li>INCLUDE_NULLS: **필수 여부** 응답 배열에 null을 포함할지 여부를 나타내는 부울 값입니다.</li><li>값: **필수 여부** 배열로 변환할 요소입니다.</li></ul> | to_&#x200B;array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | 입력 크기를 반환합니다. | <ul><li>입력: **필수 여부** 크기를 찾으려는 개체입니다.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 이 함수는 전체 입력 배열의 모든 요소를 프로필의 배열 끝에 추가하는 데 사용됩니다. 이 함수는 **전용** 업데이트 중에 적용할 수 있습니다. 삽입 문맥에서 사용하는 경우 이 함수는 입력을 그대로 반환합니다. | <ul><li>어레이: **필수 여부** 프로필에 배열을 추가할 배열입니다.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123,456] |
| upsert_array_replace | 이 함수는 배열의 요소를 바꾸는 데 사용됩니다. 이 함수는 **전용** 업데이트 중에 적용할 수 있습니다. 삽입 문맥에서 사용하는 경우 이 함수는 입력을 그대로 반환합니다. | <ul><li>어레이: **필수 여부** 프로필에서 배열을 바꿀 배열입니다.</li><li>인덱스: **선택 사항입니다** 교체해야 하는 지점입니다.</li></li> | upsert_array_replace(ARRAY, INDEX) | `upsert_array_replace([123, 456], 1)` | [123,456] |

{style=&quot;table-layout:auto&quot;}


### 논리 연산자 {#logical-operators}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | 키 및 배열로 병합된 키 값 쌍 목록이 주어지면 키가 있으면 값을 반환하거나 배열에 있는 경우 기본값을 반환합니다. | <ul><li>키: **필수 여부** 일치하는 키입니다.</li><li>OPTIONS: **필수 여부** 키/값 쌍의 병합된 배열입니다. 선택적으로, 끝에 기본값을 지정할 수 있습니다.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 제공된 stateCode가 &quot;ca&quot;, &quot;California&quot;인 경우.<br>만약 주코드가 &quot;pa&quot;, &quot;Pennsylvania&quot; 라면.<br>stateCode가 다음과 일치하지 않으면 &quot;N/A&quot;. |
| iif | 지정된 부울 표현식을 평가하고 결과를 기반으로 지정된 값을 반환합니다. | <ul><li>표현식: **필수 여부** 평가 중인 부울 식입니다.</li><li>TRUE_VALUE: **필수 여부** 표현식이 true로 평가되는 경우 반환되는 값입니다.</li><li>FALSE_VALUE: **필수 여부** 표현식이 false로 평가되는 경우 반환되는 값입니다.</li></ul> | iif(표현식, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### 집계 {#aggregation}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 지정된 인수의 최소값을 반환합니다. 자연어 순서를 사용합니다. | <ul><li>OPTIONS: **필수 여부** 서로 비교할 수 있는 하나 이상의 개체입니다.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 지정된 인수의 최대 개수를 반환합니다. 자연어 순서를 사용합니다. | <ul><li>OPTIONS: **필수 여부** 서로 비교할 수 있는 하나 이상의 개체입니다.</li></ul> | max(OPTIONS) | 최대(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### 유형 전환 {#type-conversions}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 문자열을 BigInteger로 변환합니다. | <ul><li>문자열: **필수 여부** BigInteger로 변환할 문자열입니다.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 문자열을 Double로 변환. | <ul><li>문자열: **필수 여부** Double로 변환할 문자열입니다.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 문자열을 Float로 변환. | <ul><li>문자열: **필수 여부** Float로 변환할 문자열입니다.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 문자열을 정수로 변환. | <ul><li>문자열: **필수 여부** 정수로 변환할 문자열입니다.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON 함수 {#json}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 지정된 문자열에서 JSON 컨텐츠를 deserialize합니다. | <ul><li>문자열: **필수 여부** deserialize할 JSON 문자열입니다.</li></ul> | json_to_&#x200B;object(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | JSON을 나타내는 객체입니다. |

{style=&quot;table-layout:auto&quot;}

### 특별 작업 {#special-operations}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 의사 랜덤 ID를 생성합니다. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### 사용자 에이전트 함수 {#user-agent}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 사용자 에이전트 문자열에서 운영 체제 이름을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_&#x200B;name(USER_AGENT) | ua_os_&#x200B;name(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 사용자 에이전트 문자열에서 운영 체제의 주요 버전을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0&quot;(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 사용자 에이전트 문자열에서 운영 체제의 버전을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_&#x200B;version(USER_AGENT) | ua_os_&#x200B;version(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 사용자 에이전트 문자열에서 운영 체제의 이름과 버전을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name_&#x200B;version(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 사용자 에이전트 문자열에서 에이전트 버전을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_&#x200B;version(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 사용자 에이전트 문자열에서 에이전트 이름 및 주 버전을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 사용자 에이전트 문자열에서 에이전트 이름을 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_&#x200B;name(USER_AGENT) | ua_agent_&#x200B;name(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 사용자 에이전트 문자열에서 장치 클래스를 추출합니다. | <ul><li>USER_AGENT: **필수 여부** 사용자 에이전트 문자열입니다.</li></ul> | ua_device_&#x200B;class(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0(iPhone; Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(Gecko와 같은 KHTML) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 전화 |

{style=&quot;table-layout:auto&quot;}

### 개체 복사 {#object-copy}

>[!TIP]
>
>소스 객체가 XDM의 객체에 매핑되면 객체 복사 기능이 자동으로 적용됩니다. 사용자로부터 추가 작업이 필요하지 않습니다.

객체 복사 기능을 사용하여 매핑을 변경하지 않고 객체의 속성을 자동으로 복사할 수 있습니다. 예를 들어 소스 데이터의 구조가 다음과 같은 경우

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

및 의 XDM 구조:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

그러면 매핑이 다음과 같이 됩니다.

```json
address -> addr
address.line1 -> addr.addrLine1
```

위의 예에서 `city` 및 `state` 속성은 런타임에 자동으로 수집되므로 `address` 개체가 `addr`. 다음을 만들 경우 `line2` xdm 구조의 속성과 입력 데이터에는 `line2` 에서 `address` 수동으로 매핑을 변경할 필요 없이 개체를 자동으로 수집할 수도 있습니다.

자동 매핑이 작동하려면 다음 전제 조건을 충족해야 합니다.

* 부모 수준 개체를 매핑해야 합니다.
* XDM 스키마에서 새 속성을 만들어야 합니다.
* 새 속성에는 소스 스키마와 XDM 스키마에 일치하는 이름이 있어야 합니다.

사전 요구 사항이 충족되지 않으면 데이터 준비를 사용하여 소스 스키마를 XDM 스키마에 수동으로 매핑해야 합니다.