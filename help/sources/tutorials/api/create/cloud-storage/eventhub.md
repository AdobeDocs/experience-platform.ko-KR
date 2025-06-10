---
title: 흐름 서비스 API를 사용하여 Azure Event Hubs Source 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Azure Event Hubs 계정에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 [!DNL Azure Event Hubs] 소스 연결 만들기

>[!IMPORTANT]
>
>[!DNL Azure Event Hubs] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)을(를) 사용하여 [!DNL Azure Event Hubs]&#x200B;(이하 &quot;[!DNL Event Hubs]&quot;)을(를) Experience Platform에 연결하는 방법을 알아보려면 이 자습서를 읽어 보십시오.

## 시작

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

- [원본](../../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
- [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Event Hubs]을(를) Experience Platform에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이(가) [!DNL Event Hubs] 계정에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 표준 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `sasKey` | [!DNL Event Hubs] 네임스페이스의 기본 키입니다. [!DNL Event Hubs] 목록을 채우려면 `sasKey`에 해당하는 `sasPolicy`에 `manage` 권한이 구성되어 있어야 합니다. |
| `namespace` | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

>[!TAB SAS 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `sasKey` | [!DNL Event Hubs] 네임스페이스의 기본 키입니다. [!DNL Event Hubs] 목록을 채우려면 `sasKey`에 해당하는 `sasPolicy`에 `manage` 권한이 구성되어 있어야 합니다. |
| `namespace` | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |
| `eventHubName` | [!DNL Azure Event Hub] 이름을 입력하십시오. [!DNL Event Hub] 이름에 대한 자세한 내용은 [Microsoft 설명서](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)를 참조하십시오. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

[!DNL Event Hubs]의 SAS(공유 액세스 서명) 인증에 대한 자세한 내용은 [[!DNL Azure] SAS 사용 가이드](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)를 참조하십시오.

>[!TAB 이벤트 허브 Azure Active Directory 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `tenantId` | 권한을 요청하려는 테넌트 ID입니다. 테넌트 ID는 GUID 또는 친숙한 이름으로 포맷할 수 있습니다. **참고**: 테넌트 ID는 [!DNL Microsoft Azure] 인터페이스에서 &quot;디렉터리 ID&quot;라고 합니다. |
| `clientId` | 앱에 할당된 애플리케이션 ID입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 이 ID를 검색할 수 있습니다. |
| `clientSecretValue` | 앱을 인증하기 위해 클라이언트 ID와 함께 사용되는 클라이언트 암호입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 클라이언트 암호를 검색할 수 있습니다. |
| `namespace` | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |

[!DNL Azure Active Directory]에 대한 자세한 내용은 [Microsoft Entra ID 사용에 대한 Azure 안내서](https://learn.microsoft.com/en-us/azure/healthcare-apis/register-application)를 참조하세요.

>[!TAB 이벤트 허브에서 Azure Active Directory 인증 범위를 지정함]

| 자격 증명 | 설명 |
| --- | --- |
| `tenantId` | 권한을 요청하려는 테넌트 ID입니다. 테넌트 ID는 GUID 또는 친숙한 이름으로 포맷할 수 있습니다. **참고**: 테넌트 ID는 [!DNL Microsoft Azure] 인터페이스에서 &quot;디렉터리 ID&quot;라고 합니다. |
| `clientId` | 앱에 할당된 애플리케이션 ID입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 이 ID를 검색할 수 있습니다. |
| `clientSecretValue` | 앱을 인증하기 위해 클라이언트 ID와 함께 사용되는 클라이언트 암호입니다. [!DNL Azure Active Directory]을(를) 등록한 [!DNL Microsoft Entra ID] 포털에서 클라이언트 암호를 검색할 수 있습니다. |
| `namespace` | 액세스 중인 [!DNL Event Hub]의 네임스페이스입니다. [!DNL Event Hub] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |
| `eventHubName` | [!DNL Azure Event Hub] 이름을 입력하십시오. [!DNL Event Hub] 이름에 대한 자세한 내용은 [Microsoft 설명서](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)를 참조하십시오. |

>[!ENDTABS]

이러한 값에 대한 자세한 내용은 [이 이벤트 허브 문서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)를 참조하세요.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 기본 연결 만들기

>[!TIP]
>
>만든 후에는 [!DNL Event Hubs] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

원본 연결을 만드는 첫 번째 단계는 [!DNL Event Hubs] 원본을 인증하고 기본 연결 ID를 생성하는 것입니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 [!DNL Event Hubs] 인증 자격 증명을 요청 매개 변수의 일부로 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

**API 형식**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 표준 인증]

표준 인증을 사용하여 계정을 만들려면 `sasKeyName`, `sasKey` 및 `namespace`에 대한 값을 제공하는 동안 `/connections` 끝점에 대한 POST 요청을 만듭니다.

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}"
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `auth.params.sasKey` | 생성된 공유 액세스 서명입니다. |
| `auth.params.namespace` | 액세스 중인 [!DNL Event Hubs]의 네임스페이스입니다. |
| `connectionSpec.id` | [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++응답

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 연결 ID가 필요합니다.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB SAS 인증]

SAS 인증을 사용하여 계정을 만들려면 `sasKeyName`, `sasKey`, `namespace` 및 `eventHubName`에 대한 값을 제공하는 동안 `/connections` 끝점에 POST 요청을 만듭니다.

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Azure EventHub authentication credentials",
          "params": {
              "sasKeyName": "{SAS_KEY_NAME}",
              "sasKey": "{SAS_KEY}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME} 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `auth.params.sasKey` | 생성된 공유 액세스 서명입니다. |
| `auth.params.namespace` | 액세스 중인 [!DNL Event Hubs]의 네임스페이스입니다. |
| `params.eventHubName` | [!DNL Event Hubs] 소스의 이름입니다. |
| `connectionSpec.id` | [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++응답

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 연결 ID가 필요합니다.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB 이벤트 허브 Azure Active Directory 인증]

Azure Active Directory 인증을 사용하여 계정을 만들려면 `tenantId`, `clientId`, `clientSecretValue` 및 `namespace`에 대한 값을 제공하는 동안 `/connections` 끝점에 POST 요청을 만듭니다.

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.tenantId` | 애플리케이션의 테넌트 ID입니다. **참고**: 테넌트 ID는 [!DNL Microsoft Azure] 인터페이스에서 &quot;디렉터리 ID&quot;라고 합니다. |
| `auth.params.clientId` | 조직의 클라이언트 ID입니다. |
| `auth.params.clientSecretValue` | 조직의 클라이언트 암호 값입니다. |
| `auth.params.namespace` | 액세스 중인 [!DNL Event Hubs]의 네임스페이스입니다. |
| `connectionSpec.id` | [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++응답

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 연결 ID가 필요합니다.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!TAB 이벤트 허브에서 Azure Active Directory 인증 범위를 지정함]

Azure Active Directory 인증을 사용하여 계정을 만들려면 `tenantId`, `clientId`, `clientSecretValue`, `namespace` 및 `eventHubName`에 대한 값을 제공하는 동안 `/connections` 끝점에 POST 요청을 만듭니다.

+++요청

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Event Hubs connection",
      "description": "Connector for Azure Event Hubs",
      "auth": {
          "specName": "Event Hub Scoped Azure Active Directory Auth",
          "params": {
              "tenantId": "{TENANT_ID}",
              "clientId": "{CLIENT_ID}",
              "clientSecretValue": "{CLIENT_SECRET_VALUE}",
              "namespace": "{NAMESPACE}",
              "eventHubName": "{EVENT_HUB_NAME}" 
          }
      },
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `auth.params.tenantId` | 애플리케이션의 테넌트 ID입니다. **참고**: 테넌트 ID는 [!DNL Microsoft Azure] 인터페이스에서 &quot;디렉터리 ID&quot;라고 합니다. |
| `auth.params.clientId` | 조직의 클라이언트 ID입니다. |
| `auth.params.clientSecretValue` | 조직의 클라이언트 암호 값입니다. |
| `auth.params.namespace` | 액세스 중인 [!DNL Event Hubs]의 네임스페이스입니다. |
| `auth.params.eventHubName` | [!DNL Event Hubs] 소스의 이름입니다. |
| `connectionSpec.id` | [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

+++

+++응답

성공한 응답은 고유 식별자(`id`)를 포함하여 새로 만든 기본 연결의 세부 정보를 반환합니다. 다음 단계에서 소스 연결을 만들려면 이 연결 ID가 필요합니다.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

+++

>[!ENDTABS]

## 소스 연결 만들기

>[!TIP]
>
>[!DNL Event Hubs] 소비자 그룹은 지정된 시간에 단일 흐름에만 사용할 수 있습니다.

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 소스, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

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
      "name": "Azure Event Hubs source connection",
      "description": "A source connection for Azure Event Hubs",
      "baseConnectionId": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
      "connectionSpec": {
          "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      },
      "params": {
          "eventHubName": "{EVENT_HUB_NAME}",
          "dataType": "raw",
          "reset": "latest",
          "consumerGroup": "{CONSUMER_GROUP}"
      }
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회할 때 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 포함하도록 제공할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 이전 단계에서 생성된 [!DNL Event Hubs] 소스의 연결 ID입니다. |
| `connectionSpec.id` | [!DNL Event Hubs]에 대한 고정 연결 사양 ID입니다. 이 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | 수집할 [!DNL Event Hubs] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |
| `params.eventHubName` | [!DNL Event Hubs] 소스의 이름입니다. |
| `params.dataType` | 이 매개 변수는 수집되는 데이터의 유형을 정의합니다. 지원되는 데이터 형식은 `raw` 및 `xdm`입니다. |
| `params.reset` | 이 매개 변수는 데이터를 읽는 방법을 정의합니다. `latest`을(를) 사용하여 가장 최근 데이터에서 읽기를 시작하고 `earliest`을(를) 사용하여 스트림에서 사용 가능한 첫 번째 데이터에서 읽기를 시작합니다. 이 매개 변수는 선택 사항이며 지정하지 않은 경우 기본값은 `earliest`입니다. |
| `params.consumerGroup` | [!DNL Event Hubs]에 사용할 게시 또는 구독 메커니즘입니다. 이 매개 변수는 선택 사항이며 지정하지 않은 경우 기본값은 `$Default`입니다. 자세한 내용은 이 [[!DNL Event Hubs] 이벤트 소비자 가이드](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers)를 참조하세요. **참고**: [!DNL Event Hubs] 소비자 그룹은 지정된 시간에 단일 흐름에만 사용할 수 있습니다. |

>[!NOTE]
>
>스트리밍 데이터 흐름을 만들거나 업데이트한 후 데이터 손실 또는 데이터 감소의 잠재적 인스턴스를 방지하기 위해 데이터 수집에서 5분 정도의 짧은 일시 중지가 필요합니다.

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Event Hubs] 소스 연결을 만들었습니다. 다음 자습서에서 이 원본 연결 ID를 사용하여 [API를 사용하여 스트리밍 데이터 흐름을 만들 [!DNL Flow Service] 수 있습니다](../../collect/streaming.md).
