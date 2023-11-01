---
description: Adobe Experience Platform Destination SDK을 통해 대상 구성을 만들기 위해 API 호출을 구성하는 방법을 알아봅니다.
title: 대상 구성 만들기
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 3%

---

# 대상 구성 만들기

이 페이지는 를 사용하여 고유한 대상 구성을 생성하는 데 사용할 수 있는 API 요청 및 페이로드를 예시합니다. `/authoring/destinations` API 엔드포인트.

이 끝점을 통해 구성할 수 있는 기능에 대한 자세한 설명은 다음 문서를 참조하십시오.

* [고객 인증 구성](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2 인증](../../functionality/destination-configuration/oauth2-authentication.md)
* [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)
* [UI 속성](../../functionality/destination-configuration/ui-attributes.md)
* [스키마 구성](../../functionality/destination-configuration/schema-configuration.md)
* [ID 네임스페이스 구성](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [대상 게재](../../functionality/destination-configuration/destination-delivery.md)
* [대상 메타데이터 구성](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [대상 메타데이터 구성](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [집계 정책](../../functionality/destination-configuration/aggregation-policy.md)
* [일괄 처리 구성](../../functionality/destination-configuration/batch-configuration.md)
* [과거 프로필 자격 요건](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 구성 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](../../getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상 구성 만들기 {#create}

에 POST 요청을 하여 새 대상 구성을 만들 수 있습니다. `/authoring/destinations` 엔드포인트.

>[!TIP]
>
>**API 엔드포인트**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API 형식**

```http
POST /authoring/destinations
```

다음 요청은 새 를 만듭니다 [!DNL Amazon S3] 페이로드에 제공된 매개 변수로 구성된 대상 구성 아래 페이로드에는 가 허용하는 파일 기반 대상에 대한 모든 매개 변수가 포함되어 있습니다. `/authoring/destinations` 엔드포인트.

모든 매개 변수를 API 호출에 추가할 필요는 없으며, 페이로드는 API 요구 사항에 따라 사용자 지정할 수 있습니다.

+++요청

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `name` | 문자열 | Experience Platform 카탈로그에서 대상의 제목을 나타냅니다. |
| `description` | 문자열 | Adobe이 대상 카드의 Experience Platform 대상 카탈로그에서 사용할 설명을 입력합니다. 4-5개 이하의 문장을 목표로 하라. ![대상 설명을 표시하는 플랫폼 UI 이미지입니다.](../../assets/authoring-api/destination-configuration/destination-description.png "대상 설명"){width="100" zoomable="yes"} |
| `status` | 문자열 | 대상 카드의 라이프사이클 상태를 나타냅니다. 허용되는 값은 `TEST`, `PUBLISHED` 및 `DELETED`입니다. 사용 `TEST` 대상을 처음 구성할 때. |
| `customerAuthenticationConfigurations.authType` | 문자열 | 대상 서버에 Experience Platform 고객을 인증하는 데 사용되는 구성을 나타냅니다. 다음을 참조하십시오 [고객 인증 구성](../../functionality/destination-configuration/customer-authentication.md) 지원되는 인증 유형에 대한 자세한 내용은 을 참조하십시오. |
| `customerDataFields.name` | 문자열 | 도입 중인 사용자 정의 필드의 이름을 입력합니다. <br/><br/> 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. ![고객 데이터 필드를 보여주는 플랫폼 UI 이미지입니다.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "고객 데이터 필드"){width="100" zoomable="yes"} |
| `customerDataFields.type` | 문자열 | 도입 중인 사용자 정의 필드 유형을 나타냅니다. 허용되는 값은 다음과 같습니다 `string`, `object`, `integer`. <br/><br/> 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. |
| `customerDataFields.title` | 문자열 | Experience Platform 사용자 인터페이스에서 고객에게 표시되는 필드의 이름을 나타냅니다. <br/><br/> 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. |
| `customerDataFields.description` | 문자열 | 사용자 정의 필드에 대한 설명을 입력합니다. 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. |
| `customerDataFields.isRequired` | 부울 | 대상 설정 워크플로에서 이 필드가 필요한지 여부를 나타냅니다. <br/><br/> 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. |
| `customerDataFields.enum` | 문자열 | 사용자 정의 필드를 드롭다운 메뉴로 렌더링하고 사용자가 사용할 수 있는 옵션을 나열합니다. <br/><br/> 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. |
| `customerDataFields.default` | 문자열 | 에서 기본값 정의 `enum` 목록을 표시합니다. |
| `customerDataFields.pattern` | 문자열 | 필요한 경우 사용자 정의 필드에 패턴을 적용합니다. 패턴을 적용하려면 정규 표현식을 사용하십시오. 예를 들어 고객 ID에 숫자나 밑줄이 포함되지 않은 경우 을 입력합니다 `^[A-Za-z]+$` 이 필드에서. <br/><br/> 다음을 참조하십시오 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md) 를 참조하십시오. |
| `uiAttributes.documentationLink` | 문자열 | 에서 설명서 페이지를 참조하십시오. [대상 카탈로그](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html#catalog) 목적지로요 사용 `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, 여기서 `YOURDESTINATION` 는 대상 이름입니다. Moviestar라는 대상의 경우 `https://www.adobe.com/go/destinations-moviestar-en`. 이 링크는 Adobe이 대상을 라이브로 설정하고 설명서가 게시된 후에만 작동합니다. <br/><br/> 다음을 참조하십시오 [UI 속성](../../functionality/destination-configuration/ui-attributes.md) 를 참조하십시오. ![설명서 링크를 표시하는 플랫폼 UI 이미지입니다.](../../assets/authoring-api/destination-configuration/documentation-url.png "설명서 URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | 문자열 | Adobe Experience Platform에서 대상에 할당된 카테고리를 나타냅니다. 자세한 내용은 다음을 참조하십시오 [대상 범주](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html#destination-categories). 다음 값 중 하나를 사용합니다. `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> 다음을 참조하십시오 [UI 속성](../../functionality/destination-configuration/ui-attributes.md) 를 참조하십시오. |
| `uiAttributes.connectionType` | 문자열 | 대상에 따른 연결 유형입니다. 지원되는 값: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | 문자열 | 대상에서 지원하는 데이터 내보내기 유형을 나타냅니다. 다음으로 설정 `Streaming` API 기반 통합 또는 `Batch` 파일을 대상으로 내보낼 때 |
| `identityNamespaces.externalId.acceptsAttributes` | 부울 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 부울 | 고객이 다음에 속한 ID를 매핑할 수 있는지 여부를 나타냅니다. [사용자 정의 네임스페이스](/help/identity-service/namespaces.md#manage-namespaces) 를 추가합니다. |
| `identityNamespaces.externalId.transformation` | 문자열 | _예제 구성에 표시되지 않음_. 다음과 같은 경우에 사용됩니다. [!DNL Platform] 고객은 일반 이메일 주소를 속성으로 가지고 있으며 플랫폼은 해시된 이메일만 허용합니다. 여기에서 적용해야 하는 변형을 제공합니다(예: 이메일을 소문자로 변환한 다음 해시로 변환). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 다음 항목을 나타냅니다. [표준 id 네임스페이스](/help/identity-service/namespaces.md#standard) (예: IDFA) 고객은 구성 중인 ID에 매핑할 수 있습니다. <br> 를 사용할 때 `acceptedGlobalNamespaces`, 다음을 사용할 수 있습니다 `"requiredTransformation":"sha256(lower($))"` 이메일 주소 또는 전화 번호를 소문자로 나타내고 해시합니다. |
| `destinationDelivery.authenticationRule` | 문자열 | 방법을 나타냅니다. [!DNL Platform] 고객이 대상에 연결합니다. 허용되는 값은 다음과 같습니다 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>사용 `CUSTOMER_AUTHENTICATION` platform 고객이 사용자 이름과 암호, 전달자 토큰 또는 다른 인증 방법을 통해 시스템에 로그인하는 경우. 예를 들어 을 선택한 경우 이 옵션을 선택합니다 `authType: OAUTH2` 또는 `authType:BEARER` 위치: `customerAuthenticationConfigurations`. </li><li> 사용 `PLATFORM_AUTHENTICATION` Adobe과 대상 및 간에 글로벌 인증 시스템이 있는 경우 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 개체를 만들어야 합니다 [자격 증명 API](../../credentials-api/create-credential-configuration.md) 구성. </li><li>사용 `NONE` 대상 플랫폼으로 데이터를 전송하는 데 인증이 필요하지 않은 경우 </li></ul> |
| `destinationDelivery.destinationServerId` | 문자열 | 다음 `instanceId` / [대상 서버 템플릿](../destination-server/create-destination-server.md) 이 대상에 사용됩니다. |
| `backfillHistoricalProfileData` | 부울 | 대상이 대상으로 활성화될 때 내역 프로필 데이터를 내보내는지 여부를 제어합니다. 항상 다음으로 설정 `true`. |
| `segmentMappingConfig.mapUserInput` | 부울 | 대상 활성화 워크플로의 대상 매핑 ID가 사용자에 의해 입력되는지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 부울 | 대상 활성화 워크플로의 대상 매핑 ID가 Experience Platform 대상 ID인지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 부울 | 대상 활성화 워크플로의 대상 매핑 ID가 Experience Platform 대상 이름인지 여부를 제어합니다. |
| `segmentMappingConfig.audienceTemplateId` | 부울 | 다음 `instanceId` / [대상 메타데이터 템플릿](../../metadata-api/create-audience-template.md) 이 대상에 사용됩니다. |
| `schemaConfig.profileFields` | 배열 | 사전 정의된 항목을 추가할 때 `profileFields` 위의 구성에 표시된 대로 사용자는 Experience Platform 속성을 대상 측의 사전 정의된 속성에 매핑할 수 있습니다. |
| `schemaConfig.profileRequired` | 부울 | 사용 `true` 위의 예제 구성에 표시된 대로 사용자가 Experience Platform의 프로필 속성을 대상 측의 사용자 지정 속성에 매핑할 수 있어야 하는 경우입니다. |
| `schemaConfig.segmentRequired` | 부울 | 항상 사용 `segmentRequired:true`. |
| `schemaConfig.identityRequired` | 부울 | 사용 `true` 사용자가 Experience Platform에서 원하는 스키마로 id 네임스페이스를 매핑할 수 있어야 하는 경우 |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 새로 생성된 대상 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이 문서를 읽고 나면 이제 Destination SDK을 통해 새 대상 구성을 만드는 방법을 이해할 수 있습니다 `/authoring/destinations` API 엔드포인트.

이 끝점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 구성 검색](retrieve-destination-configuration.md)
* [대상 구성 업데이트](update-destination-configuration.md)
* [대상 구성 삭제](delete-destination-configuration.md)

이 끝점이 대상 작성 프로세스에 맞는 위치를 이해하려면 다음 문서를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
