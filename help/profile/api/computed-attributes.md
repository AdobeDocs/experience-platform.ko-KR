---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API
title: 계산된 특성 API 끝점
topic: guide
type: Documentation
description: '계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 실시간 고객 프로필 데이터에 대해 작동하며, 이것은 Adobe Experience Platform에 저장된 모든 레코드 및 이벤트에 대한 값을 집계할 수 있음을 의미합니다. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 1%

---


# (알파) 계산된 특성 끝점

>[!IMPORTANT]
>
>이 문서에 요약된 계산된 특성 기능은 현재 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 프로필 수준에서 작동하며, 이는 모든 레코드 및 이벤트에 대한 값을 집계할 수 있음을 의미합니다.

계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 특성 또는 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 간 시간 또는 애플리케이션 열기 횟수와 같은 것과 관련된 질문에 쉽게 답변할 수 있습니다.

이 안내서는 Adobe Experience Platform 내에서 계산된 특성을 더 잘 이해할 수 있도록 지원하며 `/config/computedAttributes` 끝점을 사용하여 기본 CRUD 작업을 수행하는 샘플 API 호출을 포함합니다.

## 시작하기

이 안내서에 사용된 API 끝점은 [실시간 고객 프로필 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 계산된 속성 이해

Adobe Experience Platform을 사용하면 [!DNL Real-time Customer Profiles]을 생성하기 위해 여러 소스의 데이터를 쉽게 가져오고 병합할 수 있습니다. 각 프로필에는 고객의 연락처 정보, 기본 설정 및 구매 내역 등 개인 정보와 관련된 중요한 정보가 포함되어 있으며 고객의 전체 상황을 360도 파악할 수 있습니다.

데이터 필드를 직접 읽을 때 프로필에 수집된 일부 정보를 쉽게 이해할 수 있는 반면(예: &quot;이름&quot;), 다른 데이터는 정보를 생성하기 위해 여러 계산을 수행하거나 다른 필드 및 값에 의존해야 하는 경우(예: &quot;라이프타임 구매 합계&quot;). 이 데이터를 한 눈에 더 쉽게 이해하려면 [!DNL Platform]을 사용하면 이러한 참조 및 계산을 자동으로 수행하는 계산된 속성을 만들어 적절한 필드에 값을 반환할 수 있습니다.

계산된 속성에는 들어오는 데이터에 대해 작동하고 결과 값을 프로필 특성 또는 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;을 만드는 것이 포함됩니다. 표현식을 여러 가지 방법으로 정의할 수 있으므로 들어오는 이벤트, 들어오는 이벤트 및 프로필 데이터 또는 들어오는 이벤트, 프로필 데이터 및 내역 이벤트만 규칙이 평가하도록 지정할 수 있습니다.

### 사용 사례

계산된 속성에 대한 사용 사례는 단순한 계산에서 매우 복잡한 참조까지 범위를 지정할 수 있습니다. 계산된 속성에 대한 몇 가지 사용 예는 다음과 같습니다.

1. **[!UICONTROL 백분율]:** 단순 계산된 속성에는 레코드에 2개의 숫자 필드를 가져와 백분율을 만들기 위해 나누는 것이 포함될 수 있습니다. 예를 들어 개인에게 보낸 이메일의 총 수를 개별 사용자가 여는 이메일 수로 나눌 수 있습니다. 결과 계산된 속성 필드를 보면 개인이 연 총 이메일의 비율이 빠르게 표시됩니다.
1. **[!UICONTROL 애플리케이션 사용]:** 다른 예에는 사용자가 애플리케이션을 연 횟수를 집계하는 기능이 있습니다. 개별 열린 이벤트를 기반으로 전체 애플리케이션 열기 횟수를 추적하면 100일 오픈 첫날 사용자에게 특별한 제안이나 메시지를 전달하여 브랜드에 대한 참여도를 높일 수 있습니다.
1. **[!UICONTROL 라이프타임 값]:** 고객의 라이프타임 구매 값과 같은 실행 합계를 수집하는 것은 매우 어려울 수 있습니다. 이를 위해서는 새 구매 이벤트가 발생할 때마다 내역 합계를 업데이트해야 합니다. 계산된 속성을 사용하면 고객과 관련된 각 성공적인 구매 이벤트에 따라 자동으로 업데이트되는 단일 필드에서 라이프타임 값을 유지하여 이러한 작업을 훨씬 쉽게 수행할 수 있습니다.

## 계산된 속성 구성

계산된 속성을 구성하려면 먼저 계산된 속성 값이 있을 필드를 식별해야 합니다. 이 필드는 믹싱을 사용하여 기존 스키마에 필드를 추가하거나 스키마 내에서 이미 정의한 필드를 선택하여 만들 수 있습니다.

>[!NOTE]
>
>계산된 속성은 Adobe 정의 믹싱 내의 필드에 추가할 수 없습니다. 필드는 `tenant` 네임스페이스 내에 있어야 합니다. 즉, 이 필드는 사용자가 정의하고 스키마에 추가하는 필드여야 합니다.

계산된 속성 필드를 성공적으로 정의하려면 [!DNL Profile]에 대해 스키마를 사용하도록 설정하고 스키마를 기반으로 하는 클래스에 대한 공용 스키마의 일부로 표시되어야 합니다. [!DNL Profile] 사용 가능한 스키마 및 조합에 대한 자세한 내용은 [프로필 및 조합 스키마 보기](../../xdm/api/getting-started.md)의 [!DNL Schema Registry] 개발자 안내서 섹션 섹션을 참조하십시오. 스키마 구성 기본 문서에서 조합](../../xdm/schema/composition.md)의 [섹션을 검토하는 것도 좋습니다.

이 자습서의 작업 과정은 [!DNL Profile] 사용 가능한 스키마를 사용하며 계산된 속성 필드를 포함하는 새 믹싱을 정의하고 올바른 네임스페이스인지 확인하는 절차를 따릅니다. 프로필 사용 스키마 내에 올바른 네임스페이스에 있는 필드가 이미 있는 경우 [계산된 특성](#create-a-computed-attribute)을 만들기 위한 단계로 직접 진행할 수 있습니다.

### 스키마 보기

Adobe Experience Platform 사용자 인터페이스를 사용하여 스키마를 찾고, 믹싱을 추가하고, 필드를 정의하는 단계입니다. [!DNL Schema Registry] API를 사용하려는 경우 [스키마 레지스트리 개발자 안내서](../../xdm/api/getting-started.md)에서 믹싱을 만들고 스키마에 혼합을 추가하고 [!DNL Real-time Customer Profile]에서 사용할 스키마를 활성화하는 방법을 참조하십시오.

사용자 인터페이스에서 왼쪽 레일에 있는 **[!UICONTROL 스키마]**&#x200B;를 클릭하고 **[!UICONTROL 찾아보기]** 탭의 검색 막대를 사용하여 업데이트할 스키마를 빠르게 찾습니다.

![](../images/computed-attributes/Schemas-Browse.png)

스키마를 찾은 후에는 해당 이름을 클릭하여 [!DNL Schema Editor]을 열고 스키마를 편집할 수 있습니다.

![](../images/computed-attributes/Schema-Editor.png)

### 혼합 만들기

새 믹싱을 만들려면 편집기의 왼쪽에 있는 **[!UICONTROL 컴포지션]** 섹션에서 **[!UICONTROL 믹싱]** 옆에 있는 **[!UICONTROL 추가]**&#x200B;를 클릭합니다. 그러면 기존 믹스를 볼 수 있는 **[!UICONTROL 혼합 추가]** 대화 상자가 열립니다. 새 믹스를 정의하려면 **[!UICONTROL 새 믹신 만들기]**&#x200B;의 라디오 단추를 클릭합니다.

믹싱에 이름과 설명을 지정하고 완료되면 **[!UICONTROL 믹신 추가]**&#x200B;를 클릭합니다.

![](../images/computed-attributes/Add-mixin.png)

### 스키마에 계산된 속성 필드 추가

이제 새 믹싱이 &quot;[!UICONTROL 컴포지션]&quot;의 &quot;[!UICONTROL 혼합]&quot; 섹션에 표시됩니다. 믹스의 이름을 클릭하고 편집기의 **[!UICONTROL 구조]** 섹션에 여러 **[!UICONTROL 필드 추가]** 단추가 나타납니다.

최상위 수준 필드를 추가하려면 스키마 이름 옆에 있는 **[!UICONTROL 필드 추가]**&#x200B;를 선택하거나 원하는 스키마 내의 아무 곳에나 필드를 추가하도록 선택할 수 있습니다.

**[!UICONTROL 필드 추가]**&#x200B;를 클릭하면 해당 필드가 올바른 네임스페이스에 있음을 보여주는 새 개체가 테넌트 ID에 이름이 지정됩니다. 해당 개체 내에 **[!UICONTROL 새 필드]**&#x200B;가 나타납니다. 계산된 속성을 정의할 필드가 있을 경우 이 값이 필요합니다.

![](../images/computed-attributes/New-field.png)

### 필드 구성

편집기의 오른쪽에 있는 **[!UICONTROL 필드 속성]** 섹션을 사용하여 이름, 표시 이름, 유형 등 새 필드에 필요한 정보를 제공합니다.

>[!NOTE]
>
>필드의 유형은 계산된 속성 값과 같은 유형이어야 합니다. 예를 들어 계산된 속성 값이 문자열이면 스키마에 정의된 필드가 문자열이어야 합니다.

완료되면 **[!UICONTROL 적용]**&#x200B;을 클릭하고 필드 이름과 해당 유형이 편집기의 **[!UICONTROL 구조]** 섹션에 표시됩니다.

![](../images/computed-attributes/Apply.png)

### [!DNL Profile]에 대한 스키마 사용

계속하기 전에 [!DNL Profile]에 대한 스키마가 활성화되어 있는지 확인하십시오. **[!UICONTROL 스키마 속성]** 탭이 나타나도록 편집기의 **[!UICONTROL 구조]** 섹션에서 스키마 이름을 클릭합니다. **[!UICONTROL 프로필]** 슬라이더가 파란색이면 [!DNL Profile]에 대해 스키마가 활성화되었습니다.

>[!NOTE]
>
>[!DNL Profile]에 대한 스키마 활성화는 실행 취소할 수 없으므로 슬라이더를 활성화한 후 클릭하면 비활성화될 위험이 없습니다.

![](../images/computed-attributes/Profile.png)

이제 **[!UICONTROL 저장]**&#x200B;을 클릭하여 업데이트된 스키마를 저장하고 API를 사용하여 나머지 자습서를 계속 진행할 수 있습니다.

### 계산된 특성 {#create-a-computed-attribute} 만들기

계산된 속성 필드가 확인되고 [!DNL Profile]에 대해 스키마가 활성화되었는지 확인하면 이제 계산된 속성을 구성할 수 있습니다.

만들려는 계산된 속성의 세부 정보가 포함된 요청 본문으로 `/config/computedAttributes` 끝점에 POST 요청을 하는 것으로 시작합니다.

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
| `path` | 계산된 속성이 포함된 필드의 경로입니다. 이 경로는 스키마의 `properties` 특성 내에 있으며 경로에 필드 이름을 포함하지 않아야 합니다. 경로를 쓸 때는 `properties` 속성의 여러 레벨을 생략합니다. |
| `{TENANT_ID}` | 테넌트 ID에 익숙하지 않은 경우 [스키마 레지스트리 개발자 가이드](../../xdm/api/getting-started.md#know-your-tenant_id)에서 테넌트 ID를 찾는 단계를 참조하십시오. |
| `description` | 계산된 속성에 대한 설명입니다. IMS 조직 내에서 사용할 올바른 계산된 속성을 결정하는 데 도움이 되므로 계산된 속성이 여러 개 정의된 경우 특히 유용합니다. |
| `expression.value` | 유효한 [!DNL Profile Query Language](PQL) 표현식입니다. PQL 및 지원되는 쿼리 링크에 대한 자세한 내용은 [PQL 개요](../../segmentation/pql/overview.md)를 참조하십시오. |
| `schema.name` | 계산된 속성 필드를 포함하는 스키마가 기반으로 하는 클래스입니다. 예:XDM ExperienceEvent 클래스를 기반으로 한 스키마의 `_xdm.context.experienceevent`. |

**응답**

성공적으로 생성된 계산된 속성은 HTTP 상태 200(OK) 및 새로 만든 계산된 속성의 세부 정보가 포함된 응답 본문을 반환합니다. 이러한 세부 사항에는 다른 API 작업 동안 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 `id`이 포함됩니다.

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
| `id` | 다른 API 작업 중에 계산된 속성을 참조하는 데 사용할 수 있는 고유한 읽기 전용 시스템 생성 ID. |
| `imsOrgId` | 계산된 속성과 관련된 IMS 조직은 요청에 전송된 값과 일치해야 합니다. |
| `sandbox` | 샌드박스 객체에는 계산된 속성이 구성된 샌드박스의 세부 사항이 포함됩니다. 이 정보는 요청에서 전송된 샌드박스 헤더에서 그려집니다. 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오. |
| `positionPath` | 요청에서 보낸 필드에 대한 정화 `path`이 포함된 배열입니다. |
| `returnSchema.meta:xdmType` | 계산된 속성이 저장되는 필드의 유형입니다. |
| `definedOn` | 계산된 속성이 정의된 결합 스키마를 표시하는 배열입니다. 결합 스키마당 하나의 객체를 포함합니다. 즉, 계산된 속성이 다른 클래스를 기반으로 여러 스키마에 추가된 경우 배열 내에 여러 객체가 있을 수 있습니다. |
| `active` | 계산된 속성이 현재 활성 상태인지 여부를 표시하는 부울 값입니다. 기본적으로 값은 `true`입니다. |
| `type` | 만들어진 리소스의 유형입니다. 이 경우 &quot;ComputedAttribute&quot;는 기본값입니다. |
| `createEpoch` 및 `updateEpoch` | 계산된 속성이 각각 만들어지고 마지막으로 업데이트된 시간입니다. |


## 계산된 속성에 액세스

API를 사용하여 계산된 속성을 사용하는 경우 조직에서 정의한 계산된 속성에 액세스하는 두 가지 옵션이 있습니다. 첫 번째 요소는 모든 계산된 속성을 나열하는 것이며, 두 번째 방법은 고유한 `id`으로 특정 계산된 속성을 보는 것입니다.

계산된 모든 속성을 나열하고 특정 계산된 속성을 보는 단계는 다음 섹션에 요약되어 있습니다.

### 계산된 특성 목록 {#list-computed-attributes}

IMS 조직에서 여러 개의 계산된 특성을 만들 수 있으며, `/config/computedAttributes` 종단점에 대한 GET 요청을 수행하면 조직의 모든 기존 계산된 특성을 나열할 수 있습니다.

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

성공적인 응답에는 페이지에 계산된 속성의 총 수(`totalCount`)와 계산된 속성의 수를 제공하는 `_page` 특성이 포함됩니다(`pageSize`).

또한 응답에는 하나 이상의 객체로 구성된 `children` 배열이 포함되며 각 배열은 하나의 계산된 속성의 세부 정보를 포함합니다. 조직에 계산된 속성이 없는 경우 `totalCount` 및 `pageSize`은 0(영)이 되고 `children` 배열은 비어 있게 됩니다.

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
| `_page.pageSize` | 이 결과 페이지에서 반환되는 계산된 속성의 수입니다. `pageSize`이(가) `totalCount`과(와) 같으면 결과의 페이지가 하나만 있고 계산된 속성이 모두 반환되었음을 의미합니다. 같지 않으면 액세스할 수 있는 결과 페이지가 추가로 있습니다. 자세한 내용은 `_links.next`을 참조하십시오. |
| `children` | 하나 이상의 객체로 구성된 배열이며 각 객체에는 단일 계산된 속성의 세부 사항이 포함됩니다. 계산된 속성이 정의되지 않은 경우 `children` 배열은 비어 있습니다. |
| `id` | 계산된 속성이 만들어질 때 자동으로 할당된 읽기 전용 시스템 생성 값. 계산된 속성 개체의 구성 요소에 대한 자세한 내용은 이 자습서의 [계산된 특성](#create-a-computed-attribute) 만들기 섹션을 참조하십시오. |
| `_links.next` | 계산된 속성의 단일 페이지가 반환되는 경우 위의 샘플 응답에 표시된 것처럼 `_links.next`은(는) 빈 객체입니다. 조직에 많은 계산된 특성이 있는 경우 이 속성은 `_links.next` 값에 GET 요청을 수행하여 액세스할 수 있는 여러 페이지에서 반환됩니다. |

### 계산된 속성 {#view-a-computed-attribute} 보기

요청 경로에 계산된 속성 ID를 포함하여 `/config/computedAttributes` 끝점에 GET 요청을 수행하여 특정 계산된 속성을 볼 수도 있습니다.

**API 형식**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 보려는 계산된 속성의 ID. |

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

기존 계산된 특성을 업데이트해야 하는 경우 이 작업은 요청 경로에서 업데이트하려는 계산된 속성의 ID를 포함하여 `/config/computedAttributes` 끝점에 PATCH 요청을 함으로써 수행할 수 있습니다.

**API 형식**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{ATTRIBUTE_ID}` | 업데이트할 계산된 속성의 ID입니다. |

**요청**

이 요청은 [JSON 패치 서식](http://jsonpatch.com/)을 사용하여 &quot;expression&quot; 필드의 &quot;value&quot;를 업데이트합니다.

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
| `{NEW_EXPRESSION_VALUE}` | 유효한 [!DNL Profile Query Language](PQL) 표현식입니다. PQL 및 지원되는 쿼리 링크에 대한 자세한 내용은 [PQL 개요](../../segmentation/pql/overview.md)를 참조하십시오. |

**응답**

업데이트가 성공하면 HTTP 상태 204(콘텐츠 없음) 및 빈 응답 본문을 반환합니다. 업데이트가 성공했는지 확인하려면 GET 요청을 수행하여 ID로 계산된 속성을 볼 수 있습니다.

## 계산된 속성 삭제

API를 사용하여 계산된 속성을 삭제할 수도 있습니다. 이 작업은 요청 경로에서 삭제하려는 계산된 속성의 ID를 포함하여 `/config/computedAttributes` 끝점에 DELETE 요청을 함으로써 수행됩니다.

>[!NOTE]
>
>계산된 속성은 둘 이상의 스키마에서 사용 중일 수 있으며 DELETE 작업을 실행 취소할 수 없으므로 삭제할 때는 주의하십시오.

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

삭제 요청이 성공하면 HTTP 상태 200(OK) 및 빈 응답 본문을 반환합니다. 삭제에 성공했는지 확인하려면 ID로 계산된 속성을 조회하기 위한 GET 요청을 수행할 수 있습니다. 속성이 삭제되면 HTTP 상태 404(찾을 수 없음) 오류가 표시됩니다.

## 다음 단계

이제 계산된 속성의 기본 사항을 알았으므로 조직에 대해 속성을 정의할 준비가 되었습니다.