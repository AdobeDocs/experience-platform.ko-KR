---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API 파섹
topic: overview
translation-type: tm+mt
source-git-commit: c5d0372f52b0c05746a92a18442fab158b7b99fe

---


# Flow Service API 파섹

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 Flow Service API를 사용하여 Experience Platform을 Salesforce Service Cloud(이하 &quot;SSC&quot;라 한다)에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 SSC에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

Flow Service가 SSC와 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `username` | 사용자 계정의 사용자 이름입니다. |
| `password` | 사용자 계정의 암호입니다. |
| `securityToken` | 사용자 계정의 보안 토큰입니다. |

시작하는 방법에 대한 자세한 내용은 [이 Salesforce Service Cloud 문서를](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)참조하십시오.

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

SSC 연결을 만들려면 흐름 서비스 내에 SSC 연결 사양 세트가 있어야 합니다. 플랫폼에 SSC를 연결하는 첫 번째 단계는 이러한 사양을 가져오는 것입니다.

**API 형식**

사용 가능한 각 소스에는 인증 요구 사항과 같은 커넥터 속성을 설명하는 고유한 연결 사양 세트가 있습니다. GET 요청을 `/connectionSpecs` 끝점으로 보내면 사용 가능한 모든 소스에 대한 연결 사양이 반환됩니다. SSC에 대한 정보를 `property=name=="salesforce-service-cloud"` 얻기 위해 쿼리를 포함할 수도 있습니다.

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="salesforce-service-cloud"
```

**요청**

다음 요청은 SSC에 대한 연결 사양을 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="mysql"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 SSC에 대한 연결 사양을 반환합니다. 이 ID는 기본 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "items": [
        {
            "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
            "name": "salesforce-service-cloud",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "BasicAuthentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "environmentUrl": {
                                "type": "string",
                                "description": "URL of the source instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "securityToken": {
                                "type": "string",
                                "description": "Security token for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "securityToken"
                        ]
                    }
                }
            ],
        }
    ]
}
```

## 기본 연결 만들기

기본 연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져오는 데 사용할 수 있으므로 SSC 계정당 하나의 기본 연결만 필요합니다.

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
        "name": "Base connection for salesforce service cloud",
        "description": "Base connection for salesforce service cloud",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
            "version": "1.0"
        }
    }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.username` | SSC 계정과 연결된 사용자 이름입니다. |
| `auth.params.password` | SSC 계정과 연결된 암호입니다. |
| `auth.params.securityToken` | SSC 계정과 연결된 보안 토큰입니다. |
| `connectionSpec.id` | 이전 단계에서 검색한 SSC `id` 계정의 연결 사양 |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 이 ID는 다음 자습서에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 다음 단계

이 자습서를 따라 Flow Service API를 사용하여 SSC 기본 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서 Flow Service API를 사용하여 고객 성공 시스템을 [탐색하는 방법을 배울 때 이 기본 연결 ID를 사용할 수 있습니다](../../explore/customer-success.md).
