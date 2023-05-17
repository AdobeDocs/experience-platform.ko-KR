---
description: '''/destination-server'' 종단점을 통해 Adobe Experience Platform Destination SDK으로 빌드된 파일 기반 대상에 대한 파일 형식 옵션을 구성하는 방법을 알아봅니다.'
title: 파일 형식 구성
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 4%

---


# 파일 형식 구성

Destination SDK은 통합 요구 사항에 따라 구성할 수 있는 유연한 기능 세트를 지원합니다. 이러한 기능 중에는 [!DNL CSV] 파일 형식 지정

Destination SDK을 통해 파일 기반 대상을 만들 때 내보낸 CSV 파일의 형식을 지정하는 방법을 정의할 수 있습니다. 다음과 같은 여러 서식 옵션을 사용자 지정할 수 있지만 다음과 같은 옵션을 사용자 지정할 수 있습니다.

* CSV 파일에 헤더를 포함해야 하는지 여부
* 값을 인용하는 데 사용할 문자
* 빈 값의 모습은 다음과 같습니다.

대상 구성에 따라 파일 기반 대상에 연결할 때 UI에 특정 옵션이 표시됩니다. 이러한 옵션이 [파일 기반 대상에 대한 파일 형식 옵션](../../../ui/batch-destinations-file-formatting-options.md) 설명서.


파일 형식 설정은 파일 기반 대상에 대한 대상 서버 구성의 일부입니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서를 참조하십시오. [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

를 통해 파일 서식 옵션을 구성할 수 있습니다 `/authoring/destination-servers` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 서버 구성 만들기](../../authoring-api/destination-server/create-destination-server.md)
* [대상 서버 구성 업데이트](../../authoring-api/destination-server/update-destination-server.md)

이 페이지에서는 내보낸 파일에 대해 지원되는 모든 형식 설정을 설명합니다 `CSV` 파일.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 아니요 |
| 파일 기반(일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

Experience Platform에서 받은 파일을 최적의 방식으로 읽고 해석하기 위해 내보낸 파일의 여러 속성을 대상 파일 수신 시스템의 요구 사항에 맞게 수정할 수 있습니다.

>[!NOTE]
>
>CSV 옵션은 CSV 파일을 내보낼 때만 지원됩니다. 다음 `fileConfigurations` 새 대상 서버를 설정할 때는 섹션이 필수가 아닙니다. CSV 옵션에 대한 API 호출에서 값을 전달하지 않는 경우, 기본 값은 [아래의 참조 표](#file-formatting-reference-and-example) 이 사용됩니다.


## 사용자가 구성 옵션을 선택할 수 없는 CSV 옵션 {#file-configuration-templating-none}

아래 구성 예제에서 모든 CSV 옵션은 사전 정의됩니다. 각 `csvOptions` 매개 변수는 최종적이며 사용자가 수정할 수 없습니다.

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

## 사용자가 구성 옵션을 선택할 수 있는 CSV 옵션 {#file-configuration-templating-pebble}

아래 구성 예제에서 CSV 옵션 중 어느 것도 사전 정의되어 있지 않습니다. 다음 `value` 각 `csvOptions` 매개 변수는 `/destinations` 엔드포인트(예 [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) 대상 `quote` 파일 형식 지정 옵션)과 사용자는 Experience Platform UI를 사용하여 해당 고객 데이터 필드에서 구성하는 다양한 옵션 중에서 선택할 수 있습니다. 이러한 옵션이 [파일 기반 대상에 대한 파일 형식 옵션](../../../ui/batch-destinations-file-formatting-options.md) 설명서.

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
      }
   }
}
```

## 지원되는 파일 형식 옵션에 대한 전체 참조 및 예제 {#file-formatting-reference-and-example}

>[!TIP]
>
>아래 설명된 CSV 파일 형식 옵션도 [CSV 파일에 대한 Apache Spark 안내서](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). 아래 사용된 설명은 Apache Spark 안내서에서 확인할 수 있습니다.

다음은 Destination SDK에서 사용 가능한 모든 파일 형식 옵션에 대한 전체 참조이며 각 옵션에 대한 출력 예입니다.

| 필드 | 필수/선택적 | 설명 | 기본값 | 예제 출력 1 | 예제 출력 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | 필수 여부 | 구성하는 각 파일 형식 옵션에 대해 매개 변수를 추가해야 합니다 `templatingStrategy`에는 두 값이 있을 수 있습니다. <br><ul><li>`NONE`: 사용자가 구성에 대해 다른 값 중에서 선택할 수 있도록 하지 않을 경우 이 값을 사용하십시오. 자세한 내용은 [이 구성](#file-configuration-templating-none) 예를 들어 파일 서식 옵션이 수정되었습니다.</li><li>`PEBBLE_V1`: 사용자가 구성에 대해 다른 값 중에서 선택할 수 있도록 하려면 이 값을 사용하십시오. 이 경우, `/destination` UI에서 사용자에게 다양한 옵션을 표시하는 엔드포인트 구성. 자세한 내용은 [이 구성](#file-configuration-templating-pebble) 예를 들어, 사용자가 파일 서식 옵션을 위해 다른 값 중에서 선택할 수 있습니다.</li></ul> | - | - | - |
| `compression.value` | 선택 사항입니다 | 데이터를 파일에 저장할 때 사용할 압축 코덱입니다. 지원되는 값: `none`, `bzip2`, `gzip`, `lz4`, 및 `snappy`. | `none` | - | - |
| `fileType.value` | 선택 사항입니다 | 출력 파일 형식을 지정합니다. 지원되는 값: `csv`, `parquet`, 및 `json`. | `csv` | - | - |
| `csvOptions.quote.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 구분 기호가 값의 일부가 될 수 있는 따옴표 붙은 값을 이스케이프하는 데 사용되는 단일 문자를 설정합니다. | `null` | - | - |
| `csvOptions.quoteAll.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 모든 값을 항상 따옴표로 묶어야 하는지를 나타냅니다. 기본값은 따옴표 문자가 포함된 값만 이스케이프 처리하는 것입니다. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 각 필드 및 값에 대해 구분자를 설정합니다. 이 구분자는 하나 이상의 문자일 수 있습니다. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 이미 인용된 값 내에서 인용 부호를 이스케이프하는 데 사용되는 단일 문자를 설정합니다. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 따옴표를 포함하는 값을 항상 따옴표로 묶어야 하는지를 나타냅니다. 기본값은 따옴표 문자가 포함된 모든 값을 이스케이프 처리하는 것입니다. | `true` | - | - |
| `csvOptions.header.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 내보낸 파일의 첫 번째 행으로 열 이름을 쓸 것인지 여부를 나타냅니다. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 값에서 선행 공백을 트리밍할지 여부를 나타냅니다. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 값에서 후행 공백을 트리밍할지 여부를 나타냅니다. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. null 값의 문자열 표현을 설정합니다. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 날짜 형식을 나타냅니다. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 타임스탬프 형식을 나타내는 문자열을 설정합니다. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 따옴표 문자의 이스케이프를 이스케이프 처리하는 데 사용되는 단일 문자를 설정합니다. | `\` 이스케이프 및 따옴표 문자가 다른 경우. `\0` 이스케이프 문자와 따옴표 문자가 같은 경우. | - | - |
| `csvOptions.emptyValue.value` | 선택 사항입니다 | *전용`"fileType.value": "csv"`*. 빈 값의 문자열 표현을 설정합니다. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상 서버 구성에서 파일 형식이 작동하는 방식과 파일 구성 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 서버 구성 요소에 대해 자세히 알아보려면 다음 문서를 참조하십시오.

* [Destination SDK으로 생성된 대상에 대한 서버 사양](server-specs.md)
* [템플릿 사양](templating-specs.md)
* [메시지 포맷](message-format.md)