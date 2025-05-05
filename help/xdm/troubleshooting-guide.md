---
keywords: Experience Platform;인기 주제;XDM;XDM 시스템;XDM 개별 프로필;XDM 경험 이벤트;XDM 경험 이벤트;experienceEvent;experience eventExperience 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마;문제 해결;FAQ;FAQ;유니온 스키마;유니온 프로필;유니온 프로필;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: XDM 시스템 문제 해결 안내서
description: 일반적인 API 오류를 해결하는 단계를 포함하여 XDM(Experience Data Model)에 대해 자주 묻는 질문에 대한 답변을 찾아보십시오.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2348'
ht-degree: 0%

---

# XDM 시스템 문제 해결 안내서

이 문서에서는 일반적인 오류에 대한 문제 해결 안내서를 포함하여 Adobe Experience Platform의 [!DNL Experience Data Model]&#x200B;(XDM) 및 XDM 시스템에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 다른 Experience Platform 서비스와 관련된 질문 및 문제 해결은 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

**[!DNL Experience Data Model] (XDM)**&#x200B;은(는) 고객 경험 관리를 위한 표준화된 스키마를 정의하는 오픈 소스 사양입니다. [!DNL Experience Platform]이(가) 빌드된 방법론인 **XDM 시스템**&#x200B;은(는) [!DNL Experience Platform] 서비스에서 사용할 [!DNL Experience Data Model] 스키마를 운영합니다. **[!DNL Schema Registry]**&#x200B;은(는) [!DNL Experience Platform] 내에서 **[!DNL Schema Library]**&#x200B;에 액세스할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 자세한 내용은 [XDM 설명서](home.md)를 참조하세요.

## FAQ

다음은 XDM 시스템 및 [!DNL Schema Registry] API 사용에 대한 FAQ 응답 목록입니다.

## 스키마 기본 사항

이 섹션에서는 XDM 시스템의 스키마 구조, 필드 사용 및 식별에 대한 기본적인 질문에 대한 답변을 찾을 수 있습니다.

### 스키마에 필드를 추가하려면 어떻게 합니까?

스키마 필드 그룹을 사용하여 스키마에 필드를 추가할 수 있습니다. 각 필드 그룹은 하나 이상의 클래스와 호환되므로 해당 호환 클래스 중 하나를 구현하는 모든 스키마에서 필드 그룹을 사용할 수 있습니다. Adobe Experience Platform은 여러 업계 필드 그룹에 고유한 사전 정의된 필드를 제공하지만 API 또는 사용자 인터페이스를 사용하여 사용자 정의 필드 그룹을 만들어 스키마에 고유한 필드를 추가할 수 있습니다.

