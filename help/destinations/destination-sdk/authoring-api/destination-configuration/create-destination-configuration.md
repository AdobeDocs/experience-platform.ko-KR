---
description: Adobe Experience Platform Destination SDK을 통해 대상 구성을 만들기 위해 API 호출을 구성하는 방법을 알아봅니다.
title: 대상 구성 만들기
exl-id: aae4aaa8-1dd0-4041-a86c-5c86f04d7d13
source-git-commit: 20cb2dbfbfc8e73c765073818c8e7e561d4e6629
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 3%

---

# 대상 구성 만들기

이 페이지는 `/authoring/destinations` API 끝점을 사용하여 고유한 대상 구성을 만드는 데 사용할 수 있는 API 요청 및 페이로드를 예시합니다.

이 끝점을 통해 구성할 수 있는 기능에 대한 자세한 설명은 다음 문서를 참조하십시오.

* [고객 인증 구성](../../functionality/destination-configuration/customer-authentication.md)
* [OAuth2 인증](../../functionality/destination-configuration/oauth2-authorization.md)
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
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 대상 구성 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 대상 구성 만들기 {#create}

`/authoring/destinations` 끝점에 대한 POST 요청을 수행하여 새 대상 구성을 만들 수 있습니다.

>[!TIP]
>
>**API 끝점**: `platform.adobe.io/data/core/activation/authoring/destinations`

**API 형식**

```http
POST /authoring/destinations
```

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 [!DNL Amazon S3] 대상 구성을 만듭니다. 아래 페이로드에는 `/authoring/destinations` 끝점에서 허용하는 파일 기반 대상에 대한 모든 매개 변수가 포함되어 있습니다.

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
| `description` | 문자열 | Adobe이 대상 카드의 Experience Platform 대상 카탈로그에서 사용할 설명을 입력합니다. 4-5개 이하의 문장을 목표로 하라. 대상 설명을 표시하는 ![플랫폼 UI 이미지입니다.](../../assets/authoring-api/destination-configuration/destination-description.png "대상 설명"){width="100" zoomable="yes"} |
| `status` | 문자열 | 대상 카드의 라이프사이클 상태를 나타냅니다. 허용되는 값은 `TEST`, `PUBLISHED` 및 `DELETED`입니다. 대상을 처음 구성할 때 `TEST`을(를) 사용하십시오. |
| `customerAuthenticationConfigurations.authType` | 문자열 | 대상 서버에 Experience Platform 고객을 인증하는 데 사용되는 구성을 나타냅니다. 지원되는 인증 유형에 대한 자세한 내용은 [고객 인증 구성](../../functionality/destination-configuration/customer-authentication.md)을 참조하십시오. |
| `customerDataFields.name` | 문자열 | 도입 중인 사용자 정의 필드의 이름을 입력합니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하십시오. 고객 데이터 필드를 표시하는 ![플랫폼 UI 이미지입니다.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "고객 데이터 필드"){width="100" zoomable="yes"} |
| `customerDataFields.type` | 문자열 | 도입 중인 사용자 정의 필드 유형을 나타냅니다. 허용되는 값은 `string`, `object`, `integer`입니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하십시오. |
| `customerDataFields.title` | 문자열 | Experience Platform 사용자 인터페이스에서 고객에게 표시되는 필드의 이름을 나타냅니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하십시오. |
| `customerDataFields.description` | 문자열 | 사용자 정의 필드에 대한 설명을 입력합니다. 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하세요. |
| `customerDataFields.isRequired` | 부울 | 대상 설정 워크플로에서 이 필드가 필요한지 여부를 나타냅니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하십시오. |
| `customerDataFields.enum` | 문자열 | 사용자 정의 필드를 드롭다운 메뉴로 렌더링하고 사용자가 사용할 수 있는 옵션을 나열합니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하십시오. |
| `customerDataFields.default` | 문자열 | `enum` 목록에서 기본값을 정의합니다. |
| `customerDataFields.pattern` | 문자열 | 필요한 경우 사용자 정의 필드에 패턴을 적용합니다. 패턴을 적용하려면 정규 표현식을 사용하십시오. 예를 들어 고객 ID에 숫자나 밑줄이 포함되지 않은 경우 이 필드에 `^[A-Za-z]+$`을(를) 입력합니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)를 참조하십시오. |
| `uiAttributes.documentationLink` | 문자열 | 대상의 [대상 카탈로그](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html#catalog)에 있는 문서 페이지를 참조합니다. `https://www.adobe.com/go/destinations-YOURDESTINATION-en`을(를) 사용합니다. 여기서 `YOURDESTINATION`은(는) 대상 이름입니다. Moviestar라는 대상의 경우 `https://www.adobe.com/go/destinations-moviestar-en`을(를) 사용합니다. 이 링크는 Adobe이 대상을 라이브로 설정하고 설명서가 게시된 후에만 작동합니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [UI 특성](../../functionality/destination-configuration/ui-attributes.md)을 참조하십시오. 설명서 링크를 표시하는 ![플랫폼 UI 이미지입니다.](../../assets/authoring-api/destination-configuration/documentation-url.png "설명서 URL"){width="100" zoomable="yes"} |
| `uiAttributes.category` | 문자열 | Adobe Experience Platform에서 대상에 할당된 카테고리를 나타냅니다. 자세한 내용은 [대상 범주](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html#destination-categories)를 참조하세요. `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` 값 중 하나를 사용합니다. <br/><br/> 이러한 설정에 대한 자세한 내용은 [UI 특성](../../functionality/destination-configuration/ui-attributes.md)을 참조하십시오. |
| `uiAttributes.connectionType` | 문자열 | 대상에 따른 연결 유형입니다. 지원되는 값: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | 문자열 | 대상에서 지원하는 데이터 내보내기 유형을 나타냅니다. API 기반 통합을 위해 `Streaming`(으)로 설정하거나 파일을 대상으로 내보낼 때 `Batch`(으)로 설정합니다. |
| `identityNamespaces.externalId.acceptsAttributes` | 부울 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | 부울 | 고객이 [사용자 지정 네임스페이스](/help/identity-service/features/namespaces.md#manage-namespaces)에 속하는 ID를 구성할 수 있는지 여부를 나타냅니다. |
| `identityNamespaces.externalId.transformation` | 문자열 | _예제 구성에 표시되지 않음_. 예를 들어 [!DNL Platform] 고객이 일반 이메일 주소를 특성으로 가지고 있고 플랫폼이 해시된 이메일만 수락하는 경우 사용됩니다. 여기에서 적용해야 하는 변형을 제공합니다(예: 이메일을 소문자로 변환한 다음 해시로 변환). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | 사용자가 구성하는 ID에 고객이 매핑할 수 있는 [표준 ID 네임스페이스](/help/identity-service/features/namespaces.md#standard)(예: IDFA)를 나타냅니다. <br> `acceptedGlobalNamespaces`을(를) 사용하는 경우 `"requiredTransformation":"sha256(lower($))"`을(를) 사용하여 전자 메일 주소 또는 전화 번호를 소문자로 나타내고 해시할 수 있습니다. |
| `destinationDelivery.authenticationRule` | 문자열 | [!DNL Platform]명의 고객이 대상에 연결하는 방법을 나타냅니다. 허용되는 값은 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`입니다. <br> <ul><li>플랫폼 고객이 사용자 이름과 암호, 전달자 토큰 또는 다른 인증 방법을 통해 시스템에 로그인하는 경우 `CUSTOMER_AUTHENTICATION`을(를) 사용합니다. 예를 들어 `customerAuthenticationConfigurations`에서 `authType: OAUTH2` 또는 `authType:BEARER`도 선택한 경우 이 옵션을 선택합니다. </li><li> Adobe과 대상 사이에 전역 인증 시스템이 있고 [!DNL Platform] 고객이 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없는 경우 `PLATFORM_AUTHENTICATION`을(를) 사용합니다. 이 경우 [자격 증명 API](../../credentials-api/create-credential-configuration.md) 구성을 사용하여 자격 증명 개체를 만들어야 합니다. </li><li>대상 플랫폼으로 데이터를 보내는 데 인증이 필요하지 않은 경우 `NONE`을(를) 사용합니다. </li></ul> |
| `destinationDelivery.destinationServerId` | 문자열 | 이 대상에 사용된 [대상 서버 템플릿](../destination-server/create-destination-server.md)의 `instanceId`입니다. |
| `backfillHistoricalProfileData` | 부울 | 대상이 대상으로 활성화될 때 내역 프로필 데이터를 내보내는지 여부를 제어합니다. 항상 `true`(으)로 설정하십시오. |
| `segmentMappingConfig.mapUserInput` | 부울 | 대상 활성화 워크플로의 대상 매핑 ID가 사용자에 의해 입력되는지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | 부울 | 대상 활성화 워크플로의 대상 매핑 ID가 Experience Platform 대상 ID인지 여부를 제어합니다. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | 부울 | 대상 활성화 워크플로의 대상 매핑 ID가 Experience Platform 대상 이름인지 여부를 제어합니다. |
| `segmentMappingConfig.audienceTemplateId` | 문자열 | 이 대상에 사용된 [대상 메타데이터 템플릿](../../metadata-api/create-audience-template.md)의 `instanceId`입니다. |
| `schemaConfig.profileFields` | 배열 | 위의 구성에 표시된 대로 사전 정의된 `profileFields`을(를) 추가하면 사용자는 Experience Platform 특성을 대상 쪽의 사전 정의된 특성에 매핑할 수 있습니다. |
| `schemaConfig.profileRequired` | 부울 | 사용자가 위의 예제 구성에 표시된 대로 Experience Platform의 프로필 특성을 대상 측의 사용자 지정 특성에 매핑할 수 있어야 하는 경우 `true`을(를) 사용합니다. |
| `schemaConfig.segmentRequired` | 부울 | 항상 `segmentRequired:true`을(를) 사용하십시오. |
| `schemaConfig.identityRequired` | 부울 | 사용자가 Experience Platform에서 원하는 스키마로 ID 네임스페이스를 매핑할 수 있어야 하는 경우 `true`을(를) 사용합니다. |

{style="table-layout:auto"}

+++

+++응답

성공적인 응답은 새로 생성된 대상 구성에 대한 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 Destination SDK `/authoring/destinations` API 끝점을 통해 새 대상 구성을 만드는 방법을 알 수 있습니다.

이 끝점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 구성 검색](retrieve-destination-configuration.md)
* [대상 구성 업데이트](update-destination-configuration.md)
* [대상 구성 삭제](delete-destination-configuration.md)

이 끝점이 대상 작성 프로세스에 맞는 위치를 이해하려면 다음 문서를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
