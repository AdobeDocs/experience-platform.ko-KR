---
title: Snowflake 스트리밍 계정을 Adobe Experience Platform에 연결
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Snowflake 스트리밍에 연결하는 방법에 대해 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 3fc225a4-746c-4a91-aa77-bbeb091ec364
source-git-commit: 34b1676ebb5405d73cf37cd786d1e6c26cb8fdaa
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 4%

---

# [!DNL Flow Service] API를 사용하여 Experience Platform에 [!DNL Snowflake] 데이터 스트리밍

>[!IMPORTANT]
>
>
> [!DNL Snowflake] 스트리밍 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 API에서 사용할 수 있습니다.

이 자습서에서는 [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>)를 사용하여 [!DNL Snowflake] 계정의 데이터를 Adobe Experience Platform에 연결하고 스트리밍하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

[!DNL Snowflake] 스트리밍 소스에 대한 필수 구성 요소 설정 및 정보입니다. [[!DNL Snowflake] 스트리밍 원본 개요](../../../../connectors/databases/snowflake-streaming.md)를 읽으십시오.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기 {#create-a-base-connection}

기본 연결은 소스의 인증 자격 증명, 연결의 현재 상태 및 고유한 기본 연결 ID를 포함하여 소스와 플랫폼 간에 정보를 유지합니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Snowflake] 인증 자격 증명을 요청 본문의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```https
POST /connections
```

**요청**

다음 요청은 [!DNL Snowflake]에 대한 기본 연결을 만듭니다.

>[!TIP]
>
>`auth.specName` 값은 아래 예와 정확히 동일하게 입력해야 합니다(공백 포함).

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
| `auth.params.account` | [!DNL Snowflake] 스트리밍 계정의 이름입니다. |
| `auth.params.database` | 데이터를 가져올 [!DNL Snowflake] 데이터베이스의 이름입니다. |
| `auth.params.warehouse` | [!DNL Snowflake] 웨어하우스 이름. [!DNL Snowflake] 웨어하우스에서 응용 프로그램의 쿼리 실행 프로세스를 관리합니다. 각 웨어하우스는 서로 독립적이며 데이터를 플랫폼으로 가져올 때 개별적으로 액세스해야 합니다. |
| `auth.params.username` | [!DNL Snowflake] 스트리밍 계정의 사용자 이름. |
| `auth.params.schema` | (선택 사항) [!DNL Snowflake] 스트리밍 계정과 연결된 데이터베이스 스키마. |
| `auth.params.password` | [!DNL Snowflake] 스트리밍 계정의 암호입니다. |
| `auth.params.role` | (선택 사항) 이 [!DNL Snowflake] 연결에 대한 사용자의 역할입니다. 지정하지 않으면 이 값은 기본적으로 `public`(으)로 설정됩니다. |
| `connectionSpec.id` | [!DNL Snowflake] 연결 사양 ID: `51ae16c2-bdad-42fd-9fce-8d5dfddaf140`. |

**응답**

성공한 응답은 새로 생성된 기본 연결과 해당 etag를 반환합니다.

```json
{
    "id": "1b614dc0-b76e-41e1-b25f-09f4a9d3f111",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 데이터 테이블 탐색 {#explore-your-data-tables}

다음으로 기본 연결 ID를 사용하여 `/connections/{BASE_CONNECTION_ID}/explore?objectType=root` 끝점에 GET 요청을 하면서 기본 연결 ID를 매개 변수로 제공하여 원본의 데이터 테이블을 탐색하고 탐색합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | [!DNL Snowflake] 스트리밍 소스의 기본 연결 ID입니다. |


**요청**

다음 요청은 [!DNL Snowflake] 스트리밍 계정의 구조와 콘텐츠를 검색합니다.

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

소스 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 끝점에 대한 POST 요청을 만듭니다.

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
          "backfill": "true",
          "timezoneValue": "PST"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `baseConnectionId` | [!DNL Snowflake] 스트리밍 소스에 대해 인증된 기본 연결 ID입니다. 이 ID는 이전 단계에서 생성되었습니다. |
| `connectionSpec.id` | [!DNL Snowflake] 스트리밍 소스에 대한 연결 사양 ID입니다. |
| `params.tableName` | 플랫폼으로 가져올 [!DNL Snowflake] 데이터베이스의 테이블 이름입니다. |
| `params.timestampColumn` | 증분 값을 가져오는 데 사용할 타임스탬프 열의 이름입니다. |
| `params.backfill` | 데이터를 시작(0 epoch 시간)부터 가져오는지 또는 소스가 시작된 시간부터 가져오는지 여부를 결정하는 부울 플래그입니다. 이 값에 대한 자세한 내용은 [[!DNL Snowflake] 스트리밍 원본 개요](../../../../connectors/databases/snowflake-streaming.md)를 참조하세요. |
| `params.timezoneValue` | 시간대 값은 [!DNL Snowflake] 데이터베이스를 쿼리할 때 가져올 시간대의 현재 시간을 나타냅니다. 구성의 타임스탬프 열이 `TIMESTAMP_NTZ`(으)로 설정된 경우 이 매개 변수를 제공해야 합니다. 지정하지 않으면 `timezoneValue`의 기본값이 UTC로 설정됩니다. |

**응답**

응답이 성공하면 소스 연결 ID와 해당 etag가 반환됩니다. 소스 연결 ID는 이후 단계에서 데이터 흐름을 만드는 데 사용됩니다.

```json
{
    "id": "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6",
    "etag": "\"d300cf4e-0000-0200-0000-6447a7750000\""
}
```

## 데이터 흐름 만들기

데이터 흐름을 만들어 [!DNL Snowflake] 둘러보기 계정에서 플랫폼으로 데이터를 스트리밍하려면 다음 값을 제공하는 동안 `/flows` 끝점에 대한 POST 요청을 수행해야 합니다.

>[!TIP]
>
>다음 ID를 검색하는 방법에 대한 단계별 지침은 아래 링크를 따르십시오.

* [Source 연결 ID](#create-a-source-connection)
* [대상 연결 ID](../../collect/database-nosql.md#create-a-target-connection)
* [흐름 사양 ID](../../collect/database-nosql.md#retrieve-dataflow-specifications)
* [ID 매핑](../../collect/database-nosql.md#create-a-mapping)

**API 형식**

```http
POST /flows
```

**요청**

다음 요청은 [!DNL Snowflake] 계정에 대한 스트리밍 데이터 흐름을 만듭니다.

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
| `sourceConnectionIds` | [!DNL Snowflake] 스트리밍 소스에 대한 소스 연결 ID입니다. |
| `targetConnectionIds` | [!DNL Snowflake] 스트리밍 소스에 대한 대상 연결 ID입니다. |
| `flowSpec.id` | [!DNL Snowflake] 스트리밍 소스에 대한 데이터 흐름을 만들기 위한 흐름 사양 ID입니다. 이 흐름 사양 ID를 사용하면 매핑 변환을 사용하여 스트리밍 데이터 흐름을 만들 수 있습니다. 이 ID는 고정되어 있으며 `c1a19761-d2c7-4702-b9fa-fe91f0613e81`입니다. |
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

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Snowflake] 데이터에 대한 스트리밍 데이터 흐름을 만들었습니다. Adobe Experience Platform 소스에 대한 추가 정보는 다음 설명서를 참조하십시오.

* [소스 개요](../../../../home.md)
* [API를 사용하여 데이터 흐름 모니터링](../../monitor.md)
