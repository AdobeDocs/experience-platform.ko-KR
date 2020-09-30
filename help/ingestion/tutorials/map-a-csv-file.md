---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: XDM 스키마에 CSV 파일 매핑
topic: tutorial
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 XDM 스키마에 CSV 파일을 매핑하는 방법을 설명합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 2%

---


# XDM 스키마에 CSV 파일 매핑

CSV 데이터를 인제스트하려면 데이터 [!DNL Adobe Experience Platform]를 [!DNL Experience Data Model] (XDM) 스키마에 매핑해야 합니다. 이 자습서에서는 [!DNL Platform] 사용자 인터페이스를 사용하여 XDM 스키마에 CSV 파일을 매핑하는 방법을 설명합니다.

또한 이 자습서의 부록에서는 [매핑 함수 사용에 대한 자세한 정보를 제공합니다](#mapping-functions).

## 시작하기

이 자습서에서는 다음의 구성 요소에 대해 작업해야 [!DNL Platform]합니다.

- [[!DNL 경험 데이터 모델(XDM 시스템)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크
- [[!DNL 일괄 처리]](../batch-ingestion/overview.md):사용자가 제공한 데이터 파일에서 데이터를 [!DNL Platform] 인제스트하는 방법입니다.

또한 이 자습서에서는 CSV 데이터를 인제스트하기 위한 데이터 세트를 이미 만들어야 합니다. UI에서 데이터 세트를 만드는 단계는 [데이터 인제스트 자습서를 참조하십시오](./ingest-batch-data.md).

## 대상 선택

[!DNL Adobe Experience Platform]에 [로그인한 다음](https://platform.adobe.com) 왼쪽 탐색 막대에서 **[!UICONTROL 워크플로우]** 를 선택하여 **[!UICONTROL 워크플로우 작업 영역에]** 액세스합니다.

워크플로우 **[!UICONTROL 화면에서]** **[!UICONTROL 데이터 수집]** 섹션 **[!UICONTROL 에서 CSV를 XDM에]** 매핑합니다 **[!UICONTROL 를 선택한 다음 LaunchDm을]**&#x200B;선택합니다.

![](../images/tutorials/map-a-csv-file/workflows.png)

대상 **[!UICONTROL 단계부터 시작하여 XDM 스키마에]** CSV **[!UICONTROL 매핑 워크플로우가]** 나타납니다. 수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다.

**기존 데이터 세트 사용**

CSV 데이터를 기존 데이터 세트에 인제스트하려면 기존 데이터 세트 **[!UICONTROL 사용을 선택합니다]**. 검색 기능을 사용하거나 패널의 기존 데이터 집합 목록을 스크롤하여 기존 데이터 집합을 검색할 수 있습니다.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

CSV 데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL 새 데이터 세트]** 만들기를 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다. 검색 기능을 사용하거나 제공된 스키마 목록을 스크롤하여 스키마를 선택합니다. 계속하려면 **[!UICONTROL 다음]** 을 선택합니다.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## 데이터 추가

데이터 **[!UICONTROL 추가]** 단계가 나타납니다. CSV 파일을 제공된 공간으로 끌어다 놓거나 파일 선택 **[!UICONTROL 을 선택하여 CSV]** 파일을 수동으로 입력합니다.

![](../images/tutorials/map-a-csv-file/add-data.png)

파일이 업로드되면 **[!UICONTROL 샘플 데이터]** 섹션이 나타나 처음 10개의 데이터 행을 보여 줍니다. 데이터가 예상대로 업로드되었음을 확인했으면 다음을 **[!UICONTROL 선택합니다]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## XDM 스키마 필드에 CSV 필드 매핑

매핑 **[!UICONTROL 단계가]** 나타납니다. CSV 파일의 열은 **[!UICONTROL 소스 필드]**&#x200B;아래에 나열되며 해당 XDM 스키마 필드는 **[!UICONTROL Target 필드]**&#x200B;아래에 나열됩니다. 선택되지 않은 대상 필드는 빨간색으로 표시됩니다. 필터 필드 옵션을 사용하여 사용 가능한 소스 필드 목록의 범위를 좁힐 수 있습니다.

>[!TIP]
>
>[!DNL Platform] 선택한 대상 스키마나 데이터 세트에 따라 자동 매핑 필드에 대한 지능적인 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다.

CSV 열을 XDM 필드에 매핑하려면 열의 해당 대상 필드 옆에 있는 스키마 아이콘을 선택합니다.

![](../images/tutorials/map-a-csv-file/mapping.png)

스키마 **[!UICONTROL 선택 필드]** 창이 나타납니다. XDM 스키마의 구조를 탐색하고 CSV 열을 매핑할 필드를 찾을 수 있습니다. XDM 필드를 클릭하여 선택한 다음 **[!UICONTROL 선택을 클릭합니다]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

매핑되지 않은 나머지 소스 필드에 대한 단계를 완료하면 **[!UICONTROL 매핑]** 화면이 다시 나타나고 선택한 XDM 필드가 **[!UICONTROL Target 필드]**&#x200B;아래에 나타납니다.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

필드를 매핑할 때 입력 소스 필드를 기반으로 값을 계산하는 함수를 포함할 수도 있습니다. 자세한 내용은 부록에 있는 [매핑 기능](#mapping-functions) 섹션을 참조하십시오.

### 계산된 필드 추가

계산된 필드를 사용하면 입력 스키마의 특성을 기반으로 값을 만들 수 있습니다. 그런 다음 이러한 값을 대상 스키마의 속성에 할당할 수 있으며 쉽게 참조할 수 있도록 이름 및 설명을 제공할 수 있습니다.

계속하려면 계산된 필드 **[!UICONTROL 추가]** 단추를 선택합니다.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

계산된 필드 **[!UICONTROL 만들기]** 패널이 나타납니다. 왼쪽 대화 상자에는 계산된 필드에서 지원되는 필드, 함수 및 연산자가 있습니다. 표현식 편집기에 함수, 필드 또는 연산자를 추가할 탭 중 하나를 선택합니다.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| 탭 | 설명 |
| --------- | ----------- |
| 필드 | 필드 탭에는 소스 스키마에서 사용할 수 있는 필드 및 속성이 나열됩니다. |
| 함수 | 함수 탭에는 데이터를 변형하는 데 사용할 수 있는 기능이 나열됩니다. |
| 연산자 | 연산자 탭에는 데이터를 변형하는 데 사용할 수 있는 연산자가 나열됩니다. |

가운데 표현식 편집기를 사용하여 필드, 함수 및 연산자를 수동으로 추가할 수 있습니다. 표현식 생성을 시작하려면 편집기를 선택합니다.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

계속하려면 **[!UICONTROL 저장을]** 선택합니다.

새로 만든 소스 필드와 함께 매핑 화면이 다시 나타납니다. 적절한 대상 필드를 적용하고 **[!UICONTROL 마침을]** 선택하여 매핑을 완료합니다.

![](../images/tutorials/map-a-csv-file/new-field.png)

## 데이터 흐름 모니터링

CSV 파일을 매핑하고 만들면 CSV 파일을 통해 수집되는 데이터를 모니터링할 수 있습니다. 데이터 흐름 모니터링에 대한 자세한 내용은 스트리밍 데이터 흐름 [모니터링에 대한 자습서를 참조하십시오](../../ingestion/quality/monitor-data-flows.md).

## 다음 단계

이 자습서를 따라 플랫 CSV 파일을 XDM 스키마에 매핑하고 인제스트했습니다 [!DNL Platform]. 이제 이 데이터를 같은 다운스트림 [!DNL Platform] 서비스에서 사용할 수 있습니다 [!DNL Real-time Customer Profile]. 자세한 내용은 [[!DNL 실시간 고객 프로필]](../../profile/home.md) 개요를 참조하십시오.

## 부록

다음 섹션에서는 CSV 열을 XDM 필드에 매핑하기 위한 추가 정보를 제공합니다.

### 매핑 함수

특정 매핑 함수를 사용하여 소스 필드에 입력된 값을 기반으로 값을 계산하고 계산할 수 있습니다. 함수를 사용하려면 적절한 구문 및 입력 **[!UICONTROL 과 함께 소스 필드]** 아래에 입력합니다.

예를 들어 **구/군/시** 와 **국가** CSV 필드를 연결하고 **구/군** 시 `concat(city, ", ", county)`XDM 필드에 지정하려면 소스 필드를로설정합니다.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

다음 표에는 샘플 표현식 및 결과 출력을 포함하여 지원되는 모든 매핑 기능이 나열되어 있습니다.

| 함수 | 설명 | 샘플 표현식 | 샘플 출력 |
| -------- | ----------- | ----------------- | ------------- |
| concat | 지정된 문자열을 연결합니다. | concat(&quot;Hi, &quot;, &quot;there&quot;, &quot;!&quot;) | `"Hi, there!"` |
| 분해 | regex를 기반으로 문자열을 분할하고 부품 배열을 반환합니다. | explode(&quot;Hi, there!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | 하위 문자열의 위치/인덱스를 반환합니다. | instr(&quot;adobe<span>.com&quot;, &quot;com&quot;) | 6 |
| 교체 | 원래 문자열에 있는 경우 검색 문자열을 대체합니다. | replacestor(&quot;문자열 재테스트&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;문자열 대체 테스트입니다.&quot; |
| substr | 주어진 길이의 하위 문자열을 반환합니다. | substr(&quot;This is a substring test&quot;, 7, 8) | &quot; 하위 항목&quot; |
| lower /<br>lcase | 문자열을 소문자로 변환합니다. | lower(&quot;HeLlO&quot;)<br>소문자(&quot;HeLlO&quot;) | &quot;hello&quot; |
| 상단/<br>ucase | 문자열을 대문자로 변환합니다. | upper(&quot;HeLlO&quot;)<br>ucase(&quot;HeLlO&quot;) | &quot;HELLO&quot; |
| split | 구분 문자로 입력 문자열을 분할합니다. | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | 구분 기호를 사용하여 개체 목록을 연결합니다. | `join(" ", ["Hello", "world"]`) | &quot;Hello world&quot; |
| 코알스 | 지정된 목록에서 null이 아닌 첫 번째 개체를 반환합니다. | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| 디코딩 | 키워드와 배열 키 값 쌍의 목록이 지정된 경우 이 함수는 키가 있는 경우 값을 반환하거나 배열에 있는 경우 기본값을 반환합니다. | decode(&quot;k2&quot;, &quot;k1&quot;, &quot;v1&quot;, &quot;k2&quot;, &quot;v2&quot;, &quot;default&quot;) | &quot;v2&quot; |
| iif | 주어진 부울 식을 평가하고 결과를 기준으로 지정된 값을 반환합니다. | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| min | 지정된 인수의 최소 개수를 반환합니다. 자연스러운 순서를 사용합니다. | 최소(3, 1, 4) | 1 |
| max | 주어진 인수의 최대값을 반환합니다. 자연스러운 순서를 사용합니다. | max(3, 1, 4) | 4 |
| first | 주어진 첫 번째 인수를 검색합니다. | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | 마지막 주어진 인수를 검색합니다. | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| uuid /<br>guid | 의사 임의 ID를 생성합니다. | uuid()<br>guid() | {UNIQUE_ID} |
| now | 현재 시간을 검색합니다. | now() | `2019-10-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | 현재 Unix 시간을 검색합니다. | timestamp() | 1571850624571 |
| format | 지정한 형식에 따라 입력 날짜를 지정합니다. | format({DATE}, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| 형식 | 지정된 형식에 따라 타임스탬프를 날짜 문자열로 변환합니다. | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;2019년 10월 23일 11시 24분&quot; |
| 날짜 | 날짜 문자열을 ZunkedDateTime 개체(ISO 8601 형식)로 변환합니다. | date(&quot;2019년 10월 23일 11시 24분&quot;) | &quot;2019-10-23T11:24:00+00:00&quot; |
| date_part | 날짜의 부분을 검색합니다. 다음 구성 요소 값이 지원됩니다. <br><br>&quot;year&quot;<br>&quot;<br>&quot;yyyy&quot;<br><br>&quot;yyyy<br>&quot;<br>&quot;yyy&quot;q<br><br>&quot;yyy&quot;q<br>&quot;<br>&quot;cq&quot;<br><br>&quot;cq&quot;<br>&quot;cumuld&quot;alk&quot;<br>&quot;ejy&quot;y&quot;y&quot;day&quot;y&quot;y&quot;y&quot;y&quot;day&quot;<br><br>&quot;<br>&quot;<br>y&quot;ev&quot;y&quot;eyyy&quot;<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>00000000000000000000000000000000000000000000000000000000000000000000000000000 4&quot;4&quot;&quot;hh12&quot;cuts&quot;minute&quot;minutes&quot;mymi&quot;emoth&quot;n&quot;second&quot;&quot;second&quot;&quot;&quot;sighters&quot;s&quot;&quot;s&quot;s&quot;milleconds&quot;ms. | date_part(date(&quot;2019-10-17 11:55:12&quot;), &quot;MM&quot;) | 10 |
| set_date_part | 지정된 날짜의 구성 요소를 대체합니다. 다음 구성 요소가 허용됩니다. <br><br>&quot;year&quot;<br>&quot;<br>yyyy&quot;<br><br>&quot;yyy<br>&quot;<br>&quot;yyy<br><br>&quot;<br>s&quot;<br>&quot;m&quot;<br><br><br>&quot;<br><br>&quot;dd&quot;<br>&quot;<br>&quot;<br><br>&quot;chour&quot;hh&quot;cultly&quot;<br><br>&quot;cmi&quot;n&quot;&quot;n&quot;second&quot;&quot;&quot;&quot;&quot;s&quot; | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time /<br>make_timestamp | 부품으로부터 날짜를 만듭니다. | make_date_time(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| current_timestamp | 현재 타임스탬프를 반환합니다. | current_timestamp() | 1571850624571 |
| current_date | 시간 구성 요소가 없는 현재 날짜를 반환합니다. | current_date() | &quot;2019년 11월 18일&quot; |