---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;스키마 레지스트리;호환성;호환성;호환성 모드;호환성 모드;필드 유형;필드 유형;필드 유형;
solution: Experience Platform
title: 스키마 레지스트리 API 안내서 부록
description: 이 문서에서는 스키마 레지스트리 API 작업과 관련된 추가 정보를 제공합니다.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# 스키마 레지스트리 API 안내서 부록

이 문서에서는 [!DNL Schema Registry] API 작업과 관련된 추가 정보를 제공합니다.

## 쿼리 매개 변수 {#query} 사용

[!DNL Schema Registry]은 리소스를 나열할 때 쿼리 매개 변수를 페이지에 사용하고 결과를 필터링하는 기능을 지원합니다.

>[!NOTE]
>
>여러 쿼리 매개 변수를 결합할 때는 앰퍼샌드(`&`)로 구분해야 합니다.

### {#paging} 호출

페이징 시 가장 일반적인 쿼리 매개 변수는 다음과 같습니다.

| 매개 변수 | 설명 |
| --- | --- |
| `start` | 나열된 결과를 시작할 위치를 지정합니다. 이 값은 목록 응답의 `_page.next` 속성에서 얻을 수 있으며, 다음 결과 페이지에 액세스하는 데 사용할 수 있습니다. `_page.next` 값이 null이면 사용할 수 있는 추가 페이지가 없습니다. |
| `limit` | 반환된 리소스 수를 제한합니다. 예:`limit=5`은 5개의 리소스 목록을 반환합니다. |
| `orderby` | 특정 속성별로 결과를 정렬합니다. 예:`orderby=title`은(는) 결과를 오름차순으로 정렬합니다(A-Z). 매개 변수 값(`orderby=-title`) 앞에 `-`을 추가하면 제목이 내림차순(Z-A)으로 항목을 정렬합니다. |

### 필터링 {#filtering}

검색된 리소스 내의 지정된 JSON 속성에 대해 특정 연산자를 적용하는 데 사용되는 `property` 매개 변수를 사용하여 결과를 필터링할 수 있습니다. 지원되는 연산자는 다음과 같습니다.

| 연산자 | 설명 | 예 |
| --- | --- | --- |
| `==` | 속성이 제공된 값과 같은지 여부를 기준으로 필터링합니다. | `property=title==test` |
| `!=` | 속성이 제공된 값과 동일하지 않은지 여부를 기준으로 필터링합니다. | `property=title!=test` |
| `<` | 속성이 제공된 값보다 작은지 여부를 기준으로 필터링합니다. | `property=version<5` |
| `>` | 속성이 제공된 값보다 큰지 여부를 기준으로 필터링합니다. | `property=version>5` |
| `<=` | 속성이 제공된 값보다 작거나 같은지의 여부에 따라 필터링합니다. | `property=version<=5` |
| `>=` | 속성이 제공된 값보다 크거나 같은지의 여부를 필터링합니다. | `property=version>=5` |
| `~` | 속성이 제공된 정규 표현식과 일치하는지 여부를 기준으로 필터링합니다. | `property=title~test$` |
| (None) | 속성 이름만 입력하면 속성이 있는 항목만 반환됩니다. | `property=title` |

