---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프서비스 소스에 대한 소스 사양 구성(배치 SDK)
description: 이 문서에서는 셀프서비스 소스(일괄 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2090'
ht-degree: 1%

---

# 셀프 서비스 소스에 대한 소스 사양 구성(배치 SDK)

Source 사양에는 소스의 카테고리, Beta 상태 및 카탈로그 아이콘과 관련된 속성을 포함하여 소스와 관련된 정보가 포함되어 있습니다. 여기에는 URL 매개 변수, 콘텐츠, 헤더 및 일정과 같은 유용한 정보도 포함됩니다. Source 사양은 기본 연결에서 소스 연결을 만드는 데 필요한 매개 변수의 스키마도 설명합니다. 소스 연결을 만들려면 스키마가 필요합니다.

완전히 채워진 소스 사양의 예는 [부록](#source-spec)을 참조하십시오.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `sourceSpec.attributes` | UI 또는 API와 관련된 소스에 대한 정보를 포함합니다. |
| `sourceSpec.attributes.uiAttributes` | UI와 관련된 소스에 대한 정보를 표시합니다. |
| `sourceSpec.attributes.uiAttributes.isBeta` | 소스에 해당 기능에 추가하기 위해 고객의 피드백이 더 필요한지 여부를 나타내는 부울 속성. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 소스의 범주를 정의합니다. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Experience Platform UI에서 소스를 렌더링하는 데 사용되는 아이콘을 정의합니다. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 소스에 대한 간단한 설명을 표시합니다. |
| `sourceSpec.attributes.uiAttributes.label` | Experience Platform UI에서 소스의 렌더링에 사용할 레이블을 표시합니다. |
| `sourceSpec.attributes.spec.properties.urlParams` | URL 리소스 경로, 메서드 및 지원되는 쿼리 매개 변수에 대한 정보를 포함합니다. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 데이터를 가져올 위치의 리소스 경로를 정의합니다. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 데이터를 가져오도록 리소스에 요청하는 데 사용할 HTTP 메서드를 정의합니다. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 데이터 가져오기를 요청할 때 소스 URL을 추가하는 데 사용할 수 있는 지원되는 쿼리 매개 변수를 정의합니다. **참고**: 사용자가 제공한 매개 변수 값은 자리 표시자로 포맷해야 합니다. 예: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}`이(가) `/?key=value&key1=value1`(으)로 원본 URL에 추가됩니다. |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 데이터를 가져오는 동안 소스 URL에 대한 HTTP 요청에서 제공해야 하는 헤더를 정의합니다. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 이 속성은 POST 요청을 통해 HTTP 본문을 보내도록 구성할 수 있습니다. |
| `sourceSpec.attributes.spec.properties.contentPath` | Experience Platform에 수집해야 하는 항목 목록을 포함하는 노드를 정의합니다. 이 속성은 유효한 JSON 경로 구문을 따라야 하며 특정 배열을 가리켜야 합니다. | 콘텐츠 경로에 포함된 리소스의 예를 보려면 [추가 리소스 섹션](#content-path)을(를) 보십시오. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Experience Platform에 수집될 컬렉션 레코드를 가리키는 경로입니다. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 이 속성을 사용하면 콘텐츠 경로에서 식별된 리소스에서 수집에서 제외할 특정 항목을 식별할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 이 속성을 사용하면 유지할 개별 속성을 명시적으로 지정할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 이 속성을 사용하면 `contentPath`에 지정한 특성 이름의 값을 재정의할 수 있습니다. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 이 속성을 사용하면 두 배열을 병합하고 리소스 데이터를 Experience Platform 리소스로 변환할 수 있습니다. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 평면화할 컬렉션 레코드를 가리키는 경로입니다. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 이 속성을 사용하면 엔티티 경로에서 식별된 리소스에서 수집되지 않도록 제외할 특정 항목을 식별할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 이 속성을 사용하면 유지할 개별 속성을 명시적으로 지정할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 이 속성을 사용하면 `explodeEntityPath`에 지정한 특성 이름의 값을 재정의할 수 있습니다. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 사용자의 현재 페이지 응답에서 또는 다음 페이지 URL을 만드는 동안 다음 페이지에 대한 링크를 가져오기 위해 제공해야 하는 매개 변수 또는 필드를 정의합니다. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 소스에 대해 지원되는 페이지 매김 유형의 유형을 표시합니다. | <ul><li>`OFFSET`: 이 페이지 매김 유형을 사용하면 결과 배열을 시작할 위치에 인덱스를 지정하여 결과를 구문 분석할 수 있으며 반환되는 결과 수에 대한 제한을 설정할 수 있습니다.</li><li>`POINTER`: 이 페이지 매김 유형을 사용하면 `pointer` 변수를 사용하여 요청과 함께 전송해야 하는 특정 항목을 지정할 수 있습니다. 포인터 형식 페이지 매김에는 다음 페이지를 가리키는 페이로드의 경로가 필요합니다.</li><li>`CONTINUATION_TOKEN`: 이 페이지 매김 유형을 사용하면 쿼리 또는 헤더 매개 변수를 연속 토큰과 함께 추가하여 원본에서 남은 반환 데이터를 검색할 수 있습니다. 이 반환 데이터는 미리 결정된 최대값으로 인해 처음에 반환되지 않았습니다.</li><li>`PAGE`: 이 페이지 매김 유형을 사용하면 쿼리 매개 변수를 페이지 0부터 시작하여 페이지별로 반환 데이터를 이동할 수 있는 페이지 매개 변수와 함께 추가할 수 있습니다.</li><li>`NONE`: 이 페이지 매김 형식은 사용 가능한 페이지 매김 형식을 지원하지 않는 소스에 사용할 수 있습니다. 페이지 매김 형식 `NONE`이(가) 요청 후 전체 응답 데이터를 반환합니다.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. | `limit` 또는 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 페이지에서 가져올 레코드 수입니다. | `limit=10` 또는 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 오프셋 속성 이름입니다. 페이지 매김 유형이 `offset`(으)로 설정된 경우 필요합니다. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 포인터 속성 이름입니다. 이를 위해서는 다음 페이지를 가리키는 속성에 대한 json 경로가 필요합니다. 페이지 매김 유형이 `pointer`(으)로 설정된 경우 필요합니다. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 소스에 대해 지원되는 예약 형식을 정의하는 매개 변수를 포함합니다. 일정 매개 변수에는 `startTime` 및 `endTime`이(가) 포함되어 있습니다. 이 두 매개 변수 모두 일괄 처리 실행에 대한 특정 시간 간격을 설정할 수 있으므로 이전 일괄 처리 실행에서 가져온 레코드를 다시 가져오지 않습니다. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 시작 시간 매개 변수 이름을 정의합니다. | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 종료 시간 매개 변수 이름 정의 | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | `scheduleStartParamName`에 지원되는 형식을 정의합니다. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | `scheduleEndParamName`에 지원되는 형식을 정의합니다. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 사용자가 제공한 매개 변수를 정의하여 리소스 값을 가져옵니다. | `spec.properties`에 대한 사용자 입력 매개 변수의 예는 [추가 리소스](#user-input)을(를) 참조하십시오. |

{style="table-layout:auto"}

## 추가 리소스 {#appendix}

다음 단원에서는 고급 예약 및 사용자 지정 스키마를 포함하여 `sourceSpec`에 대해 수행할 수 있는 추가 구성에 대한 정보를 제공합니다.

### 콘텐츠 경로 예 {#content-path}

다음은 [!DNL MailChimp Members] 연결 사양의 `contentPath` 속성 내용의 예입니다.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` 사용자 입력 예 {#user-input}

다음은 [!DNL MailChimp Members] 연결 사양을 사용하는 사용자 제공 `spec.properties`의 예입니다.

이 예제에서는 `listId`이(가) `urlParams.path`의 일부로 제공됩니다. 고객으로부터 `listId`을(를) 검색해야 하는 경우 `spec.properties`의 일부로 정의해야 합니다.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Source 사양 예 {#source-spec}

다음은 [!DNL MailChimp Members]을(를) 사용하여 완료된 소스 사양입니다.

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### 소스에 대해 다양한 페이지 매김 유형 구성 {#pagination}

다음은 셀프서비스 소스(일괄 SDK)에서 지원하는 다른 페이지 매김 유형의 예입니다.

>[!BEGINTABS]

>[!TAB 오프셋]

이 페이지 매김 유형을 사용하면 결과 배열을 시작할 위치에 인덱스를 지정하고 반환되는 결과 수에 대한 제한을 지정하여 결과를 구문 분석할 수 있습니다. 예:

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 데이터를 반환하는 데 사용되는 페이지 매김 유형입니다. |
| `limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. |
| `limitValue` | 페이지에서 가져올 레코드 수입니다. |
| `offSetName` | 오프셋 속성 이름입니다. 페이지 매김 유형이 `offset`(으)로 설정된 경우 필요합니다. |
| `endConditionName` | 다음 HTTP 요청에서 페이지 매김 루프를 종료하는 조건을 나타내는 사용자 정의 값입니다. 종료 조건을 지정할 속성 이름을 제공해야 합니다. |
| `endConditionValue` | 종료 조건을 지정할 속성 값입니다. |

>[!TAB 포인터]

이 페이지 매김 유형을 사용하면 `pointer` 변수를 사용하여 요청과 함께 전송해야 하는 특정 항목을 지정할 수 있습니다. 포인터 형식 페이지 매김에는 다음 페이지를 가리키는 페이로드의 경로가 필요합니다. 예:

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 데이터를 반환하는 데 사용되는 페이지 매김 유형입니다. |
| `limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. |
| `limitValue` | 페이지에서 가져올 레코드 수입니다. |
| `pointerPath` | 포인터 속성 이름입니다. 이를 위해서는 다음 페이지를 가리키는 속성에 대한 json 경로가 필요합니다. |

>[!TAB 연속 토큰]

페이지 매김의 연속 토큰 유형은 단일 응답에서 반환할 수 있는 최대 항목 수가 미리 결정되었기 때문에 반환할 수 없는 항목이 더 있음을 나타내는 문자열 토큰을 반환합니다.

연속 토큰 유형의 페이지 매김을 지원하는 소스에는 다음과 유사한 페이지 매김 매개 변수가 있을 수 있습니다.

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 데이터를 반환하는 데 사용되는 페이지 매김 유형입니다. |
| `continuationTokenPath` | 반환된 결과의 다음 페이지로 이동하기 위해 쿼리 매개 변수에 추가해야 하는 값입니다. |
| `parameterType` | `parameterType` 속성은 `parameterName`을(를) 추가해야 하는 위치를 정의합니다. `QUERYPARAM` 형식을 사용하면 쿼리를 `parameterName`에 추가할 수 있습니다. `HEADERPARAM`을(를) 사용하면 헤더 요청에 `parameterName`을(를) 추가할 수 있습니다. |
| `parameterName` | 연속 토큰을 통합하는 데 사용되는 매개 변수의 이름입니다. 형식은 다음과 같습니다. `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | 페이지 매김 시 `delayRequestMillis` 속성을 사용하면 소스에 대한 요청 비율을 제어할 수 있습니다. 일부 소스는 분당 수행할 수 있는 요청 수에 제한이 있을 수 있습니다. 예를 들어 [!DNL Zendesk]에는 분당 100개의 요청 제한이 있으며 `delayRequestMillis`을(를) `850`에 정의하면 분당 100개 요청 임계값보다 훨씬 낮은 분당 80개 요청에서 호출하도록 소스를 구성할 수 있습니다. |

다음은 페이지 매김의 연속 토큰 유형을 사용하여 반환되는 응답의 예입니다.

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

>[!TAB 페이지]

`PAGE` 유형의 페이지 매김 기능을 사용하면 0부터 시작하여 페이지 수별로 반환 데이터를 이동할 수 있습니다. `PAGE` 형식 페이지 매김 사용 시 단일 페이지에 지정된 레코드 수를 제공해야 합니다.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 데이터를 반환하는 데 사용되는 페이지 매김 유형입니다. |
| `limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. |
| `limitValue` | 페이지에서 가져올 레코드 수입니다. |
| `initialPageIndex` | (선택 사항) 초기 페이지 색인은 페이지 매김이 시작될 페이지 번호를 정의합니다. 이 필드는 페이지 매김이 0부터 시작되지 않는 소스에 사용할 수 있습니다. 제공하지 않은 경우 초기 페이지 색인은 기본적으로 0으로 설정됩니다. 이 필드에는 정수가 필요합니다. |
| `endPageIndex` | (선택 사항) 종료 페이지 색인을 사용하면 종료 조건을 설정하고 페이지 매김을 중지할 수 있습니다. 페이지 매김을 중지하는 기본 종료 조건을 사용할 수 없을 때 이 필드를 사용할 수 있습니다. `PAGE` 형식 페이지 매김 사용 시 일반적으로 사용되는 응답 헤더를 통해 수집할 페이지 수 또는 마지막 페이지 번호를 제공하는 경우에도 이 필드를 사용할 수 있습니다. 끝 페이지 인덱스의 값은 마지막 페이지 번호이거나 응답 헤더의 문자열 유형 표현식 값일 수 있습니다. 예를 들어 `headers.x-pagecount`을(를) 사용하여 응답 헤더의 `x-pagecount` 값에 종료 페이지 인덱스를 할당할 수 있습니다. **참고**: `x-pagecount`은(는) 일부 소스의 필수 응답 헤더이며 수집할 페이지 수를 포함합니다. |
| `pageParamName` | 반환 데이터의 다른 페이지를 트래버스하기 위해 쿼리 매개 변수에 추가해야 하는 매개 변수의 이름입니다. 예를 들어 `https://abc.com?pageIndex=1`은(는) API 반환 페이로드의 두 번째 페이지를 반환합니다. |
| `maximumRequest` | 지정된 증분 실행에 대해 소스에서 수행할 수 있는 최대 요청 수입니다. 현재 기본 제한은 10000입니다. |

{style="table-layout:auto"}


>[!TAB 없음]

사용 가능한 페이지 매김 유형을 지원하지 않는 소스에는 `NONE` 페이지 매김 유형을 사용할 수 있습니다. `NONE`의 페이지 매김 유형을 사용하는 원본은 GET 요청이 수행될 때 검색 가능한 모든 레코드를 반환하면 됩니다.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### 셀프 서비스 소스에 대한 고급 예약(일괄 SDK)

고급 예약을 사용하여 소스의 증분 및 채우기 일정을 구성합니다. `incremental` 속성을 사용하면 원본에서 새 레코드나 수정된 레코드만 수집하는 일정을 구성할 수 있고, `backfill` 속성을 사용하면 이전 데이터를 수집하는 일정을 만들 수 있습니다.

고급 스케줄링을 사용하면 소스와 관련된 표현식 및 함수를 사용하여 증분 및 채우기 일정을 구성할 수 있습니다. 아래 예에서 [!DNL Zendesk] 원본은 증분 일정의 형식을 `type:user updated > {START_TIME} updated < {END_TIME}`(으)로 지정하고 다시 채우기를 `type:user updated < {END_TIME}`(으)로 지정해야 합니다.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| 속성 | 설명 |
| --- | --- |
| `scheduleParams.type` | 소스에서 사용할 일정 유형. 고급 예약 유형을 사용하려면 이 값을 `ADVANCE`(으)로 설정하십시오. |
| `scheduleParams.paramFormat` | 예약 매개 변수의 정의된 형식입니다. 이 값은 소스의 `scheduleStartParamFormat` 및 `scheduleEndParamFormat` 값과 같을 수 있습니다. |
| `scheduleParams.incremental` | 소스의 증분 쿼리입니다. 증분 은 새로운 데이터나 수정된 데이터만 섭취하는 수집 방법을 의미합니다. |
| `scheduleParams.backfill` | 소스의 채우기 쿼리입니다. 채우기 는 내역 데이터가 수집되는 수집 방법을 의미합니다. |

고급 예약을 구성한 후에는 특정 원본에서 지원하는 내용에 따라 URL, 본문 또는 헤더 매개 변수 섹션에서 `scheduleParams`을(를) 참조해야 합니다. 아래 예에서 `{SCHEDULE_QUERY}`은(는) 증분 및 채우기 예약 식을 사용할 위치를 지정하는 데 사용되는 자리 표시자입니다. [!DNL Zendesk] 원본의 경우 `query`이(가) `queryParams`에서 고급 예약을 지정하는 데 사용됩니다.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### 사용자 정의 스키마를 추가하여 소스의 동적 속성 정의

`sourceSpec`에 사용자 지정 스키마를 포함하여 필요한 동적 특성을 포함하여 소스에 필요한 모든 특성을 정의할 수 있습니다. 연결 사양의 `sourceSpec` 섹션에 사용자 지정 스키마를 제공하는 동안 [!DNL Flow Service] API의 `/connectionSpecs` 끝점에 대해 PUT 요청을 수행하여 소스의 해당 연결 사양을 업데이트할 수 있습니다.

다음은 소스의 연결 사양에 추가할 수 있는 사용자 정의 스키마의 예입니다.

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## 다음 단계

소스 세부 항목을 채운 상태로 Experience Platform에 통합할 소스에 대한 세부 항목 구성을 진행할 수 있습니다. 자세한 내용은 [세부 항목 탐색 구성](./explorespec.md)에 대한 문서를 참조하십시오.
