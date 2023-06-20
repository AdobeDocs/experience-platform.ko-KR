---
title: 흐름 서비스 API를 사용하여 Azure Event Hubs 소스 연결 만들기
description: 흐름 서비스 API를 사용하여 Adobe Experience Platform을 Azure Event Hubs 계정에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---

# 만들기 [!DNL Azure Event Hubs] 를 사용한 소스 연결 [!DNL Flow Service] API

>[!IMPORTANT]
>
>다음 [!DNL Azure Event Hubs] 소스는 Real-time Customer Data Platform Ultimate를 구매한 사용자에게 소스 카탈로그에서 사용할 수 있습니다.

이 자습서에서는 연결하는 단계를 안내합니다 [!DNL Azure Event Hubs] (이하 &quot;라고 한다)[!DNL Event Hubs]&quot;) Experience Platform 대상, 사용 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

- [소스](../../../../home.md): [!DNL Experience Platform] 를 사용하여 수신 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
- [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 만드는 가상 샌드박스를 제공합니다. [!DNL Platform] 인스턴스를 별도의 가상 환경으로 전환하여 디지털 경험 애플리케이션을 개발하고 발전시킵니다.

다음 섹션은 성공적으로 연결하기 위해 알아야 하는 추가 정보를 제공합니다 [!DNL Event Hubs] 를 사용하여 플랫폼으로 [!DNL Flow Service] API.

### 필요한 자격 증명 수집

주문 [!DNL Flow Service] 을(를) 사용하여 [!DNL Event Hubs] 계정, 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `sasKey` | 의 기본 키 [!DNL Event Hubs] 네임스페이스입니다. 다음 `sasPolicy` 해당 `sasKey` 은(는) 다음을 포함해야 합니다. `manage` 에 대해 순서대로 구성된 권한 [!DNL Event Hubs] 채울 목록입니다. |
| `namespace` | 의 네임스페이스 [!DNL Event Hubs] 에 액세스하고 있습니다. An [!DNL Event Hubs] 네임스페이스는 하나 이상을 만들 수 있는 고유한 범위 컨테이너를 제공합니다 [!DNL Event Hubs]. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 만들기와 관련된 인증 사양을 포함하여 소스의 커넥터 속성을 반환합니다. 다음 [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

이러한 값에 대한 자세한 내용은 [이 이벤트 허브 문서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

### Platform API 사용

Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../../landing/api-guide.md).

## 기본 연결 만들기

소스 연결을 만드는 첫 번째 단계는 [!DNL Event Hubs] 소스 및 기본 연결 ID 생성. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

POST 기본 연결 ID를 만들려면 `/connections` 을(를) 제공하는 동안 엔드포인트 [!DNL Event Hubs] 요청 매개 변수의 일부로 인증 자격 증명을 사용합니다.

**API 형식**

```http
POST /connections
```

**요청**

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
| `auth.params.namespace` | 의 네임스페이스 [!DNL Event Hubs] 에 액세스하고 있습니다. |
| `connectionSpec.id` | 다음 [!DNL Event Hubs] 연결 사양 ID: `bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**응답**

성공한 응답은 고유 식별자를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다(`id`). 다음 단계에서 소스 연결을 만들려면 이 연결 ID가 필요합니다.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 소스 연결 만들기

소스 연결은 데이터가 수집되는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 소스, 데이터 형식 및 데이터 흐름을 만드는 데 필요한 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 조직에만 해당됩니다.

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
            "eventHubName": "{EVENTHUB_NAME}",
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
| `baseConnectionId` | 의 연결 ID [!DNL Event Hubs] 이전 단계에서 생성된 소스. |
| `connectionSpec.id` | 의 고정 연결 사양 ID [!DNL Event Hubs]. 이 ID는 `bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |
| `data.format` | 형식 [!DNL Event Hubs] 수집할 데이터. 현재 지원되는 데이터 형식은 `json`. |
| `params.eventHubName` | 에 대한 이름 [!DNL Event Hubs] 소스. |
| `params.dataType` | 이 매개 변수는 수집되는 데이터의 유형을 정의합니다. 지원되는 데이터 유형은 다음과 같습니다. `raw` 및 `xdm`. |
| `params.reset` | 이 매개 변수는 데이터를 읽는 방법을 정의합니다. 사용 `latest` 최신 데이터에서 읽기를 시작하고 `earliest` 스트림에서 사용 가능한 첫 번째 데이터에서 읽기를 시작합니다. 이 매개 변수는 선택 사항이며 기본값은 입니다. `earliest` 제공되지 않는 경우 |
| `params.consumerGroup` | 에 사용할 게시 또는 구독 메커니즘 [!DNL Event Hubs]. 이 매개 변수는 선택 사항이며 기본값은 입니다. `$Default` 제공되지 않는 경우 다음을 참조하십시오. [[!DNL Event Hubs] 이벤트 소비자에 대한 안내서](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers) 추가 정보. |

## 다음 단계

이 자습서를 따라 [!DNL Event Hubs] 를 사용한 소스 연결 [!DNL Flow Service] API. 다음 자습서에서 이 소스 연결 ID를 사용하여 다음을 수행할 수 있습니다. [다음을 사용하여 스트리밍 데이터 흐름 만들기 [!DNL Flow Service] API](../../collect/streaming.md).
