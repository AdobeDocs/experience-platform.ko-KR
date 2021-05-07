---
keywords: Experience Platform;홈;인기 항목;XDM;XDM 시스템;XDM 개별 프로필;XDM ExperienceEvent;XDM 경험 이벤트;경험 이벤트;경험 이벤트;경험 이벤트;XDM 경험 이벤트;경험 이벤트;XDM 경험 이벤트;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;데이터 모델;데이터 모델;데이터 모델 스키마;문제 해결;FAQ;faq;공용 스키마;UNION PROFILE;union profile
solution: Experience Platform
title: XDM 시스템 문제 해결 안내서
description: 이 문서에서는 Adobe Experience Platform의 경험 데이터 모델(XDM) 및 XDM 시스템에 대한 질문과 더불어 일반적인 오류에 대한 문제 해결 가이드를 제공합니다.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# XDM 시스템 문제 해결 가이드

이 문서에서는 Adobe Experience Platform의 [!DNL Experience Data Model](XDM) 및 XDM 시스템에 대한 질문과 더불어 일반적인 오류에 대한 문제 해결 가이드를 제공합니다. 다른 플랫폼 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 안내서](../landing/troubleshooting.md)를 참조하십시오.

**[!DNL Experience Data Model](XDM)** 은 고객 경험 관리를 위한 표준화된 스키마를 정의하는 오픈 소스 사양입니다. [!DNL Experience Platform]이(가) 빌드된 방법론인 **XDM 시스템**&#x200B;은(는) [!DNL Experience Data Model] 스키마를 [!DNL Platform] 서비스에 사용하여 작동시킵니다. **[!DNL Schema Registry]**&#x200B;은 [!DNL Experience Platform] 내의 **[!DNL Schema Library]**&#x200B;에 액세스할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 자세한 내용은 [XDM 설명서](home.md)를 참조하십시오.

## FAQ

다음은 XDM 시스템 및 [!DNL Schema Registry] API 사용에 대한 질문과 답변 목록입니다.

### 스키마에 필드를 추가하려면 어떻게 합니까?

스키마 필드 그룹을 사용하여 스키마에 필드를 추가할 수 있습니다. 각 필드 그룹은 하나 이상의 클래스와 호환되므로, 호환되는 클래스 중 하나를 구현하는 모든 스키마에서 필드 그룹을 사용할 수 있습니다. Adobe Experience Platform은 자체 사전 정의된 필드를 포함한 여러 개의 업계 필드 그룹을 제공하지만, API 또는 사용자 인터페이스를 사용하여 새 필드 그룹을 만들어 고유한 필드를 스키마에 추가할 수 있습니다.

