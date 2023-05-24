---
description: 파일 기반 대상에 대한 파일 서식 옵션 구성
title: Destination SDK을 사용하여 파일 기반 대상에 대한 파일 서식 옵션을 구성하는 방법에 대해 알아봅니다.
exl-id: e61c7989-1123-4b3b-9781-a6097cd0e2b4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# 파일 기반 대상에 대한 파일 서식 옵션 구성

## 개요 {#overview}

Destination SDK을 사용하면 내보낸 파일의 형식 지정 및 압축 옵션을 스토리지 위치의 다운스트림 요구 사항에 맞게 광범위하게 조정할 수 있습니다.

이 페이지에서는 Destination SDK을 사용하여 파일 기반 대상에 대한 파일 서식 옵션을 구성하는 방법에 대해 설명합니다.

## 사전 요구 사항 {#prerequisites}

아래 설명된 단계로 진행하기 전에 다음을 읽어 보십시오. [Destination SDK 시작](../../getting-started.md) Destination SDK API를 사용하여 작업하는 데 필요한 Adobe I/O 인증 자격 증명 및 기타 전제 조건을 얻는 방법에 대한 자세한 내용을 보려면 페이지 를 참조하십시오.

또한 Adobe은 계속하기 전에 다음 설명서를 읽고 숙지하는 것이 좋습니다.

* 사용 가능한 모든 파일 서식 지정 옵션은 [파일 포맷 구성](../../functionality/destination-server/file-formatting.md) 섹션.
* 다음 단계를 완료합니다. [파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md) Destination SDK 사용.

## 서버 및 파일 구성 만들기 {#create-server-file-configuration}

를 사용하여 시작 `/destination-server` 내보낸 파일에 대해 설정할 파일 형식 지정 구성 옵션을 결정하는 끝점입니다.

다음은 의 대상 서버 구성 예입니다. [!DNL Amazon S3] 대상(여러 파일 형식 옵션 선택)

