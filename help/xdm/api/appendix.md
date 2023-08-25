---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;호환성;호환성;호환성 모드;호환성 모드;필드 유형;필드 유형;
solution: Experience Platform
title: 스키마 레지스트리 API 안내서 부록
description: 이 문서에서는 스키마 레지스트리 API 작업과 관련된 추가 정보를 제공합니다.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 0%

---

# 스키마 레지스트리 API 안내서 부록

이 문서에서는 작업 관련 추가 정보를 제공합니다 [!DNL Schema Registry] API.

## 쿼리 매개 변수 사용 {#query}

다음 [!DNL Schema Registry] 는 리소스를 나열할 때 결과를 페이지 및 필터링하는 데 쿼리 매개 변수를 사용할 수 있도록 지원합니다.

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(`&`).

### 페이징 {#paging}

페이징에 가장 일반적인 쿼리 매개 변수는 다음과 같습니다.

| 매개변수 | 설명 |
| --- | --- |
| `orderby` | 특정 속성별로 결과를 정렬합니다. 예: `orderby=title` 제목별로 오름차순(A-Z)으로 결과를 정렬합니다. 추가 `-` 매개 변수 값 (`orderby=-title`)는 내림차순(Z-A)으로 제목별로 항목을 정렬합니다. |
| `limit` | 와 함께 사용할 경우 `orderby` 매개 변수, `limit` 은(는) 주어진 요청에 대해 반환해야 하는 최대 항목 수를 제한합니다. 이 매개 변수는 `orderby` 매개 변수가 있습니다.<br><br>다음 `limit` 매개 변수는 양의 정수(다음 사이)를 지정합니다. `0` 및 `500`) as a *힌트* 반환해야 하는 최대 항목 수에 대해 설명합니다. 예를 들어, `limit=5` 목록에서 5개의 리소스만 반환합니다. 그러나 이 값은 엄격히 적용되지 않습니다. 실제 응답 크기는 동작의 신뢰할 수 있는 동작을 제공할 필요성에 의해 제약됨에 따라 더 작거나 더 클 수 있다 `start` 매개 변수(제공된 경우). |
| `start` | 와 함께 사용할 경우 `orderby` 매개 변수, `start` 하위 집합 항목 목록의 시작 위치를 지정합니다. 이 매개 변수는 `orderby` 매개 변수가 있습니다. 이 값은 다음에서 얻을 수 있습니다. `_page.next` 목록 응답의 속성이며, 결과의 다음 페이지에 액세스하는 데 사용됩니다. 다음과 같은 경우 `_page.next` 값이 null이면 사용할 수 있는 추가 페이지가 없습니다.<br><br>일반적으로 이 매개 변수는 결과의 첫 페이지를 가져오기 위해 생략됩니다. 그 이후에, `start` 은(는) 의 기본 정렬 속성의 최대값으로 설정해야 합니다. `orderby` 이전 페이지에서 필드 수신됨. 그런 다음 API 응답은 기본 정렬 속성이 있는 항목으로 시작하는 항목을 반환합니다 `orderby` 지정된 값보다 엄격히 큼(오름차순) 또는 엄격하게 작음(내림차순).<br><br>예를 들어 `orderby` 매개 변수가 로 설정되어 있습니다. `orderby=name,firstname`, `start` 매개 변수에는 다음 값이 포함됩니다. `name` 속성. 이 경우 &quot;Miller&quot; 이름의 바로 뒤에 있는 리소스의 다음 20개 항목을 표시하려면 다음을 사용합니다. `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### 필터링 {#filtering}

다음을 사용하여 결과를 필터링할 수 있습니다. `property` 매개 변수 : 검색된 리소스 내에서 지정된 JSON 속성에 대해 특정 연산자를 적용하는 데 사용됩니다. 지원되는 연산자는 다음과 같습니다.

| 연산자 | 설명 | 예 |
| --- | --- | --- |
| `==` | 속성이 제공된 값과 동일한지 여부를 기준으로 필터링합니다. | `property=title==test` |
| `!=` | 속성이 제공된 값과 같지 않은지 여부로 필터링합니다. | `property=title!=test` |
| `<` | 속성이 제공된 값보다 작은지 여부를 기준으로 필터링합니다. | `property=version<5` |
| `>` | 속성이 제공된 값보다 큰지 여부를 기준으로 필터링합니다. | `property=version>5` |
| `<=` | 속성이 제공된 값보다 작거나 같은지 여부를 기준으로 필터링합니다. | `property=version<=5` |
| `>=` | 속성이 제공된 값보다 크거나 같은지 여부를 기준으로 필터링합니다. | `property=version>=5` |
| (None) | 속성 이름만 입력하면 속성이 있는 항목만 반환됩니다. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>다음을 사용할 수 있습니다. `property` 호환 가능한 클래스별로 스키마 필드 그룹을 필터링하기 위한 매개 변수입니다. 예를 들어, `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 는 호환되는 필드 그룹만 반환합니다. [!DNL XDM Individual Profile] 클래스.

