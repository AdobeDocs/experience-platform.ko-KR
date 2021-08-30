---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;설명자;설명자;설명자;설명자;ID;설명자;ID;친숙한 이름;대체 이름;참조;참조;관계;관계
solution: Experience Platform
title: 설명자 API 끝점
description: 스키마 레지스트리 API의 /descriptors 종단점을 사용하면 경험 애플리케이션 내의 XDM 설명자를 프로그래밍 방식으로 관리할 수 있습니다.
topic-legacy: developer guide
exl-id: bda1aabd-5e6c-454f-a039-ec22c5d878d2
source-git-commit: f269a7b1584a6e4a0e1820a0c587a647c0c8f7b5
workflow-type: tm+mt
source-wordcount: '1630'
ht-degree: 3%

---

# 끝점 설명자

스키마는 데이터 엔티티에 대한 정적 보기를 정의하지만 이러한 스키마(예: 데이터 세트)를 기반으로 하는 데이터가 서로 관련되는 방식에 대한 특정 세부 정보는 제공하지 않습니다. Adobe Experience Platform에서는 설명자를 사용하여 스키마에 대한 이러한 관계 및 기타 해석 메타데이터를 설명할 수 있습니다.

스키마 설명자는 테넌트 수준 메타데이터입니다. 즉, 사용자 IMS에 고유하며 모든 설명자 작업이 테넌트 컨테이너에서 수행됩니다.

각 스키마에는 하나 이상의 스키마 설명자 엔티티가 적용될 수 있습니다. 각 스키마 설명자 엔티티는 설명자 `@type` 및 설명자가 적용되는 `sourceSchema`를 포함합니다. 설명자가 적용되면 스키마를 사용하여 만든 모든 데이터 세트에 적용됩니다.

[!DNL Schema Registry] API의 `/descriptors` 종단점을 사용하면 경험 애플리케이션 내의 설명자를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 엔드포인트는 [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/class-registry.yaml)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## 설명자 목록 검색 {#list}

`/tenant/descriptors`에 GET 요청을 수행하여 조직에서 정의한 모든 설명자를 나열할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xdm-link+json'
```

응답 형식은 요청에서 전송된 `Accept` 헤더에 따라 다릅니다. `/descriptors` 종단점은 [!DNL Schema Registry] API의 다른 모든 종단점과 다른 `Accept` 헤더를 사용합니다.

>[!IMPORTANT]
>
>설명자는 `xed` 을 `xdm`로 대체하는 고유한 `Accept` 헤더를 필요로 하며 설명자에 고유한 `link` 옵션을 제공합니다. 적절한 `Accept` 헤더가 아래 예제 호출에 포함되었지만 설명자를 사용하여 작업할 때 올바른 헤더가 사용되는지 확인해야 합니다.

| `Accept` 헤더 | 설명 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 설명자 ID 배열을 반환합니다. |
| `application/vnd.adobe.xdm-link+json` | 설명자 API 경로 배열 반환 |
| `application/vnd.adobe.xdm+json` | 확장된 설명자 개체의 배열을 반환합니다. |
| `application/vnd.adobe.xdm-v2+json` | 페이징 기능을 활용하려면 이 `Accept` 헤더를 사용해야 합니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

응답에는 정의된 설명자가 있는 각 설명자 유형에 대한 배열이 포함됩니다. 즉, 특정 `@type` 설명자가 정의되지 않은 경우 레지스트리에서 해당 설명자 유형에 대해 빈 배열을 반환하지 않습니다.

`link` `Accept` 헤더를 사용하는 경우 각 설명자가 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}` 형식의 배열 항목으로 표시됩니다

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

특정 설명자에 대한 세부 정보를 보려면 `@id`을 사용하여 개별 설명자를 조회(GET)할 수 있습니다.

