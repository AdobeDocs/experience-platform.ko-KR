---
title: Secret 끝점
description: Reactor API에서 /secrets 종단점을 호출하는 방법을 알아봅니다.
exl-id: 76875a28-5d13-402d-8543-24db7e2bee8e
source-git-commit: 4f3c97e2cad6160481adb8b3dab3d0c8b23717cc
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 7%

---

# Secret 끝점

암호는 이벤트 전달 속성(속성이 `platform` 속성 설정 `edge`). 이를 통해 이벤트 전달에서 보안 데이터 교환을 위해 다른 시스템을 인증할 수 있습니다.

이 안내서에서는 를 호출하는 방법을 보여 줍니다 `/secrets` reactor API의 종단점입니다. 다양한 암호 유형 및 사용 방법에 대한 자세한 내용은 [비밀](../guides/secrets.md) 이 안내서로 돌아가기 전에

## 시작하기

이 안내서에 사용된 엔드포인트는 [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). 계속하기 전에 [시작 안내서](../getting-started.md) 를 참조하십시오.

## 속성에 대한 암호 목록 검색 {#list-property}

GET 요청을 만들어 속성에 속하는 비밀을 나열할 수 있습니다.

**API 형식**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| 매개 변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 암호를 나열할 속성의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRe005d921bb724bc88c3ff28e3e916f04/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공적으로 응답하면 속성에 속하는 기밀 목록이 반환됩니다.

```json
{
  "data": [
    {
      "id": "SE8bd20bd5d16b49ee9d925929e292526c",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:29.777Z",
        "updated_at": "2021-07-16T22:29:29.777Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
          },
          "data": {
            "id": "PRe005d921bb724bc88c3ff28e3e916f04",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/environment"
          },
          "data": {
            "id": "EN80ad9efbf4ff4f15bebd770613378a75",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c",
        "property": "https://reactor.adobe.io/secrets/SE8bd20bd5d16b49ee9d925929e292526c/property"
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

## 환경에 대한 암호 목록 검색 {#list-environment}

GET 요청을 수행하여 환경에 속한 비밀을 나열할 수 있습니다.

**API 형식**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| 매개 변수 | 설명 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 나열할 비밀이 있는 환경의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/environments/EN0a1b00749daf4ff48a34d2ec37286aa7/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공적인 응답은 환경에 속하는 비밀 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "SE57b5ea69acde4595825b85befd1675b3",
      "type": "secrets",
      "attributes": {
        "created_at": "2021-07-16T22:29:35.447Z",
        "updated_at": "2021-07-16T22:29:35.447Z",
        "name": "Example Secret",
        "type_of": "token",
        "activated_at": null,
        "expires_at": null,
        "refresh_at": null,
        "status": "pending",
        "credentials": {
        }
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
          },
          "data": {
            "id": "PRb302ca3557334c13b130da719222ec97",
            "type": "properties"
          }
        },
        "environment": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/environment"
          },
          "data": {
            "id": "EN0a1b00749daf4ff48a34d2ec37286aa7",
            "type": "environments"
          },
          "meta": {
            "stage": "development"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/notes"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3",
        "property": "https://reactor.adobe.io/secrets/SE57b5ea69acde4595825b85befd1675b3/property"
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

## 비밀을 찾아라 {#lookup}

GET 요청 경로에 해당 ID를 포함하여 암호를 찾을 수 있습니다.

**API 형식**

```http
GET /secrets/{SECRET_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 조회하려는 비밀의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공적으로 응답하면 비밀의 세부 사항이 반환됩니다.

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## 암호 만들기 {#create}

POST 요청을 만들어 암호를 만들 수 있습니다.

>[!NOTE]
>
>새 암호를 만들 때 API는 해당 리소스에 대한 정보가 포함된 즉시 응답을 반환합니다. 동시에 비밀 교환 작업이 트리거되어 자격 증명 교환이 작동하는지 테스트합니다. 이 작업은 비동기적으로 처리되고 비밀의 상태 속성을 `succeeded` 또는 `failed` 결과에 따라

**API 형식**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| 매개 변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 에서 암호를 정의할 속성의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR9eff664dc6014217b76939bb78b83976/secrets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example Secret",
            "type_of": "simple-http",
            "credentials": {
              "username": "example_username",
              "password": "pass12345"
            }
          },
          "relationships": {
            "environment": {
              "data": {
                "id": "EN04cdddbdb6574170bcac9f470f3b8087",
                "type": "environments"
              }
            }
          },
          "type": "secrets"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 비밀의 고유한 수사적 이름입니다. |
