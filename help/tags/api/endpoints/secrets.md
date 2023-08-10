---
title: 암호 엔드포인트
description: Reactor API에서 /secrets 끝점을 호출하는 방법을 알아봅니다.
exl-id: 76875a28-5d13-402d-8543-24db7e2bee8e
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 4%

---

# 암호 엔드포인트

암호는 이벤트 전달 속성(가 있는 속성) 내에만 존재하는 리소스입니다. `platform` 속성이 로 설정됨 `edge`). 이벤트 전달을 통해 안전한 데이터 교환을 위해 다른 시스템을 인증할 수 있습니다.

이 안내서에서는 를 호출하는 방법을 보여 줍니다. `/secrets` Reactor API의 끝점입니다. 다양한 암호 유형 및 암호 사용 방법에 대한 자세한 설명은 의 고급 개요를 참조하십시오. [비밀](../guides/secrets.md) 이 안내서로 돌아가기 전에

## 시작하기

이 안내서에 사용된 끝점은 [반응기 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). 계속하기 전에 다음을 검토하십시오. [시작 안내서](../getting-started.md) API 인증 방법에 대한 중요한 정보를 제공합니다.

## 속성에 대한 암호 목록 검색 {#list-property}

GET 요청을 통해 속성에 속하는 암호를 나열할 수 있습니다.

**API 형식**

```http
GET /properties/{PROPERTY_ID}/secrets
```

| 매개변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 비밀을 나열할 속성의 ID입니다. |

{style="table-layout:auto"}

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

성공적인 응답은 속성에 속하는 비밀 목록을 반환합니다.

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

GET 요청을 통해 환경에 속한 비밀을 나열할 수 있습니다.

**API 형식**

```http
GET /environments/{ENVIRONMENT_ID}/secrets
```

| 매개변수 | 설명 |
| --- | --- |
| `{ENVIRONMENT_ID}` | 비밀을 나열할 환경의 ID입니다. |

{style="table-layout:auto"}

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

성공적인 응답은 환경에 속한 비밀 목록을 반환합니다.

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

## 비밀을 찾아보세요 {#lookup}

GET 요청 경로에 해당 ID를 포함하여 암호를 조회할 수 있습니다.

**API 형식**