**API 형식**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 조회할 설명자의 `@id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `@id` 값으로 설명자를 검색합니다. 설명자의 버전이 관리되지 않으므로 조회 요청에 `Accept` 헤더가 필요하지 않습니다.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 설명자 유형에 따라 달라지는 추가 정보와 `@type` 및 `sourceSchema` 등의 설명자 세부 정보를 반환합니다. 반환된 `@id`는 요청에 제공된 설명자 `@id`와 일치해야 합니다.

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
  "imsOrg": "{IMS_ORG}",
  "createdClient": "{CREATED_CLIENT}",
  "updatedUser": "{UPDATED_USER}",
  "created": 1548899346989,
  "updated": 1548899346989,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 설명자 만들기 {#create}

`/tenant/descriptors` 종단점에 대한 POST 요청을 수행하여 새 설명자를 생성할 수 있습니다.

>[!IMPORTANT]
>
>[!DNL Schema Registry] 을 사용하면 여러 가지 설명자 유형을 정의할 수 있습니다. 각 설명자 유형에는 요청 본문에서 고유한 특정 필드를 전송해야 합니다. 설명자와 설명자를 정의하는 데 필요한 필드의 전체 목록은 [부록](#defining-descriptors)을 참조하십시오.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 샘플 스키마의 &quot;email address&quot; 필드에 ID 설명자를 정의합니다. 이 호출은 [!DNL Experience Platform]에게 개인 정보를 함께 연결하는 데 도움이 되도록 이메일 주소를 식별자로 사용하도록 지시합니다.

```SHELL
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

성공한 응답은 HTTP 상태 201(생성됨) 및 새로 만든 설명자에 대한 세부 정보를 반환합니다(예: `@id`). `@id`은 [!DNL Schema Registry]에서 할당한 읽기 전용 필드이며 API의 설명자를 참조하는 데 사용됩니다.

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

PUT 요청 경로에 `@id`을 포함하여 설명자를 업데이트할 수 있습니다.

**API 형식**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 업데이트할 설명자의 `@id` |

{style=&quot;table-layout:auto&quot;}

**요청**

