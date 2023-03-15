---
description: 파일 기반 대상에 대한 서버 및 파일 구성 사양은 /destination-servers 끝점을 통해 Adobe Experience Platform Destination SDK에서 구성할 수 있습니다.
title: 파일 기반 대상 서버 사양에 대한 구성 옵션
exl-id: 56434e36-0458-45d9-961d-f6505de998f7
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 8%

---

# 파일 기반 대상 서버 사양에 대한 서버 및 파일 구성

## 개요 {#overview}

이 페이지에서는 파일 기반 대상 서버에 대한 모든 서버 구성 옵션에 대해 자세히 설명하고 Experience Platform에서 대상으로 파일을 내보내는 사용자를 위한 다양한 파일 구성 옵션을 설정하는 방법을 보여 줍니다.

파일 기반 대상에 대한 서버 및 파일 구성 사양은 다음을 통해 Adobe Experience Platform Destination SDK에서 구성할 수 있습니다 `/destination-servers` 엔드포인트. 읽기 [대상 서버 API 끝점 작업](./destination-server-api.md) 엔드포인트에서 수행할 수 있는 전체 작업 목록입니다.

아래 섹션에는 Destination SDK에서 지원되는 각 배치 대상 유형에 관련된 대상 서버 사양이 포함되어 있습니다.

## 파일 기반 Amazon S3 대상 서버 사양 {#s3-example}

아래 샘플은 Amazon S3 대상에 대한 올바른 대상 서버 구성을 보여 줍니다.

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
       // See the file formatting configuration section further below on this page
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Amazon S3], 다음으로 설정 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedS3Destination.bucket.value` | 문자열 | 의 이름입니다. [!DNL Amazon S3] 이 대상에서 사용할 버킷. |
| `fileBasedS3Destination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedS3Destination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 오브젝트 | 다음을 참조하십시오 [파일 포맷 구성](#file-configuration) 이 섹션에 대한 자세한 설명은 여기를 참조하십시오. |

{style="table-layout:auto"}

## 파일 기반 SFTP 대상 서버 사양 {#sftp-example}

아래 샘플은 SFTP 대상에 대한 올바른 대상 서버 구성을 보여 줍니다.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSftpDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL SFTP] 대상, 다음으로 설정 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedSftpDestination.rootDirectory.value` | 문자열 | 대상 스토리지의 루트 디렉토리입니다. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedSftpDestination.hostName.value` | 문자열 | 대상 스토리지의 호스트 이름입니다. |
| `port` | 정수 | SFTP 파일 서버 포트입니다. |
| `encryptionMode` | 문자열 | 파일 암호화를 사용할지 여부를 나타냅니다. 지원되는 값: <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 오브젝트 | 다음을 참조하십시오 [파일 포맷 구성](#file-configuration) 이 섹션에 대한 자세한 설명은 여기를 참조하십시오. |

{style="table-layout:auto"}

## 파일 기반 [!DNL Azure Data Lake Storage] ([!DNL ADLS]) 대상 서버 사양 {#adls-example}

아래 샘플에서는 [!DNL Azure Data Lake Storage] 대상.

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Azure Data Lake Storage] 대상, 다음으로 설정 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAdlsGen2Destination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 오브젝트 | 다음을 참조하십시오 [파일 포맷 구성](#file-configuration) 이 섹션에 대한 자세한 설명은 여기를 참조하십시오. |

{style="table-layout:auto"}

## 파일 기반 [!DNL Azure Blob Storage] 대상 서버 사양 {#blob-example}

아래 샘플에서는 [!DNL Azure Blob Storage] 대상.

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Azure Blob Storage] 대상, 다음으로 설정 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAzureBlobDestination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedAzureBlobDestination.container.value` | 문자열 | 의 이름입니다. [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다. |
| `fileConfigurations` | 오브젝트 | 다음을 참조하십시오 [파일 포맷 구성](#file-configuration) 이 섹션에 대한 자세한 설명은 여기를 참조하십시오. |

{style="table-layout:auto"}

## 파일 기반 [!DNL Data Landing Zone] ([!DNL DLZ]) 대상 서버 사양 {#dlz-example}

아래 샘플에서는 [!DNL Data Landing Zone] ([!DNL DLZ]) 대상.

```json
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
       // See the file formatting configuration section further below on this page
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Data Landing Zone] 대상, 다음으로 설정 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedDlzDestination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 오브젝트 | 다음을 참조하십시오 [파일 포맷 구성](#file-configuration) 이 섹션에 대한 자세한 설명은 여기를 참조하십시오. |

{style="table-layout:auto"}

## 파일 기반 [!DNL Google Cloud Storage] 대상 서버 사양 {#gcs-example}

아래 샘플에서는 [!DNL Google Cloud Storage] 대상.

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
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
      // See the file formatting configuration section further below on this page
   }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정하십시오. 대상 [!DNL Google Cloud Storage] 대상, 다음으로 설정 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 문자열 | 의 이름입니다. [!DNL Google Cloud Storage] 이 대상에서 사용할 버킷. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 문자열 | 내보낸 파일을 호스팅할 대상 폴더의 경로입니다. |
