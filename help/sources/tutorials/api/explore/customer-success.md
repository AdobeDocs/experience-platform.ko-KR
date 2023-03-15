---
keywords: Experience Platform;홈;인기 항목;cs;CS;고객 성공 시스템
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 고객 성공 시스템 살펴보기
description: 이 튜토리얼에서는 플로우 서비스 API를 사용하여 고객 성공(CS) 시스템을 살펴봅니다.
exl-id: 453be69d-3d72-4987-81cd-67fa3be7ee59
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 2%

---

# 다음을 사용하여 고객 성공 시스템 살펴보기 [!DNL Flow Service] API

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 개별 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결 가능한 사용자 인터페이스와 RESTful API를 제공합니다.

이 튜토리얼에서는 [!DNL Flow Service] 고객 성공(CS) 시스템을 탐색하기 위한 API입니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 를 사용하여 CS 시스템에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 기본 연결 얻기

을 사용하여 CS 시스템을 탐색하려면 [!DNL Platform] API를 사용하려면 올바른 기본 연결 ID를 보유해야 합니다. 사용하려는 CS 시스템에 대한 기본 연결이 없는 경우 다음 자습서를 통해 기본 연결을 만들 수 있습니다.

* [Salesforce 서비스 클라우드](../create/customer-success/salesforce-service-cloud.md)
* [ServiceNow](../create/customer-success/servicenow.md)

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform], 다음에 속하는 항목 포함 [!DNL Flow Service]는 특정 가상 샌드박스로 분리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 데이터 테이블 탐색

CS 시스템에 대한 기본 연결을 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 검사하거나 수집할 테이블의 경로를 찾습니다 [!DNL Platform].

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | CS 기본 연결의 ID입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 CS 시스템의 테이블 배열을 반환합니다. 가져올 테이블을 찾습니다. [!DNL Platform] 참고하시기 바랍니다. `path` 속성을 다음 단계에서 제공해야 구조를 검사할 수 있습니다.

```json
[
    {
        "type": "table",
        "name": "Accepted Event Relation",
        "path": "AcceptedEventRelation",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account",
        "path": "Account",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Change Event",
        "path": "AccountChangeEvent",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Clean Info",
        "path": "AccountCleanInfo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 표 구조 Inspect

CS 시스템에서 테이블 구조를 검사하려면 테이블의 경로를 질의 매개변수로 지정하면서 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | CS 기본 연결의 ID입니다. |
| `{TABLE_PATH}` | 표의 경로입니다. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 테이블의 구조를 반환합니다. 각 테이블 열에 대한 세부 사항은 의 요소 내에 있습니다. `columns` 배열입니다.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 다음 단계

이 자습서에 따라 CS 시스템을 탐색하고 수집하려는 표의 경로를 찾았습니다 [!DNL Platform]및 해당 구조에 대한 정보를 얻었습니다. 다음 자습서에서 이 정보를 사용하여 다음을 수행할 수 있습니다. [CS 시스템에서 데이터를 수집하고 플랫폼으로 가져옵니다.](../collect/customer-success.md).
