---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Flow Service API를 사용하여 Microsoft Dynamics 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 플랫폼을 Microsoft Dynamics(이하 "Dynamics") 계정에 연결하여 CRM 데이터를 수집하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: d332226541685108b58d88096146ed6048606774
workflow-type: tm+mt
source-wordcount: '703'
ht-degree: 1%

---


# API를 [!DNL Microsoft Dynamics] 사용하여 커넥터 [!DNL Flow Service] 만들기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집된 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 CRM 데이터 [!DNL Platform] 를 수집하기 위한 계정 [!DNL Microsoft Dynamics] (이하 &quot;Dynamics&quot;)에 연결하는 단계를 안내합니다.

에서 사용자 인터페이스를 사용하려는 경우 [!DNL Experience Platform]Dynamics 소스 커넥터 UI 자습서 [](../../../ui/create/crm/dynamics.md) 는 유사한 작업을 수행하기 위한 단계별 지침을 제공합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md):e[!DNL xperience Platform] 는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 사용하여 Dynamics 계정에 성공적으로 연결하기 위해 알아야 할 추가 정보 [!DNL Platform] 를 [!DNL Flow Service] 제공합니다.

### 필요한 자격 증명 수집

연결 [!DNL Flow Service] 을 [!DNL Dynamics]하려면 다음 연결 속성에 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUri` | 인스턴스의 서비스 URL입니다 [!DNL Dynamics] . |
| `username` | 사용자 계정의 사용자 [!DNL Dynamics] 이름입니다. |
| `password` | 계정 [!DNL Dynamics] 암호 |

시작하는 방법에 대한 자세한 내용은 [이 Dynamics 문서를 참조하십시오](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

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

계정 [!DNL Platform] 에 [!DNL Dynamics] 연결하려면 연결 사양이 있는지 확인해야 합니다 [!DNL Dynamics]. 연결 사양이 없으면 연결할 수 없습니다.

사용 가능한 각 소스에는 인증 요구 사항과 같은 커넥터 속성을 설명하는 고유한 연결 사양이 있습니다. GET 요청을 수행하고 쿼리 매개 변수를 사용하여 [!DNL Dynamics] 의 연결 사양을 조회할 수 있습니다.

**API 형식**

쿼리 매개 변수 없이 GET 요청을 보내면 사용 가능한 모든 소스에 대한 연결 사양이 반환됩니다. 쿼리를 포함하여 특정 `property=name=="dynamics-online"` 의 정보를 얻을 수 있습니다 [!DNL Dynamics].

```http
GET /connectionSpecs
GET /connectionSpecs?property=name=="dynamics-online"
```

**요청**

다음 요청은 에 대한 연결 사양을 검색합니다 [!DNL Dynamics].

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="dynamics-online"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 고유 식별자( [!DNL Dynamics])를`id`비롯한 연결 사양을 반환합니다. 이 ID는 기본 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "items": [
        {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "name": "dynamics-online",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "authSpec": [
                {
                    "name": "Basic Authentication for Dynamics-Online",
                    "settings": {
                        "authenticationType": "Office365",
                        "deploymentType": "Online"
                    },
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "type": "object",
                        "description": "defines auth params required for connecting to dynamics-online",
                        "properties": {
                            "serviceUri": {
                                "type": "string",
                                "description": "The service URL of your Dynamics instance"
                            },
                            "username": {
                                "type": "string",
                                "description": "User name for the user account"
                            },
                            "password": {
                                "type": "string",
                                "description": "Password for the user account",
                                "format": "password"
                            }
                        },
                        "required": [
                            "username",
                            "password",
                            "serviceUri"
                        ]
                    }
                }
            ]
        }
    ]
}
```

## API에 대한 연결 만들기

API에 대한 연결은 소스를 지정하며 해당 소스에 대한 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있으므로 API에 대한 연결은 [!DNL Dynamics] 계정당 하나만 필요합니다.

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
        "name": "Dynamics Base Connection",
        "description": "Base connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.serviceUri` | 인스턴스와 연결된 서비스 URI입니다 [!DNL Dynamics] . |
| `auth.params.username` | 계정과 연결된 사용자 [!DNL Dynamics] 이름입니다. |
| `auth.params.password` | 계정과 연결된 [!DNL Dynamics] 암호입니다. |
| `connectionSpec.id` | 이전 단계 `id` 에서 검색된 [!DNL Dynamics] 계정의 연결 사양입니다. |

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`)가 포함됩니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 다음 단계

이 튜토리얼을 따라 API를 사용하여 계정에 대한 연결을 [!DNL Dynamics] 생성했으며 응답 본문의 일부로 고유한 ID를 획득했습니다. 다음 자습서에서는 Flow Service API를 사용하여 CRM 시스템을 [탐색하는 방법을 학습하면서 이 연결 ID를 사용할 수 있습니다](../../explore/crm.md).