[!DNL Schema Registry] API에서 필드 그룹을 만드는 방법에 대한 자세한 내용은 [필드 그룹 끝점 안내서](api/field-groups.md#create)를 참조하십시오. UI를 사용하는 경우 [스키마 편집기 자습서](./tutorials/create-schema-ui.md)를 참조하십시오.

### 필드 그룹과 데이터 유형에 가장 적합한 용도는 무엇입니까?

[필드 그룹](./schema/composition.md#field-group)은(는) 스키마에 하나 이상의 필드를 정의하는 구성 요소입니다. 필드 그룹은 필드가 스키마의 계층 구조에 표시되는 방식을 적용하므로 포함되는 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 `meta:intendedToExtend` 특성으로 식별되는 특정 클래스와만 호환됩니다.

[데이터 형식](./schema/composition.md#data-type)은 스키마에 하나 이상의 필드를 제공할 수도 있습니다. 그러나 필드 그룹과 달리 데이터 유형은 특정 클래스에 제한되지 않습니다. 이렇게 하면 데이터 형식이 잠재적으로 다른 클래스를 사용하는 여러 스키마에서 재사용 가능한 일반적인 데이터 구조를 설명하는 보다 유연한 옵션이 됩니다.

### 스키마에 대한 고유 ID는 무엇입니까?

모든 [!DNL Schema Registry] 리소스(스키마, 필드 그룹, 데이터 형식, 클래스)에는 참조 및 조회 목적으로 고유 ID로 작동하는 URI가 있습니다. API에서 스키마를 볼 때 최상위 `$id` 및 `meta:altId` 특성에서 찾을 수 있습니다.

자세한 내용은 [!DNL Schema Registry] API 안내서의 [리소스 식별](api/getting-started.md#resource-identification) 섹션을 참조하십시오.

### 긴 필드 유형의 최대 크기는 얼마입니까?

Long 필드 형식은 최대 크기가 53(+1)비트인 정수로 -9007199254740992비트와 9007199254740992 사이의 잠재적 범위를 제공합니다. 이는 JSON의 JavaScript 구현이 긴 정수를 나타내는 방법의 제한 때문입니다.

필드 형식에 대한 자세한 내용은 [XDM 필드 형식 제약 조건](./schema/field-constraints.md)에 대한 문서를 참조하십시오.

### meta:AltId란?

`meta:altId`은(는) 스키마의 고유 식별자입니다. `meta:altId`은(는) API 호출에 사용할 사용하기 쉬운 참조 ID를 제공합니다. 이 ID는 JSON URI 형식처럼 사용될 때마다 인코딩/디코딩될 필요가 없습니다.
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### 맵 데이터 유형에 대한 사용 제한 사항은 무엇입니까?

XDM에서는 이 데이터 유형의 사용에 대해 다음과 같은 제한 사항을 적용합니다.

- 맵 유형은 유형 개체여야 합니다.
- 맵 유형에는 속성이 정의되지 않아야 합니다(즉, &quot;빈&quot; 개체를 정의함).
- 맵 유형에는 맵 내에 배치할 수 있는 값을 설명하는 additionalProperties.type 필드가 문자열 또는 정수로 포함되어야 합니다.
- 다중 엔티티 세그먼테이션은 맵 키를 기준으로만 정의할 수 있으며 값을 기준으로 정의할 수는 없습니다.
- 계정 대상자에 대해서는 맵이 지원되지 않습니다.

자세한 내용은 [맵 개체에 대한 사용 제한](./ui/fields/map.md#restrictions)을 참조하세요.

>[!NOTE]
>
>다중 수준 맵 또는 맵 맵은 지원되지 않습니다.

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## 스키마 Identity Management

이 섹션에서는 스키마 내에서 ID를 정의하고 관리하는 것과 관련된 일반적인 질문에 대한 답변을 제공합니다.

### 스키마에 대한 ID를 정의하려면 어떻게 해야 합니까?

[!DNL Experience Platform]에서 ID는 해석되는 데이터의 소스와 관계없이 주체(일반적으로 개별 사용자)를 식별하는 데 사용됩니다. 키 필드를 &quot;ID&quot;로 표시하여 스키마에 정의됩니다. ID에 일반적으로 사용되는 필드에는 전자 메일 주소, 전화 번호, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM ID 및 기타 고유 ID 필드가 포함됩니다.

필드는 API 또는 사용자 인터페이스를 사용하여 ID로 표시할 수 있습니다.

### API에서 ID 정의

API에서 ID는 ID 설명자를 만들어 설정합니다. ID 설명자는 스키마의 특정 속성이 고유 식별자라는 신호를 보냅니다.

ID 설명자는 /descriptors 끝점에 대한 POST 요청으로 만들어집니다. 성공하면 HTTP 상태 201(생성됨) 및 새 설명자의 세부 정보가 포함된 응답 개체를 받게 됩니다.

API에서 ID 설명자를 만드는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [설명자](api/descriptors.md) 섹션에 있는 문서를 참조하십시오.

### UI에서 ID 정의

스키마 편집기에서 스키마를 연 상태에서 ID로 표시할 편집기의 **[!UICONTROL 구조]** 섹션에서 필드를 선택합니다. 오른쪽의 **[!UICONTROL 필드 속성]**&#x200B;에서 **[!UICONTROL ID]** 확인란을 선택합니다.

UI에서 ID를 관리하는 방법에 대한 자세한 내용은 스키마 편집기 자습서에서 [ID 필드 정의](./tutorials/create-schema-ui.md#identity-field) 섹션을 참조하십시오.

### 내 스키마에 기본 ID가 필요합니까?

스키마에 0이나 그 중 하나가 있을 수 있으므로 기본 ID는 선택 사항입니다. 그러나 [!DNL Real-Time Customer Profile]에서 스키마를 사용하려면 스키마에 기본 ID가 있어야 합니다. 자세한 내용은 스키마 편집기 자습서의 [id](./tutorials/create-schema-ui.md#identity-field) 섹션을 참조하십시오.

## 스키마 프로필 지원

이 섹션에서는 실시간 고객 프로필에 사용할 스키마를 활성화하는 방법에 대한 지침을 제공합니다.

### [!DNL Real-Time Customer Profile]에서 사용할 스키마를 활성화하려면 어떻게 해야 합니까?

스키마는 스키마의 `meta:immutableTags` 특성 내에 &quot;유니온&quot; 태그를 추가하여 [[!DNL Real-Time Customer Profile]](../profile/home.md)에서 사용할 수 있도록 설정되었습니다. API 또는 사용자 인터페이스를 사용하여 [!DNL Profile]에 사용할 스키마를 활성화할 수 있습니다.

### API를 사용하여 [!DNL Profile]에 대한 기존 스키마 사용

스키마를 업데이트하고 `meta:immutableTags` 특성을 &quot;union&quot; 값을 포함하는 배열로 추가하려면 PATCH을 요청하십시오. 업데이트가 성공하면 이제 유니온 태그가 포함된 업데이트된 스키마가 응답에 표시됩니다.

API를 사용하여 [!DNL Real-Time Customer Profile]에서 사용할 스키마를 활성화하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [유니온](./api/unions.md) 문서를 참조하십시오.

### UI를 사용하여 [!DNL Profile]에 대한 기존 스키마 활성화

[!DNL Experience Platform]의 왼쪽 탐색에서 **[!UICONTROL 스키마]**&#x200B;를 선택하고 스키마 목록에서 활성화하려는 스키마 이름을 선택합니다. 그런 다음 편집기 오른쪽의 **[!UICONTROL 스키마 속성]**&#x200B;에서 **[!UICONTROL 프로필]**&#x200B;을 선택하여 켜십시오.

자세한 내용은 [!UICONTROL 스키마 편집기] 자습서에서 [실시간 고객 프로필에서 사용](./tutorials/create-schema-ui.md#profile)에 대한 섹션을 참조하십시오.

### Adobe Analytics 데이터를 소스로 가져오면 자동으로 생성된 스키마가 프로필에 대해 활성화됩니까?

실시간 고객 프로필에 대해 스키마가 자동으로 활성화되지 않습니다. 프로필에 대해 활성화된 스키마를 기준으로 프로필에 대한 데이터 세트를 명시적으로 활성화해야 합니다. 실시간 고객 프로필에서 사용할 데이터 세트를 활성화하는 데 필요한 [단계 및 요구 사항](../catalog/datasets/user-guide.md#enable-profile)에 대해 알아보려면 설명서를 참조하십시오.

### 프로필 활성화 스키마를 삭제할 수 있습니까?

실시간 고객 프로필에 대해 활성화된 스키마는 삭제할 수 없습니다. 프로필에 대해 스키마를 활성화하면 비활성화하거나 삭제할 수 없으며 스키마에서 필드를 제거할 수 없습니다. 따라서 프로필에 대해 활성화하기 전에 스키마 구성을 신중하게 계획하고 확인하는 것이 중요합니다. 그러나 프로필 지원 데이터 세트를 삭제할 수 있습니다. 정보를 찾을 수 있는 위치: <https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

프로필 사용 스키마를 더 이상 사용하지 않으려면 **사용하지 않음** 또는 **비활성**&#x200B;을 포함하도록 스키마 이름을 바꾸는 것이 좋습니다.

## 스키마 수정 및 제한 사항

이 섹션에서는 스키마 수정 규칙 및 변경 내용 손상 방지에 대한 설명을 제공합니다.

### 스키마가 언제 변경 내용 중단을 방지하기 시작합니까?

데이터 집합을 만드는 데 사용된 적이 없거나 [[!DNL Real-Time Customer Profile]](../profile/home.md)에서 사용할 수 있도록 설정된 적이 없는 한 스키마에 변경 내용을 적용할 수 있습니다. 데이터 집합 만들기에 스키마를 사용하거나 [!DNL Real-Time Customer Profile]에서 사용할 수 있도록 설정하면 [스키마 진화](schema/composition.md#evolution)의 규칙이 시스템에 의해 엄격하게 적용됩니다.

### 유니온 스키마를 직접 편집할 수 있습니까?

유니온 스키마는 읽기 전용이며 시스템에 의해 자동으로 생성됩니다. 직접 편집할 수는 없습니다. 유니온 스키마는 특정 클래스를 구현하는 스키마에 &quot;유니온&quot; 태그가 추가되면 해당 클래스에 대해 생성됩니다.

XDM의 유니온에 대한 자세한 내용은 [!DNL Schema Registry] API 안내서의 [유니온](./api/unions.md) 섹션을 참조하십시오.

### 데이터를 스키마로 수집하려면 데이터 파일의 형식을 어떻게 지정해야 합니까?

[!DNL Experience Platform]은(는) [!DNL Parquet] 또는 JSON 형식의 데이터 파일을 허용합니다. 이러한 파일의 내용은 데이터 세트에서 참조하는 스키마를 준수해야 합니다. 데이터 파일 수집 모범 사례에 대한 자세한 내용은 [일괄 처리 수집 개요](../ingestion/home.md)를 참조하십시오.

### 스키마를 읽기 전용 스키마로 변환하려면 어떻게 해야 합니까?

현재 스키마를 읽기 전용으로 변환할 수 없습니다.

## 오류 및 문제 해결

다음은 [!DNL Schema Registry] API로 작업할 때 발생할 수 있는 오류 메시지 목록입니다.

### 리소스를 찾을 수 없음

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

이 오류는 시스템이 특정 리소스를 찾을 수 없을 때 표시됩니다. 리소스가 삭제되었거나 API 호출의 경로가 잘못되었을 수 있습니다. API 호출에 대한 유효한 경로를 입력했는지 확인한 후 다시 시도하십시오. 리소스에 대한 올바른 ID를 입력했는지, 그리고 경로의 이름이 적절한 컨테이너(전역 또는 테넌트)와 올바르게 지정되었는지 확인할 수 있습니다.

>[!NOTE]
>
>검색 중인 리소스 유형에 따라 이 오류는 다음 `type`개의 URI를 사용할 수 있습니다.
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

API에서 조회 경로를 구성하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [컨테이너](./api/getting-started.md#container) 및 [리소스 식별](api/getting-started.md#resource-identification) 섹션을 참조하십시오.

### 제목이 고유하지 않음

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

이 오류 메시지는 다른 리소스에서 이미 사용 중인 제목으로 리소스를 만들려고 할 때 표시됩니다. 제목은 모든 리소스 유형에서 고유해야 합니다. 예를 들어 스키마에서 이미 사용 중인 제목을 사용하여 필드 그룹을 만들려고 하면 이 오류가 표시됩니다.

### 네임스페이스 유효성 검사 오류

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

이 오류 메시지는 네임스페이스가 잘못된 필드를 사용하여 리소스를 만들거나 잘못된 네임스페이스가 있는 필드를 기존 리소스에 추가하려고 할 때 표시됩니다.

조직에서 정의한 리소스는 다른 업계 및 공급업체 리소스와의 충돌을 방지하기 위해 테넌트 ID 아래에 해당 필드의 네임스페이스를 지정해야 합니다. 표준 필드 그룹을 사용하여 스키마를 작성할 때 이러한 필드 그룹의 구조 내에 추가하는 모든 사용자 정의 필드는 테넌트 ID에서도 네임스페이스가 지정되어야 합니다.

>[!NOTE]
>
>네임스페이스 오류의 특정 특성에 따라 이 오류는 다른 메시지 세부 정보와 함께 다음 `type`개의 URI를 사용할 수 있습니다.
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

XDM 리소스에 대한 적절한 데이터 구조의 자세한 예는 스키마 레지스트리 API 안내서에서 확인할 수 있습니다.

- [사용자 정의 클래스 만들기](./api/classes.md#create)
- [사용자 정의 필드 그룹 만들기](./api/field-groups.md#create)
- [사용자 지정 데이터 유형 만들기](./api/data-types.md#create)

### 잘못된 Accept 헤더

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

시스템에서 응답 형식을 지정하는 방법을 결정하려면 [!DNL Schema Registry] API의 GET 요청에 `Accept` 헤더가 필요합니다. 이 오류는 필수 `Accept` 헤더가 잘못되었거나 누락된 경우에 발생합니다.

사용 중인 끝점에 따라 `detailed-message` 속성은 성공적인 응답을 위해 올바른 `Accept` 헤더의 모양을 나타냅니다. 다시 시도하기 전에 만들려는 API 요청과 호환되는 `Accept` 헤더를 올바르게 입력했는지 확인하십시오.

>[!NOTE]
>
>사용 중인 끝점에 따라 이 오류는 다음 `type`개의 URI를 사용할 수 있습니다.
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

다른 API 요청에 대해 호환되는 Accept 헤더 목록은 [스키마 레지스트리 개발자 안내서](./api/overview.md)의 해당 섹션을 참조하십시오.

### [!DNL Real-Time Customer Profile]개 오류

다음 오류 메시지는 [!DNL Real-Time Customer Profile]에 대해 스키마를 사용하는 작업과 관련되어 있습니다. 자세한 내용은 [!DNL Schema Registry] API 안내서의 [유니온](./api/unions.md) 섹션을 참조하십시오.

#### 참조 ID 설명자가 있어야 합니다.

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

이 오류 메시지는 [!DNL Profile]에 대해 스키마를 사용하도록 설정하려고 할 때 해당 속성 중 하나에 참조 ID 설명자가 없는 관계 설명자가 포함되어 있을 때 표시됩니다. 이 오류를 해결하려면 해당 스키마 필드에 참조 ID 설명자를 추가하십시오.

#### 참조 ID 설명자 필드와 대상 스키마의 네임스페이스가 일치해야 함

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>이 오류의 경우 &quot;대상 스키마&quot;는 관계의 참조 스키마를 참조합니다.

[!DNL Profile]에서 사용할 관계 설명자가 포함된 스키마를 활성화하려면 원본 필드의 네임스페이스와 참조 필드의 기본 네임스페이스가 같아야 합니다. 이 오류 메시지는 참조 ID 설명자에 대해 일치하지 않는 네임스페이스가 포함된 스키마를 활성화하려고 할 때 표시됩니다.

이 문제를 해결하려면 참조 스키마 ID 필드의 `xdm:namespace` 값이 소스 필드의 참조 ID 설명자에 있는 `xdm:identityNamespace` 속성의 값과 일치하는지 확인하십시오.

표준 ID 네임스페이스 코드 목록은 ID 네임스페이스 개요에서 [표준 네임스페이스](../identity-service/features/namespaces.md)에 대한 섹션을 참조하십시오.

#### 스키마에 identityMap 또는 기본 ID가 포함되어야 합니다.

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

프로필에 대한 스키마를 활성화하기 전에 먼저 스키마에 대한 [기본 ID 설명자를 만들거나](./api/descriptors.md#create)하거나 기본 ID에서 작동할 ID 맵 필드를 포함해야 합니다.

#### 호환되지 않는 데이터 형식을 병합할 수 없습니다.

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

동일한 클래스에 속하는 모든 프로필 사용 스키마가 함께 병합될 수 있어야 해당 클래스의 유니온 스키마를 구성할 수 있습니다. 이 오류는 다른 프로필 활성화 스키마에서 경로를 공유하고 데이터 유형이 원본과 다른 스키마에 필드를 추가하려고 할 때 나타납니다. 스키마가 둘 다 프로필을 사용할 수 있고 동일한 필드 경로를 포함하므로, 프로필은 유니온 스키마를 구성할 때 이 두 필드를 하나로 병합하려고 시도합니다. 서로 다른 데이터 유형은 함께 병합할 수 없으므로 병합 충돌로 간주되어 허용되지 않습니다.

이 문제를 해결하려면 필드에 대해 다른 이름을 선택하거나 고유하게 이름이 지정된 개체 아래에 중첩하여 유사한 필드가 있는 동일한 클래스의 다른 프로필 사용 스키마와 병합되지 않도록 합니다.
