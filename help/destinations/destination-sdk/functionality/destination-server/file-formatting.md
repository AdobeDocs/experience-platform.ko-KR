---
description: '`/destination-servers'' 끝점을 통해 Adobe Experience Platform Destination SDK으로 빌드된 파일 기반 대상의 파일 형식 옵션을 구성하는 방법을 알아봅니다.'
title: 파일 서식 구성
exl-id: 98fec559-9073-4517-a10e-34c2caf292d5
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 2%

---

# 파일 서식 구성

Destination SDK은 통합 요구 사항에 따라 구성할 수 있는 유연한 기능 세트를 지원합니다. 이러한 기능 중 [!DNL CSV] 파일 형식을 지원합니다.

Destination SDK을 통해 파일 기반 대상을 만들 때 내보낸 CSV 파일의 형식을 지정하는 방법을 정의할 수 있습니다. 다음과 같은 다양한 서식 옵션을 사용자 지정할 수 있습니다.

* CSV 파일에 헤더를 포함할지 여부
* 값 따옴표에 사용할 문자
* 빈 값은 어떤 모습이어야 합니까?

대상 구성에 따라 사용자는 파일 기반 대상에 연결할 때 UI에 특정 옵션이 표시됩니다. [파일 기반 대상에 대한 파일 서식 옵션](../../../ui/batch-destinations-file-formatting-options.md) 설명서에서 이러한 옵션이 어떻게 표시되는지 확인할 수 있습니다.


파일 형식 설정은 파일 기반 대상에 대한 대상 서버 구성의 일부입니다.

이 구성 요소가 Destination SDK으로 만든 통합에 어떻게 적합한지 이해하려면 [구성 옵션](../configuration-options.md) 설명서에서 다이어그램을 참조하거나 [Destination SDK을 사용하여 파일 기반 대상을 구성하는 방법](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)에 대한 안내서를 참조하십시오.

`/authoring/destination-servers` 끝점을 통해 파일 서식 옵션을 구성할 수 있습니다. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 서버 구성 만들기](../../authoring-api/destination-server/create-destination-server.md)
* [대상 서버 구성 업데이트](../../authoring-api/destination-server/update-destination-server.md)

이 페이지에서는 내보낸 `CSV`개 파일에 대해 지원되는 모든 파일 형식 설정을 설명합니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 아니요 |
| 파일 기반 (일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

Experience Platform에서 받은 파일을 최적으로 읽고 해석하기 위해 내보낸 파일의 여러 속성을 대상 파일 수신 시스템의 요구 사항과 일치하도록 수정할 수 있습니다.

>[!NOTE]
>
>CSV 옵션은 CSV 파일을 내보낼 때만 지원됩니다. 새 대상 서버를 설정할 때 `fileConfigurations` 섹션이 필수가 아닙니다. CSV 옵션에 대한 API 호출에 값을 전달하지 않으면 [아래 ](#file-formatting-reference-and-example)의 참조 표에 있는 기본 값이 사용됩니다.


## 사용자가 구성 옵션을 선택할 수 없는 CSV 옵션 {#file-configuration-templating-none}

아래 구성 예제에서 모든 CSV 옵션은 사전 정의되어 있습니다. 각 `csvOptions` 매개 변수에 정의된 내보내기 설정은 최종적이며 사용자가 수정할 수 없습니다.

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
        "maxFileRowCount":5000000,
        "includeFileManifest": {
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{ customerData.includeFileManifest }}"
      }
    }
```

## 사용자가 구성 옵션을 선택할 수 있는 CSV 옵션 {#file-configuration-templating-pebble}

아래 구성 예에서는 사전 정의된 CSV 옵션이 없습니다. 각 `csvOptions` 매개 변수의 `value`은(는) `/destinations` 엔드포인트(예: `quote` 파일 형식 옵션의 경우 [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options))를 통해 해당 고객 데이터 필드에 구성되어 있으며 사용자는 Experience Platform UI를 사용하여 해당 고객 데이터 필드에서 사용자가 구성하는 다양한 옵션 중에서 선택할 수 있습니다. [파일 기반 대상에 대한 파일 서식 옵션](../../../ui/batch-destinations-file-formatting-options.md) 설명서에서 이러한 옵션이 어떻게 표시되는지 확인할 수 있습니다.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      },
      "maxFileRowCount":5000000,
      "includeFileManifest": {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{ customerData.includeFileManifest }}"
      }
   }
}
```

## 지원되는 파일 형식 옵션에 대한 전체 참조 및 예제 {#file-formatting-reference-and-example}