```http
GET /secrets/{SECRET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 조회할 비밀의 ID입니다. |

{style="table-layout:auto"}

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

성공한 응답은 암호의 세부 정보를 반환합니다.

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

POST 요청을 통해 암호를 만들 수 있습니다.

>[!NOTE]
>
>새 암호를 만들면 API는 해당 리소스에 대한 정보가 포함된 즉시 응답을 반환합니다. 동시에 자격 증명 교환이 작동하는지 테스트하기 위해 비밀 교환 작업이 트리거됩니다. 이 작업은 비동기적으로 처리되며 비밀의 상태 속성을 다음으로 업데이트합니다. `succeeded` 또는 `failed` 결과에 따라.

**API 형식**

```http
POST /properties/{PROPERTY_ID}/secrets
```

| 매개변수 | 설명 |
| --- | --- |
| `{PROPERTY_ID}` | 아래에서 암호를 정의할 속성의 ID입니다. |

{style="table-layout:auto"}

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
| `name` | 암호에 대한 고유하고 수사적인 이름. |
| `type_of` | 암호가 나타내는 인증 자격 증명의 유형입니다. 에는 세 가지 허용되는 값이 있습니다.<ul><li>`token`: 토큰 문자열입니다.</li><li>`simple-http`: 사용자 이름 및 암호.</li><li>`oauth2`: OAuth 표준을 준수하는 자격 증명.</li></ul> |
| `credentials` | 암호에 대한 자격 증명 값을 포함하는 개체입니다. 에 따라 `type_of` attribute, 다른 속성을 제공해야 합니다. 의 섹션을 참조하십시오. [자격 증명](../guides/secrets.md#credentials) 각 유형의 요구 사항에 대한 자세한 내용은 비밀 안내서에서 참조하십시오. |
| `relationships.environment` | 각 암호는 처음 만들 때 환경과 연결되어 있어야 합니다. 다음 `data` 이 속성 내의 객체에는 `id` 과(와) 함께 할당되고 있는 환경 `type` 값 `environments`. |
| `type` | 만들어지는 리소스의 유형입니다. 이 호출의 경우 값은 다음과 같아야 합니다. `secrets`. |

{style="table-layout:auto"}

**응답**

성공한 응답은 암호의 세부 정보를 반환합니다. 암호의 유형에 따라 다음 중 일부 속성을 사용할 수 있습니다. `credentials` 숨겨져 있을 수 있습니다.

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

## 테스트 `oauth2` 비밀 {#test}

>[!NOTE]
>
>이 작업은 이(가) 있는 비밀에 대해서만 수행할 수 있습니다. `type_of` 값 `oauth2`.

다음을 테스트할 수 있습니다. `oauth2` PATCH 요청 경로에 해당 ID를 포함하여 보안을 설정합니다. 테스트 작업은 교환을 수행하고 인증 서비스 응답을 `test_exchange` 비밀의 속성 `meta` 개체. 이 작업은 비밀 자체를 업데이트하지 않습니다.

**API 형식**

```http
PATCH /secrets/{SECRET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 의 ID `oauth2` 테스트하려는 비밀입니다. |

{style="table-layout:auto"}

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
| `attributes` | 다음을 포함해야 함: `type_of` 값이 인 속성 `oauth2`. |
| `meta` | 은(는) 다음을 포함해야 합니다. `action` 값이 인 속성 `test`. |
| `id` | 테스트 중인 암호의 ID입니다. 요청 경로에 제공된 ID와 일치해야 합니다. |
| `type` | 작동 중인 리소스 유형. 을(를) (으)로 설정해야 합니다. `secrets`. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 비밀 정보를 반환하며, 인증 서비스의 응답은 `meta.test_exchange`.

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

암호를 다시 시도하는 것은 암호 교환을 수동으로 트리거하는 작업입니다. PATCH 요청 경로에 해당 ID를 포함하여 암호를 다시 시도할 수 있습니다.

**API 형식**

```http
PATCH /secrets/{SECRET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 다시 시도할 암호의 ID입니다. |

{style="table-layout:auto"}

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
| `attributes` | 다음을 포함해야 함: `type_of` 업데이트 중인 비밀의 속성과 일치하는 속성(`token`, `simple-http`, 또는 `oauth2`). |
| `meta` | 은(는) 다음을 포함해야 합니다. `action` 값이 인 속성 `retry`. |
| `id` | 다시 시도하는 암호의 ID입니다. 요청 경로에 제공된 ID와 일치해야 합니다. |
| `type` | 작동 중인 리소스 유형. 을(를) (으)로 설정해야 합니다. `secrets`. |

{style="table-layout:auto"}

**응답**

성공적인 응답은 암호의 세부 사항을 반환하며 상태는 로 재설정됩니다. `pending`. 교환이 완료되면 비밀의 상태는 다음으로 업데이트됩니다. `succeeded` 또는 `failed` 결과에 따라.

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

각 `oauth2-google` 암호에 다음 포함: `meta.authorization_url_expires_at` 인증 URL이 만료되는 시기를 나타내는 속성입니다. 이 시간이 지나면 비밀이 다시 승인되어야 인증 프로세스가 갱신됩니다.

을(를) 재승인하려면 `oauth2-google` 비밀, 해당 비밀에 대해 PATCH 요청을 합니다.

**API 형식**

```http
PATCH /secrets/{SECRET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 다음 `id` 을(를) 다시 승인할 수 있습니다. |

**요청**

다음 `data` 요청 페이로드의 오브젝트에는 `meta.action` 속성이 로 설정됨 `reauthorize`.

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

성공한 응답은 업데이트된 암호의 세부 정보를 반환합니다. 여기에서 을(를) 복사하여 붙여넣어야 합니다. `meta.authorization_url` 을 브라우저에 추가하여 인증 프로세스를 완료합니다.

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
      "authorization_url": "https://accounts.google.com/o/oauth2/auth?access_type=offline&approval_prompt=force&client_id=434635668552-0qvlu519fdjtnkvk8hu8c8dj8rg3723r.apps.googleusercontent.com&redirect_uri=https%3A%2F%2Freactor.adobe.io%2Foauth2%2Fcallback&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fadwords&state=state", 
      "authorization_url_expires_at": "2021-07-15T20:00:25.628Z" 
    } 
  } 
}
```

## 암호 삭제 {#delete}

DELETE 요청 경로에 해당 ID를 포함하여 암호를 삭제할 수 있습니다. 이는 즉각적인 효과가 있는 하드 삭제이며 라이브러리를 다시 게시할 필요가 없습니다.

이 작업은 관련 환경에서 암호를 제거하고 기본 리소스를 삭제합니다.

>[!WARNING]
>
>삭제된 암호를 참조하는 배포된 규칙이 있는 경우 해당 규칙은 즉시 작동하지 않습니다. 이 암호를 참조하는 모든 데이터 요소는 나중에 업데이트하거나 제거해야 합니다.

**API 형식**

```http
DELETE /secrets/{SECRET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 삭제할 암호의 ID입니다. |

{style="table-layout:auto"}

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

성공적인 응답은 시스템에서 비밀이 삭제되었음을 나타내는 HTTP 상태 204(컨텐츠 없음) 및 빈 응답 본문을 반환합니다.

## 암호에 대한 메모 나열 {#notes}

Reactor API를 사용하면 암호를 포함하여 특정 리소스에 메모를 추가할 수 있습니다. 참고는 리소스 동작에 영향을 주지 않는 텍스트 주석이며, 다양한 사용 사례에 사용할 수 있습니다.

>[!NOTE]
>
>다음을 참조하십시오. [notes 엔드포인트 안내서](./notes.md) Reactor API 리소스에 대한 메모를 만들고 편집하는 방법에 대한 자세한 정보.

GET 요청을 통해 암호와 관련된 모든 메모를 검색할 수 있습니다.

**API 형식**

```http
GET /secrets/{SECRET_ID}/notes
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 메모를 나열할 암호의 ID. |

{style="table-layout:auto"}

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

성공한 응답은 암호에 속하는 메모 목록을 반환합니다.

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

## 암호에 대한 관련 리소스 검색 {#related}

다음 호출은 암호에 대한 관련 리소스를 검색하는 방법을 보여 줍니다. 날짜 [비밀 찾기](#lookup), 이러한 관계는 아래에 나열됩니다. `relationships` 속성.

다음을 참조하십시오. [관계 안내서](../guides/relationships.md) Reactor API의 관계에 대한 자세한 정보입니다.

### 관련 환경에서 암호를 찾습니다. {#environment}

비밀을 활용하는 환경을 추가하여 조회할 수 있습니다 `/environment` GET 요청 경로로 이동합니다.

**API 형식**

```http
GET /secrets/{SECRET_ID}/environment
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 환경을 조회할 비밀의 ID입니다. |

{style="table-layout:auto"}

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

성공한 응답은 환경의 세부 정보를 반환합니다.

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

### 암호의 관련 속성을 조회합니다. {#property}

을 추가하여 암호를 소유한 속성을 조회할 수 있습니다. `/property` GET 요청 경로로 이동합니다.

**API 형식**

```http
GET /secrets/{SECRET_ID}/property
```

| 매개변수 | 설명 |
| --- | --- |
| `{SECRET_ID}` | 조회할 속성의 비밀 ID입니다. |

{style="table-layout:auto"}

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

성공한 응답은 속성의 세부 정보를 반환합니다.

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
