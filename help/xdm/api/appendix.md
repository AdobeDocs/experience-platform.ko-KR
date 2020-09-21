---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;compatibility;Compatibility;compatibility mode;Compatibility mode;field type;field types;
solution: Experience Platform
title: 스키마 레지스트리 개발자 부록
description: 이 문서에서는 스키마 레지스트리 API 작업과 관련된 보충 정보를 제공합니다.
topic: developer guide
translation-type: tm+mt
source-git-commit: 42d3bed14c5f926892467baeeea09ee7a140ebdc
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# 부록

이 문서에서는 [!DNL Schema Registry] API 작업과 관련된 추가 정보를 제공합니다.

## 호환성 모드

[!DNL Experience Data Model] (XDM)은 디지털 경험의 상호 운용성, 풍부한 표현 능력 및 성능을 개선하기 위해 Adobe을 기반으로 공개적으로 문서화된 사양입니다. Adobe은 GitHub의 [오픈 소스 프로젝트에서 소스 코드와 공식 XDM 정의를 유지 관리합니다](https://github.com/adobe/xdm/). 이러한 정의는 XDM 스키마를 정의하는 문법으로 JSON-LD(JavaScript Object Notation for Linked Data) 및 JSON 스키마를 사용하여 XDM 표준 표기법으로 작성됩니다.

공용 저장소에서 공식 XDM 정의를 살펴보면 표준 XDM이 Adobe Experience Platform에 있는 내용과 다른 것을 확인할 수 있습니다. 호환성 모드 [!DNL Experience Platform] 에서 볼 수 있는 것은 표준 XDM과 표준 XDM을 사용하는 방법 간의 간단한 매핑을 제공하는 [!DNL Platform]것입니다.

### 호환성 모드 작동 방식

호환성 모드를 사용하면 XDM JSON-LD 모델이 표준 XDM 내의 값을 변경하여 기존 데이터 인프라와 연동하고 의미론도 동일하게 유지할 수 있습니다. 중첩된 JSON 구조를 사용하여 트리 형식의 스키마를 표시합니다.

표준 XDM과 호환성 모드 간의 주요 차이점은 필드 이름에 대한 &quot;xdm:&quot; 접두어가 제거된다는 것입니다.

다음은 표준 XDM과 호환성 모드 모두에서 생일 관련 필드(&quot;description&quot; 속성이 제거됨)를 보여주는 나란히 비교입니다. 호환성 모드 필드에는 &quot;meta:xdmField&quot; 및 &quot;meta:xdmType&quot; 속성에 XDM 필드 및 해당 데이터 유형에 대한 참조가 포함되어 있습니다.

<table>
  <th>표준 XDM</th>
  <th>호환성 모드</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        { "xdm:birthDate":{ "title":"생년월일", "유형":"string", "format":"date", }, "xdm:birthDayAndMonth":{ "title":"생년월일", "유형":"string", "pattern":"[0-1][0-9]-[0-9][0-9]", }, "xdm:birthYear":{ "title":"생년월일", "유형":"integer", "minimum":1, "최대":32767 }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
        { "birthDate":{ "title":"생년월일", "유형":"string", "format":"date", "meta:xdmField":"xdm:birthDate", "meta:xdmType":"date" }, "birthDayAndMonth":{ "title":"생년월일", "유형":"string", "pattern":"[0-1][0-9]-[0-9][0-9]", "meta:xdmField":"xdm:birthDayAndMonth", "meta:xdmType":"string" }, "birthYear":{ "title":"생년월일", "유형":"integer", "minimum":1, "최대":32767, "meta:xdmField":"xdm:birthYear", "meta:xdmType":"short" }
      </pre>
  </td>
  </tr>
</table>

### 호환성 모드가 필요한 이유는 무엇입니까?

Adobe Experience Platform은 기술적 문제와 제한 사항을 가진 다양한 솔루션 및 서비스를 사용하도록 설계되었습니다(예: 특정 기술이 특수 문자를 처리하는 방법). 이러한 제한 사항을 극복하기 위해 호환성 모드가 개발되었습니다.

표준 XDM [!DNL Experience Platform] 을 [!DNL Catalog]대신하여, [!DNL Data Lake]및 [!DNL Real-time Customer Profile] [!DNL Compatibility Mode] 사용하는 대부분의 서비스 API는 [!DNL Schema Registry] 또한 사용하고 이 문서의 [!DNL Compatibility Mode]예는 모두 를 사용하여 표시됩니다 [!DNL Compatibility Mode].

표준 XDM과 표준 XDM의 운영 방식 사이에서 매핑이 이루어지는 것은 [!DNL Experience Platform]유용하지만 [!DNL Platform] 서비스 사용에 영향을 미치지 않습니다.

오픈 소스 프로젝트를 사용할 수 있지만, 를 통해 리소스와 상호 작용하는 경우 이 문서의 API 예는 알고 따라야 하는 우수 사례를 [!DNL Schema Registry]제공합니다.