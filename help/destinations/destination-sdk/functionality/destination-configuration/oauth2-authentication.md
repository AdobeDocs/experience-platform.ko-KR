---
description: 이 페이지에서는 Destination SDK에서 지원하는 다양한 OAuth 2 인증 흐름에 대해 설명하고 대상에 대한 OAuth 2 인증을 설정하는 지침을 제공합니다.
title: OAuth 2 인증
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 4%

---

# OAuth 2 인증

Destination SDK은 대상에 대한 몇 가지 인증 방법을 지원합니다. 이 중에서 다음을 사용하여 대상을 인증할 수 있습니다 [OAuth 2 인증 프레임워크](https://tools.ietf.org/html/rfc6749).

이 페이지에서는 Destination SDK에서 지원하는 다양한 OAuth 2 인증 흐름에 대해 설명하고 대상에 대한 OAuth 2 인증을 설정하는 지침을 제공합니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 아니요 |

## 대상 구성에 OAuth 2 인증 세부 사항을 추가하는 방법 {#how-to-setup}

### 시스템의 사전 요구 사항 {#prerequisites}

첫 번째 단계로, 시스템에서 Adobe Experience Platform용 앱을 만들거나 시스템에 Experience Platform을 등록해야 합니다. 목표는 대상에 대한 Experience Platform을 인증하는 데 필요한 클라이언트 ID와 클라이언트 암호를 생성하는 것입니다. 시스템에서 이 구성의 일부로 아래 목록에서 가져올 수 있는 Adobe Experience Platform OAuth 2 리디렉션/콜백 URL이 필요합니다.

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>시스템에서 Adobe Experience Platform에 대한 리디렉션/콜백 URL을 등록하는 단계는 [인증 코드가 있는 OAuth 2](oauth2-authentication.md#authorization-code) 부여 유형. 지원되는 다른 두 가지 권한 부여 유형(암호 및 클라이언트 자격 증명)에 대해 이 단계를 건너뛸 수 있습니다.

이 단계를 마치면 다음을 수행해야 합니다.
* 클라이언트 ID;
* 클라이언트 암호
* Adobe의 콜백 URL(인증 코드 부여용).

### Destination SDK에서 수행할 작업 {#to-do-in-destination-sdk}

Experience Platform에서 대상에 대한 OAuth 2 인증을 설정하려면 OAuth 2 세부 사항을 [대상 구성](../../authoring-api/destination-configuration/create-destination-configuration.md)아래에 있는 `customerAuthenticationConfigurations` 매개 변수. 자세한 내용은 [고객 인증](../../functionality/destination-configuration/customer-authentication.md) 자세한 예 OAuth 2 인증 부여 유형에 따라 구성 템플릿에 추가해야 하는 필드에 대한 특정 지침은 이 페이지에서 더 아래에 나와 있습니다.

## 지원되는 OAuth 2 부여 유형 {#oauth2-grant-types}

Experience Platform은 아래 표에서 세 가지 OAuth 2 부여 유형을 지원합니다. 사용자 지정 OAuth 2 설정이 있는 경우 Adobe은 통합에서 사용자 지정 필드의 도움을 받아 이 설정을 지원할 수 있습니다. 자세한 내용은 각 부여 유형에 대한 섹션을 참조하십시오.

>[!IMPORTANT]
>
>* 아래 섹션에 설명된 대로 입력 매개 변수를 제공합니다. Adobe 내부 시스템은 플랫폼의 인증 시스템에 연결하고 출력 매개 변수를 가져오므로 사용자를 인증하고 대상에 대한 인증을 유지 관리하는 데 사용됩니다.
>* 테이블에서 굵게 강조 표시된 입력 매개 변수는 OAuth 2 인증 흐름의 필수 매개 변수입니다. 다른 매개 변수는 선택 사항입니다. 여기에 표시되지 않지만 섹션에서 길이에 설명된 다른 사용자 지정 입력 매개 변수가 있습니다 [OAuth 2 구성 사용자 지정](#customize-configuration) 및 [액세스 토큰 새로 고침](#access-token-refresh).


| OAuth 2 그랜트 | 입력 | 출력 |
|---------|----------|---------|
| 인증 코드 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>범위</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| 암호 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>범위</li><li><b>accessTokenUrl</b></li><li><b>사용자 이름</b></li><li><b>암호</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| 클라이언트 자격 증명 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>범위</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

위의 표에는 표준 OAuth 2 흐름에 사용되는 필드가 나와 있습니다. 이러한 표준 필드 외에도 다양한 파트너 통합에서 추가 입력 및 출력이 필요할 수 있습니다. Adobe은 만료된 액세스 토큰과 같은 잘못된 출력을 자동으로 재생성하는 메커니즘을 지원하면서 위의 표준 필드 패턴으로 변형을 처리할 수 있는 Destination SDK을 위한 유연한 OAuth 2 인증/인증 프레임워크를 설계했습니다.

모든 경우에 출력에는 Experience Platform이 대상에 대한 인증을 인증하고 유지 관리하는 데 사용하는 액세스 토큰이 포함됩니다.

Adobe이 OAuth 2 인증을 위해 디자인한 시스템:
* 추가 데이터 필드, 비표준 API 호출 등과 같은 모든 변형을 처리하는 동안 세 가지 OAuth 2 그랜트를 모두 지원합니다.
* 다양한 라이프타임 값, 90일, 30분 또는 지정한 다른 라이프타임 값과 함께 액세스 토큰을 지원합니다.
* 는 새로 고침 토큰이 있거나 없는 OAuth 2 인증 흐름을 지원합니다.

## 인증 코드가 있는 OAuth 2 {#authorization-code}

대상이 표준 OAuth 2.0 인증 코드 흐름을 지원하는 경우( [RFC 표준 사양](https://tools.ietf.org/html/rfc6749#section-4.1)) 또는 그 변형에 대해서는 아래의 필수 및 선택적 필드를 참조하십시오.

| OAuth 2 그랜트 | 입력 | 출력 |
|---------|----------|---------|
| 인증 코드 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>범위</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

대상에 대해 이 인증 방법을 설정하려면 다음 줄을 구성 시 추가합니다. [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `authType` | 문자열 | &quot;OAUTH2&quot;를 사용합니다. |
| `grant` | 문자열 | &quot;OAUTH2_AUTHORIZATION_CODE&quot;를 사용합니다. |
| `accessTokenUrl` | 문자열 | 액세스 토큰을 발급하고, 원할 경우 토큰을 새로 고치는 URL입니다. |
| `authorizationUrl` | 문자열 | 응용 프로그램에 로그인할 사용자를 리디렉션하는 인증 서버의 URL입니다. |
| `refreshTokenUrl` | 문자열 | *선택 사항입니다.* 사용자 측의 URL로, 토큰을 새로 고침하는 문제가 발생합니다. 종종 `refreshTokenUrl` 와(과) 같습니다 `accessTokenUrl`. |
| `clientId` | 문자열 | 시스템이 Adobe Experience Platform에 할당하는 클라이언트 ID입니다. |
| `clientSecret` | 문자열 | 시스템이 Adobe Experience Platform에 할당하는 클라이언트 암호입니다. |
| `scope` | 문자열 목록 | *선택 사항입니다*. Experience Platform이 리소스에 대해 수행할 수 있는 액세스 토큰의 범위를 설정합니다. 예: &quot;읽기, 쓰기&quot; |

{style="table-layout:auto"}

## 암호 부여가 있는 OAuth 2

OAuth 2 암호 부여의 경우 [RFC 표준 사양](https://tools.ietf.org/html/rfc6749#section-4.3)), Experience Platform을 사용하려면 사용자의 사용자 이름과 암호가 필요합니다. 인증 플로우에서 Experience Platform은 액세스 토큰 및 선택적으로 새로 고침 토큰에 대해 이러한 자격 증명을 교환합니다.
Adobe은 아래의 표준 입력을 사용하여 대상 구성을 단순화하고 값을 재정의할 수 있습니다.

| OAuth 2 그랜트 | 입력 | 출력 |
|---------|----------|---------|
| 암호 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>범위</li><li><b>accessTokenUrl</b></li><li><b>사용자 이름</b></li><li><b>암호</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> 에 매개 변수를 추가할 필요는 없습니다 `username` 및 `password` 아래에 나열된 상태로 남아 있습니다. 추가할 때 `"grant": "OAUTH2_PASSWORD"` 대상 구성에서 시스템은 대상을 인증할 때 사용자에게 Experience Platform UI에 사용자 이름과 암호를 제공하도록 요청합니다.

대상에 대해 이 인증 방법을 설정하려면 다음 줄을 구성 시 추가합니다. [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `authType` | 문자열 | &quot;OAUTH2&quot;를 사용합니다. |
| `grant` | 문자열 | &quot;OAUTH2_PASSWORD&quot;를 사용합니다. |
| `accessTokenUrl` | 문자열 | 액세스 토큰을 발급하고, 원할 경우 토큰을 새로 고치는 URL입니다. |
| `clientId` | 문자열 | 시스템이 Adobe Experience Platform에 할당하는 클라이언트 ID입니다. |
| `clientSecret` | 문자열 | 시스템이 Adobe Experience Platform에 할당하는 클라이언트 암호입니다. |
| `scope` | 문자열 목록 | *선택 사항입니다*. Experience Platform이 리소스에 대해 수행할 수 있는 액세스 토큰의 범위를 설정합니다. 예: &quot;읽기, 쓰기&quot; |

{style="table-layout:auto"}

## 클라이언트 자격 증명 부여가 있는 OAuth 2

OAuth 2 클라이언트 자격 증명을 구성할 수 있습니다( [RFC 표준 사양](https://tools.ietf.org/html/rfc6749#section-4.4)) 대상. 아래에 나열된 표준 입력 및 출력을 지원합니다. 값을 사용자 지정할 수 있습니다. 자세한 내용은 [OAuth 2 구성 사용자 지정](#customize-configuration) 자세한 내용

| OAuth 2 그랜트 | 입력 | 출력 |
|---------|----------|---------|
| 클라이언트 자격 증명 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>범위</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

대상에 대해 이 인증 방법을 설정하려면 다음 줄을 구성 시 추가합니다. [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `authType` | 문자열 | &quot;OAUTH2&quot;를 사용합니다. |
| `grant` | 문자열 | &quot;OAUTH2_CLIENT_CREDENTIALS&quot;를 사용합니다. |
| `accessTokenUrl` | 문자열 | 액세스 토큰 및 선택적 새로 고침 토큰을 발급하는 인증 서버의 URL입니다. |
| `refreshTokenUrl` | 문자열 | *선택 사항입니다.* 사용자 측의 URL로, 토큰을 새로 고침하는 문제가 발생합니다. 종종 `refreshTokenUrl` 와(과) 같습니다 `accessTokenUrl`. |
| `clientId` | 문자열 | 시스템이 Adobe Experience Platform에 할당하는 클라이언트 ID입니다. |
| `clientSecret` | 문자열 | 시스템이 Adobe Experience Platform에 할당하는 클라이언트 암호입니다. |
| `scope` | 문자열 목록 | *선택 사항입니다*. Experience Platform이 리소스에 대해 수행할 수 있는 액세스 토큰의 범위를 설정합니다. 예: &quot;읽기, 쓰기&quot; |

{style="table-layout:auto"}

## OAuth 2 구성 사용자 지정 {#customize-configuration}

위의 섹션에 설명된 구성은 표준 OAuth 2 부여에 대해 설명합니다. 그러나 Adobe으로 디자인된 시스템은 유연성을 제공하므로 OAuth 2 부여의 모든 변형에 사용자 지정 매개 변수를 사용할 수 있습니다. 표준 OAuth 2 설정을 사용자 지정하려면 `authenticationDataFields` 매개 변수에 채울 수 있습니다.

### 예제 1: 사용 `authenticationDataFields` 인증 응답에서 오는 정보를 캡처하려면 {#example-1}

이 예제에서 대상 플랫폼에는 특정 시간 후에 만료되는 새로 고침 토큰이 있습니다. 이 경우 파트너는 `refreshTokenExpiration` 사용자 지정 필드를 사용하여 `refresh_token_expires_in` API 응답의 필드.

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### 예제 2: 사용 `authenticationDataFields` 특별 새로 고침 토큰을 제공하려면 {#example-2}

이 예에서는 파트너가 대상을 설정하여 특수 새로 고침 토큰을 제공합니다. 또한 액세스 토큰에 대한 만료 날짜가 API 응답으로 반환되지 않으므로 이 경우 3600초를 하드코딩할 수 있습니다.

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### 예제 3: 사용자는 대상을 구성할 때 클라이언트 ID 및 클라이언트 암호를 입력합니다 {#example-3}

이 예에서는 섹션에 표시된 대로 글로벌 클라이언트 ID 및 클라이언트 암호를 만드는 대신 [시스템의 사전 요구 사항](#prerequisites)를 지정하는 경우 고객이 클라이언트 ID, 클라이언트 암호 및 계정 ID(고객이 대상에 로그인하는 데 사용하는 ID)를 입력해야 합니다

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



에서 다음 매개 변수를 사용할 수 있습니다 `authenticationDataFields` oaUth 2 구성을 사용자 지정하는 방법:

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `authenticationDataFields.name` | 문자열 | 사용자 지정 필드의 이름입니다. |
| `authenticationDataFields.title` | 문자열 | 사용자 지정 필드에 제공할 수 있는 제목입니다. |
| `authenticationDataFields.description` | 문자열 | 설정한 사용자 지정 데이터 필드에 대한 설명입니다. |
| `authenticationDataFields.type` | 문자열 | 사용자 지정 데이터 필드의 유형을 정의합니다. <br> 허용되는 값: `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | 부울 | 인증 흐름에서 사용자 지정 데이터 필드가 필요한지 여부를 지정합니다. |
| `authenticationDataFields.format` | 문자열 | 선택 시 `"format":"password"`, Adobe 는 인증 데이터 필드의 값을 암호화합니다. 와 함께 사용하는 경우 `"fieldType": "CUSTOMER"`로 지정하는 경우 사용자가 필드에 입력할 때 UI의 입력도 숨깁니다. |
| `authenticationDataFields.fieldType` | 문자열 | Experience Platform에서 대상을 설정할 때 입력이 파트너(사용자)에서 발생하는지 아니면 사용자에서 발생하는지를 나타냅니다. |
| `authenticationDataFields.value` | 문자열. 부울. 정수 | 사용자 지정 데이터 필드의 값입니다. 값은 선택한 유형과 일치합니다. `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | 문자열 | 참조하는 API 응답 경로의 필드를 나타냅니다. |

{style="table-layout:auto"}

## 액세스 토큰 새로 고침 {#access-token-refresh}

Adobe은 사용자가 플랫폼에 다시 로그인하지 않고도 만료된 액세스 토큰을 새로 고치는 시스템을 설계했습니다. 시스템은 대상에 대한 활성화를 고객에 대해 계속 원활하게 수행할 수 있도록 새 토큰을 생성할 수 있습니다.

액세스 토큰 새로 고침을 설정하려면 Adobe이 새로 고침 토큰을 사용하여 새 액세스 토큰을 가져올 수 있도록 하는 템플릿 지정 HTTP 요청을 구성해야 할 수 있습니다. 액세스 토큰이 만료되면 Adobe은 사용자가 제공한 템플릿 요청을 가져와 제공한 매개 변수를 추가합니다. 를 사용하십시오 `accessTokenRequest` 액세스 토큰 새로 고침 메커니즘을 구성하기 위한 매개 변수입니다.


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

에서 다음 매개 변수를 사용할 수 있습니다 `accessTokenRequest` 토큰 새로 고침 프로세스를 사용자 정의하려면

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | 문자열 | `URL_BASED` 사용. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | 문자열 | <ul><li>사용 `PEBBLE_V1` 의 값에 템플릿을 사용하는 경우 `accessTokenRequest.urlBasedDestination.url.value`.</li><li> 사용 `NONE` 필드의 값이 `accessTokenRequest.urlBasedDestination.url.value` 는 상수입니다. </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | 문자열 | Experience Platform이 액세스 토큰을 요청하는 URL입니다. |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | 문자열 | <ul><li>사용 `PEBBLE_V1` 템플릿을 사용하는 경우 `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> 사용 `NONE` 필드의 값이 `accessTokenRequest.httpTemplate.requestBody.value` 는 상수입니다. </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | 문자열 | 템플릿 언어를 사용하여 액세스 토큰 끝점에 대한 HTTP 요청의 필드를 사용자 지정합니다. 템플릿을 사용하여 필드를 사용자 지정하는 방법에 대한 자세한 내용은 [템플릿 규칙](#templating-conventions) 섹션을 참조하십시오. |
| `accessTokenRequest.httpTemplate.httpMethod` | 문자열 | 액세스 토큰 끝점을 호출하는 데 사용되는 HTTP 메서드를 지정합니다. 대부분의 경우 이 값은 `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | 문자열 | 액세스 토큰 끝점에 대한 HTTP 호출의 콘텐츠 유형을 지정합니다. <br> 예: `application/x-www-form-urlencoded` 또는 `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | 문자열 | 액세스 토큰 끝점에 대한 HTTP 호출에 헤더를 추가해야 하는지를 지정합니다. |
| `accessTokenRequest.responseFields.templatingStrategy` | 문자열 | <ul><li>사용 `PEBBLE_V1` 템플릿을 사용하는 경우 `accessTokenRequest.responseFields.value`.</li><li> 사용 `NONE` 필드의 값이 `accessTokenRequest.responseFields.value` 는 상수입니다. </li></li> |
| `accessTokenRequest.responseFields.value` | 문자열 | 템플릿 언어를 사용하여 액세스 토큰 끝점의 HTTP 응답에 있는 필드에 액세스합니다. 템플릿을 사용하여 필드를 사용자 지정하는 방법에 대한 자세한 내용은 [템플릿 규칙](#templating-conventions) 섹션을 참조하십시오. |
| `accessTokenRequest.validations.name` | 문자열 | 이 유효성 검사에 대해 제공한 이름을 나타냅니다. |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | 문자열 | <ul><li>사용 `PEBBLE_V1` 템플릿을 사용하는 경우 `accessTokenRequest.validations.actualValue.value`.</li><li> 사용 `NONE` 필드의 값이 `accessTokenRequest.validations.actualValue.value` 는 상수입니다. </li></li> |
| `accessTokenRequest.validations.actualValue.value` | 문자열 | 템플릿 언어를 사용하여 HTTP 응답의 필드에 액세스합니다. 템플릿을 사용하여 필드를 사용자 지정하는 방법에 대한 자세한 내용은 [템플릿 규칙](#templating-conventions) 섹션을 참조하십시오. |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | 문자열 | <ul><li>사용 `PEBBLE_V1` 템플릿을 사용하는 경우 `accessTokenRequest.validations.expectedValue.value`.</li><li> 사용 `NONE` 필드의 값이 `accessTokenRequest.validations.expectedValue.value` 는 상수입니다. </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | 문자열 | 템플릿 언어를 사용하여 HTTP 응답의 필드에 액세스합니다. 템플릿을 사용하여 필드를 사용자 지정하는 방법에 대한 자세한 내용은 [템플릿 규칙](#templating-conventions) 섹션을 참조하십시오. |

{style="table-layout:auto"}

## 템플릿 규칙 {#templating-conventions}

인증 사용자 지정에 따라 이전 섹션에 표시된 대로 인증 응답의 데이터 필드에 액세스해야 할 수 있습니다. 이를 수행하려면 다음을 숙지하십시오 [자갈 템플릿 언어](https://pebbletemplates.io/) Adobe에서 사용되고 아래 템플릿 규칙을 참조하여 OAuth 2 구현을 사용자 지정합니다.


| 접두사 | 설명 | 예 |
|---------|----------|---------|
| authData | 파트너 또는 고객 데이터 필드의 값에 액세스합니다. | ``{{ authData.accessToken }}`` |
| response.body | HTTP 응답 본문 | ``{{ response.body.access_token }}`` |
| response.status | HTTP 응답 상태 | ``{{ response.status }}`` |
| response.headers | HTTP 응답 헤더 | ``{{ response.headers.server[0] }}`` |
| userContext | 현재 인증 시도에 대한 정보 액세스 | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 Adobe Experience Platform에서 지원하는 OAuth 2 인증 패턴을 이해하고 OAuth 2 인증 지원을 사용하여 대상을 구성하는 방법을 알아봅니다. 다음으로, Destination SDK을 사용하여 OAuth 2 지원 대상을 설정할 수 있습니다. 읽기 [Destination SDK을 사용하여 대상을 구성합니다](../../guides/configure-destination-instructions.md) 을 참조하십시오.
