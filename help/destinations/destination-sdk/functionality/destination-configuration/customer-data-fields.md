---
description: 사용자가 데이터를 대상에 연결 및 내보내는 방법과 관련된 다양한 정보를 지정할 수 있도록 해주는 Experience Platform UI에서 입력 필드를 만드는 방법을 알아봅니다.
title: 고객 데이터 필드
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 2%

---


# 고객 데이터 필드를 통해 사용자 입력 구성

Experience Platform UI에서 대상에 연결할 때 사용자가 특정 구성 세부 사항을 제공하거나 사용자가 사용할 수 있도록 하는 특정 옵션을 선택해야 할 수 있습니다. Destination SDK에서 이러한 옵션을 고객 데이터 필드라고 합니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서나 다음 대상 구성 개요 페이지를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## 고객 데이터 필드에 대한 사용 사례 {#use-cases}

사용자가 Experience Platform UI에 데이터를 입력해야 하는 다양한 사용 사례에 고객 데이터 필드를 사용하십시오. 예를 들어, 사용자가 다음을 제공해야 할 때 고객 데이터 필드를 사용합니다.

* 파일 기반 대상의 클라우드 스토리지 버킷 이름 및 경로.
* 고객 데이터 필드에서 허용하는 형식입니다.
* 사용자가 선택할 수 있는 파일 압축 종류입니다.
* 실시간(스트리밍) 통합을 위해 사용할 수 있는 엔드포인트 목록.

를 통해 고객 데이터 필드를 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 고객 데이터 필드 구성 유형에 대해 설명하고 Experience Platform UI에서 고객이 보게 될 내용을 보여줍니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

고유한 고객 데이터 필드를 만들 때 아래 표에 설명된 매개 변수를 사용하여 해당 동작을 구성할 수 있습니다.

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---------|----------|------|---|
| `name` | 문자열 | 필수 여부 | 도입하는 사용자 정의 필드의 이름을 입력합니다. 이 이름은 `title` 필드가 비어 있거나 없습니다. |
| `type` | 문자열 | 필수 여부 | 도입하는 사용자 지정 필드의 유형을 나타냅니다. 허용되는 값: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | 문자열 | 선택 사항입니다 | 플랫폼 UI에서 고객이 볼 수 있는 필드의 이름을 나타냅니다. 이 필드가 비어 있거나 누락된 경우 UI는 `name` 값. |
| `description` | 문자열 | 선택 사항입니다 | 사용자 지정 필드에 대한 설명을 입력합니다. 이 설명은 플랫폼 UI에 표시되지 않습니다. |
| `isRequired` | 부울 | 선택 사항입니다 | 사용자가 대상 구성 워크플로우에서 이 필드에 값을 제공해야 하는지 여부를 나타냅니다. |
| `pattern` | 문자열 | 선택 사항입니다 | 필요한 경우 사용자 지정 필드에 패턴을 적용합니다. 패턴을 적용하려면 정규 표현식을 사용합니다. 예를 들어 고객 ID에 숫자나 밑줄이 포함되지 않은 경우 을 입력합니다 `^[A-Za-z]+$` 을 입력합니다. |
| `enum` | 문자열 | 선택 사항입니다 | 사용자 지정 필드를 드롭다운 메뉴로 렌더링하고 사용자가 사용할 수 있는 옵션을 나열합니다. |
| `default` | 문자열 | 선택 사항입니다 | 다음에서 기본값을 정의합니다 `enum` 목록. |
| `hidden` | 부울 | 선택 사항입니다 | 고객 데이터 필드가 UI에 표시되는지 여부를 나타냅니다. |
| `unique` | 부울 | 선택 사항입니다 | 사용자 조직에서 설정한 모든 대상 데이터 흐름에서 값이 고유해야 하는 고객 데이터 필드를 만들어야 하는 경우 이 매개 변수를 사용하십시오. 예: **[!UICONTROL 통합 별칭]** 의 필드 [사용자 지정 개인화](../../../catalog/personalization/custom-personalization.md) 대상은 고유해야 합니다. 즉, 이 대상에 대해 두 개의 개별 데이터 흐름이 이 필드에 대해 동일한 값을 가질 수 없습니다. |
| `readOnly` | 부울 | 선택 사항입니다 | 고객이 필드의 값을 변경할 수 있는지 여부를 나타냅니다. |

{style="table-layout:auto"}

아래 예에서는 `customerDataFields` 섹션에는 대상에 연결할 때 플랫폼 UI에 사용자가 입력해야 하는 두 개의 필드가 정의되어 있습니다.

* `Account ID`: 대상 플랫폼에 대한 사용자 계정 ID입니다.
* `Endpoint region`: 연결할 API의 지역 끝점입니다. 다음 `enum` 섹션에서 사용자가 선택할 수 있는 내에 정의된 값이 있는 드롭다운 메뉴를 만듭니다.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

결과 UI 경험이 아래 이미지에 표시됩니다.

