---
keywords: Experience Platform;home;popular topicsAPI 자습서;스트리밍 대상 API;플랫폼
solution: Experience Platform
title: Adobe Experience Platform에서 API 호출을 사용하여 스트리밍 대상에 연결하고 데이터 활성화
description: 이 문서에서는 Adobe Experience Platform API를 사용하여 스트리밍 대상을 만드는 방법에 대해 설명합니다
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '2021'
ht-degree: 1%

---


# 스트리밍 대상에 연결하고 API 호출을 사용하여 데이터 활성화

>[!NOTE]
>
>플랫폼의 [!DNL Amazon Kinesis] 및 [!DNL Azure Event Hubs] 대상은 현재 베타 상태입니다. 설명서 및 기능은 변경될 수 있습니다.

이 자습서에서는 API 호출을 사용하여 Adobe Experience Platform 데이터에 연결하고, 스트리밍 클라우드 저장소 대상에 대한 연결을 만들고([Amazon Kinesis](../catalog/cloud-storage/amazon-kinesis.md) 또는 [Azure 이벤트 허브](../catalog/cloud-storage/azure-event-hubs.md)), 새로 만든 대상에 데이터 흐름을 만들고, 새 만든 대상에 데이터를 활성화하는 방법을 보여 줍니다.

이 자습서는 모든 예에서 [!DNL Amazon Kinesis] 대상을 사용하지만 이 단계는 [!DNL Azure Event Hubs]에 대해 동일합니다.

![개요 - 스트리밍 대상을 만들고 세그먼트를 활성화하는 절차](../assets/api/streaming-destination/overview.png)

