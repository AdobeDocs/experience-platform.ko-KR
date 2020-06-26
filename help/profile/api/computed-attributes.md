---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로필 API 개발자 가이드
topic: guide
translation-type: tm+mt
source-git-commit: d464a6b4abd843f5f8545bc3aa8000f379a86c6d
workflow-type: tm+mt
source-wordcount: '2431'
ht-degree: 1%

---


# (알파) 계산된 특성 끝점

>[!IMPORTANT]
>The computed attribute functionality outlined in this document is currently in alpha and is not available to all users. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 프로필 수준에서 작동합니다. 즉, 모든 레코드와 이벤트에 대한 값을 합산할 수 있습니다.

계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성이나 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 시간 또는 애플리케이션 열기 횟수와 같은 문제와 관련된 질문에 쉽게 응답할 수 있습니다.

이 안내서는 Adobe Experience Platform 내에서 계산된 특성을 더 잘 이해할 수 있도록 도움을 드리며 종단점을 사용하여 기본 CRUD 작업을 수행하기 위한 샘플 API 호출을 포함합니다 `/config/computedAttributes` .

## 시작하기

이 안내서에서 사용되는 API 끝점은 [실시간 고객 프로필 API의 일부입니다](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). 계속하기 전에 [시작하기 가이드](getting-started.md) (관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서)와 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 계산된 속성 이해

Adobe Experience Platform을 사용하면 실시간 고객 프로파일을 생성하기 위해 다양한 소스의 데이터를 손쉽게 가져와 병합할 수 있습니다. 각 프로필에는 고객의 연락처 정보, 선호도, 구매 내역 등 개인 정보와 관련된 중요한 정보가 포함되어 있으므로 고객의 전체 상황을 파악할 수 있습니다.

프로필에서 수집된 일부 정보는 데이터 필드를 직접 읽을 때 쉽게 이해할 수 있는 반면(예: &quot;이름&quot;) 다른 데이터는 정보를 생성하기 위해 여러 계산을 수행하거나 다른 필드 및 값에 의존해야 합니다(예: &quot;라이프타임 구매 합계&quot;). 이 데이터를 한 눈에 쉽게 파악할 수 있도록 Platform을 사용하면 이러한 참조 및 계산을 자동으로 수행하는 **계산된 속성을** 만들어 적절한 필드에 값을 반환할 수 있습니다.

Computed attributes include creating an expression, or &quot;rule&quot;, that operates on incoming data and stores the resulting value in a profile attribute or event. 표현식을 여러 가지 방법으로 정의할 수 있으므로 규칙이 들어오는 이벤트, 들어오는 이벤트 및 프로필 데이터 또는 들어오는 이벤트, 프로필 데이터 및 내역 이벤트만을 평가하도록 지정할 수 있습니다.

### 사용 사례

Use cases for computed attributes can range from simple calculations to very complex references. 다음은 계산된 속성에 대한 몇 가지 사용 사례입니다.

1. **Percentages:** A simple computed attribute could include taking two numeric fields on a record and dividing them to create a percentage. For example, you could take the total number of emails sent to an individual and divide it by the number of emails the individual opens. Looking at the resulting computed attribute field would quickly show the percentage of total emails opened by the individual.
1. **애플리케이션 사용:** 다른 예로는 사용자가 애플리케이션을 연 횟수를 집계하는 기능이 있습니다. By tracking the total number of application opens, based on individual open events, you could deliver special offers or messages to users on their 100th open, encouraging deeper engagement with your brand.
1. **Lifetime values:** Gathering running totals, such as a lifetime purchase value for a customer, can be very difficult. This requires updating the historic total each time a new purchase event occurs. 계산된 속성을 사용하면 고객과 관련된 각 성공적인 구매 이벤트에 따라 자동으로 업데이트되는 단일 필드에서 라이프타임 값을 유지하여 보다 쉽게 이 작업을 수행할 수 있습니다.

## 계산된 속성 구성

계산된 속성을 구성하려면 먼저 계산된 속성 값이 포함될 필드를 식별해야 합니다. 이 필드는 혼합을 사용하여 기존 스키마에 필드를 추가하거나 스키마 내에 이미 정의된 필드를 선택하여 만들 수 있습니다.

>[!NOTE]
>계산된 속성은 Adobe에서 정의한 믹스의 필드에 추가할 수 없습니다. 필드는 `tenant` 네임스페이스 내에 있어야 합니다. 즉, 스키마를 정의하고 추가하는 필드여야 합니다.

