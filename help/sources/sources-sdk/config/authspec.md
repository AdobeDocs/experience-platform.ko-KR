---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 셀프 서비스 소스(배치 SDK)에 대한 인증 사양 구성
topic-legacy: overview
description: 이 문서에서는 셀프 서비스 소스(배치 SDK)를 사용하기 위해 준비해야 하는 구성에 대한 개요를 제공합니다.
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 셀프 서비스 소스(배치 SDK)에 대한 인증 사양 구성

인증 사양은 Adobe Experience Platform 사용자가 소스에 연결할 수 있는 방법을 정의합니다.

다음 `authSpec` 배열에 소스를 Platform에 연결하는 데 필요한 인증 매개 변수에 대한 정보가 포함되어 있습니다. 지정된 모든 소스는 다양한 유형의 인증을 지원할 수 있습니다.

## 인증 사양

셀프 서비스 소스(배치 SDK)는 OAuth 2 새로 고침 코드 및 기본 인증을 지원합니다. OAuth 2 새로 고침 코드 및 기본 인증 사용에 대한 지침은 아래 표를 참조하십시오

### OAuth 2 새로 고침 코드

OAuth 2 새로 고침 코드는 임시 액세스 토큰 및 새로 고침 토큰을 생성하여 응용 프로그램에 안전하게 액세스할 수 있도록 합니다. 액세스 토큰을 사용하면 다른 자격 증명을 제공하지 않고도 리소스에 안전하게 액세스할 수 있으며, 새로 고침 토큰을 사용하면 액세스 토큰이 만료되면 새 액세스 토큰을 생성할 수 있습니다.

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
      "host",
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
| `authSpec.spec.properties.clientId` | 응용 프로그램과 연결된 클라이언트 ID입니다. 클라이언트 ID가 클라이언트 암호와 함께 사용되어 액세스 토큰을 검색합니다. |
| `authSpec.spec.properties.clientSecret` | 응용 프로그램과 연결된 클라이언트 암호입니다. 클라이언트 암호는 클라이언트 ID와 함께 사용하여 액세스 토큰을 검색합니다. |
| `authSpec.spec.properties.accessToken` | 액세스 토큰은 애플리케이션에 대한 보안 액세스를 허용합니다. |
| `authSpec.spec.properties.refreshToken` | 새로 고침 토큰은 액세스 토큰이 만료되면 새 액세스 토큰을 생성하는 데 사용됩니다. |
| `authSpec.spec.properties.expirationDate` | 액세스 토큰의 만료 날짜를 정의합니다. |
| `authSpec.spec.properties.refreshTokenUrl` | 새로 고침 토큰을 검색하는 데 사용되는 URL입니다. |
| `authSpec.spec.properties.accessTokenUrl` | 새로 고침 토큰을 검색하는 데 사용되는 URL입니다. |
| `authSpec.spec.properties.requestParameterOverride` | 인증 시 재정의할 자격 증명 매개 변수를 지정할 수 있습니다. |
| `authSpec.spec.required` | 인증하는 데 필요한 자격 증명을 표시합니다. | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### 기본 인증

기본 인증은 응용 프로그램의 호스트 URL, 계정 사용자 이름 및 계정 암호를 조합하여 응용 프로그램에 액세스할 수 있는 인증 유형입니다.

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource url host path"
      },
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
      "host",
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
| `authSpec.spec.description` | 인증 유형에 대한 추가 정보를 표시합니다. |
| `authSpec.spec.properties` | 인증에 사용되는 자격 증명에 대한 정보를 포함합니다. |
| `authSpec.spec.properties.host` | 애플리케이션의 호스트 URL입니다. |
| `authSpec.spec.properties.username` | 애플리케이션과 연관된 계정 사용자 이름. |
| `authSpec.spec.properties.password` | 응용 프로그램과 연결된 계정 암호입니다. |
| `authSpec.spec.required` | Platform에 입력해야 하는 필수 값으로 필요한 필드를 지정합니다. | `host` |

{style=&quot;table-layout:auto&quot;}

## 인증 사양 예

다음은 [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) 소스.

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
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
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
          "host",
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
          "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
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
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
```

## 다음 단계

인증 사양이 채워지면 Platform에 통합할 소스에 대한 소스 사양을 구성할 수 있습니다. 다음 문서를 참조하십시오 [소스 사양 구성](./sourcespec.md) 추가 정보.
