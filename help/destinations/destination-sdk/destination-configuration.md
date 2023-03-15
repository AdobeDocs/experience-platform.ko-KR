---
description: 이 구성을 통해 대상 이름, 카테고리, 설명, 로고 등과 같은 기본 정보를 표시할 수 있습니다. 또한 이 구성의 설정은 Experience Platform 사용자가 대상에 인증하는 방법, Experience Platform 사용자 인터페이스에 표시되는 방법 및 대상으로 내보낼 수 있는 ID를 결정합니다.
title: Destination SDK을 위한 스트리밍 대상 구성 옵션
exl-id: b7e4db67-2981-4f18-b202-3facda5c8f0b
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '1883'
ht-degree: 3%

---

# 스트리밍 대상 구성 {#destination-configuration}

## 개요 {#overview}

이 구성을 통해 대상 이름, 카테고리, 설명 등과 같은 스트리밍 대상에 대한 필수 정보를 나타낼 수 있습니다. 또한 이 구성의 설정은 Experience Platform 사용자가 대상에 인증하는 방법, Experience Platform 사용자 인터페이스에 표시되는 방법 및 대상으로 내보낼 수 있는 ID를 결정합니다.

이 구성은 또한 대상이 작동하는 데 필요한 다른 구성(대상 서버 및 대상 메타데이터)을 이 구성에 연결합니다. 의 두 구성을 참조하는 방법 읽기 [추가 하위 섹션](./destination-configuration.md#connecting-all-configurations).

다음을 사용하여 이 문서에 설명된 기능을 구성할 수 있습니다. `/authoring/destinations` API 엔드포인트. 읽기 [대상 API 엔드포인트 작업](./destination-configuration-api.md) 엔드포인트에서 수행할 수 있는 전체 작업 목록입니다.

## 스트리밍 구성 예 {#example-configuration}

이는 지구상의 4개 위치에 엔드포인트가 있는 가상의 스트리밍 도착지 Moviestar의 예제 구성입니다. 대상이 모바일 대상 범주에 속합니다.

```json
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointRegion",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "schemaConfig":{
      "profileRequired":false,
      "segmentRequired":true,
      "identityRequired":true
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "aggregation":{
      "aggregationType":"CONFIGURABLE_AGGREGATION",
      "configurableAggregation":{
         "splitUserById":true,
         "maxBatchAgeInSecs":2400,
         "maxNumEventsInBatch":5000,
         "aggregationKey":{
            "includeSegmentId":true,
            "includeSegmentStatus":true,
            "includeIdentity":true,
            "oneIdentityPerGroup":true,
            "groups":[
               {
                  "namespaces":[
                     "IDFA",
                     "GAID"
                  ]
               },
               {
                  "namespaces":[
                     "EMAIL"
                  ]
               }
            ]
         }
      }
   },
   "backfillHistoricalProfileData":true
}
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `name` | 문자열 | Experience Platform 카탈로그에서 대상의 제목을 나타냅니다. |
| `description` | 문자열 | Experience Platform 대상 카탈로그에 대상 카드에 대한 설명을 입력합니다. 4-5개 이하의 문장을 목표로 하라. |
| `status` | 문자열 | 대상 카드의 라이프사이클 상태를 나타냅니다. 허용되는 값은 `TEST`, `PUBLISHED` 및 `DELETED`입니다. 사용 `TEST` 대상을 처음 구성할 때. |

{style="table-layout:auto"}

## 고객 인증 구성 {#customer-authentication-configurations}

대상 구성의 이 섹션에서는 [새 대상 구성](/help/destinations/ui/connect-destination.md) Experience Platform을 대상이 있는 계정에 연결하는 Experience Platform 사용자 인터페이스의 페이지입니다. 에 지정하는 인증 옵션에 따라 `authType` 필드에서는 다음과 같이 사용자에 대한 Experience Platform 페이지가 생성됩니다.

### 전달자 인증

전달자 인증 유형을 구성할 때 사용자는 대상에서 얻은 전달자 토큰을 입력해야 합니다.

![베어러 인증을 사용한 UI 렌더링](assets/bearer-authentication-ui.png)

### OAuth 2 인증

사용자 선택 **[!UICONTROL 대상에 연결]** 사용자 지정 대상 Twitter 대상에 대해 아래 예에 표시된 대로 대상에 대한 OAuth 2 인증 흐름을 트리거합니다. 대상 끝점에 대한 OAuth 2 인증 구성에 대한 자세한 내용은 전용 을 참조하십시오 [Destination SDK OAuth 2 인증 페이지](./oauth2-authentication.md).

![OAuth 2 인증을 통해 UI 렌더링](assets/oauth2-authentication-ui.png)

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `customerAuthenticationConfigurations` | 문자열 | 서버에 Experience Platform 고객을 인증하는 데 사용되는 구성을 나타냅니다. 다음을 참조하십시오 `authType` 허용되는 값은 아래를 참조하십시오. |
| `authType` | 문자열 | 스트리밍 대상에 대해 허용되는 값은 다음과 같습니다.<ul><li>`BASIC` 질문에 답합니다. 대상이 기본 인증을 지원하는 경우 다음을 설정하십시오. `"authType":"Basic"` 및  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 다음에서 [대상 게재 섹션](./destination-configuration.md).</li><li>`BEARER` 질문에 답합니다. 대상이 전달자 인증을 지원하는 경우 다음을 설정하십시오. `"authType":"Bearer"` 및  `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 다음에서 [대상 게재 섹션](./destination-configuration.md).</li><li>`OAUTH2` 질문에 답합니다. 대상이 OAuth 2 인증을 지원하는 경우 다음을 설정하십시오. `"authType":"OAUTH2"` 과 함께 OAuth 2에 대한 필수 필드를 추가합니다. [Destination SDK OAuth 2 인증 페이지](./oauth2-authentication.md). 추가로, 설정 `"authenticationRule":"CUSTOMER_AUTHENTICATION"` 다음에서 [대상 게재 섹션](./destination-configuration.md).</li> |

{style="table-layout:auto"}

## 고객 데이터 필드 {#customer-data-fields}

이 섹션을 사용하여 Experience Platform UI에서 대상에 연결할 때 사용자에게 대상에 대한 사용자 정의 필드를 입력하도록 요청합니다. 구성은 아래와 같이 인증 흐름에 반영됩니다.

![사용자 정의 필드 인증 흐름](./assets/custom-field-authentication-flow.png)

>[!TIP]
>
>템플릿에서 고객 데이터 필드의 고객 입력에 액세스하고 사용할 수 있습니다. 매크로 사용 `{{customerData.name}}`. 예를 들어, 사용자에게 이름이 인 고객 ID 필드를 입력하도록 하는 경우 `userId`를 설정하는 경우 매크로를 사용하여 템플릿에서 액세스할 수 있습니다 `{{customerData.userId}}`. 에서 API 끝점의 URL에 고객 데이터 필드가 사용되는 방식의 예를 봅니다. [대상 서버 구성](/help/destinations/destination-sdk/server-and-template-configuration.md#server-specs).

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `name` | 문자열 | 도입 중인 사용자 정의 필드의 이름을 입력합니다. |
| `type` | 문자열 | 도입 중인 사용자 정의 필드 유형을 나타냅니다. 허용되는 값은 다음과 같습니다 `string`, `object`, `integer`. |
| `title` | 문자열 | Experience Platform 사용자 인터페이스에서 고객에게 표시되는 필드의 이름을 나타냅니다. |
| `description` | 문자열 | 사용자 정의 필드에 대한 설명을 입력합니다. |
| `isRequired` | 부울 | 대상 설정 워크플로에서 이 필드가 필요한지 여부를 나타냅니다. |
| `enum` | 문자열 | 사용자 정의 필드를 드롭다운 메뉴로 렌더링하고 사용자가 사용할 수 있는 옵션을 나열합니다. |
| `pattern` | 문자열 | 필요한 경우 사용자 정의 필드에 패턴을 적용합니다. 패턴을 적용하려면 정규 표현식을 사용하십시오. 예를 들어 고객 ID에 숫자나 밑줄이 포함되지 않은 경우 을 입력합니다 `^[A-Za-z]+$` 이 필드에서 을(를) 참조하십시오. |

{style="table-layout:auto"}

## UI 속성 {#ui-attributes}

이 섹션은 위의 구성에서 Adobe이 Adobe Experience Platform 사용자 인터페이스에서 대상에 사용해야 하는 UI 요소를 나타냅니다. 아래를 참조하십시오.

![UI 속성 구성 이미지.](/help/destinations/destination-sdk/assets/ui-attributes-configuration.png)

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `documentationLink` | 문자열 | 에서 설명서 페이지를 참조하십시오. [대상 카탈로그](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 목적지로요 사용 `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, 여기서 `YOURDESTINATION` 는 대상 이름입니다. Moviestar라는 대상의 경우 `http://www.adobe.com/go/destinations-moviestar-en`. 이 링크는 Adobe이 대상을 라이브로 설정하고 설명서가 게시된 후에만 작동합니다. |
| `category` | 문자열 | Adobe Experience Platform에서 대상에 할당된 카테고리를 나타냅니다. 자세한 내용은 다음을 참조하십시오 [대상 범주](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). 다음 값 중 하나를 사용합니다. `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br> 현재는 대상당 하나의 범주만 선택할 수 있습니다. |
| `connectionType` | 문자열 | `Server-to-server` 는 현재 사용 가능한 유일한 옵션입니다. |
| `frequency` | 문자열 | 대상에서 지원하는 데이터 내보내기 유형을 나타냅니다. 지원되는 값: <ul><li>`Streaming`</li><li>`Batch`</li></ul> |

{style="table-layout:auto"}

## 매핑 단계의 스키마 구성 {#schema-configuration}

![매핑 단계 활성화](./assets/enable-mapping-step.png)

에서 매개 변수 사용 `schemaConfig` 대상 활성화 워크플로의 매핑 단계를 활성화합니다. 아래 설명된 매개 변수를 사용하여 Experience Platform 사용자가 프로필 속성 및/또는 ID를 대상 측의 원하는 스키마에 매핑할 수 있는지 여부를 결정할 수 있습니다.

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `profileFields` | 배열 | *위의 예제 구성에 표시되지 않습니다.* 사전 정의된 항목을 추가할 때 `profileFields`, Experience Platform 사용자는 Platform 속성을 대상 측의 사전 정의된 속성에 매핑할 수 있는 옵션이 있습니다. |
| `profileRequired` | 부울 | 사용 `true` 위의 예제 구성에 표시된 대로 사용자가 Experience Platform의 프로필 속성을 대상 측의 사용자 지정 속성에 매핑할 수 있어야 하는 경우입니다. |
| `segmentRequired` | 부울 | 항상 사용 `segmentRequired:true`. |
| `identityRequired` | 부울 | 사용 `true` 사용자가 Experience Platform의 id 네임스페이스를 원하는 스키마에 매핑할 수 있어야 하는 경우. |

{style="table-layout:auto"}

## ID 및 속성 {#identities-and-attributes}

이 섹션의 매개 변수는 대상이 허용하는 ID를 결정합니다. 이 구성은 또한 의 타겟 ID 및 속성을 채웁니다. [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) XDM 스키마의 ID 및 속성을 대상의 스키마에 매핑하는 Experience Platform 사용자 인터페이스의 .

다음을 나타내야 합니다. [!DNL Platform] id 고객은 대상으로 내보낼 수 있습니다. 몇 가지 예는 다음과 같습니다 [!DNL Experience Cloud ID], 해시된 이메일, 장치 ID([!DNL IDFA], [!DNL GAID]). 이 값은 다음과 같습니다 [!DNL Platform] 고객이 대상에서 id 네임스페이스에 매핑할 수 있는 id 네임스페이스. 또한 고객이 사용자 정의 네임스페이스를 대상에서 지원하는 ID에 매핑할 수 있는지 여부를 나타낼 수도 있습니다(`acceptsCustomNamespaces: true`) 및 고객이 표준 XDM 속성을 대상에서 지원하는 ID에 매핑할 수 있는 경우(`acceptsAttributes: true`).

ID 네임스페이스는 다음 사이에 1:1 대응이 필요하지 않습니다. [!DNL Platform] 목적지도요
예를 들어 고객은 를 매핑할 수 있습니다. [!DNL Platform] [!DNL IDFA] 네임스페이스를 다음에 추가 [!DNL IDFA] 대상에서 네임스페이스를 매핑하거나 동일한 네임스페이스를 [!DNL Platform] [!DNL IDFA] 네임스페이스 대상 [!DNL Customer ID] 네임스페이스를 대상에 추가합니다.

에서 ID에 대해 자세히 알아보기 [ID 네임스페이스 개요](/help/identity-service/namespaces.md).

![UI에서 대상 ID 렌더링](./assets/target-identities-ui.png)

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `acceptsAttributes` | 부울 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `acceptsCustomNamespaces` | 부울 | 고객이 대상에서 사용자 정의 네임스페이스를 설정할 수 있는지 여부를 나타냅니다. |
| `transformation` | 문자열 | *예제 구성에 표시되지 않음*. 다음과 같은 경우에 사용됩니다. [!DNL Platform] 고객은 일반 이메일 주소를 속성으로 가지고 있으며 플랫폼은 해시된 이메일만 허용합니다. 이 객체에서는 적용해야 하는 변형을 적용할 수 있습니다(예: 이메일을 소문자로 변환한 다음 해시로 변환). 예를 보려면 다음을 참조하십시오. `requiredTransformation` 다음에서 [대상 구성 API 참조](./destination-configuration-api.md#update). |
| `acceptedGlobalNamespaces` | - | 다음 항목을 나타냅니다. [표준 id 네임스페이스](/help/identity-service/namespaces.md#standard) (예: IDFA) 고객은 구성 중인 ID에 매핑할 수 있습니다. <br> 를 사용할 때 `acceptedGlobalNamespaces`, 다음을 사용할 수 있습니다 `"requiredTransformation":"sha256(lower($))"` 이메일 주소 또는 전화 번호를 소문자로 나타내고 해시합니다. |

{style="table-layout:auto"}

## 대상 게재 {#destination-delivery}

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `authenticationRule` | 문자열 | 방법을 나타냅니다. [!DNL Platform] 고객이 대상에 연결합니다. 허용되는 값은 다음과 같습니다 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>사용 `CUSTOMER_AUTHENTICATION` platform 고객이 사용자 이름과 암호, 전달자 토큰 또는 다른 인증 방법을 통해 시스템에 로그인하는 경우. 예를 들어 을 선택한 경우 이 옵션을 선택합니다 `authType: OAUTH2` 또는 `authType:BEARER` 위치: `customerAuthenticationConfigurations`. </li><li> 사용 `PLATFORM_AUTHENTICATION` Adobe과 대상 및 간에 글로벌 인증 시스템이 있는 경우 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 개체를 만들어야 합니다 [자격 증명](./credentials-configuration-api.md) 구성. </li><li>사용 `NONE` 대상 플랫폼으로 데이터를 전송하는 데 인증이 필요하지 않은 경우 </li></ul> |
| `destinationServerId` | 문자열 | 다음 `instanceId` / [대상 서버 구성](./destination-server-api.md) 이 대상에 사용됩니다. |

{style="table-layout:auto"}

## 세그먼트 매핑 구성 {#segment-mapping}

![세그먼트 매핑 구성 섹션](./assets/segment-mapping-configuration.png)

대상 구성의 이 섹션은 Experience Platform 이름 또는 ID와 같은 세그먼트 메타데이터를 세그먼트와 대상 간에 공유하는 방식과 관련이 있습니다.

다음을 통해 `audienceTemplateId`, 이 섹션은 또한 이 구성을 [대상 메타데이터 구성](./audience-metadata-management.md).

위의 구성에 표시된 매개변수는 [대상 끝점 API 참조](./destination-configuration-api.md).

## 집계 정책 {#aggregation}

![구성 템플릿의 집계 정책](./assets/aggregation-configuration.png)

이 섹션에서는 데이터를 대상으로 내보낼 때 Experience Platform이 사용해야 하는 집계 정책을 설정할 수 있습니다.

집계 정책은 내보낸 프로필이 데이터 내보내기에서 결합되는 방식을 결정합니다. 사용 가능한 옵션은 다음과 같습니다.
* 최상의 작업 집계
* 구성 가능한 합계 (위의 구성에 표시됨)

의 섹션 읽기 [템플릿 사용](./message-format.md#using-templating) 및 [집계 키 예](./message-format.md#template-aggregation-key) 선택한 집계 정책을 기반으로 메시지 변환 템플릿에 집계 정책을 포함하는 방법을 이해합니다.

### 최상의 작업 집계 {#best-effort-aggregation}

>[!TIP]
>
>API 끝점이 API 호출당 100개 미만의 프로필을 허용하는 경우 이 옵션을 사용합니다.

이 옵션은 요청당 프로필 수를 줄이고, 데이터가 많은 요청보다 데이터가 적은 요청을 더 많이 받는 대상에 가장 적합합니다.

사용 `maxUsersPerRequest` 매개 변수를 사용하여 대상에서 요청할 수 있는 최대 프로필 수를 지정합니다.

### 구성 가능한 집계 {#configurable-aggregation}

이 옵션은 동일한 호출에 수천 개의 프로필이 있는 대용량 일괄 처리를 하려는 경우에 가장 적합합니다. 이 옵션을 사용하면 복잡한 집계 규칙을 기반으로 내보낸 프로필을 집계할 수도 있습니다.

이 옵션을 사용하면 다음 작업을 수행할 수 있습니다.

* 대상에 API 호출이 수행되기 전에 집계할 최대 프로필 수와 시간을 설정합니다.
* 다음을 기반으로 대상에 매핑된 내보낸 프로필 집계:
   * 세그먼트 ID;
   * 세그먼트 상태;
   * ID 또는 ID 그룹.

>[!NOTE]
>
>대상에 대해 구성 가능한 합계 옵션을 사용할 때는 두 매개 변수에 사용할 수 있는 최소값과 최대값을 염두에 두어야 합니다 `maxBatchAgeInSecs` (최소 1,800 ~ 최대 3,600) 및 `maxNumEventsInBatch` (최소 1,000개, 최대 10,000개).

합계 매개변수에 대한 자세한 설명은 다음을 참조하십시오. [대상 API 엔드포인트 작업](./destination-configuration-api.md) 각 매개 변수에 대해 설명하는 참조 페이지입니다.

## 과거 프로필 자격 요건 {#profile-backfill}

다음을 사용할 수 있습니다. `backfillHistoricalProfileData` 대상 구성의 매개 변수를 사용하여 이전 프로필 자격을 대상으로 내보내야 하는지 여부를 결정합니다.

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `backfillHistoricalProfileData` | 부울 | 세그먼트가 대상으로 활성화될 때 내역 프로필 데이터를 내보내는지 여부를 제어합니다. <br> <ul><li> `true`: [!DNL Platform] 세그먼트가 활성화되기 전에 세그먼트에 적합한 내역 사용자 프로필을 보냅니다. </li><li> `false`: [!DNL Platform] 는 세그먼트가 활성화된 후에만 해당 세그먼트에 적합한 사용자 프로필을 포함합니다. </li></ul> |

{style="table-layout:auto"}

## 이 구성이 대상에 필요한 모든 정보를 연결하는 방법 {#connecting-all-configurations}

일부 대상 설정은 다음을 통해 구성해야 합니다. [대상 서버](./server-and-template-configuration.md) 또는 [대상 메타데이터 구성](./audience-metadata-management.md). 여기에 설명된 대상 구성은 다음과 같이 다른 두 구성을 참조하여 이러한 모든 설정을 연결합니다.

* 사용 `destinationServerId` 대상 서버 및 대상에 대해 설정된 템플릿 구성을 참조합니다.
* 사용 `audienceMetadataId` 대상에 대해 설정된 대상 메타데이터 구성을 참조합니다.