계산된 속성 필드를 성공적으로 정의하려면 스키마를 프로필에 대해 활성화해야 하며 스키마를 기반으로 하는 클래스에 대한 조합 스키마의 일부로 나타나야 합니다. 프로필 사용 가능한 스키마 및 조합에 대한 자세한 내용은 프로필 스키마 [활성화 및 조합 스키마 보기에 대한 스키마 부여에 대한 스키마 레지스트리 개발자 가이드 섹션](../../xdm/api/getting-started.md)을 참조하십시오. It is also recommended to review the [section on unions](../../xdm/schema/composition.md) in the schema composition basics documentation.

이 자습서의 워크플로우는 프로필 사용 스키마를 사용하며, 계산된 속성 필드가 포함된 새 혼합을 정의하고 올바른 네임스페이스인지 확인하는 단계를 따릅니다. 프로필 사용 스키마 내의 올바른 네임스페이스에 있는 필드가 이미 있는 경우 계산된 속성을 [만드는 단계를 직접 진행할 수 있습니다](#create-a-computed-attribute).

### View a schema

다음 단계는 Adobe Experience Platform 사용자 인터페이스를 사용하여 스키마를 찾고, 혼합을 추가하고, 필드를 정의하는 단계입니다. 스키마 레지스트리 API를 사용하려면 [스키마 레지스트리 개발자 안내서를](../../xdm/api/getting-started.md) 참조하여 믹스를 만들고, 스키마에 혼합을 추가하고, 실시간 고객 프로필과 함께 사용할 스키마를 활성화하는 방법에 대한 단계를 확인하십시오.

사용자 인터페이스에서 왼쪽 레일의 **스키마** 를 클릭하고 *찾아보기* 탭의 검색 막대를 사용하여 업데이트할 스키마를 빠르게 찾습니다.

![](../images/computed-attributes/Schemas-Browse.png)

스키마를 찾으면 해당 이름을 클릭하여 스키마를 편집할 수 있는 스키마 편집기를 엽니다.

![](../images/computed-attributes/Schema-Editor.png)

### 혼합 만들기

새 혼합을 만들려면 편집기 **왼쪽** 의 *[* 컴포지션 *] 섹션에서* [믹싱] 옆에있는 [추가]를 클릭합니다. 그러면 기존 믹스를 볼 수 있는 **믹신** 추가 대화 상자가 열립니다. 새 믹스를 정의하려면 [새 믹싱 **만들기** ]의 라디오 단추를 클릭합니다.

믹싱에 이름과 설명을 지정하고, 완료되면 믹신 **추가를** 클릭합니다.

![](../images/computed-attributes/Add-mixin.png)

### 스키마에 계산된 속성 필드 추가

이제 새 믹싱이 [컴포지션] 아래의 [ *믹싱* ] 섹션에 *표시됩니다*. 믹싱의 이름과 여러 필드 **추가** 단추가 편집기의 *구조* 섹션에 나타납니다.

최상위 **필드를 추가하려면 스키마 이름 옆에 있는 필드** 추가를 선택하거나, 원하는 스키마 내의 아무 곳에나 필드를 추가하도록 선택할 수 있습니다.

필드 **추가를 클릭하면** 테넌트 ID에 대해 이름이 지정된 새 개체가 열리고 필드가 올바른 네임스페이스에 있음을 보여줍니다. 해당 개체 내에 *새 필드가* 나타납니다. 계산된 속성을 정의할 필드가 있는 경우입니다.

![](../images/computed-attributes/New-field.png)

### 필드 구성

편집기의 오른쪽에 있는 *필드 속성* 섹션을 사용하여 이름, 표시 이름, 유형 등 새 필드에 필요한 정보를 제공합니다.

>[!NOTE]
>필드의 유형은 계산된 속성 값과 같은 형식이어야 합니다. 예를 들어 계산된 속성 값이 문자열인 경우 스키마에 정의된 필드는 문자열이어야 합니다.

완료되면 **적용** 을 클릭하고 *필드 이름과 해당 유형이 편집기의* 구조섹션에나타납니다.

![](../images/computed-attributes/Apply.png)

### 프로필에 대한 스키마 사용

계속하기 전에 스키마에 대해 프로필이 활성화되어 있는지 확인하십시오. [스키마 속성] 탭이 나타나도록 편집기의 *구조* 섹션에서 *스키마* 이름을클릭합니다. 프로필 **슬라이더가 파란색이면** 프로필에 대해 스키마가 활성화됩니다.

>[!NOTE]
>프로필에 대한 스키마 활성화는 실행 취소할 수 없으므로 슬라이더를 활성화한 후 클릭하면 비활성화될 위험이 없습니다.

![](../images/computed-attributes/Profile.png)

이제 **저장을** 클릭하여 업데이트된 스키마를 저장하고 API를 사용하여 나머지 튜토리얼을 계속 진행할 수 있습니다.

### 계산된 속성 만들기 {#create-a-computed-attribute}

계산된 속성 필드가 확인되고 스키마가 프로필에 대해 활성화되어 있는지 확인하면 이제 계산된 속성을 구성할 수 있습니다.

만들려는 계산된 속성의 세부 사항을 포함하는 요청 본문으로 끝점에 POST 요청을 `/config/computedAttributes` 하는 것으로 시작합니다.

**API 형식**

```http
POST /config/computedAttributes
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 속성 | 설명 |
|---|---|
| `name` | 계산된 속성 필드의 이름입니다. |
| `path` | 계산된 속성이 포함된 필드의 경로입니다. 이 경로는 스키마의 `properties` 특성 내에 있으며 경로에 필드 이름을 포함하지 않아야 합니다. 패스를 작성할 때는 여러 수준의 속성을 생략합니다 `properties` . |
| `{TENANT_ID}` | 테넌트 ID에 익숙하지 않은 경우 [스키마 레지스트리 개발자 안내서에서 테넌트 ID를 찾는 단계를 참조하십시오](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 IMS 내에서 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 여러 계산된 속성이 정의된 경우에 특히 유용합니다. |
| `expression.value` | 유효한 PQL(프로필 쿼리 언어) 식입니다. PQL 및 지원되는 쿼리 링크에 대한 자세한 내용은 [PQL 개요를 참조하십시오](../../segmentation/pql/overview.md). |
| `schema.name` | 계산된 속성 필드가 포함된 스키마를 기반으로 하는 클래스입니다. 예: `_xdm.context.experienceevent` for a schema based on the XDM ExperienceEvent class. |

**응답**

성공적으로 생성된 계산된 속성은 HTTP Status 200(OK) 및 새로 만든 계산된 속성의 세부 정보가 포함된 응답 본문을 반환합니다. 이러한 세부 사항에는 다른 API 작업 동안 계산된 속성을 참조하는 데 사용할 수 `id` 있는 고유한 읽기 전용 시스템이 생성됩니다.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| 속성 | 설명 |
|---|---|
| `id` | 다른 API 작업 동안 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID입니다. |
| `imsOrgId` | 계산된 속성과 관련된 IMS 조직은 요청에 전송된 값과 일치해야 합니다. |
| `sandbox` | 샌드박스 객체에는 계산된 속성이 구성된 샌드박스의 세부 사항이 포함됩니다. 이 정보는 요청에서 전송된 샌드박스 헤더에서 가져옵니다. 자세한 내용은 [샌드박스 개요를 참조하십시오](../../sandboxes/home.md). |
| `positionPath` | 요청에서 전송된 필드 `path` 로 분해된 항목이 포함된 배열. |
| `returnSchema.meta:xdmType` | 계산된 속성이 저장되는 필드의 유형입니다. |
| `definedOn` | 계산된 속성이 정의된 결합 스키마를 표시하는 배열. 조합 스키마당 하나의 객체를 포함합니다. 즉, 계산된 속성이 다른 클래스를 기반으로 여러 스키마에 추가된 경우 배열 내에 여러 개의 객체가 있을 수 있습니다. |
| `active` | 계산된 속성이 현재 활성 상태인지 여부를 표시하는 부울 값입니다. 기본값은 입니다 `true`. |
| `type` | 만들어진 리소스 유형인 이 경우 &quot;ComputedAttribute&quot;가 기본값입니다. |
| `createEpoch` 및 `updateEpoch` | 계산된 속성이 각각 만들어지고 마지막으로 업데이트된 시간입니다. |


## 계산된 속성에 액세스

API를 사용하여 계산된 속성을 사용하는 경우 조직에서 정의한 계산된 속성에 액세스하는 두 가지 옵션이 있습니다. 첫 번째 방법은 모든 계산된 속성을 나열하는 것이며, 두 번째 방법은 고유한 계산된 속성을 보는 것입니다 `id`.

계산된 모든 속성을 나열하고 특정 계산된 속성을 보는 단계는 다음 섹션에 요약되어 있습니다.

### 계산된 속성 목록 {#list-computed-attributes}

IMS 조직은 여러 개의 계산된 속성을 만들 수 있으며, 종단점에 대한 GET 요청을 수행하면 조직의 모든 기존 계산된 특성을 나열할 수 `/config/computedAttributes` 있습니다.

**API 형식**

```http
GET /config/computedAttributes
```

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답에는 페이지의 총 계산된 속성( `_page` )과 계산된 속성 수를 제공하는`totalCount`속성이 포함됩니다(`pageSize`).

응답에는 하나 이상의 개체로 구성된 `children` 배열이 포함되며, 각 배열은 하나의 계산된 속성의 세부 정보를 포함합니다. 조직에 계산된 속성이 없으면 0(영) `totalCount` 이 `pageSize` 되고 `children` 배열이 비어 있게 됩니다.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| 속성 | 설명 |
|---|---|
| `_page.totalCount` | IMS 조직에서 정의한 계산된 속성의 총 수입니다. |
| `_page.pageSize` | 이 결과 페이지에서 반환되는 계산된 속성의 수입니다. 이 `pageSize` `totalCount`가 같은 경우, 결과의 한 페이지만이 있고 모든 계산된 속성이 반환되었음을 의미합니다. 같지 않으면 액세스할 수 있는 추가 결과 페이지가 있습니다. See `_links.next` for details. |
| `children` | 하나 이상의 개체로 구성된 배열이며, 각각 단일 계산된 속성의 세부 정보가 들어 있습니다. 계산된 속성이 정의되지 않은 경우 `children` 배열이 비어 있습니다. |
| `id` | 계산된 속성이 생성될 때 자동으로 할당된 읽기 전용 시스템 생성 값. 계산된 속성 개체의 구성 요소에 대한 자세한 내용은 이 자습서 앞의 계산된 속성 [을](#create-a-computed-attribute) 만드는 섹션을 참조하십시오. |
| `_links.next` | 계산된 속성의 단일 페이지가 반환되는 경우 위 샘플 응답에 표시된 것처럼 빈 개체 `_links.next` 가 됩니다. 조직에 많은 계산된 속성이 있는 경우 해당 값에 대한 GET 요청을 수행하여 액세스할 수 있는 여러 페이지에서 `_links.next` 반환됩니다. |

### 계산된 속성 보기 {#view-a-computed-attribute}

종단점에 대한 GET 요청을 만들고 요청 경로에 계산된 속성 ID를 포함하여 특정 계산된 속성을 볼 수도 있습니다. `/config/computedAttributes`

**API 형식**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 보려는 계산된 속성의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## 계산된 속성 업데이트

기존 계산된 속성을 업데이트해야 하는 경우 종단점에 대한 PATCH 요청을 수행하고 요청 경로에서 업데이트하려는 계산된 속성의 ID를 포함하여 이 작업을 수행할 수 있습니다. `/config/computedAttributes`

**API 형식**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 업데이트할 계산된 속성의 ID입니다. |

**요청**

이 요청에서는 [JSON 패치 형식을](http://jsonpatch.com/) 사용하여 &quot;표현식&quot; 필드의 &quot;값&quot;을 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 속성 | 설명 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 유효한 PQL(프로필 쿼리 언어) 식입니다. PQL 및 지원되는 쿼리 링크에 대한 자세한 내용은 [PQL 개요를 참조하십시오](../../segmentation/pql/overview.md). |

**응답**

업데이트가 성공하면 HTTP Status 204(콘텐츠 없음) 및 빈 응답 본문을 반환합니다. 업데이트가 성공했는지 확인하려면 GET 요청을 수행하여 계산된 속성을 ID로 볼 수 있습니다.

## 계산된 속성 삭제

API를 사용하여 계산된 속성을 삭제할 수도 있습니다. 이것은 종단점에 DELETE 요청을 하고 요청 경로에서 삭제하려는 계산된 속성의 ID를 포함하여 수행됩니다. `/config/computedAttributes`

>[!N참고]
>계산된 특성을 둘 이상의 스키마에서 사용 중일 수 있으며 DELETE 작업을 취소할 수 없으므로 삭제할 때는 주의하십시오.

**API 형식**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 삭제할 계산된 속성의 ID입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**응답**

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. 삭제를 성공적으로 확인하려면 GET 요청을 수행하여 계산된 속성을 ID로 조회할 수 있습니다. 속성이 삭제된 경우 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 다음 단계

이제 계산된 속성의 기본 사항에 대해 배웠으므로 조직에 대해 이러한 속성을 정의할 수 있습니다.