---
description: 이 페이지에서는 Destination SDK을 사용하여 파일 기반 대상을 구성하는 단계를 나열하고 설명합니다.
title: Destination SDK을 사용하여 파일 기반 대상 구성
exl-id: 84d73452-88e4-4e0f-8fc7-d0d8e10f9ff5
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# Destination SDK을 사용하여 파일 기반 대상 구성

## 개요 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK을 사용하여 파일 기반 대상을 구성하고 제출하는 기능은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

이 페이지에서는에서 정보를 사용하는 방법을 설명합니다. [대상 SDK의 구성 옵션](./configuration-options.md) 및 를 사용하여 다음을 구성할 수 있습니다 [파일 기반 대상](../../destinations/destination-types.md#file-based). 단계는 아래의 순차적 순서로 수행됩니다.

## 전제 조건 {#prerequisites}

아래 표시된 단계로 이동하기 전에 다음을 참조하십시오. [Destination SDK 시작](./getting-started.md) 페이지 를 참조하십시오.

## Destination SDK의 구성 옵션을 사용하여 대상을 설정하는 절차 {#steps}

![Destination SDK 종단점 사용 단계 설명](./assets/destination-sdk-steps-batch.png)

## 1단계: 서버 및 파일 구성 만들기 {#create-server-file-configuration}

먼저 을 사용하여 서버 및 파일 구성을 만듭니다 `/destinations-server` 엔드포인트(읽기 [API 참조](./destination-server-api.md)).

아래에 표시된 것은 [!DNL Amazon S3] 대상. 다른 유형의 파일 기반 대상을 구성하려면 해당 대상을 참조하십시오 [서버 구성](server-and-file-configuration.md).

**API 형식**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

```json
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
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

다음은 를 사용하여 만든 대상 구성의 예입니다. `/destinations` API 엔드포인트. 이 구성에 대한 자세한 내용은 [대상 구성](./file-based-destination-configuration.md).

1단계의 서버 및 파일 구성을 이 대상 구성에 연결하려면 서버 및 템플릿 구성의 인스턴스 ID를 `destinationServerId` 여기 있습니다.

**API 형식**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

```json
{
    "name": "Amazon S3 destination",
    "description": "Amazon S3 destination is a fictional destination, used for this example.",
    "releaseNotes": "Test",
    "status": "Test",
    "customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
    "customerEncryptionConfigurations": [],
    "customerDataFields": [
        {
            "name": "bucket",
            "title": "Amazon S3 bucket name",
            "description": "Enter the Amazon S3 Bucket name that will host the exported files.",
            "type": "string",
            "isRequired": true,
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "path",
            "title": "Amazon S3 path",
            "description": "Enter Amazon S3 folder path",
            "type": "string",
            "isRequired": true,
            "pattern": "^[A-Za-z]+$",
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
        "defaultStartTime": "00:00"
    },
    "backfillHistoricalProfileData": true
}
```

## 3단계: 대상 메타데이터 구성 만들기 {#create-audience-metadata-configuration}

일부 대상의 경우, Destination SDK을 사용하려면 대상의 대상을 프로그래밍 방식으로 만들거나, 업데이트하거나, 삭제하도록 대상 메타데이터 구성을 구성해야 합니다. 을(를) 참조하십시오. [대상 메타데이터 관리](./audience-metadata-management.md) 이 구성을 설정해야 하는 시점 및 이 작업을 수행하는 방법에 대한 자세한 정보를 제공합니다.

대상 메타데이터 구성을 사용하는 경우 이 구성을 2단계에서 만든 대상 구성에 연결해야 합니다. 대상 메타데이터 구성의 인스턴스 ID를 대상 구성에 다음으로 추가합니다. `audienceTemplateId`.

## 4단계: 인증 설정 {#set-up-authentication}

지정 여부에 따라 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 또는 `"authenticationRule": "PLATFORM_AUTHENTICATION"` 위의 대상 구성에서는 `/destination` 또는 `/credentials` 엔드포인트.

* 선택한 경우 `"authenticationRule": "CUSTOMER_AUTHENTICATION"` 대상 구성에서 파일 기반 대상에 대해 Destination SDK에서 지원하는 인증 유형에 대해서는 다음 섹션을 참조하십시오.

   * [Amazon S3 인증](authentication-configuration.md#s3)
   * [Azure Blob](authentication-configuration.md#blob)
   * [Azure Data Lake 저장소](authentication-configuration.md#adls)
   * [Google 클라우드 스토리지](authentication-configuration.md#gcs)
   * [SSH 키를 사용한 SFTP 인증](authentication-configuration.md#sftp-ssh)
   * [암호를 사용한 SFTP 인증](authentication-configuration.md#sftp-password)

* 선택한 경우 `"authenticationRule": "PLATFORM_AUTHENTICATION"`를 참조하려면 [인증 구성](./authentication-configuration.md#when-to-use).


<!-- ## Step 5: Test your destination {#test-destination}

After setting up your destination using the configuration endpoints in the previous steps, you can use the [destination testing tool](./create-template.md) to test the integration between Adobe Experience Platform and your destination.

As part of the process to test your destination, you must use the Experience Platform UI to create segments, which you will activate to your destination. Refer to the two resources below for instructions how to create segments in Experience Platform:

* [Create a segment documentation page](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=en#create-segment)
* [Create a segment video walkthrough](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) -->

## 5단계: 대상 게시 {#publish-destination}

>[!NOTE]
>
>사용자가 사용할 비공개 대상을 만들고 다른 고객이 사용할 수 있도록 대상 카탈로그에 게시하려고 하지 않는 경우 이 단계는 필요하지 않습니다.

대상을 구성하고 테스트한 후 [대상 게시 API](./destination-publish-api.md) 검토를 위해 Adobe에 구성을 제출합니다.

## 6단계: 대상을 문서화합니다. {#document-destination}

>[!NOTE]
>
>사용자가 사용할 비공개 대상을 만들고 다른 고객이 사용할 수 있도록 대상 카탈로그에 게시하려고 하지 않는 경우 이 단계는 필요하지 않습니다.

ISV(Independent Software Vendor) 또는 SI(System Integrator)가 [제품 통합](./overview.md#productized-custom-integrations)를 사용하려면 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md) 에서 대상에 대한 제품 설명서 페이지를 만들려면 [Experience Platform 대상 카탈로그](/help/destinations/catalog/overview.md).
