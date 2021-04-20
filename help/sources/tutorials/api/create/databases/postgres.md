---
keywords: Experience Platform;홈;인기 항목;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Flow 서비스 API를 사용하여 PostgreSQL 소스 연결 만들기
topic: overview
type: Tutorial
description: Flow Service API를 사용하여 Adobe Experience Platform을 PostgreSQL에 연결하는 방법을 알아봅니다.
translation-type: tm+mt
source-git-commit: 8851e11e956b393e56714d4d48870b7f68947c18
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---


# [!DNL Flow Service] API를 사용하여 [!DNL PostgreSQL] 소스 연결 만들기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] API를 사용하여 [!DNL Experience Platform]을(를) [!DNL PostgreSQL](이하 &quot;PSQL&quot;)에 연결하는 단계를 안내합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 PSQL에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) PSQL과 연결하려면 다음 연결 속성을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `connectionString` | PSQL 계정과 연결된 연결 문자열입니다. PSQL 연결 문자열 패턴은 다음과 같습니다.`Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | 연결을 생성하는 데 사용되는 ID. PSQL에 대한 고정 연결 사양 ID는 `74a1c565-4e59-48d7-9d67-7c03b8a13137`입니다. |

연결 문자열을 얻는 방법에 대한 자세한 내용은 [이 PSQL 문서](https://www.postgresql.org/docs/9.2/app-psql.html)를 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 연결 만들기

연결은 소스를 지정하며 해당 소스의 자격 증명을 포함합니다. 여러 소스 커넥터를 만들어 다른 데이터를 가져올 수 있으므로 PSQL 계정당 하나의 연결만 필요합니다.

**API 형식**

```http
POST /connections
```

**요청**

PSQL 연결을 만들려면 고유한 연결 사양 ID를 POST 요청의 일부로 제공해야 합니다. PSQL에 대한 연결 사양 ID는 `74a1c565-4e59-48d7-9d67-7c03b8a13137`입니다.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| 속성 | 설명 |
| ------------- | --------------- |
| `auth.params.connectionString` | PSQL 계정과 연결된 연결 문자열입니다. PSQL 연결 문자열 패턴은 다음과 같습니다.`Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | PSQL에 대한 연결 사양 ID는 다음과 같습니다.`74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**응답**

성공적인 응답은 새로 만든 기본 연결의 고유 식별자(`id`)를 반환합니다. 다음 자습서에서 PSQL 데이터베이스를 살펴보려면 이 ID가 필요합니다.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## 다음 단계

이 자습서를 따라 [!DNL Flow Service] API를 사용하여 PSQL 연결을 만들고 연결의 고유 ID 값을 받았습니다. 흐름 서비스 API](../../explore/database-nosql.md)를 사용하여 데이터베이스 또는 NoSQL 시스템을 탐색하는 방법을 배울 때 다음 자습서에서 이 연결 ID를 사용할 수 있습니다.[
