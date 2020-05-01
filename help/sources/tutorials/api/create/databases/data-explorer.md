---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Azure 데이터 탐색기 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: c4162d88a688ce2028de08b63e7b7eab954a0e29

---


# 흐름 서비스 API를 사용하여 Azure 데이터 탐색기 커넥터 만들기

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 Flow Service API를 사용하여 Azure 데이터 탐색기(이하 &quot;데이터 탐색기&quot;라 함)를 경험 플랫폼에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있으며, 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): 경험 플랫폼은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 데이터 탐색기에 성공적으로 연결할 수 있도록 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

Flow Service가 Data Explorer와 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `endpoint` | 데이터 탐색기 서버의 끝점입니다. |
| `database` | 데이터 탐색기 데이터베이스의 이름입니다. |
| `tenant` | 데이터 탐색기 데이터베이스에 연결하는 데 사용되는 고유한 테넌트 ID입니다. |
| `servicePrincipalId` | 데이터 탐색기 데이터베이스에 연결하는 데 사용되는 고유 서비스 주체 ID. |
| `servicePrincipalKey` | 데이터 탐색기 데이터베이스에 연결하는 데 사용되는 고유한 서비스 주체 키. |
| `connectionSpec.id` | 연결을 만드는 데 필요한 고유 식별자입니다. 데이터 탐색기의 연결 사양 ID입니다 `0479cc14-7651-4354-b233-7480606c2ac3`. |

시작하는 방법에 대한 자세한 내용은 [이 데이터 탐색기 문서를 참조하십시오](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 경험 플랫폼 문제 해결 안내서에서 예제 API 호출 [](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기를 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 경험 플랫폼 API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 연결 만들기

연결은 소스를 지정하고 해당 소스에 대한 자격 증명을 포함합니다. 다른 데이터를 가져오기 위해 여러 소스 커넥터를 만드는 데 사용할 수 있으므로 데이터 탐색기 계정당 하나의 커넥터만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

데이터 탐색기 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. 데이터 탐색기의 연결 사양 ID입니다 `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `auth.params.endpoint` | 데이터 탐색기 서버의 끝점입니다. |
| `auth.params.database` | 데이터 탐색기 데이터베이스의 이름입니다. |
| `auth.params.tenant` | 데이터 탐색기 데이터베이스에 연결하는 데 사용되는 고유한 테넌트 ID입니다. |
| `auth.params.servicePrincipalId` | 데이터 탐색기 데이터베이스에 연결하는 데 사용되는 고유 서비스 주체 ID. |
| `auth.params.servicePrincipalKey` | 데이터 탐색기 데이터베이스에 연결하는 데 사용되는 고유한 서비스 주체 키. |
| `connectionSpec.id` | 데이터 탐색기 연결 사양 ID: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 만든 연결의 세부 정보를 반환합니다. 이 ID는 다음 튜토리얼에서 데이터를 탐색하는 데 필요합니다.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## 다음 단계

이 자습서를 따라 Flow Service API를 사용하여 데이터 탐색기 연결을 만들고 연결의 고유 ID 값을 받았습니다. 다음 자습서에서는 Flow Service API를 사용하여 데이터베이스를 [탐색하는 방법을 배울 때 이 ID를 사용할 수 있습니다](../../explore/database-nosql.md).