| `type_of` | 비밀에서 나타내는 인증 자격 증명 유형입니다. 에는 세 개의 허용되는 값이 있습니다.<ul><li>`token`: 토큰 문자열입니다.</li><li>`simple-http`: 사용자 이름과 암호입니다.</li><li>`oauth2`: OAuth 표준을 따르는 자격 증명.</li></ul> |
| `credentials` | 비밀의 자격 증명 값을 포함하는 객체입니다. 에 따라 `type_of` 특성은 다른 속성을 제공해야 합니다. 의 섹션을 참조하십시오. [자격 증명](../guides/secrets.md#credentials) 각 유형에 대한 요구 사항에 대한 자세한 내용은 secrets guide를 참조하십시오. |
| `relationships.environment` | 각 암호는 처음 만들 때 환경과 연결되어야 합니다. 다음 `data` 이 속성 내의 개체는 반드시 포함해야 합니다 `id` 이 비밀과 `type` 값 `environments`. |
| `type` | 만들어지는 리소스 유형입니다. 이 호출의 경우 값은 `secrets`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적으로 응답하면 비밀의 세부 사항이 반환됩니다. 비밀의 유형에 따라 `credentials` 숨겨진 것일 수 있습니다.

```json
{
  "data": { 
    "id": "SE39fdf431f8ad4600bbc24ea73fcb1154", 
    "type": "secrets", 
    "attributes": { 
    "created_at": "2021-07-14T19:33:25.628Z", 
    "updated_at": "2021-07-14T19:33:25.628Z", 
    "name": "Example Secret", 
    "type_of": "simple-http", 
    "activated_at": null, 
    "expires_at": null, 
    "refresh_at": null, 
    "status": "pending", 
    "credentials": { 
      "username": "example_username" 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    } 
  } 
}
```

## 테스트 및 `oauth2` 비밀 {#test}

>[!NOTE]
>
>이 작업은 `type_of` 값 `oauth2`.

을(를) 테스트할 수 있습니다 `oauth2` PATCH 요청 경로에 해당 ID를 포함하여 암호를 지정합니다. 테스트 작업은 교환을 수행하며, `test_exchange` 비밀의 속성 `meta` 개체. 이 작업은 암호 자체를 업데이트하지 않습니다.

**API 형식**

```http
PATCH /secrets/{SECRET_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 의 ID입니다 `oauth2` 테스트할 비밀. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SE6c15a7a64f9041b5985558ed3e19a449 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2"
          },
          "meta": {
            "action": "test"
          },
          "id": "SE6c15a7a64f9041b5985558ed3e19a449",
          "type": "secrets"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 다음을 포함해야 합니다. `type_of` 값이 인 속성 `oauth2`. |
| `meta` | 다음을 포함해야 합니다. `action` 값이 인 속성 `test`. |
| `id` | 테스트하고 있는 비밀의 ID입니다. 이 ID는 요청 경로에 제공된 ID와 일치해야 합니다. |
| `type` | 작동 중인 리소스 유형입니다. 을(를) 로 설정해야 합니다. `secrets`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답으로 인증 서비스의 응답이 포함된 비밀의 세부 정보가 반환됩니다 `meta.test_exchange`.

```json
{ 
  "data": { 
    "id": "SE6c15a7a64f9041b5985558ed3e19a449", 
    "type": "secrets", 
    "attributes": { 
      "activated_at": null, 
      "created_at": "2021-07-14T19:33:25.628Z", 
      "credentials": { 
        "token_url": "https://token_url.test/token/authorize?required_param=value",
        "client_id": "test_client_id", 
        "client_secret": "test_client_secret", 
        "refresh_offset": 14400, 
      },
      "expires_at": null, 
      "name": "Example Secret", 
      "refresh_at": null, 
      "status": "pending", 
      "type_of": "oauth2", 
      "updated_at": "2021-07-14T19:33:25.628Z", 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154", 
      "property": "https://reactor.adobe.io/secrets/SE39fdf431f8ad4600bbc24ea73fcb1154/property" 
    }, 
    "meta": { 
      "test_exchange": { 
        "access_token": "FpIkBn3zxW0fH6EBC4MB", 
        "expires_in": 36000, 
        "token_type": "Bearer", 
      } 
    } 
  } 
}
```

## 암호 다시 시도 {#retry}

암호를 재시도하는 것은 암호 교환을 수동으로 트리거하는 작업입니다. PATCH 요청 경로에 해당 ID를 포함하여 암호를 다시 시도할 수 있습니다.

**API 형식**

```http
PATCH /secrets/{SECRET_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 다시 시도할 비밀의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "token"
          },
          "meta": {
            "action": "retry"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

| 속성 | 설명 |
| --- | --- |
| `attributes` | 다음을 포함해야 합니다. `type_of` 업데이트할 암호와 일치하는 속성(`token`, `simple-http`, 또는 `oauth2`). |
| `meta` | 다음을 포함해야 합니다. `action` 값이 인 속성 `retry`. |
| `id` | 다시 시도하는 비밀의 ID입니다. 이 ID는 요청 경로에 제공된 ID와 일치해야 합니다. |
| `type` | 작동 중인 리소스 유형입니다. 을(를) 로 설정해야 합니다. `secrets`. |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적으로 응답하면 비밀의 세부 정보가 반환되고 그 상태는 로 재설정됩니다 `pending`. 교환이 완료되면 비밀의 상태가 `succeeded` 또는 `failed` 결과에 따라

```json
{
  "data": {
    "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-16T22:29:41.135Z",
      "updated_at": "2021-07-16T22:29:41.135Z",
      "name": "Example Secret",
      "type_of": "token",
      "activated_at": null,
      "expires_at": null,
      "refresh_at": null,
      "status": "pending",
      "credentials": {
        }
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
        },
        "data": {
          "id": "PR19717d5acf114209a5aebd0f2b228438",
          "type": "properties"
        }
      },
      "environment": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment"
        },
        "data": {
          "id": "EN04d820606cc74d5eaf51616e8b50201a",
          "type": "environments"
        },
        "meta": {
          "stage": "development"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/notes"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3",
      "property": "https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property"
    }
  }
}
```

## 권한 재인증 `oauth2-google` 비밀 {#reauthorize}

각 `oauth2-google` 비밀 `meta.token_url_expires_at` 인증 URL이 만료되는 시기를 나타내는 속성입니다. 이 시간 이후에는 인증 프로세스를 갱신하려면 암호를 재승인해야 합니다.

를 재승인하려면 `oauth2-google` 비밀, 문제의 비밀을 PATCH에 요청하라.

**API 형식**

```http
PATCH /secrets/{SECRET_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 다음 `id` 재승인을 원하는 비밀의 |

**요청**

다음 `data` 요청 페이로드의 객체에는 다음이 포함되어야 합니다. `meta.action` 속성 설정 `reauthorize`.

```shell
curl -X PATCH \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "type_of": "oauth2-google"
          },
          "meta": {
            "action": "reauthorize"
          },
          "id": "SEa3756b962e964fadb61e31df1f7dd5a3",
          "type": "secrets"
        }
      }'
