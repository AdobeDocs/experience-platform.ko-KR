---
title: 확장 패키지 사용 권한 부여 끝점
description: Reactor API에서 /extension_package_usage 권한 부여 끝점을 호출하는 방법을 알아봅니다.
source-git-commit: fdf01451527e2fab8eb6e6f9d7b4901a85381450
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 4%

---


# 확장 패키지 사용 승인 끝점

확장 패키지는 [확장](./extensions.md) 확장 개발자가 작성한 경우입니다. 태그 사용자가 사용할 수 있는 추가 기능은 확장 패키지로 정의됩니다. 이러한 기능에는 주 모듈 및 공유 모듈이 포함될 수 있지만, 이러한 모듈은 다음과 같이 가장 자주 제공됩니다. [규칙 구성 요소](./rule-components.md) (이벤트, 조건 및 작업) 및 [데이터 요소](./data-elements.md).

확장 패키지는 개발자의 소유입니다. [회사](./companies.md). 확장 패키지의 소유자는 다른 비즈니스에 패키지의 개인 버전을 사용하도록 승인할 수 있습니다. 승인된 각 비즈니스에는 단일 확장 패키지에 대한 사용 승인이 제공되며, 이는 패키지의 모든 향후 및 현재 비공개 버전에 대해 유효합니다.

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/experience-platform-apis/references/reactor/). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 확장 패키지에 대한 확장 패키지 사용 권한 검색 {#list}

확장 패키지에 대한 사용 승인 목록을 검색하려면 다음 끝점에 대한 GET 요청을 수행하십시오.

**API 형식**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 매개변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 다음 `ID` 목록에 추가할 확장 패키지 사용 승인이 있는 속성의 입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답이 확장 패키지 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
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

## 확장 패키지 사용 인증 만들기 {#create}

각각에 대한 확장 패키지 사용 권한 만들기 [확장 패키지](./extension-packages.md) 및 `{ORG_ID}` 을(를) 인증할 조직입니다. 새 확장 패키지 사용 권한 부여를 만들려면 아래 끝점에 POST 요청을 하십시오.

**API 형식**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 매개변수 | 설명 |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | 다음 `ID` 인증을 만들려는 확장 패키지의 경우입니다.&quot; |

{style="table-layout:auto"}

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| 속성 | 설명 |
| --- | --- |
| `attributes.authorized_org_id` | 다음 `ID` 을(를) 인증할 조직입니다. |

**응답**

성공적인 응답은 새로 생성된 확장 패키지 사용 승인에 대한 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>위의 예제 응답에서 권한 부여는 현재 `pending_approval` 스테이지. 확장 패키지를 사용하기 전에 조직에서 승인을 받아야 합니다. 조직의 사용자는 권한 부여가 승인 보류 중인 동안 비공개 확장 패키지를 검색할 수 있지만 설치할 수 없고 확장 카탈로그에서 찾을 수 없습니다.

## 확장 패키지 사용 승인 목록 검색 {#list_authorizations}

GET 요청을 통해 확장 패키지 사용 승인 목록을 검색할 수 있습니다.

**API 형식**

```http
GET /extension_package_usage_authorizations
```

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답이 확장 패키지 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## 확장 패키지 사용 권한 삭제 {#delete}

확장 패키지 사용 인증을 삭제하려면 다음을 포함하십시오. `ID` DELETE 요청의 경로에 있습니다. 이렇게 하면 승인된 조직이 카탈로그에서 확장 패키지의 개인 버전을 보고 해당 속성에 설치하지 못합니다.

>[!NOTE]
>
>이전에 설치한 모든 비공개 버전은 예상대로 계속 작동합니다.

**API 형식**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `ID` | 다음 `ID` 삭제하려는 확장 패키지 사용 권한 |

{style="table-layout:auto"}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공적인 응답은 응답 본문이 없는 HTTP 상태 204(컨텐츠 없음)를 반환합니다. 확장이 삭제되었음을 나타냅니다.

## 확장 패키지 사용 인증 업데이트 {#update}

확장 패키지 사용 승인을 승인하거나 거부하려면 다음을 포함하십시오. `ID` PATCH 요청의 경로에 있습니다.

>[!NOTE]
>
>회사에 대한 확장 패키지 사용 승인을 승인하거나 거부하려면 다음을 수행해야 합니다. `manage_properties` 권한.

**API 형식**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `ID` | 다음 `ID` 삭제하려는 확장 패키지 사용 권한 |

{style="table-layout:auto"}

**요청**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 수정할 속성입니다. 확장 패키지 사용 승인의 경우 이를 수정할 수 있습니다. `state`. |

**응답**

성공적인 응답은 수정된 확장 패키지 사용 승인의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>승인이 승인되면 조직에서 속성에 확장 패키지를 설치할 수 있습니다.

## 확장 패키지 사용 권한 부여를 위해 확장 패키지에 대한 데이터 검색 {#retrieve_data}

GET 요청을 하여 확장 패키지 사용 승인에 대한 확장 패키지에 대한 데이터를 검색할 수 있습니다.

**API 형식**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| 매개변수 | 설명 |
| --- | --- |
| `ID` | 다음 `ID` 검색할 확장 패키지 사용 권한 중 하나입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**응답**

성공적인 응답은 확장 패키지 인증을 위한 확장 패키지에 대한 데이터를 반환합니다.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
