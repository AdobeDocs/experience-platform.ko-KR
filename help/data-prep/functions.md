---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;mapper;mapping;mapping fields;mapping functions;
solution: Experience Platform
title: 데이터 준비 함수
topic: overview
description: 이 문서에서는 데이터 준비와 함께 사용되는 매핑 기능을 소개합니다.
translation-type: tm+mt
source-git-commit: 16c718c7c653a0cfe4c3dcefddfc5472525e1828
workflow-type: tm+mt
source-wordcount: '3432'
ht-degree: 3%

---


# 데이터 준비 함수

데이터 준비 함수를 사용하여 소스 필드에 입력된 값을 기반으로 값을 계산하고 계산할 수 있습니다.

## 필드

필드 이름은 문자, 달러 기호(`$`) 또는 밑줄 문자(`_`)로 시작하는 무제한의 유니코드 문자 및 숫자 시퀀스와 같은 모든 법적 식별자가 될 수 있습니다. 변수 이름은 대소문자를 구분합니다.

필드 이름이 이 규칙을 따르지 않으면 필드 이름은 로 둘러싸야 합니다 `${}`. 예를 들어 필드 이름이 &quot;이름&quot; 또는 &quot;이름&quot;인 경우 이름이 `${First Name}` 또는 `${First.Name}` 각각

또한 필드 이름은 **다음 예약 키워드로** 둘러싸야 합니다 `${}`.

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

도트 표기법을 사용하여 하위 필드 내의 데이터에 액세스할 수 있습니다. 예를 들어, `name` 개체가 있는 경우 `firstName` 필드에 액세스하십시오 `name.firstName`.

## 함수 목록

다음 표에는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 기능이 나열되어 있습니다.

