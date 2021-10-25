---
keywords: Experience Platform;홈;인기 있는 주제 API 자습서 스트리밍 대상 API; 플랫폼
solution: Experience Platform
title: Adobe Experience Platform에서 Flow Service API를 사용하여 스트리밍 대상에 연결하고 데이터를 활성화합니다
description: 이 문서에서는 Adobe Experience Platform API를 사용하여 스트리밍 대상 만들기에 대해 설명합니다
topic-legacy: tutorial
type: Tutorial
exl-id: 3e8d2745-8b83-4332-9179-a84d8c0b4400
source-git-commit: 2b1cde9fc913be4d3bea71e7d56e0e5fe265a6be
workflow-type: tm+mt
source-wordcount: '2021'
ht-degree: 2%

---

# Flow Service API를 사용하여 스트리밍 대상에 연결하고 데이터를 활성화합니다

>[!NOTE]
>
>다음 [!DNL Amazon Kinesis] 및 [!DNL Azure Event Hubs] Platform의 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

이 자습서에서는 API 호출을 사용하여 Adobe Experience Platform 데이터에 연결하고 스트리밍 클라우드 저장소 대상([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) 또는 [Azure 이벤트 허브](../catalog/cloud-storage/azure-event-hubs.md))를 편집하거나, 새로 만든 대상에 데이터 흐름을 만들고, 데이터를 새로 만든 대상에 활성화합니다.

이 자습서에서는 [!DNL Amazon Kinesis] 대상이 될 수 있지만 이 단계는 [!DNL Azure Event Hubs].

![개요 - 스트리밍 대상을 만들고 세그먼트를 활성화하는 절차](../assets/api/streaming-destination/overview.png)

Platform의 사용자 인터페이스를 사용하여 대상에 연결하고 데이터를 활성화하려면 를 참조하십시오. [대상 연결](../ui/connect-destination.md) 및 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../ui/activate-segment-streaming-destinations.md) 튜토리얼.

