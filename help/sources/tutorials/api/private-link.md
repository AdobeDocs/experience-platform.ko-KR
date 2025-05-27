---
title: 소스의 비공개 링크 지원
description: Adobe Experience Platform 소스에 대한 개인 링크를 만들고 사용하는 방법을 알아봅니다
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 4c91ffc60a2537fcc76ce935bf3b163984fdc5e4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 5%

---

# 소스의 비공개 링크 지원

>[!AVAILABILITY]
>
>이 기능은 제한된 가용성에 있으며 현재 다음 소스에서만 지원됩니다.
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

비공개 링크를 통해 Azure 기반 소스에 비공개 끝점 연결을 설정하고 데이터에 대한 보다 안전한 전송 메커니즘을 허용하는 방법에 대해 알아보려면 이 안내서를 읽어 보십시오.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 [!DNL Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 비공개 엔드포인트 만들기 {#create-private-endpoint}

비공개 끝점을 만들려면 `/privateEndpoints`에 POST 요청을 만듭니다.

**API 형식**

```http
POST /privateEndpoints
```

**요청**

다음 요청은 비공개 끝점을 만듭니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 비공개 엔드포인트의 이름. |
| `subscriptionId` | [!DNL Azure] 구독과 연계된 ID. 자세한 내용은 [구독 및 테넌트 ID 검색 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)에 대한 [!DNL Azure] 가이드를 참조하십시오. |
| `resourceGroupName` | [!DNL Azure]에 있는 리소스 그룹의 이름입니다. 리소스 그룹에 [!DNL Azure] 솔루션에 대한 관련 리소스가 포함되어 있습니다. 자세한 내용은 [리소스 그룹 관리](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)에 대한 [!DNL Azure] 안내서를 참조하십시오. |
| `resourceName` | 리소스의 이름입니다. [!DNL Azure]에서 리소스는 가상 컴퓨터, 웹 앱 및 데이터베이스와 같은 인스턴스를 참조합니다. 자세한 내용은 [리소스 관리자 이해 [!DNL Azure] 에 대한 [!DNL Azure] 안내서를 참조하십시오.](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview) |
| `fqdns` | 소스에 대해 정규화된 도메인 이름. 이 속성은 [!DNL Snowflake] 원본을 사용하는 경우에만 필요합니다. |
| `connectionSpec.id` | 사용 중인 소스의 연결 사양 ID입니다. |
| `connectionSpec.version` | 사용 중인 연결 사양 ID의 버전입니다. |

+++

**응답**

성공적인 응답은 다음을 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 새로 만든 비공개 엔드포인트의 ID입니다. |
| `name` | 비공개 엔드포인트의 이름. |
| `subscriptionId` | [!DNL Azure] 구독과 연계된 ID. 자세한 내용은 [구독 및 테넌트 ID 검색 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)에 대한 [!DNL Azure] 가이드를 참조하십시오. |
| `resourceGroupName` | [!DNL Azure]에 있는 리소스 그룹의 이름입니다. 리소스 그룹에 [!DNL Azure] 솔루션에 대한 관련 리소스가 포함되어 있습니다. 자세한 내용은 [리소스 그룹 관리](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)에 대한 [!DNL Azure] 안내서를 참조하십시오. |
| `resourceName` | 리소스의 이름입니다. [!DNL Azure]에서 리소스는 가상 컴퓨터, 웹 앱 및 데이터베이스와 같은 인스턴스를 참조합니다. 자세한 내용은 [리소스 관리자 이해 [!DNL Azure] 에 대한 [!DNL Azure] 안내서를 참조하십시오.](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview) |
| `fqdns` | 소스에 대해 정규화된 도메인 이름. 이 속성은 [!DNL Snowflake] 원본을 사용하는 경우에만 필요합니다. |
| `connectionSpec.id` | 사용 중인 소스의 연결 사양 ID입니다. |
| `connectionSpec.version` | 사용 중인 연결 사양 ID의 버전입니다. |
| `state` | 비공개 끝점의 현재 상태입니다. 유효한 상태는 다음과 같습니다. <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## 비공개 엔드포인트 목록 검색 {#retrieve-private-endpoints}

조직의 지정된 샌드박스에서 개인 끝점 목록을 검색하려면 `/privateEndpoints`에 GET 요청을 합니다.

**API 형식**

```http
GET /privateEndpoints
```

**요청**

다음 요청은 조직에 있는 모든 비공개 엔드포인트 목록을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공적인 응답은 조직의 비공개 끝점 목록을 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## 지정된 소스에 대한 비공개 엔드포인트 목록 검색 {#retrieve-private-endpoints-by-source}

특정 소스에 해당하는 개인 끝점 목록을 검색하려면 `/privateEndpoints` 끝점에 GET 요청을 하고 소스의 `connectionSpec.id`을(를) 제공하십시오.

**API 형식**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 전용 끝점을 검색할 소스의 연결 사양 ID입니다. |

**요청**

다음 요청은 연결 사양 ID가 `4c10e202-c428-4796-9208-5f1f5732b1cf`인 소스에 해당하는 모든 개인 끝점 목록을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공한 응답은 연결 사양 ID가 `4c10e202-c428-4796-9208-5f1f5732b1cf`인 소스에 해당하는 모든 개인 끝점 목록을 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## 비공개 끝점 검색 {#retrieve-specific-private-endpoint}

특정 개인 끝점을 검색하려면 `/privateEndpoints`에 GET 요청을 만들고 검색할 개인 끝점의 ID를 제공하십시오.

**API 형식**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | 검색할 개인 엔드포인트의 ID입니다. |

**요청**

다음 요청은 ID가 `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`인 개인 끝점을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공적인 응답이 ID가 `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`인 개인 끝점을 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## 비공개 끝점 확인 {#resolve-private-endpoint}

**API 형식**

```http
GET /privateEndpoints?op=autoResolve
```

**요청**

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**응답**

+++응답 예를 보려면 선택

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## 대화형 작성 활성화 {#enable-interactive-authoring}

대화형 작성은 연결 또는 계정을 탐색하고 데이터를 미리 보는 것과 같은 기능에 사용됩니다. 대화형 작성을 활성화하려면 `/privateEndpoints/interactiveAuthoring`에 POST를 요청하고 쿼리 매개 변수에 `enable`을(를) 연산자로 지정하십시오.

**API 형식**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `op` | 수행할 작업입니다. 대화형 작성을 사용하려면 `op` 값을 `enable`(으)로 설정하십시오. |

**요청**

다음 요청은 비공개 엔드포인트에 대한 대화형 작성을 활성화하고 TTL을 60분으로 설정합니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| 속성 | 설명 |
| --- | --- |
| `autoTerminationMinutes` | 대화형 작성 TTL(time-to-live)(분)입니다. 대화형 작성은 연결 또는 계정을 탐색하고 데이터를 미리 보는 것과 같은 기능에 사용됩니다. 최대 TTL은 120분으로 설정할 수 있습니다. 기본 TTL은 60분입니다. |

+++

**응답**

성공적인 응답은 HTTP 상태 202(허용됨)를 반환합니다.

## 대화형 작성 상태 검색 {#retrieve-interactive-authoring-status}

개인 끝점에 대한 대화형 작성의 현재 상태를 보려면 `/privateEndpoints/interactiveAuthoring`에 GET을 요청하십시오.

**API 형식**

```http
GET /privateEndpoints/interactiveAuthoring
```

**요청**

다음 요청은 대화형 작성 상태를 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

+++응답 예를 보려면 선택

```json
{
    "status": "Disabled"
}
```

| 속성 | 설명 |
| --- | --- |
| `status` | 대화형 작성 상태입니다. 유효한 값은 `disabled`, `enabling`, `enabled`입니다. |

+++

## 비공개 엔드포인트 삭제 {#delete-private-endpoint}

개인 끝점을 삭제하려면 `/privateEndpoints`에 DELETE 요청을 하고 삭제할 끝점의 ID를 제공하십시오.

**API 형식**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | 삭제하려는 개인 엔드포인트의 ID입니다. |

**요청**

다음 요청은 ID가 `02a74b31-a566-4a86-9cea-309b101a7f24`인 개인 끝점을 삭제합니다.

+++요청 예제를 보려면 선택

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공적인 응답은 HTTP 상태 200(성공)을 반환합니다. GET 요청 및 `/privateEndpoints`을(를) 만들고 삭제된 ID를 쿼리 매개 변수로 제공하여 삭제를 확인할 수 있습니다.

## 플로우 서비스 {#flow-service}

[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)와 함께 개인 끝점을 사용하는 방법에 대한 자세한 내용은 다음 섹션을 참조하십시오.

### 개인 끝점으로 연결 만들기 {#create-base-connection}

Experience Platform에서 개인 끝점으로 연결을 만들려면 [!DNL Flow Service] API의 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /connections/
```

**요청**

다음 요청은 개인 끝점을 사용하면서 [!DNL Snowflake]에 대해 인증된 기본 연결을 만듭니다.

+++요청 예제를 보려면 선택

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 기본 연결의 이름입니다. |
| `description` | (선택 사항) 연결에 대한 추가 정보를 제공하는 설명입니다. |
| `auth.specName` | 소스를 Experience Platform에 연결하는 데 사용 중인 인증입니다. |
| `auth.params.connectionString` | [!DNL Snowflake] 연결 문자열입니다. 자세한 내용은 [[!DNL Snowflake] API 인증 안내서](../api/create/databases/snowflake.md)를 참조하십시오. |
| `auth.params.usePrivateLink` | 개인 끝점을 사용하는지 여부를 결정하는 부울 값입니다. 개인 끝점을 사용하는 경우 이 값을 `true`(으)로 설정하십시오. |
| `connectionSpec.id` | 연결 사양 ID [!DNL Snowflake]입니다. |
| `connectionSpec.version` | [!DNL Snowflake] 연결 사양 ID의 버전입니다. |

+++

**응답**

성공적인 응답은 새로 생성된 기본 연결 ID 및 etag를 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### 지정된 비공개 엔드포인트에 연결된 연결 검색 {#retrieve-connections-by-endpoint}

특정 개인 끝점에 연결된 연결을 검색하려면 `/connections` 끝점에 대한 GET 요청을 만들고 개인 끝점의 ID를 쿼리 매개 변수로 제공하십시오.

**API 형식**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| 쿼리 매개변수 | 설명 |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | 검색하려는 연결에 연결된 개인 끝점의 ID입니다. |

**요청**

다음 요청은 ID가 `02a74b31-a566-4a86-9cea-309b101a7f24`인 개인 끝점에 연결된 기존 연결을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공한 응답은 쿼리된 개인 끝점에 연결된 연결 목록을 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### 비공개 엔드포인트와 연계된 연결 검색 {#retrieve-connections}

개인 끝점과 연결된 연결을 검색하려면 `/connections` 끝점에 GET 요청을 만들고 `property=auth.params.usePrivateLink==true`을(를) 쿼리 매개 변수로 제공하십시오.

**API 형식**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**요청**

다음 요청은 비공개 끝점을 사용하는 조직의 모든 연결을 검색합니다.

+++요청 예제를 보려면 선택

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공적인 응답은 개인 끝점에 연결된 모든 연결을 반환합니다.

+++응답 예를 보려면 선택

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++