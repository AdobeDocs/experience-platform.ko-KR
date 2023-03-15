---
description: 이 페이지에서는 "/authoring/destinations" API 끝점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 대상 API 엔드포인트 작업
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 59ac7749d788d8527da3578ec140248f7acf8e98
workflow-type: tm+mt
source-wordcount: '2539'
ht-degree: 4%

---

# 대상 엔드포인트 API 작업 {#destination-configuration}

>[!IMPORTANT]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destinations`

이 페이지에서는 다음을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/destinations` API 엔드포인트. 이 끝점에서 지원하는 기능에 대한 설명은 다음을 참조하십시오. [대상 구성](./destination-configuration.md).

## 대상 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 스트리밍 대상에 대한 구성 만들기 {#create}

에 POST 요청을 하여 새 대상 구성을 만들 수 있습니다. `/authoring/destinations` 엔드포인트.

**API 형식**

```http
POST /authoring/destinations
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 스트리밍 대상 구성을 만듭니다. 아래 페이로드에는 가 허용하는 스트리밍 대상에 대한 모든 매개 변수가 포함되어 있습니다. `/authoring/destinations` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
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
         "name":"endpointsInstance",
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
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `name` | 문자열 | Experience Platform 카탈로그에 대상의 제목을 나타냅니다. |
| `description` | 문자열 | Adobe이 대상 카드의 Experience Platform 대상 카탈로그에서 사용할 설명을 입력합니다. 4-5개 이하의 문장을 목표로 하라. |
| `status` | 문자열 | 대상 카드의 라이프사이클 상태를 나타냅니다. 허용되는 값은 `TEST`, `PUBLISHED` 및 `DELETED`입니다. 사용 `TEST` 대상을 처음 구성할 때. |
| `customerAuthenticationConfigurations` | 문자열 | 서버에 Experience Platform 고객을 인증하는 데 사용되는 구성을 나타냅니다. 다음을 참조하십시오 `authType` 허용되는 값은 아래를 참조하십시오. |
| `customerAuthenticationConfigurations.authType` | 문자열 | 스트리밍 대상에 대해 지원되는 값은 다음과 같습니다. <ul><li>`BASIC`</li><li>`BEARER`</li><li>`OAUTH2`</li></ul> 파일 기반 대상에 대해 지원되는 값은 다음과 같습니다. <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | 문자열 | 도입 중인 사용자 정의 필드의 이름을 입력합니다. |
| `customerDataFields.type` | 문자열 | 도입 중인 사용자 정의 필드 유형을 나타냅니다. 허용되는 값은 다음과 같습니다 `string`, `object`, `integer` |
| `customerDataFields.title` | 문자열 | Experience Platform 사용자 인터페이스에서 고객에게 표시되는 필드의 이름을 나타냅니다. |
| `customerDataFields.description` | 문자열 | 사용자 정의 필드에 대한 설명을 입력합니다. |
| `customerDataFields.isRequired` | 부울 | 대상 설정 워크플로에서 이 필드가 필요한지 여부를 나타냅니다. |
| `customerDataFields.enum` | 문자열 | 사용자 정의 필드를 드롭다운 메뉴로 렌더링하고 사용자가 사용할 수 있는 옵션을 나열합니다. |
| `customerDataFields.pattern` | 문자열 | 필요한 경우 사용자 정의 필드에 패턴을 적용합니다. 패턴을 적용하려면 정규 표현식을 사용하십시오. 예를 들어 고객 ID에 숫자나 밑줄이 포함되지 않은 경우 을 입력합니다 `^[A-Za-z]+$` 이 필드에서 을(를) 참조하십시오. |
| `uiAttributes.documentationLink` | 문자열 | 에서 설명서 페이지를 참조하십시오. [대상 카탈로그](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 목적지로요 사용 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, 여기서 `YOURDESTINATION` 는 대상 이름입니다. Moviestar라는 대상의 경우 `https://www.adobe.com/go/destinations-moviestar-en`. 이 링크는 Adobe이 대상을 라이브로 설정하고 설명서가 게시된 후에만 작동합니다. |
| `uiAttributes.category` | 문자열 | Adobe Experience Platform에서 대상에 할당된 카테고리를 나타냅니다. 자세한 내용은 다음을 참조하십시오 [대상 범주](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 다음 값 중 하나를 사용합니다. `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | 문자열 | `Server-to-server` 는 현재 사용 가능한 유일한 옵션입니다. |
| `uiAttributes.frequency` | 문자열 | `Streaming` 는 현재 사용 가능한 유일한 옵션입니다. |
| `identityNamespaces.externalId.acceptsAttributes` | 부울 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 부울 | 고객이 다음에 속한 ID를 매핑할 수 있는지 여부를 나타냅니다. [사용자 정의 네임스페이스](/help/identity-service/namespaces.md#manage-namespaces) 를 추가합니다. |
| `identityNamespaces.externalId.transformation` | 문자열 | _예제 구성에 표시되지 않음_. 다음과 같은 경우에 사용됩니다. [!DNL Platform] 고객은 일반 이메일 주소를 속성으로 가지고 있으며 플랫폼은 해시된 이메일만 허용합니다. 여기에서 적용해야 하는 변형을 제공합니다(예: 이메일을 소문자로 변환한 다음 해시로 변환). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 다음 항목을 나타냅니다. [표준 id 네임스페이스](/help/identity-service/namespaces.md#standard) (예: IDFA) 고객은 구성 중인 ID에 매핑할 수 있습니다. <br> 를 사용할 때 `acceptedGlobalNamespaces`, 다음을 사용할 수 있습니다 `"requiredTransformation":"sha256(lower($))"` 이메일 주소 또는 전화 번호를 소문자로 나타내고 해시합니다. |
| `destinationDelivery.authenticationRule` | 문자열 | 방법을 나타냅니다. [!DNL Platform] 고객이 대상에 연결합니다. 허용되는 값은 다음과 같습니다 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>사용 `CUSTOMER_AUTHENTICATION` platform 고객이 사용자 이름과 암호, 전달자 토큰 또는 다른 인증 방법을 통해 시스템에 로그인하는 경우. 예를 들어 을 선택한 경우 이 옵션을 선택합니다 `authType: OAUTH2` 또는 `authType:BEARER` 위치: `customerAuthenticationConfigurations`. </li><li> 사용 `PLATFORM_AUTHENTICATION` Adobe과 대상 및 간에 글로벌 인증 시스템이 있는 경우 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 개체를 만들어야 합니다 [자격 증명](./credentials-configuration-api.md) 구성. </li><li>사용 `NONE` 대상 플랫폼으로 데이터를 전송하는 데 인증이 필요하지 않은 경우 </li></ul> |
| `destinationDelivery.destinationServerId` | 문자열 | 다음 `instanceId` / [대상 서버 템플릿](./destination-server-api.md) 이 대상에 사용됩니다. |
| `backfillHistoricalProfileData` | 부울 | 세그먼트가 대상으로 활성화될 때 내역 프로필 데이터를 내보내는지 여부를 제어합니다. <br> <ul><li> `true`: [!DNL Platform] 세그먼트가 활성화되기 전에 세그먼트에 적합한 내역 사용자 프로필을 보냅니다. </li><li> `false`: [!DNL Platform] 는 세그먼트가 활성화된 후에만 해당 세그먼트에 적합한 사용자 프로필을 포함합니다. </li></ul> |
| `segmentMappingConfig.mapUserInput` | 부울 | 대상 활성화 워크플로의 세그먼트 매핑 ID가 사용자에 의해 입력되는지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 부울 | 대상 활성화 워크플로의 세그먼트 매핑 ID가 Experience Platform 세그먼트 ID인지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 부울 | 대상 활성화 워크플로의 세그먼트 매핑 ID가 Experience Platform 세그먼트 이름인지 여부를 제어합니다. |
| `segmentMappingConfig.audienceTemplateId` | 부울 | 다음 `instanceId` / [대상 메타데이터 템플릿](./audience-metadata-api.md) 이 대상에 사용됩니다. |
| `schemaConfig.profileFields` | 배열 | 사전 정의된 항목을 추가할 때 `profileFields` 위의 구성에 표시된 대로 사용자는 Experience Platform 속성을 대상 측의 사전 정의된 속성에 매핑할 수 있습니다. |
| `schemaConfig.profileRequired` | 부울 | 사용 `true` 위의 예제 구성에 표시된 대로 사용자가 Experience Platform의 프로필 속성을 대상 측의 사용자 지정 속성에 매핑할 수 있어야 하는 경우입니다. |
| `schemaConfig.segmentRequired` | 부울 | 항상 사용 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 부울 | 사용 `true` 사용자가 Experience Platform에서 원하는 스키마로 id 네임스페이스를 매핑할 수 있어야 하는 경우 |
| `aggregation.aggregationType` | - | `BEST_EFFORT` 또는 `CONFIGURABLE_AGGREGATION` 중 하나를 선택합니다. 위의 예제 구성은 다음을 포함합니다. `BEST_EFFORT` 집계. 의 예 `CONFIGURABLE_AGGREGATION`에서 예제 구성을 참조하십시오. [대상 구성](./destination-configuration.md#example-configuration) 문서. 구성 가능한 집계와 관련된 매개 변수는 이 표 아래에 설명되어 있습니다. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | 정수 | Experience Platform은 단일 HTTP 호출에서 내보낸 여러 프로필을 집계할 수 있습니다. 끝점이 단일 HTTP 호출에서 수신해야 하는 최대 프로필 수를 지정합니다. 이는 최선의 작업 집계입니다. 예를 들어 값을 100으로 지정하면 Platform이 호출 시 100보다 작은 수의 프로필을 보낼 수 있습니다. <br> 서버가 요청당 여러 사용자를 수락하지 않는 경우 이 값을 1로 설정하십시오. |
| `aggregation.bestEffortAggregation.splitUserById` | 부울 | 대상에 대한 호출을 ID로 분할해야 하는 경우 이 플래그를 사용합니다. 이 플래그를 다음으로 설정 `true` 서버가 주어진 네임스페이스에 대해 호출당 하나의 id만 허용하는 경우. |
| `aggregation.configurableAggregation.splitUserById` | 부울 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 대상에 대한 호출을 ID로 분할해야 하는 경우 이 플래그를 사용합니다. 이 플래그를 다음으로 설정 `true` 서버가 주어진 네임스페이스에 대해 호출당 하나의 id만 허용하는 경우. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | 정수 | <ul><li>*최소값: 1800*</li><li>*최대값: 3600*</li><li>예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 허용되는 최소 값과 최대 값 사이의 값을 구성합니다. 과 함께 `maxNumEventsInBatch`, 이 매개 변수는 API 호출을 엔드포인트로 보낼 때까지 Experience Platform이 대기하는 시간을 결정합니다. <br> 예를 들어 두 매개 변수에 모두 최대값을 사용하는 경우 Experience Platform은 API 호출을 수행하기 전에 3600초 또는 10,000개의 적격 프로필이 있을 때까지 기다리며, 둘 중 먼저 발생하는 작업이 수행됩니다. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | 정수 | <ul><li>*최소값: 1000*</li><li>*최대값: 10000*</li><li>예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 허용되는 최소 값과 최대 값 사이의 값을 구성합니다. 이 매개 변수에 대한 설명은 을 참조하십시오. `maxBatchAgeInSecs` 바로 위에.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | 부울 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 아래 매개 변수를 기반으로 대상에 매핑된 내보낸 프로필을 집계할 수 있습니다. <br> <ul><li>세그먼트 ID</li><li> 세그먼트 상태 </li><li> id 네임스페이스 </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | 부울 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 다음으로 설정 `true` 대상으로 내보낸 프로필을 세그먼트 ID로 그룹화하려는 경우. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | 부울 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 둘 다 설정해야 합니다. `includeSegmentId:true` 및 `includeSegmentStatus:true` 대상으로 내보낸 프로필을 세그먼트 ID 및 세그먼트 상태별로 그룹화하려는 경우. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | 부울 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 다음으로 설정 `true` 대상으로 내보낸 프로필을 id 네임스페이스별로 그룹화하려는 경우. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | 부울 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 이 매개 변수를 사용하여 내보낸 프로필을 단일 ID(GAID, IDFA, 전화 번호, 이메일 등) 그룹으로 집계할지 여부를 지정합니다. |
| `aggregation.configurableAggregation.aggregationKey.groups` | 문자열 | 예제 구성에서 매개 변수 를 참조하십시오 [여기](./destination-configuration.md#example-configuration). 대상으로 내보낸 프로필을 ID 네임스페이스 그룹별로 그룹화하려면 ID 그룹 목록을 만듭니다. 예를 들어 예제의 구성을 사용하여 IDFA 및 GAID 모바일 식별자를 포함하는 프로필을 대상에 대한 한 호출로 결합하고 이메일을 다른 호출로 결합할 수 있습니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 대상 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 파일 기반 대상에 대한 구성 만들기 {#create-file-based}

에 POST 요청을 하여 새 대상 구성을 만들 수 있습니다. `/authoring/destinations` 엔드포인트.

**API 형식**

```http
POST /authoring/destinations
```

**요청**

다음 요청은 새 를 만듭니다 [!DNL Amazon S3] 페이로드에 제공된 매개 변수로 구성된 파일 기반 대상 구성 아래 페이로드에는 가 허용하는 파일 기반 대상에 대한 모든 매개 변수가 포함되어 있습니다. `/authoring/destinations` 엔드포인트. 호출에 모든 매개 변수를 추가할 필요는 없으며 API 요구 사항에 따라 템플릿을 사용자 지정할 수 있습니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
            "allowedExportMode":[
                "DAILY_FULL_EXPORT",
                "FIRST_FULL_THEN_INCREMENTAL"
            ],
            "allowedScheduleFrequency":[
                "DAILY",
                "EVERY_3_HOURS",
                "EVERY_6_HOURS",
                "EVERY_8_HOURS",
                "EVERY_12_HOURS",
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

위의 모든 매개 변수에 대한 자세한 설명은 을 참조하십시오. [파일 기반 대상 구성](file-based-destination-configuration.md).

**응답**

성공적인 응답은 새로 생성된 대상 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

## 대상 구성 나열 {#retrieve-list}

에 GET 요청을 하여 IMS 조직에 대한 모든 대상 구성 목록을 검색할 수 있습니다. `/authoring/destinations` 엔드포인트.

**API 형식**


```http
GET /authoring/destinations
```

**요청**

다음 요청은 IMS 조직 및 샌드박스 구성을 기반으로 액세스 권한이 있는 대상 구성 목록을 검색합니다.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

다음 응답은 사용한 IMS 조직 ID와 샌드박스 이름을 기반으로 액세스 권한이 있는 대상 구성 목록과 함께 HTTP 상태 200을 반환합니다. 1개 `instanceId` 은 하나의 대상에 대한 템플릿에 해당합니다. 응답은 간결성을 위해 잘립니다.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
               "name":"endpointsInstance",
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
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
         "segmentMappingConfig":{
            "mapExperiencePlatformSegmentName":false,
            "mapExperiencePlatformSegmentId":false,
            "mapUserInput":false,
            "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
         },
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| 매개 변수 | 유형 | 설명 |
|---------|----------|------|
| `name` | 문자열 | Experience Platform 카탈로그에서 대상의 제목을 나타냅니다. |
| `description` | 문자열 | Adobe이 대상 카드의 Experience Platform 대상 카탈로그에서 사용할 설명을 입력합니다. 4-5개 이하의 문장을 목표로 하라. |
| `status` | 문자열 | 대상 카드의 라이프사이클 상태를 나타냅니다. 허용되는 값은 `TEST`, `PUBLISHED` 및 `DELETED`입니다. 사용 `TEST` 대상을 처음 구성할 때. |
| `customerAuthenticationConfigurations` | 문자열 | 서버에 Experience Platform 고객을 인증하는 데 사용되는 구성을 나타냅니다. 다음을 참조하십시오 `authType` 허용되는 값은 아래를 참조하십시오. |
| `customerAuthenticationConfigurations.authType` | 문자열 | 허용되는 값은 다음과 같습니다 `OAUTH2, BEARER`. |
| `customerDataFields.name` | 문자열 | 도입 중인 사용자 정의 필드의 이름을 입력합니다. |
| `customerDataFields.type` | 문자열 | 도입 중인 사용자 정의 필드 유형을 나타냅니다. 허용되는 값은 다음과 같습니다 `string`, `object`, `integer` |
| `customerDataFields.title` | 문자열 | Experience Platform 사용자 인터페이스에서 고객에게 표시되는 필드의 이름을 나타냅니다. |
| `customerDataFields.description` | 문자열 | 사용자 정의 필드에 대한 설명을 입력합니다. |
| `customerDataFields.isRequired` | 부울 | 대상 설정 워크플로에서 이 필드가 필요한지 여부를 나타냅니다. |
| `customerDataFields.enum` | 문자열 | 사용자 정의 필드를 드롭다운 메뉴로 렌더링하고 사용자가 사용할 수 있는 옵션을 나열합니다. |
| `customerDataFields.pattern` | 문자열 | 필요한 경우 사용자 정의 필드에 패턴을 적용합니다. 패턴을 적용하려면 정규 표현식을 사용하십시오. 예를 들어 고객 ID에 숫자나 밑줄이 포함되지 않은 경우 을 입력합니다 `^[A-Za-z]+$` 이 필드에서 을(를) 참조하십시오. |
| `uiAttributes.documentationLink` | 문자열 | 에서 설명서 페이지를 참조하십시오. [대상 카탈로그](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) 목적지로요 사용 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, 여기서 `YOURDESTINATION` 는 대상 이름입니다. Moviestar라는 대상의 경우 `https://www.adobe.com/go/destinations-moviestar-en`. 이 링크는 Adobe이 대상을 라이브로 설정하고 설명서가 게시된 후에만 작동합니다. |
| `uiAttributes.category` | 문자열 | Adobe Experience Platform에서 대상에 할당된 카테고리를 나타냅니다. 자세한 내용은 다음을 참조하십시오 [대상 범주](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). 다음 값 중 하나를 사용합니다. `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | 문자열 | `Server-to-server` 는 현재 사용 가능한 유일한 옵션입니다. |
| `uiAttributes.frequency` | 문자열 | `Streaming` 는 현재 사용 가능한 유일한 옵션입니다. |
| `identityNamespaces.externalId.acceptsAttributes` | 부울 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 부울 | 고객이 다음에 속한 ID를 매핑할 수 있는지 여부를 나타냅니다. [사용자 정의 네임스페이스](/help/identity-service/namespaces.md#manage-namespaces) 를 추가합니다. |
| `identityNamespaces.externalId.transformation` | 문자열 | _예제 구성에 표시되지 않음_. 다음과 같은 경우에 사용됩니다. [!DNL Platform] 고객은 일반 이메일 주소를 속성으로 가지고 있으며 플랫폼은 해시된 이메일만 허용합니다. 여기에서 적용해야 하는 변형을 제공합니다(예: 이메일을 소문자로 변환한 다음 해시로 변환). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 다음 항목을 나타냅니다. [표준 id 네임스페이스](/help/identity-service/namespaces.md#standard) (예: IDFA) 고객은 구성 중인 ID에 매핑할 수 있습니다. <br> 를 사용할 때 `acceptedGlobalNamespaces`, 다음을 사용할 수 있습니다 `"requiredTransformation":"sha256(lower($))"` 이메일 주소 또는 전화 번호를 소문자로 나타내고 해시합니다. |
| `destinationDelivery.authenticationRule` | 문자열 | 방법을 나타냅니다. [!DNL Platform] 고객이 대상에 연결합니다. 허용되는 값은 다음과 같습니다 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>사용 `CUSTOMER_AUTHENTICATION` platform 고객이 사용자 이름과 암호, 전달자 토큰 또는 다른 인증 방법을 통해 시스템에 로그인하는 경우. 예를 들어 을 선택한 경우 이 옵션을 선택합니다 `authType: OAUTH2` 또는 `authType:BEARER` 위치: `customerAuthenticationConfigurations`. </li><li> 사용 `PLATFORM_AUTHENTICATION` Adobe과 대상 및 간에 글로벌 인증 시스템이 있는 경우 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 개체를 만들어야 합니다 [자격 증명](./authentication-configuration.md) 구성. </li><li>사용 `NONE` 대상 플랫폼으로 데이터를 전송하는 데 인증이 필요하지 않은 경우 </li></ul> |
| `destinationDelivery.destinationServerId` | 문자열 | 다음 `instanceId` / [대상 서버 템플릿](./destination-server-api.md) 이 대상에 사용됩니다. |
| `destConfigId` | 문자열 | 이 필드는 자동으로 생성되며 입력이 필요하지 않습니다. |
| `backfillHistoricalProfileData` | 부울 | 세그먼트가 대상으로 활성화될 때 내역 프로필 데이터를 내보내는지 여부를 제어합니다. <br> <ul><li> `true`: [!DNL Platform] 세그먼트가 활성화되기 전에 세그먼트에 적합한 내역 사용자 프로필을 보냅니다. </li><li> `false`: [!DNL Platform] 는 세그먼트가 활성화된 후에만 해당 세그먼트에 적합한 사용자 프로필을 포함합니다. </li></ul> |
| `segmentMappingConfig.mapUserInput` | 부울 | 대상 활성화 워크플로의 세그먼트 매핑 ID가 사용자에 의해 입력되는지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 부울 | 대상 활성화 워크플로의 세그먼트 매핑 ID가 Experience Platform 세그먼트 ID인지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 부울 | 대상 활성화 워크플로의 세그먼트 매핑 ID가 Experience Platform 세그먼트 이름인지 여부를 제어합니다. |
| `segmentMappingConfig.audienceTemplateId` | 부울 | 다음 `instanceId` / [대상 메타데이터 템플릿](./audience-metadata-management.md) 이 대상에 사용됩니다. 대상 메타데이터 템플릿을 설정하려면 다음을 참조하십시오. [audience metadata API 참조](./audience-metadata-api.md). |

{style="table-layout:auto"}

## 기존 대상 구성 업데이트 {#update}

에 PUT 요청을 하여 기존 대상 구성을 업데이트할 수 있습니다. `/authoring/destinations` 엔드포인트 및 업데이트하려는 대상 구성의 인스턴스 ID 제공 호출 본문에서 업데이트된 대상 구성을 제공합니다.

**API 형식**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 대상 구성의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 기존 대상 구성을 업데이트합니다. 아래 예제 호출에서는 구성을 업데이트하는 중입니다 [이전에 생성됨](./destination-configuration-api.md#create) 이제 GAID, IDFA 및 해시된 이메일 식별자를 ID 네임스페이스로 허용합니다.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "name":"endpointsInstance",
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
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## 특정 대상 구성 검색 {#get}

에 GET 요청을 하여 특정 대상 구성에 대한 자세한 정보를 검색할 수 있습니다. `/authoring/destinations` 끝점 을 참조하고 검색할 대상 구성의 인스턴스 ID를 제공합니다.

**API 형식**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 검색할 대상 구성의 ID입니다. |

**요청**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 대상 구성에 대한 자세한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
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
         "name":"endpointsInstance",
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
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
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
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## 특정 대상 구성 삭제 {#delete}

에 DELETE 요청을 하여 지정된 대상 구성을 삭제할 수 있습니다. `/authoring/destinations` 엔드포인트 및 요청 경로에 삭제할 대상 구성의 ID 제공

**API 형식**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 다음 `id` 삭제할 대상 구성의 일부입니다. |

**요청**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 빈 HTTP 응답과 함께 HTTP 상태 200을 반환합니다.

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이 문서를 읽고 나면 이제 를 사용하여 대상을 구성하는 방법을 이해할 수 있습니다. `/authoring/destinations` API 엔드포인트. 읽기 [Destination SDK을 사용하여 대상을 구성하는 방법](./configure-destination-instructions.md) 대상을 구성하는 프로세스에 이 단계가 어디에 적합한지 이해할 수 있습니다.