## 호환성 모드 {#compatibility}

[!DNL Experience Data Model] (XDM)은 디지털 경험의 상호 운용성, 표현력 및 기능을 개선하기 위해 Adobe을 기반으로 하는, 공개적으로 문서화된 사양입니다. Adobe은에서 소스 코드 및 공식 XDM 정의를 유지 관리합니다 [gitHub의 오픈 소스 프로젝트](https://github.com/adobe/xdm/). 이러한 정의는 XDM 스키마를 정의하기 위한 문법으로 JSON-LD(연결된 데이터에 대한 JavaScript 개체 표기법) 및 JSON 스키마를 사용하여 XDM 표준 표기법으로 작성됩니다.

공개 저장소의 공식 XDM 정의를 보면 표준 XDM이 Adobe Experience Platform에 표시되는 것과 다르다는 것을 알 수 있습니다. 에서 보고 있는 항목 [!DNL Experience Platform] 호환 모드라고 하며 표준 XDM과 내에서 사용되는 방식 간에 간단한 매핑을 제공합니다 [!DNL Platform].

### 호환성 모드 작동 방식

호환성 모드를 사용하면 의미 체계를 동일하게 유지하면서 표준 XDM 내에서 값을 변경하여 XDM JSON-LD 모델을 기존 데이터 인프라에서 작업할 수 있습니다. 중첩된 JSON 구조를 사용하여 스키마를 트리와 유사한 형식으로 표시합니다.

표준 XDM과 호환성 모드 간의 주요 차이점은 필드 이름에 대한 &quot;xdm:&quot; 접두사의 제거입니다.

다음은 표준 XDM과 호환성 모드 모두에서 생일 관련 필드(&quot;설명&quot; 속성이 제거된)를 보여 주는 나란히 비교입니다. 호환성 모드 필드에는 &quot;meta:xdmField&quot; 및 &quot;meta:xdmType&quot; 속성의 XDM 필드 및 해당 데이터 유형에 대한 참조가 포함됩니다.

<table style="table-layout:auto">
  <th>표준 XDM</th>
  <th>호환성 모드</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate": { "title": "Birth Date", "type": "string", "format": "date" }, "xdm:birthDayAndMonth": { "title": "Birth Date", "type": "string", "pattern": "[0-1][0-9]-[0-9]" }, "xdm:birthYear": { "title": "Birth year", "type": "integer", "minimum": 1, "maximum": 32767 } }
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{ "birthDate": { "title": "생년월일", "type": "string", "format": "date", "meta:xdmField": "xdm:birthDate", "meta:xdmType": "date" }, "birthDayAndMonth": { "title": "생년월일", "type": "string", "pattern": "[0-1][0-9]-[0-9]", "meta:xdmField": "xdm:birthDayAndMonth", "meta:xdmType": "string" }, "birthYear": { "title": "Birth year", "type" 최소": 1, "maximum": 32767, "meta:xdmField": "xdm:birthYear", "meta:xdmType": "short" } }
      </pre>
  </td>
  </tr>
</table>

### 호환성 모드가 필요한 이유는 무엇입니까?

Adobe Experience Platform은 여러 솔루션 및 서비스와 함께 작동하도록 설계되었으며, 각 솔루션에는 고유한 기술적 과제와 제한 사항(예: 특정 기술이 특수 문자를 처리하는 방법)이 있습니다. 이러한 한계를 극복하기 위하여 호환성 모드(Compatibility Mode)를 개발하였다.

가장 [!DNL Experience Platform] 다음을 포함한 서비스 [!DNL Catalog], [!DNL Data Lake], 및 [!DNL Real-Time Customer Profile] 사용 [!DNL Compatibility Mode] 표준 XDM 대신 다음 [!DNL Schema Registry] API는 을 사용하기도 합니다. [!DNL Compatibility Mode]및 이 문서의 예는 모두 다음을 사용하여 표시됩니다. [!DNL Compatibility Mode].

매핑은 표준 XDM과 이 XDM이 작동하는 방식 간에 발생한다는 것을 아는 것이 좋습니다 [!DNL Experience Platform], 그러나 사용 방법에 영향을 주지 않음 [!DNL Platform] 서비스.

오픈 소스 프로젝트는 사용자가 사용할 수 있지만, 를 통해 리소스와 상호 작용할 때는 [!DNL Schema Registry], 이 문서의 API 예는 알고 따라야 하는 모범 사례를 제공합니다.