>[!TIP]
>
>`property` 매개 변수를 사용하여 호환되는 클래스로 믹스를 필터링할 수 있습니다. 예를 들어 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile`은 [!DNL XDM Individual Profile] 클래스와 호환되는 혼합만 반환합니다.

## 호환성 모드

[!DNL Experience Data Model] (XDM)은 Adobe을 통해 디지털 경험의 상호 운용성, 풍부한 표현 능력 및 성능을 향상시킴으로써 공개적으로 문서화된 사양입니다. Adobe은 GitHub](https://github.com/adobe/xdm/)의 오픈 소스 프로젝트에 소스 코드와 공식 XDM 정의를 유지 관리합니다. [ 이러한 정의는 XDM 표준 표기법으로 작성되며, JSON-LD(연결된 데이터에 대한 JavaScript 개체 표기법) 및 JSON 스키마를 XDM 스키마를 정의하는 문법으로 사용합니다.

공용 저장소에서 공식 XDM 정의를 볼 때 표준 XDM이 Adobe Experience Platform에 있는 정의와 다른 것을 확인할 수 있습니다. [!DNL Experience Platform]에서 표시되는 내용을 호환성 모드라고 하며 표준 XDM과 [!DNL Platform] 내에서 사용하는 방법 간의 간단한 매핑을 제공합니다.

### 호환성 모드 작동 방식

호환성 모드를 사용하면 XDM JSON-LD 모델이 표준 XDM 내에서 값을 변경하여 기존 데이터 인프라와 함께 작업할 수 있을 뿐만 아니라 의미 체계를 동일하게 유지할 수 있습니다. 중첩된 JSON 구조를 사용하여 트리와 같은 형식으로 스키마를 표시합니다.

표준 XDM과 호환성 모드 간의 주요 차이점은 필드 이름에 대한 &quot;xdm:&quot; 접두어가 제거된다는 점입니다.

다음은 표준 XDM 및 호환성 모드 모두에서 생일 관련 필드(&quot;description&quot; 속성이 제거됨)를 보여주는 간단한 비교를 나란히 나타낸 것입니다. 호환성 모드 필드에는 &quot;meta:xdmField&quot; 및 &quot;meta:xdmType&quot; 속성에 XDM 필드 및 해당 데이터 유형에 대한 참조가 포함되어 있습니다.

<table>
  <th>표준 XDM</th>
  <th>호환성 모드</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate":{
              "title":"생년월일",
              "type":"string",
              "format":"date",
          },
          "xdm:birthDayAndMonth":{
              "title":"생년월일",
              "type":"string",
              "패턴":"[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear":{
              "title":'탄생년'
              "type":"integer",
              "최소":1,
              "maximum":32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "생년월일":{
              "title":"생년월일",
              "type":"string",
              "format":"date",
              "meta:xdmField":"xdm:birthDate",
              "meta:xdmType":"date"
          },
          "birthDayAndMonth":{
              "title":"생년월일",
              "type":"string",
              "패턴":"[0-1][0-9]-[0-9][0-9]",
              "meta:xdmField":"xdm:birthDayAndMonth",
              "meta:xdmType":"string"
          },
          "탄생년":{
              "title":'탄생년'
              "type":"integer",
              "최소":1,
              "maximum":32767년,
              "meta:xdmField":"xdm:birthYear",
              "meta:xdmType":"short"
        }
      </pre>
  </td>
  </tr>
</table>

### 호환성 모드가 필요한 이유는 무엇입니까?

Adobe Experience Platform은 여러 솔루션과 서비스를 사용하여 각각 기술적 문제와 제한 사항(예: 특정 기술이 특수 문자를 처리하는 방법)을 가지고 작업하도록 설계되었습니다. 이러한 제한 사항을 극복하기 위해 호환성 모드가 개발되었습니다.

[!DNL Catalog], [!DNL Data Lake] 및 [!DNL Real-time Customer Profile]을 비롯한 대부분의 [!DNL Experience Platform] 서비스는 표준 XDM 대신 [!DNL Compatibility Mode]을 사용합니다. [!DNL Schema Registry] API는 [!DNL Compatibility Mode]도 사용하며 이 문서의 예제는 모두 [!DNL Compatibility Mode]를 사용하여 표시됩니다.

매핑은 표준 XDM과 [!DNL Experience Platform]에서 관리하는 방법 간에 수행되지만 [!DNL Platform] 서비스 사용에 영향을 미치지 않습니다.

오픈 소스 프로젝트를 사용할 수 있지만, [!DNL Schema Registry]을 통해 리소스와 상호 작용하는 경우 이 문서의 API 예는 알고 따라야 하는 최상의 방법을 제공합니다.
