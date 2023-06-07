---
title: Snowflake 스트리밍 계정을 Adobe Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Snowflake 스트리밍에 연결하는 방법에 대해 알아봅니다.
badgeBeta: label="Beta" type="Informative"
badgeUltimate: label="Ultimate" type="Positive"
source-git-commit: 8bc232034301fa713f61bd3f11fbde122afcdcf9
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 2%

---

# 스트림 [!DNL Snowflake] 를 사용하여 Experience Platform 할 데이터 [!DNL Flow Service] API

>[!IMPORTANT]
>
>* 다음 [!DNL Snowflake] 스트리밍 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.
>* API 지원 [!DNL Snowflake] 스트리밍 소스는 Real-Time CDP Ultimate를 구매한 고객만 사용할 수 있습니다.


이 튜토리얼에서는 [!DNL Snowflake] 계정을 Adobe Experience Platform에 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

사전 요구 사항 설정 및 [!DNL Snowflake] 스트리밍 소스. 다음을 읽으십시오. [[!DNL Snowflake] 스트리밍 소스 개요](../../../../connectors/databases/snowflake-streaming.md).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기 {#create-a-base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Snowflake] 요청 본문의 일부인 인증 자격 증명입니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은에 대한 기본 연결을 만듭니다. [!DNL Snowflake]:

>[!TIP]
>
>다음 `auth.specName` 아래 예와 같이 빈칸을 포함하여 값을 정확히 입력해야 합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "Snowflake base connection",
      "auth": {
          "specName": "Basic Authentication for Snowflake",
          "params": {
              "account": "wixnnnd-ui60793.snowflakecomputing.com",
              "database": "ACME_DB",
              "warehouse": "ACME_WH",
              "username": "nikola15",
              "schema": "PUBLIC",
              "password": "xxxx",
              "role": "ACCOUNTADMIN"
          }
      },
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `auth.params.account` | 의 이름 [!DNL Snowflake] 스트리밍 계정입니다. |
| `auth.params.database` | 의 이름 [!DNL Snowflake] 데이터를 가져올 데이터베이스입니다. |
| `auth.params.warehouse` | 의 이름 [!DNL Snowflake] 웨어하우스 다음 [!DNL Snowflake] warehouse는 애플리케이션의 쿼리 실행 프로세스를 관리합니다. 각 웨어하우스는 서로 독립적이며 데이터를 플랫폼으로 가져올 때 개별적으로 액세스해야 합니다. |
| `auth.params.username` | 에 대한 사용자 이름 [!DNL Snowflake] 스트리밍 계정입니다. |
| `auth.params.schema` | (선택 사항) 와 연관된 데이터베이스 스키마 [!DNL Snowflake] 스트리밍 계정입니다. |
| `auth.params.password` | 에 대한 암호 [!DNL Snowflake] 스트리밍 계정입니다. |
| `auth.params.role` | (선택 사항) 이에 대한 사용자의 역할 [!DNL Snowflake] 연결. 제공되지 않은 경우 이 값의 기본값은 입니다. `public`. |
| `connectionSpec.id` | 다음 [!DNL Snowflake] 연결 사양 ID: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**응답**

성공한 응답은 새로 생성된 기본 연결과 해당 etag를 반환합니다.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 데이터 테이블 탐색 {#explore-your-data-tables}

다음으로 기본 연결 ID를 사용하여에 GET 요청을 하여 소스의 데이터 테이블을 탐색하고 탐색합니다. `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` 기본 연결 ID를 매개 변수로 제공하는 동안 엔드포인트가 발생했습니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 의 기본 연결 ID [!DNL Snowflake] 스트리밍 소스. |


**요청**

다음 요청은 의 구조와 컨텐츠를 검색합니다. [!DNL Snowflake] 스트리밍 계정입니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/1b614dc0-b76e-41e1-b25f-09f4a9d3f111/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 루트 수준에서 소스 데이터의 구조와 콘텐츠를 반환합니다.

```json
{
    "items": [
        {
            "type": "table",
            "name": "ACME"
        }
    ]
}
```

| 속성 | 설명 |
| --- | --- |
| `items.type` | 테이블 유형. |
| `items.names` | 테이블 이름. |

## 소스 연결 만들기 {#create-a-source-connection}

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다.

POST 소스 연결을 만들려면 `/sourceConnections` 의 엔드포인트 [!DNL Flow Service] API.

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Snowflake Streaming Source Connection",
      "description": "A source connection for Snowflake Streaming data",
      "baseConnectionId": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
      "connectionSpec": {
          "id": "51ae16c2-bdad-42fd-9fce-8d5dfddaf140",
          "version": "1.0"
      },
      "params": {
          "tableName": "ACME",
          "timestampColumn": "dOb",
          "backfill": "true"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `baseConnectionId` | 에 대해 인증된 기본 연결 ID [!DNL Snowflake] 스트리밍 소스. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | 에 대한 연결 사양 ID [!DNL Snowflake] 스트리밍 소스. |
| `params.tableName` | 에 있는 테이블 이름 [!DNL Snowflake] 플랫폼으로 가져올 데이터베이스입니다. |
| `params.timestampColumn` | 증분 값을 가져오는 데 사용할 타임스탬프 열의 이름입니다. |
| `params.backfill` | 데이터를 시작(0 epoch 시간)부터 가져오는지 또는 소스가 시작된 시간부터 가져오는지 여부를 결정하는 부울 플래그입니다. 이 값에 대한 자세한 내용은 [[!DNL Snowflake] 스트리밍 소스 개요](../../../../connectors/databases/snowflake-streaming.md). |

**응답**

응답이 성공하면 소스 연결 ID와 해당 etag가 반환됩니다. 소스 연결 ID는 이후 단계에서 데이터 흐름을 만드는 데 사용됩니다.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 데이터 흐름 만들기

데이터 흐름을 만들어 둘러보기에서 데이터를 스트리밍하려면 [!DNL Snowflake] account to Platform에 대해 POST 요청을 해야 합니다. `/flows` 다음 값을 제공하는 동안 엔드포인트:

>[!TIP]
>
>다음 ID를 검색하는 방법에 대한 단계별 지침은 아래 링크를 따르십시오.

* [소스 연결 ID](#create-a-source-connection)
* [Target 연결 ID](../../collect/database-nosql.md#create-a-target-connection)
* [흐름 사양 ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID 매핑](../../collect/database-nosql.md#create-a-mapping)

**API 형식**

```http
POST /flows
```

**요청**

다음 요청은 다음에 대한 스트리밍 데이터 흐름을 만듭니다. [!DNL Snowflake] 계정입니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake Streaming Dataflow",
      "description": "A dataflow for Snowflake streaming data",
      "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
      ],
      "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
      ],
      "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
            "mappingVersion": 0
          }
        }
      ]
    }'