플랫폼의 사용자 인터페이스를 사용하여 대상에 연결하고 데이터를 활성화하려면 [대상 연결](../ui/connect-destination.md) 및 [프로필 및 세그먼트를 대상](../ui/activate-destinations.md) 튜토리얼로 활성화를 참조하십시오.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Catalog Service]](../../catalog/home.md): [!DNL Catalog] 는 Experience Platform 내의 데이터 위치 및 리니지에 대한 기록 시스템입니다.
* [샌드박스](../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 플랫폼의 스트리밍 대상으로 데이터를 활성화하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

이 자습서의 단계를 완료하려면 세그먼트를 연결하고 활성화할 대상 유형에 따라 다음 자격 증명이 준비되어야 합니다.

* [!DNL Amazon Kinesis] 연결의 경우:`accessKeyId`, `secretKey`, `region` 또는 `connectionUrl`
* [!DNL Azure Event Hubs] 연결의 경우:`sasKeyName`, `sasKey`, `namespace`

### 샘플 API 호출 읽기{#reading-sample-api-calls}

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법을 참조하십시오.

### 필수 및 선택적 헤더 {#gather-values} 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 인증:Bearer `{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

Experience Platform의 리소스는 특정 가상 샌드박스로 분리할 수 있습니다. 플랫폼 API에 대한 요청에서 작업을 수행할 샌드박스의 이름과 ID를 지정할 수 있습니다. 선택적 매개 변수입니다.

* x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

### Swagger 설명서 {#swagger-docs}

이 자습서에서는 Swagger에서 모든 API 호출에 대한 참조 설명서를 찾을 수 있습니다. Adobe.io](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)에 대한 [Flow Service API 설명서를 참조하십시오. 이 자습서와 Swagger 설명서 페이지를 동시에 사용하는 것이 좋습니다.

## 사용 가능한 스트리밍 대상 목록 {#get-the-list-of-available-streaming-destinations} 가져오기

![대상 단계 개요 단계 1](../assets/api/streaming-destination/step1.png)

첫 번째 단계로 데이터를 활성화할 스트리밍 대상을 결정해야 합니다. 먼저 세그먼트를 연결하고 활성화할 수 있는 사용 가능한 대상 목록을 요청하는 호출을 수행하십시오. 사용 가능한 대상 목록을 반환하려면 `connectionSpecs` 끝점에 다음 GET 요청을 수행하십시오.

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

성공적인 응답에는 사용 가능한 대상 및 고유 식별자(`id`) 목록이 포함됩니다. 추가 단계에서 필요하므로 사용할 대상의 값을 저장합니다. 예를 들어 세그먼트를 연결하고 [!DNL Amazon Kinesis] 또는 [!DNL Azure Event Hubs]에 제공하려는 경우 응답에서 다음 코드 조각을 찾습니다.

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

## Experience Platform 데이터 {#connect-to-your-experience-platform-data}에 연결

![대상 단계 개요 단계 2](../assets/api/streaming-destination/step2.png)

다음으로 프로필 데이터를 내보내고 원하는 대상에서 활성화할 수 있도록 Experience Platform 데이터에 연결해야 합니다. 이것은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 Experience Platform에서 데이터에 대한 액세스를 승인하려면 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 소스 연결을 만드는 다른 호출을 수행하여 Experience Platform 데이터에 대한 연결을 설정합니다.


### Experience Platform에서 데이터에 대한 액세스 권한 부여

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


* `{CONNECTION_SPEC_ID}`:통합 프로필 서비스에 연결 사양 ID 사용 -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`)가 포함됩니다. 소스 연결을 만들기 위해 다음 단계에서 필요에 따라 이 값을 저장합니다.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Experience Platform 데이터 {#connect-to-platform-data}에 연결

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
            "name": "Connecting to Unified Profile Service",
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

* `{BASE_CONNECTION_ID}`:이전 단계에서 얻은 ID를 사용합니다.
* `{CONNECTION_SPEC_ID}`:통합 프로필 서비스에 연결 사양 ID 사용 -  `8a9c3494-9708-43d7-ae3f-cda01e5030e1`.

**응답**

성공적인 응답으로 새로 만든 통합 프로필 서비스에 대한 원본 연결의 고유 식별자(`id`)가 반환됩니다. Experience Platform 데이터에 성공적으로 연결되었음을 확인합니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```


## 스트리밍 대상 {#connect-to-streaming-destination}에 연결

![대상 단계 개요 단계 3](../assets/api/streaming-destination/step3.png)

이 단계에서는 원하는 스트리밍 대상에 대한 연결을 설정합니다. 이것은 아래에 설명된 두 가지 하위 단계로 구성됩니다.

1. 먼저 기본 연결을 설정하여 스트리밍 대상에 대한 액세스를 인증하는 호출을 수행해야 합니다.
2. 그런 다음 기본 연결 ID를 사용하여 대상 연결을 만드는 다른 호출을 수행합니다. 이 호출은 내보낸 데이터를 전달할 저장소 계정의 위치 및 내보낼 데이터의 형식을 지정합니다.

### 스트리밍 대상에 대한 액세스 권한 부여

**API 형식**

```http
POST /connections
```

**요청**

>[!IMPORTANT]
>
>아래 예에는 `//` 접두어가 붙은 코드 주석이 포함되어 있습니다. 이러한 주석은 서로 다른 스트리밍 대상에 서로 다른 값을 사용해야 하는 위치를 강조 표시합니다. 코드 조각을 사용하기 전에 주석을 제거하십시오.

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

* `{CONNECTION_SPEC_ID}`:사용 가능한 대상 목록  [가져오기 단계에서 얻은 연결 사양 ID를 사용합니다](#get-the-list-of-available-destinations).
* `{AUTHENTICATION_CREDENTIALS}`:스트리밍 대상의 이름을 입력합니다. `Aws Kinesis authentication credentials` 또는 `Azure EventHub authentication credentials`.
* `{ACCESS_ID}`: *[!DNL Amazon Kinesis] 연결.* Amazon Kinesis 저장 위치에 대한 액세스 ID.
* `{SECRET_KEY}`: *[!DNL Amazon Kinesis] 연결.* Amazon Kinesis 저장 위치에 대한 비밀 키
* `{REGION}`: *[!DNL Amazon Kinesis] 연결.* Platform이  [!DNL Amazon Kinesis] 데이터를 스트리밍할 계정의 영역입니다.
* `{SAS_KEY_NAME}`: *[!DNL Azure Event Hubs] 연결.* SAS 키 이름을 입력합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)에서 SAS 키를 사용하여 [!DNL Azure Event Hubs]에 인증하는 방법에 대해 학습합니다.
* `{SAS_KEY}`: *[!DNL Azure Event Hubs] 연결.* SAS 키를 입력합니다. [Microsoft 설명서](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)에서 SAS 키를 사용하여 [!DNL Azure Event Hubs]에 인증하는 방법에 대해 학습합니다.
* `{EVENT_HUB_NAMESPACE}`: *[!DNL Azure Event Hubs] 연결.* Platform에서  [!DNL Azure Event Hubs] 데이터를 스트리밍할 네임스페이스를 채웁니다. 자세한 내용은 [!DNL Microsoft] 설명서의 [이벤트 허브 네임스페이스 만들기](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)를 참조하십시오.

**응답**

성공적인 응답에는 기본 연결의 고유 식별자(`id`)가 포함됩니다. 대상 연결을 만들기 위해 다음 단계에서 필요에 따라 이 값을 저장합니다.

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
>아래 예에는 `//` 접두어가 붙은 코드 주석이 포함되어 있습니다. 이러한 주석은 서로 다른 스트리밍 대상에 서로 다른 값을 사용해야 하는 위치를 강조 표시합니다. 코드 조각을 사용하기 전에 주석을 제거하십시오.

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

* `{BASE_CONNECTION_ID}`:위 단계에서 얻은 기본 연결 ID를 사용합니다.
* `{CONNECTION_SPEC_ID}`:사용 가능한 대상 목록  [가져오기 단계에서 얻은 연결 사양을 사용합니다](#get-the-list-of-available-destinations).
* `{NAME_OF_DATA_STREAM}`: *[!DNL Amazon Kinesis] 연결.* 계정에 있는 기존 데이터 스트림의 이름을  [!DNL Amazon Kinesis] 제공합니다. 플랫폼이 데이터를 이 스트림으로 내보냅니다.
* `{REGION}`: *[!DNL Amazon Kinesis] 연결.* Platform이 데이터를 스트리밍할 Amazon Kinesis 계정의 영역입니다.
* `{EVENT_HUB_NAME}`: *[!DNL Azure Event Hubs] 연결.* Platform에서 데이터를  [!DNL Azure Event Hub] 스트리밍할 이름을 입력합니다. 자세한 내용은 [!DNL Microsoft] 설명서의 [이벤트 허브](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub) 만들기를 참조하십시오.

**응답**

성공적인 응답은 스트리밍 대상에 새로 만든 대상 연결에 대한 고유 식별자(`id`)를 반환합니다. 이 값은 이후 단계에서 필요에 따라 저장합니다.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 데이터 흐름 만들기

![대상 단계 개요 단계 4](../assets/api/streaming-destination/step4.png)

이전 단계에서 얻은 ID를 사용하여 이제 Experience Platform 데이터와 데이터를 활성화할 대상 간에 데이터 흐름을 만들 수 있습니다. 이 단계를 Experience Platform과 원하는 대상 간에 나중에 데이터가 진행될 파이프라인을 구성하는 것으로 생각해 보십시오.

데이터 흐름을 만들려면 아래에 표시된 대로 POST 요청을 수행하고 페이로드 내에 아래 언급된 값을 제공합니다.

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

* `{FLOW_SPEC_ID}`:프로필 기반 대상에 대한 흐름 사양 ID는 다음과 같습니다 `71471eba-b620-49e4-90fd-23f1fa0174d8`. 호출에서 이 값을 사용합니다.
* `{SOURCE_CONNECTION_ID}`:Experience Platform 연결 단계에서 얻은 소스 연결 ID [를 사용합니다](#connect-to-your-experience-platform-data).
* `{TARGET_CONNECTION_ID}`:스트리밍 대상에  [연결 단계에서 얻은 대상 연결 ID를 사용합니다](#connect-to-streaming-destination).

**응답**

성공적인 응답은 새로 만든 데이터 흐름의 ID(`id`) 및 `etag`을 반환합니다. 두 값을 모두 적어 둡니다. 를 클릭하여 세그먼트를 활성화합니다.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 새 대상 {#activate-data}에 대한 데이터 활성화

![대상 단계 개요 단계 5](../assets/api/streaming-destination/step5.png)

모든 연결과 데이터 흐름을 만들었으므로 이제 프로필 데이터를 스트리밍 플랫폼에 활성화할 수 있습니다. 이 단계에서 대상으로 보내는 세그먼트 및 프로필 속성을 선택하고 데이터를 예약하고 대상에 보낼 수 있습니다.

세그먼트를 새 대상에 활성화하려면 아래 예와 유사한 JSON PATCH 작업을 수행해야 합니다. 한 번의 클릭으로 여러 세그먼트 및 프로필 속성을 활성화할 수 있습니다. JSON PATCH에 대한 자세한 내용은 [RFC 사양](https://tools.ietf.org/html/rfc6902)을 참조하십시오.

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

* `{DATAFLOW_ID}`:이전 단계에서 얻은 데이터 흐름을 사용합니다.
* `{ETAG}`:이전 단계에서 얻은 태그를 사용합니다.
* `{SEGMENT_ID}`:이 대상으로 내보낼 세그먼트 ID를 제공합니다. 활성화할 세그먼트에 대한 세그먼트 ID를 검색하려면 **https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/**&#x200B;으로 이동하여 왼쪽 탐색 메뉴에서 **[!UICONTROL 세그멘테이션 서비스 API]**&#x200B;를 선택하고 **[!UICONTROL 세그먼트 정의]**&#x200B;에서 `GET /segment/definitions` 작업을 찾습니다.
* `{PROFILE_ATTRIBUTE}`:예를 들어,  `personalEmail.address` 또는  `person.lastName`

**응답**

202 OK 응답을 찾습니다. 응답 본문이 반환되지 않습니다. 요청이 올바른지 확인하려면 다음 단계인 데이터 흐름 유효성 검사를 참조하십시오.

## 데이터 흐름 확인

![대상 단계 개요 단계 6](../assets/api/streaming-destination/step6.png)

자습서의 마지막 단계로, 세그먼트와 프로필 속성이 실제로 데이터 흐름에 올바르게 매핑되었는지 확인해야 합니다.

유효성을 확인하려면 다음 GET 요청을 수행하십시오.

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

* `{DATAFLOW_ID}`:이전 단계의 데이터 흐름을 사용합니다.
* `{ETAG}`:이전 단계의 태그를 사용합니다.

**응답**

반환된 응답에는 이전 단계에서 제출한 세그먼트 및 프로필 속성이 `transformations` 매개 변수에 포함되어야 합니다. 응답의 샘플 `transformations` 매개 변수는 다음과 같습니다.

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
> 프로필 특성 및 [새 대상에 데이터 활성화](#activate-data) 단계의 세그먼트 외에도 [!DNL AWS Kinesis] 및 [!DNL Azure Event Hubs]에서 내보낸 데이터에는 ID 맵에 대한 정보도 포함됩니다. 내보낸 프로필의 ID를 나타냅니다(예: [ECID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html), 모바일 ID, Google ID, 이메일 주소 등). 아래 예를 참조하십시오.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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

## Postman 컬렉션을 사용하여 스트리밍 대상 {#collections}에 연결

이 튜토리얼에서 설명하는 스트리밍 대상에 보다 효율적인 방식으로 연결하려면 [[!DNL Postman]](https://www.postman.com/)을 사용할 수 있습니다.

[!DNL Postman] 는 API를 호출하고 사전 정의된 호출 및 환경의 라이브러리를 관리하는 데 사용할 수 있는 도구입니다.

이 특정 자습서에 대해 다음 [!DNL Postman] 컬렉션이 첨부되었습니다.

* [!DNL AWS Kinesis] [!DNL Postman] collection
* [!DNL Azure Event Hubs] [!DNL Postman] collection

컬렉션 보관 파일을 다운로드하려면 [여기](../assets/api/streaming-destination/DestinationPostmanCollection.zip)를 클릭합니다.

각 컬렉션에는 각각 [!DNL AWS Kinesis] 및 [!DNL Azure Event Hub]에 필요한 요청 및 환경 변수가 포함되어 있습니다.

### Postman 컬렉션을 사용하는 방법

첨부된 [!DNL Postman] 컬렉션을 사용하여 대상에 연결하려면 다음 단계를 따르십시오.

* [!DNL Postman]; 다운로드 및 설치
* [첨부된 컬렉션 ](../assets/api/streaming-destination/DestinationPostmanCollection.zip) 다운로드 및 압축 해제;
* 해당 폴더의 컬렉션을 Postman으로 가져옵니다.
* 이 문서의 지침에 따라 환경 변수를 입력합니다.
* 이 문서의 지침에 따라 Postman의 [!DNL API] 요청을 실행합니다.

## 다음 단계

이 튜토리얼을 따라 선호하는 스트리밍 대상 중 하나에 성공적으로 플랫폼을 연결하여 각 대상에 대한 데이터 흐름을 설정합니다. 이제 고객 분석 또는 수행하려는 기타 데이터 작업을 위해 보내는 데이터를 대상에서 사용할 수 있습니다. 자세한 내용은 다음 페이지를 참조하십시오.

* [대상 개요](../home.md)
* [대상 카탈로그 개요](../catalog/overview.md)