## 시작

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 는 Experience Platform 내의 데이터 위치 및 계열에 대한 레코드 시스템입니다.
* [샌드박스](../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Platform에서 데이터를 스트리밍 대상으로 활성화하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

이 자습서의 단계를 완료하려면 세그먼트를 연결하고 활성화할 대상 유형에 따라 다음 자격 증명이 준비되어야 합니다.

* 대상 [!DNL Amazon Kinesis] 연결: `accessKeyId`, `secretKey`, `region` 또는 `connectionUrl`
* 대상 [!DNL Azure Event Hubs] 연결: `sasKeyName`, `sasKey`, `namespace`

### 샘플 API 호출 읽기 {#reading-sample-api-calls}

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform 문제 해결 안내서에서 을 참조하십시오.

### 필수 및 선택적 헤더에 대한 값을 수집합니다 {#gather-values}

플랫폼 API를 호출하려면 먼저 를 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform의 리소스는 특정 가상 샌드박스로 분리할 수 있습니다. Platform API에 대한 요청에서 작업을 수행할 샌드박스의 이름 및 ID를 지정할 수 있습니다. 선택적 매개 변수입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### Swagger 설명서 {#swagger-docs}

Swagger에서 이 자습서에서 모든 API 호출에 대한 추가 참조 설명서를 찾을 수 있습니다. 자세한 내용은 [Adobe I/O에 대한 Flow Service API 설명서](https://www.adobe.io/experience-platform-apis/references/flow-service/). 이 자습서와 Swagger 설명서 페이지를 동시에 사용하는 것이 좋습니다.

## 사용 가능한 스트리밍 대상 목록 가져오기 {#get-the-list-of-available-streaming-destinations}

![대상 단계 개요 1단계](../assets/api/streaming-destination/step1.png)

첫 번째 단계에서는 데이터를 활성화할 스트리밍 대상을 결정해야 합니다. 시작하려면 호출을 수행하여 세그먼트를 연결하고 활성화할 수 있는 사용 가능한 대상 목록을 요청합니다. 에 다음 GET 요청을 수행합니다. `connectionSpecs` 사용 가능한 대상 목록을 반환하는 끝점:

**API 형식**

```http
GET /connectionSpecs
```

**요청**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**응답**

성공적인 응답에는 사용 가능한 대상 목록과 고유한 식별자(`id`). 추가 단계에서 필요하므로 사용할 대상의 값을 저장합니다. 예를 들어 세그먼트를 연결하고 [!DNL Amazon Kinesis] 또는 [!DNL Azure Event Hubs], 응답에서 다음 코드 조각을 찾습니다.

```json
{
    "id": "86043421-563b-46ec-8e6c-e23184711bf6",
  "name": "Amazon Kinesis",
  ...
  ...
}

{
    "id": "bf9f5905-92b7-48bf-bf20-455bc6b60a4e",
  "name": "Azure Event Hubs",
  ...
  ...
}
```

## Experience Platform 데이터에 연결 {#connect-to-your-experience-platform-data}

![대상 단계 개요 2단계](../assets/api/streaming-destination/step2.png)

다음으로, 프로필 데이터를 내보내고 선호하는 대상에서 활성화할 수 있도록 Experience Platform 데이터에 연결해야 합니다. 이 작업은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 Experience Platform에서 데이터에 대한 액세스를 승인하려면 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 소스 연결을 만드는 다른 호출을 수행하여 Experience Platform 데이터에 대한 연결을 설정합니다.


### Experience Platform에서 데이터에 대한 액세스 권한 인증

**API 형식**

```http
POST /connections
```

**요청**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```


* `{CONNECTION_SPEC_ID}`: 프로필 서비스에 연결 사양 ID 사용 - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`). 다음 단계에서 필요에 따라 이 값을 저장하여 소스 연결을 만듭니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Experience Platform 데이터에 연결 {#connect-to-platform-data}

**API 형식**

```http
POST /sourceConnections
```

**요청**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile Service",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "json"
            },
            "params" : {}
}'
```

* `{BASE_CONNECTION_ID}`: 이전 단계에서 얻은 ID를 사용합니다.
* `{CONNECTION_SPEC_ID}`: 프로필 서비스에 연결 사양 ID 사용 - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**응답**

성공적인 응답은 고유 식별자(`id`) 를 사용하도록 설정합니다. 이를 통해 Experience Platform 데이터에 성공적으로 연결되었음을 알 수 있습니다. 이 값은 이후 단계에서 필요하므로 저장합니다.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 스트리밍 대상에 연결 {#connect-to-streaming-destination}

![대상 단계 개요 3단계](../assets/api/streaming-destination/step3.png)

이 단계에서는 원하는 스트리밍 대상에 대한 연결을 설정합니다. 이 작업은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 스트리밍 대상에 대한 액세스를 승인하려면 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 대상 연결을 만드는 다른 호출을 수행합니다. 이 호출은 내보낸 데이터가 전달될 저장소 계정의 위치와 내보낼 데이터 형식을 지정합니다.

### 스트리밍 대상에 대한 액세스 권한 인증

**API 형식**

```http
POST /connections
```

**요청**

>[!IMPORTANT]
>
>아래 예에는 `//`. 이러한 주석에서는 서로 다른 스트리밍 대상에 서로 다른 값을 사용해야 하는 위치를 강조 표시합니다. 코드 조각을 사용하기 전에 설명을 제거하십시오.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connection for Amazon Kinesis/ Azure Event Hubs",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "{_CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "auth": {
        "specName": "{AUTHENTICATION_CREDENTIALS}",
        "params": { // use these values for Amazon Kinesis connections
            "accessKeyId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}",
            "region": "{REGION}"
        },
        "params": { // use these values for Azure Event Hubs connections
            "sasKeyName": "{SAS_KEY_NAME}",
            "sasKey": "{SAS_KEY}",
            "namespace": "{EVENT_HUB_NAMESPACE}"
        }        
    }
}'
```

* `{CONNECTION_SPEC_ID}`: 단계에서 얻은 연결 사양 ID를 사용합니다 [사용 가능한 대상 목록 가져오기](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`: 스트리밍 대상의 이름을 입력합니다. `Aws Kinesis authentication credentials` 또는 `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *대상 [!DNL Amazon Kinesis] 연결.* Amazon Kinesis 저장소 위치에 대한 액세스 ID입니다.
* `{SECRET_KEY}`: *대상 [!DNL Amazon Kinesis] 연결.* Amazon Kinesis 저장소 위치의 암호 키입니다.
* `{REGION}`: *대상 [!DNL Amazon Kinesis] 연결.* 귀하의 지역 [!DNL Amazon Kinesis] Platform이 데이터를 스트리밍할 계정.
* `{SAS_KEY_NAME}`: *대상 [!DNL Azure Event Hubs] 연결.* SAS 키 이름을 입력합니다. 인증 방법에 대해 알아보기 [!DNL Azure Event Hubs] SAS 키를 사용하여 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{SAS_KEY}`: *대상 [!DNL Azure Event Hubs] 연결.* SAS 키를 입력합니다. 인증 방법에 대해 알아보기 [!DNL Azure Event Hubs] SAS 키를 사용하여 [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* `{EVENT_HUB_NAMESPACE}`: *대상 [!DNL Azure Event Hubs] 연결.* 을 입력합니다. [!DNL Azure Event Hubs] platform이 데이터를 스트리밍할 네임스페이스입니다. 자세한 내용은 [이벤트 허브 네임스페이스 만들기](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace) 에서 [!DNL Microsoft] 설명서.

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`). 다음 단계에서 필요에 따라 이 값을 저장하여 대상 연결을 만듭니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 저장소 위치 및 데이터 형식 지정

**API 형식**

```http
POST /targetConnections
```

**요청**

>[!IMPORTANT]
>
>아래 예에는 `//`. 이러한 주석에서는 서로 다른 스트리밍 대상에 서로 다른 값을 사용해야 하는 위치를 강조 표시합니다. 코드 조각을 사용하기 전에 설명을 제거하십시오.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Amazon Kinesis/ Azure Event Hubs target connection",
    "description": "Connection to Amazon Kinesis/ Azure Event Hubs",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "{CONNECTION_SPEC_ID}",
        "version": "1.0"
    },
    "data": {
        "format": "json"
    },
    "params": { // use these values for Amazon Kinesis connections
        "stream": "{NAME_OF_DATA_STREAM}", 
        "region": "{REGION}"
    },
    "params": { // use these values for Azure Event Hubs connections
        "eventHubName": "{EVENT_HUB_NAME}"
    }
}'
```

* `{BASE_CONNECTION_ID}`: 위의 단계에서 얻은 기본 연결 ID를 사용합니다.
* `{CONNECTION_SPEC_ID}`: 단계에서 얻은 연결 사양을 사용합니다 [사용 가능한 대상 목록 가져오기](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *대상 [!DNL Amazon Kinesis] 연결.* 에 기존 데이터 스트림의 이름을 입력합니다 [!DNL Amazon Kinesis] 계정이 필요합니다. Platform에서 데이터를 이 스트림으로 내보냅니다.
* `{REGION}`: *대상 [!DNL Amazon Kinesis] 연결.* Platform이 데이터를 스트리밍할 Amazon Kinesis 계정의 영역입니다.
* `{EVENT_HUB_NAME}`: *대상 [!DNL Azure Event Hubs] 연결.* 을 입력합니다. [!DNL Azure Event Hub] Platform이 데이터를 스트리밍할 위치에 이름을 지정합니다. 자세한 내용은 [이벤트 허브 만들기](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) 에서 [!DNL Microsoft] 설명서.

**응답**

성공적인 응답은 고유 식별자(`id`)를 추가하여 새로 만든 스트리밍 대상에 연결할 수 있습니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 데이터 흐름 만들기

![대상 단계 개요 4단계](../assets/api/streaming-destination/step4.png)

이제 이전 단계에서 얻은 ID를 사용하여 Experience Platform 데이터와 데이터를 활성화할 대상 사이에 데이터 흐름을 만들 수 있습니다. 이 단계는 나중에 데이터가 Experience Platform과 원하는 대상 간에 이동하는 파이프라인을 구성하는 것으로 생각해 보십시오.

데이터 흐름을 만들려면 페이로드 내에서 아래에 언급된 값을 제공하면서 아래 표시된 대로 POST 요청을 수행하십시오.

데이터 흐름을 만들려면 다음 POST 요청을 수행하십시오.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {IMS_ORG}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
  "name": "Azure Event Hubs",
  "description": "Azure Event Hubs",
  "flowSpec": {
    "id": "{FLOW_SPEC_ID}",
    "version": "1.0"
  },
  "sourceConnectionIds": [
    "{SOURCE_CONNECTION_ID}"
  ],
  "targetConnectionIds": [
    "{TARGET_CONNECTION_ID}"
  ],
  "transformations": [
    {
      "name": "GeneralTransform",
      "params": {
        "profileSelectors": {
          "selectors": [
            
          ]
        },
        "segmentSelectors": {
          "selectors": [
            
          ]
        }
      }
    }
  ]
}
```

