---
title: 환경 끝점
description: Reactor API에서 /environments 끝점을 호출하는 방법을 알아봅니다.
exl-id: 4c22f799-8338-4cf0-980a-3900d725ab5d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 4%

---

# 환경 끝점

다음과 같은 경우 [라이브러리](./libraries.md) 는에 컴파일됩니다. [빌드](./builds.md) Reactor API에서 빌드의 정확한 콘텐츠는 환경 설정 및 라이브러리에 포함된 리소스에 따라 다릅니다. 특히 환경은 다음을 결정합니다.

1. **대상**: 빌드를 배포할 위치입니다. 다음을 선택하여 제어합니다. [호스트](./hosts.md) 을 참조하십시오.
1. **보관**: 빌드를 배포 가능한 파일 세트로 검색하거나 보관 형식으로 압축하도록 선택할 수 있습니다. 이는 다음에 의해 제어됩니다. `archive` 을(를) 환경에 설정합니다.

환경에 의해 구성된 대상 및 아카이브 형식은 애플리케이션에서 빌드를 참조하는 방법을 변경합니다(이 참조는 [포함 코드](../../ui/publishing/environments.md#embed-code)). 대상 또는 파일 형식을 변경하는 경우 새 참조를 사용하려면 응용 프로그램에 대해 일치하는 업데이트를 수행해야 합니다.

환경은 세 가지 유형(또는 단계)으로 구성되며 각 유형에는 가질 수 있는 총 수에 대한 서로 다른 제한이 있습니다.

| 환경 유형 | 허용된 숫자 |
| --- | --- |
| 개발 | (제한 없음) |
| 스테이징 | 1개 |
| 프로덕션 | 1개 |

{style="table-layout:auto"}

이러한 환경 유형은 유사한 비헤이비어를 가지지만 의 여러 단계에서 사용됩니다. [태그 게시 워크플로](../../ui/publishing/publishing-flow.md).

환경은 정확히 하나에 속함 [속성](./properties.md).

환경에 대한 일반적인 내용은 [환경](../../ui/publishing/environments.md) 을 참조하십시오.

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 환경 목록 검색 {#list}

GET 요청의 경로에 속성 ID를 포함하여 속성에 대한 환경 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /properties/{PROPERTY_ID}/environments
```

| 매개변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 다음 `id` 환경을 소유하는 속성. |

{style="table-layout:auto"}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 환경을 다음 속성에 따라 필터링할 수 있습니다.<ul><li>`archive`</li><li>`created_at`</li><li>`name`</li><li>`stage`</li><li>`token`</li><li>`updated_at`</li></ul>다음 안내서를 참조하십시오 [응답 필터링](../guides/filtering.md) 추가 정보.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 속성에 대한 환경 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "ENbe322acb4fc64dfdb603254ffe98b5d3",
      "type": "environments",
      "attributes": {
        "archive": false,
        "created_at": "2020-12-14T17:38:51.047Z",
        "library_path": "f9fd106ab399/cb29d726b35e",
        "library_name": "launch-c0331746ae03-development.min.js",
        "library_entry_points": [
          {
            "library_name": "launch-c0331746ae03-development.min.js",
            "minified": true,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.min.js"
            ],
            "license_path": "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
          },
          {
            "library_name": "launch-c0331746ae03-development.js",
            "minified": false,
            "references": [
              "f9fd106ab399/cb29d726b35e/launch-c0331746ae03-development.js"
            ]
          }
        ],
        "name": "Development Environment A",
        "path": "https://assets.adobedtm.com/staging",
        "stage": "development",
        "updated_at": "2020-12-14T17:38:51.047Z",
        "status": "succeeded",
        "token": "c0331746ae03"
      },
      "relationships": {
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/library"
          },
          "data": null
        },
        "builds": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/builds"
          }
        },
        "host": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/host",
            "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/relationships/host"
          },
          "data": {
            "id": "HTc5cae9ce1e3943aab185bdba939f98bd",
            "type": "hosts"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3/property"
          },
          "data": {
            "id": "PR06c9196bc57048dd8ff169c27baeeca8",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR06c9196bc57048dd8ff169c27baeeca8",
        "self": "https://reactor.adobe.io/environments/ENbe322acb4fc64dfdb603254ffe98b5d3"
      },
      "meta": {
        "archive_encrypted": false
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 환경 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 환경을 조회할 수 있습니다.

**API 형식**

```http
GET /environments/{ENVIRONMENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `ENVIRONMENT_ID` | 다음 `id` 조회하려는 환경. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 환경의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "ENb0c1fbfdc1fd4b8593bfd269f827b3e6",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:30.378Z",
      "library_path": "f9fd106ab399/2f67fccade5e",
      "library_name": "launch-4436c89f6839-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4436c89f6839-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.min.js"
          ],
          "license_path": "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
        },
        {
          "library_name": "launch-4436c89f6839-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/2f67fccade5e/launch-4436c89f6839-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:30.378Z",
      "status": "succeeded",
      "token": "4436c89f6839"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/host",
          "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/relationships/host"
        },
        "data": {
          "id": "HTecb76453c8284f84a3c55fe981b5e6c9",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6/property"
        },
        "data": {
          "id": "PRadbee4fb64754081a945ed2a5b66627a",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRadbee4fb64754081a945ed2a5b66627a",
      "self": "https://reactor.adobe.io/environments/ENb0c1fbfdc1fd4b8593bfd269f827b3e6"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## 환경 만들기 {#create}

POST 요청을 하여 새 환경을 만들 수 있습니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/environments
```

| 매개변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 다음 `id` / [속성](./properties.md) 아래에 환경을 정의하는 경우 |

{style="table-layout:auto"}

**요청**

다음 요청은 지정된 속성에 대해 새 환경을 만듭니다. 또한 이 호출은 를 통해 환경을 기존 호스트와 연결합니다. `relationships` 속성. 다음 안내서를 참조하십시오 [관계](../guides/relationships.md) 추가 정보.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d/environments \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Development Environment A",
            "archive": true,
            "archive_passphrase": "pass12345",
            "path": "/development-a",
            "stage": "development"
          },
          "relationships": {
            "host": {
              "data": {
                "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
                "type": "hosts"
              }
            }
          },
          "type": "environments"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes.name` | **(필수)** 사람이 인식할 수 있는 환경 이름. |
| `attributes.archive` | 빌드가 보관 형식인지 여부를 나타내는 부울 값입니다. |
| `attributes.archive_passphrase` | 아카이브 파일의 잠금을 해제하는 데 사용할 수 있는 문자열 암호입니다. |
| `attributes.path` | 환경에 대한 호스트 URL의 경로입니다. |
| `attributes.stage` | 환경의 스테이지(개발, 스테이징 또는 프로덕션)입니다. |
| `id` | 다음 `id` 을(를) 업데이트하려는 환경입니다. 다음과 일치해야 합니다. `{ENVIRONMENT_ID}` 요청 경로에 제공된 값입니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 다음과 같아야 합니다. `environments`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 새로 생성된 환경의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "EN867c480dc5ea4158be3ea68e5543bd85",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:31:57.857Z",
      "library_path": "f9fd106ab399/bd007122e3e3",
      "library_name": "launch-4d5a31f6ca53-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-4d5a31f6ca53-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.min.js"
          ],
          "license_path": "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
        },
        {
          "library_name": "launch-4d5a31f6ca53-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/bd007122e3e3/launch-4d5a31f6ca53-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:31:57.857Z",
      "status": "succeeded",
      "token": "4d5a31f6ca53"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/host",
          "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/relationships/host"
        },
        "data": {
          "id": "HT5d3fbe7bd34d4f65a46fad4598aefd4e",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85/property"
        },
        "data": {
          "id": "PRa41874e4d1604efd9c3c67d7a123f4c6",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRa41874e4d1604efd9c3c67d7a123f4c6",
      "self": "https://reactor.adobe.io/environments/EN867c480dc5ea4158be3ea68e5543bd85"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## 환경 업데이트 {#update}

PATCH 요청 경로에 해당 ID를 포함하여 환경을 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /environments/{ENVIRONMENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `ENVIRONMENT_ID` | 다음 `id` 업데이트하려는 환경 내에서 사용됩니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 `name` 기존 환경의 경우.

```shell
curl -X PATCH \
  https://reactor.adobe.io/environments/DE3fab176ccf8641838b3da59f716fc42b \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New Environment Name"
          },
          "id": "ENeb00d8f62d244732bd27765301b1410f",
          "type": "environments"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 환경에 대해 업데이트할 속성을 나타내는 속성을 가진 객체입니다. 다음 환경 속성을 업데이트할 수 있습니다. <ul><li>`archive`</li><li>`archive_passphrase`</li><li>`include_debug_library`</li><li>`name`</li><li>`path`</li></ul> 에 대한 호출 예 를 참조하십시오 [환경 만들기](#create) 속성 및 해당 사용 사례의 목록입니다. |
| `id` | 다음 `id` 을(를) 업데이트하려는 환경입니다. 다음과 일치해야 합니다. `{ENVIRONMENT_ID}` 요청 경로에 제공된 값입니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 다음과 같아야 합니다. `environments`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 업데이트된 환경의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "ENeb00d8f62d244732bd27765301b1410f",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2020-12-14T17:38:40.608Z",
      "library_path": "f9fd106ab399/1eb59e88f015",
      "library_name": "launch-caa955ee58ff-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-caa955ee58ff-development.min.js",
          "minified": true,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.min.js"
          ],
          "license_path": "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
        },
        {
          "library_name": "launch-caa955ee58ff-development.js",
          "minified": false,
          "references": [
            "f9fd106ab399/1eb59e88f015/launch-caa955ee58ff-development.js"
          ]
        }
      ],
      "name": "New environment name",
      "path": "https://assets.adobedtm.com/staging",
      "stage": "development",
      "updated_at": "2020-12-14T17:38:41.210Z",
      "status": "succeeded",
      "token": "caa955ee58ff"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host",
          "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/relationships/host"
        },
        "data": {
          "id": "HT7ea0b7c5c556476bafae8240da2d657d",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property"
        },
        "data": {
          "id": "PR558b6514e529409fa740a34e5f974dd8",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR558b6514e529409fa740a34e5f974dd8",
      "self": "https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

## 환경 삭제

DELETE 요청 경로에 해당 ID를 포함하여 환경을 삭제할 수 있습니다.

**API 형식**

```http
DELETE /environments/{ENVIRONMENT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `ENVIRONMENT_ID` | 다음 `id` 삭제할 환경의 일부입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 응답 본문이 없는 HTTP 상태 204(콘텐츠 없음)를 반환하여 환경이 삭제되었음을 나타냅니다.

## 환경에 대한 관련 리소스 검색 {#related}

다음 호출은 환경에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. 날짜 [환경 조회](#lookup), 이러한 관계는 아래에 나열됩니다. `relationships` 속성.

다음을 참조하십시오. [관계 안내서](../guides/relationships.md) Reactor API의 관계에 대한 자세한 정보입니다.

### 환경에 대한 관련 빌드 나열 {#builds}

를 추가하여 환경을 사용하는 빌드를 나열할 수 있습니다 `/builds` 조회 요청의 경로에 매핑됩니다.

**API 형식**

```http
GET  /environments/{ENVIRONMENT_ID}/builds
```

| 매개변수 | 설명 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 다음 `id` 빌드를 나열할 환경. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/builds \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 환경을 사용하는 빌드 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "BL775f919553aa4c6c8116cbf1da8baec8",
      "type": "builds",
      "attributes": {
        "created_at": "2020-12-14T17:32:43.113Z",
        "status": "pending",
        "updated_at": "2020-12-14T17:32:43.113Z",
        "token": "983989bcdad4"
      },
      "relationships": {
        "data_elements": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/data_elements"
          }
        },
        "extensions": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/extensions"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/rules"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/environment"
          },
          "data": {
            "id": "ENd8b1aee9d1674e7aa6135752ce839f82",
            "type": "environments"
          }
        },
        "library": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/library"
          },
          "data": {
            "id": "LB9bca25483e0849a089524c5ca655f2fe",
            "type": "libraries"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8/property"
          },
          "data": {
            "id": "PRbe32d7f41b2741ecae1c06f6fd2d3906",
            "type": "properties"
          }
        }
      },
      "links": {
        "environment": "https://reactor.adobe.io/environments/ENd8b1aee9d1674e7aa6135752ce839f82",
        "library": "https://reactor.adobe.io/libraries/LB9bca25483e0849a089524c5ca655f2fe",
        "self": "https://reactor.adobe.io/builds/BL775f919553aa4c6c8116cbf1da8baec8"
      },
      "meta": {
        "artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/launch-d481f2d29bd0-development.min.js",
        "direct_artifact_url": "https://assets.adobedtm.com/staging/f9fd106ab399/70ee12a3f313/983989bcdad4/launch-d481f2d29bd0-development.min.js",
        "archive": false,
        "host_type_of": "akamai"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

### 환경에 대한 관련 호스트 조회 {#host}

환경을 활용하는 호스트를 추가하려면 다음을 추가합니다 `/host` GET 요청 경로로 이동합니다.

>[!NOTE]
>
>다음을 통해 호스트 관계 객체 자체를 조회할 수 있습니다. [별도의 호출](#host-relationship).

**API 형식**

```http
GET  /environments/{ENVIRONMENT_ID}/host
```

| 매개변수 | 설명 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 다음 `id` 조회하려는 호스트가 있는 환경입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/host \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 환경을 사용하는 호스트의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "HT621241cf4fbb4f7da5b6415ee1b15ac0",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:43:05.382Z",
      "server": null,
      "name": "Example Akamai Host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:43:05.382Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0/property"
        },
        "data": {
          "id": "PR50586546f7764fc59997342b8ff7647c",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR50586546f7764fc59997342b8ff7647c",
      "self": "https://reactor.adobe.io/hosts/HT621241cf4fbb4f7da5b6415ee1b15ac0"
    }
  }
}
```

### 환경에 대한 관련 라이브러리 조회 {#library}

를 추가하여 환경을 사용하는 라이브러리를 조회할 수 있습니다 `/library` GET 요청 경로로 이동합니다.

**API 형식**

```http
GET  /environments/{ENVIRONMENT_ID}/library
```

| 매개변수 | 설명 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 다음 `id` 라이브러리를 조회할 환경의 일부입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/library \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 환경을 사용하는 라이브러리의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "LB6ce27064ebe04ceab3d6942e9de563db",
    "type": "libraries",
    "attributes": {
      "created_at": "2020-12-14T17:50:06.695Z",
      "name": "My Library",
      "published_at": null,
      "state": "development",
      "updated_at": "2020-12-14T17:50:06.695Z",
      "build_required": true
    },
    "relationships": {
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/builds"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/environment",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/environment"
        },
        "data": {
          "id": "EN3287da6fafa143c289afd2f578b4d33d",
          "type": "environments"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/data_elements",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/extensions",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/notes"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/rules",
          "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/relationships/rules"
        }
      },
      "upstream_library": {
        "data": null
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/property"
        },
        "data": {
          "id": "PR95eaa16990c745a78f5bee8439fe4c34",
          "type": "properties"
        }
      },
      "last_build": {
        "links": {
          "related": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db/last_build"
        },
        "data": null
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR95eaa16990c745a78f5bee8439fe4c34",
      "self": "https://reactor.adobe.io/libraries/LB6ce27064ebe04ceab3d6942e9de563db"
    },
    "meta": {
      "build_status": null,
      "build_required_detail": "No build found since last state change"
    }
  }
}
```

### 환경에 대한 관련 속성 조회 {#property}

를 추가하여 환경을 소유한 속성을 조회할 수 있습니다 `/property` GET 요청 경로로 이동합니다.

**API 형식**

```http
GET  /environments/{ENVIRONMENT_ID}/property
```

| 매개변수 | 설명 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 다음 `id` 속성을 조회하려는 환경입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/ENeb00d8f62d244732bd27765301b1410f/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 환경을 소유하는 속성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "PR7688dba9f1384507bbd20f10947536f2",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:55.254Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:55.254Z",
      "platform": "web",
      "development": false,
      "token": "9611419d84a4",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/environments",
      "extensions": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/extensions",
      "rules": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2/rules",
      "self": "https://reactor.adobe.io/properties/PR7688dba9f1384507bbd20f10947536f2"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