[!DNL Schema Registry] API에서 새 필드 그룹을 만드는 방법에 대한 자세한 내용은 [필드 그룹 끝점 안내서](api/field-groups.md#create)를 참조하십시오. UI를 사용하는 경우 [스키마 편집기 자습서](./tutorials/create-schema-ui.md)를 참조하십시오.

### 필드 그룹과 데이터 유형에 대한 가장 좋은 용도는 무엇입니까?

[필드 ](./schema/composition.md#field-group) 그룹은 스키마에서 하나 이상의 필드를 정의하는 구성 요소입니다. 필드 그룹은 해당 필드가 스키마의 계층에서 표시되는 방식을 적용하므로 해당 필드가 포함된 모든 스키마에서 동일한 구조를 표시합니다. 필드 그룹은 `meta:intendedToExtend` 특성으로 식별되는 특정 클래스와만 호환됩니다.

[데이터 ](./schema/composition.md#data-type) 유형은 스키마에 대해 하나 이상의 필드를 제공할 수도 있습니다. 하지만 필드 그룹과 달리 데이터 유형은 특정 클래스로 제한되지 않습니다. 따라서 데이터 유형을 보다 유연하게 설명하여 서로 다른 클래스가 있는 여러 스키마에서 다시 사용할 수 있는 일반적인 데이터 구조를 설명합니다.

### 스키마에 대한 고유 ID는 무엇입니까?

모든 [!DNL Schema Registry] 리소스(스키마, 필드 그룹, 데이터 유형, 클래스)에는 참조 및 조회 목적으로 고유한 ID로 작동하는 URI가 있습니다. API에서 스키마를 볼 때 최상위 수준 `$id` 및 `meta:altId` 특성에서 찾을 수 있습니다.

자세한 내용은 [!DNL Schema Registry] API 개발자 안내서의 [리소스 식별](api/getting-started.md#resource-identification) 섹션을 참조하십시오.

### 스키마는 언제 변경 내용을 중단하지 못하도록 합니까?

데이터 세트 생성에 사용되지 않거나 [[!DNL Real-time Customer Profile]](../profile/home.md)에서 사용할 수 있는 경우 스키마를 변경할 수 있습니다. 스키마를 데이터 집합 만들기에서 사용하거나 [!DNL Real-time Customer Profile]에 사용할 수 있도록 활성화하면 [스키마 진행](schema/composition.md#evolution)의 규칙은 시스템에 의해 엄격히 적용됩니다.

### 긴 필드 유형의 최대 크기는 얼마입니까?

긴 필드 유형은 최대 크기가 53(+1) 비트인 정수로, -9007199254740992 및 9007199254740992 사이의 잠재적 범위를 제공합니다. 이는 JSON의 JavaScript 구현이 긴 정수를 나타내는 방법에 대한 제한 때문입니다.

필드 유형에 대한 자세한 내용은 [XDM 필드 유형 제한 조건](./schema/field-constraints.md)에 있는 문서를 참조하십시오.

### 스키마에 대한 ID를 어떻게 정의합니까?

[!DNL Experience Platform]에서 ID는 해석되는 데이터의 소스와 관계없이 주체(일반적으로 개인)를 식별하는 데 사용됩니다. 키 필드를 &quot;ID&quot;로 표시하여 스키마에 정의됩니다. ID에 일반적으로 사용되는 필드에는 이메일 주소, 전화 번호, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM ID 및 기타 고유한 ID 필드가 있습니다.

필드는 API 또는 사용자 인터페이스를 사용하여 ID로 표시할 수 있습니다.

#### API에서 ID 정의

API에서 ID 설명자를 만들어 ID를 설정합니다. ID 설명자는 스키마의 특정 속성이 고유 식별자임을 나타냅니다.

ID 설명자는 /descriptors 끝점에 대한 POST 요청에 의해 만들어집니다. 성공하면 HTTP 상태 201(만들어짐)과 새 설명자의 세부 정보가 포함된 응답 개체를 받게 됩니다.

API에서 ID 설명자를 만드는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 안내서의 [설명자](api/descriptors.md) 섹션에 있는 문서를 참조하십시오.

#### UI에서 ID 정의

스키마 편집기에서 스키마를 열고 ID로 표시하려는 편집기의 **[!UICONTROL Structure]** 섹션에서 필드를 선택합니다. 오른쪽의 **[!UICONTROL Field Properties]** 아래에서 **[!UICONTROL Identity]** 확인란을 선택합니다.

UI에서 ID 관리에 대한 자세한 내용은 스키마 편집기 자습서의 [ID 필드 정의](./tutorials/create-schema-ui.md#identity-field) 섹션에 있는 섹션을 참조하십시오.

### 스키마에 기본 ID가 필요합니까?

기본 ID는 선택 사항이며, 스키마에 0 또는 1이 있을 수 있습니다. 그러나 스키마를 [!DNL Real-time Customer Profile]에서 사용하도록 설정하려면 스키마에 기본 ID가 있어야 합니다. 자세한 내용은 스키마 편집기 자습서의 [identity](./tutorials/create-schema-ui.md#identity-field) 섹션을 참조하십시오.

### [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화하려면 어떻게 합니까?

스키마의 `meta:immutableTags` 속성에 있는 &quot;union&quot; 태그를 추가하여 [[!DNL Real-time Customer Profile]](../profile/home.md)에서 스키마를 사용할 수 있습니다. [!DNL Profile]에 사용할 스키마 활성화는 API 또는 사용자 인터페이스를 사용하여 수행할 수 있습니다.

#### API를 사용하여 [!DNL Profile]에 대한 기존 스키마 활성화

PATCH 요청을 수행하여 스키마를 업데이트하고 `meta:immutableTags` 속성을 값 &quot;union&quot;이 포함된 배열로 추가합니다. 업데이트가 성공하면 응답에 이제 union 태그가 포함된 업데이트된 스키마가 표시됩니다.

API를 사용하여 [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 안내서의 [union](./api/unions.md) 문서를 참조하십시오.

#### UI를 사용하여 [!DNL Profile]에 대한 기존 스키마 활성화

[!DNL Experience Platform]의 왼쪽 탐색 메뉴에서 **[!UICONTROL Schemas]**&#x200B;을 선택하고 스키마 목록에서 활성화할 스키마 이름을 선택합니다. 그런 다음 **[!UICONTROL Schema Properties]** 아래의 편집기의 오른쪽에서 **[!UICONTROL Profile]**&#x200B;을 선택하여 켜십시오.


자세한 내용은 [!UICONTROL Schema Editor] 자습서의 [실시간 고객 프로필](./tutorials/create-schema-ui.md#profile)에서 사용 섹션을 참조하십시오.

### 조합 스키마를 직접 편집할 수 있습니까?

결합 스키마는 읽기 전용이며 시스템에 의해 자동으로 생성됩니다. 직접 편집할 수는 없습니다. &quot;union&quot; 태그가 해당 클래스를 구현하는 스키마에 추가될 때 특정 클래스에 대해 공용 스키마가 생성됩니다.

XDM의 조합에 대한 자세한 내용은 [!DNL Schema Registry] API 개발자 안내서의 [union](./api/unions.md) 섹션을 참조하십시오.

### 데이터를 스키마로 인제스트하려면 내 데이터 파일의 형식을 어떻게 지정해야 합니까?

[!DNL Experience Platform] 데이터 파일은  [!DNL Parquet] 또는 JSON 형식으로 수락합니다. 이러한 파일의 내용은 데이터 세트에서 참조하는 스키마를 따라야 합니다. 데이터 파일 섭취에 대한 우수 사례에 대한 자세한 내용은 [일괄 처리 통합 개요](../ingestion/home.md)를 참조하십시오.

## 오류 및 문제 해결

다음은 [!DNL Schema Registry] API를 사용하여 작업할 때 발생할 수 있는 오류 메시지 목록입니다.

### 개체를 찾을 수 없음

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

시스템이 특정 리소스를 찾을 수 없을 때 이 오류가 표시됩니다. 리소스가 삭제되었거나 API 호출의 경로가 올바르지 않을 수 있습니다. 다시 시도하기 전에 API 호출에 유효한 경로를 입력했는지 확인하십시오. 리소스의 올바른 ID를 입력했으며 경로가 적절한 컨테이너(글로벌 또는 테넌트)와 올바르게 지정되었는지 확인할 수 있습니다.

API에서 조회 경로를 구성하는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 개발자 안내서의 [컨테이너](./api/getting-started.md#container) 및 [리소스 식별](api/getting-started.md#resource-identification) 섹션을 참조하십시오.

### 제목은 고유해야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

이 오류 메시지는 다른 리소스에서 이미 사용 중인 제목을 사용하여 리소스를 만들려고 하면 표시됩니다. 제목은 모든 리소스 유형에서 고유해야 합니다. 예를 들어 이미 스키마에서 사용 중인 제목과 함께 필드 그룹을 만들려고 하면 이 오류가 표시됩니다.

### 사용자 정의 필드는 최상위 필드를 사용해야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

이 오류 메시지는 잘못 지정된 필드가 있는 새 필드 그룹을 만들려고 하면 표시됩니다. IMS 조직에 의해 정의된 필드 그룹은 다른 업계 및 공급업체 리소스와 충돌을 방지하기 위해 해당 필드를 `TENANT_ID`으로 네임스페이스해야 합니다. 필드 그룹에 적합한 데이터 구조의 자세한 예는 [필드 그룹 끝점 안내서](./api/field-groups.md#create)에서 확인할 수 있습니다.


### [!DNL Real-time Customer Profile] 오류

다음 오류 메시지는 [!DNL Real-time Customer Profile]에 대한 스키마 활성화에 관련된 작업과 연관되어 있습니다. 자세한 내용은 [!DNL Schema Registry] API 개발자 안내서의 [union](./api/unions.md) 섹션을 참조하십시오.

#### 프로필 데이터 집합을 사용하려면 스키마가 유효해야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

이 오류 메시지는 [!DNL Real-time Customer Profile]에 대해 활성화되지 않은 스키마에 대해 프로필 데이터 세트를 활성화하려고 할 때 표시됩니다. 데이터 집합을 활성화하기 전에 스키마에 공용 태그가 포함되어 있는지 확인하십시오.

#### 참조 ID 설명자가 있어야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

이 오류 메시지는 [!DNL Profile]에 대한 스키마를 활성화하려고 시도하며 해당 속성 중 하나에 참조 ID 설명자 없이 관계 설명자가 들어 있을 때 표시됩니다. 해당 스키마 필드에 참조 ID 설명자를 추가하여 이 오류를 해결하십시오.

#### 참조 ID 설명자 필드 및 대상 스키마의 네임스페이스가 일치해야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

[!DNL Profile]에서 사용할 관계 설명자를 포함하는 스키마를 사용하려면 소스 필드의 네임스페이스와 대상 필드의 기본 네임스페이스가 동일해야 합니다. 이 오류 메시지는 참조 ID 설명자에 대해 일치하지 않는 네임스페이스를 포함하는 스키마를 활성화하려고 할 때 표시됩니다. 대상 스키마 ID 필드의 `xdm:namespace` 값이 소스 필드의 참조 ID 설명자에 있는 `xdm:identityNamespace` 속성 값과 일치하는지 확인합니다.

지원되는 ID 네임스페이스 코드 목록은 ID 네임스페이스 개요의 [표준 네임스페이스](../identity-service/namespaces.md)에 대한 섹션을 참조하십시오.

### 헤더 오류 허용

[!DNL Schema Registry] API의 대부분의 GET 요청은 시스템에서 응답의 형식 지정 방법을 결정하기 위해 수락 헤더가 필요합니다. 다음은 수락 헤더와 연관된 일반적인 오류 목록입니다. 서로 다른 API 요청에 대한 호환되는 수락 헤더 목록은 [스키마 레지스트리 개발자 안내서](api/getting-started.md)에서 해당 섹션을 참조하십시오.

#### 헤더 매개 변수 허용이 필요합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

이 오류 메시지는 API 요청에서 수락 헤더가 누락되면 표시됩니다. 다시 시도하기 전에 수락 헤더가 포함되어 있는지 확인합니다.

#### 알 수 없는 수락 미디어가 제공됨

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

승인 헤더가 유효하지 않을 때 이 오류 메시지가 표시됩니다. 다시 시도하기 전에 하려는 API 요청과 호환되는 수락 헤더를 올바르게 입력했는지 확인하십시오.

#### 사용할 수 있는 알 수 없는 수락 형식

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

설명자를 조회할 때 승인 헤더가 잘못 제공되면 이 오류 메시지가 표시됩니다. 다시 시도하기 전에 설명자](./api/descriptors.md)에 대해 [지원되는 헤더 수락 중 하나를 올바르게 입력했는지 확인하십시오.

#### 버전은 수락 헤더에 제공해야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

이 오류 메시지는 버전 번호가 승인 헤더에 포함되지 않은 경우에 표시됩니다. 스키마와 같은 특정 요소는 개별 인스턴스를 조회할 때 버전을 지정해야 합니다. 버전 번호가 포함된 Accept 헤더는 다음과 비슷합니다.

```plaintext
application/vnd.adobe.xed+json; version=1
```

지원되는 헤더 수락 목록은 [!DNL Schema Registry] 개발자 안내서의 [헤더](api/getting-started.md#accept) 수락 섹션을 참조하십시오.

#### 버전은 수락 헤더에 제공되지 않아야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

(GET) 리소스를 나열할 때 승인 헤더에 버전을 포함하려고 하면 이 오류가 표시됩니다. 단일 리소스에서 조회 요청을 시도하는 경우에만 버전이 필요합니다. Accept 헤더에서 버전을 제거하여 오류를 해결하십시오.