이 요청은 설명자를 다시 기록하므로, 요청 본문에 해당 유형의 설명자를 정의하는 데 필요한 모든 필드가 포함되어야 합니다. 즉, 설명자를 업데이트(PUT)하는 요청 페이로드는 같은 유형의 설명자](#create)만들기(POST)에 대한 페이로드와 동일합니다.[

>[!IMPORTANT]
>
>POST 요청을 사용하여 설명자를 만드는 것과 마찬가지로 각 설명자 유형에는 PUT 요청 페이로드에서 고유한 특정 필드를 전송해야 합니다. 설명자와 설명자를 정의하는 데 필요한 필드의 전체 목록은 [부록](#defining-descriptors)을 참조하십시오.

다음 예에서는 ID 설명자를 업데이트하여 다른 `xdm:sourceProperty`(`mobile phone`)을 참조하고 `xdm:namespace`를 `Phone`(으)로 변경합니다.

```SHELL
curl -X PUT \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

성공적인 응답은 HTTP 상태 201(생성됨) 및 업데이트된 설명자의 `@id`을 반환합니다(요청에서 전송된 `@id`과 일치해야 함).

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

설명자를 보기 위해 [조회(GET) 요청](#lookup)을 수행하면 PUT 요청에 전송된 변경 사항을 반영하도록 필드가 업데이트되었음을 나타냅니다.

## 설명자 삭제 {#delete}

경우에 따라 [!DNL Schema Registry]에서 정의한 설명자를 제거해야 합니다. 이 작업은 제거할 설명자의 `@id`을 참조하는 DELETE 요청을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 삭제할 설명자의 `@id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(컨텐츠 없음) 및 빈 본문을 반환합니다.

설명자가 삭제되었는지 확인하려면 설명자 `@id`에 대해 [조회 요청](#lookup)을 수행할 수 있습니다. 설명자가 [!DNL Schema Registry]에서 제거되었기 때문에 응답에서 HTTP 상태 404(찾을 수 없음)를 반환합니다.

## 부록

다음 섹션에서는 [!DNL Schema Registry] API에서 설명자를 사용하는 작업에 대한 추가 정보를 제공합니다.

### 설명자 정의 {#defining-descriptors}

다음 섹션에서는 각 유형의 설명자를 정의하는 데 필요한 필드를 비롯하여 사용 가능한 설명자 유형에 대한 개요를 제공합니다.

#### ID 설명자

ID 설명자는 &quot;[!UICONTROL sourceSchema]&quot;의 &quot;[!UICONTROL sourceProperty]&quot;가 [Adobe Experience Platform Identity Service](../../identity-service/home.md)에서 설명한 대로 [!DNL Identity] 필드임을 나타냅니다.

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
| `@type` | 정의되는 설명자의 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | ID가 될 특정 속성의 경로입니다. 경로는 &quot;/&quot;로 시작해야 하며 하나로 끝나지 않습니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;를 사용) |
| `xdm:namespace` | ID 네임스페이스의 `id` 또는 `code` 값. 네임스페이스 목록은 [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service)을 사용하여 찾을 수 있습니다. |
| `xdm:property` | 사용된 `xdm:namespace`에 따라 `xdm:id` 또는 `xdm:code` 중 하나를 선택합니다. |
| `xdm:isPrimary` | 선택적 부울 값입니다. true이면 는 필드를 기본 ID로 나타냅니다. 스키마에는 기본 ID가 하나만 포함될 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

#### 이름 설명자

친숙한 이름 설명자를 사용하면 사용자가 코어 라이브러리 스키마 필드의 `title`, `description` 및 `meta:enum` 값을 수정할 수 있습니다. 특히 조직에 관련된 정보를 포함하는 것으로 레이블을 지정할 &quot;eVar&quot; 및 기타 &quot;일반&quot; 필드를 사용할 때 유용합니다. UI에서는 이러한 필드를 사용하여 보다 친숙한 이름을 표시하거나 친숙한 이름이 있는 필드만 표시할 수 있습니다.

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
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의되는 설명자의 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | ID가 될 특정 속성의 경로입니다. 경로는 &quot;/&quot;로 시작해야 하며 하나로 끝나지 않습니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;를 사용) |
| `xdm:title` | 제목 사례에 작성된 이 필드에 표시할 새 제목입니다. |
| `xdm:description` | 선택적 설명을 제목과 함께 추가할 수 있습니다. |
| `meta:enum` | `xdm:sourceProperty`으로 표시된 필드가 문자열 필드인 경우 `meta:enum` UI에서 필드에 대해 권장되는 값 목록을 결정합니다. [!DNL Experience Platform] `meta:enum` 은 열거형을 선언하지 않거나 XDM 필드에 대한 데이터 유효성 검사를 제공하지 않습니다.<br><br>Adobe에 의해 정의된 코어 XDM 필드에만 사용해야 합니다. 소스 속성이 조직에서 정의한 사용자 정의 필드인 경우 대신 필드의 상위 리소스에 대한 PATCH 요청을 통해 필드의 `meta:enum` 속성을 직접 편집해야 합니다. |

{style=&quot;table-layout:auto&quot;}

#### 관계 설명자

관계 설명자는 `sourceProperty` 및 `destinationProperty`에 설명된 속성에 키 지정된 두 개의 다른 스키마 간의 관계를 설명합니다. 자세한 내용은 [두 스키마 간의 관계 정의 자습서](../tutorials/relationship-api.md)를 참조하십시오.

```json
{
  "@type": "xdm:descriptorOneToOne",
  "xdm:sourceSchema":
    "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/parentField/subField",
  "xdm:destinationSchema": 
    "https://ns.adobe.com/{TENANT_ID}/schemas/78bab6346b9c5102b60591e15e75d254",
  "xdm:destinationVersion": 1,
  "xdm:destinationProperty": "/parentField/subField"
}
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 정의되는 설명자의 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | 관계가 정의된 소스 스키마의 필드에 대한 경로입니다. &quot;/&quot;로 시작해야 하며 하나로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;). |
| `xdm:destinationSchema` | 이 설명자가 관계를 정의하는 대상 스키마의 `$id` URI입니다. |
| `xdm:destinationVersion` | 대상 스키마의 주 버전입니다. |
| `xdm:destinationProperty` | 대상 스키마 내의 대상 필드에 대한 선택적 경로입니다. 이 속성을 생략하면 대상 필드는 일치하는 참조 ID 설명자를 포함하는 모든 필드에 의해 추론됩니다(아래 참조). |

{style=&quot;table-layout:auto&quot;}


#### 참조 ID 설명자

참조 ID 설명자는 스키마 필드의 기본 ID에 대한 참조 컨텍스트를 제공하여 다른 스키마의 필드에서 참조할 수 있습니다. 참조 설명자를 적용하려면 먼저 필드에 ID 설명자로 레이블을 지정해야 합니다.

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
| `@type` | 정의되는 설명자의 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | 설명자가 정의되는 소스 스키마의 필드에 대한 경로입니다. &quot;/&quot;로 시작해야 하며 하나로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;). |
| `xdm:identityNamespace` | 소스 속성에 대한 ID 네임스페이스 코드입니다. |
