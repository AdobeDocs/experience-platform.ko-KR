---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 설명자
topic: developer guide
translation-type: tm+mt
source-git-commit: c8cc57a8629f04c7af68b6f5cfee365527caa3c1
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 1%

---


# 설명자

스키마는 데이터 엔티티의 정적 보기를 정의하지만 이러한 스키마(예: 데이터 집합)를 기반으로 한 데이터가 서로 관련될 수 있는 방법에 대한 구체적인 세부 정보를 제공하지 않습니다. Adobe Experience Platform을 사용하면 설명자를 사용하여 스키마에 대한 이러한 관계 및 기타 해석 메타데이터를 설명할 수 있습니다.

스키마 설명자는 테넌트 수준 메타데이터로서, 이는 IMS에 고유함을 의미합니다. 조직 및 모든 설명자 작업은 테넌트 컨테이너에서 수행됩니다.

각 스키마에는 하나 이상의 스키마 설명자 개체가 적용될 수 있습니다. 각 스키마 설명자 엔터티에는 설명자 `@type` 와 설명자가 적용되는 `sourceSchema` 항목이 포함됩니다. 설명자가 적용되면 스키마를 사용하여 만든 모든 데이터 세트에 적용됩니다.

이 문서에서는 설명자에 대한 예제 API 호출, 사용 가능한 설명자의 전체 목록 및 각 유형을 정의하는 데 필요한 필드를 제공합니다.

>[!NOTE] 설명자는 고유한 수락 헤더가 필요하며 `xed` , 그렇지 않으면 스키마 레지스트리 `xdm`의 다른 위치에서 사용되는 헤더 허용과 매우 비슷합니다. 아래 샘플 호출에는 적절한 수락 머리글이 포함되었지만 정확한 헤더가 사용되고 있는지 확인하기 위해 특별히 주의하십시오.

## 목록 설명자

단일 GET 요청을 사용하여 조직에서 정의한 모든 설명자 목록을 반환할 수 있습니다.

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

응답 형식은 요청에서 전송된 수락 헤더에 따라 다릅니다. 끝점이 `/descriptors` 스키마 레지스트리 API의 다른 모든 끝점과 다른 수락 헤더를 사용합니다.

설명자 승인 헤더 `xed` 를 다음으로 대체하고 설명자 고유의 `xdm``link` 옵션을 제공합니다.

| 수락 | 설명 |
| -------|------------ |
| `application/vnd.adobe.xdm-id+json` | 설명자 ID 배열을 반환합니다. |
| `application/vnd.adobe.xdm-link+json` | 설명자 API 경로 배열을 반환합니다. |
| `application/vnd.adobe.xdm+json` | 확장된 설명자 개체의 배열을 반환합니다. |

**응답**

응답에는 정의된 설명자가 있는 각 설명자 유형에 대한 배열이 포함됩니다. 즉, 정의된 특정 설명자가 없으면 레지스트리에서 해당 설명자 유형에 대한 빈 배열을 반환하지 않습니다 `@type` .

수락 `link` 헤더를 사용하는 경우 각 설명자가 `/{CONTAINER}/descriptors/{DESCRIPTOR_ID}`

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

## 설명자 찾기

특정 설명자의 세부 정보를 보려면 설명자를 사용하여 개별 설명자를 조회(GET)할 수 있습니다 `@id`.

**API 형식**

