---
description: Destination SDK을 사용하여 사용자 지정 파일 이름 및 서식 옵션을 사용하여 Amazon S3 대상을 구성하는 방법을 알아봅니다.
title: (베타) 사용자 지정 파일 이름 및 서식 옵션을 사용하여 Amazon S3 대상을 구성합니다.
source-git-commit: 1e6515bf4fe34258194f56d341e477a02a1c31be
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# (베타) 사용자 지정 파일 이름 및 서식 옵션을 사용하여 Amazon S3 대상을 구성합니다

## 개요 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK을 사용하여 파일 기반 대상을 구성하는 기능은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

이 페이지에서는 Destination SDK을 사용하여 사용자 지정 Amazon S3 대상을 구성하는 방법을 설명합니다 [파일 서식 옵션](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) 및 사용자 지정 [파일 이름 구성](/help/destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration).

이 페이지에는 Amazon S3 대상에 사용할 수 있는 모든 구성 옵션이 표시됩니다. 아래 단계에 표시된 구성을 편집하거나 필요에 따라 구성의 특정 부분을 삭제할 수 있습니다.

## 전제 조건 {#prerequisites}

아래 요약된 단계로 이동하기 전에 다음을 참조하십시오. [Destination SDK 시작](/help/destinations/destination-sdk/getting-started.md) 페이지 를 참조하십시오.

## 1단계: 서버 및 파일 구성 만들기 {#create-server-file-configuration}

을 사용하여 시작합니다 `/destination-server` 서버 및 파일 구성을 만드는 끝점입니다. HTTP 요청의 매개 변수에 대한 자세한 내용은 [파일 기반 대상에 대한 서버 및 파일 구성 사양](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example) 그리고 [파일 형식 구성](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration).

