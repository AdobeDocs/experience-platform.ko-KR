---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프 서비스 소스(배치 SDK)에 대한 소스 사양 구성
topic-legacy: overview
description: 이 문서에서는 셀프 서비스 소스(배치 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: adaa0e1a63536bc1fdf751eec477e5cda9fd20ae
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# 셀프 서비스 소스(배치 SDK)에 대한 소스 사양 구성

소스 사양은 소스의 카테고리, 베타 상태 및 카탈로그 아이콘과 관련된 속성을 비롯하여 소스와 관련된 정보를 포함합니다. 또한 URL 매개 변수, 컨텐츠, 헤더 및 예약과 같은 유용한 정보가 포함되어 있습니다. 소스 사양은 기본 연결에서 소스 연결을 만드는 데 필요한 매개 변수의 스키마를 설명합니다. 소스 연결을 만들려면 스키마가 필요합니다.

자세한 내용은 [부록](#source-spec) 완전히 채워진 소스 세부 항목의 예입니다.


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
| `sourceSpec.attributes.uiAttributes.isBeta` | 소스에 기능을 추가하기 위해 고객으로부터 더 많은 피드백을 필요로 하는지 여부를 나타내는 부울 속성입니다. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | 소스의 카테고리를 정의합니다. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | 플랫폼 UI에서 소스를 렌더링하는 데 사용되는 아이콘을 정의합니다. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | 출처에 대한 간단한 설명을 표시합니다. |
| `sourceSpec.attributes.uiAttributes.label` | 플랫폼 UI에서 소스를 렌더링하는 데 사용할 레이블을 표시합니다. |
| `sourceSpec.attributes.spec.properties.urlParams` | URL 리소스 경로, 메서드 및 지원되는 쿼리 매개 변수에 대한 정보를 포함합니다. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | 데이터를 가져올 의 리소스 경로를 정의합니다. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | 리소스에 대한 데이터 가져오기를 요청하는 데 사용할 HTTP 메서드를 정의합니다. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | 데이터 가져오기를 요청할 때 소스 URL을 추가하는 데 사용할 수 있는 지원되는 쿼리 매개 변수를 정의합니다. **참고**: 사용자가 제공한 모든 매개 변수 값은 자리 표시자로 형식을 지정해야 합니다. 예: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` 은 소스 URL에 다음과 같이 추가됩니다. `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | 데이터를 가져오는 동안 소스 URL에 HTTP 요청에서 제공해야 하는 헤더를 정의합니다. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | 이 속성은 POST 요청을 통해 HTTP 본문을 보내도록 구성할 수 있습니다. |
| `sourceSpec.attributes.spec.properties.contentPath` | Platform에 수집해야 하는 항목 목록이 포함된 노드를 정의합니다. 이 속성은 유효한 JSON 경로 구문을 따라야 하며 특정 배열을 가리켜야 합니다. | 보기 [추가 리소스 섹션](#content-path) 컨텐츠 경로 내에 포함된 리소스의 예입니다. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | Platform에 수집할 컬렉션 레코드를 가리키는 경로입니다. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | 이 속성을 사용하면 수집되지 않도록 제외할 컨텐츠 경로에서 식별된 리소스에서 특정 항목을 식별할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | 이 속성을 사용하면 유지할 개별 속성을 명시적으로 지정할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | 이 속성을 사용하면 지정한 속성 이름의 값을 재정의할 수 있습니다 `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | 이 속성을 사용하면 두 개의 배열을 병합하고 리소스 데이터를 플랫폼 리소스로 변환할 수 있습니다. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | 평면화할 컬렉션 레코드를 가리키는 경로입니다. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | 이 속성을 사용하면 수집되지 않도록 제외할 엔티티 경로에서 식별된 리소스에서 특정 항목을 식별할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | 이 속성을 사용하면 유지할 개별 속성을 명시적으로 지정할 수 있습니다. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | 이 속성을 사용하면 지정한 속성 이름의 값을 재정의할 수 있습니다 `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | 사용자의 현재 페이지 응답에서 다음 페이지로 이동하는 링크를 가져오거나 다음 페이지 URL을 만드는 동안 제공해야 하는 매개 변수 또는 필드를 정의합니다. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 소스에 대해 지원되는 페이지 매김 유형의 유형을 표시합니다. | <ul><li>`OFFSET`: 이 페이지 매김 유형을 사용하면 결과 배열을 시작할 위치의 색인과 반환된 결과 수에 대한 제한을 지정하여 결과를 구문 분석할 수 있습니다.</li><li>`POINTER`: 이 페이지 매김 유형을 사용하면 `pointer` 변수와 함께 요청하여 전송해야 하는 특정 항목을 가리키도록 하는 변수입니다. 포인터 유형 페이지 매김에는 다음 페이지를 가리키는 페이로드에 경로가 필요합니다.</li><li>`CONTINUATION_TOKEN`: 이 페이지 매김 유형을 사용하면 미리 결정된 최대값으로 인해 처음에 반환되지 않은 소스의 나머지 반환 데이터를 검색할 수 있도록 쿼리 또는 헤더 매개 변수를 연속 토큰에 추가할 수 있습니다.</li><li>`PAGE`: 이 페이지 매김 유형을 사용하면 페이지 0부터 시작하여 페이지별로 반환 데이터를 트래버스하기 위해 페이징 매개 변수와 함께 쿼리 매개 변수를 추가할 수 있습니다.</li><li>`NONE`: 이 페이지 매김 유형은 사용 가능한 페이지 매김 유형을 지원하지 않는 소스에 사용할 수 있습니다. 페이지 매김 유형 `NONE` 요청 후 전체 응답 데이터를 반환합니다.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. | `limit` 또는 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 페이지에서 가져올 레코드 수입니다. | `limit=10` 또는 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 오프셋 속성 이름입니다. 페이지 매김 유형이 `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 포인터 특성 이름입니다. 이를 위해서는 다음 페이지를 가리키는 속성에 대한 json 경로가 필요합니다. 페이지 매김 유형이 `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 출처에 대해 지원되는 예약 형식을 정의하는 매개 변수를 포함합니다. 예약 매개 변수에는 다음이 포함됩니다 `startTime` 및 `endTime`두 가지 모두 배치 실행에 대한 특정 시간 간격을 설정할 수 있도록 하며, 이 경우 이전 배치 실행에서 가져온 레코드를 다시 가져오지 않습니다. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 시작 시간 매개 변수 이름을 정의합니다. | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 종료 시간 매개 변수 이름을 정의합니다. | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 에 지원되는 형식을 정의합니다 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 에 지원되는 형식을 정의합니다 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 리소스 값을 가져올 사용자가 제공한 매개 변수를 정의합니다. | 자세한 내용은 [추가 리소스](#user-input) 예를 들어, 사용자가 입력한 매개 변수 `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## 추가 리소스 {#appendix}

다음 섹션에서는 다음의 추가 구성에 대해 설명합니다 `sourceSpec`고급 예약 및 사용자 지정 스키마 등

### 컨텐츠 경로 예 {#content-path}

다음은 컨텐츠의 예입니다 `contentPath` 속성을 [!DNL MailChimp Members] 연결 사양입니다.

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

다음은 사용자가 제공한 예입니다 `spec.properties` 사용 [!DNL MailChimp Members] 연결 사양입니다.

이 예제에서는 `listId` 는 의 일부로 제공됩니다 `urlParams.path`. 검색해야 하는 경우 `listId` 고객에서 다음을 의 일부로 정의해야 합니다 `spec.properties`.


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

### 소스 사양 예 {#source-spec}

다음은 [!DNL MailChimp Members]:

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

### 소스의 여러 페이지 매김 유형 구성 {#pagination}

다음은 셀프 서비스 소스(배치 SDK)에서 지원하는 다른 페이지 매김 유형의 예입니다.

#### `CONTINUATION_TOKEN`

페이지 매김의 연속 토큰 유형은 단일 응답으로 반환될 수 있는 항목의 수가 미리 결정되어 반환되지 않는 더 많은 항목이 있음을 나타내는 문자열 토큰을 반환합니다.

페이지 매김의 연속 토큰 유형을 지원하는 소스에는 다음과 유사한 페이지 매김 매개 변수가 있을 수 있습니다.

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
| `parameterType` | 다음 `parameterType` 속성은 다음 위치를 정의합니다. `parameterName` 를 추가해야 합니다. 다음 `QUERYPARAM` 유형을 사용하면 `parameterName`. 다음 `HEADERPARAM` 을(를) 통해 `parameterName` 헤더 요청에 대한 매개 변수 값을 로 지정합니다. |
| `parameterName` | 연속 토큰을 통합하는 데 사용되는 매개 변수의 이름입니다. 형식은 다음과 같습니다. `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | 다음 `delayRequestMillis` 페이지 매김의 속성을 사용하면 소스에 대한 요청 비율을 제어할 수 있습니다. 일부 소스는 분당 수행할 수 있는 요청 수에 제한이 있을 수 있습니다. 예, [!DNL Zendesk] 에는 분당 100개의 요청 및 정의가 제한됩니다  `delayRequestMillis` to `850` 분당 약 80개의 요청과 분당 100개의 요청 하에서 호출을 하도록 소스를 구성할 수 있습니다. |

다음은 페이지 매김의 연속 토큰 유형을 사용하여 반환된 응답의 예입니다.

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

#### `PAGE`

다음 `PAGE` 페이지 매김 유형을 사용하면 0부터 시작하는 페이지 수로 반환 데이터를 트래버스할 수 있습니다. 사용 시 `PAGE` 페이지 매김을 입력합니다. 단일 페이지에 지정된 레코드 수를 제공해야 합니다.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| 속성 | 설명 |
| --- | --- |
| `type` | 데이터를 반환하는 데 사용되는 페이지 매김 유형입니다. |
| `limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. |
| `limitValue` | 페이지에서 가져올 레코드 수입니다. |
| `pageParamName` | 반환 데이터의 다른 페이지를 통과하기 위해 쿼리 매개 변수에 추가해야 하는 매개 변수의 이름입니다. 예, `https://abc.com?pageIndex=1` 는 API의 반환 페이로드의 두 번째 페이지를 반환합니다. |
| `maximumRequest` | 소스가 주어진 증분 실행에 대해 수행할 수 있는 최대 요청 수입니다. 현재 기본 제한은 10000. |

#### `NONE`

다음 `NONE` 사용 가능한 페이지 매김 유형을 지원하지 않는 소스에 페이지 매김 유형을 사용할 수 있습니다. 페이지 매김 유형을 사용하는 소스 `NONE` GET 요청이 수행될 때 검색 가능한 모든 레코드를 반환하면 됩니다.

```json
"paginationParams": {
  "type": "NONE"
}
```

### 셀프 서비스 소스(배치 SDK)에 대한 고급 예약

고급 예약을 사용하여 소스의 증분 및 채우기 일정을 구성합니다. 다음 `incremental` 속성을 사용하면 소스에서 새 레코드나 수정된 레코드만 수집하는 일정을 구성할 수 있습니다 `backfill` 속성을 사용하면 이전 데이터를 수집할 일정을 만들 수 있습니다.

고급 예약을 사용하면 소스별 표현식 및 함수를 사용하여 증분 및 채우기 일정을 구성할 수 있습니다. 아래 예에서는 [!DNL Zendesk] 소스에서는 증분 스케줄을 `type:user updated > {START_TIME} updated < {END_TIME}` 및 채우기 `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | 소스에서 사용할 예약 유형입니다. 이 값을 다음으로 설정 `ADVANCE` 고급 스케줄링 유형을 사용하려면 |
| `scheduleParams.paramFormat` | 예약 매개변수의 정의된 형식입니다. 이 값은 소스의 값과 같을 수 있습니다 `scheduleStartParamFormat` 및 `scheduleEndParamFormat` 값. |
| `scheduleParams.incremental` | 소스의 증분 쿼리 증분 은 새 데이터나 수정된 데이터만 수집하는 수집 방법을 나타냅니다. |
| `scheduleParams.backfill` | 소스의 채우기 질의입니다. 채우기 란 이전 데이터를 수집하는 수집 방법을 의미합니다. |

고급 예약을 구성하고 나면 `scheduleParams` 을 입력합니다. 아래 예에서는 `{SCHEDULE_QUERY}` 는 증분 및 채우기 예약 표현식이 사용될 위치를 지정하는 데 사용되는 자리 표시자입니다. 의 경우 [!DNL Zendesk] 소스, `query` 다음에서 사용 `queryParams` 고급 예약을 지정하려면

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

### 사용자 지정 스키마를 추가하여 소스의 동적 속성을 정의합니다

사용자 지정 스키마를 `sourceSpec` 필요한 동적 속성을 비롯하여 소스에 필요한 모든 속성을 정의하려면 에 PUT 요청을 수행하여 소스의 해당 연결 사양을 업데이트할 수 있습니다 `/connectionSpecs` 의 끝점 [!DNL Flow Service] API에 사용자 지정 스키마를 제공하는 동안 `sourceSpec` 연결 사양에 대한 섹션을 참조하십시오.

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

소스 사양이 채워지면 Platform에 통합할 소스에 대한 탐색 사양을 구성할 수 있습니다. 다음 문서를 참조하십시오 [탐색 사양 구성](./explorespec.md) 추가 정보.