### 문자열 함수

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | 지정된 문자열을 연결합니다. | <ul><li>문자열:연결할 문자열.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | regex를 기반으로 문자열을 분할하고 부품 배열을 반환합니다. 선택적으로 문자열을 분할할 regex를 포함할 수 있습니다. 기본적으로 분할은 &quot;,&quot;로 확인됩니다. | <ul><li>문자열: **필수** : 분할해야 하는 문자열입니다.</li><li>REGEX: *선택* 사항문자열을 분할하는 데 사용할 수 있는 정규 표현식.</li></ul> | explode(STRING, REGEX) | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | 하위 문자열의 위치/인덱스를 반환합니다. | <ul><li>입력: **필수** 검색되는 문자열입니다.</li><li>하위 문자열: **필수** 문자열 내에서 검색되는 하위 문자열입니다.</li><li>START_POSITION: *선택* 사항문자열에서 찾을 위치의 위치입니다.</li><li>발생: *선택* 사항시작 위치에서 찾을 n번째 항목입니다. 기본적으로 1입니다. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe`<span>`.com&quot;, &quot;com&quot;) | 6 |
| 교체 | 원래 문자열에 있는 경우 검색 문자열을 대체합니다. | <ul><li>입력: **필수** 입력 문자열입니다.</li><li>TO_FIND: **필수** 입력 내에서 검색하기 위한 문자열입니다.</li><li>TO_REPLACE: **필수** &quot;TO_FIND&quot; 내의 값을 대체할 문자열입니다.</li></ul> | replacestor(INPUT, TO_FIND, TO_REPLACE) | replacestor(&quot;문자열 재테스트&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 대체 테스트입니다.&quot; |
| substr | 주어진 길이의 하위 문자열을 반환합니다. | <ul><li>입력: **필수** 입력 문자열입니다.</li><li>START_INDEX: **필수** 하위 문자열이 시작되는 입력 문자열의 인덱스입니다.</li><li>LENGTH: **Required** The length of the substring.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; 하위 항목&quot; |
| lower /<br>lcase | 문자열을 소문자로 변환합니다. | <ul><li>입력: **필수** 소문자가 변환될 문자열입니다.</li></ul> | lower(INPUT) | lower(&quot;HeLlO&quot;)<br>소문자(&quot;HeLlO&quot;) | &quot;hello&quot; |
| 상단/<br>ucase | 문자열을 대문자로 변환합니다. | <ul><li>입력: **필수** 대문자로 변환할 문자열입니다.</li></ul> | upper(INPUT) | upper(&quot;HeLlO&quot;)<br>ucase(&quot;HeLlO&quot;) | &quot;HELLO&quot; |
| split | 구분 문자로 입력 문자열을 분할합니다. | <ul><li>입력: **필수** 분할될 입력 문자열입니다.</li><li>구분 문자: **필수** 입력 분할에 사용되는 문자열입니다.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | 구분 기호를 사용하여 개체 목록을 연결합니다. | <ul><li>구분 문자: **필수** 개체 연결에 사용할 문자열입니다.</li><li>개체: **필수** 연결할 문자열 배열.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", ["Hello", "world"])` | &quot;Hello world&quot; |
| lpad | 문자열의 왼쪽에 지정된 문자열을 넣습니다. | <ul><li>입력: **필수** 채워질 문자열입니다. 이 문자열은 null일 수 있습니다.</li><li>카운트: **필수** 입력 가능한 문자열의 크기입니다.</li><li>패딩: **필수** 입력 내용을 패드하는 문자열입니다. null 또는 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzygybat&quot; |
| rpad | 지정된 문자열을 포함한 문자열의 오른쪽에 패드를 넣습니다. | <ul><li>입력: **필수** 채워질 문자열입니다. 이 문자열은 null일 수 있습니다.</li><li>카운트: **필수** 입력 가능한 문자열의 크기입니다.</li><li>패딩: **필수** 입력 내용을 패드하는 문자열입니다. null 또는 비어 있으면 단일 공백으로 처리됩니다.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | 지정된 문자열의 첫 번째 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열: **필수** : 첫 번째 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트: **필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자입니다.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | 지정된 문자열의 마지막 &quot;n&quot; 문자를 가져옵니다. | <ul><li>문자열: **필수** 마지막 &quot;n&quot; 문자를 가져오는 문자열입니다.</li><li>카운트: **필수**&#x200B;문자열에서 가져올 &quot;n&quot; 문자입니다.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| 트리밍 | 문자열 시작 부분에서 공백을 제거합니다. | <ul><li>문자열: **필수** 공백을 제거할 문자열입니다.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| 트리밍 | 문자열 끝에서 공백을 제거합니다. | <ul><li>문자열: **필수** 공백을 제거할 문자열입니다.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;hello&quot; |
| trim | 문자열의 시작 및 끝에서 공백을 제거합니다. | <ul><li>문자열: **필수** 공백을 제거할 문자열입니다.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| 다음과 같음 | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분합니다. | <ul><li>STRING1: **필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2: **필수** 비교할 두 번째 문자열입니다.</li></ul> | STRING1.equals(STRING2) | &quot;string1&quot;.equals(&quot;STRING1) | false |
| equalsIgnoreCase | 두 문자열을 비교하여 동일한지 확인합니다. 이 함수는 대/소문자를 구분하지 **않습니다** . | <ul><li>STRING1: **필수** 비교할 첫 번째 문자열입니다.</li><li>STRING2: **필수** 비교할 두 번째 문자열입니다.</li></ul> | STRING1.equalsIgnoreCase(STRING2) | &quot;string1&quot;.equalsIgnoreCase(&quot;STRING1) | true |

### 해싱 함수

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | SHA-1(보안 해시 알고리즘 1)을 사용하여 입력을 받고 해시 값을 생성합니다. | <ul><li>입력: **일반** 텍스트를 해시해야 합니다.</li><li>CHARSET: *선택* 사항문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Secure Hash Algorithm 256(SHA-256)을 사용하여 입력을 받고 해시 값을 생성합니다. | <ul><li>입력: **일반** 텍스트를 해시해야 합니다.</li><li>CHARSET: *선택* 사항문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Secure Hash Algorithm 512(SHA-512)를 사용하여 입력을 받고 해시 값을 생성합니다. | <ul><li>입력: **일반** 텍스트를 해시해야 합니다.</li><li>CHARSET: *선택* 사항문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd0788 a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | MD5를 사용하여 입력을 가져와 해시 값을 생성합니다. | <ul><li>입력: **일반** 텍스트를 해시해야 합니다.</li><li>CHARSET: *선택* 사항문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다. </li></ul> | md5(입력, CHARSET) | md5(&quot;내 텍스트&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | 입력은 CRC(Cycle Redundancy Check) 알고리즘을 사용하여 32비트 순환 코드를 생성합니다. | <ul><li>입력: **일반** 텍스트를 해시해야 합니다.</li><li>CHARSET: *선택* 사항문자 세트의 이름입니다. 가능한 값에는 UTF-8, UTF-16, ISO-8859-1 및 US-ASCII가 포함됩니다.</li></ul> | CRC32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### URL 함수

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | 지정된 URL에서 프로토콜을 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL: **필수** 프로토콜이 추출되어야 하는 URL입니다.</li></ul> | get_url_protocol(URL) | get_url_protocol(&quot;https://platform.adobe.com/home&quot;) | https |
| get_url_host | 주어진 URL의 호스트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL: **필수** 호스트를 추출해야 하는 URL입니다.</li></ul> | get_url_host(URL) | get_url_host(&quot;https://platform.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | 지정된 URL의 포트를 반환합니다. 입력이 잘못된 경우 null을 반환합니다. | <ul><li>URL: **필수** 포트를 추출해야 하는 URL입니다.</li></ul> | get_url_port(URL) | get_url_port(&quot;sftp://example.com//home/joe/employee.csv&quot;) | 22 |
| get_url_path | 지정된 URL의 경로를 반환합니다. 기본적으로 전체 경로가 반환됩니다. | <ul><li>URL: **필수** 경로를 추출해야 하는 URL입니다.</li><li>FULL_PATH: *선택* 사항전체 경로가 반환되는지 여부를 결정하는 부울 값입니다. false로 설정하면 경로의 끝만 반환됩니다.</li></ul> | get_url_path(URL, FULL_PATH) | get_url_path(&quot;sftp://example.com//home/joe/employee.csv&quot;) | &quot;//home/joe/employee.csv&quot; |
| get_url_query_str | 지정된 URL의 쿼리 문자열을 반환합니다. | <ul><li>URL: **필수** 쿼리 문자열을 가져오려는 URL입니다.</li><li>앵커: **필수** 쿼리 문자열에서 앵커로 수행할 작업을 결정합니다. 다음 세 값 중 하나일 수 있습니다.&quot;retain&quot;, &quot;remove&quot; 또는 &quot;append&quot;를 선택합니다.<br><br>값이 &quot;retain&quot;이면 반환된 값에 앵커가 추가됩니다.<br>값이 &quot;remove&quot;이면 반환된 값에서 앵커가 제거됩니다.<br>값이 &quot;append&quot;이면 앵커가 별도의 값으로 반환됩니다.</li></ul> | get_url_query_str(URL, ANCHOR) | get_url_query_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;retain&quot;)<br>get_url_query_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str(&quot;foo://example.com:8042/over/there?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### 날짜 및 시간 함수

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | 현재 시간을 검색합니다. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 현재 Unix 시간을 검색합니다. |  | timestamp() | timestamp() | 1571850624571 |
| format | 지정한 형식에 따라 입력 날짜를 지정합니다. | <ul><li>날짜: **필수** 형식을 지정할 ZunitedDateTime 개체로서 입력 날짜입니다.</li><li>형식: **필수** 날짜를 변경할 형식.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| 형식 | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | <ul><li>타임스탬프: **필수** 형식을 지정할 타임스탬프입니다. 밀리초 단위로 기록됩니다.</li><li>형식: **필수** 타임스탬프를 변경할 형식입니다.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;2019년 10월 23일 11시 24분&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜: **필수** 날짜를 나타내는 문자열입니다.</li><li>형식: **필수** 날짜 형식을 나타내는 문자열입니다.</li><li>DEFAULT_DATE: **필수** 제공된 날짜가 null인 경우 반환된 기본 날짜입니다.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | &quot;2019-10-23T11:24Z&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜: **필수** 날짜를 나타내는 문자열입니다.</li><li>형식: **필수** 날짜 형식을 나타내는 문자열입니다.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 개체(ISO 8601 형식)로 변환합니다. | <ul><li>날짜: **필수** 날짜를 나타내는 문자열입니다.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | 날짜의 부분을 검색합니다. 다음 구성 요소 값이 지원됩니다. <br><br>&quot;year&quot;<br>&quot;<br>&quot;yyyy&quot;<br><br>&quot;yyyy<br>&quot;<br>&quot;yyy&quot;q<br><br>&quot;yyy&quot;q<br>&quot;<br>&quot;cq&quot;<br><br>&quot;cq&quot;<br>&quot;cumuld&quot;alk&quot;<br>&quot;ejy&quot;y&quot;y&quot;day&quot;y&quot;y&quot;y&quot;y&quot;day&quot;<br><br>&quot;<br>&quot;<br>y&quot;ev&quot;y&quot;eyyy&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>00000000000000000000000000000000000000000000000000000000000000000000000000000 4&quot;4&quot;&quot;hh12&quot;cuts&quot;minute&quot;minutes&quot;mymi&quot;emoth&quot;n&quot;second&quot;&quot;second&quot;&quot;&quot;sighters&quot;s&quot;&quot;s&quot;s&quot;milleconds&quot;ms. | <ul><li>구성 요소: **필수** 날짜 부분을 나타내는 문자열. </li><li>날짜: **필수** 날짜입니다(표준 형식).</li></ul> | date_part(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | 지정된 날짜의 구성 요소를 대체합니다. 다음 구성 요소가 허용됩니다. <br><br>&quot;year&quot;<br>&quot;<br>yyyy&quot;<br><br>&quot;yyy<br>&quot;<br>&quot;yyy<br><br>&quot;<br>s&quot;<br>&quot;m&quot;<br><br><br>&quot;<br><br>&quot;dd&quot;<br>&quot;<br>&quot;<br><br>&quot;chour&quot;hh&quot;cultly&quot;<br><br>&quot;cmi&quot;n&quot;&quot;n&quot;second&quot;&quot;&quot;&quot;&quot;s&quot; | <ul><li>구성 요소: **필수** 날짜 부분을 나타내는 문자열. </li><li>값: **필수** 지정된 날짜에 구성 요소에 대해 설정할 값입니다.</li><li>날짜: **필수** 날짜입니다(표준 형식).</li></ul> | set_date_part(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | 부품으로부터 날짜를 만듭니다. make_timestamp를 사용하여 이 함수를 유도할 수도 있습니다. | <ul><li>연도: **필수** 연도, 4자리 숫자</li><li>월: **필요한** 월입니다. 허용되는 값은 1~12입니다.</li><li>일: **필요한** 날짜입니다. 허용되는 값은 1~31입니다.</li><li>시간: **필요한** 시간 허용되는 값은 0부터 23까지입니다.</li><li>분: **필수** 시간입니다. 허용되는 값은 0~59입니다.</li><li>나노초: **나노초 값이 필요합니다** . 허용되는 값은 0부터 99999999까지입니다.</li><li>시간대: **필수** 날짜 시간에 대한 표준 시간대입니다.</li></ul> | make_date_time(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, 나노초, TIMEZONE) | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | 표준 시간대의 날짜를 UTC의 날짜로 변환합니다. | <ul><li>날짜: **필수** 변환하려는 날짜입니다.</li></ul> | zone_date_to_utc(DATE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | 한 시간대에서 다른 시간대로 날짜를 변환합니다. | <ul><li>날짜: **필수** 변환하려는 날짜입니다.</li><li>영역: **필수** 날짜를 변환할 시간대입니다.</li></ul> | zone_date_to_zone(DATE, ZONE) | `zone_date_to_utc(2019-10-17T11:55:12.000000999-07:00[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

### 계층 - 객체

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| size_of | 입력의 크기를 반환합니다. | <ul><li>입력: **필수** 크기를 찾으려고 하는 개체입니다.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | 개체가 비어 있는지 여부를 확인합니다. | <ul><li>입력: **필수** 확인하려는 개체가 비어 있습니다.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | 개체 목록을 만듭니다. | <ul><li>입력: **필수** 키 및 배열 쌍의 그룹입니다.</li></ul> | array_to_object(INPUT) | 샘플 | 샘플 |
| to_object | 주어진 플랫 키/값 쌍을 기반으로 개체를 만듭니다. | <ul><li>입력: **필수** 키/값 쌍의 일반 목록입니다.</li></ul> | to_object(INPUT) | to_object(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | 입력 문자열에서 개체를 만듭니다. | <ul><li>문자열: **필수** 개체를 만들기 위해 파싱되는 문자열입니다.</li><li>VALUE_DELIMITER: *선택* 사항필드와 값을 구분하는 구분 기호입니다. The default delimiter is `:`.</li><li>FIELD_DELIMITER: *선택* 사항필드 값 쌍을 구분하는 구분 기호입니다. The default delimiter is `,`.</li></ul> | str_to_object(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | 전화 - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | 소스 데이터 내에 개체가 있는지 확인합니다. | <ul><li>입력: **필수** 소스 데이터 내에 있는지 확인할 경로입니다.</li></ul> | is_set(INPUT) | is_set(&quot;evars.evar.field1&quot;) | true |

### 계층 - 배열

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 코알스 | 지정된 배열에서 null이 아닌 첫 번째 개체를 반환합니다. | <ul><li>입력: **필수** null이 아닌 첫 번째 개체를 찾을 배열입니다.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| first | 지정된 배열의 첫 번째 요소를 검색합니다. | <ul><li>입력: **필수** 요소의 첫 번째 요소를 찾을 배열입니다.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | 지정된 배열의 마지막 요소를 검색합니다. | <ul><li>입력: **필수** 마지막 요소를 찾을 배열입니다.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | 입력 목록을 가져와 배열로 변환합니다. | <ul><li>INCLUDE_NULLS: **응답 배열에 null을 포함할지 여부를 나타내는 부울 값이 필요합니다** .</li><li>값: **필수** 배열로 변환할 요소입니다.</li></ul> | to_array(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### 논리 연산자

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| 디코딩 | 키워드와 배열 키 값 쌍의 목록이 지정된 경우 이 함수는 키가 있는 경우 값을 반환하거나 배열에 있는 경우 기본값을 반환합니다. | <ul><li>키: **일치해야** 합니다.</li><li>OPTIONS: **필수** 키/값 쌍의 분리된 배열입니다. 선택적으로 기본값을 끝에 배치할 수 있습니다.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | 지정된 stateCode가 &quot;ca&quot;, &quot;California&quot;인 경우.<br>만약 주법이 &quot;pa&quot;, &quot;펜실베이니아&quot; 라면.<br>stateCode가 다음과 일치하지 않는 경우 &quot;N/A&quot; |
| iif | 주어진 부울 식을 평가하고 결과를 기준으로 지정된 값을 반환합니다. | <ul><li>BOOLEAN_EXPRESSION: **필수** 평가되는 부울 식입니다.</li><li>TRUE_VALUE: **필수** 표현식이 true로 평가되는 경우 반환되는 값입니다.</li><li>FALSE_VALUE: **필수** 표현식이 false로 평가되는 경우 반환되는 값입니다.</li></ul> | iif(BOOLEAN_EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### 집계

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | 지정된 인수의 최소 개수를 반환합니다. 자연스러운 순서를 사용합니다. | <ul><li>OPTIONS: **필요한** 하나 이상의 개체가 서로 비교할 수 있습니다.</li></ul> | min(OPTIONS) | 최소(3, 1, 4) | 1 |
| max | 주어진 인수의 최대값을 반환합니다. 자연스러운 순서를 사용합니다. | <ul><li>OPTIONS: **필요한** 하나 이상의 개체가 서로 비교할 수 있습니다.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

### 문자 변환

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | 문자열을 BigInteger로 변환합니다. | <ul><li>문자열: **필수** BigInteger로 변환할 문자열입니다.</li></ul> | to_bigint(STRING) | to_bigint(&quot;100000.34&quot;) | 1000000.34 |
| to_decimal | 문자열을 Double로 변환합니다. | <ul><li>문자열: **필수** Double로 변환할 문자열입니다.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20.5 |
| to_float | 문자열을 Float로 변환합니다. | <ul><li>문자열: **필수** Float로 변환할 문자열입니다.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12.34566 |
| to_integer | 문자열을 정수로 변환합니다. | <ul><li>문자열: **필수** 정수(Integer)로 변환할 문자열입니다.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### JSON 함수

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | 지정된 문자열에서 JSON 콘텐츠를 역직렬화합니다. | <ul><li>문자열: **deserialize할 JSON 문자열이 필요합니다** .</li></ul> | json_to_object(STRING) | json_to_object({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot; :&quot;Doe&quot;}) | JSON을 나타내는 개체입니다. |

### 특별 작업

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | 의사 임의 ID를 생성합니다. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c20633 |

### 사용자 에이전트 기능

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 함수 | 설명 | 매개 변수 | 구문 | 표현식 | 샘플 출력 |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | 사용자 에이전트 문자열에서 운영 체제 이름을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name(USER_AGENT) | ua_os_name(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | iOS |
| ua_os_version_major | 사용자 에이전트 문자열에서 운영 체제의 주 버전을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version_major(USER_AGENT) | ua_os_version_major(&quot;Mozilla/5.0 (iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | iOS 5 |
| ua_os_version | 사용자 에이전트 문자열에서 운영 체제의 버전을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_version(USER_AGENT) | ua_os_version(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | 5.1.1 |
| ua_os_name_version | 사용자 에이전트 문자열에서 운영 체제의 이름과 버전을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_os_name_version(USER_AGENT) | ua_os_name_version(&quot;Mozilla/5.0 (iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | iOS 5.1.1 |
| ua_agent_version | 사용자 에이전트 문자열에서 에이전트 버전을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version(USER_AGENT) | ua_agent_version(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | 5.1 |
| ua_agent_version_major | 사용자 에이전트 문자열에서 에이전트 이름과 주 버전을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_version_major(USER_AGENT) | ua_agent_version_major(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | Safari 5 |
| ua_agent_name | 사용자 에이전트 문자열에서 에이전트 이름을 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_agent_name(USER_AGENT) | ua_agent_name(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | Safari |
| ua_device_class | 사용자 에이전트 문자열에서 장치 클래스를 추출합니다. | <ul><li>USER_AGENT: **필수** 사용자 에이전트 문자열입니다.</li></ul> | ua_device_class(USER_AGENT) | ua_device_class(&quot;Mozilla/5.0(iPhone;CPU iPhone OS 5_1_1(Mac OS X) AppleWebKit/534.46(KHTML(Gecko와 같은) 버전/5.1 Mobile/9B206 Safari/7534.48.3인치) | 전화 |