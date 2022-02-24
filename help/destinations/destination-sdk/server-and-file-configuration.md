---
description: 파일 기반 대상의 서버 및 파일 구성 사양은 /destination-servers 엔드포인트를 통해 Adobe Experience Platform Destination SDK에서 구성할 수 있습니다.
title: (베타) 파일 기반 대상 서버 사양을 위한 구성 옵션
source-git-commit: bc357e2e93b80edb5f7825bf2dee692f14bd7297
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 10%

---

# (베타) 파일 기반 대상 서버 사양을 위한 서버 및 파일 구성

## 개요 {#overview}

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK을 사용하여 파일 기반 대상을 구성하고 제출하는 기능은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

이 페이지에서는 파일 기반 대상 서버에 대한 모든 서버 구성 옵션에 대해 자세히 설명하고 Experience Platform에서 대상으로 파일을 내보내는 사용자에 대한 다양한 파일 구성 옵션을 설정하는 방법을 설명합니다.

파일 기반 대상의 서버 및 파일 구성 사양은 를 통해 Adobe Experience Platform Destination SDK에서 구성할 수 있습니다 `/destination-servers` 엔드포인트. 읽기 [대상 서버 API 끝점 작업](./destination-server-api.md) 전체 작업 목록을 보려면 종단점에서 수행할 수 있습니다.

## 파일 기반 Amazon S3 대상 서버 사양 {#s3-example}

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
       // see File-based destinations file configuration
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Amazon S3]으로 설정합니다. `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | 문자열 | 의 이름 [!DNL Amazon S3] 이 대상에서 사용할 버킷입니다. |
| `fileBasedS3Destination.path.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |

## 파일 기반 SFTP 대상 서버 사양 {#sftp-example}

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
       // see File-based destinations file configuration
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL SFTP] 대상, 다음 위치로 설정 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | 문자열 | 대상 저장소의 루트 디렉토리입니다. |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | 문자열 | 대상 스토리지의 호스트 이름입니다. |
| `port` | 정수 | SFTP 파일 서버 포트입니다. |
| `encryptionMode` | 문자열 | 파일 암호화를 사용할지 여부를 나타냅니다. 지원되는 값: <ul><li>PGP</li><li>None</li></ul> |

## 파일 기반 [!DNL Azure Data Lake Storage] ([!DNL ADLS]) 대상 서버 사양 {#adls-example}

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
       // see File-based destinations file configuration
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Azure Data Lake Storage] 대상, 다음 위치로 설정 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |

## 파일 기반 [!DNL Azure Blob Storage] 대상 서버 사양 {#blob-example}

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
       // see File-based destinations file configuration
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Azure Blob Storage] 대상, 다음 위치로 설정 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 문자열 | *필수 여부.*  `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | 문자열 | 의 이름 [!DNL Azure Blob Storage] 이 대상에서 사용할 컨테이너입니다. |

## 파일 기반 [!DNL Data Landing Zone] ([!DNL DLZ]) 대상 서버 사양 {#dlz-example}

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
       // see File-based destinations file configuration
    }
}
```

| 매개 변수 | 유형 | 설명 |
|---|---|---|
| `name` | 문자열 | 대상 연결의 이름입니다. |
| `destinationServerType` | 문자열 | 대상 플랫폼에 따라 이 값을 설정합니다. 대상 [!DNL Data Landing Zone] 대상, 다음 위치로 설정 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 문자열 | *필수 여부.*   `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 문자열 | 내보낸 파일을 호스트할 대상 폴더의 경로입니다. |

## 파일 기반 대상 파일 구성 {#file-configuration}

이 섹션에서는 내보낸 파일의 파일 형식 설정을 설명합니다 `CSV` 파일. Experience Platform에서 받은 파일을 최적의 방식으로 읽고 해석할 수 있도록 내보낸 파일의 여러 속성을 사용자 측에서 파일 수신 시스템의 요구 사항에 맞게 수정할 수 있습니다.

>[!NOTE]
>
>CSV 옵션은 CSV 파일을 내보낼 때만 지원됩니다. 다음 `fileConfigurations` 새 대상 서버를 설정할 때는 섹션이 필수가 아닙니다. CSV 옵션에 대한 API 호출에서 값을 전달하지 않으면 아래 표의 기본 값이 사용됩니다.

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
            },
            "lineSep": {
                "templatingStrategy": "NONE",
                "value": "\n"
            }
        }
    }
```

| 필드 | 필수/선택적 | 설명 | 기본값 |
|---|---|---|---|
| `compression.value` | 선택 사항입니다 | 데이터를 파일에 저장할 때 사용할 압축 코덱입니다. 지원되는 값: `none`, `bzip2`, `gzip`, `lz4`, 및 `snappy`. | `none` |
| `fileType.value` | 선택 사항입니다 | 출력 파일 형식을 지정합니다. 지원되는 값: `csv`, `parquet`, 및 `json`. | `csv` |
| `csvOptions.quote.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 구분 기호가 값의 일부가 될 수 있는 따옴표 붙은 값을 이스케이프하는 데 사용되는 단일 문자를 설정합니다. | `null` |
| `csvOptions.quoteAll.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 모든 값을 항상 따옴표로 묶어야 하는지를 나타냅니다. 기본값은 따옴표 문자가 포함된 값만 이스케이프 처리하는 것입니다. | `false` |
| `csvOptions.escape.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 이미 따옴표로 묶인 값 내에 따옴표를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `\` |
| `csvOptions.escapeQuotes.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 따옴표를 포함하는 값을 항상 따옴표로 묶어야 하는지를 나타냅니다. 기본값은 따옴표 문자가 포함된 모든 값을 이스케이프 처리하는 것입니다. | `true` |
| `csvOptions.header.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 열 이름을 첫 번째 행으로 쓸지 여부를 나타냅니다. | `true` |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 값에서 선행 공백을 트리밍할지 여부를 나타냅니다. | `true` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 값에서 후행 공백을 트리밍할지 여부를 나타냅니다. | `true` |
| `csvOptions.nullValue.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. null 값의 문자열 표현을 설정합니다. | `""` |
| `csvOptions.dateFormat.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 날짜 형식을 나타냅니다. | `yyyy-MM-dd` |
| `csvOptions.timestampFormat.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 타임스탬프 형식을 나타내는 문자열을 설정합니다. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` |
| `csvOptions.charToEscapeQuoteEscaping.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 따옴표 문자의 이스케이프를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `\` 이스케이프 및 따옴표 문자가 다른 경우. `\0` 이스케이프 문자와 따옴표 문자가 같은 경우. |
| `csvOptions.emptyValue.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 빈 값의 문자열 표현을 설정합니다. | `""` |
| `csvOptions.lineSep.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 작성에 사용해야 하는 라인 구분자를 정의합니다. 최대 길이는 1자입니다. | `\n` |
