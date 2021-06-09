---
keywords: Experience Platform;홈;인기 항목;csv 매핑;csv 파일 매핑;csv 파일을 xdm에 매핑;csv를 xdm에 매핑;ui 안내서;맵;매핑;필드 매핑;매핑 함수;
solution: Experience Platform
title: 데이터 준비 매핑 함수
topic-legacy: overview
description: 이 문서에서는 데이터 준비에 사용되는 매핑 기능을 소개합니다.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 1133580d6d4d8df352ab901d5106f0bb6c1f2a08
workflow-type: tm+mt
source-wordcount: '3935'
ht-degree: 3%

---

# 데이터 준비 매핑 함수

데이터 준비 함수를 사용하여 소스 필드에 입력한 내용에 따라 값을 계산하고 계산할 수 있습니다.

## 필드

필드 이름은 문자, 달러 기호(`$`) 또는 밑줄 문자(`_`)로 시작하는 유니코드 문자 및 자릿수의 무제한 길이 시퀀스일 수 있습니다. 변수 이름은 대소문자를 구분합니다.

필드 이름이 이 규칙을 따르지 않는 경우 필드 이름을 `${}`으로 래핑해야 합니다. 따라서 예를 들어 필드 이름이 &quot;First Name&quot; 또는 &quot;First.Name&quot;인 경우 이름을 각각 `${First Name}` 또는 `${First.Name}`으로 래핑해야 합니다.

또한 필드 이름이 다음 예약된 키워드의 **임의의**&#x200B;인 경우 `${}`로 래핑해야 합니다.

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

점 표기법을 사용하여 하위 필드 내의 데이터에 액세스할 수 있습니다. 예를 들어 `name` 개체가 있는 경우 `firstName` 필드에 액세스하려면 `name.firstName` 를 사용하십시오.

## 함수 목록

다음 표에는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 함수가 나열되어 있습니다.