![고객 데이터 필드의 예를 보여주는 Ui 이미지입니다.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## 대상 연결 이름 및 설명 {#names-description}

새 대상을 만들 때 Destination SDK이 자동으로 추가됩니다 **[!UICONTROL 이름]** 및 **[!UICONTROL 설명]** 플랫폼 UI의 대상 연결 화면에 필드를 추가합니다. 위의 예에서 볼 수 있듯이 **[!UICONTROL 이름]** 및 **[!UICONTROL 설명]** 필드는 고객 데이터 필드 구성에 포함되지 않고 UI에서 렌더링됩니다.

>[!IMPORTANT]
>
>추가할 경우 **[!UICONTROL 이름]** 및 **[!UICONTROL 설명]** 고객 데이터 필드 구성의 경우 사용자는 UI에서 중복되는 필드를 보게 됩니다.

## 고객 데이터 필드 순서 지정 {#ordering}

대상 구성에서 고객 데이터 필드를 추가하는 순서는 Platform UI에 반영됩니다.

예를 들어, 아래 구성은 UI에 그에 따라 반영되며, 선택 사항은 순서대로 표시됩니다 **[!UICONTROL 이름]**, **[!UICONTROL 설명]**, **[!UICONTROL 버킷 이름]**, **[!UICONTROL 폴더 경로]**, **[!UICONTROL 파일 유형]**, **[!UICONTROL 압축 포맷]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
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
}
]
```

![Experience Platform UI의 파일 형식 옵션 순서를 보여주는 이미지입니다.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## 고객 데이터 필드 그룹화 {#grouping}

하나의 섹션 내에 여러 고객 데이터 필드를 그룹화할 수 있습니다. UI에서 대상에 대한 연결을 설정할 때 사용자는 유사한 필드를 시각적으로 그룹화하여 이점을 얻을 수 있습니다.

이렇게 하려면 `"type": "object"` 그룹을 만들고 `properties` 아래 이미지에 표시된 대로, 그룹화가 있는 개체 **[!UICONTROL CSV 옵션]** 이 강조 표시됩니다.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![UI에서 고객 데이터 필드 그룹을 보여주는 이미지입니다.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## 고객 데이터 필드에 대한 드롭다운 선택기 만들기 {#dropdown-selectors}

사용자가 여러 옵션 중에서 선택할 수 있도록 허용하려는 경우(예: CSV 파일의 필드를 구분하기 위해 사용해야 하는 문자), UI에 드롭다운 필드를 추가할 수 있습니다.

이렇게 하려면 `namedEnum` 아래에 표시된 대로 개체를 구성하고 `default` 사용자가 선택할 수 있는 옵션에 대한 값입니다.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![위에 표시된 구성으로 생성된 드롭다운 선택기의 예를 보여주는 화면 기록.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## 조건부 고객 데이터 필드 만들기 {#conditional-options}

조건부 고객 데이터 필드를 만들 수 있으며, 이 필드는 사용자가 특정 옵션을 선택할 때만 활성화 워크플로우에 표시됩니다.

예를 들어, 사용자가 특정 파일 내보내기 유형을 선택한 경우에만 표시할 조건부 파일 형식 옵션을 만들 수 있습니다.

아래 구성은 CSV 파일 형식 옵션을 위한 조건부 그룹을 만듭니다. CSV 파일 옵션은 사용자가 내보낼 파일 유형으로 CSV를 선택하는 경우에만 표시됩니다.

필드를 조건부 필드로 설정하려면 `conditional` 매개 변수 를 참조하십시오.

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

더 넓은 컨텍스트에서 다음을 볼 수 있습니다 `conditional` 아래의 대상 구성에서 사용되고 있는 필드, `fileType` 문자열 및 `csvOptions` 정의된 객체입니다.

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

아래에서는 위의 구성에 따라 결과 UI 화면을 볼 수 있습니다. 사용자가 파일 유형 CSV를 선택하면 CSV 파일 유형을 참조하는 추가 파일 형식 옵션이 UI에 표시됩니다.

![CSV 파일에 대한 조건부 파일 형식 옵션을 보여주는 화면 기록.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## 템플릿화된 고객 데이터 필드 액세스 {#accessing-templatized-fields}

대상에 사용자 입력이 필요한 경우, 사용자에게 플랫폼 UI를 통해 입력할 수 있는 다양한 고객 데이터 필드를 제공해야 합니다. 그런 다음 고객 데이터 필드에서 사용자 입력을 올바르게 읽도록 대상 서버를 구성해야 합니다. 이것은 템플화된 필드를 통해 행해진다.

템플릿 필드는 형식을 사용합니다 `{{customerData.fieldName}}`, 위치 `fieldName` 는 정보를 읽는 고객 데이터 필드의 이름입니다. 템플릿화된 모든 고객 데이터 필드 앞에는 다음 항목이 있습니다 `customerData.` 중괄호 안에 묶어서 `{{ }}`.

예를 들어 다음 Amazon S3 대상 구성을 고려해 보겠습니다.

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

이 구성에서는 사용자에게 을 입력하라는 메시지가 표시됩니다 [!DNL Amazon S3] 버킷 이름 및 해당 고객 데이터 필드에 대한 폴더 경로.

Experience Platform이 올바르게 연결하려면 [!DNL Amazon S3], 대상 서버는 아래와 같이 이 두 고객 데이터 필드의 값을 읽도록 구성해야 합니다.

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

템플화된 가치들 `{{customerData.bucketName}}` 및 `{{customerData.path}}` Experience Platform이 대상 플랫폼에 성공적으로 연결할 수 있도록 사용자가 제공한 값을 읽습니다.

템플릿 필드를 읽도록 대상 서버를 구성하는 방법에 대한 자세한 내용은 [하드코딩된 필드와 템플레이션된 필드](../destination-server/server-specs.md#templatized-fields).

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 고객 데이터 필드를 통해 사용자가 Experience Platform UI에서 정보를 입력할 수 있도록 허용하는 방법을 더 잘 이해할 수 있어야 합니다. 이제 사용 사례에 적합한 고객 데이터 필드를 선택하고 Platform UI에서 고객 데이터 필드를 구성, 순서 및 그룹화하는 방법도 알 수 있습니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [배치 구성](batch-configuration.md)
* [내역 프로필 자격](historical-profile-qualifications.md)