| `fileConfigurations` | 오브젝트 | 다음을 참조하십시오 [파일 포맷 구성](#file-configuration) 이 섹션에 대한 자세한 설명은 여기를 참조하십시오. |

{style="table-layout:auto"}

## 파일 서식 구성 {#file-configuration}

이 섹션에서는 내보낸 파일의 형식 설정에 대해 설명합니다 `CSV` 파일. Experience Platform에서 받은 파일을 최적으로 읽고 해석하기 위해 내보낸 파일의 여러 속성을 사용자 측의 파일 수신 시스템의 요구 사항과 일치하도록 수정할 수 있습니다.

>[!NOTE]
>
>CSV 옵션은 CSV 파일을 내보낼 때만 지원됩니다. 다음 `fileConfigurations` 섹션은 새 대상 서버를 설정할 때 필수가 아닙니다. CSV 옵션에 대한 API 호출에서 값을 전달하지 않은 경우 [추가 아래 참조 표](#file-formatting-reference-and-example) 이 사용됩니다.

### CSV 옵션을 사용한 파일 구성 및 `templatingStrategy` 을 로 설정 `NONE` {#file-configuration-templating-none}

아래 구성 예에서 모든 CSV 옵션은 수정되었습니다. 각각에 정의된 내보내기 설정 `csvOptions` 매개 변수는 최종적이며 사용자가 수정할 수 없습니다.

```json
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
        },
        "maxFileRowCount":5000000
    }
```

### CSV 옵션을 사용한 파일 구성 및 `templatingStrategy` 을 로 설정 `PEBBLE_V1` {#file-configuration-templating-pebble}

아래 구성 예제에서 CSV 옵션은 수정되지 않습니다. 다음 `value` 의 각 항목 `csvOptions` 매개 변수는 다음을 통해 해당 고객 데이터 필드에 구성됩니다. `/destinations` 끝점(예: `customerData.quote` 대상: `quote` 파일 형식 옵션)과 사용자는 Experience Platform UI를 사용하여 해당 고객 데이터 필드에서 구성하는 다양한 옵션 중에서 선택할 수 있습니다.

```json
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
```

### 지원되는 파일 형식 옵션에 대한 전체 참조 및 예제 {#file-formatting-reference-and-example}

>[!TIP]
>
>아래에 설명된 CSV 파일 형식 지정 옵션도 [CSV 파일용 Apache Spark 안내서](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 아래에 사용된 설명은 Apache Spark 안내서에서 가져온 것입니다.

다음은 각 옵션의 출력 예와 함께 Destination SDK에서 사용 가능한 모든 파일 형식 옵션에 대한 전체 참조입니다.

| 필드 | 필수/선택적 | 설명 | 기본값 | 출력 예 1 | 출력 예 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 필수 여부 | 구성하는 각 파일 서식 옵션에 대해 매개 변수를 추가해야 합니다 `templatingStrategy`, 다음 두 가지 값을 가질 수 있습니다. <br><ul><li>`NONE`: 사용자가 구성에 대해 서로 다른 값 중에서 선택할 수 있도록 허용하지 않으려는 경우 이 값을 사용합니다. 다음을 참조하십시오 [이 구성](#file-configuration-templating-none) 파일 형식 지정 옵션이 고정된 예제.</li><li>`PEBBLE_V1`: 사용자가 구성에 대해 서로 다른 값 중에서 선택할 수 있도록 하려면 이 값을 사용합니다. 이 경우 에도 해당 고객 데이터 필드를 설정해야 합니다. `/destination` 엔드포인트 구성 : UI에서 사용자에게 다양한 옵션을 표시합니다. 다음을 참조하십시오 [이 구성](#file-configuration-templating-pebble) 예를 들어 사용자가 파일 서식 옵션에 대해 서로 다른 값 중에서 선택할 수 있습니다.</li></ul> | - | - | - |
| `compression.value` | 선택 사항입니다 | 파일에 데이터를 저장할 때 사용할 압축 코덱입니다. 지원되는 값: `none`, `bzip2`, `gzip`, `lz4`, 및 `snappy`. | `none` | - | - |
| `fileType.value` | 선택 사항입니다 | 출력 파일 형식을 지정합니다. 지원되는 값: `csv`, `parquet`, 및 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 구분 기호가 값의 일부일 수 있는 따옴표 붙은 값을 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `null` | - | - |
| `csvOptions.quoteAll.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 모든 값을 항상 따옴표로 묶어야 하는지 여부를 나타냅니다. 기본적으로 따옴표 문자가 포함된 값만 이스케이프합니다. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 각 필드 및 값에 대한 구분 기호를 설정합니다. 이 구분 기호는 하나 이상의 문자일 수 있습니다. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 이미 인용한 값 내에서 따옴표를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 따옴표를 포함하는 값을 항상 따옴표로 묶어야 하는지 여부를 나타냅니다. 기본적으로 따옴표 문자가 포함된 모든 값은 이스케이프 처리됩니다. | `true` | - | - |
| `csvOptions.header.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 내보낸 파일의 첫 번째 행으로 열 이름을 작성할지 여부를 나타냅니다. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 값에서 선행 공백을 트리밍할지 여부를 나타냅니다. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 값에서 후행 공백을 트리밍할지 여부를 나타냅니다. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. Null 값의 문자열 표현을 설정합니다. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 날짜 형식을 나타냅니다. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 타임스탬프 형식을 나타내는 문자열을 설정합니다. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 따옴표 문자의 이스케이프를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `\` 이스케이프 문자와 따옴표 문자가 다른 경우. `\0` 이스케이프와 따옴표 문자가 동일한 경우. | - | - |
| `csvOptions.emptyValue.value` | 선택 사항입니다 | *다음에 대해서만`"fileType.value": "csv"`*. 빈 값의 문자열 표현을 설정합니다. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}