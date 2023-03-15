---
title: 호스트 엔드포인트
description: Reactor API에서 /hosts 끝점을 호출하는 방법을 알아봅니다.
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: 905384b3190cd55e7caa9c4560d6b2774280eee7
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 3%

---

# 호스트 엔드포인트

>[!NOTE]
>
>이 문서에서는 Reactor API에서 호스트를 관리하는 방법을 다룹니다. 태그의 호스트에 대한 일반적인 내용은 [호스트 개요](../../ui/publishing/hosts/hosts-overview.md) 을 참조하십시오.

Reactor API에서 호스트는 다음 위치에 있는 대상을 정의합니다. [빌드](./builds.md) 게재 가능.

Adobe Experience Platform의 태그 사용자가 빌드를 요청하면 시스템이 라이브러리를 검사하여 빌드 대상을 결정합니다 [환경](./environments.md) 라이브러리를 빌드해야 합니다. 각 환경은 빌드를 전달할 위치를 나타내는 호스트와 관계를 갖습니다.

호스트는 정확히 하나의 호스트에 속함 [속성](./properties.md)과 같은 제한이 있지만 속성에는 호스트가 여러 개 있을 수 있습니다. 속성에 게시하려면 호스트가 하나 이상 있어야 합니다.

호스트는 속성 내의 두 개 이상의 환경에서 사용할 수 있습니다. 속성에 단일 호스트가 있고 해당 속성의 모든 환경이 동일한 호스트를 사용하도록 하는 것이 일반적입니다.

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 호스트 목록 검색 {#list}

GET 요청의 경로에 속성 ID를 포함하여 속성에 대한 호스트 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 다음 `id` 호스트를 소유하는 속성입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>쿼리 매개 변수를 사용하여 나열된 호스트를 다음 속성을 기준으로 필터링할 수 있습니다.<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>다음 안내서를 참조하십시오 [응답 필터링](../guides/filtering.md) 추가 정보.

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 속성에 대한 호스트 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## 호스트 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 호스트를 조회할 수 있습니다.

**API 형식**

```http
GET /hosts/{HOST_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `HOST_ID` | 다음 `id` 조회하려는 호스트에 대해 설명합니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 호스트의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## 호스트 만들기 {#create}

POST 요청을 하여 새 호스트를 만들 수 있습니다.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| 매개 변수 | 설명 |
| --- | --- |
| `PROPERTY_ID` | 다음 `id` / [속성](./properties.md) 아래에 호스트를 정의합니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 지정된 속성에 대해 새 호스트를 만듭니다. 또한 호출은 를 통해 호스트를 기존 확장과 연결합니다. `relationships` 속성. 다음 안내서를 참조하십시오 [관계](../guides/relationships.md) 추가 정보.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "skip_symlinks": true,
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes.name` | **(필수)** 사람이 인식할 수 있는 호스트 이름. |
| `attributes.type_of` | **(필수)** 호스트의 유형입니다. 다음 두 옵션 중 하나가 될 수 있습니다. <ul><li>`akamai` 대상 [Adobe 관리 호스트](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` 대상 [SFTP 호스트](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | 호스트 인증에 사용할 선택적 개인 키입니다. |
| `attributes.path` | 에 추가할 경로 `server` URL. |
| `attributes.port` | 사용할 특정 서버 포트를 나타내는 정수입니다. |
| `attributes.server` | 서버의 호스트 URL입니다. |
| `attributes.skip_symlinks`<br><br>(SFTP 호스트 전용) | 기본적으로 모든 SFTP 호스트는 기호 링크(symlink)를 사용하여 서버에 저장된 라이브러리 빌드를 참조합니다. 그러나 모든 서버가 symlink의 사용을 지원하는 것은 아닙니다. 이 속성이 포함되고 로 설정된 경우 `true`에서 호스트는 심볼릭 링크를 사용하는 대신 복사 작업을 사용하여 빌드 에셋을 직접 업데이트합니다. |
| `attributes.username` | 인증을 위한 선택적 사용자 이름입니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 다음과 같아야 합니다. `hosts`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 새로 생성된 호스트의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## 호스트 업데이트 {#update}

>[!NOTE]
>
>SFTP 호스트만 업데이트할 수 있습니다.

PATCH 요청 경로에 해당 ID를 포함하여 호스트를 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /hosts/{HOST_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `HOST_ID` | 다음 `id` 을(를) 업데이트하려는 호스트에 대해 설명합니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 `name` 기존 호스트의 경우

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 속성을 가진 객체는 호스트에 대해 업데이트될 속성을 나타냅니다. 호스트에 대해 다음 속성을 업데이트할 수 있습니다. <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | 다음 `id` 업데이트할 호스트의 입니다. 다음과 일치해야 합니다. `{HOST_ID}` 요청 경로에 제공된 값입니다. |
| `type` | 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 다음과 같아야 합니다. `hosts`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 업데이트된 호스트의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## 호스트 삭제

DELETE 요청 경로에 해당 ID를 포함하여 호스트를 삭제할 수 있습니다.

**API 형식**

```http
DELETE /hosts/{HOST_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `HOST_ID` | 다음 `id` 을(를) 삭제하려는 호스트에 대해 설명합니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답은 응답 본문이 없는 HTTP 상태 204(콘텐츠 없음)를 반환하여 호스트가 삭제되었음을 나타냅니다.

## 호스트에 대한 관련 리소스 검색 {#related}

다음 호출은 호스트에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. 날짜 [호스트 조회](#lookup), 이러한 관계는 아래에 나열됩니다. `relationships` 속성.

다음을 참조하십시오. [관계 안내서](../guides/relationships.md) Reactor API의 관계에 대한 자세한 정보입니다.

### 호스트에 대한 관련 속성 조회 {#property}

를 추가하여 호스트를 소유하는 속성을 조회할 수 있습니다 `/property` 조회 요청의 경로에 매핑됩니다.

**API 형식**

```http
GET /hosts/{HOST_ID}/property
```

| 매개 변수 | 설명 |
| --- | --- |
| `{HOST_ID}` | 다음 `id` 속성을 조회할 호스트의 속성입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 호스트의 속성에 대한 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
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
