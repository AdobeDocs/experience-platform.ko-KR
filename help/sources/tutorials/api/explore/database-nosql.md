---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 데이터베이스 탐색
topic: overview
translation-type: tm+mt
source-git-commit: c4162d88a688ce2028de08b63e7b7eab954a0e29

---


# Flow Service API를 사용하여 데이터베이스 탐색

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 Flow Service API를 사용하여 타사 데이터베이스의 컨텐츠와 파일 구조를 탐색합니다.

## 시작하기

이 가이드에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../home.md): Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있으며, 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../sandboxes/home.md): 경험 플랫폼은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 타사 데이터베이스에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

이 자습서에서는 데이터를 인제스트할 타사 데이터베이스와 유효한 연결이 필요합니다. 유효한 연결에는 데이터베이스의 연결 사양 ID 및 연결 ID가 포함됩니다. 데이터베이스 연결 만들기 및 이러한 값 검색에 대한 자세한 내용은 [소스 커넥터 개요를 참조하십시오](./../../../home.md#database).

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 경험 플랫폼 문제 해결 안내서에서 예제 API 호출 [](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기를 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 경험 플랫폼 API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증: 무기명 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속하는 리소스를 비롯하여 경험 플랫폼의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 데이터 테이블 살펴보기

데이터베이스의 연결 ID를 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 Platform에서 검사하거나 인제스트할 테이블의 경로를 찾습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 데이터베이스 연결의 ID입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터베이스의 테이블 배열을 반환합니다. Platform(플랫폼)으로 가져올 테이블을 찾아 구조를 검사하는 다음 단계에서 제공해야 하는 만큼 해당 `path` 속성을 확인합니다.

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 테이블 구조 검사

데이터베이스에서 테이블 구조를 검사하려면 테이블의 경로를 쿼리 매개 변수로 지정하는 동안 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 데이터베이스 연결의 ID입니다. |
| `{TABLE_PATH}` | 표의 경로입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 테이블의 구조를 반환합니다. 표의 각 열에 대한 세부 사항은 `columns` 배열의 요소 내에 있습니다.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
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
            }
        ]
    }
}
```

## 다음 단계

이 튜토리얼을 따라 데이터베이스를 살펴보고, 플랫폼에 인제스트할 테이블의 경로를 발견했으며, 해당 구조에 대한 정보를 얻었습니다. 다음 자습서에서 이 정보를 사용하여 데이터베이스에서 데이터를 [수집하여 Platform으로 가져올 수 있습니다](../collect/database-nosql.md).