* `{FLOW_SPEC_ID}`: 프로필 기반 대상의 흐름 사양 ID는 다음과 같습니다 `71471eba-b620-49e4-90fd-23f1fa0174d8`. 호출에서 이 값을 사용합니다.
* `{SOURCE_CONNECTION_ID}`: 단계에서 얻은 소스 연결 ID를 사용합니다 [Experience Platform에 연결](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`: 단계에서 얻은 대상 연결 ID를 사용합니다 [스트리밍 대상에 연결](#connect-to-streaming-destination).

**응답**

성공적인 응답은 ID(`id`)을 만들 수 있습니다 `etag`. 두 값을 모두 메모하십시오. 다음 단계에서 이러한 세그먼트를 활성화하여 세그먼트를 활성화합니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 새 대상에 데이터 활성화 {#activate-data}

![대상 단계 개요 5단계](../assets/api/streaming-destination/step5.png)

모든 연결 및 데이터 흐름을 만들었으므로 이제 프로필 데이터를 스트리밍 플랫폼으로 활성화할 수 있습니다. 이 단계에서 대상에 전송하는 세그먼트 및 프로필 속성을 선택하고 데이터를 예약하고 대상에 보낼 수 있습니다.

세그먼트를 새 대상에 활성화하려면 아래 예와 같이 JSON PATCH 작업을 수행해야 합니다. 한 번의 호출로 여러 세그먼트와 프로필 속성을 활성화할 수 있습니다. JSON PATCH에 대해 자세히 알아보려면 [RFC 사양](https://tools.ietf.org/html/rfc6902).

**API 형식**

```http
PATCH /flows
```

**요청**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/transformations/0/params/segmentSelectors/selectors/-",
    "value": {
      "type": "PLATFORM_SEGMENT",
      "value": {
        "name": "Name of the segment that you are activating",
        "description": "Description of the segment that you are activating",
        "id": "{SEGMENT_ID}"
      }
    }
  },
  {
    "op": "add",
    "path": "/transformations/0/params/profileSelectors/selectors/-",
    "value": {
      "type": "JSON_PATH",
      "value": {
        "operator": "EXISTS",
        "path": "{PROFILE_ATTRIBUTE}"
      }
    }
  }
]
```

* `{DATAFLOW_ID}`: 이전 단계에서 얻은 데이터 흐름을 사용합니다.
* `{ETAG}`: 이전 단계에서 얻은 태그를 사용합니다.
* `{SEGMENT_ID}`: 이 대상으로 내보낼 세그먼트 ID를 제공합니다. 활성화할 세그먼트의 세그먼트 ID를 검색하려면 다음 위치로 이동하십시오. **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**, 선택 **[!UICONTROL 세그멘테이션 서비스 API]** 왼쪽 탐색 메뉴에서 `GET /segment/definitions` 작업 **[!UICONTROL 세그먼트 정의]**.
* `{PROFILE_ATTRIBUTE}`: 예, `personalEmail.address` 또는 `person.lastName`

**응답**

202 OK 응답을 찾습니다. 응답 본문이 반환되지 않습니다. 요청이 올바른지 확인하려면 다음 단계인 데이터 흐름 유효성 검사를 참조하십시오.

## 데이터 흐름 유효성 검사

![대상 단계 개요 6단계](../assets/api/streaming-destination/step6.png)

자습서의 마지막 단계에서는 세그먼트 및 프로필 속성이 데이터 플로우에 올바르게 매핑되었는지 확인해야 합니다.

유효성을 검사하려면 다음 GET 요청을 수행합니다.

**API 형식**

```http
GET /flows
```

**요청**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: 이전 단계의 데이터 흐름을 사용합니다.
* `{ETAG}`: 이전 단계의 태그를 사용합니다.

**응답**

반환된 응답에는 `transformations` 매개 변수 이전 단계에서 제출한 세그먼트 및 프로필 속성을 지정합니다. 샘플 `transformations` 응답의 매개 변수는 다음과 같을 수 있습니다.

```json
"transformations": [
    {
        "name": "GeneralTransform",
        "params": {
            "profileSelectors": {
                        "selectors": [
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "personalEmail.address",
                                    "operator": "EXISTS"
                                }
                            },
                            {
                                "type": "JSON_PATH",
                                "value": {
                                    "path": "person.lastname",
                                    "operator": "EXISTS"
                                }
                            }
                        ]
                    },
            "segmentSelectors": {
                "selectors": [
                    {
                        "type": "PLATFORM_SEGMENT",
                        "value": {
                            "name": "Men over 50",
                            "description": "",
                            "id": "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02"
                        }
                    }
                ]
            }
        }
    }
],
```

**내보낸 데이터**

>[!IMPORTANT]
>
> 단계의 프로필 속성 및 세그먼트 외에 [새 대상에 데이터 활성화](#activate-data), 내보낸 데이터를에서 [!DNL AWS Kinesis] 및 [!DNL Azure Event Hubs] 또한 id 맵에 대한 정보가 포함됩니다. 내보낸 프로필의 ID를 나타냅니다(예: [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), 모바일 ID, Google ID, 이메일 주소 등) 아래 예를 참조하십시오.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "72ddd79b-6b0a-4e97-a8d2-112ccd81bd02": {
        "lastQualificationTime": "2020-03-03T21:24:39Z",
        "status": "exited"
      },
      "7841ba61-23c1-4bb3-a495-00d695fe1e93": {
        "lastQualificationTime": "2020-03-04T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```

## Postman 컬렉션을 사용하여 스트리밍 대상에 연결  {#collections}

이 자습서에 설명된 스트리밍 대상에 보다 능률적인 방법으로 연결하려면 [[!DNL Postman]](https://www.postman.com/).

[!DNL Postman] 는 API를 호출하고 사전 정의된 호출 및 환경의 라이브러리를 관리하는 데 사용할 수 있는 도구입니다.

이 특정 자습서에 대해 다음을 수행하십시오 [!DNL Postman] 컬렉션이 첨부되었습니다.

* [!DNL AWS Kinesis] [!DNL Postman] 컬렉션
* [!DNL Azure Event Hubs] [!DNL Postman] 컬렉션

클릭 [여기](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 컬렉션 아카이브를 다운로드하려면 다음을 수행하십시오.

각 컬렉션에는 [!DNL AWS Kinesis], 및 [!DNL Azure Event Hub]각각 입니다.

### Postman 컬렉션을 사용하는 방법

첨부된 항목을 사용하여 대상에 성공적으로 연결하려면 [!DNL Postman] 컬렉션, 다음 단계를 수행합니다.

* 다운로드 및 설치 [!DNL Postman];
* [다운로드](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 연결된 컬렉션의 압축을 해제합니다.
* 해당 폴더의 컬렉션을 Postman으로 가져옵니다.
* 이 문서의 지침에 따라 환경 변수를 입력합니다.
* 를 실행합니다. [!DNL API] 이 문서의 지침에 따라 Postman의 요청을 참조하십시오.

## 다음 단계

이 자습서를 따라 선호하는 스트리밍 대상 중 하나에 플랫폼을 연결하고 각 대상에 데이터 흐름을 설정했습니다. 이제 발신 데이터를 대상 고객 분석 또는 수행하려는 기타 데이터 작업에서 사용할 수 있습니다. 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
