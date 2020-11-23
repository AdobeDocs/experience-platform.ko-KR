---
keywords: Experience Platform;home;popular topics;;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema;troubleshooting;FAQ;faq;Union schema;UNION PROFILE;union profile
solution: Experience Platform
title: XDM(Experience Data Model) 시스템 문제 해결 안내서
description: 이 문서에서는 XDM(Experience Data Model) 시스템에 대한 FAQ와 일반적인 오류에 대한 문제 해결 가이드를 제공합니다.
topic: troubleshooting
translation-type: tm+mt
source-git-commit: e87fcd9f028bc6dedaec0435c4eef54e6aecae2d
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) 시스템 문제 해결 안내서

이 문서에서는 XDM(Frequently Asked Questions) 시스템 [!DNL Experience Data Model] 에 대한 답변과 일반적인 오류에 대한 문제 해결 가이드를 제공합니다. Adobe Experience Platform의 다른 서비스와 관련된 질문 및 문제 해결에 대해서는 [Experience Platform 문제 해결 가이드를 참조하십시오](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** 은 고객 경험 관리를 위한 표준화된 스키마를 정의하는 오픈 소스 사양입니다. XDM 시스템 [!DNL Experience Platform] 이 구축된 방법론 **은**&#x200B;서비스 [!DNL Experience Data Model] 에서 사용할 수 있도록 스키마 [!DNL Platform] 운영을수행합니다. 이 **[!DNL Schema Registry]** 는 사용자 인터페이스와 내부 **[!DNL Schema Library]** 에 액세스할 수 있는 RESTful API를 제공합니다 [!DNL Experience Platform]. See the [XDM documentation](home.md) for more information.

## FAQ

다음은 XDM 시스템 및 [!DNL Schema Registry] API 사용에 대한 자주 묻는 질문에 대한 답변 목록입니다.

### 스키마에 필드를 추가하려면 어떻게 해야 합니까?

혼합을 사용하여 스키마에 필드를 추가할 수 있습니다. 각 혼합은 하나 이상의 클래스와 호환되므로 호환되는 클래스 중 하나를 구현하는 모든 스키마에서 혼합을 사용할 수 있습니다. Adobe Experience Platform은 자체 사전 정의된 필드가 포함된 여러 산업 조합을 제공하지만, API 또는 사용자 인터페이스를 사용하여 새 믹스를 만들어 사용자 정의 필드를 스키마에 추가할 수 있습니다.

API에서 새 믹스를 만드는 방법에 대한 자세한 내용은 [!DNL Schema Registry] 믹신 끝점 안내서를 참조하십시오 [](api/mixins.md#create). UI를 사용하는 경우 스키마 [편집기 자습서를 참조하십시오](./tutorials/create-schema-ui.md).

### 혼합과 데이터 유형의 최적화는 무엇입니까?

[혼합은](./schema/composition.md#mixin) 스키마에서 하나 이상의 필드를 정의하는 구성 요소입니다. 혼합은 스키마의 계층에서 필드가 표시되는 방식을 적용하므로 해당 필드가 포함된 모든 스키마에서 동일한 구조를 표시합니다. 믹스는 해당 속성으로 식별되는 특정 클래스와 호환됩니다 `meta:intendedToExtend` .

[데이터 유형은](./schema/composition.md#data-type) 스키마에 대해 하나 이상의 필드를 제공할 수도 있습니다. 그러나 믹스와는 달리 데이터 유형은 특정 클래스에 한정되지 않습니다. 따라서 데이터 유형이 보다 유연한 옵션을 사용하여 여러 개의 스키마에서 재사용할 수 있는 일반적인 데이터 구조를 설명할 수 있습니다.

### 스키마의 고유 ID는 무엇입니까?

모든 리소스(스키마, 믹싱, 데이터 유형, 클래스)에는 참조 및 조회 목적으로 고유한 ID로 작동하는 URI가 있습니다. [!DNL Schema Registry] API에서 스키마를 볼 때 최상위 수준 `$id` 및 `meta:altId` 속성에서 찾을 수 있습니다.

자세한 내용은 API 개발자 안내서의 [리소스 식별](api/getting-started.md#resource-identification) 섹션을 [!DNL Schema Registry] 참조하십시오.

### 스키마는 언제 변경 사항을 방지하기 시작합니까?

데이터 집합 생성 시 또는 사용 가능한 스키마는 스키마에 대해 변경 사항을 적용할 수 있습니다 [[!DNL Real-time Customer Profile]](../profile/home.md). 스키마를 데이터 세트 생성에서 사용하거나 이와 함께 사용할 수 있도록 활성화하면 [!DNL Real-time Customer Profile]스키마 진화 [](schema/composition.md#evolution) 규칙은 시스템에 의해 엄격히 적용됩니다.

### 긴 필드 유형의 최대 크기는 얼마입니까?

긴 필드 유형은 최대 크기가 53비트(+1)인 정수로, 잠재적 범위는 -9007199254740992와 900719925470992 사이입니다. 이는 JSON의 JavaScript 구현이 긴 정수를 나타내는 방식에 대한 제한 때문입니다.

필드 유형에 대한 자세한 내용은 [XDM 필드 유형 제약 조건에 대한 문서를 참조하십시오](./schema/field-constraints.md).

### 스키마에 대한 ID를 어떻게 정의합니까?

에서 ID [!DNL Experience Platform]는 해석되는 데이터의 소스와 관계없이 제목(일반적으로 개인)을 식별하는 데 사용됩니다. 키 필드를 &quot;ID&quot;로 표시하여 스키마에 정의됩니다. ID에 일반적으로 사용되는 필드에는 이메일 주소, 전화 번호, CRM ID [[!DNL Experience Cloud ID (ECID)]](https://docs.adobe.com/content/help/ko-KR/id-service/using/home.html)및 기타 고유한 ID 필드가 포함됩니다.

필드는 API 또는 사용자 인터페이스를 사용하여 ID로 표시할 수 있습니다.

#### API에서 ID 정의

API에서 ID는 ID 설명자를 만들어 설정합니다. ID 설명자는 스키마의 특정 속성이 고유 식별자임을 나타냅니다.

ID 설명자는 /descriptors 끝점에 대한 POST 요청에 의해 만들어집니다. 성공하면 HTTP 상태 201(생성됨) 및 새 설명자의 세부 정보가 포함된 응답 개체를 받게 됩니다.

API에서 ID 설명자를 만드는 방법에 대한 자세한 내용은 개발자 안내서의 [설명자](api/descriptors.md) 문서 섹션을 [!DNL Schema Registry] 참조하십시오.

#### UI에서 ID 정의

스키마 편집기에서 스키마를 열고 ID로 표시하려는 편집기의 **[!UICONTROL 구조]** 섹션에 있는 필드를 클릭합니다. 오른쪽의 **[!UICONTROL 필드 속성]** 아래에서 **[!UICONTROL ID]** 확인란을 클릭합니다.

UI에서 ID 관리에 대한 자세한 내용은 스키마 편집기 자습서의 ID 필드 [정의](./tutorials/create-schema-ui.md#identity-field) 섹션에 대한 섹션을 참조하십시오.

### 스키마에는 기본 ID가 필요합니까?

기본 ID는 스키마에 0 또는 1이 있을 수 있으므로 선택 사항입니다. 하지만 스키마를 사용할 수 있도록 하려면 스키마에 기본 ID가 있어야 합니다 [!DNL Real-time Customer Profile]. 자세한 내용은 스키마 편집기 자습서의 [ID](./tutorials/create-schema-ui.md#identity-field) 섹션을 참조하십시오.

### 스키마를 사용하도록 설정하려면 어떻게 합니까 [!DNL Real-time Customer Profile]?

스키마는 스키마의 속성에 있는 &quot;union&quot; 태그 [[!DNL Real-time Customer Profile]](../profile/home.md) 를 추가하여 사용할 수 `meta:immutableTags` 있습니다. API 또는 사용자 인터페이스를 사용하여 사용할 스키마를 활성화할 [!DNL Profile] 수 있습니다.

#### API 사용을 위한 기존 스키마 [!DNL Profile] 활성화

스키마를 업데이트하고 값 &quot;union&quot;이 들어 있는 배열로 `meta:immutableTags` 속성을 추가하는 PATCH 요청을 만듭니다. 업데이트가 성공하면 응답에 이제 union 태그가 포함된 업데이트된 스키마가 표시됩니다.

API를 사용하여 스키마를 사용할 수 있도록 하는 방법에 대한 자세한 내용 [!DNL Real-time Customer Profile]은 개발자 안내서의 [조합](./api/unions.md) 문서를 [!DNL Schema Registry] 참조하십시오.

#### UI 사용을 위한 기존 스키마 [!DNL Profile] 활성화

에서 왼쪽 탐색 [!DNL Experience Platform]에서 **[!UICONTROL 스키마]** 를 클릭하고 스키마 목록에서 활성화할 스키마 이름을 선택합니다. 그런 다음, [스키마 속성] 아래의 편집기 **[!UICONTROL 오른쪽의]**&#x200B;프로필 **[!UICONTROL 을]** 클릭하여전환합니다.


자세한 내용은 스키마 편집기 자습서의 실시간 고객 [프로필에서](./tutorials/create-schema-ui.md#profile) 사용 [!UICONTROL 에 대한 섹션을] 참조하십시오.

### 조합 스키마를 직접 편집할 수 있습니까?

결합 스키마는 읽기 전용이며 시스템에 의해 자동으로 생성됩니다. 직접 편집할 수는 없습니다. 해당 클래스를 구현하는 스키마에 &quot;union&quot; 태그가 추가되면 특정 클래스에 대한 결합 스키마가 생성됩니다.

XDM의 조합에 대한 자세한 내용은 API 개발자 가이드의 [조합](./api/unions.md) 섹션 [!DNL Schema Registry] 을 참조하십시오.

### 데이터 파일을 스키마로 인제스트하려면 어떻게 데이터 파일을 포맷해야 합니까?

[!DNL Experience Platform] 데이터 파일을 [!DNL Parquet] 하나 또는 JSON 형식으로 허용합니다. 이러한 파일의 내용은 데이터 세트에서 참조하는 스키마를 따라야 합니다. 데이터 파일 섭취에 대한 우수 사례에 대한 자세한 내용은 [배치 처리 개요를 참조하십시오](../ingestion/home.md).

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

시스템이 특정 리소스를 찾을 수 없을 때 이 오류가 표시됩니다. 리소스가 삭제되었거나 API 호출의 경로가 잘못되었습니다. 다시 시도하기 전에 API 호출에 유효한 경로를 입력했는지 확인하십시오. 리소스의 올바른 ID를 입력했는지, 경로가 적절한 컨테이너(글로벌 또는 테넌트)와 올바르게 지정되었는지 확인할 수 있습니다.

API에서 조회 경로를 구성하는 방법에 대한 자세한 내용은 개발자 안내서의 [컨테이너](./api/getting-started.md#container) 및 [리소스 식별](api/getting-started.md#resource-identification) 섹션을 [!DNL Schema Registry] 참조하십시오.

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

이 오류 메시지는 다른 리소스에서 이미 사용 중인 제목과 함께 리소스를 만들려고 하면 표시됩니다. 제목은 모든 리소스 유형에서 고유해야 합니다. 예를 들어 이미 스키마에서 사용 중인 제목과 혼합을 만들려고 하면 이 오류가 표시됩니다.

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

잘못된 이름 지정 필드가 있는 새 혼합을 만들려고 하면 이 오류 메시지가 표시됩니다. IMS 조직에서 정의한 믹스는 다른 산업 및 공급업체 리소스 `TENANT_ID` 와의 충돌을 방지하기 위해 해당 분야를 A와 함께 네임스페이스해야 합니다. mixins에 대한 적절한 데이터 구조의 자세한 예는 [mixins 종단점 안내서에서 확인할 수 있습니다](./api/mixins.md#create).


### [!DNL Real-time Customer Profile] 오류

다음 오류 메시지는 스키마 활성화 관련 작업과 연관됩니다 [!DNL Real-time Customer Profile]. 자세한 내용은 [API 개발자 안내서의](./api/unions.md) 조합 [!DNL Schema Registry] 섹션을 참조하십시오.

#### 프로필 데이터 집합을 활성화하려면 스키마가 유효해야 합니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

이 오류 메시지는 활성화되지 않은 스키마에 대해 프로필 데이터 세트를 활성화하려고 할 때 표시됩니다 [!DNL Real-time Customer Profile]. 데이터 세트를 활성화하기 전에 스키마에 결합 태그가 있는지 확인합니다.

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

이 오류 메시지는 에 대한 스키마를 활성화하려고 [!DNL Profile] 시도하고 해당 속성 중 하나가 참조 ID 설명자 없이 관계 설명자를 포함할 때 표시됩니다. 해당 스키마 필드에 참조 ID 설명자를 추가하여 이 오류를 해결하십시오.

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

사용할 관계 설명자를 포함하는 스키마를 사용하려면 소스 필드 [!DNL Profile]의 네임스페이스와 대상 필드의 기본 네임스페이스가 동일해야 합니다. 이 오류 메시지는 참조 ID 설명자에 대해 일치하지 않는 네임스페이스를 포함하는 스키마를 활성화하려고 하면 표시됩니다. 대상 스키마 ID 필드 `xdm:namespace` 의 값이 소스 필드의 참조 ID 설명자에 있는 `xdm:identityNamespace` 속성 값과 일치하는지 확인합니다.

지원되는 ID 네임스페이스 코드 목록은 ID 네임스페이스 개요에서 [표준 네임스페이스에](../identity-service/namespaces.md) 대한 섹션을 참조하십시오.

### 헤더 오류 허용

시스템에서 응답의 형식을 지정하는 방법을 결정하기 위해 API의 대부분의 GET 요청에 [!DNL Schema Registry] 수락 헤더가 필요합니다. 다음은 수락 헤더와 연관된 일반적인 오류 목록입니다. 서로 다른 API 요청에 대해 호환되는 수락 헤더 목록은 스키마 레지스트리 개발자 안내서의 해당 섹션을 [참조하십시오](api/getting-started.md).

#### 헤더 매개 변수를 승인해야 합니다.

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

수락 헤더가 잘못된 경우 이 오류 메시지가 표시됩니다. 다시 시도하려는 API 요청과 호환되는 수락 헤더를 올바르게 입력했는지 확인하십시오.

#### 알 수 없는 수락 형식 사용 가능

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

설명자를 조회할 때 수락 헤더가 잘못 제공되면 이 오류 메시지가 표시됩니다. 설명자에 대해 [지원되는 헤더 수락 중 하나를 올바르게 입력했는지](./api/descriptors.md) 확인하고 다시 시도하십시오.

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

이 오류 메시지는 승인 헤더에 버전 번호가 포함되지 않은 경우 표시됩니다. 스키마와 같은 특정 요소는 개별 인스턴스를 조회할 때 버전을 지정해야 합니다. 버전 번호가 포함된 승인 헤더는 다음과 비슷합니다.

```plaintext
application/vnd.adobe.xed+json; version=1
```

지원되는 수락 헤더 목록은 개발자 안내서의 [수락 헤더](api/getting-started.md#accept) 섹션을 [!DNL Schema Registry] 참조하십시오.

#### 수락 헤더에서 버전을 제공해서는 안 됩니다.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

리소스를 나열할 때 승인 헤더에 버전을 포함하려고 하면 이 오류가 표시됩니다. 단일 리소스에서 조회 요청을 시도하는 경우에만 버전이 필요합니다. 승인 헤더에서 버전을 제거하여 오류를 해결하십시오.