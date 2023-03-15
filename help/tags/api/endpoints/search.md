---
title: 끝점 검색
description: Reactor API에서 /search 끝점을 호출하는 방법을 알아봅니다.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 1%

---

# 끝점 검색

다음 `/search` Reactor API의 끝점은 쿼리로 표현되는, 원하는 기준과 일치하는 리소스를 찾는 방법을 제공합니다.

다음 API 리소스 유형은 API에서 반환되는 리소스 기반 문서와 동일한 데이터 구조를 활용하여 검색할 수 있습니다.

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

모든 쿼리의 범위는 현재 회사 및 액세스 가능한 속성으로 지정됩니다.

>[!IMPORTANT]
>
>검색 기능에는 다음과 같은 주의 사항과 예외가 있습니다.
>* 메타는 검색할 수 없으며 검색 결과에 반환되지 않습니다.
>* 확장 패키지 위임에 대한 스키마 필드(작업, 조건 등) 중첩된 데이터 구조가 아닌 텍스트로 검색할 수 있습니다.
>* 범위 쿼리는 현재 정수만 지원합니다.


이 기능을 사용하는 방법에 대한 자세한 내용은 [검색 안내서](../guides/search.md).

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 검색 수행 {#perform}

POST 요청을 하여 검색을 수행할 수 있습니다.

**API 형식**

```http
POST /search
```

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `from` | 응답을 오프셋할 결과 수. |
| `size` | 반환할 최대 결과 양입니다. 결과는 100개 항목을 초과할 수 없습니다. |
| `query` | 검색 쿼리를 나타내는 개체입니다. 이 개체의 각 속성에 대해 키는 쿼리할 필드 경로를 나타내야 하며 값은 하위 속성이 쿼리할 항목을 결정하는 개체여야 합니다.<br><br>각 필드 경로에 대해 다음 하위 속성을 사용할 수 있습니다.<ul><li>`exists`: 리소스에 필드가 있는 경우 true를 반환합니다.</li><li>`value`: 필드의 값이 이 속성의 값과 일치하는 경우 true를 반환합니다.</li><li>`value_operator`: 방법을 결정하는 데 사용되는 부울 논리 `value` 쿼리가 처리되어야 합니다. 허용되는 값은 다음과 같습니다. `AND` 및 `OR`. 제외되는 경우 `AND` 논리를 가정합니다. 의 섹션을 참조하십시오. [값 연산자 논리](#value-operator) 추가 정보.</li><li>`range` 필드의 값이 특정 숫자 범위 내에 있으면 true를 반환합니다. 범위 자체는 다음 하위 속성에 의해 결정됩니다.<ul><li>`gt`: 제공한 값보다 크며, 값을 포함할 수 없습니다.</li><li>`gte`: 제공된 값보다 크거나 같습니다.</li><li>`lt`: 제공한 값보다 작으며, 값을 포함하지 않습니다.</li><li>`lte`: 제공된 값보다 작거나 같음.</li></ul></li></ul> |
| `sort` | 결과를 정렬하는 순서를 나타내는 객체 배열입니다. 각 객체에는 단일 속성이 포함되어야 합니다. 키는 정렬할 필드 경로를 나타내고 값은 정렬 순서(`asc` 오름차순의 경우 `desc` 내림차순). |
| `resource_types` | 검색할 특정 리소스 유형을 나타내는 문자열 배열입니다. |

{style="table-layout:auto"}

**응답**

성공한 응답은 쿼리에 대해 일치하는 리소스 목록을 반환합니다. API가 특정 값에 대한 일치 항목을 결정하는 방법에 대한 자세한 내용은 의 부록 섹션을 참조하십시오. [일치 규칙](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## 부록

다음 섹션에는 사용 방법에 대한 추가 정보가 포함되어 있습니다. `/search` 엔드포인트.

### 값 연산자 논리 {#value-operator}

검색 쿼리 값은 색인화된 문서와 일치하도록 용어로 분할됩니다. 각 용어 사이에 `AND` 관계를 가정합니다.

사용 시 `AND` (으)로 `value_operator`, 쿼리 값 `My Rule Holiday Sale` 를 포함하는 필드가 있는 문서로 해석됩니다. `My AND Rule AND Holiday AND Sale`.

사용 시 `OR` (으)로 `value_operator`, 쿼리 값 `My Rule Holiday Sale` 를 포함하는 필드가 있는 문서로 해석됩니다. `My OR Rule OR Holiday OR Sale`. 일치하는 용어가 많을수록 `match_score`. 부분 용어 일치의 특성으로 인해 원하는 값과 거의 일치하는 항목이 없을 때 텍스트 문자 몇 개와 같은 매우 기본적인 수준에서만 값이 일치하는 결과 세트를 얻을 수 있습니다.

### 일치하는 규칙 {#conventions}

검색은 문서가 제공된 질의와 얼마나 관련이 있는지 답변하는 것과 관련이 있습니다. 문서 데이터가 분석되고 색인화되는 방식은 여기에 직접적인 영향을 미칩니다.

다음 표는 일반적인 필드 유형에 대한 일치 규칙을 분류합니다.

| 필드 유형 | 일치 규칙 |
| --- | --- |
| 문자열 | 부분 용어 분석이 포함된 텍스트로서 대소문자를 구분하지 않음 |
| 열거형 값 | 정확한 일치, 대/소문자 구분 |
| 정수 | 정확한 일치 |
| 부동 | 정확한 일치 |
| 타임스탬프 | 정확한 일치(DateTime 형식) |
| 이름 표시 | 부분 용어 분석이 포함된 텍스트로서 대소문자를 구분하지 않음 |

API에 표시되는 특정 필드에 대한 추가 규칙이 있습니다.

| 필드 | 일치 규칙 |
| --- | --- |
| `id` | 정확한 일치, 대/소문자 구분 |
| `delegate_descriptor_id` | 대/소문자를 구분하고 용어가 분할된 정확한 일치 `::` |
| `name` | 정확한 일치, 대/소문자 구분 |
| `settings` | 부분 용어 분석이 포함된 텍스트로서 대소문자를 구분하지 않음 |
| `type` | 정확한 일치, 대/소문자 구분 |
