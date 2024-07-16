---
description: 이 페이지는 Adobe Experience Platform Destination SDK을 통해 기존 대상 구성을 업데이트하는 데 사용되는 API 호출을 보여 줍니다.
title: 대상 구성 업데이트
exl-id: d7f18689-9806-4f73-a63a-fa112569819c
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# 대상 구성 업데이트

이 페이지에서는 `/authoring/destinations` API 끝점을 사용하여 기존 대상 구성을 업데이트하는 데 사용할 수 있는 API 요청 및 페이로드를 구현합니다.

>[!TIP]
>
>제품화된/공개 대상에 대한 모든 업데이트 작업은 [게시 API](../../publishing-api/create-publishing-request.md)를 사용하고 Adobe 검토를 위해 업데이트를 제출한 후에만 표시됩니다.

대상 구성의 기능에 대한 자세한 설명은 다음 문서를 참조하십시오.

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

## 대상 구성 업데이트 {#update}

업데이트된 페이로드로 `/authoring/destinations` 끝점에 대한 `PUT` 요청을 수행하여 [기존](create-destination-configuration.md) 대상 구성을 업데이트할 수 있습니다.

>[!TIP]
>
>API 끝점: `platform.adobe.io/data/core/activation/authoring/destinations`

기존 대상 구성 및 해당 `{INSTANCE_ID}`을(를) 가져오려면 [대상 구성 검색](retrieve-destination-configuration.md)에 대한 문서를 참조하십시오.

**API 형식**

```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 업데이트할 대상 구성의 ID입니다. 기존 대상 구성 및 해당 `{INSTANCE_ID}`을(를) 가져오려면 [대상 구성 검색](retrieve-destination-configuration.md)을 참조하십시오. |

+++요청

다음 요청은 [이 예제](create-destination-configuration.md#create)에서 만든 대상을 다른 `filenameConfig` 옵션으로 업데이트합니다.

```shell {line-numbers="true" highlight="115-128"}
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
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
   "customerEncryptionConfigurations":[
       
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
         "title":"File type",
         "description":"Select the exported file type.",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%_%DESTINATION_INSTANCE_ID%,"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

+++

+++응답

성공적인 응답은 업데이트된 대상 구성의 세부 정보와 함께 HTTP 상태 200을 반환합니다.

+++

## API 오류 처리 {#error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 Destination SDK `/authoring/destinations` API 끝점을 통해 대상 구성을 업데이트하는 방법을 배웁니다.

이 끝점으로 수행할 수 있는 작업에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [대상 구성 만들기](create-destination-configuration.md)
* [대상 구성 검색](retrieve-destination-configuration.md)
* [대상 구성 삭제](delete-destination-configuration.md)
