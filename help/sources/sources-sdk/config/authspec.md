---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프서비스 소스에 대한 인증 사양 구성(일괄 SDK)
description: 이 문서에서는 셀프서비스 소스(일괄 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 3%

---

# 셀프서비스 소스에 대한 인증 사양 구성(일괄 SDK)

인증 사양은 Adobe Experience Platform 사용자가 소스에 연결하는 방법을 정의합니다.

`authSpec` 배열에는 원본을 Experience Platform에 연결하는 데 필요한 인증 매개 변수에 대한 정보가 포함되어 있습니다. 지정된 모든 소스는 서로 다른 여러 유형의 인증을 지원할 수 있습니다.

## 인증 사양

셀프 서비스 소스(일괄 SDK)는 OAuth 2 새로 고침 코드 및 기본 인증을 지원합니다. OAuth 2 새로 고침 코드 및 기본 인증 사용에 대한 지침은 아래 표를 참조하십시오

### OAuth 2 새로 고침 코드

OAuth 2 새로 고침 코드는 임시 액세스 토큰 및 새로 고침 토큰을 생성하여 애플리케이션에 안전하게 액세스할 수 있도록 합니다. 액세스 토큰을 사용하면 다른 자격 증명을 제공할 필요 없이 리소스에 안전하게 액세스할 수 있으며, 새로 고침 토큰을 사용하면 액세스 토큰이 만료되면 새 액세스 토큰을 생성할 수 있습니다.

+++OAuth 2 새로 고침 코드의 보기 예

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `authSpec.name` | 지원되는 인증 유형의 이름을 표시합니다. | `oAuth2-refresh-code` |
| `authSpec.type` | 소스에서 지원하는 인증 유형을 정의합니다. | `oAuth2-refresh-code` |
| `authSpec.spec` | 인증의 스키마, 데이터 유형 및 속성에 대한 정보를 포함합니다. |
| `authSpec.spec.$schema` | 인증에 사용되는 스키마를 정의합니다. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 스키마의 데이터 유형을 정의합니다. | `object` |
| `authSpec.spec.properties` | 인증에 사용되는 자격 증명에 대한 정보를 포함합니다. |
| `authSpec.spec.properties.description` | 자격 증명에 대한 간단한 설명을 표시합니다. |
| `authSpec.spec.properties.type` | 자격 증명의 데이터 유형을 정의합니다. | `string` |
| `authSpec.spec.properties.clientId` | 응용 프로그램과 연결된 클라이언트 ID입니다. 클라이언트 ID는 액세스 토큰을 검색하기 위해 클라이언트 암호와 함께 사용됩니다. |
| `authSpec.spec.properties.clientSecret` | 응용 프로그램과 연결된 클라이언트 암호입니다. 클라이언트 암호는 액세스 토큰을 검색하기 위해 클라이언트 ID와 함께 사용됩니다. |
| `authSpec.spec.properties.accessToken` | 액세스 토큰은 애플리케이션에 대한 보안 액세스를 승인합니다. |
| `authSpec.spec.properties.refreshToken` | 새로 고침 토큰은 액세스 토큰이 만료될 때 새 액세스 토큰을 생성하는 데 사용됩니다. |
| `authSpec.spec.properties.expirationDate` | 액세스 토큰의 만료 날짜를 정의합니다. |
| `authSpec.spec.properties.refreshTokenUrl` | 새로 고침 토큰을 검색하는 데 사용되는 URL입니다. |
| `authSpec.spec.properties.accessTokenUrl` | 새로 고침 토큰을 검색하는 데 사용되는 URL입니다. |
| `authSpec.spec.properties.requestParameterOverride` | 인증 시 재정의할 자격 증명 매개 변수를 지정할 수 있습니다. |
| `authSpec.spec.required` | 인증에 필요한 자격 증명을 표시합니다. | `accessToken` |

{style="table-layout:auto"}

+++

### 기본 인증

기본 인증은 계정 사용자 이름과 계정 암호를 조합하여 애플리케이션에 액세스할 수 있는 인증 유형입니다.

+++ 기본 인증의 예 보기

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| 속성 | 설명 | 예 |
| --- | --- | --- |
| `authSpec.name` | 지원되는 인증 유형의 이름을 표시합니다. | `Basic Authentication` |
| `authSpec.type` | 소스에서 지원하는 인증 유형을 정의합니다. | `BasicAuthentication` |
| `authSpec.spec` | 인증의 스키마, 데이터 유형 및 속성에 대한 정보를 포함합니다. |
| `authSpec.spec.$schema` | 인증에 사용되는 스키마를 정의합니다. | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 스키마의 데이터 유형을 정의합니다. | `object` |
| `authSpec.spec.description` | 인증 유형과 관련된 추가 정보를 표시합니다. |
| `authSpec.spec.properties` | 인증에 사용되는 자격 증명에 대한 정보를 포함합니다. |
| `authSpec.spec.properties.username` | 응용 프로그램과 연결된 계정 사용자 이름입니다. |
| `authSpec.spec.properties.password` | 응용 프로그램과 연결된 계정 암호입니다. |
| `authSpec.spec.required` | Experience Platform에서 입력해야 할 필수 값으로 필요한 필드를 지정합니다. | `username` |

{style="table-layout:auto"}

+++

### API 키 인증 {#api-key-authentication}

API 키 인증은 요청에 API 키 및 기타 관련 인증 매개 변수를 제공하여 API에 액세스하는 보안 방법입니다. 특정 API 정보에 따라 API 키를 요청 헤더, 쿼리 매개 변수 또는 본문의 일부로 보낼 수 있습니다.

API 키 인증을 사용할 때 일반적으로 다음 매개 변수가 필요합니다.

| 매개변수 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `host` | 문자열 | 아니요 | 리소스 URL. |
| `authKey1` | 문자열 | 예 | API 액세스에 필요한 첫 번째 인증 키입니다. 일반적으로 요청 헤더 또는 쿼리 매개 변수에서 전송됩니다. |
| `authKey2` | 문자열 | 선택 사항입니다 | 두 번째 인증 키. 필요한 경우 이 키를 사용하여 요청의 유효성을 추가로 검사할 수 있습니다. |
| `authKeyN` | 문자열 | 선택 사항입니다 | 필요에 따라 사용할 수 있지만 API인 추가 인증 변수입니다. |

{style="table-layout:auto"}

+++API 키 인증 보기

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### 인증 비헤이비어

`restAttributes` 매개 변수를 사용하여 API 키를 요청에 포함하는 방법을 정의할 수 있습니다. 예를 들어 아래 예에서 `headerParamName` 특성은 `X-Auth-Key1`을(를) 헤더로 보내야 함을 나타냅니다.

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

각 인증 키(예: `authKey1`, `authKey2` 등)를 `restAttributes`과(와) 연결하여 요청으로 전송되는 방법을 지정할 수 있습니다.

`authKey1`에 `"headerParamName": "X-Auth-Key1"`이(가) 있는 경우. 즉, 요청 헤더에 `X-Auth-Key:{YOUR_AUTH_KEY1}`이(가) 포함되어야 합니다. 또한 키 이름과 `headerParamName`이(가) 반드시 같을 필요는 없습니다. 예:

* `authKey1`에 `headerParamName: X-Custom-Auth-Key`이(가) 있을 수 있습니다. 즉, 요청 헤더에서 `authKey1` 대신 `X-Custom-Auth-Key`을(를) 사용합니다.
* 반대로 `authKey1`은(는) `headerParamName: authKey1`을(를) 가질 수 있습니다. 즉, 요청 헤더 이름은 변경되지 않습니다.

**예제 API 형식**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## 인증 사양 예

다음은 [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) 원본을 사용하여 완료된 인증 사양의 예입니다.

+++예제 인증 사양 보기

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

+++

## 다음 단계

인증 사양을 채워 Experience Platform에 통합할 소스의 소스 사양을 계속 구성할 수 있습니다. 자세한 내용은 [소스 사양 구성](./sourcespec.md)에 대한 문서를 참조하십시오.