```

| 속성 | 설명 |
| --- | --- |
| `sourceConnectionIds` | 에 대한 소스 연결 ID [!DNL Snowflake] 스트리밍 소스. |
| `targetConnectionIds` | 에 대한 대상 연결 ID [!DNL Snowflake] 스트리밍 소스. |
| `flowSpec.id` | 데이터 흐름을 만들 수 있는 흐름 사양 ID [!DNL Snowflake] 스트리밍 소스. 이 흐름 사양 ID를 사용하면 매핑 변환을 사용하여 스트리밍 데이터 흐름을 만들 수 있습니다. 이 ID는 고정되어 있으며 다음과 같습니다. `c1a19761-d2c7-4702-b9fa-fe91f0613e81`. |
| `transformations.params.mappingId` | 데이터 흐름에 대한 매핑 ID입니다. |

**응답**

성공적인 응답은 흐름 ID와 해당 etag를 반환합니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"770029f8-0000-0200-0000-6019e7d40000\""
}
```

## 다음 단계

이 자습서를 따라 를 위한 스트리밍 데이터 흐름을 만들었습니다. [!DNL Snowflake] 를 사용하는 데이터 [!DNL Flow Service] API. Adobe Experience Platform 소스에 대한 추가 정보는 다음 설명서를 참조하십시오.

* [소스 개요](../../../../home.md)
* [API를 사용하여 데이터 흐름 모니터링](../../monitor.md)