```http
GET /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 조회할 설명자 `@id` 의 이름입니다. |

**요청**

설명자는 버전이 관리되지 않으므로 조회 요청에서 수락 헤더가 필요하지 않습니다.

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/f3a1dfa38a4871cf4442a33074c1f9406a593407 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답으로 설명자의 세부 정보 `@type` 와 설명자 유형 `sourceSchema`에 따라 다른 추가 정보를 반환합니다. 반환된 설명자가 요청에 `@id` 제공된 설명자와 일치해야 `@id` 합니다.

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

## 설명자 만들기

스키마 레지스트리를 사용하면 여러 가지 다른 설명자 유형을 정의할 수 있습니다. 각 설명자 유형에는 POST 요청에서 전송할 고유한 특정 필드가 필요합니다. 설명자 [정의](#defining-descriptors)설명자의 부록 섹션에서 설명자의 전체 목록과 이를 정의하는 데 필요한 필드를 사용할 수 있습니다.

**API 형식**

```http
POST /tenant/descriptors
```

**요청**

다음 요청은 샘플 스키마의 &quot;이메일 주소&quot; 필드에 ID 설명자를 정의합니다. 그러면 경험 플랫폼이 이메일 주소를 식별자로 사용하여 개인 정보를 연결하는 데 도움이 됩니다.

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

성공적인 응답은 HTTP 상태 201(작성됨)과 새로 만든 설명자를 비롯하여 세부 정보를 반환합니다 `@id`. 스키마 레지스트리에서 할당한 읽기 전용 필드 `@id` 로, API의 설명자를 참조하는 데 사용됩니다.

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

## 업데이트 설명자

요청 경로에서 업데이트하려는 설명자의 `@id` 를 참조하는 PUT 요청을 수행하여 설명자를 업데이트할 수 있습니다.

**API 형식**

```http
PUT /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 업데이트할 설명자 `@id` 의 이름입니다. |

**요청**

이 요청은 _설명자를 다시 작성하므로 요청 본문에는 해당 유형의 설명자를 정의하는 데 필요한 모든 필드가 포함되어야 합니다_ . 즉, 설명자를 업데이트할 요청 페이로드(PUT)는 동일한 유형의 설명자를 만들기 위한 페이로드(POST)와 동일합니다.

이 예에서 ID 설명자가 다른 `xdm:sourceProperty` (&quot;휴대폰&quot;)을 참조하고 이 설명자를 &quot;전화&quot; `xdm:namespace` 로 변경하도록 업데이트됩니다.

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

속성 `xdm:namespace` 과 속성 액세스 방법 `xdm:property`등 속성에 대한 세부 사항은 설명자 [정의](#defining-descriptors)부록 섹션에서 확인할 수 있습니다.

**응답**

성공적인 응답은 HTTP 상태 201(작성됨)과 업데이트된 설명자 `@id` 의 값(요청에서 전송된 것과 일치해야 함)을 `@id` 반환합니다.

```JSON
{
    "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

설명자를 보기 위해 조회(GET) 요청을 수행하면 이제 필드가 PUT 요청에 전송된 변경 사항을 반영하도록 업데이트되었음을 알 수 있습니다.

## 설명자 삭제

스키마 레지스트리에서 정의한 설명자를 제거해야 하는 경우가 있습니다. 이 작업은 제거할 설명자의 DELETE 요청 `@id` 을 수행하여 수행됩니다.

**API 형식**

```http
DELETE /tenant/descriptors/{DESCRIPTOR_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DESCRIPTOR_ID}` | 삭제할 설명자 `@id` 의 이름입니다. |

**요청**

설명자를 삭제할 때는 헤더를 승인하지 않아도 됩니다.

```SHELL
curl -X DELETE \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors/ca921946fb5281cbdb8ba5e07087486ce531a1f2  \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 HTTP 상태 204(콘텐츠 없음) 및 빈 본문을 반환합니다.

설명자가 삭제되었는지 확인하려면 설명자에 대해 조회 요청을 수행할 수 있습니다 `@id`. 설명자가 스키마 레지스트리에서 제거되었기 때문에 응답이 HTTP 상태 404(찾을 수 없음)를 반환합니다.

## 부록

다음 섹션에서는 스키마 레지스트리 API의 설명자 작업에 대한 추가 정보를 제공합니다.

### 설명자 정의

다음 섹션에서는 각 유형의 설명자를 정의하는 데 필요한 필드를 비롯하여 사용 가능한 설명자 유형에 대한 개요를 제공합니다.

#### ID 설명자

ID 설명자는 &quot;sourceSchema&quot;의 &quot;sourceProperty&quot;가 [Adobe Experience Platform Identity Service에 설명된 ID 필드임을 알립니다](../../identity-service/home.md).

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
| `@type` | 정의할 설명자 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | ID가 될 특정 속성의 경로입니다. 경로는 &quot;/&quot;로 시작하고 하나로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;를 사용). |
| `xdm:namespace` | ID 네임스페이스의 `id` 또는 `code` 값입니다. ID 서비스 API를 사용하여 네임스페이스 목록을 [찾을 수 있습니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml). |
| `xdm:property` | 또는 `xdm:id` 중 하나 `xdm:code`는, 사용한 것에 따라 `xdm:namespace` 달라집니다. |
| `xdm:isPrimary` | 선택적 부울 값입니다. true이면 필드를 기본 ID로 나타냅니다. 스키마에는 하나의 기본 ID만 포함될 수 있습니다. |

