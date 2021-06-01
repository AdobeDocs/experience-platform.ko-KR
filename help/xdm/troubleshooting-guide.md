---
keywords: Experience Platform;홈;인기 항목;XDM;XDM 시스템;XDM 개별 프로필;XDM ExperienceEvent;XDM 경험 이벤트;경험 이벤트;경험 이벤트;XDM 경험 이벤트;XDM 경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;스키마;문제 해결;FAQ;통합 스키마;FAQ 프로필;프로필;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;
solution: Experience Platform
title: XDM 시스템 문제 해결 안내서
description: 일반적인 API 오류를 해결하는 단계를 포함하여 XDM(Experience Data Model)에 대해 자주 묻는 질문에 대한 답변을 찾습니다.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 415938f6f3aeec342774b73d1ae5f2dc0e27349c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---

# XDM 시스템 문제 해결 안내서

이 문서에서는 일반적인 오류에 대한 문제 해결 가이드를 포함하여 Adobe Experience Platform의 [!DNL Experience Data Model](XDM) 및 XDM 시스템에 대해 자주 묻는 질문에 대한 답변을 제공합니다. 다른 플랫폼 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

**[!DNL Experience Data Model](XDM)** 은 고객 경험 관리를 위해 표준화된 스키마를 정의하는 오픈 소스 사양입니다. [!DNL Experience Platform]이(가) 빌드된 방법론인 **XDM 시스템**&#x200B;은(는) [!DNL Platform] 서비스에서 사용하기 위해 [!DNL Experience Data Model] 스키마를 운영하고 있습니다. **[!DNL Schema Registry]**&#x200B;은 [!DNL Experience Platform] 내에서 **[!DNL Schema Library]**&#x200B;에 액세스할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 자세한 내용은 [XDM 설명서](home.md)를 참조하십시오.

## FAQ

다음은 XDM 시스템 및 [!DNL Schema Registry] API 사용에 대해 자주 묻는 질문에 대한 답변 목록입니다.

### 스키마에 필드를 추가하려면 어떻게 해야 합니까?

스키마 필드 그룹을 사용하여 스키마에 필드를 추가할 수 있습니다. 각 필드 그룹은 하나 이상의 클래스와 호환되므로 호환되는 클래스 중 하나를 구현하는 스키마에서 필드 그룹을 사용할 수 있습니다. Adobe Experience Platform은 자체 사전 정의된 필드를 포함하는 여러 업계 필드 그룹을 제공하지만 API 또는 사용자 인터페이스를 사용하여 사용자 지정 필드 그룹을 만들어 스키마에 고유한 필드를 추가할 수 있습니다.

