---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;계정 업데이트;;home;popular topics;flow service;update accounts
solution: Experience Platform
title: Flow Service API를 사용하여 계정 업데이트
topic-legacy: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 계정의 세부 사항 및 자격 증명을 업데이트하는 절차를 설명합니다.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---

# Flow Service API를 사용하여 계정 업데이트

경우에 따라 기존 소스 연결의 세부 사항을 업데이트해야 할 수 있습니다. [!DNL Flow Service] 이름, 설명 및 자격 증명을 포함하여 기존 배치 또는 스트리밍 연결의 세부 사항을 추가, 편집 및 삭제할 수 있는 기능을 제공합니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 연결의 세부 사항과 자격 증명을 업데이트하는 단계를 다룹니다.

## 시작하기

이 자습서를 사용하려면 기존 연결 및 유효한 연결 ID가 있어야 합니다. 기존 연결이 없는 경우 [소스 개요](../../home.md)에서 원하는 소스를 선택하고 이 튜토리얼을 시작하기 전에 설명한 단계를 따릅니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 자세히 알아야 합니다.

* [소스](../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 연결을 성공적으로 업데이트하려면 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 세부 사항 보기

연결을 업데이트하는 첫 번째 단계는 연결 ID를 사용하여 연결 세부 사항을 가져오는 것입니다. 연결의 현재 세부 사항을 검색하려면 업데이트할 연결의 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 GET 요청을 하십시오.

**API 형식**

```http
GET /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 검색할 연결에 대한 고유한 `id` 값입니다. |

**요청**

다음 요청은 연결에 대한 정보를 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 자격 증명, 고유 식별자(`id`) 및 버전을 포함하여 연결의 현재 세부 정보를 반환합니다. 연결을 업데이트하려면 버전 값이 필요합니다.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## 연결 업데이트

연결의 이름, 설명 및 자격 증명을 업데이트하려면 연결 ID, 버전 및 사용할 새 정보를 제공하는 동안 [!DNL Flow Service] API에 PATCH 요청을 수행하십시오.

>[!IMPORTANT]
>
>PATCH 요청을 할 때는 `If-Match` 헤더가 필요합니다. 이 헤더의 값은 업데이트할 연결의 고유한 버전입니다.

**API 형식**

```http
PATCH /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 업데이트할 연결에 대한 고유한 `id` 값입니다. |

**요청**

다음 요청에서는 새 이름 및 설명뿐만 아니라 연결을 업데이트하는 새 자격 증명 세트를 제공합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `op` | 연결을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 다음이 포함됩니다.`add`, `replace` 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 연결 ID와 업데이트된 태그를 반환합니다. 연결 ID를 제공하는 동안 [!DNL Flow Service] API에 GET 요청을 하여 업데이트를 확인할 수 있습니다.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 연결과 관련된 자격 증명과 정보를 업데이트했습니다. 소스 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md)를 참조하십시오.
