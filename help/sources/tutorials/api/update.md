---
keywords: Experience Platform;홈;인기 항목;흐름 서비스;계정 업데이트
solution: Experience Platform
title: Flow Service API를 사용하여 계정 업데이트
topic-legacy: overview
type: Tutorial
description: 이 자습서에서는 Flow Service API를 사용하여 계정의 세부 정보 및 자격 증명을 업데이트하는 단계를 설명합니다.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 2%

---

# Flow Service API를 사용하여 계정 업데이트

경우에 따라 기존 소스 연결의 세부 사항을 업데이트해야 할 수 있습니다. [!DNL Flow Service] 이름, 설명 및 자격 증명을 포함하여 기존 일괄 처리 또는 스트리밍 연결의 세부 사항을 추가, 편집 및 삭제할 수 있는 기능을 제공합니다.

이 자습서에서는 를 사용하여 연결의 세부 사항 및 자격 증명을 업데이트하는 단계를 설명합니다 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 자습서에서는 기존 연결과 유효한 연결 ID가 있어야 합니다. 기존 연결이 없는 경우, [소스 개요](../../home.md) 및 이 자습서를 시도하기 전에 설명된 단계를 따릅니다.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 플랫폼 API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).

## 연결 세부 정보 조회

연결을 업데이트하는 첫 번째 단계는 연결 ID를 사용하여 세부 사항을 검색하는 것입니다. 연결의 현재 세부 사항을 검색하려면 [!DNL Flow Service] 업데이트할 연결의 연결 ID를 제공하는 동안 API입니다.

**API 형식**

```http
GET /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 고유 `id` 검색할 연결의 값입니다. |

**요청**

다음 요청은 연결에 대한 정보를 검색합니다.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 해당 자격 증명, 고유 식별자( )를 포함하여 연결의 현재 세부 정보를 반환합니다`id`) 및 버전으로 마이그레이션 하는 것이 좋습니다. 연결을 업데이트하려면 버전 값이 필요합니다.

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

연결의 이름, 설명 및 자격 증명을 업데이트하려면 [!DNL Flow Service] 연결 ID, 버전 및 사용할 새 정보를 제공하는 동안 API를 참조하십시오.

>[!IMPORTANT]
>
>다음 `If-Match` PATCH 요청을 만들 때는 헤더가 필요합니다. 이 헤더의 값은 업데이트할 연결의 고유한 버전입니다.

**API 형식**

```http
PATCH /connections/{CONNECTION_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 고유 `id` 업데이트할 연결의 값입니다. |

**요청**

다음 요청에서는 연결을 업데이트할 새 이름 및 설명과 새 자격 증명 세트를 제공합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | 연결을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업은 다음과 같습니다. `add`, `replace`, 및 `remove`. |
| `path` | 업데이트할 매개 변수의 경로입니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 연결 ID와 업데이트된 태그를 반환합니다. 에 GET 요청을 수행하여 업데이트를 확인할 수 있습니다 [!DNL Flow Service] API, 연결 ID를 제공하는 동안

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## 다음 단계

이 자습서에 따라 를 사용하여 연결과 관련된 자격 증명과 정보를 업데이트했습니다 [!DNL Flow Service] API. 소스 커넥터 사용에 대한 자세한 내용은 다음을 참조하십시오. [소스 개요](../../home.md).