#### 친숙한 이름 설명자

친숙한 이름 설명자를 사용하면 사용자가 핵심 라이브러리 스키마 필드 `title`의, `description`및 `meta:enum` 값을 수정할 수 있습니다. 특히 &quot;eVar&quot; 및 기타 &quot;일반&quot; 필드로 레이블을 지정할 때 조직 고유의 정보를 포함하도록 유용합니다. UI에서는 이러한 이름을 사용하여 보다 친숙한 이름을 표시하거나 친숙한 이름을 가진 필드만 표시할 수 있습니다.

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
| `@type` | 정의할 설명자 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | ID가 될 특정 속성의 경로입니다. 경로는 &quot;/&quot;로 시작하고 하나로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;를 사용). |
| `xdm:title` | 제목 사례에 작성된 이 필드에 표시할 새 제목입니다. |
| `xdm:description` | 선택적인 설명은 제목과 함께 추가할 수 있습니다. |
| `meta:enum` | 로 표시된 필드가 문자열 필드 `xdm:sourceProperty` 인 경우, 경험 플랫폼 UI에 있는 필드에 대해 제안된 값의 목록을 `meta:enum` 결정합니다. 열거형을 선언하거나 XDM 필드에 대한 데이터 유효성 검사를 제공하지 `meta:enum` 않는다는 점에 유의하십시오.<br><br>Adobe에서 정의한 핵심 XDM 필드에만 사용해야 합니다. 소스 속성이 조직에서 정의한 사용자 지정 필드인 경우 대신 PUT 요청을 통해 필드 `meta:enum` 속성을 직접 [편집해야 합니다](./update-resource.md). |

#### 관계 설명자

관계 설명자는 및 `sourceProperty` 에 설명된 속성에 따라 서로 다른 두 스키마 간의 관계를 설명합니다 `destinationProperty`. 자세한 내용은 두 스키마 [의 관계를 정의하는 방법에 대한 자습서를](../tutorials/relationship-api.md) 참조하십시오.

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
| `@type` | 정의할 설명자 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | 관계가 정의된 소스 스키마의 필드 경로입니다. &quot;/&quot;로 시작하고 하나로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;). |
| `xdm:destinationSchema` | 이 설명자가 관계를 정의하는 대상 스키마의 `$id` URI입니다. |
| `xdm:destinationVersion` | 대상 스키마의 주 버전입니다. |
| `xdm:destinationProperty` | 대상 스키마 내의 대상 필드에 대한 선택적 경로입니다. 이 속성을 생략하면 일치하는 참조 ID 설명자를 포함하는 모든 필드에서 대상 필드를 유추할 수 있습니다(아래 참조). |


#### 참조 ID 설명자

참조 ID 설명자는 스키마 필드에 참조 컨텍스트를 제공하여 대상 스키마의 기본 ID 필드에 연결할 수 있습니다. 참조 설명자를 필드에 적용하려면 먼저 필드에 ID 설명자로 레이블이 지정되어 있어야 합니다.

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
| `@type` | 정의할 설명자 유형입니다. |
| `xdm:sourceSchema` | 설명자가 정의된 스키마의 `$id` URI입니다. |
| `xdm:sourceVersion` | 소스 스키마의 주 버전입니다. |
| `xdm:sourceProperty` | 설명자가 정의된 소스 스키마의 필드 경로입니다. &quot;/&quot;로 시작하고 하나로 끝나지 않아야 합니다. 경로에 &quot;속성&quot;을 포함하지 마십시오(예: &quot;/properties/personalEmail/properties/address&quot; 대신 &quot;/personalEmail/address&quot;). |
| `xdm:identityNamespace` | 소스 속성에 대한 ID 네임스페이스 코드입니다. |