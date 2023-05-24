---
keywords: Experience Platform;홈;인기 항목;타사 데이터베이스;데이터베이스 흐름 서비스
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 데이터베이스 탐색
description: 이 자습서에서는 흐름 서비스 API를 사용하여 서드파티 데이터베이스의 내용과 파일 구조를 살펴봅니다.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# 다음을 사용하여 데이터베이스 탐색 [!DNL Flow Service] API

이 튜토리얼에서는 [!DNL Flow Service] 서드파티 데이터베이스의 콘텐츠 및 파일 구조를 살펴보기 위한 API입니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션에서는 를 사용하여 타사 데이터베이스에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

이 자습서에서는 데이터를 수집하려는 타사 데이터베이스에 대해 유효한 연결이 필요합니다. 유효한 연결에는 데이터베이스의 연결 사양 ID와 연결 ID가 포함됩니다. 데이터베이스 연결을 만들고 이러한 값을 검색하는 방법에 대한 자세한 내용은 [소스 커넥터 개요](./../../../home.md#database).

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 E에서 필요한 각 헤더에 대한 값이 제공됩니다[!DNL xperience Platform] 아래와 같이 API 호출:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

의 모든 리소스 [!DNL Experience Platform], 다음에 속하는 항목 포함 [!DNL Flow Service]는 특정 가상 샌드박스로 분리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 테이블 탐색

데이터베이스에 대한 연결 ID를 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 검사하거나 수집할 테이블의 경로를 찾습니다 [!DNL Platform].

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 데이터베이스 소스의 연결 ID입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터베이스의 테이블 배열을 반환합니다. 가져올 테이블을 찾습니다. [!DNL Platform] 참고하시기 바랍니다. `path` 속성을 다음 단계에서 제공해야 구조를 검사할 수 있습니다.

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

## 표 구조 Inspect

데이터베이스에서 테이블 구조를 검사하려면 테이블의 경로를 쿼리 매개 변수로 지정하면서 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 데이터베이스 연결의 ID입니다. |
| `{TABLE_PATH}` | 표의 경로입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
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

이 자습서에 따라 데이터베이스를 탐색하고 수집하려는 테이블의 경로를 찾았습니다 [!DNL Platform]및 해당 구조에 대한 정보를 얻었습니다. 다음 자습서에서 이 정보를 사용하여 다음을 수행할 수 있습니다. [데이터베이스에서 데이터를 수집하여 플랫폼으로 가져옵니다.](../collect/database-nosql.md).
