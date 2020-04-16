---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 HubSpot 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 7aa6f85308bacb275bd6f3234d03530a621c1c02

---


# Flow Service API를 사용하여 HubSpot 커넥터 만들기

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 Flow Service API를 사용하여 Experience Platform을 HubSpot에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 HubSpot에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

Flow Service가 HubSpot에 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `clientId` | HubSpot 응용 프로그램과 연결된 클라이언트 ID입니다. |
| `clientSecret` | HubSpot 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `accessToken` | 처음에 OAuth 통합을 인증할 때 얻은 액세스 토큰입니다. |
| `refreshToken` | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰입니다. |

시작하는 방법에 대한 자세한 내용은 이 HubSpot [문서를](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../../../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속하는 리소스를 비롯하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 사양 조회

HubSpot 연결을 만들려면 Flow Service 내에 HubSpot 연결 사양 세트가 있어야 합니다. Platform과 HubSpot를 연결하는 첫 번째 단계는 이러한 사양을 가져오는 것입니다.

**API 형식**

사용 가능한 각 소스에는 인증 요구 사항과 같은 커넥터 속성을 설명하는 고유한 연결 사양 세트가 있습니다. GET 요청을 `/connectionSpecs` 끝점으로 보내면 사용 가능한 모든 소스에 대한 연결 사양이 반환됩니다. 또한 쿼리를 포함하여 HubSpot에 대한 정보를 얻을 `property=name=="hubspot"` 수도 있습니다.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="hubspot"
```

**요청**

다음 요청은 HubSpot에 대한 연결 사양을 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="hubspot"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 고유한 식별자(`id`)를 포함하여 HubSpot에 대한 연결 사양을 반환합니다. API에 대한 연결을 만들려면 다음 단계에서 이 ID가 필요합니다.

```json
{
    "items": [
        {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "name": "hubspot",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to HubSpot",
                        "properties": {
                            "clientId": {
                                "type": "string",
                                "description": "The client ID associated with your HubSpot application."
                            },
                            "clientSecret": {
                                "type": "string",
                                "description": "The client secret associated with your HubSpot application.",
                                "format": "password"
                            },
                            "accessToken": {
                                "type": "string",
                                "description": "The access token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            },
                            "refreshToken": {
                                "type": "string",
                                "description": "The refresh token obtained when initially authenticating your OAuth integration.",
                                "format": "password"
                            }
                        },
                        "required": [
                            "clientId",
                            "clientSecret",
                            "accessToken",
                            "refreshToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## API에 대한 연결 만들기

API에 대한 연결은 소스를 지정하며 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져오는 데 사용할 수 있으므로 API에 대한 연결은 HubSpot 계정당 하나만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for hubspot",
        "description": "connection for hubspot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.clientId` | HubSpot 응용 프로그램과 연결된 클라이언트 ID입니다. |
| `auth.params.clientSecret` | HubSpot 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `auth.params.accessToken` | 처음에 OAuth 통합을 인증할 때 얻은 액세스 토큰입니다. |
| `auth.params.refreshToken` | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 API에 대해 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "2eb9c78b-e8b8-4400-b9c7-8be8b86400b2",
    "etag": "\"05026cf5-0000-0200-0000-5e4c42920000\""
}
```

이 자습서를 따라 Flow Service API를 사용하여 HubSpot 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서 Flow Service API를 사용하여 CRM 시스템을 [탐색하는 방법을 배울 때 이 연결 ID를 사용할 수 있습니다](../../explore/crm.md).