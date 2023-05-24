---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 속성 API 끝점
type: Documentation
description: Adobe Experience Platform에서 계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화에서 사용할 수 있도록 자동으로 계산됩니다. 이 안내서에서는 Real-Time Customer Profile API를 사용하여 계산된 속성을 생성, 보기, 업데이트 및 삭제하는 방법을 보여줍니다.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 2%

---

# (알파) 계산된 속성 API 끝점

>[!IMPORTANT]
>
>이 문서에 설명된 계산된 속성 기능은 현재 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화에서 사용할 수 있도록 자동으로 계산됩니다. 이 안내서에는 를 사용하여 기본 CRUD 작업을 수행하기 위한 샘플 API 호출이 포함되어 있습니다. `/computedAttributes` 엔드포인트.

계산된 속성에 대해 자세히 알아보려면 다음을 읽음으로써 시작하십시오. [계산된 속성 개요](overview.md).

## 시작하기

이 안내서에 사용된 API 끝점은 [실시간 고객 프로필 API](https://www.adobe.com/go/profile-apis-en).

계속하기 전에 다음을 검토하십시오. [프로필 API 시작 안내서](../api/getting-started.md) 권장 설명서에 대한 링크, 이 설명서에 표시되는 샘플 API 호출 읽기에 대한 안내서 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보입니다.

## 계산된 속성 필드 구성

계산된 속성을 생성하려면 먼저 계산된 속성 값을 보유할 스키마의 필드를 식별해야 합니다.

다음에 대한 설명서를 참조하십시오. [계산된 속성 구성](configure-api.md) 를 참조하십시오. 스키마에서 계산된 속성 필드를 만드는 방법에 대한 전체 안내서입니다.

>[!WARNING]
>
>API 안내서를 계속 진행하려면 계산된 속성 필드가 구성되어 있어야 합니다.

## 계산된 속성 만들기 {#create-a-computed-attribute}

이제 프로필 활성화 스키마에 정의된 계산된 속성 필드를 사용하여 계산된 속성을 구성할 수 있습니다. 아직 수행하지 않았다면 다음에 설명된 워크플로를 따르십시오. [계산된 속성 구성](configure-api.md) 설명서를 참조하십시오.

POST 계산된 속성을 만들려면 먼저 `/config/computedAttributes` 만들려는 계산된 속성의 세부 정보가 포함된 요청 본문이 있는 끝점입니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
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
| `path` | 계산된 속성이 포함된 필드의 경로. 이 경로는 `properties` 스키마의 속성이며 경로에 필드 이름을 포함해서는 안 됩니다. 경로를 작성할 때 의 여러 수준을 생략합니다. `properties` 속성. |
| `{TENANT_ID}` | 테넌트 ID에 익숙하지 않은 경우 의 테넌트 ID 찾기 단계를 참조하십시오. [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 조직 내의 다른 사용자가 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 여러 계산된 속성이 정의된 경우에 특히 유용합니다. |
| `expression.value` | 유효 [!DNL Profile Query Language] (PQL) 표현식입니다. 계산된 속성은 현재 sum, count, min, max 및 boolean 함수를 지원합니다. 샘플 표현식 목록은 [샘플 PQL 표현식](expressions.md) 설명서를 참조하십시오. |
| `schema.name` | 계산된 속성 필드를 포함하는 스키마의 기준이 되는 클래스입니다. 예: `_xdm.context.experienceevent` XDM ExperienceEvent 클래스 기반 스키마용. |

**응답**

성공적으로 생성된 계산된 속성은 HTTP 상태 200(OK) 및 새로 생성된 계산된 속성의 세부 정보가 포함된 응답 본문을 반환합니다. 이러한 세부 정보에는 고유한 읽기 전용 시스템 생성 정보가 포함됩니다 `id` 다른 API 작업 중에 계산된 속성을 참조하는 데 사용할 수 있습니다.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
| `id` | 다른 API 작업 중에 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID입니다. |
| `imsOrgId` | 계산된 속성과 관련된 IMS 조직은 요청에서 전송된 값과 일치해야 합니다. |
| `sandbox` | 샌드박스 객체에는 계산된 속성이 구성된 샌드박스의 세부 정보가 포함됩니다. 이 정보는 요청에서 전송된 샌드박스 헤더에서 가져옵니다. 자세한 내용은 다음을 참조하십시오. [샌드박스 개요](../../sandboxes/home.md). |
| `positionPath` | 해체된 가 포함된 배열입니다. `path` 을 추가하여 요청에서 전송된 필드에 추가합니다. |
| `returnSchema.meta:xdmType` | 계산된 속성이 저장될 필드의 유형입니다. |
| `definedOn` | 계산된 속성이 정의된 유니온 스키마를 보여 주는 배열입니다. 유니온 스키마당 하나의 객체를 포함합니다. 즉, 계산된 속성이 다른 클래스를 기반으로 여러 스키마에 추가된 경우 배열 내에 여러 객체가 있을 수 있습니다. |
| `active` | 계산된 속성이 현재 활성 상태인지 여부를 표시하는 부울 값입니다. 기본값은 `true`입니다.  |
| `type` | 생성된 리소스 유형(이 경우 &quot;ComputedAttribute&quot;)이 기본값입니다. |
| `createEpoch` 및 `updateEpoch` | 계산된 속성이 만들어지고 마지막으로 업데이트된 시간입니다. |

## 기존 계산된 속성을 참조하는 계산된 속성 만들기

기존의 계산된 속성을 참조하는 계산된 속성을 만들 수도 있습니다. POST 이렇게 하려면 먼저 `/config/computedAttributes` 엔드포인트. 요청 본문에는에서 계산된 속성에 대한 참조가 포함됩니다. `expression.value` 다음 예와 같은 필드.

**API 형식**

```http
POST /config/computedAttributes
```

**요청**

이 예에서 두 개의 계산된 속성이 이미 만들어졌으며 세 번째 속성을 정의하는 데 사용됩니다. 기존 계산된 속성은 다음과 같습니다.

* **`totalSpend`:** 고객이 지출한 총 달러 금액을 캡처합니다.
* **`countPurchases`:** 고객이 구매한 횟수를 카운트합니다.

아래 요청은 새로운 속성을 계산하기 위해 유효한 PQL을 사용하여 두 개의 기존 계산된 속성을 참조합니다 `averageSpend` 계산된 속성입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
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
| `path` | 계산된 속성이 포함된 필드의 경로. 이 경로는 `properties` 스키마의 속성이며 경로에 필드 이름을 포함해서는 안 됩니다. 경로를 작성할 때 의 여러 수준을 생략합니다. `properties` 속성. |
| `{TENANT_ID}` | 테넌트 ID에 익숙하지 않은 경우 의 테넌트 ID 찾기 단계를 참조하십시오. [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | 계산된 속성에 대한 설명입니다. 이 기능은 IMS 조직 내의 다른 사람이 사용할 올바른 연산 속성을 결정하는 데 도움이 되므로 여러 연산 속성이 정의된 경우에 특히 유용합니다. |
| `expression.value` | 유효한 PQL 표현식입니다. 계산된 속성은 현재 sum, count, min, max 및 boolean 함수를 지원합니다. 샘플 표현식 목록은 [샘플 PQL 표현식](expressions.md) 설명서를 참조하십시오.<br/><br/>이 예에서 표현식은 두 개의 기존 계산된 속성을 참조합니다. 속성은 다음을 사용하여 참조됩니다. `path` 및 `name` 계산된 속성이 정의된 스키마에 나타나는 계산된 속성. 예를 들어 `path` 의 첫 번째 참조 연산 속성은 다음과 같습니다. `_{TENANT_ID}.purchaseSummary` 및 `name` 은(는) `totalSpend`. |
| `schema.name` | 계산된 속성 필드를 포함하는 스키마의 기준이 되는 클래스입니다. 예: `_xdm.context.experienceevent` XDM ExperienceEvent 클래스 기반 스키마용. |

**응답**

성공적으로 생성된 계산된 속성은 HTTP 상태 200(OK) 및 새로 생성된 계산된 속성의 세부 정보가 포함된 응답 본문을 반환합니다. 이러한 세부 정보에는 고유한 읽기 전용 시스템 생성 정보가 포함됩니다 `id` 다른 API 작업 중에 계산된 속성을 참조하는 데 사용할 수 있습니다.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
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
| `id` | 다른 API 작업 중에 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID입니다. |
| `imsOrgId` | 계산된 속성과 관련된 IMS 조직은 요청에서 전송된 값과 일치해야 합니다. |
| `sandbox` | 샌드박스 객체에는 계산된 속성이 구성된 샌드박스의 세부 정보가 포함됩니다. 이 정보는 요청에서 전송된 샌드박스 헤더에서 가져옵니다. 자세한 내용은 다음을 참조하십시오. [샌드박스 개요](../../sandboxes/home.md). |
| `positionPath` | 해체된 가 포함된 배열입니다. `path` 을 추가하여 요청에서 전송된 필드에 추가합니다. |
| `returnSchema.meta:xdmType` | 계산된 속성이 저장될 필드의 유형입니다. |
| `definedOn` | 계산된 속성이 정의된 유니온 스키마를 보여 주는 배열입니다. 유니온 스키마당 하나의 객체를 포함합니다. 즉, 계산된 속성이 다른 클래스를 기반으로 여러 스키마에 추가된 경우 배열 내에 여러 객체가 있을 수 있습니다. |
| `active` | 계산된 속성이 현재 활성 상태인지 여부를 표시하는 부울 값입니다. 기본값은 `true`입니다.  |
| `type` | 생성된 리소스 유형(이 경우 &quot;ComputedAttribute&quot;)이 기본값입니다. |
| `createEpoch` 및 `updateEpoch` | 계산된 속성이 만들어지고 마지막으로 업데이트된 시간입니다. |

## 계산된 속성에 액세스

API를 사용하여 계산된 속성으로 작업하는 경우 조직에서 정의한 계산된 속성에 액세스하기 위한 두 가지 옵션이 있습니다. 첫 번째는 계산된 모든 속성을 나열하는 것이고, 두 번째는 계산된 특정 속성을 고유한 값으로 보는 것입니다 `id`.

이 문서에서는 두 액세스 패턴 모두에 대한 단계를 설명합니다. 시작하려면 다음 중 하나를 선택하십시오.

* **[기존의 모든 계산된 속성 나열](#list-all-computed-attributes):** 조직에서 생성한 기존의 모든 계산된 속성 목록을 반환합니다.
* **[특정 계산된 속성 보기](#view-a-computed-attribute):** 요청 중에 해당 ID를 지정하여 단일 계산된 속성의 세부 정보를 반환합니다.

### 계산된 모든 속성 나열 {#list-all-computed-attributes}

IMS 조직은 계산된 속성을 여러 개 만들고 다음에 대한 GET 요청을 수행할 수 있습니다. `/config/computedAttributes` 끝점을 사용하면 조직의 기존 계산된 속성을 모두 나열할 수 있습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답에는 다음이 포함됩니다. `_page` 계산된 속성의 총 수를 제공하는 속성(`totalCount`) 및 페이지의 계산된 속성 수(`pageSize`).

응답에는 `children` 하나 이상의 객체로 구성되며, 각 객체에는 하나의 계산된 속성에 대한 세부 사항이 포함됩니다. 조직에 계산된 속성이 없는 경우 `totalCount` 및 `pageSize` 은(는) 0(영)이 되고 `children` 배열이 비어 있습니다.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
                "type": "PQL", 
                "format": "pql/text", 
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
| `_page.pageSize` | 이 결과 페이지에서 반환되는 계산된 속성 수입니다. If `pageSize` 다음과 같음 `totalCount`즉, 결과 페이지가 한 개만 있고 계산된 모든 속성이 반환되었습니다. 이 페이지들이 같지 않으면 액세스할 수 있는 추가 결과 페이지가 있습니다. 다음을 참조하십시오 `_links.next` 을 참조하십시오. |
| `children` | 하나 이상의 객체로 구성되며 각각 계산된 단일 속성의 세부 정보가 포함된 배열입니다. 계산된 속성이 정의되지 않은 경우 `children` 배열이 비어 있습니다. |
| `id` | 속성이 생성될 때 계산된 속성에 자동으로 할당된 고유한 읽기 전용 시스템 생성 값입니다. 계산된 속성 객체의 구성 요소에 대한 자세한 내용은 [계산된 속성 생성](#create-a-computed-attribute) 이 자습서의 앞부분입니다. |
| `_links.next` | 계산된 속성의 단일 페이지가 반환되면, `_links.next` 는 위의 샘플 응답에 표시된 대로 비어 있는 개체입니다. 조직에 많은 계산된 속성이 있는 경우 GET에 요청하여 액세스할 수 있는 여러 페이지에 반환됩니다 `_links.next` 값. |

### 계산된 속성 보기 {#view-a-computed-attribute}

에 GET 요청을 하여 특정 계산된 속성을 볼 수 있습니다. `/config/computedAttributes` 엔드포인트 및 계산된 속성 ID를 요청 경로에 포함합니다.

**API 형식**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 보려는 계산된 속성의 ID입니다. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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

기존 계산된 속성을 업데이트해야 하는 경우 PATCH 요청을에 제출하면 됩니다. `/config/computedAttributes` 엔드포인트 및 요청 경로에 업데이트할 계산된 속성의 ID 포함.

**API 형식**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 업데이트하려는 계산된 속성의 ID입니다. |

**요청**

이 요청은 을 사용합니다. [JSON 패치 형식 지정](https://datatracker.ietf.org/doc/html/rfc6902) 를 입력하여 &quot;표현식&quot; 필드의 &quot;값&quot;을 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| 속성 | 설명 |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | 유효 [!DNL Profile Query Language] (PQL) 표현식입니다. 계산된 속성은 현재 sum, count, min, max 및 boolean 함수를 지원합니다. 샘플 표현식 목록은 [샘플 PQL 표현식](expressions.md) 설명서를 참조하십시오. |

**응답**

성공한 업데이트는 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환합니다. 업데이트가 성공했는지 확인하려면 GET 요청을 수행하여 해당 ID로 계산된 속성을 볼 수 있습니다.

## 계산된 속성 삭제

API를 사용하여 계산된 속성을 삭제할 수도 있습니다. 이 작업은 다음에 대한 DELETE 요청을 통해 수행됩니다. `/config/computedAttributes` 엔드포인트 및 요청 경로에서 삭제하려는 계산된 속성의 ID 포함.

>[!NOTE]
>
>계산된 속성이 둘 이상의 스키마에서 사용 중일 수 있고 DELETE 작업은 실행 취소할 수 없으므로 삭제할 때 주의하십시오.

**API 형식**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 삭제하려는 계산된 속성의 ID입니다. |

**요청**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**응답**

성공적인 삭제 요청은 HTTP 상태 200(OK)과 빈 응답 본문을 반환합니다. 삭제가 성공했는지 확인하기 위해 GET 요청을 수행하여 계산된 속성을 해당 ID로 조회할 수 있습니다. 속성이 삭제되면 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 계산된 속성을 참조하는 세그먼트 정의 만들기

Adobe Experience Platform을 사용하면 프로필 그룹에서 특정 속성이나 동작 그룹을 정의하는 세그먼트를 만들 수 있습니다. 세그먼트 정의는 PQL로 작성된 쿼리를 캡슐화하는 표현식을 포함합니다. 이러한 표현식은 계산된 속성을 참조할 수도 있습니다.

다음 예제에서는 기존 계산된 속성을 참조하는 세그먼트 정의를 만듭니다. 세그먼트 정의와 세그먼테이션 서비스 API에서 세그먼트 정의로 작업하는 방법에 대해 자세히 알아보려면 다음을 참조하십시오. [세그먼트 정의 API 엔드포인트 안내서](../../segmentation/api/segment-definitions.md).

시작하려면 다음에 대한 POST 요청을 만듭니다. `/segment/definitions` 요청 본문에 계산된 속성을 제공하는 종단점입니다.

**API 형식**

```http
POST /segment/definitions
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 세그먼트의 고유한 이름(문자열)입니다. |
| `description` | 사람이 인식할 수 있는 정의 설명. |
| `schema.name` | 세그먼트의 엔티티와 연결된 스키마입니다. 다음 중 하나로 구성됩니다. `id` 또는 `name` 필드. |
| `expression` | 세그먼트 정의에 대한 정보가 있는 필드가 포함된 객체입니다. |
| `expression.type` | 표현식 유형을 지정합니다. 현재 &quot;PQL&quot;만 지원됩니다. |
| `expression.format` | 값의 식 구조를 나타냅니다. 현재는 `pql/text` 은(는) 지원됩니다. |
| `expression.value` | 유효한 PQL 표현식이며, 이 예에는 기존 계산된 속성에 대한 참조가 포함됩니다. |

스키마 정의 속성에 대한 자세한 내용은 [세그먼트 정의 API 엔드포인트 안내서](../../segmentation/api/segment-definitions.md).

**응답**

성공적인 응답은 새로 생성된 세그먼트 정의에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다. 세그먼트 정의 응답 개체에 대한 자세한 내용은 [세그먼트 정의 API 엔드포인트 안내서](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
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

이제 계산된 속성에 대한 기본 사항을 배웠으므로 조직에 대해 속성 정의를 시작할 준비가 되었습니다.
