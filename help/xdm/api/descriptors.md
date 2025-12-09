---
keywords: Experience Platform;홈;인기 주제;api;API;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;설명자;설명자;설명자;설명자;ID;ID;친숙한 이름;친숙한 이름;대체 표시 정보;참조;참조;관계;관계
solution: Experience Platform
title: 설명자 API 끝점
description: 스키마 레지스트리 API의 /descriptors 끝점을 사용하면 경험 애플리케이션 내에서 XDM 설명자를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: 491588dab1388755176b5e00f9d8ae3e49b7f856
workflow-type: tm+mt
source-wordcount: '2882'
ht-degree: 1%

---

# 설명자 엔드포인트

스키마는 데이터 엔티티의 구조를 정의하지만 이러한 스키마에서 생성된 데이터 세트가 서로 관련되는 방식은 지정하지 않습니다. Adobe Experience Platform에서는 설명자를 사용하여 이러한 관계를 설명하고 해석적 메타데이터를 스키마에 추가할 수 있습니다.

설명자는 Adobe Experience Platform의 스키마에 적용되는 테넌트 수준의 메타데이터 개체입니다. 또한 구조적 관계, 키 및 데이터 유효성 검사, 결합 또는 해석 다운스트림에 영향을 주는 동작 필드(예: 타임스탬프 또는 버전 관리)를 정의합니다.

스키마에는 하나 이상의 설명자가 있을 수 있습니다. 각 설명자는 `@type`과(와) 적용되는 `sourceSchema`을(를) 정의합니다. 설명자는 해당 스키마에서 생성된 모든 데이터 세트에 자동으로 적용됩니다.

Adobe Experience Platform에서 설명자는 스키마에 동작 규칙 또는 구조적 의미를 추가하는 메타데이터입니다.
설명자에는 다음과 같은 여러 유형이 있습니다.

