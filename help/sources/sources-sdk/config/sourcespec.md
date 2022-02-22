---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 소스 SDK에 대한 인증 사양 구성
topic-legacy: overview
description: 이 문서에서는 소스 SDK를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
hide: true
hidefromtoc: true
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 4c4c89ab7db7d3546163d707ac80210561c2fa02
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# 소스 SDK에 대한 소스 사양 구성

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
| `sourceSpec.attributes.spec.properties.contentPath` | Platform에 수집해야 하는 항목 목록이 포함된 노드를 정의합니다. 이 속성은 유효한 JSON 경로 구문을 따라야 하며 특정 배열을 가리켜야 합니다. | 자세한 내용은 [부록](#content-path) 컨텐츠 경로 내에 포함된 리소스의 예입니다. |
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
| `sourceSpec.attributes.spec.properties.paginationParams.type` | 소스에 대해 지원되는 페이지 매김 유형의 유형을 표시합니다. | <ul><li>`offset`: 이 페이지 매김 유형을 사용하면 결과 배열을 시작할 위치의 색인과 반환된 결과 수에 대한 제한을 지정하여 결과를 구문 분석할 수 있습니다.</li><li>`pointer`: 이 페이지 매김 유형을 사용하면 `pointer` 변수와 함께 요청하여 전송해야 하는 특정 항목을 가리키도록 하는 변수입니다. 포인터 유형 페이지 매김에는 다음 페이지를 가리키는 페이로드에 경로가 필요합니다</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | API가 페이지에서 가져올 레코드 수를 지정할 수 있는 제한 이름입니다. | `limit` 또는 `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | 페이지에서 가져올 레코드 수입니다. | `limit=10` 또는 `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | 오프셋 속성 이름입니다. 페이지 매김 유형이 `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | 포인터 특성 이름입니다. 이를 위해서는 다음 페이지를 가리키는 속성에 대한 json 경로가 필요합니다. 페이지 매김 유형이 `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | 출처에 대해 지원되는 예약 형식을 정의하는 매개 변수를 포함합니다. 예약 매개 변수에는 다음이 포함됩니다 `startTime` 및 `endTime`두 가지 모두 배치 실행에 대한 특정 시간 간격을 설정할 수 있도록 하며, 이 경우 이전 배치 실행에서 가져온 레코드를 다시 가져오지 않습니다. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | 시작 시간 매개 변수 이름을 정의합니다. | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | 종료 시간 매개 변수 이름을 정의합니다. | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | 에 지원되는 형식을 정의합니다 `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | 에 지원되는 형식을 정의합니다 `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | 리소스 값을 가져올 사용자가 제공한 매개 변수를 정의합니다. | 자세한 내용은 [부록](#user-input) 예를 들어, 사용자가 입력한 매개 변수 `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## 부록 {#appendix}

### 컨텐츠 경로 예 {#content-path}

다음은 컨텐츠의 예입니다 `contentPath` 속성을 [!DNL MailChimp Campaigns] 연결 사양입니다.

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

## 다음 단계

소스 사양이 채워지면 Platform에 통합할 소스에 대한 탐색 사양을 구성할 수 있습니다. 다음 문서를 참조하십시오 [탐색 사양 구성](./explorespec.md) 추가 정보.
