---
keywords: Experience Platform;인기 주제;XDM;XDM 시스템;XDM 개별 프로필;XDM 경험 이벤트;XDM 경험 이벤트;experienceEvent;experience eventExperience 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마;문제 해결;FAQ;FAQ;유니온 스키마;유니온 프로필;유니온 프로필;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: XDM 시스템 문제 해결 안내서
description: 일반적인 API 오류를 해결하는 단계를 포함하여 XDM(Experience Data Model)에 대해 자주 묻는 질문에 대한 답변을 찾아보십시오.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '2074'
ht-degree: 0%

---

# XDM 시스템 문제 해결 안내서

이 문서에서는 다음에 대한 FAQ에 대한 답변을 제공합니다 [!DNL Experience Data Model] 일반적인 오류에 대한 문제 해결 안내서를 포함하여 Adobe Experience Platform의 XDM(XDM) 및 XDM 시스템 기타 플랫폼 서비스와 관련된 질문 및 문제 해결은 다음을 참조하십시오. [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** 는 고객 경험 관리를 위한 표준화된 스키마를 정의하는 오픈 소스 사양입니다. 다음에 대한 방법론 [!DNL Experience Platform] 이(가) 빌드되었습니다. **XDM 시스템**, 운영 [!DNL Experience Data Model] 에서 사용할 스키마 [!DNL Platform] 서비스. 다음 **[!DNL Schema Registry]** 는 사용자 인터페이스와 RESTful API를 제공하여 **[!DNL Schema Library]** 다음 범위 내 [!DNL Experience Platform]. 다음을 참조하십시오. [XDM 설명서](home.md) 추가 정보.

## FAQ

다음은 XDM 시스템 및 사용 방법에 대한 FAQ 목록입니다. [!DNL Schema Registry] API.

### 스키마에 필드를 추가하려면 어떻게 합니까?

스키마 필드 그룹을 사용하여 스키마에 필드를 추가할 수 있습니다. 각 필드 그룹은 하나 이상의 클래스와 호환되므로 해당 호환 클래스 중 하나를 구현하는 모든 스키마에서 필드 그룹을 사용할 수 있습니다. Adobe Experience Platform은 여러 업계 필드 그룹에 고유한 사전 정의된 필드를 제공하지만 API 또는 사용자 인터페이스를 사용하여 사용자 정의 필드 그룹을 만들어 스키마에 고유한 필드를 추가할 수 있습니다.

에서 필드 그룹을 만드는 방법에 대한 자세한 내용은 [!DNL Schema Registry] API에서 다음을 참조하십시오. [필드 그룹 끝점 안내서](api/field-groups.md#create). UI를 사용 중인 경우 다음을 참조하십시오. [스키마 편집기 튜토리얼](./tutorials/create-schema-ui.md).

### 필드 그룹과 데이터 유형에 가장 적합한 용도는 무엇입니까?

[필드 그룹](./schema/composition.md#field-group) 는 스키마에서 하나 이상의 필드를 정의하는 구성 요소입니다. 필드 그룹은 필드가 스키마의 계층 구조에 표시되는 방식을 적용하므로 포함되는 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 클래스에서 식별되는 특정 클래스와만 호환됩니다. `meta:intendedToExtend` 특성.

[데이터 유형](./schema/composition.md#data-type) 는 스키마에 하나 이상의 필드를 제공할 수도 있습니다. 그러나 필드 그룹과 달리 데이터 유형은 특정 클래스에 제한되지 않습니다. 이렇게 하면 데이터 형식이 잠재적으로 다른 클래스를 사용하는 여러 스키마에서 재사용 가능한 일반적인 데이터 구조를 설명하는 보다 유연한 옵션이 됩니다.

### 스키마에 대한 고유 ID는 무엇입니까?

모두 [!DNL Schema Registry] 리소스(스키마, 필드 그룹, 데이터 유형, 클래스)에는 참조 및 조회 목적으로 고유 ID로 작동하는 URI가 있습니다. API에서 스키마를 볼 때 최상위 수준에서 찾을 수 있습니다 `$id` 및 `meta:altId` 속성.

자세한 내용은 [리소스 식별](api/getting-started.md#resource-identification) 의 섹션 [!DNL Schema Registry] API 안내서.

### 스키마가 언제 변경 내용 중단을 방지하기 시작합니까?

데이터 세트 만들기에 사용된 적이 없거나 에서 사용할 수 있도록 설정된 적이 없는 한 스키마에 호환될 수 있습니다 [[!DNL Real-Time Customer Profile]](../profile/home.md). 데이터 세트 생성에 스키마를 사용하거나 [!DNL Real-Time Customer Profile], 의 규칙 [스키마 진화](schema/composition.md#evolution) 시스템에 의해 엄격히 시행되다.

### 긴 필드 유형의 최대 크기는 얼마입니까?

Long 필드 형식은 최대 크기가 53(+1)비트인 정수로 -9007199254740992비트와 9007199254740992 사이의 잠재적 범위를 제공합니다. 이는 JSON의 JavaScript 구현이 긴 정수를 나타내는 방법의 제한 때문입니다.

필드 유형에 대한 자세한 내용은 [XDM 필드 유형 제약 조건](./schema/field-constraints.md).

### 스키마에 대한 ID를 정의하려면 어떻게 해야 합니까?

위치 [!DNL Experience Platform]: id는 해석되는 데이터의 소스에 관계없이 주체(일반적으로 개인)를 식별하는 데 사용됩니다. 키 필드를 &quot;ID&quot;로 표시하여 스키마에 정의됩니다. ID에 일반적으로 사용되는 필드에는 이메일 주소, 전화 번호, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM ID 및 기타 고유 ID 필드.

필드는 API 또는 사용자 인터페이스를 사용하여 ID로 표시할 수 있습니다.

#### API에서 ID 정의

API에서 ID는 ID 설명자를 만들어 설정합니다. ID 설명자는 스키마의 특정 속성이 고유 식별자라는 신호를 보냅니다.

ID 설명자는 /descriptors 끝점에 대한 POST 요청으로 만들어집니다. 성공하면 HTTP 상태 201(생성됨) 및 새 설명자의 세부 정보가 포함된 응답 개체를 받게 됩니다.

API에서 ID 설명자를 만드는 방법에 대한 자세한 내용은 [설명자](api/descriptors.md) 의 섹션 [!DNL Schema Registry] 개발자 안내서.

#### UI에서 ID 정의

스키마 편집기에서 스키마를 연 상태에서 **[!UICONTROL 구조]** id로 표시할 편집기의 섹션입니다. 아래 **[!UICONTROL 필드 속성]** 오른쪽에서 **[!UICONTROL 신원]** 확인란.

UI에서 ID를 관리하는 방법에 대한 자세한 내용은 [id 필드 정의](./tutorials/create-schema-ui.md#identity-field) 섹션에 자세히 설명되어 있습니다.

### 내 스키마에 기본 ID가 필요합니까?

스키마에 0이나 그 중 하나가 있을 수 있으므로 기본 ID는 선택 사항입니다. 그러나 스키마에에서 사용할 수 있도록 설정하려면 스키마에 기본 ID가 있어야 합니다. [!DNL Real-Time Customer Profile]. 다음을 참조하십시오. [신원](./tutorials/create-schema-ui.md#identity-field) 자세한 내용은 스키마 편집기 튜토리얼의 섹션을 참조하십시오.

### 에서 사용할 스키마를 활성화하려면 어떻게 합니까 [!DNL Real-Time Customer Profile]?

스키마는에서 사용할 수 있도록 설정되었습니다. [[!DNL Real-Time Customer Profile]](../profile/home.md) 에서 &quot;union&quot; 태그를 추가하여 `meta:immutableTags` 스키마의 속성입니다. 사용할 스키마 활성화 [!DNL Profile] API 또는 사용자 인터페이스를 사용하여 수행할 수 있습니다.

#### 기존 스키마 활성화 [!DNL Profile] api 사용

스키마를 업데이트하고 를 추가하기 위해 PATCH 요청 `meta:immutableTags` attribute를 &quot;union&quot; 값을 포함하는 배열로 지정합니다. 업데이트가 성공하면 이제 유니온 태그가 포함된 업데이트된 스키마가 응답에 표시됩니다.

API를 사용하여에서 사용할 스키마를 활성화하는 방법에 대한 자세한 정보 [!DNL Real-Time Customer Profile], 다음을 참조하십시오. [합집합](./api/unions.md) 문서 [!DNL Schema Registry] 개발자 안내서.

#### 기존 스키마 활성화 [!DNL Profile] UI 사용

위치 [!DNL Experience Platform], 선택 **[!UICONTROL 스키마]** 왼쪽 탐색에서 스키마 목록에서 활성화하고자 하는 스키마 이름을 선택합니다. 그런 다음 아래의 편집기 오른쪽에서 **[!UICONTROL 스키마 속성]**, 선택 **[!UICONTROL 프로필]** 켜십시오.


자세한 내용은 다음 섹션 을 참조하십시오 [실시간 고객 프로필에 사용](./tutorials/create-schema-ui.md#profile) 다음에서 [!UICONTROL 스키마 편집기] 튜토리얼.

### 유니온 스키마를 직접 편집할 수 있습니까?

유니온 스키마는 읽기 전용이며 시스템에 의해 자동으로 생성됩니다. 직접 편집할 수는 없습니다. 유니온 스키마는 특정 클래스를 구현하는 스키마에 &quot;유니온&quot; 태그가 추가되면 해당 클래스에 대해 생성됩니다.

XDM의 유니온에 대한 자세한 내용은 [합집합](./api/unions.md) 의 섹션 [!DNL Schema Registry] API 안내서.

### 데이터를 스키마로 수집하려면 데이터 파일의 형식을 어떻게 지정해야 합니까?

[!DNL Experience Platform] 다음 중 하나의 데이터 파일을 허용합니다. [!DNL Parquet] 또는 JSON 형식이어야 합니다. 이러한 파일의 내용은 데이터 세트에서 참조하는 스키마를 준수해야 합니다. 데이터 파일 수집을 위한 모범 사례에 대한 자세한 내용은 [일괄 처리 수집 개요](../ingestion/home.md).

## 오류 및 문제 해결

다음은 를 사용하여 작업할 때 발생할 수 있는 오류 메시지 목록입니다 [!DNL Schema Registry] API.

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
>검색되는 리소스 유형에 따라 이 오류는 다음 중 하나를 사용할 수 있습니다 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


API에서 조회 경로를 구성하는 방법에 대한 자세한 내용은 [컨테이너](./api/getting-started.md#container) 및 [리소스 식별](api/getting-started.md#resource-identification) 의 섹션 [!DNL Schema Registry] 개발자 안내서.

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

IMS 조직에서 정의한 리소스는 다른 업계 및 공급업체 리소스와의 충돌을 방지하기 위해 테넌트 ID 아래에 해당 필드의 네임스페이스를 지정해야 합니다. 표준 필드 그룹을 사용하여 스키마를 작성할 때 이러한 필드 그룹의 구조 내에 추가하는 모든 사용자 정의 필드는 테넌트 ID에서도 네임스페이스가 지정되어야 합니다.

>[!NOTE]
>
>네임스페이스 오류의 특정 특성에 따라 이 오류는 다음 중 하나를 사용할 수 있습니다 `type` 다른 메시지 세부 정보와 함께 URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


XDM 리소스에 대한 적절한 데이터 구조의 자세한 예는 스키마 레지스트리 API 안내서에서 확인할 수 있습니다.

* [사용자 정의 클래스 만들기](./api/classes.md#create)
* [사용자 정의 필드 그룹 만들기](./api/field-groups.md#create)
* [사용자 지정 데이터 유형 만들기](./api/data-types.md#create)

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

의 GET 요청 [!DNL Schema Registry] API에 필요 `Accept` 응답 형식을 지정하는 방법을 시스템에서 결정하기 위한 헤더. 이 오류는 필요한 경우 발생합니다 `Accept` 헤더가 잘못되었거나 누락되었습니다.

사용 중인 엔드포인트에 따라 `detailed-message` 유효한 속성을 나타냅니다. `Accept` 헤더는 성공적인 응답을 위한 것으로 표시되어야 합니다. 다음을 올바르게 입력했는지 확인합니다. `Accept` 다시 시도하기 전에 만들려는 API 요청과 호환되는 헤더입니다.

>[!NOTE]
>
>사용 중인 끝점에 따라 이 오류는 다음 중 하나를 사용할 수 있습니다 `type` URI:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


다른 API 요청에 대해 호환되는 Accept 헤더 목록은 의 해당 섹션을 참조하십시오. [스키마 레지스트리 개발자 안내서](./api/overview.md).

### [!DNL Real-Time Customer Profile] 오류

다음 오류 메시지는 의 스키마 활성화와 관련된 작업과 관련됩니다. [!DNL Real-Time Customer Profile]. 다음을 참조하십시오. [합집합](./api/unions.md) 의 섹션 [!DNL Schema Registry] API 안내서 를 참조하십시오.

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

이 오류 메시지는에 대한 스키마를 활성화하려고 할 때 표시됩니다 [!DNL Profile] 속성 중 하나에는 참조 id 설명자가 없는 관계 설명자가 포함됩니다. 이 오류를 해결하려면 해당 스키마 필드에 참조 ID 설명자를 추가하십시오.

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

에서 사용할 관계 설명자가 포함된 스키마를 활성화하려면 [!DNL Profile]: 소스 필드의 네임스페이스와 참조 필드의 기본 네임스페이스가 동일해야 합니다. 이 오류 메시지는 참조 ID 설명자에 대해 일치하지 않는 네임스페이스가 포함된 스키마를 활성화하려고 할 때 표시됩니다.

다음을 확인합니다. `xdm:namespace` 참조 스키마의 id 필드 값이 `xdm:identityNamespace` 이 문제를 해결하기 위한 소스 필드의 참조 id 설명자에 있는 속성입니다.

표준 ID 네임스페이스 코드 목록은 의 섹션을 참조하십시오. [표준 네임스페이스](../identity-service/namespaces.md) id 네임스페이스 개요에서 참조하십시오.

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

프로필에 대한 스키마를 활성화하기 전에 먼저 [기본 ID 설명자 만들기](./api/descriptors.md#create) 스키마에 대해 또는 기본 id에서 작동할 id 맵 필드를 포함합니다.

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
