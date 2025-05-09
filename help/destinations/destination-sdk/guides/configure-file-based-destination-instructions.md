---
description: 이 페이지에서는 Destination SDK을 사용하여 파일 기반 대상을 구성하는 단계를 나열하고 설명합니다.
title: Destination SDK을 사용하여 파일 기반 대상 구성
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 804370a778a4334603f3235df94edaa91b650223
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Destination SDK을 사용하여 파일 기반 대상 구성

## 개요 {#overview}

이 페이지에서는 [대상 SDK](../functionality/configuration-options.md)의 구성 옵션 및 기타 Destination SDK 기능 및 API 참조 문서의 정보를 사용하여 [파일 기반 대상](../../destination-types.md#file-based)을 구성하는 방법에 대해 설명합니다. 단계는 아래에 순서대로 나열되어 있습니다.

## 전제 조건 {#prerequisites}

아래 표시된 단계로 진행하기 전에 [Destination SDK 시작하기](../getting-started.md) 페이지에서 Destination SDK API를 사용하는 데 필요한 Adobe I/O 인증 자격 증명 및 기타 필수 구성 요소를 가져오는 방법에 대한 정보를 참조하십시오.

## Destination SDK의 구성 옵션을 사용하여 대상을 설정하는 절차 {#steps}

![Destination SDK 엔드포인트를 사용하는 단계](../assets/guides/destination-sdk-steps-batch.png)

## 1단계: 서버 및 파일 구성 만들기 {#create-server-file-configuration}

`/destinations-server` 끝점을 사용하여 [서버 및 파일 구성을 만드는](../authoring-api/destination-server/create-destination-server.md)부터 시작합니다.

다음은 [!DNL Amazon S3] 대상에 대한 예제 구성입니다. 구성에 사용되는 필드에 대한 자세한 내용과 다른 유형의 파일 기반 대상을 구성하려면 해당 [서버 구성](../functionality/destination-server/server-specs.md)을 참조하십시오.

**API 형식**

```shell
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucketName}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

## 2단계: 대상 구성 만들기 {#create-destination-configuration}

다음은 `/destinations` API 끝점을 사용하여 만든 대상 구성의 예입니다.

1단계의 서버 및 파일 구성을 이 대상 구성에 연결하려면 여기에 서버 및 파일 구성의 `instance ID`을(를) `destinationServerId`(으)로 추가하십시오.

**API 형식**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json {line-numbers="true" highlight="83"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
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
      }
    },
    "backfillHistoricalProfileData": true
}
```

## 3단계: 대상 메타데이터 구성 만들기 {#create-audience-metadata-configuration}

일부 대상의 경우 Destination SDK에서는 대상에서 대상을 프로그래밍 방식으로 생성, 업데이트 또는 삭제하도록 대상 메타데이터 구성을 구성해야 합니다. 이 구성을 설정해야 하는 시기 및 방법에 대한 자세한 내용은 [대상 메타데이터 관리](../functionality/audience-metadata-management.md)를 참조하십시오.

대상 메타데이터 구성을 사용하는 경우 2단계에서 만든 대상 구성에 연결해야 합니다. 대상 구성에 대상 메타데이터 구성의 인스턴스 ID를 `audienceTemplateId`(으)로 추가합니다.

```json {line-numbers="true" highlight="90"}
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucketName",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "compression",
            "title": "Select compression type",
            "description": "Select the file compression type used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "enum": [
                "GZIP",
                "NONE",
                "bzip2",
                "lz4",
                "snappy",
                "deflate"
            ]
        },
        {
            "name": "fileType",
            "title": "Select a file format",
            "description": "Select the file format to be used by the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false,
            "enum": [
                "csv",
                "json",
                "parquet"
            ],
            "default": "csv"
        }
    ],
    "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/destinations-YOURDESTINATION-en",
        "category": "S3",
        "connectionType": "S3",
        "flowRunsSupported": true,
        "monitoringSupported": true,
        "frequency": "Batch"
    },
    "destinationDelivery": [
        {
            "deliveryMatchers": [
                {
                    "type": "SOURCE",
                    "value": [
                        "batch"
                    ]
                }
            ],
            "authenticationRule": "CUSTOMER_AUTHENTICATION",
            "destinationServerId": "eec25bde-4f56-4c02-a830-9aa9ec73ee9d"
        }
    ],
    "segmentMappingConfig":{
        "mapExperiencePlatformSegmentName":false,
        "mapExperiencePlatformSegmentId":false,
        "mapUserInput":false
    },
    "audienceMetadataConfig":{
        "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
    },   
    "schemaConfig": {
        "profileRequired": true,
        "segmentRequired": true,
        "identityRequired": true
    },
    "batchConfig": {
        "allowMandatoryFieldSelection": true,
        "allowDedupeKeyFieldSelection": true,
        "defaultExportMode": "DAILY_FULL_EXPORT",
        "allowedExportMode": [
            "DAILY_FULL_EXPORT",
            "FIRST_FULL_THEN_INCREMENTAL"
        ],
        "allowedScheduleFrequency": [
            "DAILY",
            "EVERY_3_HOURS",
            "EVERY_6_HOURS",
            "EVERY_8_HOURS",
            "EVERY_12_HOURS",
            "ONCE"
        ],
        "defaultFrequency": "DAILY",
        "defaultStartTime": "00:00",
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
      }
    },
    "backfillHistoricalProfileData": true
}
```

## 4단계: 인증 설정 {#set-up-authentication}

위의 대상 구성에서 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 또는 `"authenticationRule": "PLATFORM_AUTHENTICATION"`을(를) 지정하는지 여부에 따라 `/destination` 또는 `/credentials` 끝점을 사용하여 대상에 대한 인증을 설정할 수 있습니다.

>[!NOTE]
>
>`CUSTOMER_AUTHENTICATION`은(는) 두 인증 규칙 중 더 일반적이며 사용자가 연결을 설정하고 데이터를 내보내기 전에 대상에 일부 인증 형식을 제공해야 하는 경우 사용할 수 있는 규칙입니다.

* 대상 구성에서 `"authenticationRule": "CUSTOMER_AUTHENTICATION"`을(를) 선택한 경우 파일 기반 대상에 대해 Destination SDK에서 지원하는 인증 유형에 대해 다음 섹션을 참조하십시오.

   * [Amazon S3 인증](../functionality/destination-configuration/customer-authentication.md#s3)
   * [Azure Blob](../functionality/destination-configuration/customer-authentication.md#blob)
   * [Azure 데이터 레이크 스토리지](../functionality/destination-configuration/customer-authentication.md#adls)
   * [Google 클라우드 스토리지](../functionality/destination-configuration/customer-authentication.md#gcs)
   * [SSH 키를 사용한 SFTP 인증](../functionality/destination-configuration/customer-authentication.md#sftp-ssh)
   * [암호가 포함된 SFTP 인증](../functionality/destination-configuration/customer-authentication.md#sftp-password)

* `"authenticationRule": "PLATFORM_AUTHENTICATION"`을(를) 선택한 경우 [자격 증명 구성 API 설명서](../credentials-api/create-credential-configuration.md#when-to-use)를 참조하세요.


## 5단계: 대상 테스트 {#test-destination}

이전 단계의 구성 끝점을 사용하여 대상을 설정한 후 [대상 테스트 도구](../testing-api/batch-destinations/file-based-destination-testing-overview.md)를 사용하여 Adobe Experience Platform과 대상 간의 통합을 테스트할 수 있습니다.

대상을 테스트하는 프로세스의 일부로 Experience Platform UI를 사용하여 대상에 활성화할 대상을 만들어야 합니다. Experience Platform에서 대상자를 만드는 방법에 대한 지침은 아래 두 리소스를 참조하십시오.

* [대상자 만들기 - 설명서 페이지](/help/segmentation/ui/audience-portal.md#create-audience)
* [대상 만들기 - 비디오 연습](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=ko)

## 6단계: 대상 게시 {#publish-destination}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

대상을 구성하고 테스트한 후 [대상 게시 API](../publishing-api/create-publishing-request.md)를 사용하여 Adobe에 구성을 제출하여 검토하십시오.

## 7단계: 대상 문서화 {#document-destination}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

[제품화된 통합을 만드는 ISV(독립 소프트웨어 공급업체) 또는 SI(시스템 통합자)인 경우](../overview.md#productized-custom-integrations) [셀프 서비스 설명서 프로세스](../docs-framework/documentation-instructions.md)를 사용하여 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md)에서 대상에 대한 제품 설명서 페이지를 만드십시오.

## 8단계: Adobe 검토 대상 제출 {#submit-for-review}

>[!NOTE]
>
>이 단계는 직접 사용할 개인 대상을 만들고 다른 고객이 사용할 대상 카탈로그에 게시하려고 하지 않는 경우에는 필요하지 않습니다.

마지막으로, 대상을 Experience Platform 카탈로그에 게시하여 모든 Experience Platform 고객에게 표시하려면 먼저 Adobe의 검토를 위해 대상을 공식적으로 제출해야 합니다. Destination SDK에서 작성된 제품화된 대상을 검토하기 위해 [제출](../guides/submit-destination.md)하는 방법에 대한 전체 정보를 찾으십시오.
