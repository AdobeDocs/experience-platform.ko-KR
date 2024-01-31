---
keywords: Experience Platform;홈;인기 항목;csv 매핑;csv 파일 매핑;xdm에 csv 파일 매핑;xdm에 csv 매핑;ui 안내서;매퍼;매핑;필드 매핑;필드 매핑;
solution: Experience Platform
title: 데이터 준비 매핑 기능
description: 이 문서에서는 데이터 준비에 사용되는 매핑 기능을 소개합니다.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: f250d8e6e5368a785dcb154dbe0b611baed73a4c
workflow-type: tm+mt
source-wordcount: '5459'
ht-degree: 2%

---

# 데이터 준비 매핑 함수

데이터 준비 함수를 사용하여 소스 필드에 입력된 내용을 기반으로 값을 계산하고 계산할 수 있습니다.

## 필드

필드 이름은 임의의 법적 식별자(문자로 시작하는 유니코드 문자와 숫자의 무제한 시퀀스)가 될 수 있습니다( 달러 기호)`$`) 또는 밑줄 문자(`_`). 변수 이름도 대소문자를 구분합니다.

필드 이름이 이 규칙을 따르지 않는 경우 필드 이름은 로 래핑해야 합니다 `${}`. 따라서 예를 들어 필드 이름이 &quot;First Name&quot; 또는 &quot;First.Name&quot;이면 이름은 다음과 같이 래핑되어야 합니다 `${First Name}` 또는 `${First\.Name}` 각각.

>[!TIP]
>
>계층과 상호 작용할 때 하위 속성에 점(`.`), 백슬래시( )를 사용해야 합니다`\`)를 클릭하여 특수 문자를 이스케이프 처리합니다. 자세한 내용은 의 안내서를 참조하십시오. [특수 문자 이스케이프 처리](home.md#escape-special-characters).

또한 필드 이름이 인 경우 **임의** 다음 예약 키워드 중 하나를 래핑해야 합니다. `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

하위 필드 내의 데이터는 점 표기법을 사용하여 액세스할 수 있습니다. 예를 들어 `name` 개체, 액세스 `firstName` 필드, 사용 `name.firstName`.

## 함수 목록

다음 표에는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 함수가 나열되어 있습니다.