**API 형식**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 대상 서버 구성을 만듭니다.
아래 페이로드에는 사용자 지정 기능이 있는 일반 Amazon S3 구성이 포함되어 있습니다 [CSV 파일 형식](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) 사용자가 Experience Platform UI에서 정의할 수 있는 구성 매개 변수입니다.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d ' {
   "name":"Amazon S3 destination server with custom file formatting options",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.compression}}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.sep}}"
         },
         "encoding":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.encoding}}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quote}}"
         },
         "quoteAll":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.quoteAll}}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escape}}"
         },
         "escapeQuotes":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.escapeQuotes}}"
         },
         "header":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.header}}"
         },
         "ignoreLeadingWhiteSpace":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.ignoreLeadingWhiteSpace}}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.nullValue}}"
         },
         "dateFormat":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         },
         "charToEscapeQuoteEscaping":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.charToEscapeQuoteEscaping}}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{customerData.dateFormat}}"
         }
      }
   }
}'
```

성공적인 응답은 고유 식별자( )를 포함하여 새 대상 서버 구성을 반환합니다`instanceId`) 내의 아무 곳에나 삽입할 수 있습니다. 이 값은 다음 단계에서 필요에 따라 저장합니다.

## 2단계: 대상 구성 만들기 {#create-destination-configuration}

이전 단계에서 대상 서버와 파일 형식 구성을 만든 후 이제 `/destinations` 대상 구성을 만들기 위한 API 엔드포인트.

에서 서버 구성을 연결하려면 [1단계](#create-server-file-configuration) 이 대상 구성에 대해 `destinationServerId` 에서 대상 서버를 만들 때 얻은 값으로 아래의 API 요청에 있는 값 [1단계](#create-server-file-configuration).

아래 사용된 매개 변수에 대한 자세한 설명은 다음 페이지를 참조하십시오.

* [인증 구성](/help/destinations/destination-sdk/authentication-configuration.md#s3)
* [배치 대상 구성](/help/destinations/destination-sdk/file-based-destination-configuration.md#batch-configuration)
* [파일 기반 대상 구성 API 작업](/help/destinations/destination-sdk/destination-configuration-api.md#create-file-based)

**API 형식**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with custom file formatting options and custom file name configuration",
   "description":"Amazon S3 destination with custom file formatting options and custom file name configuration",
   "releaseNotes":"Amazon S3 destination with custom file formatting options and custom file name configuration",
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
         "name":"sep",
         "title":"Enter your desired separator for each field and value",
         "description":"Enter your desired separator for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Select the desired CSV file encoding",
         "description":"Select the desired CSV file encoding",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Quoted values escape character",
         "description":"Enter the desired character to be used for escaping quoted values.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Quote escaping character",
         "description":"Enter the desired character to be used for escaping quotes inside an already quoted value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Enclose quoted values within quotes",
         "description":"Select whether values containing quotes should always be enclosed in quotes.",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"Generate file header.",
         "description":"Select whether to write the names of columns as the first line of the exported files.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"Select whether leading whitespaces should be trimmed from exported values.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"NULL value string format",
         "description":"Enter the string representation of a NULL value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Enter the desired date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Quote escaping escape character",
         "description":"Enter the desired character to be used for escaping the escaping of a quote character.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Empty value string format",
         "description":"Enter the string representation of an empty value.",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
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
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
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

성공적인 응답은 고유 식별자( )를 포함하여 새 대상 구성을 반환합니다`instanceId`) 내의 아무 곳에나 삽입할 수 있습니다. 대상 구성을 업데이트하기 위해 추가 HTTP 요청을 수행해야 하는 경우 이 값을 필요에 따라 저장합니다.

## 3단계: Experience Platform UI 확인 {#verify-ui}

위의 구성에 따라 이제 Experience Platform 카탈로그에 사용할 새 개인 대상 카드가 표시됩니다.

![선택한 대상 카드가 있는 대상 카탈로그 페이지를 표시하는 화면 기록](../../assets/destination-card.gif)

아래 이미지 및 레코딩에서 [파일 기반 대상에 대한 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md) 대상 구성에서 선택한 옵션과 일치시킵니다.

대상에 대한 세부 사항을 입력할 때 구성 시 설정한 사용자 지정 데이터 필드가 어떻게 표시되는지 확인하십시오.

>[!TIP]
>
>대상 구성에 사용자 지정 데이터 필드를 추가하는 순서는 UI에 반영되지 않습니다. 사용자 지정 데이터 필드는 항상 아래 화면 기록에 표시되는 순서대로 표시됩니다.

![대상 세부 사항 채우기](../../assets/file-configuration-options.gif)

내보내기 간격을 예약할 때 표시되는 필드가 `batchConfig` 구성.
![예약 옵션 내보내기](../../assets/file-export-scheduling.png)

파일 이름 구성 옵션을 볼 때 표시되는 필드가 `filenameConfig` 구성에 설정한 옵션입니다.
![파일 구성 옵션](../../assets/file-naming-options.gif)

위에 언급된 필드를 조정하려면 을 반복합니다 [단계 1](#create-server-file-configuration) 및 [2개](#create-destination-configuration) 필요에 따라 구성을 수정합니다.

## 4단계: (선택 사항) 대상을 게시합니다 {#publish-destination}

>[!NOTE]
>
>사용자가 사용할 비공개 대상을 만들고 다른 고객이 사용할 수 있도록 대상 카탈로그에 게시하려고 하지 않는 경우 이 단계는 필요하지 않습니다.

대상을 구성한 후 [대상 게시 API](/help/destinations/destination-sdk/destination-publish-api.md) 검토를 위해 Adobe에 구성을 제출합니다.

## 5단계: (선택 사항) 대상을 문서화합니다 {#document-destination}

>[!NOTE]
>
>사용자가 사용할 비공개 대상을 만들고 다른 고객이 사용할 수 있도록 대상 카탈로그에 게시하려고 하지 않는 경우 이 단계는 필요하지 않습니다.

ISV(Independent Software Vendor) 또는 SI(System Integrator)가 [제품 통합](/help/destinations/destination-sdk/overview.md#productized-custom-integrations)를 사용하려면 [셀프 서비스 설명서 프로세스](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md) 에서 대상에 대한 제품 설명서 페이지를 만들려면 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md).

## 다음 단계 {#next-steps}

이 문서를 읽으면 이제 사용자 정의 작성 방법을 알 수 있습니다 [!DNL Amazon S3] Destination SDK 사용 대상. 다음으로, 팀이 [파일 기반 대상에 대한 활성화 워크플로우](/help/destinations/ui/activate-batch-profile-destinations.md) 데이터를 대상으로 내보내려면 다음을 수행하십시오.