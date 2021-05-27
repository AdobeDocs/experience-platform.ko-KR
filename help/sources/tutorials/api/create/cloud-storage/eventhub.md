---
keywords: Experience Platform;홈;인기 항목;이벤트 허브;Azure 이벤트 허브;이벤트 허브
solution: Experience Platform
title: Flow Service API를 사용하여 Azure 이벤트 허브 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: 플로우 서비스 API를 사용하여 Adobe Experience Platform을 Azure 이벤트 허브 계정에 연결하는 방법을 알아봅니다.
exl-id: a4d0662d-06e3-44f3-8cb7-4a829c44f4d9
source-git-commit: 091f6751f4377a25844328ce924f3c33899b3344
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 1%

---


# [!DNL Flow Service] API를 사용하여 [!DNL Azure Event Hubs] 소스 연결을 만듭니다

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용하여 [!DNL Azure Event Hubs](이하 &quot;[!DNL Event Hubs]&quot;라 함)을 Experience Platform에 연결하는 단계를 안내합니다.

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

- [소스](../../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
- [샌드박스](../../../../../sandboxes/home.md): [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 [!DNL Event Hubs]을 Platform에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

[!DNL Flow Service]이 [!DNL Event Hubs] 계정에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `sasKeyName` | SAS 키 이름이라고도 하는 인증 규칙의 이름입니다. |
| `sasKey` | 생성된 공유 액세스 서명. |
| `namespace` | 액세스하는 [!DNL Event Hubs]의 네임스페이스입니다. [!DNL Event Hubs] 네임스페이스는 하나 이상의 [!DNL Event Hubs]을(를) 만들 수 있는 고유한 범위 컨테이너를 제공합니다. |
| `connectionSpec.id` | 연결 사양은 기본 및 소스 연결 생성과 관련된 인증 사양이 포함된 소스의 커넥터 등록 정보를 반환합니다. [!DNL Event Hubs] 연결 사양 ID는 다음과 같습니다.`bf9f5905-92b7-48bf-bf20-455bc6b60a4e`. |

이러한 값에 대한 자세한 내용은 [이 이벤트 허브 문서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)를 참조하십시오.

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 기본 연결 만들기

소스 연결을 만드는 첫 번째 단계는 [!DNL Event Hubs] 소스를 인증하고 기본 연결 ID를 생성하는 것입니다. 기본 연결 ID를 사용하면 소스 내에서 파일을 탐색 및 탐색하고 해당 데이터 유형 및 형식에 대한 정보를 포함하여 수집할 특정 항목을 식별할 수 있습니다.

기본 연결 ID를 만들려면 요청 매개 변수의 일부로 [!DNL Event Hubs] 인증 자격 증명을 제공하는 동안 `/connections` 끝점에 POST 요청을 하십시오.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.sasKey` | 생성된 공유 액세스 서명. |
| `auth.params.namespace` | 액세스하는 [!DNL Event Hubs]의 네임스페이스입니다. |
| `connectionSpec.id` | [!DNL Event Hubs] 연결 사양 ID는 다음과 같습니다.`bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |

**응답**

성공적인 응답은 고유 식별자(`id`)를 포함하여 새로 생성된 기본 연결의 세부 정보를 반환합니다. 이 연결 ID는 소스 연결을 만들려면 다음 단계에서 필요합니다.

```json
{
    "id": "4cdbb15c-fb1e-46ee-8049-0f55b53378fe",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## 소스 연결 만들기

소스 연결은 데이터를 수집하는 외부 소스와의 연결을 만들고 관리합니다. 소스 연결은 데이터 흐름을 만드는 데 필요한 데이터 소스, 데이터 형식 및 소스 연결 ID와 같은 정보로 구성됩니다. 소스 연결 인스턴스는 테넌트 및 IMS 조직에 따라 다릅니다.

소스 연결을 만들려면 [!DNL Flow Service] API의 `/sourceConnections` 종단점에 대해 POST 요청을 수행하십시오.

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
    -H 'x-gw-ims-org-id: {IMS_Org}' \
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
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 포함하도록 제공할 수 있는 선택적 값입니다. |
| `baseConnectionId` | 이전 단계에서 생성된 [!DNL Event Hubs] 소스의 연결 ID입니다. |
| `connectionSpec.id` | [!DNL Event Hubs]에 대한 고정 연결 사양 ID입니다. 이 ID는 입니다.`bf9f5905-92b7-48bf-bf20-455bc6b60a4e` |
| `data.format` | 수집할 [!DNL Event Hubs] 데이터의 형식입니다. 현재 지원되는 데이터 형식은 `json`뿐입니다. |
| `params.eventHubName` | [!DNL Event Hubs] 소스의 이름입니다. |
| `params.dataType` | 이 매개 변수는 수집할 데이터의 유형을 정의합니다. 지원되는 데이터 유형은 다음과 같습니다.`raw` 및 `xdm` |
| `params.reset` | 이 매개 변수는 데이터를 읽는 방법을 정의합니다. `latest` 을 사용하여 가장 최근 데이터에서 읽기를 시작하고 `earliest` 을 사용하여 스트림에서 사용 가능한 첫 번째 데이터에서 읽기를 시작합니다. 이 매개 변수는 선택 사항이며 지정하지 않은 경우 기본값은 `earliest` 입니다. |
| `params.consumerGroup` | [!DNL Event Hubs]에 사용할 게시 또는 구독 메커니즘입니다. 이 매개 변수는 선택 사항이며 지정하지 않은 경우 기본값은 `$Default` 입니다. 자세한 내용은 이벤트 소비자](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-features#event-consumers)에 대한 이 [[!DNL Event Hubs] 안내서를 참조하십시오. |

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 [!DNL Event Hubs] 소스 연결을 만들었습니다. 이 소스 연결 ID는 [API](../../collect/streaming.md)를 사용하여 스트리밍 데이터 흐름을 만드는 다음 자습서에서 사용할 수 있습니다. [!DNL Flow Service] 