[!DNL Schema Registry] API에서 필드 그룹을 만드는 방법에 대한 자세한 내용은 [필드 그룹 끝점 안내서](api/field-groups.md#create)를 참조하십시오. UI를 사용하는 경우 [스키마 편집기 자습서](./tutorials/create-schema-ui.md)를 참조하십시오.

### 필드 그룹과 데이터 유형에 가장 적합한 사용 방법은 무엇입니까?

[필드 ](./schema/composition.md#field-group) 그룹은 스키마에 필드를 하나 이상 정의하는 구성 요소입니다. 필드 그룹은 해당 필드가 스키마 계층에 표시되는 방식을 적용하므로 포함된 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 `meta:intendedToExtend` 속성으로 식별되는 특정 클래스와 호환됩니다.

[데이터 유형](./schema/composition.md#data-type) 은 스키마에 대해 하나 이상의 필드를 제공할 수도 있습니다. 그러나 필드 그룹과 달리 데이터 형식은 특정 클래스에 한정되지 않습니다. 따라서 데이터 형식을 보다 유연하게 사용하여 여러 스키마에서 다시 사용할 수 있는 공통 데이터 구조를 설명하거나 다른 클래스를 사용할 수 있습니다.

### 스키마의 고유 ID는 무엇입니까?

모든 [!DNL Schema Registry] 리소스(스키마, 필드 그룹, 데이터 유형, 클래스)에는 참조 및 조회 목적으로 고유한 ID로 작동하는 URI가 있습니다. API에서 스키마를 볼 때 최상위 `$id` 및 `meta:altId` 속성에 있습니다.

자세한 내용은 [!DNL Schema Registry] API 안내서의 [리소스 ID](api/getting-started.md#resource-identification) 섹션을 참조하십시오.

### 스키마는 언제 변경 내용을 중단하지 않습니까?

데이터 집합을 만들거나 [[!DNL Real-time Customer Profile]](../profile/home.md)에서 사용할 수 있도록 활성화한 적이 없는 한 스키마에 변경 사항을 적용할 수 있습니다. 데이터 집합 만들기에 스키마를 사용하거나 [!DNL Real-time Customer Profile]에 사용할 수 있도록 활성화하면 [스키마 진화](schema/composition.md#evolution)의 규칙이 시스템에 의해 엄격하게 적용됩니다.

### 긴 필드 유형의 최대 크기는 얼마입니까?

긴 필드 형식은 최대 크기가 53(+1)비트인 정수로, -9007199254740992과 9007199254740992 사이의 잠재적 범위를 제공합니다. 이는 JSON의 JavaScript 구현이 긴 정수를 나타내는 방법에 대한 제한 때문입니다.

필드 유형에 대한 자세한 내용은 [XDM 필드 유형 제약 조건](./schema/field-constraints.md)에 있는 문서를 참조하십시오.

### 스키마에 대한 ID를 정의하려면 어떻게 해야 합니까?

[!DNL Experience Platform]에서 ID는 해석되는 데이터의 소스와 관계없이 제목(일반적으로 개별 개인)을 식별하는 데 사용됩니다. 키 필드를 &quot;ID&quot;로 표시하여 스키마에 정의됩니다. ID에 일반적으로 사용되는 필드에는 이메일 주소, 전화번호, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM ID 및 기타 고유한 ID 필드가 포함됩니다.

필드는 API 또는 사용자 인터페이스를 사용하여 ID로 표시할 수 있습니다.

#### API에서 ID 정의

API에서 ID는 ID 설명자를 만들어 설정합니다. ID 설명자는 스키마에 대한 특정 속성이 고유한 식별자임을 나타냅니다.

ID 설명자는 /descriptors 엔드포인트에 대한 POST 요청에 의해 만들어집니다. 성공하면 HTTP 상태 201(생성됨) 및 새 설명자의 세부 정보가 포함된 응답 개체를 받게 됩니다.

API에서 ID 설명자를 만드는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [설명자](api/descriptors.md) 섹션에 있는 문서를 참조하십시오.

#### UI에서 ID 정의

스키마 편집기에서 스키마를 연 상태에서 ID로 표시할 편집기의 **[!UICONTROL 구조]** 섹션에서 필드를 선택합니다. 오른쪽의 **[!UICONTROL 필드 속성]**&#x200B;에서 **[!UICONTROL ID]** 확인란을 선택합니다.

UI에서 ID 관리에 대한 자세한 내용은 스키마 편집기 자습서에서 [ID 필드 정의](./tutorials/create-schema-ui.md#identity-field) 섹션의 섹션을 참조하십시오.

### 스키마에 기본 ID가 필요합니까?

기본 ID는 스키마에 0이나 하나가 있을 수 있으므로 선택 사항입니다. 그러나 [!DNL Real-time Customer Profile]에서 사용할 수 있도록 스키마를 활성화하려면 스키마에 기본 ID가 있어야 합니다. 자세한 내용은 스키마 편집기 자습서의 [identity](./tutorials/create-schema-ui.md#identity-field) 섹션을 참조하십시오.

### [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화하려면 어떻게 합니까?

스키마는 스키마의 `meta:immutableTags` 속성 내에 &quot;union&quot; 태그를 추가하여 [[!DNL Real-time Customer Profile]](../profile/home.md)에서 사용할 수 있도록 활성화됩니다. [!DNL Profile]에 사용할 스키마 활성화는 API 또는 사용자 인터페이스를 사용하여 수행할 수 있습니다.

#### API를 사용하여 [!DNL Profile]에 대한 기존 스키마 활성화

스키마를 업데이트하고 `meta:immutableTags` 속성을 &quot;union&quot; 값이 포함된 배열로 추가하도록 PATCH 요청을 만듭니다. 업데이트가 성공하면 응답에 이제 결합 태그가 포함된 업데이트된 스키마가 표시됩니다.

API를 사용하여 [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [union](./api/unions.md) 문서를 참조하십시오.

#### UI를 사용하여 [!DNL Profile]에 대한 기존 스키마 활성화

[!DNL Experience Platform]의 왼쪽 탐색에서 **[!UICONTROL 스키마]**&#x200B;를 선택하고 스키마 목록에서 활성화할 스키마의 이름을 선택합니다. 그런 다음 **[!UICONTROL 스키마 속성]** 아래의 편집기 오른쪽에서 **[!UICONTROL 프로필]**&#x200B;을 선택하여 켜십시오.


자세한 내용은 [!UICONTROL 스키마 편집기] 자습서의 [실시간 고객 프로필](./tutorials/create-schema-ui.md#profile)에서 사용하는 섹션을 참조하십시오.

### 결합 스키마를 직접 편집할 수 있습니까?

결합 스키마는 읽기 전용이며 시스템에 의해 자동으로 생성됩니다. 직접 편집할 수는 없습니다. 해당 클래스를 구현하는 스키마에 &quot;union&quot; 태그가 추가되면 특정 클래스에 대한 결합 스키마가 만들어집니다.

XDM의 조합에 대한 자세한 내용은 [!DNL Schema Registry] API 안내서의 [union](./api/unions.md) 섹션을 참조하십시오.

### 데이터를 스키마에 수집하기 위해 내 데이터 파일의 형식을 어떻게 지정해야 합니까?

[!DNL Experience Platform] 는 또는 JSON 형식 [!DNL Parquet] 으로 데이터 파일을 허용합니다. 이러한 파일의 컨텐츠는 데이터 집합에서 참조하는 스키마를 따라야 합니다. 데이터 파일 처리에 대한 우수 사례에 대한 자세한 내용은 [배치 수집 개요](../ingestion/home.md)를 참조하십시오.

## 오류 및 문제 해결

다음은 [!DNL Schema Registry] API를 사용하여 작업할 때 발생할 수 있는 오류 메시지 목록입니다.

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

시스템에서 특정 리소스를 찾을 수 없을 때 이 오류가 표시됩니다. 리소스가 삭제되었거나 API 호출의 경로가 잘못되었습니다. 다시 시도하기 전에 API 호출에 올바른 경로를 입력했는지 확인하십시오. 리소스에 대한 올바른 ID를 입력했는지 그리고 경로가 적절한 컨테이너(글로벌 또는 테넌트)와 올바르게 지정되었는지 확인할 수 있습니다.

>[!NOTE]
>
>검색할 리소스 유형에 따라 이 오류는 다음 `type` URI 중 하나를 사용할 수 있습니다.
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


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

이 오류 메시지는 다른 리소스에서 이미 사용하고 있는 제목과 함께 리소스를 만들려고 할 때 표시됩니다. 제목은 모든 리소스 유형에서 고유해야 합니다. 예를 들어 스키마에 이미 사용 중인 제목이 있는 필드 그룹을 만들려고 하면 이 오류가 표시됩니다.

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

이 오류 메시지는 잘못 지정된 필드가 있는 리소스를 만들거나 잘못된 네임스페이스 필드를 기존 리소스에 추가하려고 할 때 표시됩니다.

IMS 조직에서 정의한 리소스는 다른 업계 및 공급업체 리소스와 충돌을 방지하기 위해 테넌트 ID 아래에 해당 필드를 네임스페이스를 지정해야 합니다. 표준 필드 그룹을 사용하여 스키마를 작성할 때, 해당 필드 그룹의 구조 내에 추가하는 사용자 지정 필드도 테넌트 ID 아래에 지정해야 합니다.

>[!NOTE]
>
>네임스페이스 오류의 구체적인 특성에 따라 이 오류는 다른 메시지 세부 정보와 함께 다음 `type` URI를 사용할 수 있습니다.
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


XDM 리소스를 위한 적절한 데이터 구조에 대한 자세한 예는 스키마 레지스트리 API 안내서에서 확인할 수 있습니다.

* [사용자 지정 클래스 만들기](./api/classes.md#create)
* [사용자 지정 필드 그룹 만들기](./api/field-groups.md#create)
* [사용자 지정 데이터 유형 만들기](./api/data-types.md#create)

### 잘못된 헤더 수락

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

시스템이 응답의 형식을 지정하는 방법을 결정하려면 [!DNL Schema Registry] API의 GET 요청에 `Accept` 헤더가 필요합니다. 이 오류는 필수 `Accept` 헤더가 잘못되었거나 없을 때 발생합니다.

사용 중인 엔드포인트에 따라, `detailed-message` 속성은 유효한 `Accept` 헤더가 성공적인 응답을 위해 어떤 모습이어야 하는지를 나타냅니다. 다시 시도하기 전에 수행하려는 API 요청과 호환되는 `Accept` 헤더를 올바르게 입력했는지 확인하십시오.

>[!NOTE]
>
>사용 중인 엔드포인트에 따라 이 오류는 다음 `type` URI 중 하나를 사용할 수 있습니다.
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


다른 API 요청에 호환되는 Accept 헤더 목록은 [스키마 레지스트리 개발자 안내서](./api/overview.md)에서 해당 섹션을 참조하십시오.

### [!DNL Real-time Customer Profile] 오류

다음 오류 메시지는 [!DNL Real-time Customer Profile]에 대한 스키마 활성화와 관련된 작업과 연결됩니다. 자세한 내용은 [!DNL Schema Registry] API 안내서의 [union](./api/unions.md) 섹션을 참조하십시오.

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

이 오류 메시지는 [!DNL Profile]에 대한 스키마를 활성화하려고 할 때 표시되고 해당 속성 중 하나에 참조 ID 설명자가 없는 관계 설명자가 포함되어 있으면 표시됩니다. 이 오류를 해결하려면 해당 스키마 필드에 참조 ID 설명자를 추가합니다.

#### 참조 ID 설명자 필드 및 대상 스키마의 네임스페이스가 일치해야 합니다

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

[!DNL Profile]에 사용할 관계 설명자를 포함하는 스키마를 활성화하려면 소스 필드의 네임스페이스와 대상 필드의 기본 네임스페이스가 같아야 합니다. 이 오류 메시지는 참조 ID 설명자에 대해 일치하지 않는 네임스페이스가 포함된 스키마를 활성화하려고 할 때 표시됩니다. 대상 스키마의 ID 필드의 `xdm:namespace` 값이 소스 필드의 참조 ID 설명자에 있는 `xdm:identityNamespace` 속성 값과 일치하는지 확인합니다.

표준 ID 네임스페이스 코드 목록을 보려면 ID 네임스페이스 개요에서 [표준 네임스페이스](../identity-service/namespaces.md)의 섹션을 참조하십시오.

#### 스키마에는 identityMap 또는 기본 ID가 포함되어야 합니다

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

프로필에 대한 스키마를 활성화하기 전에 먼저 스키마에 대한 기본 ID 설명자](./api/descriptors.md#create)를 만들거나, 대신 기본 ID에서 사용할 ID 맵 필드를 포함해야 합니다.[