>[!TIP]
>
>아래 설명된 CSV 파일 형식 지정 옵션은 [CSV 파일에 대한 Apache Spark 안내서](https://spark.apache.org/docs/latest/sql-data-sources-csv.html)에도 설명되어 있습니다. 아래에 사용된 설명은 Apache Spark 안내서에서 가져온 것입니다.

다음은 각 옵션의 출력 예와 함께 Destination SDK에서 사용 가능한 모든 파일 형식 옵션에 대한 전체 참조입니다.

| 필드 | 필수/선택 사항 | 설명 | 기본 값 | 출력 예 1 | 출력 예 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 필수 여부 | 구성하는 각 파일 서식 옵션에 대해 `templatingStrategy` 매개 변수를 추가해야 합니다. 이 매개 변수에는 <br> 값이 있을 수 있습니다.<ul><li>`NONE`: 사용자가 구성에 대해 다른 값 중에서 선택할 수 있도록 허용하지 않으려는 경우 이 값을 사용하십시오. 파일 서식 지정 옵션이 수정되는 예제는 [이 구성](#file-configuration-templating-none)을 참조하십시오.</li><li>`PEBBLE_V1`: 사용자가 구성에 대해 다른 값 중에서 선택할 수 있도록 하려면 이 값을 사용하십시오. 이 경우 UI에서 사용자에게 다양한 옵션을 표시하려면 `/destination` 끝점 구성에서 해당 고객 데이터 필드도 설정해야 합니다. 사용자가 파일 서식 옵션에 대해 다양한 값 중에서 선택할 수 있는 예제는 [이 구성](#file-configuration-templating-pebble)을 참조하십시오.</li></ul> | - | - | - |
| `compression.value` | 선택 사항입니다 | 파일에 데이터를 저장할 때 사용할 압축 코덱입니다. 지원되는 값: `none`, `bzip2`, `gzip`, `lz4` 및 `snappy`. | `none` | - | - |
| `fileType.value` | 선택 사항입니다 | 출력 파일 형식을 지정합니다. 지원되는 값: `csv`, `parquet` 및 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 구분 기호가 값의 일부일 수 있는 따옴표 붙은 값을 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `null` | 기본값 예: `quote.value: "u0000"` —> `male,NULJohn,LastNameNUL` | 사용자 지정 예: `quote.value: "\""` —> `male,"John,LastName"` |
| `csvOptions.quoteAll.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 모든 값을 항상 따옴표로 묶어야 하는지 여부를 나타냅니다. 기본적으로 따옴표 문자가 포함된 값만 이스케이프합니다. | `false` | `quoteAll`:`false` —> `male,John,"TestLastName"` | `quoteAll`:`true` —>`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 각 필드 및 값에 대한 구분 기호를 설정합니다. 이 구분 기호는 하나 이상의 문자일 수 있습니다. | `,` | `delimiter`:`,` —> `comma-separated values"` | `delimiter`:`\t` —> `tab-separated values` |
| `csvOptions.escape.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 이미 인용한 값 내에서 따옴표를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `\` | `"escape"`:`"\\"` —> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` —> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 따옴표를 포함하는 값을 항상 따옴표로 묶어야 하는지 여부를 나타냅니다. 기본적으로 따옴표 문자가 포함된 모든 값은 이스케이프 처리됩니다. | `true` | - | - |
| `csvOptions.header.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 내보낸 파일의 첫 번째 행으로 열 이름을 작성할지 여부를 나타냅니다. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 값에서 선행 공백을 트리밍할지 여부를 나타냅니다. | `true` | `ignoreLeadingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`—> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 값에서 후행 공백을 트리밍할지 여부를 나타냅니다. | `true` | `ignoreTrailingWhiteSpace`:`true` —> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`—> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. Null 값의 문자열 표현을 설정합니다. | `""` | `nullvalue`:`""` —> `male,"",TestLastName` | `nullvalue`:`"NULL"` —> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 날짜 형식을 나타냅니다. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` —> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` —> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 타임스탬프 형식을 나타내는 문자열을 설정합니다. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 따옴표 문자의 이스케이프를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | 이스케이프 문자와 따옴표 문자가 다른 경우 `\`. 이스케이프 문자와 따옴표가 같은 경우 `\0`. | - | - |
| `csvOptions.emptyValue.value` | 선택 사항입니다 | `"fileType.value": "csv"`*에 대해서만*&#x200B;합니다. 빈 값의 문자열 표현을 설정합니다. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | 선택 사항입니다 | 내보낸 파일당 1,000,000행과 10,000,000행 사이의 최대 행 수를 나타냅니다. | 5,000,000 |
| `includeFileManifest` | 선택 사항입니다 | 파일 내보내기와 함께 파일 매니페스트 내보내기에 대한 지원을 활성화합니다. 매니페스트 JSON 파일에는 내보내기 위치, 내보내기 크기 등에 대한 정보가 포함되어 있습니다. 매니페스트의 이름은 `manifest-<<destinationId>>-<<dataflowRunId>>.json` 형식을 사용하여 지정합니다. | [샘플 매니페스트 파일](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json)을(를) 봅니다. 매니페스트 파일에는 다음 필드가 포함되어 있습니다. <ul><li>`flowRunId`: 내보낸 파일을 생성한 [데이터 흐름 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).</li><li>`scheduledTime`: 파일을 내보낸 시간(UTC)입니다. </li><li>`exportResults.sinkPath`: 내보낸 파일이 저장된 저장소 위치의 경로입니다. </li><li>`exportResults.name`: 내보낸 파일의 이름입니다.</li><li>`size`: 내보낸 파일의 크기(바이트)입니다.</li></ul> |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상 서버 구성에서 파일 형식이 작동하는 방식과 파일 형식을 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 서버 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [Destination SDK으로 생성된 대상의 서버 사양](server-specs.md)
* [사양 템플릿](templating-specs.md)
* [메시지 포맷](message-format.md)
