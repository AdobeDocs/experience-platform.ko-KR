---
keywords: Experience Platform;home;popular topics;redshift;Redshift;Amazon Redshift;amazon redshift
solution: Experience Platform
title: Flow Service API를 사용하여 Amazon Redshift 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서는 Flow Service API를 사용하여 Experience Platform을 Amazon Redshift(이하 "Redshift"라 한다)에 연결하는 단계를 단계별로 안내합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---


# API를 사용하여 [!DNL Amazon Redshift] 커넥터 [!DNL Flow Service] 만들기

>[!NOTE]
>
>커넥터의 [!DNL Amazon Redshift] 베타입니다. 베타 [레이블이 지정된 커넥터 사용에 대한 자세한 내용은 소스 개요를](../../../../home.md#terms-and-conditions) 참조하십시오.

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 연결 단계 [!DNL Experience Platform] 를 [!DNL Amazon Redshift] 안내합니다(이하 &quot;[!DNL Redshift]&quot;라 함).

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 [!DNL Redshift] 사용하기 위해 연결하기 위해 알아야 할 추가 정보를 [!DNL Flow Service] 제공합니다.

### 필요한 자격 증명 수집

연결 [!DNL Flow Service] 을 하려면 [!DNL Redshift]다음 연결 속성을 제공해야 합니다.

| **자격 증명** | **설명** |
| -------------- | --------------- |
| `server` | 계정과 연결된 [!DNL Redshift] 서버입니다. |
| `username` | 계정과 연결된 사용자 [!DNL Redshift] 이름입니다. |
| `password` | 계정과 연결된 [!DNL Redshift] 암호입니다. |
| `database` | 액세스하는 [!DNL Redshift] 데이터베이스입니다. |

시작하는 방법에 대한 자세한 내용은 [이 Redshift 문서를 참조하십시오](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

에 속하는 리소스를 [!DNL Experience Platform]포함한 모든 리소스 [!DNL Flow Service]는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 사양 조회

연결을 만들려면 [!DNL Redshift] 연결 사양의 세트가 안에 있어야 합니다 [!DNL Redshift] [!DNL Flow Service]. 연결 [!DNL Platform] 의 첫 번째 단계는 이러한 사양 [!DNL Redshift] 을 가져오는 것입니다.

**API 형식**

사용 가능한 각 소스에는 인증 요구 사항과 같은 커넥터 속성을 설명하는 고유한 연결 사양이 있습니다. GET 요청을 수행하고 쿼리 매개 변수를 사용하여 [!DNL Redshift] 의 연결 사양을 조회할 수 있습니다.

쿼리 매개 변수 없이 GET 요청을 보내면 사용 가능한 모든 소스에 대한 연결 사양이 반환됩니다. 쿼리를 포함하여 특정 `property=name=="amazon-redshift"` 의 정보를 얻을 수 있습니다 [!DNL Redshift].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="amazon-redshift"
```

**요청**

다음 요청은 에 대한 연결 사양을 검색합니다 [!DNL Redshift].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="amazon-redshift"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 고유 식별자( [!DNL Redshift])를`id`비롯한 연결 사양을 반환합니다. 이 ID는 기본 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "items": [
        {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "name": "amazon-redshift",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication",
                    "type": "Basic_Authentication",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params",
                        "properties": {
                            "server": {
                                "type": "string",
                                "description": "IP address or host name of the Amazon Redshift server"
                            },
                            "username": {
                                "type": "string",
                                "description": "Name of user who has access to the database"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            },
                            "database": {
                                "type": "string",
                                "description": "Name of the Amazon Redshift database"
                            }
                        },
                        "required": [
                            "server",
                            "username",
                            "password",
                            "database"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## 기본 연결 만들기

기본 연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 [!DNL Redshift] 계정당 하나의 기본 연결만 필요합니다.

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
        "name": "amazon-redshift base connection",
        "description": "base connection for amazon-redshift,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "server": "{SERVER}",
                "database": "{DATABASE}",
                "password": "{PASSWORD}",
                "username": "{USERNAME}"
            }
        },
        "connectionSpec": {
            "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| ------------- | --------------- |
| `auth.params.server` | 사용자 [!DNL Redshift] 서버 |
| `auth.params.database` | 계정과 연결된 [!DNL Redshift] 데이터베이스입니다. |
| `auth.params.password` | 계정과 연결된 [!DNL Redshift] 암호입니다. |
| `auth.params.username` | 계정과 연결된 사용자 [!DNL Redshift] 이름입니다. |
| `connectionSpec.id` | 이전 단계 `id` 에서 검색된 [!DNL Redshift] 계정의 연결 사양입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 [!DNL Redshift] 기본 연결을 만들고 연결 [!DNL Flow Service] 의 고유 ID 값을 얻게 되었습니다. Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템을 [탐색하는 방법을 배울 때 다음 자습서에서 이 기본 연결 ID를 사용할 수 있습니다](../../explore/database-nosql.md).