- [ID 설명자](#identity-descriptor) - 필드를 ID로 표시합니다.
- [기본 키 설명자](#primary-key-descriptor) - 고유성을 적용합니다.
- [관계 설명자](#relationship-descriptor) - 외래 키 조인 정의
- [대체 표시 정보 설명자](#friendly-name) - UI의 필드 이름을 바꿀 수 있습니다.
- [버전](#version-descriptor) 및 [타임스탬프](#timestamp-descriptor) 설명자 - 이벤트 순서 추적 및 변경 내용 검색

`/descriptors` API의 [!DNL Schema Registry] 끝점을 사용하면 경험 응용 프로그램 내의 설명자를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작

이 가이드에 사용된 끝점은 [[!DNL Schema Registry] API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

[!DNL Schema Registry]은(는) 표준 설명자 외에도 **기본 키**, **버전** 및 **타임스탬프**&#x200B;와 같은 관계형 스키마에 대한 설명자 형식을 지원합니다. 이러한 기능은 고유성을 적용하고 버전 관리를 제어하며 스키마 수준에서 시계열 필드를 정의합니다. 관계형 스키마에 익숙하지 않은 경우 [Data Mirror 개요](../data-mirror/overview.md) 및 [관계형 스키마 기술 참조](../schema/relational.md)를 검토한 후 계속하십시오.

>[!IMPORTANT]
>
>모든 설명자 유형에 대한 자세한 내용은 [부록](#defining-descriptors)을 참조하십시오.

## 설명자 목록 검색 {#list}

`/tenant/descriptors`에 GET 요청을 하여 조직에서 정의한 모든 설명자를 나열할 수 있습니다.

**API 형식**

```http
GET /tenant/descriptors
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

응답 형식은 요청에서 보낸 `Accept` 헤더에 따라 다릅니다. `/descriptors` 끝점은 `Accept` API의 다른 모든 끝점과 다른 [!DNL Schema Registry] 헤더를 사용합니다.

>[!IMPORTANT]
>
>설명자에는 `Accept`을(를) `xed`(으)로 바꾸고 설명자에 고유한 `xdm` 옵션을 제공하는 고유한 `link` 헤더가 필요합니다. 아래 예제 호출에 적절한 `Accept` 헤더가 포함되었지만 설명자로 작업할 때 올바른 헤더가 사용되고 있는지 각별히 주의하십시오.

| `Accept` 헤더 | 설명 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 설명자 ID 배열 반환 |
| `application/vnd.adobe.xdm-link+json` | 설명자 API 경로 배열 반환 |
| `application/vnd.adobe.xdm+json` | 확장된 설명자 개체의 배열을 반환합니다. |
| `application/vnd.adobe.xdm-v2+json` | 페이징 기능을 사용하려면 이 `Accept` 헤더를 사용해야 합니다. |

{style="table-layout:auto"}

**응답**

응답에는 설명자가 정의된 각 설명자 유형에 대한 배열이 포함됩니다. 즉, 정의된 특정 `@type`의 설명자가 없으면 레지스트리는 해당 설명자 유형에 대해 빈 배열을 반환하지 않습니다.

`link` `Accept` 헤더를 사용할 때 각 설명자가 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}` 형식의 배열 항목으로 표시됩니다.

```JSON
{
  "xdm:alternateDisplayInfo": [
    "/tenant/descriptors/85dc1bc8b91516ac41163365318e38a9f1e4f351",
    "/tenant/descriptors/49bd5abb5a1310ee80ebc1848eb508d383a462cf",
    "/tenant/descriptors/b3b3e548f1c653326bcf5459ceac4140fc0b9e08"
  ],
  "xdm:descriptorIdentity": [
    "/tenant/descriptors/f7a4bc25429496c4740f8f9a7a49ba96862c5379"
  ],
  "xdm:descriptorOneToOne": [
    "/tenant/descriptors/cb509fd6f8ab6304e346905441a34b58a0cd481a"
  ]
}
```

## 설명자 조회 {#lookup}

특정 설명자의 세부 정보를 보려면 해당 `@id`을(를) 사용하여 GET 요청을 전송하십시오.

**API 형식**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 조회할 설명자의 `@id`입니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 `@id` 값으로 설명자를 검색합니다. 설명자의 버전이 없으므로 조회 요청에는 `Accept` 헤더가 필요하지 않습니다.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 설명자 유형에 따라 달라지는 추가 정보와 해당 `@type` 및 `sourceSchema`을(를) 포함하여 설명자의 세부 정보를 반환합니다. 반환된 `@id`은(는) 요청에 제공된 설명자 `@id`과(와) 일치해야 합니다.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "createdUser": "{CREATED_USER}",
  "imsOrg": "{ORG_ID}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 설명자 만들기 {#create}

`/tenant/descriptors` 끝점에 대한 POST 요청을 수행하여 새 설명자를 만들 수 있습니다.

>[!IMPORTANT]
>
>[!DNL Schema Registry]을(를) 사용하면 여러 다른 설명자 유형을 정의할 수 있습니다. 각 설명자 유형은 요청 본문에 보낼 고유한 필드를 필요로 합니다. 설명자의 전체 목록과 설명자를 정의하는 데 필요한 필드는 [부록](#defining-descriptors)을 참조하세요.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 샘플 스키마의 &quot;이메일 주소&quot; 필드에 ID 설명자를 정의합니다. 이에 따라 [!DNL Experience Platform]이(가) 전자 메일 주소를 식별자로 사용하여 개인에 대한 정보를 결합하도록 합니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**응답**

성공적인 응답은 HTTP 상태 201(생성됨) 및 해당 `@id`을(를) 포함하여 새로 생성된 설명자의 세부 정보를 반환합니다. `@id`은(는) [!DNL Schema Registry]에 의해 할당되고 API의 설명자를 참조하는 데 사용되는 읽기 전용 필드입니다.

```JSON
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 설명자 업데이트 {#put}

PUT 요청의 경로에 `@id`을(를) 포함하여 설명자를 업데이트할 수 있습니다.

**API 형식**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 업데이트할 설명자의 `@id`입니다. |

{style="table-layout:auto"}

**요청**

이 요청은 본질적으로 설명자를 재작성하므로 요청 본문에는 해당 유형의 설명자를 정의하는 데 필요한 모든 필드가 포함되어야 합니다. 다시 말해, 설명자를 업데이트(PUT)하기 위한 요청 페이로드는 같은 유형의 설명자를 [생성(POST)하기 위한 페이로드와 동일합니다](#create).

>[!IMPORTANT]
>
>POST 요청을 사용하여 설명자를 만드는 경우와 마찬가지로, 각 설명자 유형에는 고유한 필드를 PUT 요청 페이로드에서 전송해야 합니다. 설명자의 전체 목록과 설명자를 정의하는 데 필요한 필드는 [부록](#defining-descriptors)을 참조하세요.

다음 예제에서는 다른 `xdm:sourceProperty`(`mobile phone`)을(를) 참조하도록 ID 설명자를 업데이트하고 `xdm:namespace`을(를) `Phone`(으)로 변경합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/mobilePhone/number",
        "xdm:namespace": "Phone",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

**응답**

성공적인 응답은 HTTP 상태 201(생성됨) 및 업데이트된 설명자의 `@id`(요청에서 전송된 `@id`과(와) 일치해야 함)을 반환합니다.

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

설명자를 보기 위해 [조회(GET) 요청](#lookup)을 수행하면 PUT 요청에 전송된 변경 사항을 반영하도록 필드가 업데이트되었음을 알 수 있습니다.

## 설명자 삭제 {#delete}

[!DNL Schema Registry]에서 정의한 설명자를 제거해야 하는 경우가 있습니다. 이 작업은 제거할 설명자의 `@id`을(를) 참조하는 DELETE 요청을 통해 수행됩니다.

**API 형식**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 삭제할 설명자의 `@id`입니다. |

{style="table-layout:auto"}

**요청**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

설명자가 삭제되었는지 확인하기 위해 설명자 [에 대해 ](#lookup)조회 요청`@id`을 수행할 수 있습니다. 설명자가 [!DNL Schema Registry]에서 제거되었으므로 응답에서 HTTP 상태 404(찾을 수 없음)를 반환합니다.

## 부록 {#appendix}

다음 섹션에서는 [!DNL Schema Registry] API의 설명자 작업에 대한 추가 정보를 제공합니다.

### 설명자 정의 {#defining-descriptors}

>[!NOTE]
>
>조직의 샌드박스에 적용할 수 있는 최대 설명자 수는 4000개입니다.

다음 섹션에서는 각 유형의 설명자를 정의하는 데 필요한 필드를 포함하여 사용 가능한 설명자 유형에 대한 개요를 제공합니다.

>[!IMPORTANT]
>
>시스템이 해당 샌드박스의 모든 사용자 정의 필드에 해당 레이블을 적용하므로 테넌트 네임스페이스 개체에 레이블을 지정할 수 없습니다. 대신 레이블을 지정해야 하는 개체 아래에 리프 노드를 지정해야 합니다.

#### ID 설명자 {#identity-descriptor}

ID 설명자는 &quot;[!UICONTROL sourceProperty]&quot;의 &quot;[!UICONTROL sourceSchema]&quot;이(가) [!DNL Identity]Experience Platform Identity 서비스[에서 설명한 대로 ](../../identity-service/home.md) 필드임을 알립니다.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의 중인 설명자 유형. ID 설명자의 경우 이 값을 `xdm:descriptorIdentity`(으)로 설정해야 합니다. |
| `xdm:sourceSchema` | 설명자가 정의되는 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전. |
| `xdm:sourceProperty` | ID가 될 특정 속성에 대한 경로입니다. 경로는 &quot;/&quot;로 시작하고 1로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot; 사용). |
| `xdm:namespace` | ID 네임스페이스의 `id` 또는 `code` 값입니다. [[!DNL Identity Service API]](https://developer.adobe.com/experience-platform-apis/references/identity-service)을(를) 사용하여 네임스페이스 목록을 찾을 수 있습니다. |
| `xdm:property` | 사용된 `xdm:id`에 따라 `xdm:code` 또는 `xdm:namespace`입니다. |
| `xdm:isPrimary` | 선택적 부울 값입니다. true인 경우 는 필드를 기본 ID로 나타냅니다. 스키마에는 기본 ID가 하나만 포함될 수 있습니다. |

{style="table-layout:auto"}

#### 설명자에 대한 알기 쉬운 이름 {#friendly-name}

사용자가 알기 쉬운 이름 설명자를 사용하여 코어 라이브러리 스키마 필드의 `title`, `description` 및 `meta:enum` 값을 수정할 수 있습니다. 특히 조직에 관련된 정보를 포함하는 것으로 레이블을 지정하려는 &quot;eVar&quot; 및 기타 &quot;일반&quot; 필드로 작업할 때 유용합니다. UI는 이러한 매개 변수를 사용하여 보다 친숙한 이름을 표시하거나 친숙한 이름이 있는 필드만 표시할 수 있습니다.

```json
{
  "@type": "xdm:alternateDisplayInfo",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/xdm:eventType",
  "xdm:title": {
    "en_us": "Event Type"
  },
  "xdm:description": {
    "en_us": "The type of experience event detected by the system."
  },
  "meta:enum": {
    "click": "Mouse Click",
    "addCart": "Add to Cart",
    "checkout": "Cart Checkout"
  },
  "xdm:excludeMetaEnum": {
    "web.formFilledOut": "Web Form Filled Out",
    "media.ping": "Media ping"
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의 중인 설명자 유형. 알기 쉬운 이름 설명자의 경우 이 값을 `xdm:alternateDisplayInfo`(으)로 설정해야 합니다. |
| `xdm:sourceSchema` | 설명자가 정의되는 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전. |
| `xdm:sourceProperty` | 세부 정보를 수정할 특정 속성의 경로입니다. 경로는 슬래시(`/`)로 시작하고 슬래시로 끝나지 않아야 합니다. 경로에 `properties`을(를) 포함하지 마십시오(예: `/personalEmail/address` 대신 `/properties/personalEmail/properties/address` 사용). |
| `xdm:title` | 이 필드에 표시할 새 제목(제목 대/소문자로 작성됨)입니다. |
| `xdm:description` | 제목과 함께 선택적 설명을 추가할 수 있습니다. |
| `meta:enum` | `xdm:sourceProperty`에 표시된 필드가 문자열 필드인 경우 `meta:enum`을(를) 사용하여 세분화 UI에서 필드에 대해 제안된 값을 추가할 수 있습니다. `meta:enum`은(는) 열거형을 선언하거나 XDM 필드에 대한 데이터 유효성 검사를 제공하지 않습니다.<br><br>Adobe에서 정의한 코어 XDM 필드에만 사용해야 합니다. 소스 속성이 조직에서 정의한 사용자 지정 필드인 경우 대신 필드의 상위 리소스에 대한 PATCH 요청을 통해 직접 필드의 `meta:enum` 속성을 편집해야 합니다. |
| `meta:excludeMetaEnum` | `xdm:sourceProperty`이(가) 나타내는 필드가 `meta:enum` 필드 아래에 제공된 기존의 제안 값이 있는 문자열 필드인 경우 이 개체를 알기 쉬운 이름 설명자에 포함시켜 세분화에서 이러한 값의 일부 또는 모두를 제외할 수 있습니다. 항목을 제외하려면 각 항목의 키 및 값이 필드의 원래 `meta:enum`에 포함된 값과 일치해야 합니다. |

{style="table-layout:auto"}

#### 관계 설명자 {#relationship-descriptor}

관계 설명자는 `xdm:sourceProperty` 및 `xdm:destinationProperty`에 설명된 속성을 기준으로 서로 다른 두 스키마 간의 관계를 설명합니다. 자세한 내용은 [두 스키마 간의 관계 정의](../tutorials/relationship-api.md)에 대한 자습서를 참조하십시오.

이러한 속성을 사용하여 원본 필드(외래 키)가 대상 필드([기본 키](#primary-key-descriptor) 또는 후보 키)와 관련되는 방식을 선언합니다.

>[!TIP]
>
>**외래 키**&#x200B;은(는) 다른 스키마의 키 필드를 참조하는 원본 스키마(`xdm:sourceProperty`에 의해 정의됨)의 필드입니다. **후보 키**&#x200B;은(는) 레코드를 고유하게 식별하는 대상 스키마의 모든 필드(또는 필드 집합)이며 기본 키 대신 사용할 수 있습니다.

API는 다음 두 가지 패턴을 지원합니다.

- `xdm:descriptorOneToOne`: 표준 1:1 관계.
- `xdm:descriptorRelationship`: 새 작업 및 관계형 스키마에 대한 일반 패턴(카디널리티, 이름 지정 및 기본 키 이외의 대상 지원).

##### 일대일 관계(표준 스키마)

이미 `xdm:descriptorOneToOne`에 의존하는 기존 표준 스키마 통합을 유지 관리할 때 사용합니다.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

다음 표에서는 일대일 관계 설명자를 정의하는 데 필요한 필드를 설명합니다.

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의 중인 설명자 유형. 관계 설명자의 경우 Real-Time CDP B2B edition에 대한 액세스 권한이 없는 경우 이 값을 `xdm:descriptorOneToOne`(으)로 설정해야 합니다. B2B edition을 사용하면 `xdm:descriptorOneToOne` 또는 [`xdm:descriptorRelationship`](#b2b-relationship-descriptor)을(를) 사용할 수 있습니다. |
| `xdm:sourceSchema` | 설명자가 정의되는 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전. |
| `xdm:sourceProperty` | 관계가 정의되는 소스 스키마의 필드 경로. &quot;/&quot;로 시작하고 &quot;/&quot;로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;). |
| `xdm:destinationSchema` | 이 설명자가 관계를 정의하는 참조 스키마의 `$id` URI입니다. |
| `xdm:destinationVersion` | 참조 스키마의 주 버전. |
| `xdm:destinationProperty` | (선택 사항) 참조 스키마 내의 대상 필드 경로입니다. 이 속성을 생략하면 일치하는 참조 ID 설명자가 포함된 모든 필드에서 대상 필드를 유추합니다(아래 참조). |

##### 일반 관계(관계형 스키마 및 새 프로젝트에 권장)

모든 새 구현 및 관계형 스키마에 이 설명자를 사용합니다. 이를 통해 관계의 카디널리티를 정의하고(일대일 또는 다대일 등), 관계 이름을 지정하고, 기본 키가 아닌 대상 필드에 연결할 수 있습니다(기본 키가 아님).

다음 예는 일반적인 관계 설명자를 정의하는 방법을 보여줍니다.

**최소 예:**

이 최소 예에는 두 스키마 간의 다대일 관계를 정의하는 데 필요한 필드만 포함됩니다.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceProperty": "/customer_ref",
  "xdm:sourceVersion": 1,
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:cardinality": "M:1"
}
```

**모든 선택적 필드가 있는 예제:**

이 예에는 관계 이름, 표시 제목 및 명시적 기본이 아닌 키 대상 필드와 같은 모든 선택적 필드가 포함되어 있습니다.

```json
{
  "@type": "xdm:descriptorRelationship",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SOURCE_SCHEMA_ID}",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/customer_ref",
  "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{DEST_SCHEMA_ID}",
  "xdm:destinationProperty": "/customer_id",
  "xdm:sourceToDestinationName": "CampaignToCustomer",
  "xdm:destinationToSourceName": "CustomerToCampaign",
  "xdm:sourceToDestinationTitle": "Customer campaigns",
  "xdm:destinationToSourceTitle": "Campaign customers",
  "xdm:cardinality": "M:1"
}
```

##### 관계 설명자 선택

적용할 관계 설명자를 결정하려면 다음 지침을 따르십시오.

| 상황 | 사용할 설명자 |
| --------------------------------------------------------------------- | ----------------------------------------- |
| 새 작업 또는 관계형 스키마 | `xdm:descriptorRelationship` |
| 표준 스키마의 기존 1:1 매핑 | `xdm:descriptorOneToOne`에서만 지원되는 기능이 필요한 경우가 아니면 `xdm:descriptorRelationship`을(를) 계속 사용하십시오. |
| 다대일 또는 선택적 카디널리티(`1:1`, `1:0`, `M:1`, `M:0`)가 필요합니다. | `xdm:descriptorRelationship` |
| UI/다운스트림 가독성을 위해 관계 이름 또는 제목 필요 | `xdm:descriptorRelationship` |
| ID가 아닌 대상 대상 필요 | `xdm:descriptorRelationship` |

>[!NOTE]
>
>표준 스키마의 기존 `xdm:descriptorOneToOne` 설명자의 경우 기본 ID 대상이 아닌 대상, 사용자 지정 이름 지정 또는 확장된 카디널리티 옵션과 같은 기능이 필요하지 않는 한 계속 사용하십시오.

##### 기능 비교

다음 표에서는 두 설명자 유형의 기능을 비교합니다.

| 기능 | `xdm:descriptorOneToOne` | `xdm:descriptorRelationship` |
| ------------------ | ------------------------ | ------------------------------------------------------------------------ |
| 카디널리티 | 1:1 | 1:1, 1:0, M:1, M:0(정보 제공) |
| 대상 대상 대상 | ID/명시적 필드 | 기본적으로 기본 키 또는 `xdm:destinationProperty`을(를) 통한 비기본 키 |
| 이름 지정 필드 | 지원되지 않음 | `xdm:sourceToDestinationName`, `xdm:destinationToSourceName` 및 제목 |
| 관계 맞춤 | 제한적 | 관계형 스키마에 대한 기본 패턴 |

##### 제한 및 유효성 검사

일반적인 관계 설명자를 정의할 때 다음 요구 사항 및 권장 사항을 따르십시오.

- 관계형 스키마의 경우 소스 필드(외래 키)를 루트 수준에 배치합니다. 이는 단순한 모범 사례 권장 사항이 아닌 수집을 위한 현재 기술적 제한입니다.
- 소스 및 대상 필드의 데이터 형식(숫자, 날짜, 부울, 문자열)이 호환되는지 확인합니다.
- 카디널리티는 정보 제공용이며 스토리지는 이를 적용하지 않습니다. 카디널리티를 `<source>:<destination>` 형식으로 지정하십시오. 허용되는 값은 `1:1`, `1:0`, `M:1` 또는 `M:0`입니다.

#### 기본 키 설명자 {#primary-key-descriptor}

기본 키 설명자(`xdm:descriptorPrimaryKey`)는 스키마에 있는 하나 이상의 필드에 고유성 및 null이 아닌 제약 조건을 적용합니다.

```json
{
  "@type": "xdm:descriptorPrimaryKey",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": ["/orderId", "/orderLineId"]
}
```

| 속성 | 설명 |
| -------------------- | ----------------------------------------------------------------------------- |
| `@type` | `xdm:descriptorPrimaryKey`이어야 합니다. |
| `xdm:sourceSchema` | 스키마의 `$id` URI입니다. |
| `xdm:sourceProperty` | 기본 키 필드에 대한 JSON 포인터. 복합 키에 배열을 사용합니다. 시계열 스키마의 경우, 복합 키는 이벤트 레코드에서 고유성을 보장하기 위해 타임스탬프 필드를 포함해야 합니다. |

#### 버전 설명자 {#version-descriptor}

>[!NOTE]
>
>UI 스키마 편집기에서 버전 설명자가 &quot;[!UICONTROL Version identifier]&quot;(으)로 나타납니다.

버전 설명자(`xdm:descriptorVersion`)는 잘못된 변경 이벤트에서 충돌을 감지하고 방지하는 필드를 지정합니다.

```json
{
  "@type": "xdm:descriptorVersion",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/versionNumber"
}
```

| 속성 | 설명 |
| -------------------- | ------------------------------------------------------------- |
| `@type` | `xdm:descriptorVersion`이어야 합니다. |
| `xdm:sourceSchema` | 스키마의 `$id` URI입니다. |
| `xdm:sourceProperty` | 버전 필드에 대한 JSON 포인터. `required`(으)로 표시되어야 합니다. |

#### 타임스탬프 설명자 {#timestamp-descriptor}

>[!NOTE]
>
>UI 스키마 편집기에서 타임스탬프 설명자가 &quot;[!UICONTROL Timestamp identifier]&quot;(으)로 나타납니다.

타임스탬프 설명자(`xdm:descriptorTimestamp`)는 `"meta:behaviorType": "time-series"`이(가) 있는 스키마의 타임스탬프로 날짜-시간 필드를 지정합니다.

```json
{
  "@type": "xdm:descriptorTimestamp",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
  "xdm:sourceProperty": "/eventTime"
}
```

| 속성 | 설명 |
| -------------------- | ------------------------------------------------------------------------------------------ |
| `@type` | `xdm:descriptorTimestamp`이어야 합니다. |
| `xdm:sourceSchema` | 스키마의 `$id` URI입니다. |
| `xdm:sourceProperty` | 타임스탬프 필드에 대한 JSON 포인터. `required`(으)로 표시되어야 하며 `date-time` 형식이어야 합니다. |

##### B2B 관계 설명자 {#B2B-relationship-descriptor}

Real-Time CDP B2B edition에서는 다대일 관계를 허용하는 스키마 간의 관계를 정의하는 대체 방법을 도입했습니다. 이 새 관계는 `@type: xdm:descriptorRelationship` 형식이어야 하며 페이로드에 `@type: xdm:descriptorOneToOne` 관계보다 많은 필드가 포함되어야 합니다. 자세한 내용은 [B2B edition에 대한 스키마 관계 정의](../tutorials/relationship-b2b.md)에 대한 자습서를 참조하십시오.

```json
{
   "@type": "xdm:descriptorRelationship",
   "xdm:sourceSchema" : "https://ns.adobe.com/{TENANT_ID}/schemas/9f2b2f225ac642570a110d8fd70800ac0c0573d52974fa9a",
   "xdm:sourceVersion" : 1,
   "xdm:sourceProperty" : "/person-ref",
   "xdm:destinationSchema" : "https://ns.adobe.com/{TENANT_ID/schemas/628427680e6b09f1f5a8f63ba302ee5ce12afba8de31acd7",
   "xdm:destinationVersion" : 1,
   "xdm:destinationProperty": "/personId",
   "xdm:destinationNamespace" : "People", 
   "xdm:destinationToSourceTitle" : "Opportunity Roles",
   "xdm:sourceToDestinationTitle" : "People",
   "xdm:cardinality": "M:1"
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의 중인 설명자 유형. 다음 필드가 있는 경우 값을 `xdm:descriptorRelationship`(으)로 설정해야 합니다. 추가 유형에 대한 자세한 내용은 [관계 설명자](#relationship-descriptor) 섹션을 참조하십시오. |
| `xdm:sourceSchema` | 설명자가 정의되는 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전. |
| `xdm:sourceProperty` | 관계가 정의되는 소스 스키마의 필드 경로. &quot;/&quot;로 시작하고 &quot;/&quot;로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;). |
| `xdm:destinationSchema` | 이 설명자가 관계를 정의하는 참조 스키마의 `$id` URI입니다. |
| `xdm:destinationVersion` | 참조 스키마의 주 버전. |
| `xdm:destinationProperty` | (선택 사항) 참조 스키마 내의 대상 필드 경로입니다. 스키마의 기본 ID나 `xdm:sourceProperty`과(와) 호환되는 데이터 형식의 다른 필드로 확인되어야 합니다. 생략하면 관계가 예상대로 작동하지 않을 수 있습니다. |
| `xdm:destinationNamespace` | 참조 스키마에서 기본 ID의 네임스페이스입니다. |
| `xdm:destinationToSourceTitle` | 참조 스키마에서 소스 스키마로의 관계 표시 이름. |
| `xdm:sourceToDestinationTitle` | 소스 스키마에서 참조 스키마로의 관계 표시 이름. |
| `xdm:cardinality` | 스키마 간의 조인 관계입니다. 다대일 관계를 참조하여 이 값을 `M:1`(으)로 설정해야 합니다. |

{style="table-layout:auto"}

#### 참조 ID 설명자

참조 ID 설명자는 스키마 필드의 기본 ID에 대한 참조 컨텍스트를 제공하여 다른 스키마의 필드에서 참조할 수 있도록 합니다. 참조 스키마에는 이미 기본 ID 필드가 정의되어 있어야 해당 설명자를 통해 다른 스키마에서 참조할 수 있습니다.

```json
{
  "@type": "xdm:descriptorReferenceIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:identityNamespace": "Email"
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의 중인 설명자 유형. 참조 ID 설명자의 경우 이 값을 `xdm:descriptorReferenceIdentity`(으)로 설정해야 합니다. |
| `xdm:sourceSchema` | 설명자가 정의되는 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전. |
| `xdm:sourceProperty` | 참조 스키마를 참조하는 데 사용할 소스 스키마의 필드 경로입니다. &quot;/&quot;로 시작하고 1로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: `/personalEmail/address` 대신 `/properties/personalEmail/properties/address`). |
| `xdm:identityNamespace` | 소스 속성에 대한 ID 네임스페이스 코드. |

{style="table-layout:auto"}

#### 사용되지 않는 필드 설명자

해당 필드에 [(으)로 설정된 ](../tutorials/field-deprecation-api.md#custom) 특성을 추가하여 사용자 지정 XDM 리소스 내의 필드를 `meta:status`사용하지 않을 수 있습니다`deprecated`. 그러나 스키마의 표준 XDM 리소스에서 제공하는 필드를 사용하지 않으려면 해당 스키마에 더 이상 사용되지 않는 필드 설명자를 할당하여 동일한 효과를 얻을 수 있습니다. [올바른 `Accept` 헤더](../tutorials/field-deprecation-api.md#verify-deprecation)를 사용하면 API에서 조회할 때 스키마에 대해 더 이상 사용되지 않는 표준 필드를 볼 수 있습니다.

```json
{
  "@type": "xdm:descriptorDeprecated",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/faxPhone"
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 설명자 유형. 필드 사용 중단 설명자의 경우 이 값을 `xdm:descriptorDeprecated`(으)로 설정해야 합니다. |
| `xdm:sourceSchema` | 설명자를 적용하는 스키마의 URI `$id`입니다. |
| `xdm:sourceVersion` | 설명자를 적용 중인 스키마 버전입니다. `1`(으)로 설정해야 합니다. |
| `xdm:sourceProperty` | 설명자를 적용하는 스키마 내의 속성에 대한 경로입니다. 설명자를 여러 속성에 적용하려면 경로 목록을 배열 형식으로 제공할 수 있습니다(예: `["/firstName", "/lastName"]`). |

{style="table-layout:auto"}
