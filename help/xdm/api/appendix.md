---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;호환성;호환성;호환성;호환성 모드;호환성 모드;필드 유형;필드 유형;
solution: Experience Platform
title: 스키마 레지스트리 API 안내서 부록
description: 이 문서에서는 스키마 레지스트리 API 작업과 관련된 추가 정보를 제공합니다.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 1%

---

# 스키마 레지스트리 API 안내서 부록

이 문서에서는 [!DNL Schema Registry] API.

## 쿼리 매개 변수 사용 {#query}

다음 [!DNL Schema Registry] 은 리소스를 나열할 때 쿼리 매개 변수를 페이지 및 필터 결과로 사용할 수 있도록 지원합니다.

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(`&`).

### 페이징 {#paging}

페이징의 가장 일반적인 쿼리 매개 변수는 다음과 같습니다.

| 매개 변수 | 설명 |
| --- | --- |
| `orderby` | 특정 속성별로 결과를 정렬합니다. 예: `orderby=title` 제목별로 결과를 오름차순으로 정렬합니다(A-Z). 추가 `-` 매개 변수 값 앞에(`orderby=-title`)은 제목별로 항목을 내림차순으로 정렬합니다(Z-A). |
| `limit` | 와 함께 사용하는 경우 `orderby` 매개 변수, `limit` 지정된 요청에 대해 반환해야 하는 최대 항목 수를 제한합니다. 이 매개 변수는 `orderby` 매개 변수가 있습니다.<br><br>다음 `limit` 매개 변수는 양의 정수(다음 사이)를 지정합니다 `0` 및 `500`) *힌트* 을 반환해야 하는 최대 항목 수에 대한 값입니다. 예, `limit=5` 목록에서 5개의 리소스만 반환합니다. 그러나 이 가치는 엄격히 존중되지는 않는다. 실제 응답 크기는 Target의 신뢰 작업을 제공할 필요가 있기 때문에 제한될 수 있습니다 `start` 매개 변수(제공된 경우)입니다. |
| `start` | 와 함께 사용하는 경우 `orderby` 매개 변수, `start` 항목의 하위 설정 목록을 시작할 위치를 지정합니다. 이 매개 변수는 `orderby` 매개 변수가 있습니다. 이 값은 `_page.next` 목록 응답의 속성입니다. 다음 결과 페이지에 액세스하는 데 사용됩니다. 만약 `_page.next` 값이 null이면 사용할 수 있는 추가 페이지가 없습니다.<br><br>일반적으로 이 매개 변수는 결과의 첫 번째 페이지를 가져오기 위해 생략됩니다. 그 후에 `start` 기본 정렬 속성의 최대값으로 설정해야 합니다. `orderby` 이전 페이지에서 받은 필드. 그런 다음 API 응답이 기본 정렬 속성이 있는 항목부터 시작하는 항목을 반환합니다. `orderby` (오름차순) 또는 지정된 값보다 엄격히 작거나, (내림차순) 엄격하게 지정합니다.<br><br>예를 들어 `orderby` 매개 변수가 `orderby=name,firstname`, `start` 매개 변수에는 `name` 속성을 사용합니다. 이 경우 &quot;Miller&quot;라는 이름 바로 뒤에 있는 리소스의 다음 20개 항목을 표시하려면 다음을 사용합니다. `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### 필터링 {#filtering}

를 사용하여 결과를 필터링할 수 있습니다 `property` 매개 변수 - 검색된 리소스 내에서 지정된 JSON 속성에 대해 특정 연산자를 적용하는 데 사용됩니다. 지원되는 연산자는 다음과 같습니다.

| 연산자 | 설명 | 예 |
| --- | --- | --- |
| `==` | 속성이 제공된 값과 같은지 여부를 기준으로 필터링합니다. | `property=title==test` |
| `!=` | 속성이 제공된 값과 같지 않은지 필터링합니다. | `property=title!=test` |
| `<` | 속성이 제공된 값보다 작은지 여부에 따라 필터링합니다. | `property=version<5` |
| `>` | 속성이 제공된 값보다 커야 하는지 여부를 기준으로 필터링합니다. | `property=version>5` |
| `<=` | 속성이 제공된 값보다 작거나 같은지의 여부를 기준으로 필터링합니다. | `property=version<=5` |
| `>=` | 속성이 제공된 값보다 크거나 같은지 여부를 기준으로 필터링합니다. | `property=version>=5` |
| `~` | 속성이 제공된 정규 표현식과 일치하는지 여부를 기준으로 필터링합니다. | `property=title~test$` |
| (None) | 속성 이름만 지정하면 속성이 있는 항목만 반환됩니다. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>를 사용할 수 있습니다 `property` 호환 클래스 별로 스키마 필드 그룹을 필터링하는 매개 변수입니다. 예, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 와 호환되는 필드 그룹만 반환합니다. [!DNL XDM Individual Profile] 클래스 이름을 지정합니다.

## 호환성 모드 {#compatibility}

[!DNL Experience Data Model] (XDM)은 디지털 경험의 상호 운용성, 표현성 및 기능을 향상시키기 위해 Adobe에 의해 문서화된 사양입니다. Adobe은 [GitHub에서 소스 프로젝트 열기](https://github.com/adobe/xdm/). 이러한 정의는 XDM 스키마를 정의하는 문법으로 JSON-LD(연결된 데이터에 대한 JavaScript 개체 표기법)와 JSON 스키마를 사용하여 XDM 표준 표기법으로 작성됩니다.

공용 리포지토리에서 공식 XDM 정의를 보면 표준 XDM이 Adobe Experience Platform에 표시되는 정의와 다르다는 것을 알 수 있습니다. 보고 있는 내용 [!DNL Experience Platform] 는 호환성 모드라고 하며, 표준 XDM과 표준 XDM에서 사용하는 방법 간의 간단한 매핑을 제공합니다 [!DNL Platform].

### 호환성 모드 작동 방식

호환성 모드 를 사용하면 XDM JSON-LD 모델이 표준 XDM 내에서 값을 변경하여 기존 데이터 인프라와 함께 작업할 수 있고 동시에 의미 체계를 유지할 수 있습니다. 이 템플릿은 중첩된 JSON 구조를 사용하여 트리와 같은 형식으로 스키마를 표시합니다.

표준 XDM과 호환성 모드 간의 주요 차이점은 필드 이름에 대한 &quot;xdm:&quot; 접두사를 제거하는 것입니다.

다음은 표준 XDM과 호환성 모드 모두에서 생일 관련 필드(&quot;설명&quot; 속성이 제거됨)를 보여주는 나란히 비교입니다. 호환성 모드 필드에는 &quot;meta:xdmField&quot; 및 &quot;meta:xdmType&quot; 속성에 있는 XDM 필드 및 해당 데이터 유형에 대한 참조가 포함되어 있습니다.

<table style="table-layout:auto">
  <th>표준 XDM</th>
  <th>호환성 모드</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate": { "title": "생년월일", "type": "string", "format": "date" }, "xdm:birthDayAndMonth": { "title": "생년월일", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]" }, "xdm:birthYear": { "title": "출생 연도", "type": "integer", "minimum": 1, "최대값": 32767 }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "naignDate": { "title": "생년월일", "type": "string", "format": "date", "meta:xdmField": "xdm:birthDate", "meta:xdmType": "date" }, "firstDayAndMonth": { "title": "생년월일", "type": "string", "pattern": "[0-1][0-9]-[0-9][0-9]", "meta:xdmField": "xdm:birthDayAndMonth", "meta:xdmType": "string" }, "naignYear": { "title": "출생 연도", "type": "integer", "minimum": 1, "최대값": 32767, "meta:xdmField": "xdm:birthYear", "meta:xdmType": "short" }
      </pre>
  </td>
  </tr>
</table>

### 호환성 모드가 필요한 이유는 무엇입니까?

Adobe Experience Platform은 각각 고유한 기술적 과제와 제한 사항(예: 특정 기술이 특수 문자를 처리하는 방법)을 가진 여러 솔루션 및 서비스와 작동하도록 설계되었습니다. 이러한 제한 사항을 극복하기 위해 호환성 모드가 개발되었습니다.

가장 많이 [!DNL Experience Platform] 서비스 포함 [!DNL Catalog], [!DNL Data Lake], 및 [!DNL Real-Time Customer Profile] 사용 [!DNL Compatibility Mode] 표준 XDM 대신 사용됩니다. 다음 [!DNL Schema Registry] API는 도 사용합니다 [!DNL Compatibility Mode]및 이 문서의 예는 모두 [!DNL Compatibility Mode].

표준 XDM과 매핑 방식이 에서 작동하는 방식 간에 매핑이 발생함을 파악하는 것이 유용합니다 [!DNL Experience Platform]그러나 사용자의 사용에 영향을 주지 않습니다 [!DNL Platform] 서비스.

개방형 소스 프로젝트를 사용할 수 있지만, [!DNL Schema Registry]를 설정하는 것이 좋습니다.
