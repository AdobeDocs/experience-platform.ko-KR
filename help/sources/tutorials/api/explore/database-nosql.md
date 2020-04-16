---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템 살펴보기
topic: overview
translation-type: tm+mt
source-git-commit: 4c34ecdaeb4a0df1faf2dd54e8a264b9126f20b4

---


# Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템 살펴보기

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템을 탐색합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../home.md):Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션은 Flow Service API를 사용하여 데이터베이스 또는 NoSQL 시스템에 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다.

### 기본 연결 받기

플랫폼 API를 사용하여 데이터베이스 또는 NoSQL 시스템을 탐색하려면 유효한 기본 연결 ID를 보유해야 합니다. 작업할 데이터베이스 또는 NoSQL 시스템에 대한 기본 연결이 아직 없는 경우 다음 자습서를 통해 데이터베이스를 만들 수 있습니다.

* [Amazon Redshift](../create/databases/redshift.md)
* [Azure HDInsights의 Apache Spark ](../create/databases/spark.md)
* [Azure Synapse Analytics](../create/databases/synapse-analytics.md)
* [Azure 테이블 저장소](../create/databases/ats.md)
* [Google BigQuery](../create/databases/bigquery.md)
* [하이브](../create/databases/hive.md)
* [MariaDB](../create/databases/mariadb.md)
* [MySQL](../create/databases/mysql.md)
* [피닉스](../create/databases/phoenix.md)
* [PostgreSQL](../create/databases/postgres.md)
* [SQL Server](../create/databases/sql-server.md)

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속한 리소스를 비롯하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 데이터 테이블 살펴보기

데이터베이스 또는 NoSQL 시스템에 대한 기본 연결을 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 Platform에서 검사하거나 인제스트할 테이블의 경로를 찾습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 데이터베이스 또는 NoSQL 기본 연결의 ID입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터베이스 또는 NoSQL 시스템에서 테이블 배열을 반환합니다. Platform(플랫폼)으로 가져올 표를 찾아 다음 단계에서 제공해야 하므로 해당 `path` 속성을 기록해 두십시오.

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

데이터베이스 또는 NoSQL 시스템에서 테이블 구조를 검사하려면 테이블의 경로를 쿼리 매개 변수로 지정하는 동안 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 데이터베이스 또는 NoSQL 기본 연결의 ID입니다. |
| `{TABLE_PATH}` | 표의 경로입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 테이블의 구조를 반환합니다. 각 테이블의 열에 대한 세부 사항은 `columns` 배열의 요소 내에 있습니다.

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

이 자습서를 따라 데이터베이스 또는 NoSQL 시스템을 살펴보고, 플랫폼에 인제스트할 테이블의 경로를 발견했으며, 해당 구조에 대한 정보를 얻었습니다. 다음 자습서에서 이 정보를 사용하여 데이터베이스 또는 NoSQL 시스템에서 데이터를 [수집하고 Platform으로 가져올 수 있습니다](../collect/database-nosql.md).