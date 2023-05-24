---
title: 메모 엔드포인트
description: Reactor API에서 /notes 끝점을 호출하는 방법을 알아봅니다.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# 메모 엔드포인트

Reactor API에서 참고는 특정 리소스에 추가할 수 있는 텍스트 주석입니다. 참고는 기본적으로 해당 리소스에 대한 주석입니다. 참고의 내용은 리소스 동작에 영향을 주지 않으며, 다음을 포함한 다양한 사용 사례에 사용할 수 있습니다.

* 배경 정보 제공
* 할 일 목록으로 작동
* 리소스 사용 조언 전달
* 다른 팀원에게 지침 제공
* 기록 컨텍스트 기록

다음 `/notes` Reactor API의 끝점을 사용하면 이러한 메모를 프로그래밍 방식으로 관리할 수 있습니다.

참고는 다음 리소스에 적용할 수 있습니다.

* [데이터 요소](./data-elements.md)
* [확장](./extensions.md)
* [라이브러리](./libraries.md)
* [속성](./properties.md)
* [규칙 구성 요소](./rule-components.md)
* [규칙](./rules.md)
* [비밀](./secrets.md)

이 6가지 유형을 통칭하여 &quot;주목할 만한&quot; 리소스라고 합니다. 주목할 만한 리소스를 삭제하면 연결된 참고도 삭제됩니다.

>[!NOTE]
>
>여러 개의 수정 버전이 있을 수 있는 리소스의 경우 현재(헤드) 수정 버전에 모든 메모를 만들어야 합니다. 다른 수정 사항에 첨부할 수 없습니다.
>
>그러나 참고는 여전히 수정 버전에서 읽을 수 있습니다. 이러한 경우 API는 개정 생성 전에 존재했던 참고만 반환합니다. 이 스냅샷은 수정본을 잘라낼 때의 주석 스냅샷을 제공합니다. 반면 현재(헤드) 수정본에서 메모를 읽으면 해당 메모가 모두 반환됩니다.

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 메모 목록 검색 {#list}

를 추가하여 리소스에 대한 노트 목록을 검색할 수 있습니다 `/notes` 해당 리소스에 대한 GET 요청 경로로 이동합니다.

**API 형식**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 매개변수 | 설명 |
| --- | --- |
| `RESOURCE_TYPE` | 메모를 가져오는 리소스의 유형입니다. 다음 값 중 하나여야 합니다. <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 다음 `id` 메모를 나열할 특정 리소스. |

{style="table-layout:auto"}

**요청**

다음 요청은 라이브러리에 첨부된 메모를 나열합니다.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공한 응답은 지정된 리소스에 첨부된 참고 목록을 반환합니다.

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

## 메모 조회 {#lookup}

GET 요청 경로에 해당 ID를 제공하여 메모를 조회할 수 있습니다.

**API 형식**

```http
GET /notes/{NOTE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `NOTE_ID` | 다음 `id` 조회하려는 메모. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 메모의 세부 사항을 반환합니다.

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
>새 메모를 작성하기 전에 메모를 편집할 수 없으며 삭제할 수 있는 유일한 방법은 해당 리소스를 삭제하는 것입니다.

다음을 추가하여 새 메모를 만들 수 있습니다. `/notes` 해당 리소스에 대한 POST 요청 경로로 이동합니다.

**API 형식**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| 매개변수 | 설명 |
| --- | --- |
| `RESOURCE_TYPE` | 메모를 작성 중인 리소스의 유형입니다. 다음 값 중 하나여야 합니다. <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | 다음 `id` 메모를 만들 특정 리소스. |

{style="table-layout:auto"}

**요청**

다음 요청은 속성에 대한 새 메모를 만듭니다.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | **(필수)** 업데이트 중인 리소스 유형. 이 끝점의 경우 값은 다음과 같아야 합니다. `notes`. |
| `attributes.text` | **(필수)** 메모를 구성하는 텍스트입니다. 각 참고는 512개의 유니코드 문자로 제한됩니다. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 새로 생성된 노트의 세부 정보를 반환합니다.

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
