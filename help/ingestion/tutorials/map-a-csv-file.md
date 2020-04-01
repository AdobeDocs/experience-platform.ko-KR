---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM 스키마에 CSV 파일 매핑
topic: tutorial
translation-type: tm+mt
source-git-commit: 33282b1c8ab1129344bd4d7054e86fed75e7b899

---


# XDM 스키마에 CSV 파일 매핑

CSV 데이터를 Adobe Experience Platform으로 인제스트하려면 데이터를 XDM(Experience Data Model) 스키마에 매핑해야 합니다. 이 자습서에서는 Experience Platform 사용자 인터페이스를 사용하여 CSV 파일을 XDM 스키마에 매핑하는 방법에 대해 설명합니다.

또한 이 자습서의 부록에서는 [매핑 기능의](#mapping-functions)사용에 대한 자세한 정보를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

- [경험 데이터 모델(XDM 시스템)](../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [일괄 처리](../batch-ingestion/overview.md):Platform이 사용자가 제공한 데이터 파일의 데이터를 인제스트하는 방법입니다.

또한 이 자습서에서는 CSV 데이터를 인제스트할 데이터 세트를 이미 만들어야 합니다. UI에서 데이터 세트를 만드는 단계는 [데이터 인제스트 자습서를](./ingest-batch-data.md)참조하십시오.

## 데이터 추가

Experience Platform UI에서 왼쪽 **탐색** 창에서 워크플로우를 클릭한 다음 XDM 스키마에 **CSV**&#x200B;매핑을 클릭합니다. 오른쪽 레일이 나타나면 시작을 **클릭합니다**.

![](../images/tutorials/map-a-csv-file/workflow-tab.png)

XDM _스키마에_ CSV 매핑 워크플로우가 나타납니다. 데이터 _추가_ 단계에서 시작합니다.

![](../images/tutorials/map-a-csv-file/add-data.png)

CSV 파일을 제공된 공간으로 끌어다 놓거나 찾아보기를 클릭하여 **파일을** 직접 선택합니다. 파일이 _업로드되면 샘플 데이터_ 섹션이 나타나 처음 10개의 데이터 행을 보여 줍니다. 데이터가 예상대로 업로드되었음을 확인했으면 다음을 **클릭합니다**.

![](../images/tutorials/map-a-csv-file/csv-added.png)

## 대상 선택

대상 _단계가_ 나타납니다. 제공된 목록에서 CSV 데이터를 수집할 데이터 세트를 선택한 다음 다음을 **클릭합니다**.

![](../images/tutorials/map-a-csv-file/select-destination.png)

## XDM 스키마 필드에 CSV 필드 매핑

매핑 _단계가_ 나타납니다. CSV 파일의 열은 소스 필드 아래에 _나열되며_&#x200B;해당 XDM 스키마 필드가 대상 필드 아래에 _나열됩니다_. 선택되지 않은 대상 필드는 빨간색으로 표시됩니다.

CSV 열을 XDM 필드에 매핑하려면 열의 해당 대상 필드 옆에 있는 스키마 아이콘을 클릭합니다.

![](../images/tutorials/map-a-csv-file/target-field-mapping.png)

스키마 _선택 필드_ 창이 나타납니다. XDM 스키마의 구조를 탐색하고 CSV 열을 매핑할 필드를 찾을 수 있습니다. XDM 필드를 클릭하여 선택한 다음 선택을 **클릭합니다**.

![](../images/tutorials/map-a-csv-file/xdm-field-selection.png)

매핑 _화면이_ 다시 나타나고 선택한 XDM 필드가 이제 타겟 필드 아래에 _나타납니다_.

![](../images/tutorials/map-a-csv-file/xdm-field-mapped.png)

특정 CSV 열을 매핑하지 않으려면 대상 필드 옆에 있는 **제거 아이콘을** 클릭하여 매핑을 제거할 수 있습니다. 새 매핑을 추가하려면 목록 **하단에서 새 매핑** 추가를 클릭합니다.

![](../images/tutorials/map-a-csv-file/remove-or-add-mapping.png)

필드를 매핑할 때 입력 소스 필드를 기반으로 값을 계산하는 함수를 포함할 수도 있습니다. 자세한 내용은 부칙의 [매핑 기능](#mapping-functions) 섹션을 참조하십시오.

위의 단계를 반복하여 CSV 열을 XDM 필드에 매핑합니다. 완료되면 [다음]을 **클릭합니다**.

![](../images/tutorials/map-a-csv-file/mapping-finish.png)

## 데이터 인제스트

인제스트 _단계가_ 표시되어 소스 파일과 대상 데이터 세트에 대한 세부 사항을 검토할 수 있습니다. 인제스트를 **클릭하여** CSV 데이터 인제스트를 시작합니다. CSV 파일의 크기에 따라 이 프로세스는 몇 분 정도 걸릴 수 있습니다. 통합 작업이 완료되면 성공 또는 실패를 나타내는 화면이 업데이트됩니다. Click **Finish** to complete the workflow.

![](../images/tutorials/map-a-csv-file/ingest-data.png)

## 다음 단계

이 자습서를 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 플랫폼에 인제스트했습니다. 이제 이 데이터를 실시간 고객 프로파일과 같은 다운스트림 플랫폼 서비스에서 사용할 수 있습니다. 자세한 [내용은 실시간 고객 프로필 개요를](../../profile/home.md) 참조하십시오.

## 부록

다음 섹션에서는 CSV 열을 XDM 필드에 매핑하기 위한 추가 정보를 제공합니다.

### 매핑 함수

특정 매핑 함수를 사용하여 소스 필드에 입력된 값을 기반으로 값을 계산하고 계산할 수 있습니다. 함수를 사용하려면 소스 필드 아래에 해당 _구문과_ 입력과 함께 입력합니다.

예를 들어 **구/군/시** 및 **국가****CSV 필드를 연결하고** 구/군/시 `concat(city, ", ", county)`XDM 필드에 지정하려면소스 필드를 로설정합니다.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

다음 표에는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 함수가 나와 있습니다.

| 함수 | 설명 | 샘플 표현식 | 샘플 출력 |
| -------- | ----------- | ----------------- | ------------- |
| concat | 지정된 문자열을 연결합니다. | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | regex를 기반으로 문자열을 분할하고 부분 배열을 반환합니다. | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instant | 하위 문자열의 위치/인덱스를 반환합니다. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| 교체 | 원래 문자열에 있는 경우 검색 문자열을 대체합니다. | replacestor(&quot;문자열 재테스트&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 바꾸기 테스트입니다.&quot; |
| substr | 지정된 길이의 하위 문자열을 반환합니다. | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; 하위 항목&quot; |
| lower /<br>lcase | 문자열을 소문자로 변환합니다. | lower(&quot;HeLlO&quot;)<br>소문자(&quot;HeLlO&quot;) | &quot;hello&quot; |
| 대문자/<br>ucase | 문자열을 대문자로 변환합니다. | upper(&quot;HeLlO&quot;)<br>ucase(&quot;HeLlO&quot;) | &quot;HELLO&quot; |
| split | 구분 문자로 입력 문자열을 분할합니다. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | 구분 기호를 사용하여 개체 목록에 연결합니다. | `join(" ", ["Hello", "world"]`) | &quot;Hello world&quot; |
| coalesce | 지정된 목록에서 null이 아닌 첫 번째 개체를 반환합니다. | coalesce(null, null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| decode | 키와 배열로 분리된 키 값 쌍의 목록이 제공되면 키가 발견되면 값을 반환하거나 배열에 있는 경우 기본값을 반환합니다. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | 주어진 부울 표현식을 평가하고 결과를 기준으로 지정된 값을 반환합니다. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | 지정된 인수의 최소값을 반환합니다. 자연스러운 순서를 사용합니다. | min(3, 1, 4) | 1 |
| max | 주어진 인수의 최대값을 반환합니다. 자연스러운 순서를 사용합니다. | max(3, 1, 4) | 4 |
| first | 주어진 첫 번째 인수를 검색합니다. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | 마지막 주어진 인수를 검색합니다. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | 의사 임의 ID를 생성합니다. | uuid()<br>guid() | {UNIQUE_ID} |
| now | 현재 시간을 검색합니다. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 현재 Unix 시간을 검색합니다. | timestamp() | 1571850624571 |
| format | 지정된 형식에 따라 입력 날짜를 포맷합니다. | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| 형식 | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;2019년 10월 23일 11:24&quot; |
| date | 날짜 문자열을 ZundedDateTime 개체(ISO 8601 형식)로 변환합니다. | date(&quot;2019년 10월 23일 11:24&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | 날짜의 부분을 검색합니다. 다음 구성 요소 값이 지원됩니다.&quot; <br><br>&quot;year&quot;<br>&quot;<br>yyyyy&quot;<br><br>&quot;<br><br>&quot;<br><br>&quot;<br>&quot;<br>yyyy&quot;<br><br><br>&quot;년&quot;년&quot;년<br>&quot;년&quot;007<br><br>&quot;일&quot;007000700800800800800<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>0800000008000000000000000000800000000000000000000000000000000000000000000000024&quot;4&quot;o죽이면&quot;hh12&quot;minute&quot;minute&quot;mi&quot;mi&quot;n&quot;eths&quot;second&quot;Eths&quot;S&quot;S&quot;S&quot;Oths&quot;S&quot;Elds&quot;입니다. | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | 지정된 날짜의 구성 요소를 대체합니다. 다음 구성 요소가 허용됩니다.&quot;year&quot; <br><br>&quot;yyyyy&quot;<br><br>&quot;<br><br>yyyy<br>&quot;<br>yyyy<br><br>&quot;<br>yy년<br>&quot;yy<br><br>&quot;yyy<br>&quot;yyy&quot;yy<br><br>&quot;yyy&quot;<br>&quot;yy&quot;m&quot;Dd&quot;<br><br><br><br><br>&quot;Ykh&quot;Hour&quot;Kh&quot;Minutes&quot;Mi&quot;Oth&quot;Second&quot;S&quot;s&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | 부품에서 날짜를 만듭니다. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | 현재 타임스탬프를 반환합니다. | current_timestamp() | 1571850624571 |
| current_date | 시간 구성 요소 없이 현재 날짜를 반환합니다. | current_date() | &quot;2019년 11월 18일&quot; |