```

**응답**

성공적으로 응답하면 업데이트된 비밀의 세부 정보가 반환됩니다. 여기에서 을(를) 복사하여 붙여넣어야 합니다 `meta.token_url` 를 브라우저에서 클릭하여 인증 프로세스를 완료합니다.

```json
{
  "data": {
    "id": "SE5fdfa4c0a2d8404e8b1bc38827cc41c9",
    "type": "secrets",
    "attributes": {
      "created_at": "2021-07-15T19:00:25.628Z", 
      "updated_at": "2021-07-15T19:00:25.628Z", 
      "name": "Example Secret", 
      "type_of": "oauth2-google", 
      "activated_at": null, 
      "expires_at": null, 
      "refresh_at": null, 
      "status": "pending", 
      "credentials": { 
        "scopes": [
          "https://www.googleapis.com/auth/adwords",
          "https://www.googleapis.com/auth/pubsub"
        ], 
      } 
    }, 
    "relationships": { 
      "property": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/property" 
        }, 
        "data": { 
          "id": "PR9eff664dc6014217b76939bb78b83976", 
          "type": "properties" 
        } 
      }, 
      "environment": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/environment" 
        }, 
        "data": { 
          "id": "EN04cdddbdb6574170bcac9f470f3b8087", 
          "type": "environments" 
        }, 
        "meta": { 
          "stage": "development" 
        } 
      }, 
      "notes": { 
        "links": { 
          "related": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/notes" 
        } 
      } 
    }, 
    "links": { 
      "self": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9", 
      "property": "https://reactor.adobe.io/secrets/SE5fdfa4c0a2d8404e8b1bc38827cc41c9/property" 
    }, 
    "meta": { 
      "token_url": "https://accounts.google.com/o/oauth2/auth?access_type=offline&approval_prompt=force&client_id=434635668552-0qvlu519fdjtnkvk8hu8c8dj8rg3723r.apps.googleusercontent.com&redirect_uri=https%3A%2F%2Freactor.adobe.io%2Foauth2%2Fcallback&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fadwords&state=state", 
      "token_url_expires_at": "2021-07-15T20:00:25.628Z" 
    } 
  } 
}
```

## 암호 삭제 {#delete}

DELETE 요청 경로에 해당 ID를 포함하여 암호를 삭제할 수 있습니다. 이 작업은 즉시 효과를 사용하여 하드 삭제되며 라이브러리를 다시 게시할 필요가 없습니다.

이 작업은 관련된 환경에서 암호를 제거하고 기본 리소스가 삭제됩니다.

>[!WARNING]
>
>삭제된 암호를 참조하는 규칙을 배포한 경우 해당 규칙이 즉시 작동하지 않습니다. 이 암호를 참조하는 모든 데이터 요소는 나중에 업데이트하거나 제거해야 합니다.

**API 형식**

```http
DELETE /secrets/{SECRET_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 삭제할 비밀의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X DELETE \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공적으로 응답하면 시스템에서 암호가 삭제되었음을 나타내는 HTTP 상태 204(컨텐츠 없음) 및 빈 응답 본문을 반환합니다.

## 비밀의 노트 나열 {#notes}

Reactor API를 사용하면 암호를 포함한 특정 리소스에 메모를 추가할 수 있습니다. 참고는 리소스 동작에 영향을 주지 않고 다양한 사용 사례에 사용할 수 있는 텍스트 주석입니다.

>[!NOTE]
>
>자세한 내용은 [참고 끝점 안내서](./notes.md) reactor API 리소스에 대한 메모를 만들고 편집하는 방법에 대한 자세한 정보입니다.

GET 요청을 수행하여 비밀과 관련된 모든 메모를 검색할 수 있습니다.

**API 형식**

```http
GET /secrets/{SECRET_ID}/notes
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 메모를 나열할 비밀의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공한 응답은 비밀에 속하는 메모 목록을 반환합니다.

```json
{
  "data": [
    {
      "id": "NTe666dbcc2f204218b6fde2fe60ab7043",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Doe",
        "author_email": "jdoe@example.com",
        "created_at": "2021-07-16T22:29:58.259Z",
        "text": "This is a secret note."
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1"
          },
          "data": {
            "id": "SE591d3b86910f4e6883f0e1c36e54bff1",
            "type": "secrets"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/secrets/SE591d3b86910f4e6883f0e1c36e54bff1",
        "self": "https://reactor.adobe.io/notes/NTe666dbcc2f204218b6fde2fe60ab7043"
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

## 비밀의 관련 리소스 검색 {#related}

다음 호출에서는 암호와 관련된 리소스를 검색하는 방법을 보여 줍니다. When [비밀을 찾다](#lookup)로 설정되면 이러한 관계는 `relationships` 속성을 사용합니다.

자세한 내용은 [관계 안내서](../guides/relationships.md) 를 참조하십시오.

### 관련 환경을 검색하여 암호를 확인하십시오 {#environment}

다음을 추가하여 암호를 사용하는 환경을 조회할 수 있습니다 `/environment` GET 요청의 경로.

**API 형식**

```http
GET /secrets/{SECRET_ID}/environment
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 조회하려는 환경의 암호 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/environment \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공적인 응답은 환경의 세부 사항을 반환합니다.

```json
{
  "data": {
    "id": "EN33e8d63ac647448da1f77ced5c3c8580",
    "type": "environments",
    "attributes": {
      "archive": false,
      "created_at": "2021-07-16T22:19:13.438Z",
      "library_path": "bc12f2b85d11/b9a3067414ff",
      "library_name": "launch-3b6c4eea15ae-development.min.js",
      "library_entry_points": [
        {
          "library_name": "launch-3b6c4eea15ae-development.min.js",
          "minified": true,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.min.js"
          ],
          "license_path": "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
        },
        {
          "library_name": "launch-3b6c4eea15ae-development.js",
          "minified": false,
          "references": [
            "bc12f2b85d11/b9a3067414ff/launch-3b6c4eea15ae-development.js"
          ]
        }
      ],
      "name": "Development Environment A",
      "path": null,
      "stage": "development",
      "updated_at": "2021-07-16T22:19:13.438Z",
      "status": "succeeded",
      "token": "3b6c4eea15ae"
    },
    "relationships": {
      "library": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/library"
        },
        "data": null
      },
      "builds": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/builds"
        }
      },
      "host": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/host",
          "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/relationships/host"
        },
        "data": {
          "id": "HT7d5cf665463e46a1968ada1ceb1b5ca7",
          "type": "hosts"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580/property"
        },
        "data": {
          "id": "PRba81d3027db846b084212391aa5d2f1f",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRba81d3027db846b084212391aa5d2f1f",
      "self": "https://reactor.adobe.io/environments/EN33e8d63ac647448da1f77ced5c3c8580"
    },
    "meta": {
      "archive_encrypted": false
    }
  }
}
```

### 비밀에서 관련 속성 검색 {#property}

다음을 추가하여 암호를 소유하는 속성을 찾을 수 있습니다 `/property` GET 요청의 경로.

**API 형식**

```http
GET /secrets/{SECRET_ID}/property
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 속성을 조회하려는 비밀의 ID입니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

```shell
curl -X GET \
  https://reactor.adobe.io/secrets/SEa3756b962e964fadb61e31df1f7dd5a3/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json'
```

**응답**

성공적인 응답은 속성의 세부 정보를 반환합니다.

```json
{
  "data": {
    "id": "PR2d191feafef54c5da4ddb5ef647d4867",
    "type": "properties",
    "attributes": {
      "created_at": "2021-07-16T22:26:25.320Z",
      "enabled": true,
      "name": "Kessel Edge Example Property",
      "updated_at": "2021-07-16T22:26:25.320Z",
      "platform": "edge",
      "development": false,
      "token": "8efbe7023155"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/company"
        },
        "data": {
          "id": "COc26fb19f87d24cbe827a70ad2a672093",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/COc26fb19f87d24cbe827a70ad2a672093",
      "data_elements": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/data_elements",
      "environments": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/environments",
      "extensions": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/extensions",
      "rules": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867/rules",
      "self": "https://reactor.adobe.io/properties/PR2d191feafef54c5da4ddb5ef647d4867"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "edit_property",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