**API 형식**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**요청**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
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
}
}'
```

## 대상 구성에 파일 형식 옵션 추가 {#create-destination-configuration}

>[!TIP]
>
>**Experience Platform UI 확인**. 아래 섹션에 설명된 구성으로 파일 형식 지정 옵션을 구성할 때 이러한 옵션이 렌더링되는 방법에 대한 Experience Platform UI를 확인해야 합니다.

이전 단계에서 대상 서버 및 파일 형식 구성에 원하는 파일 형식 지정 옵션을 추가한 후 다음을 사용할 수 있습니다. `/destinations` 원하는 필드를 대상 구성에 고객 데이터 필드로 추가하기 위한 API 엔드포인트.

>[!IMPORTANT]
>
>이 단계는 선택 사항이며 Experience Platform UI에서 사용자에게 표시되는 파일 형식 옵션 중 하나만 결정합니다. 파일 형식 지정 옵션을 고객 데이터 필드로 설정하지 않으면 파일 내보내기가 [서버 및 파일 구성](#create-server-file-configuration).

이 단계에서는 표시된 옵션을 원하는 순서로 그룹화할 수 있으며, 선택한 파일 유형을 기반으로 사용자 정의 그룹화, 드롭다운 필드 및 조건부 그룹화를 만들 수 있습니다. 이러한 모든 설정은 녹음/녹화 및 아래 섹션에 표시됩니다.

![배치 파일에 대한 다양한 파일 서식 옵션을 보여 주는 화면 기록입니다.](../../assets/guides/batch/file-formatting-options.gif)

### 파일 서식 옵션 순서 지정 {#ordering}

파일 형식 옵션을 대상 구성의 고객 데이터 필드로 추가하는 순서는 UI에 반영됩니다. 예를 들어 아래 구성은 옵션이 순서대로 표시되는 UI에 그에 따라 반영됩니다 **[!UICONTROL 구분 기호]**, **[!UICONTROL 인용 문자]**, **[!UICONTROL 문자 이스케이프 처리]**, **[!UICONTROL 빈 값]**, **[!UICONTROL Null 값]**.

![Experience Platform UI에서 파일 형식 옵션 순서를 보여 주는 이미지입니다.](../../assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### 파일 서식 옵션 그룹화 {#grouping}

한 섹션 내에서 여러 파일 서식 옵션을 그룹화할 수 있습니다. UI에서 대상에 대한 연결을 설정할 때 사용자는 유사한 필드를 시각적으로 그룹화할 수 있습니다.

이렇게 하려면 다음을 사용합니다. `"type": "object"` 을 클릭하여 그룹을 만들고 파일 형식 지정 옵션을 `properties` 아래 예에 표시된 대로 매개 변수를 사용하여 **[!UICONTROL CSV 옵션]** 강조 표시됩니다.

```json {line-numbers="true" start-number="100" highlight="106-128"}
"customerDataFields":[
[...]
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
      },
      [...]
   ]
}
[...]
]
```

![UI의 CSV 옵션 그룹화를 보여 주는 이미지입니다.](../../assets/guides/batch/file-formatting-grouping.png)

### 파일 형식 옵션에 대한 드롭다운 선택기 만들기 {#dropdown-selectors}

사용자가 여러 옵션(예: CSV 파일의 필드를 구분하는 데 사용해야 하는 문자) 중에서 선택할 수 있도록 하려는 경우, 드롭다운 필드를 UI에 추가할 수 있습니다.

이렇게 하려면 `namedEnum` 아래 표시된 대로 개체 및 구성 `default` 사용자가 선택할 수 있는 옵션의 값입니다.

```json {line-numbers="true" start-number="100" highlight="114-124"}
[...]
"customerDataFields":[
[...]
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
      },
      [...]
   ]
}
[...]
]
```

![위에 표시된 구성으로 생성된 드롭다운 선택기의 예를 보여 주는 화면 레코딩입니다.](../../assets/guides/batch/dropdown-options-file-formatting.gif)

### 조건부 파일 서식 옵션 만들기 {#conditional-options}

사용자가 내보낼 특정 파일 유형을 선택한 경우에만 활성화 워크플로에 표시되는 조건부 파일 서식 옵션을 만들 수 있습니다. 예를 들어 아래 구성은 CSV 파일 옵션에 대한 조건부 그룹화를 만듭니다. CSV 파일 옵션은 사용자가 내보내기에 원하는 파일 유형으로 CSV를 선택할 때만 표시됩니다.

필드를 조건부로 설정하려면 `conditional` 아래와 같은 매개 변수:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

더 넓은 맥락에서 다음을 볼 수 있습니다. `conditional` 아래 대상 구성에서 사용할 필드 및 `fileType` 문자열 및 `csvOptions` 개체가 정의된 개체입니다.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

위의 구성을 기반으로 하는 결과 UI 화면을 아래에서 확인할 수 있습니다. 사용자가 파일 유형 CSV를 선택하면 CSV 파일 유형을 참조하는 추가 파일 형식 옵션이 UI에 표시됩니다.

![CSV 파일에 대한 조건부 파일 형식 지정 옵션을 보여 주는 화면 기록입니다.](../../assets/guides/batch/conditional-file-formatting.gif)

### 위에 표시된 모든 옵션을 포함하는 전체 API 요청

아래 API 요청은 위의 섹션에 설명된 모든 옵션을 한 구성에 결합합니다.

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
  "name": "My S3 Destination",
  "description": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
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
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
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
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

성공적인 응답은 고유 식별자( )를 포함하여 대상 구성을 반환합니다.`instanceId`)을 참조하십시오.

## 알려진 제한 사항 {#known-limitations}

특정 파일 형식 옵션 조합을 사용하면 원하지 않는 파일 내보내기 결과가 발생할 수 있습니다.
Adobe은 다음 CSV 옵션 조합을 선택하지 않는 것을 권장합니다.

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

제한을 예시하려면 아래 값이 있는 파일의 내보내기를 고려하십시오.

| 이름 | 성 | 국가 | state |
|---------|----------|---------|--------|
| Michael | 로즈 | 미국 | 뉴욕 |
| 제임스 | Smith |  | null |

{style="table-layout:auto"}

이렇게 하면 아래와 같이 출력이 생성됩니다. 테이블의 null 값이 이스케이프 처리된 견적으로 잘못 내보내지는 방식을 확인합니다.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## 다음 단계 {#next-steps}

이 문서를 읽으면 이제 Destination SDK을 사용하여 내보낸 파일에 대한 사용자 정의 파일 서식 옵션을 설정하는 방법을 알 수 있습니다. 다음으로, 팀은 [파일 기반 대상에 대한 활성화 워크플로](../../../ui/activate-batch-profile-destinations.md) 데이터를 대상으로 내보냅니다.
