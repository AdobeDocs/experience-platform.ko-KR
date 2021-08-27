---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 특성 API 끝점
topic-legacy: guide
type: Documentation
description: Adobe Experience Platform에서 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다. 이 안내서에서는 실시간 고객 프로필 API를 사용하여 계산된 속성을 생성, 보기, 업데이트 및 삭제하는 방법을 보여줍니다.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
source-git-commit: 4c544170636040b8ab58780022a4c357cfa447de
workflow-type: tm+mt
source-wordcount: '2272'
ht-degree: 2%

---

# (알파) 계산된 특성 API 끝점

>[!IMPORTANT]
>
>이 문서에 요약된 계산된 특성 기능은 현재 알파 상태이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다. 이 안내서에는 `/computedAttributes` 종단점을 사용하여 기본 CRUD 작업을 수행하기 위한 샘플 API 호출이 포함되어 있습니다.

계산된 속성에 대해 자세히 알려면 [계산된 속성 개요](overview.md)를 읽어 보십시오.

## 시작하기

이 안내서에 사용된 API 엔드포인트는 [실시간 고객 프로필 API](https://www.adobe.com/go/profile-apis-en)의 일부입니다.

계속하기 전에 [프로필 API 시작 안내서](../api/getting-started.md)에서 권장 설명서에 대한 링크, 이 문서에 표시되는 샘플 API 호출 읽기에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 계산된 속성 필드 구성

계산된 속성을 만들려면 먼저 계산된 속성 값을 저장할 스키마의 필드를 식별해야 합니다.

스키마에 계산된 속성 필드를 만들려면 [계산된 속성 구성](configure-api.md)에 대한 설명서를 참조하십시오.

>[!WARNING]
>
>API 안내서를 계속하려면 계산된 속성 필드가 구성되어 있어야 합니다.

## 계산된 속성 만들기 {#create-a-computed-attribute}

이제 프로필 활성화 스키마에 계산된 속성 필드를 정의하여 계산된 속성을 구성할 수 있습니다. 아직 이 작업을 수행하지 않았다면 [계산된 속성](configure-api.md) 설명서 구성에 설명된 작업 과정을 따르십시오.

계산된 속성을 만들려면 먼저 만들려는 계산된 속성의 세부 사항을 포함하는 요청 본문으로 `/config/computedAttributes` 종단점에 POST 요청을 합니다.

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
| `name` | 계산된 속성 필드의 이름(문자열)입니다. |
| `path` | 계산된 속성이 포함된 필드의 경로입니다. 이 경로는 스키마의 `properties` 속성 내에 있으며 경로에 필드 이름을 포함하지 않아야 합니다. 경로를 쓸 때 `properties` 속성의 여러 수준을 생략합니다. |
| `{TENANT_ID}` | 테넌트 ID에 익숙하지 않은 경우 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md#know-your-tenant_id)에서 테넌트 ID를 찾는 단계를 참조하십시오. |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 IMS 조직 내의 다른 사용자가 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 여러 계산된 속성이 정의된 경우에 특히 유용합니다. |
| `expression.value` | 유효한 [!DNL Profile Query Language] (PQL) 식입니다. 계산된 속성은 현재 다음 함수를 지원합니다. sum, count, min, max 및 boolean 샘플 표현식 목록은 [샘플 PQL 표현식](expressions.md) 설명서를 참조하십시오. |
| `schema.name` | 계산된 속성 필드를 포함하는 스키마의 기반이 되는 클래스입니다. 예: XDM ExperienceEvent 클래스를 기반으로 한 스키마에 대한 `_xdm.context.experienceevent` 입니다. |

**응답**

성공적으로 생성된 계산된 특성은 HTTP Status 200(OK) 및 새로 생성된 계산된 속성의 세부 정보를 포함하는 응답 본문을 반환합니다. 이러한 세부 사항에는 다른 API 작업 중 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 `id`이 포함됩니다.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
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
| `id` | 다른 API 작업 중 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID입니다. |
| `imsOrgId` | 계산된 속성과 관련된 IMS 조직 은 요청에서 전송된 값과 일치해야 합니다. |
| `sandbox` | sandbox 객체에는 계산된 속성이 구성된 샌드박스의 세부 정보가 포함되어 있습니다. 이 정보는 요청에 전송된 샌드박스 헤더에서 추출됩니다. 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오. |
| `positionPath` | 요청 시 전송된 필드에 대한 해체된 `path`이 포함된 배열입니다. |
| `returnSchema.meta:xdmType` | 계산된 속성이 저장되는 필드의 유형입니다. |
| `definedOn` | 계산된 속성이 정의된 결합 스키마를 표시하는 배열입니다. 조합 스키마당 하나의 개체를 포함합니다. 즉, 계산된 특성이 다른 클래스를 기반으로 한 여러 스키마에 추가된 경우 배열 내에 여러 개체가 있을 수 있습니다. |
| `active` | 계산된 속성이 현재 활성 상태인지 여부를 표시하는 부울 값입니다. 기본적으로 값은 `true`입니다. |
| `type` | 생성된 리소스의 유형이며, 이 경우 &quot;ComputedAttribute&quot;는 기본값입니다. |
| `createEpoch` 및 `updateEpoch` | 계산된 속성이 만들어진 시간과 마지막으로 업데이트된 시간입니다. |

## 기존 계산된 속성을 참조하는 계산된 속성을 만듭니다

기존 계산된 속성을 참조하는 계산된 속성을 만들 수도 있습니다. 이렇게 하려면 `/config/computedAttributes` 종단점에 POST 요청을 하는 것으로 시작하십시오. 요청 본문에 다음 예와 같이 `expression.value` 필드에 계산된 속성에 대한 참조가 포함됩니다.

**API 형식**

```http
POST /config/computedAttributes
```

**요청**

이 예에서는 두 개의 계산된 속성이 이미 만들어졌고 세 번째 속성을 정의하는 데 사용됩니다. 기존 계산된 속성은 다음과 같습니다.

* **`totalSpend`** : 고객이 사용한 총 달러 금액을 캡처합니다.
* **`countPurchases`** : 고객이 구매한 횟수를 카운트합니다.

아래 요청은 유효한 PQL을 사용하여 두 개의 기존 계산된 속성을 참조하여 새 `averageSpend` 계산된 속성을 계산합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| 속성 | 설명 |
|---|---|
| `name` | 계산된 속성 필드의 이름(문자열)입니다. |
| `path` | 계산된 속성이 포함된 필드의 경로입니다. 이 경로는 스키마의 `properties` 속성 내에 있으며 경로에 필드 이름을 포함하지 않아야 합니다. 경로를 쓸 때 `properties` 속성의 여러 수준을 생략합니다. |
| `{TENANT_ID}` | 테넌트 ID에 익숙하지 않은 경우 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md#know-your-tenant_id)에서 테넌트 ID를 찾는 단계를 참조하십시오. |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 IMS 조직 내의 다른 사용자가 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 여러 계산된 속성이 정의된 경우에 특히 유용합니다. |
| `expression.value` | 유효한 PQL 식입니다. 계산된 속성은 현재 다음 함수를 지원합니다. sum, count, min, max 및 boolean 샘플 표현식 목록은 [샘플 PQL 표현식](expressions.md) 설명서를 참조하십시오.<br/><br/>이 예제에서 표현식은 두 개의 기존 계산된 속성을 참조합니다. 계산된 속성이 정의된 스키마에 나타나는 계산된 속성의 `path` 및 `name`을 사용하여 속성을 참조합니다. 예를 들어 처음 참조된 계산된 속성의 `path`은 `_{TENANT_ID}.purchaseSummary`이고 `name`는 `totalSpend`입니다. |
| `schema.name` | 계산된 속성 필드를 포함하는 스키마의 기반이 되는 클래스입니다. 예: XDM ExperienceEvent 클래스를 기반으로 한 스키마에 대한 `_xdm.context.experienceevent` 입니다. |

**응답**

성공적으로 생성된 계산된 특성은 HTTP Status 200(OK) 및 새로 생성된 계산된 속성의 세부 정보를 포함하는 응답 본문을 반환합니다. 이러한 세부 사항에는 다른 API 작업 중 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 `id`이 포함됩니다.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| 속성 | 설명 |
|---|---|
| `id` | 다른 API 작업 중 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID입니다. |
| `imsOrgId` | 계산된 속성과 관련된 IMS 조직 은 요청에서 전송된 값과 일치해야 합니다. |
| `sandbox` | sandbox 객체에는 계산된 속성이 구성된 샌드박스의 세부 정보가 포함되어 있습니다. 이 정보는 요청에 전송된 샌드박스 헤더에서 추출됩니다. 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오. |
| `positionPath` | 요청 시 전송된 필드에 대한 해체된 `path`이 포함된 배열입니다. |
| `returnSchema.meta:xdmType` | 계산된 속성이 저장되는 필드의 유형입니다. |
| `definedOn` | 계산된 속성이 정의된 결합 스키마를 표시하는 배열입니다. 조합 스키마당 하나의 개체를 포함합니다. 즉, 계산된 특성이 다른 클래스를 기반으로 한 여러 스키마에 추가된 경우 배열 내에 여러 개체가 있을 수 있습니다. |
| `active` | 계산된 속성이 현재 활성 상태인지 여부를 표시하는 부울 값입니다. 기본적으로 값은 `true`입니다. |
| `type` | 생성된 리소스의 유형이며, 이 경우 &quot;ComputedAttribute&quot;는 기본값입니다. |
| `createEpoch` 및 `updateEpoch` | 계산된 속성이 만들어진 시간과 마지막으로 업데이트된 시간입니다. |

## 계산된 속성에 액세스

API를 사용하여 계산된 속성을 사용하여 작업하는 경우 조직에서 정의한 계산된 속성에 액세스하기 위한 두 가지 옵션이 있습니다. 첫 번째는 모든 계산된 속성을 나열하는 것이고 두 번째는 고유한 `id`으로 특정 계산된 속성을 보는 것입니다.

두 액세스 패턴에 대한 단계는 이 문서에 요약되어 있습니다. 시작하려면 다음 중 하나를 선택합니다.

* **[기존의 계산된 속성 모두 나열](#list-all-computed-attributes):**  조직에서 생성한 모든 기존 계산된 속성 목록을 반환합니다.
* **[특정 계산된 속성 보기](#view-a-computed-attribute):** 요청 중에 해당 ID를 지정하여 단일 계산된 속성의 세부 정보를 반환합니다.

### 모든 계산된 속성 나열 {#list-all-computed-attributes}

IMS 조직은 여러 계산된 속성을 만들 수 있으며 `/config/computedAttributes` 종단점에 대한 GET 요청을 수행하면 조직에 대한 기존의 모든 계산된 속성을 나열할 수 있습니다.

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

성공적인 응답에는 계산된 속성의 총 수(`totalCount`)와 페이지에서 계산된 속성의 수를 제공하는 `_page` 속성이 포함됩니다(`pageSize`).

또한, 상기 응답에는 하나 이상의 개체로 구성된 `children` 배열이 포함되어 있으며, 각각 하나의 계산된 속성의 세부 정보가 들어 있습니다. 조직에 계산된 속성이 없는 경우 `totalCount` 및 `pageSize`은 0(0)이 되고 `children` 배열은 비어 있습니다.

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
| `_page.totalCount` | IMS 조직에서 정의한 총 계산된 속성 수입니다. |
| `_page.pageSize` | 이 결과 페이지에서 반환되는 계산된 속성의 수입니다. `pageSize`이 `totalCount`과 동일한 경우, 결과 페이지가 하나만 있고 계산된 속성이 모두 반환되었음을 의미합니다. 같지 않으면 액세스할 수 있는 추가 결과 페이지가 있습니다. 자세한 내용은 `_links.next` 을 참조하십시오. |
| `children` | 하나 이상의 개체로 구성된 배열이며 각각 하나의 계산된 속성의 세부 정보가 포함됩니다. 계산된 속성이 정의되지 않은 경우 `children` 배열이 비어 있습니다. |
| `id` | 계산 속성을 만들 때 자동으로 계산된 속성에 지정된 고유한 읽기 전용 시스템 생성 값입니다. 계산된 특성 개체의 구성 요소에 대한 자세한 내용은 이 자습서의 [계산된 특성](#create-a-computed-attribute) 만들기 섹션을 참조하십시오. |
| `_links.next` | 계산된 속성의 단일 페이지가 반환되면 위의 샘플 응답에 표시된 대로 `_links.next`은 빈 객체인 것입니다. 조직에 많은 계산된 속성이 있는 경우 `_links.next` 값에 대한 GET 요청을 수행하여 액세스할 수 있는 여러 페이지에서 반환됩니다. |

### 계산된 속성 보기 {#view-a-computed-attribute}

`/config/computedAttributes` 종단점에 대한 GET 요청을 만들고 요청 경로에 계산된 속성 ID를 포함하여 특정 계산된 속성을 볼 수 있습니다.

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

## 계산된 특성 업데이트

기존 계산된 속성을 업데이트해야 하는 경우 이 작업은 `/config/computedAttributes` 종단점에 PATCH 요청을 수행하고 요청 경로에서 업데이트하려는 계산된 결과의 ID를 포함하여 수행할 수 있습니다.

**API 형식**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 업데이트할 계산된 속성의 ID입니다. |

**요청**

이 요청은 [JSON 패치 형식](http://jsonpatch.com/)을 사용하여 &quot;expression&quot; 필드의 &quot;value&quot;를 업데이트합니다.

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
| `{NEW_EXPRESSION_VALUE}` | 유효한 [!DNL Profile Query Language] (PQL) 식입니다. 계산된 속성은 현재 다음 함수를 지원합니다. sum, count, min, max 및 boolean 샘플 표현식 목록은 [샘플 PQL 표현식](expressions.md) 설명서를 참조하십시오. |

**응답**

성공적으로 업데이트되면 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문이 반환됩니다. 업데이트가 성공했는지 확인하려면 GET 요청을 수행하여 해당 ID로 계산된 속성을 볼 수 있습니다.

## 계산된 속성 삭제

API를 사용하여 계산된 속성을 삭제할 수도 있습니다. 이 작업은 `/config/computedAttributes` 종단점에 DELETE 요청을 수행하고 요청 경로에서 삭제하려는 계산된 속성의 ID를 포함하여 수행됩니다.

>[!NOTE]
>
>계산된 특성을 삭제할 때 두 개 이상의 스키마에서 사용 중일 수 있으며 DELETE 작업은 취소할 수 없으므로 주의하십시오.

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

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. 성공적으로 삭제를 확인하려면 ID로 계산된 속성을 조회하기 위한 GET 요청을 수행할 수 있습니다. 속성이 삭제되면 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 계산된 속성을 참조하는 세그먼트 정의 만들기

Adobe Experience Platform에서는 프로필 그룹에서 특정 속성 또는 동작 그룹을 정의하는 세그먼트를 만들 수 있습니다. 세그먼트 정의에는 PQL로 작성된 쿼리를 캡슐화하는 식이 포함됩니다. 이러한 표현식은 계산된 속성을 참조할 수도 있습니다.

다음 예제에서는 기존 계산된 속성을 참조하는 세그먼트 정의를 만듭니다. 세그먼트 정의 및 세그먼트 서비스 API에서 세그먼트 정의를 사용하는 방법에 대한 자세한 내용은 [세그먼트 정의 API 엔드포인트 가이드](../../segmentation/api/segment-definitions.md)를 참조하십시오.

시작하려면 요청 본문에 계산된 속성을 제공하여 `/segment/definitions` 종단점에 POST 요청을 수행하십시오.

**API 형식**

```http
POST /segment/definitions
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 세그먼트의 고유한 이름(문자열). |
| `description` | 사용자가 읽을 수 있는 정의 설명. |
| `schema.name` | 세그먼트의 엔티티와 연관된 스키마입니다. `id` 또는 `name` 필드로 구성됩니다. |
| `expression` | 세그먼트 정의에 대한 정보가 있는 필드가 포함된 객체입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 표현식 구조를 나타냅니다. 현재 `pql/text`만 지원됩니다. |
| `expression.value` | 이 예에서 유효한 PQL 표현식은 기존 계산된 속성에 대한 참조를 포함합니다. |

스키마 정의 속성에 대한 자세한 내용은 [세그먼트 정의 API 엔드포인트 가이드](../../segmentation/api/segment-definitions.md)에 제공된 예를 참조하십시오.

**응답**

성공적인 응답은 새로 만든 세그먼트 정의에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다. 세그먼트 정의 응답 개체에 대해 자세히 알아보려면 [세그먼트 정의 API 엔드포인트 가이드](../../segmentation/api/segment-definitions.md)를 참조하십시오.

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## 다음 단계

이제 계산된 속성의 기본 사항을 배웠으므로 조직에 대해 특성을 정의할 준비가 되었습니다.