### 문자열 함수 {#string}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 지정된 문자열을 연결합니다. | <ul><li>STRING: 연결할 문자열입니다.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;안녕하세요, &quot;, &quot;저기&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | 정규 표현식을 기준으로 문자열을 분할하고 부분 배열을 반환합니다. 문자열을 분할하도록 regex를 선택적으로 포함할 수 있습니다. 기본적으로 분할은 &quot;,&quot;로 확인됩니다. 다음 구분 기호 **필요** 함께 이스케이프 처리됨 `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` 여러 문자를 구분 기호로 포함하면 구분 기호는 여러 문자 구분 기호로 처리됩니다. | <ul><li>문자열: **필수** 분할해야 하는 문자열입니다.</li><li>정규 표현식: *선택 사항* 문자열을 분할하는 데 사용할 수 있는 정규 표현식.</li></ul> | explode(문자열, 정규 표현식) | explode(&quot;안녕하세요!&quot;, &quot;) | `["Hi,", "there"]` |
| instr | 하위 문자열의 위치/인덱스를 반환합니다. | <ul><li>입력: **필수** 검색 중인 문자열입니다.</li><li>하위 문자열: **필수** 문자열 내에서 검색 중인 하위 문자열.</li><li>시작 위치: *선택 사항* 문자열에서 찾기 시작할 위치입니다.</li><li>발생 횟수: *선택 사항* 시작 위치에서 찾을 n번째 발생 횟수입니다. 기본적으로 1입니다. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| replacestr | 원래 문자열에 있는 경우 검색 문자열을 대체합니다. | <ul><li>입력: **필수** 입력 문자열입니다.</li><li>찾기(_F): **필수** 입력 내에서 조회할 문자열입니다.</li><li>바꾸기(_R): **필수** &quot;TO_FIND&quot; 내의 값을 대체할 문자열입니다.</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacetr(&quot;문자열 re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 바꾸기 테스트입니다.&quot; |
| substr | 주어진 길이의 하위 문자열을 반환합니다. | <ul><li>입력: **필수** 입력 문자열입니다.</li><li>시작 색인: **필수** 하위 문자열이 시작되는 입력 문자열의 인덱스입니다.</li><li>길이: **필수** 하위 문자열의 길이입니다.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;하위 문자열 테스트임&quot;, 7, 8) | &quot; a 하위&quot; |
| 하한 /<br>케이스 | 문자열을 소문자로 변환합니다. | <ul><li>입력: **필수** 소문자로 변환되는 문자열입니다.</li></ul> | lower(입력) | lower(&quot;HeLlO&quot;)<br>lcase(&quot;HeLlO&quot;) | &quot;hello&quot; |
| upper /<br>우카세 | 문자열을 대문자로 변환합니다. | <ul><li>입력: **필수** 대문자로 변환되는 문자열입니다.</li></ul> | upper(입력) | upper(&quot;HeLlO&quot;)<br>ucase(&quot;HeLlO&quot;) | &quot;HELLO&quot; |
| split | 구분 기호에서 입력 문자열을 분할합니다. 다음 구분 기호 **필요** 함께 이스케이프 처리됨 `\`: `\`. 여러 구분 기호를 포함하는 경우 문자열이 다음으로 분할됩니다. **임의** 문자열에 있는 구분 기호입니다. **참고:** 이 함수는 구분 기호의 존재 여부에 관계없이 문자열에서 null이 아닌 인덱스만 반환합니다. 결과 배열에 null을 포함한 모든 인덱스가 필요한 경우에는 &quot;explode&quot; 함수를 대신 사용하십시오. | <ul><li>입력: **필수** 분할할 입력 문자열입니다.</li><li>분리자: **필수** 입력을 분할하는 데 사용되는 문자열입니다.</li></ul> | split(입력, 구분 기호) | split(&quot;Hello world&quot;, &quot;) | `["Hello", "world"]` |
| 가입 | 구분 기호를 사용하여 개체 목록을 조인합니다. | <ul><li>분리자: **필수** 개체를 연결하는 데 사용할 문자열입니다.</li><li>개체: **필수** 조인할 문자열 배열입니다.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | 문자열의 왼쪽을 지정된 다른 문자열과 연결합니다. | <ul><li>입력: **필수** 채워질 끈. 이 문자열은 null일 수 있습니다.</li><li>카운트: **필수** 패딩할 문자열의 크기입니다.</li><li>패딩: **필수** 입력을 연결하는 문자열입니다. null이거나 비어 있으면, 단일 공백으로 처리됩니다.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzybat&quot; |
| rpad | 문자열의 오른쪽을 지정된 다른 문자열과 연결합니다. | <ul><li>입력: **필수** 채워질 끈. 이 문자열은 null일 수 있습니다.</li><li>카운트: **필수** 패딩할 문자열의 크기입니다.</li><li>패딩: **필수** 입력을 연결하는 문자열입니다. null이거나 비어 있으면, 단일 공백으로 처리됩니다.</li></ul> | rpad(입력, 카운트, 패딩) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | 지정된 문자열의 첫 번째 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열: **필수** 첫 번째 &quot;n&quot; 문자를 받는 문자열입니다.</li><li>카운트: **필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| 오른쪽 | 지정된 문자열의 마지막 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열: **필수** 에 대한 마지막 &quot;n&quot;자를 가져오는 문자열입니다.</li><li>카운트: **필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | 문자열의 시작에서 공백을 제거합니다. | <ul><li>문자열: **필수** 공백을 제거할 문자열입니다.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | 문자열 끝에서 공백을 제거합니다. | <ul><li>문자열: **필수** 공백을 제거할 문자열입니다.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | 문자열의 시작과 끝에서 공백을 제거합니다. | <ul><li>문자열: **필수** 공백을 제거할 문자열입니다.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 다음과 같음 | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분합니다. | <ul><li>STRING1: **필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2: **필수** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equals(&#x200B;STRING2) | &quot;string1&quot;. &#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 **아님** 대/소문자를 구분합니다. | <ul><li>STRING1: **필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2: **필수** 비교할 두 번째 문자열입니다.</li></ul> | 문자열1&#x200B;.equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### 정규 표현식 함수

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | 정규 표현식을 기반으로 입력 문자열에서 그룹을 추출합니다. | <ul><li>문자열: **필수** 그룹을 추출하는 문자열입니다.</li><li>정규 표현식: **필수** 그룹을 일치시킬 정규 표현식입니다.</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot;&#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | 문자열이 입력한 정규 표현식과 일치하는지 확인합니다. | <ul><li>문자열: **필수** 확인 중인 문자열은 정규 표현식과 일치합니다.</li><li>정규 표현식: **필수** 비교 중인 정규 표현식입니다.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style="table-layout:auto"}

### 해시 함수 {#hashing}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | 입력을 가져오고 SHA-1(Secure Hash Algorithm 1)을 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수** 해시할 일반 텍스트입니다.</li><li>문자 집합: *선택 사항* 문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | 입력을 가져오고 보안 해시 알고리즘 256(SHA-256)을 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수** 해시할 일반 텍스트입니다.</li><li>문자 집합: *선택 사항* 문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | 입력을 가져오고 보안 해시 알고리즘 512(SHA-512)를 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수** 해시할 일반 텍스트입니다.</li><li>문자 집합: *선택 사항* 문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | 입력을 가져오고 MD5를 사용하여 해시 값을 생성합니다. | <ul><li>입력: **필수** 해시할 일반 텍스트입니다.</li><li>문자 집합: *선택 사항* 문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다. </li></ul> | md5(입력, 문자 집합) | md5(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | 입력이 CRC(순환 중복 검사) 알고리즘을 사용하여 32비트 순환 코드를 생성합니다. | <ul><li>입력: **필수** 해시할 일반 텍스트입니다.</li><li>문자 집합: *선택 사항* 문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | crc32(입력, CHARSET) | crc32(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### URL 함수 {#url}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 지정된 URL에서 프로토콜을 반환합니다. 입력이 올바르지 않으면 null을 반환합니다. | <ul><li>URL: **필수** 프로토콜을 추출해야 하는 URL입니다.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | 지정된 URL의 호스트를 반환합니다. 입력이 올바르지 않으면 null을 반환합니다. | <ul><li>URL: **필수** 호스트를 추출해야 하는 URL입니다.</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 지정된 URL의 포트를 반환합니다. 입력이 올바르지 않으면 null을 반환합니다. | <ul><li>URL: **필수** 포트를 추출해야 하는 URL입니다.</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | 지정된 URL의 경로를 반환합니다. 기본적으로 전체 경로가 반환됩니다. | <ul><li>URL: **필수** 경로를 추출해야 하는 URL입니다.</li><li>전체 경로: *선택 사항* 전체 경로가 반환되는지 여부를 결정하는 부울 값입니다. false로 설정하면 경로의 끝만 반환됩니다.</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B;employee.csv&quot; |
| get_url_query_str | 주어진 URL의 쿼리 문자열을 쿼리 문자열 이름 및 쿼리 문자열 값의 맵으로 반환합니다. | <ul><li>URL: **필수** 쿼리 문자열을 가져오려는 URL.</li><li>앵커: **필수** 쿼리 문자열에서 앵커를 사용하여 수행할 작업을 결정합니다. &quot;retain&quot;, &quot;remove&quot; 또는 &quot;append&quot;의 세 가지 값 중 하나일 수 있습니다.<br><br>값이 &quot;retain&quot;이면 앵커가 반환된 값에 첨부됩니다.<br>값이 &quot;remove&quot;이면 반환된 값에서 앵커가 제거됩니다.<br>값이 &quot;append&quot;이면 앵커가 별도의 값으로 반환됩니다.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#nose&quot;, &quot;retain&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com&#x200B;:8042/over/there&#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | 이 함수는 URL을 입력으로 취하여 특수 문자를 ASCII 문자로 바꾸거나 인코딩합니다. 특수 문자에 대한 자세한 내용은 [특수 문자 목록](#special-characters) 이 문서의 부록에서. | <ul><li>URL: **필수** ASCII 문자로 바꾸거나 인코딩할 특수 문자가 있는 입력 URL입니다.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | 이 함수는 URL을 입력으로 사용하고 ASCII 문자를 특수 문자로 디코딩합니다.  특수 문자에 대한 자세한 내용은 [특수 문자 목록](#special-characters) 이 문서의 부록에서. | <ul><li>URL: **필수** 특수 문자로 디코딩할 ASCII 문자가 있는 입력 URL입니다.</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>://example.com/partneralliance_아시아 태평양_2022 |

{style="table-layout:auto"}

### 날짜 및 시간 함수 {#date-and-time}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오. 에 대한 추가 정보 `date` 함수는 의 날짜 섹션에서 찾을 수 있습니다. [데이터 형식 처리 안내서](./data-handling.md#dates).

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 현재 시간을 검색합니다. | | now() | now() | `2021-10-26T10:10:24Z` |
| 타임스탬프 | 현재 Unix 시간을 검색합니다. | | timestamp() | timestamp() | 1571850624571 |
| 형식 | 지정된 형식에 따라 입력 날짜 형식을 지정합니다. | <ul><li>날짜: **필수** 서식을 지정할 ZonedDateTime 개체의 입력 날짜입니다.</li><li>형식: **필수** 날짜를 변경할 형식입니다.</li></ul> | format(DATE, FORMAT) | 형식(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | <ul><li>타임스탬프: **필수** 서식을 지정할 타임스탬프입니다. 밀리초 단위로 기록됩니다.</li><li>형식: **필수** 타임스탬프를 지정할 형식입니다.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| 날짜 | 날짜 문자열을 ZonedDateTime 개체로 변환합니다(ISO 8601 형식). | <ul><li>날짜: **필수** 날짜를 나타내는 문자열입니다.</li><li>형식: **필수** 소스 날짜의 형식을 나타내는 문자열입니다.**참고:** 다음과 같습니다. **아님** 날짜 문자열을 로 변환할 형식을 나타냅니다. </li><li>DEFAULT_DATE: **필수** 제공된 날짜가 null인 경우 반환되는 기본 날짜.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| 날짜 | 날짜 문자열을 ZonedDateTime 개체로 변환합니다(ISO 8601 형식). | <ul><li>날짜: **필수** 날짜를 나타내는 문자열입니다.</li><li>형식: **필수** 소스 날짜의 형식을 나타내는 문자열입니다.**참고:** 다음과 같습니다. **아님** 날짜 문자열을 로 변환할 형식을 나타냅니다. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| 날짜 | 날짜 문자열을 ZonedDateTime 개체로 변환합니다(ISO 8601 형식). | <ul><li>날짜: **필수** 날짜를 나타내는 문자열입니다.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | 날짜의 일부를 검색합니다. 지원되는 구성 요소 값은 다음과 같습니다. <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;월&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;주&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;weekday&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;밀리초&quot;<br>&quot;SSS&quot; | <ul><li>구성 요소: **필수** 날짜의 일부를 나타내는 문자열입니다. </li><li>날짜: **필수** 표준 형식의 날짜입니다.</li></ul> | date_&#x200B;part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;)) | 10 |
| set_date_part | 지정된 날짜의 구성 요소를 대체합니다. 다음 구성 요소가 허용됩니다. <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;월&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>구성 요소: **필수** 날짜의 일부를 나타내는 문자열입니다. </li><li>값: **필수** 지정된 날짜의 구성 요소에 대해 설정할 값입니다.</li><li>날짜: **필수** 표준 형식의 날짜입니다.</li></ul> | set_date_&#x200B;part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | 부품에서 날짜를 생성합니다. 이 함수는 make_timestamp를 사용하여 유도할 수도 있습니다. | <ul><li>연도: **필수** 네 자리 숫자로 쓰인 연도입니다.</li><li>월: **필수** 월. 허용되는 값은 1-12입니다.</li><li>일: **필수** 그날. 허용되는 값은 1~31입니다.</li><li>시간: **필수** 시간. 허용되는 값은 0~23입니다.</li><li>분: **필수** 분. 허용되는 값은 0~59입니다.</li><li>나노초: **필수** 나노초 값입니다. 허용되는 값은 0에서 999999999까지입니다.</li><li>시간대: **필수** 날짜 시간에 대한 시간대입니다.</li></ul> | make_date_&#x200B;time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | 모든 시간대의 날짜를 UTC 형식의 날짜로 변환합니다. | <ul><li>날짜: **필수** 변환하려는 날짜입니다.</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | 날짜를 한 시간대에서 다른 시간대로 변환합니다. | <ul><li>날짜: **필수** 변환하려는 날짜입니다.</li><li>영역: **필수** 날짜를 전환하려는 시간대입니다.</li></ul> | zone_date_to_&#x200B;zone(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### 계층 - 객체 {#objects}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | 개체가 비어 있는지 확인합니다. | <ul><li>입력: **필수** 확인하려는 개체가 비어 있습니다.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| arrays_to_object | 개체 목록을 만듭니다. | <ul><li>입력: **필수** 키 및 배열 쌍의 그룹입니다.</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | 지정된 플랫 키/값 쌍을 기반으로 개체를 만듭니다. | <ul><li>입력: **필수** 키/값 쌍의 단순 목록입니다.</li></ul> | to_object(INPUT) | to_&#x200B;object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 입력 문자열에서 개체를 만듭니다. | <ul><li>문자열: **필수** 개체를 만들기 위해 구문 분석 중인 문자열입니다.</li><li>VALUE_DELIMITER: *선택 사항* 필드와 값을 구분하는 구분 기호입니다. 기본 구분 기호는 입니다. `:`.</li><li>필드 구분 기호: *선택 사항* 필드 값 쌍을 구분하는 구분 기호입니다. 기본 구분 기호는 입니다. `,`.</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **참고**: 다음을 사용할 수 있습니다 `get()` 과 함께 함수 `str_to_object()` 문자열의 키 값을 검색합니다. | <ul><li>예 #1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>예 #2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>예 #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>예 #2: &quot;John&quot;</li></ul> |
| contains_key | 원본 데이터 내에 개체가 있는지 확인합니다. **참고:** 이 함수는 사용되지 않는 을 대체합니다. `is_set()` 함수. | <ul><li>입력: **필수** 소스 데이터 내에 있는지 확인할 경로입니다.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| 무효화 | 속성 값을 로 설정합니다. `null`. 필드를 대상 스키마에 복사하지 않으려는 경우 사용해야 합니다. | | 무효화() | 무효화() | `null` |
| get_keys | 키/값 쌍을 구문 분석하고 모든 키를 반환합니다. | <ul><li>개체: **필수** 키를 추출할 개체입니다.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Preference&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | 키/값 쌍을 구문 분석하고 지정된 키를 기준으로 문자열 값을 반환합니다. | <ul><li>문자열: **필수** 구문 분석할 문자열입니다.</li><li>키: **필수** 값을 추출해야 하는 키입니다.</li><li>VALUE_DELIMITER: **필수** 필드와 값을 구분하는 구분 기호입니다. 다음 중 하나의 경우: `null` 빈 문자열이 제공된 경우 이 값은 다음과 같습니다. `:`.</li><li>필드 구분 기호: *선택 사항* 필드 쌍과 값 쌍을 구분하는 구분 기호입니다. 다음 중 하나의 경우: `null` 빈 문자열이 제공된 경우 이 값은 다음과 같습니다. `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | 맵과 키 입력을 가져옵니다. 입력이 단일 키인 경우 함수는 해당 키와 연관된 값을 반환합니다. 입력이 문자열 배열이면 함수는 제공된 키에 해당하는 모든 값을 반환합니다. 들어오는 맵에 중복 키가 있는 경우 반환 값은 키를 중복 제거하고 고유 값을 반환해야 합니다. | <ul><li>맵: **필수** 입력 맵 데이터.</li><li>키:  **필수** 키는 단일 문자열 또는 문자열 배열일 수 있습니다. 다른 기본 유형(데이터/숫자)이 제공되면 문자열로 처리됩니다.</li></ul> | get_values(MAP, KEY) | 다음을 참조하십시오. [부록](#map_get_values) 코드 샘플. | |
| map_has_keys | 하나 이상의 입력 키가 제공되면 함수는 true를 반환합니다. 문자열 배열이 입력으로 제공되면 함수는 발견되는 첫 번째 키에 true를 반환합니다. | <ul><li>맵:  **필수** 입력 맵 데이터</li><li>키:  **필수** 키는 단일 문자열 또는 문자열 배열일 수 있습니다. 다른 기본 유형(데이터/숫자)이 제공되면 문자열로 처리됩니다.</li></ul> | map_has_keys(MAP, KEY) | 다음을 참조하십시오. [부록](#map_has_keys) 코드 샘플. | |
| add_to_map | 최소 두 개 이상의 입력을 허용합니다. 맵의 수는 입력으로서 제공될 수 있다. 데이터 준비는 모든 입력의 모든 키-값 쌍이 있는 단일 맵을 반환합니다. 하나 이상의 키가 동일한 맵에서 또는 맵 간에 반복되는 경우, 데이터 준비는 첫 번째 키-값 쌍이 입력에서 전달된 순서대로 유지되도록 키를 중복 제거합니다. | 맵: **필수** 입력 맵 데이터. | add_to_map(지도 1, 지도 2, 지도 3, ...) | 다음을 참조하십시오. [부록](#add_to_map) 코드 샘플. | |
| object_to_map (구문 1) | 이 함수를 사용하여 맵 데이터 유형을 만듭니다. | <ul><li>키: **필수** 키는 문자열이어야 합니다. 정수 또는 날짜와 같은 다른 기본 값이 제공되면 문자열로 자동 변환되고 문자열로 처리됩니다.</li><li>ANY_TYPE **필수** 맵은 제외하고 지원되는 모든 XDM 데이터 유형을 참조합니다.</li></ul> | object_to_map(KEY, ANY_TYPE, KEY, ANY_TYPE, ... ) | 다음을 참조하십시오. [부록](#object_to_map) 코드 샘플. | |
| object_to_map (구문 2) | 이 함수를 사용하여 맵 데이터 유형을 만듭니다. | <ul><li>개체: **필수** 들어오는 개체 또는 개체 배열을 제공하고 개체 내의 속성을 키로 지정할 수 있습니다.</li></ul> | object_to_map(OBJECT) | 다음을 참조하십시오. [부록](#object_to_map) 코드 샘플. |
| object_to_map (구문 3) | 이 함수를 사용하여 맵 데이터 유형을 만듭니다. | <ul><li>개체: **필수** 들어오는 개체 또는 개체 배열을 제공하고 개체 내의 속성을 키로 지정할 수 있습니다.</li></ul> | object_to_map(OBJECT_ARRAY, ATTRIBUTE_IN_OBJECT_TO_BE_USED_AS_A_KEY) | 다음을 참조하십시오. [부록](#object_to_map) 코드 샘플. |

{style="table-layout:auto"}

개체 복사 기능에 대한 자세한 내용은 섹션을 참조하십시오 [아래](#object-copy).

### 계층 - 배열 {#arrays}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 결합 | 지정된 배열에서 null이 아닌 첫 번째 개체를 반환합니다. | <ul><li>입력: **필수** null이 아닌 첫 번째 개체를 찾을 배열입니다.</li></ul> | coalesce(입력) | coalesce(null, null, null, null, &quot;첫 번째&quot;, null, &quot;두 번째&quot;) | &quot;first&quot; |
| 첫 번째 | 지정된 배열의 첫 번째 요소를 검색합니다. | <ul><li>입력: **필수** 의 첫 번째 요소를 찾을 배열입니다.</li></ul> | 첫 번째(입력) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| 마지막 | 지정된 배열의 마지막 요소를 검색합니다. | <ul><li>입력: **필수** 의 마지막 요소를 찾을 배열입니다.</li></ul> | 마지막(입력) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | 배열 끝에 요소를 추가합니다. | <ul><li>배열: **필수** 요소를 추가할 배열입니다.</li><li>값: 배열에 추가할 요소입니다.</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_arrays | 배열을 서로 결합합니다. | <ul><li>배열: **필수** 요소를 추가할 배열입니다.</li><li>값: 상위 배열에 추가할 배열입니다.</li></ul> | join_arrays&#x200B;(ARRAY, VALUES) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [&#39;d&#39;, &#39;e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | 입력 목록을 가져와서 배열로 변환합니다. | <ul><li>INCLUDE_NULL: **필수** 응답 배열에 null을 포함할지 여부를 나타내는 부울 값입니다.</li><li>값: **필수** 배열로 변환할 요소입니다.</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | 입력 크기를 반환합니다. | <ul><li>입력: **필수** 크기를 찾으려는 개체입니다.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | 이 함수는 전체 입력 배열의 모든 요소를 프로필의 배열 끝에 추가하는 데 사용합니다. 이 함수는 **전용** 업데이트 중에 적용할 수 있습니다. 삽입 컨텍스트에서 사용되는 경우 이 함수는 입력을 그대로 반환합니다. | <ul><li>배열: **필수** 프로필에 배열을 추가할 배열입니다.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [123,456] |
| upsert_array_replace | 이 함수는 배열에서 요소를 바꾸는 데 사용합니다. 이 함수는 **전용** 업데이트 중에 적용할 수 있습니다. 삽입 컨텍스트에서 사용되는 경우 이 함수는 입력을 그대로 반환합니다. | <ul><li>배열: **필수** 프로필에서 배열을 대체할 배열입니다.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [123,456] |

{style="table-layout:auto"}

### 계층 - 맵 {#map}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| array_to_map | 이 함수는 개체 배열과 키를 입력으로 취하여 값을 키로 사용하고 배열 요소를 값으로 하는 키 필드의 맵을 반환합니다. | <ul><li>입력: **필수** null이 아닌 첫 번째 개체를 찾을 개체 배열입니다.</li><li>키:  **필수** 키는 개체 배열의 필드 이름이어야 하며 개체를 값으로 사용해야 합니다.</li></ul> | array_to_map(OBJECT[] 입력, 키) | 읽기 [부록](#object_to_map) 코드 샘플. |
| object_to_map | 이 함수는 개체를 인수로 사용하고 키-값 쌍의 맵을 반환합니다. | <ul><li>입력: **필수** null이 아닌 첫 번째 개체를 찾을 개체 배열입니다.</li></ul> | object_to_map(OBJECT_INPUT) | &quot;object_to_map(address) 여기서 입력은 &quot; + &quot;address: {line1 : \&quot;345 park ave\&quot;,line2: \&quot;bldg 2\&quot;,도시 : \&quot;san jose\&quot;,상태 : \&quot;CA\&quot;,유형: \&quot;office\&quot;}입니다.&quot; | 입력이 null인 경우 필드 이름과 값 쌍이 지정된 맵을 반환하거나 null을 반환합니다. 예: `"{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"` |
| to_map | 이 함수는 키-값 쌍의 목록을 가져와서 키-값 쌍의 맵을 반환합니다. | | to_map(OBJECT_INPUT) | &quot;to_map(\&quot;firstName\&quot;, \&quot;John\&quot;, \&quot;lastName\&quot;, \&quot;Doe\&quot;)&quot; | 입력이 null인 경우 필드 이름과 값 쌍이 지정된 맵을 반환하거나 null을 반환합니다. 예: `"{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"` |

{style="table-layout:auto"}

### 논리 연산자 {#logical-operators}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decode | 키와 키 값 쌍의 목록이 배열로 병합되면 이 함수는 키가 있는 경우 값을 반환하고 배열에 있는 경우 기본값을 반환합니다. | <ul><li>키: **필수** 일치시킬 키입니다.</li><li>OPTIONS: **필수** 키/값 쌍의 병합된 배열입니다. 원할 경우 끝에 기본값을 입력할 수 있습니다.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 지정된 stateCode가 &quot;ca&quot;, &quot;California&quot;인 경우<br>주코드가 &quot;pa&quot;이면 &quot;Pennsylvania&quot;입니다.<br>stateCode가 다음과 일치하지 않으면 &quot;N/A&quot;입니다. |
| iif | 주어진 부울 표현식을 평가하고 결과를 기반으로 지정된 값을 반환합니다. | <ul><li>표현식: **필수** 평가 중인 부울 표현식입니다.</li><li>TRUE_값: **필수** 표현식이 true로 평가되는 경우 반환되는 값입니다.</li><li>FALSE_값: **필수** 표현식이 false로 평가되는 경우 반환되는 값입니다.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style="table-layout:auto"}

### 집계 {#aggregation}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 주어진 인수의 최소값을 반환합니다. 자연어 순서 지정을 사용합니다. | <ul><li>OPTIONS: **필수** 서로 비교할 수 있는 하나 이상의 개체입니다.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | 주어진 인수의 최대값을 반환합니다. 자연어 순서 지정을 사용합니다. | <ul><li>OPTIONS: **필수** 서로 비교할 수 있는 하나 이상의 개체입니다.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### 유형 전환 {#type-conversions}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 문자열을 BigInteger로 변환합니다. | <ul><li>문자열: **필수** BigInteger로 변환될 문자열입니다.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000.34 |
| to_decimal | 문자열을 Double로 변환합니다. | <ul><li>문자열: **필수** Double로 변환할 문자열입니다.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 문자열을 Float로 변환합니다. | <ul><li>문자열: **필수** Float으로 변환될 문자열입니다.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 문자열을 정수로 변환합니다. | <ul><li>문자열: **필수** 정수로 변환될 문자열입니다.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### JSON 함수 {#json}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 해당 문자열에서 JSON 콘텐츠를 deserialize합니다. | <ul><li>문자열: **필수** 역직렬화할 JSON 문자열.</li></ul> | json_to_&#x200B;object(STRING) | &#x200B; json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}}) | JSON을 나타내는 개체입니다. |

{style="table-layout:auto"}

### 특수 작업 {#special-operations}

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 의사 무작위 ID를 생성합니다. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | 이 함수는 FPID 문자열을 가져와 Adobe Experience Platform 및 Adobe Experience Cloud 애플리케이션에서 사용할 ECID로 변환합니다. | <ul><li>문자열: **필수** ECID로 변환할 FPID 문자열입니다.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### 사용자 에이전트 기능 {#user-agent}

아래 표에 포함된 모든 사용자 에이전트 함수는 다음 값 중 하나를 반환할 수 있습니다.

* 휴대폰 - 작은 화면이 있는 모바일 디바이스(일반적으로 7&quot; 미만)
* 모바일 - 아직 식별되지 않은 모바일 디바이스. 이 모바일 디바이스는 eReader, 태블릿, 전화기, 시계 등일 수 있다.

장치 필드 값에 대한 자세한 내용은 [장치 필드 값 목록](#device-field-values) 이 문서의 부록에서.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 사용자 에이전트 문자열에서 운영 체제 이름을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | 사용자 에이전트 문자열에서 운영 체제의 주요 버전을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0(iPhone, CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46(KHTML, like Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | 사용자 에이전트 문자열에서 운영 체제 버전을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | 사용자 에이전트 문자열에서 운영 체제 이름과 버전을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | 사용자 에이전트 문자열에서 에이전트 버전을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | 사용자 에이전트 문자열에서 에이전트 이름과 주요 버전을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | 사용자 에이전트 문자열에서 에이전트 이름을 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | 사용자 에이전트 문자열에서 장치 클래스를 추출합니다. | <ul><li>사용자 에이전트(_A): **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0(iPhone, Mac OS X와 같은 CPU iPhone OS 5_1_1) AppleWebKit/534.46(KHTML, Gecko) 버전/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 전화 |

{style="table-layout:auto"}

### 개체 복사 {#object-copy}

>[!TIP]
>
>원본 객체가 XDM의 객체에 매핑되면 객체 복사 기능이 자동으로 적용됩니다. 사용자의 추가 작업이 필요하지 않습니다.

객체 복사 기능을 사용하면 매핑을 변경하지 않고 객체의 속성을 자동으로 복사할 수 있습니다. 예를 들어 소스 데이터의 구조가 다음과 같은 경우:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

XDM 구조:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

그러면 매핑은 다음과 같이 됩니다.

```json
address -> addr
address.line1 -> addr.addrLine1
```

위의 예에서 `city` 및 `state` 또한 속성은 런타임 시 자동으로 수집됩니다. `address` 개체가 매핑됩니다. `addr`. 다음을 생성하고자 하는 경우 `line2` xdm 구조의 속성과 입력 데이터에는 `line2` 다음에서 `address` 그러면 매핑을 수동으로 변경할 필요 없이 자동으로 수집됩니다.

자동 매핑이 작동하도록 하려면 다음 전제 조건을 충족해야 합니다.

* 상위 수준 개체를 매핑해야 합니다.
* 새 속성은 XDM 스키마에서 생성되어야 합니다.
* 새 속성은 소스 스키마와 XDM 스키마에서 이름이 일치해야 합니다.

전제 조건 중 어느 것이든 충족되지 않으면 데이터 준비를 사용하여 소스 스키마를 XDM 스키마에 수동으로 매핑해야 합니다.

## 부록

다음은 데이터 준비 매핑 기능 사용에 대한 추가 정보입니다

### 특수 문자 {#special-characters}

아래 표는 예약 문자와 해당 인코딩 문자 목록을 간략하게 설명합니다.

| 예약된 문자 | 인코딩된 문자 |
| --- | --- |
| 공간 | %20 |
| ! | %21 |
| ” | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| 및 | %26 |
| &#39; | %27 |
| ( | %28 |
| ) | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### 장치 필드 값 {#device-field-values}

아래 표에는 장치 필드 값 목록과 해당 설명이 나와 있습니다.

| 디바이스 | 설명 |
| --- | --- |
| 데스크탑 | 데스크탑 또는 랩탑 유형의 장치입니다. |
| 익명화 | 익명 장치입니다. 경우에 따라 다음과 같습니다. `useragents` 익명화 소프트웨어에 의해 바뀐 것입니다. |
| 알 수 없음 | 알 수 없는 장치입니다. 이들은 보통 다음과 같다. `useragents` 장치에 대한 정보가 포함되어 있지 않습니다. |
| 모바일 | 아직 식별되지 않은 모바일 디바이스. 이 모바일 디바이스는 eReader, 태블릿, 전화기, 시계 등일 수 있다. |
| 태블릿 | 화면이 큰 모바일 디바이스(일반적으로 7인치 이상). |
| 전화 | 화면이 작은 모바일 디바이스(일반적으로 7&quot; 미만). |
| 시청 | 화면이 작은 모바일 디바이스(일반적으로 2&quot; 미만). 이러한 디바이스들은 일반적으로 전화/태블릿 타입의 디바이스를 위한 추가 스크린으로서 동작한다. |
| 증강 현실 | AR 기능이 있는 모바일 장치입니다. |
| 가상 현실 | VR 기능이 있는 모바일 장치입니다. |
| eReader | 태블릿과 유사하지만 일반적으로 [!DNL eInk] 화면. |
| 셋톱 박스 | TV 크기의 화면을 통해 상호 작용이 가능한 연결된 장치입니다. |
| TV | 셋톱 박스와 비슷하지만 TV에 내장된 장치입니다. |
| 가전 제품 | 냉장고와 같은 (보통 큰) 가전 제품. |
| 게임 콘솔 | 와 같은 고정 게임 시스템 [!DNL Playstation] 또는 [!DNL XBox]. |
| 휴대용 게임기 | 와 같은 모바일 게임 시스템 [!DNL Nintendo Switch]. |
| 음성 | 다음과 같은 음성 기반 디바이스 [!DNL Amazon Alexa] 또는 [!DNL Google Home]. |
| 자동차 | 차량 기반 브라우저. |
| 로봇 | 웹 사이트를 방문하는 로봇. |
| 로봇 모바일 | 웹 사이트를 방문하지만 모바일 방문자로 간주하기를 원함을 나타내는 로봇. |
| 로봇 모의실험자 | 로봇을 가장하여 웹 사이트를 방문하는 로봇 [!DNL Google], 하지만 그렇지 않습니다. **참고**: 대부분의 경우, 로봇 모방자는 실제로 로봇입니다. |
| 클라우드 | 클라우드 기반 애플리케이션. 이들은 로봇도 해커도 아니지만 연결이 필요한 애플리케이션이다. 여기에는 다음이 포함됩니다 [!DNL Mastodon] 서버. |
| 해커 | 이 장치 값은 스크립팅이 `useragent` 문자열. |

{style="table-layout:auto"}

### 코드 샘플 {#code-samples}

#### map_get_values {#map-get-values}

+++예를 보려면 선택

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++예를 보려면 선택

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++예를 보려면 선택

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++

#### object_to_map {#object_to_map}

**구문 1**

+++예를 보려면 선택

```json
example = "object_to_map(\"firstName\", \"John\", \"lastName\", \"Doe\")",
result = "{\"firstName\" : \"John\", \"lastName\": \"Doe\"}"
```

+++

**구문 2**

+++예를 보려면 선택

```json
example = "object_to_map(address) where input is " +
  "address: {line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}",
result = "{line1 : \"345 park ave\",line2: \"bldg 2\",City : \"san jose\",State : \"CA\",type: \"office\"}"
```

+++

**구문 3**

+++예를 보려면 선택

```json
example = "object_to_map(addresses,type)" +
        "\n" +
        "[\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "]" ,
result = "{\n" +
        "    \"home\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City\": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"home\"\n" +
        "    },\n" +
        "    \"work\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"work\"\n" +
        "    },\n" +
        "    \"office\":\n" +
        "    {\n" +
        "        \"line1\": \"345 park ave\",\n" +
        "        \"line2\": \"bldg 2\",\n" +
        "        \"City \": \"san jose\",\n" +
        "        \"State\": \"CA\",\n" +
        "        \"type\": \"office\"\n" +
        "    }\n" +
        "}" 
```

+++

#### array_to_map {#array_to_map}

+++예를 보려면 선택

```json
example = "array_to_map(addresses, \"type\") where addresses is\n" +
  "\n" +
  "[\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "]" ,
result = "{\n" +
  "    \"home\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City\": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"home\"\n" +
  "    },\n" +
  "    \"work\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"work\"\n" +
  "    },\n" +
  "    \"office\":\n" +
  "    {\n" +
  "        \"line1\": \"345 park ave\",\n" +
  "        \"line2\": \"bldg 2\",\n" +
  "        \"City \": \"san jose\",\n" +
  "        \"State\": \"CA\",\n" +
  "        \"type\": \"office\"\n" +
  "    }\n" +
  "}",
returns = "Returns a map with given field name and value pairs or null if input is null"
```

+++