### 문자열 함수 {#string}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 지정된 문자열을 연결합니다. | <ul><li>문자열:연결할 문자열입니다.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | regex를 기반으로 문자열을 분할하고 부분 배열을 반환합니다. 선택적으로 regex를 포함하여 문자열을 분할할 수 있습니다. 기본적으로 분할은 &quot;,&quot;로 확인됩니다. **다음 구분 기호는 `\`로 이스케이프해야 합니다.`+, ?, ^, |, ., [, (, {, ), *, $, \` 여러 문자를 구분 기호로 포함하는 경우 구분 기호는 다중 문자 구분 기호로 처리됩니다.** | <ul><li>문자열:**필수** 분할해야 하는 문자열입니다.</li><li>REGEX:*선택 사항* 문자열을 분할하는 데 사용할 수 있는 정규 표현식입니다.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| 인스턴스 | 하위 문자열의 위치/인덱스를 반환합니다. | <ul><li>입력:**필수** 검색 중인 문자열입니다.</li><li>하위 문자열:**필수** 문자열 내에서 검색되는 하위 문자열입니다.</li><li>START_POSITION:*선택 사항* 문자열에서 찾기를 시작할 위치입니다.</li><li>발생 횟수:*선택 사항* 시작 위치에서 찾을 n번째 발생 항목입니다. 기본적으로 1입니다. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| 교체 | 원래 문자열에 있는 경우 검색 문자열을 바꿉니다. | <ul><li>입력:**필수** 입력 문자열입니다.</li><li>TO_FIND:**필수** 입력 내에서 찾을 문자열입니다.</li><li>TO_REPLACE:**필수** &quot;TO_FIND&quot; 내에 값을 바꿀 문자열입니다.</li></ul> | replacestor(INPUT, TO_FIND, TO_REPLACE) | replacestor(&quot;문자열 재테스트&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 바꾸기 테스트입니다.&quot; |
| substr | 지정된 길이의 하위 문자열을 반환합니다. | <ul><li>입력:**필수** 입력 문자열입니다.</li><li>START_INDEX:**필수** 하위 문자열이 시작되는 입력 문자열의 색인입니다.</li><li>길이:**필수** 하위 문자열의 길이입니다.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot;subst&quot; |
| lcase /<br>lcase | 문자열을 소문자로 변환. | <ul><li>입력:**필수** 소문자로 변환됩니다.</li></ul> | lower(입력) | lower(&quot;HeO&quot;)<br>lcase(&quot;HeO&quot;) | &quot;hello&quot; |
| upper /<br>ucase | 문자열을 대문자로 변환. | <ul><li>입력:**필수** 대문자로 변환할 문자열입니다.</li></ul> | upper(입력) | upper(&quot;HeO&quot;)<br>ucase(&quot;HeO&quot;) | &quot;HELLO&quot; |
| split | 구분 기호로 입력 문자열을 분할합니다. 다음 구분 기호 **는 `\`로 이스케이프해야 합니다.`\`.** 여러 구분 기호를 포함하는 경우 문자열은 문자열에 있는 구분 기호의 **any**&#x200B;에서 분할됩니다. | <ul><li>입력:**필수** 분할될 입력 문자열입니다.</li><li>구분 기호:**필수** 입력을 분할하는 데 사용되는 문자열입니다.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| 가입 | 구분 기호를 사용하여 개체 목록을 연결합니다. | <ul><li>구분 기호:**필수** 개체를 결합하는 데 사용할 문자열입니다.</li><li>개체:**필수** 조인될 문자열의 배열입니다.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | 문자열의 왼쪽에 지정된 다른 문자열을 패드합니다. | <ul><li>입력:**필수** 패딩할 문자열입니다. 이 문자열은 null일 수 있습니다.</li><li>카운트:**필수** 채울 문자열 크기입니다.</li><li>패딩:**필수** 입력을 패딩하는 문자열입니다. null이거나 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | lpad(입력, 카운트, 패딩) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| rpad | 문자열의 오른쪽을 지정된 다른 문자열로 패드합니다. | <ul><li>입력:**필수** 패딩할 문자열입니다. 이 문자열은 null일 수 있습니다.</li><li>카운트:**필수** 채울 문자열 크기입니다.</li><li>패딩:**필수** 입력을 패딩하는 문자열입니다. null이거나 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | rpad(입력, 카운트, 패딩) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| 왼쪽 | 지정된 문자열의 첫 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열:**필수** 첫 번째 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트:**필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자입니다.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| 오른쪽 | 지정된 문자열의 마지막 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열:**필수** 마지막 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트:**필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자입니다.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | 문자열 시작 부분에서 공백을 제거합니다. | <ul><li>문자열:**필수** 공백을 제거할 문자열입니다.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 문자열 끝에서 공백을 제거합니다. | <ul><li>문자열:**필수** 공백을 제거할 문자열입니다.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | 문자열의 시작과 끝에서 공백을 제거합니다. | <ul><li>문자열:**필수** 공백을 제거할 문자열입니다.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 다음과 같음 | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분합니다. | <ul><li>문자열1:**필수** 비교할 첫 번째 문자열입니다.</li><li>문자열2:**필수** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equals( &#x200B;문자열2) | &quot;string1&quot;&#x200B;을 참조하십시오.equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 **대/소문자를 구분하지 않습니다.** | <ul><li>문자열1:**필수** 비교할 첫 번째 문자열입니다.</li><li>문자열2:**필수** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;&#x200B;을 참조하십시오.equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### 정규 표현식 함수

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 정규 표현식을 기반으로 입력 문자열에서 그룹을 추출합니다. | <ul><li>문자열:**필수** 그룹을 추출하는 문자열입니다.</li><li>REGEX:**필수** 그룹을 일치시킬 정규 표현식입니다.</li></ul> | extract_regex(STRING, REGEX) | extract_regex(&quot;&#x200B;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | 문자열이 입력된 정규 표현식과 일치하는지 확인합니다. | <ul><li>문자열:**필수** 확인 중인 문자열이 정규 표현식과 일치합니다.</li><li>REGEX:**필수** 비교할 정규 표현식입니다.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### 해시 함수 {#hashing}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 입력을 가져오고 SHA-1(보안 해시 알고리즘 1)을 사용하여 해시 값을 생성합니다. | <ul><li>입력:**필수** 일반 텍스트를 해시할 수 있습니다.</li><li>CHARSET:*선택 사항* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha1(입력, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 48690840c5dfcce3c80 |
| sha256 | 입력을 가져오고 보안 해시 알고리즘 256(SHA-256)을 사용하여 해시 값을 생성합니다. | <ul><li>입력:**필수** 일반 텍스트를 해시할 수 있습니다.</li><li>CHARSET:*선택 사항* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha256(입력, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21&#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 입력을 가져오고 보안 해시 알고리즘 512(SHA-512)를 사용하여 해시 값을 생성합니다. | <ul><li>입력:**필수** 일반 텍스트를 해시할 수 있습니다.</li><li>CHARSET:*선택 사항* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha512(입력, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef708bf11b4232bb21d2a8704ada2cdcd7b367dd078a5c908cfe377aceb107a7f7f7a7f8f4f8a4f8f8f8a4f8f7f8a4f8f8f8a4f8a4f8f8f8f8f8a4f8a4f8a4f 68a8fd24d16 |
| md5 | 입력을 가져오고 MD5를 사용하여 해시 값을 생성합니다. | <ul><li>입력:**필수** 일반 텍스트를 해시할 수 있습니다.</li><li>CHARSET:*선택 사항* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다. </li></ul> | md5(입력, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 입력을 받으면 CRC(순환 중복 검사) 알고리즘을 사용하여 32비트 순환 코드를 생성합니다. | <ul><li>입력:**필수** 일반 텍스트를 해시할 수 있습니다.</li><li>CHARSET:*선택 사항* 문자 집합의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | crc32(입력, 문자) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### URL 함수 {#url}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 지정된 URL에서 프로토콜을 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL:**필수** 프로토콜을 추출해야 하는 URL입니다.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | 주어진 URL의 호스트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL:**필수** 호스트를 추출해야 하는 URL입니다.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 지정된 URL의 포트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL:**필수** 포트를 추출해야 하는 URL입니다.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | 지정된 URL의 경로를 반환합니다. 기본적으로 전체 경로가 반환됩니다. | <ul><li>URL:**필수** 경로를 추출해야 하는 URL입니다.</li><li>FULL_PATH:*선택적* 전체 경로가 반환되는지 여부를 결정하는 부울 값입니다. false로 설정하면 경로의 끝만 반환됩니다.</li></ul> | get_url_&#x200B;path(URL, FULL_PATH) | get_url_&#x200B;path(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B; employee.csv&quot; |
| get_url_query_str | 주어진 URL의 쿼리 문자열을 반환합니다. | <ul><li>URL:**필수** 쿼리 문자열을 가져오려는 URL입니다.</li><li>앵커:**필수** 쿼리 문자열에서 앵커에 수행할 작업을 결정합니다. 다음 세 값 중 하나일 수 있습니다.&quot;keep&quot;, &quot;remove&quot; 또는 &quot;append&quot;.<br><br>값이 &quot;keep&quot;이면 앵커가 반환된 값에 연결됩니다.<br>값이 &quot;remove&quot;이면 반환된 값에서 앵커가 제거됩니다.<br>값이 &quot;append&quot;이면 앵커는 별도의 값으로 반환됩니다.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str(&quot;foo://example.com:8042&#x200B;/over/there?name=&quot;name=&quot;&#x200B;ferret#nose&quot;, &quot;retget&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B; over/there?name= &quot;hnose&quot;, remove&quot;))<br>get_url_query_str(&quot;csv0x/vertx/petnet2&quot;)get_url_query_str(&quot;8x0v0pet2:&quot;ferret0ods0pet&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### 날짜 및 시간 함수 {#date-and-time}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오. `date` 함수에 대한 자세한 내용은 [데이터 형식 처리 안내서](./data-handling.md#dates)의 날짜 섹션에서 찾을 수 있습니다.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 현재 시간을 검색합니다. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 현재 Unix 시간을 검색합니다. |  | timestamp() | timestamp() | 1571850624571 |
| 포맷 | 입력 날짜를 지정된 형식에 따라 형식을 지정합니다. | <ul><li>날짜:**필수** 형식을 지정할 ZoneDateTime 개체로서 입력 날짜입니다.</li><li>형식:**필수** 날짜를 변경할 형식입니다.</li></ul> | format(날짜, 형식) | 형식(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | <ul><li>타임스탬프:**필수** 형식을 지정할 타임스탬프입니다. 밀리초 단위로 기록됩니다.</li><li>형식:**필수** 타임스탬프를 변경할 형식입니다.</li></ul> | 형식(&#x200B;타임스탬프, 형식) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | &quot;2019-10-23T11:24:35.000Z&quot; |
| 날짜 | 날짜 문자열을 ZoneDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜:**필수** 날짜를 나타내는 문자열입니다.</li><li>형식:**필수** 날짜 형식을 나타내는 문자열입니다.</li><li>DEFAULT_DATE:**필수** 제공된 날짜가 null인 경우 기본 날짜가 반환됩니다.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| 날짜 | 날짜 문자열을 ZoneDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜:**필수** 날짜를 나타내는 문자열입니다.</li><li>형식:**필수** 날짜 형식을 나타내는 문자열입니다.</li></ul> | date(날짜, 형식) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| 날짜 | 날짜 문자열을 ZoneDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜:**필수** 날짜를 나타내는 문자열입니다.</li></ul> | date(날짜) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | 날짜의 부분을 검색합니다. 지원되는 구성 요소 값은 다음과 같습니다.<br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;q&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br><br>&quot;y&quot;<br><br>&quot;day<br>&quot;dd&quot;<br>&quot;14>&quot; <br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh23/>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi<br>&quot;2초/>&quot;<br>&quot;a8/>&quot; &quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;ms&quot;<br>&quot;ms&quot;<br><br><br> | <ul><li>구성 요소:**필수** 날짜의 부분을 나타내는 문자열입니다. </li><li>날짜:**필수** 표준 형식의 날짜입니다.</li></ul> | date_&#x200B;part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 지정된 날짜에서 구성 요소를 바꿉니다. 다음 구성 요소가 수락됩니다.<br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br><br>&quot;hh&quot;<br>&quot;n&quot;<br><br>&quot;/>&quot;a<br>&quot;/>&quot; 6/>&quot;s&quot;<br><br> | <ul><li>구성 요소:**필수** 날짜의 부분을 나타내는 문자열입니다. </li><li>값:**필수** 지정된 날짜에 대해 구성 요소에 설정할 값입니다.</li><li>날짜:**필수** 표준 형식의 날짜입니다.</li></ul> | set_date_&#x200B;part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | 부품으로부터 날짜를 생성합니다. make_timestamp를 사용하여 이 함수를 유도할 수도 있습니다. | <ul><li>년:**필수** 년, 4자리 숫자</li><li>월:**필수** 월입니다. 허용되는 값은 1~12입니다.</li><li>일:**필수** 날짜입니다. 허용되는 값은 1~31입니다.</li><li>시간:**필수** 시간입니다. 허용되는 값은 0~23입니다.</li><li>분:**필수** 분입니다. 허용되는 값은 0~59입니다.</li><li>나노초:**필수** 나노초 값입니다. 허용되는 값은 0에서 999999999.</li><li>시간대:**필수** 날짜 시간에 대한 시간대입니다.</li></ul> | make_date_&#x200B;time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | 시간대의 날짜를 UTC의 날짜로 변환합니다. | <ul><li>날짜:**필수** 변환하려는 날짜입니다.</li></ul> | zone_date_to_&#x200B;utc(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | 날짜를 하나의 시간대에서 다른 시간대로 변환합니다. | <ul><li>날짜:**필수** 변환하려는 날짜입니다.</li><li>영역:**필수** 날짜를 변환하려는 시간대입니다.</li></ul> | zone_date_to_&#x200B;zone(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### 계층 - 객체 {#objects}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | 입력 크기를 반환합니다. | <ul><li>입력:**필수** 크기를 찾으려는 개체입니다.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | 개체가 비어 있는지 여부를 확인합니다. | <ul><li>입력:**필수** 확인하려는 개체가 비어 있습니다.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | 개체 목록을 만듭니다. | <ul><li>입력:**필수** 키 및 배열 쌍의 그룹입니다.</li></ul> | array_to_object(INPUT) | 샘플 필요 | 샘플 필요 |
| to_object | 제공된 플랫 키/값 쌍을 기반으로 개체를 만듭니다. | <ul><li>입력:**필수** 키/값 쌍의 단순 목록입니다.</li></ul> | to_object(INPUT) | to_&#x200B;object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 입력 문자열에서 개체를 만듭니다. | <ul><li>문자열:**필수** 개체를 만들기 위해 구문 분석되는 문자열입니다.</li><li>VALUE_DELIMITER:*선택 사항* 값과 필드를 구분하는 구분 기호입니다. 기본 구분 기호는 `:`입니다.</li><li>FIELD_DELIMITER:*선택 사항* 필드 값 쌍을 구분하는 구분 기호입니다. 기본 구분 기호는 `,`입니다.</li></ul> | str_to_&#x200B;object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | phone - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | 개체가 소스 데이터 내에 있는지 확인합니다. | <ul><li>입력:**필수** 경로가 소스 데이터 내에 있을 경우 확인할 경로입니다.</li></ul> | is_set(INPUT) | is_&#x200B;set(&quot;evars.evar.field1&quot;) | true |
| 무효 | 속성 값을 `null`(으)로 설정합니다. 대상 스키마에 필드를 복사하지 않으려는 경우 사용해야 합니다. |  | nothing() | nothing() | `null` |
| get_keys | 키/값 쌍을 구문 분석하고 모든 키를 반환합니다. | <ul><li>개체:**필수** 키를 추출할 개체입니다.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;):&quot;오만과 편견&quot;, &quot;책2&quot;&quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | 키/값 쌍을 구문 분석하고 지정된 키를 기반으로 문자열 값을 반환합니다. | <ul><li>문자열:**필수** 구문 분석할 문자열입니다.</li><li>키:**필수** 값을 추출해야 하는 키입니다.</li><li>VALUE_DELIMITER:**필수** 필드와 값을 구분하는 구분 기호입니다. `null` 또는 빈 문자열이 제공되면 이 값은 `:`입니다.</li><li>FIELD_DELIMITER:*선택 사항* 필드 및 값 쌍을 구분하는 구분 기호입니다. `null` 또는 빈 문자열이 제공되면 이 값은 `,`입니다.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | 존 |

{style=&quot;table-layout:auto&quot;}

### 계층 - 배열 {#arrays}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | 지정된 배열에서 null이 아닌 첫 번째 개체를 반환합니다. | <ul><li>입력:**필수** null이 아닌 첫 번째 개체를 찾을 배열입니다.</li></ul> | coalesce(입력) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| 첫 번째 | 지정된 배열의 첫 번째 요소를 검색합니다. | <ul><li>입력:**필수** 첫 번째 요소를 찾을 배열입니다.</li></ul> | first(입력) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 마지막 | 지정된 배열의 마지막 요소를 검색합니다. | <ul><li>입력:**필수** 마지막 요소를 찾을 배열입니다.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 배열 끝에 요소를 추가합니다. | <ul><li>어레이:**필수** 요소를 추가할 배열입니다.</li><li>값:배열에 추가할 요소입니다.</li></ul> | add_to_&#x200B;array(ARRAY, VALUES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | 배열을 서로 결합합니다. | <ul><li>어레이:**필수** 요소를 추가할 배열입니다.</li><li>값:상위 배열에 추가할 배열입니다.</li></ul> | join_&#x200B;arrays(ARRAY, VALUES) | join_arrays([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | 입력 목록을 가져와 배열로 변환합니다. | <ul><li>INCLUDE_NULLS:**필수** 응답 배열에 null을 포함할지 여부를 나타내는 부울 값입니다.</li><li>값:**필수** 배열로 변환할 요소입니다.</li></ul> | to_&#x200B;array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

{style=&quot;table-layout:auto&quot;}

### 논리 연산자 {#logical-operators}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | 키 및 배열로 병합된 키 값 쌍 목록이 주어지면 키가 있으면 값을 반환하거나 배열에 있는 경우 기본값을 반환합니다. | <ul><li>키:**필수** 일치하는 키입니다.</li><li>OPTIONS:**필수** 키/값 쌍의 병합된 배열입니다. 선택적으로, 끝에 기본값을 지정할 수 있습니다.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 제공된 stateCode가 &quot;ca&quot;, &quot;California&quot;인 경우.<br>만약 주코드가 &quot;pa&quot;, &quot;Pennsylvania&quot; 라면.<br>stateCode가 다음과 일치하지 않으면 &quot;N/A&quot;. |
| iif | 지정된 부울 표현식을 평가하고 결과를 기반으로 지정된 값을 반환합니다. | <ul><li>표현식:**필수** 평가되는 부울 식입니다.</li><li>TRUE_VALUE:**필수** 표현식이 true로 평가되는 경우 반환되는 값입니다.</li><li>FALSE_VALUE:**필수** 표현식이 false로 평가되는 경우 반환되는 값입니다.</li></ul> | iif(표현식, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### 집계 {#aggregation}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 지정된 인수의 최소값을 반환합니다. 자연어 순서를 사용합니다. | <ul><li>OPTIONS:**필수** 서로 비교할 수 있는 하나 이상의 개체입니다.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 지정된 인수의 최대 개수를 반환합니다. 자연어 순서를 사용합니다. | <ul><li>OPTIONS:**필수** 서로 비교할 수 있는 하나 이상의 개체입니다.</li></ul> | max(OPTIONS) | 최대(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### 전환 입력 {#type-conversions}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 문자열을 BigInteger로 변환합니다. | <ul><li>문자열:**필수** BigInteger로 변환할 문자열입니다.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 문자열을 Double로 변환. | <ul><li>문자열:**필수** Double로 변환할 문자열입니다.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 문자열을 Float로 변환. | <ul><li>문자열:**필수** Float로 변환할 문자열입니다.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 문자열을 정수로 변환. | <ul><li>문자열:**필수** 정수로 변환할 문자열입니다.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### JSON 함수 {#json}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 지정된 문자열에서 JSON 컨텐츠를 deserialize합니다. | <ul><li>문자열:**필수** 역직렬화할 JSON 문자열입니다.</li></ul> | json_to_&#x200B;object(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; :&quot;Doe&quot;}) | JSON을 나타내는 객체입니다. |

{style=&quot;table-layout:auto&quot;}

### 특수 작업 {#special-operations}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 의사 랜덤 ID를 생성합니다. |  | uuid(<br>guid() | uuid(<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### 사용자 에이전트 함수 {#user-agent}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 사용자 에이전트 문자열에서 운영 체제 이름을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_&#x200B;name(USER_AGENT) | ua_os_&#x200B;name(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 사용자 에이전트 문자열에서 운영 체제의 주요 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 사용자 에이전트 문자열에서 운영 체제의 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_&#x200B;version(USER_AGENT) | ua_os_&#x200B;version(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 사용자 에이전트 문자열에서 운영 체제의 이름과 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name_&#x200B;version(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 사용자 에이전트 문자열에서 에이전트 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_&#x200B;version(USER_AGENT) | ua_agent_&#x200B;version(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 사용자 에이전트 문자열에서 에이전트 이름 및 주 버전을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 사용자 에이전트 문자열에서 에이전트 이름을 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_&#x200B;name(USER_AGENT) | ua_agent_&#x200B;name(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 사용자 에이전트 문자열에서 장치 클래스를 추출합니다. | <ul><li>USER_AGENT:**필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_device_&#x200B;class(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0(iPhone;Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko 등) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 전화 |

{style=&quot;table-layout:auto&quot;}
