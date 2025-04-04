---
keywords: Experience Platform;홈;인기 항목;타사 데이터베이스;데이터베이스 흐름 서비스
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 데이터베이스 탐색
description: 이 자습서에서는 흐름 서비스 API를 사용하여 서드파티 데이터베이스의 내용과 파일 구조를 살펴봅니다.
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 9%

---

# [!DNL Flow Service] API를 사용하여 데이터베이스 탐색

이 자습서에서는 [!DNL Flow Service] API를 사용하여 타사 데이터베이스의 내용과 파일 구조를 살펴봅니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 타사 데이터베이스에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

이 자습서에서는 데이터를 수집하려는 타사 데이터베이스에 대해 유효한 연결이 필요합니다. 유효한 연결에는 데이터베이스의 연결 사양 ID와 연결 ID가 포함됩니다. 데이터베이스 연결을 만들고 이러한 값을 검색하는 방법에 대한 자세한 내용은 [소스 커넥터 개요](./../../../home.md#database)를 참조하십시오.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [예제 API 호출을 읽는 방법](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Experience Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 E[!DNL xperience Experience Platform] API 호출의 각 필수 헤더에 대한 값이 제공됩니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Flow Service]에 속하는 리소스를 포함한 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리됩니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 테이블 탐색

데이터베이스에 대한 연결 ID를 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. [!DNL Experience Platform]을(를) 검사하거나 수집할 테이블의 경로를 찾으려면 다음 호출을 사용하십시오.

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

성공적인 응답은 데이터베이스의 테이블 배열을 반환합니다. [!DNL Experience Platform]&#x200B;(으)로 가져올 테이블을 찾고 `path` 속성을 기록해 두십시오. 다음 단계에서 테이블 구조를 검사하기 위해 테이블을 제공해야 합니다.

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

성공한 응답은 지정된 테이블의 구조를 반환합니다. 각 테이블의 열에 대한 세부 정보는 `columns` 배열의 요소 내에 있습니다.

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

이 자습서에 따라 데이터베이스를 탐색하고 [!DNL Experience Platform]에 수집할 테이블의 경로를 찾은 다음 해당 테이블의 구조에 대한 정보를 얻었습니다. 다음 자습서에서 이 정보를 사용하여 [데이터베이스에서 데이터를 수집하여 Experience Platform으로 가져오기](../collect/database-nosql.md)할 수 있습니다.
