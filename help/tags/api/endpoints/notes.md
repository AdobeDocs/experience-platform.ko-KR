---
title: 메모 끝점
description: Reactor API에서 /notes 종단점을 호출하는 방법을 알아봅니다.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 7%

---

# 메모 끝점

Reactor API에서 참고는 특정 리소스에 추가할 수 있는 텍스트 주석입니다. 메모는 본질적으로 각 리소스에 대한 주석입니다. 참고의 내용은 리소스 동작에 영향을 주지 않으며, 다음을 포함한 다양한 사용 사례에 사용할 수 있습니다.

* 배경 정보 제공
* 할 일 목록으로 사용
* 리소스 사용 조언 전달
* 다른 팀 구성원에게 지침 제공
* 기록 컨텍스트 기록

Reactor API의 `/notes` 종단점을 사용하면 이러한 메모를 프로그래밍 방식으로 관리할 수 있습니다.

참고는 다음 리소스를 적용할 수 있습니다.

* [데이터 요소](./data-elements.md)
* [확장](./extensions.md)
* [라이브러리](./libraries.md)
* [속성](./properties.md)
* [규칙 구성 요소](./rule-components.md)
* [규칙](./rules.md)

이 여섯 가지 유형들은 전체적으로 &quot;주목할 만한&quot; 자원이라고 알려져 있습니다. 주목할 만한 리소스가 삭제되면 관련 참고 사항도 삭제됩니다.

>[!NOTE]
>
>여러 개의 개정을 사용할 수 있는 리소스의 경우 현재 (head) 수정 버전에 모든 메모를 만들어야 합니다. 다른 수정 버전에 첨부되지 않을 수 있습니다.
>
>그러나 참고 사항은 여전히 개정 버전에서 읽힐 수 있습니다. 이러한 경우 API는 개정을 만들기 전에 존재했던 참고만 반환합니다. 수정 사항이 삭제되었을 때 주석에 대한 스냅샷을 제공합니다. 반면에 현재(헤드) 개정에서 노트를 읽으면 해당 메모가 모두 반환됩니다.

## 시작

이 안내서에 사용된 끝점은 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml)의 일부입니다. 계속하기 전에 API 인증 방법에 대한 중요한 정보가 필요하면 [시작 안내서](../getting-started.md)를 검토하십시오.

## 메모 목록 검색 {#list}

해당 리소스에 대한 GET 요청 경로에 `/notes`을 추가하여 리소스에 대한 메모 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 매개 변수 | 설명 |
| --- | --- |
| `RESOURCE_TYPE` | 메모를 가져오는 리소스 유형입니다. 다음 값 중 하나여야 합니다. <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 메모를 나열할 특정 리소스의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청에는 라이브러리에 첨부된 참고가 나열됩니다.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 지정된 리소스에 첨부된 참고 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
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

## 참고 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 메모를 조회할 수 있습니다.

**API 형식**

```http
GET /notes/{NOTE_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `NOTE_ID` | 조회할 메모의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 참고의 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## 참고 만들기 {#create}

>[!WARNING]
>
>새 메모를 만들려면 먼저 메모를 편집할 수 없으며 해당 리소스를 삭제하는 방법만 기억하십시오.

해당 리소스에 대한 POST 요청 경로에 `/notes`을 추가하여 새 메모를 만들 수 있습니다.

**API 형식**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 매개 변수 | 설명 |
| --- | --- |
| `RESOURCE_TYPE` | 메모를 만드는 리소스 유형입니다. 다음 값 중 하나여야 합니다. <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 메모를 만들 특정 리소스의 `id` |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 속성에 대한 새 메모를 만듭니다.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `type` | **(필수)** 업데이트할 리소스 유형입니다. 이 끝점의 경우 값은 `notes`이어야 합니다. |
| `attributes.text` | **(필수)** 메모를 포함하는 텍스트입니다. 각 메모는 512개의 유니코드 문자로 제한됩니다. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적으로 응답하면 새로 만든 참고의 세부 정보가 반환됩니다.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
