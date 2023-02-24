---
title: Flow Service API를 사용하여 Pendo용 소스 연결 및 데이터 흐름 만들기
description: Flow Service API를 사용하여 Adobe Experience Platform과 Pendo를 연결하는 방법을 알아봅니다.
badge: "Beta"
source-git-commit: c35daa60db315f1ed04ed6424464f1ae7bfb4243
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 1%

---

# 에 대한 소스 연결 및 데이터 흐름 만들기 [!DNL Pendo] 흐름 서비스 API 사용

>[!NOTE]
>
>다음 [!DNL Pendo] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

다음 자습서에서는 가져올 소스 연결 및 데이터 흐름을 만드는 단계를 안내합니다 [[!DNL Pendo]](https://Pendo.com/) 이벤트를 사용하여 Adobe Experience Platform에 데이터 보내기 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기 {#getting-started}

이 안내서에서는 Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 데이터를 다양한 소스에서 수집할 수 있으며 를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공할 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## Connect [!DNL Pendo] 를 사용하여 플랫폼 구현 [!DNL Flow Service] API {#connect-platform-to-flow-api}

다음은 소스 연결 및 데이터 흐름을 만들어 데이터를 가져오기 위해 수행해야 하는 절차에 대해 설명합니다 [!DNL Pendo] 이벤트 데이터를 Experience Platform에 추가합니다.

### 소스 연결 만들기 {#source-connection}

에 POST 요청을 수행하여 소스 연결을 만듭니다. [!DNL Flow Service] API로, 소스의 연결 사양 ID를 제공하는 동안 이름, 설명 및 데이터 형식과 같은 세부 사항을 제공합니다.

**API 형식**

```https
POST /sourceConnections
```

**요청**

다음 요청은에 대한 소스 연결을 만듭니다 [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for Pendo",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for Pendo",
      "connectionSpec": {
          "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 소스 연결의 이름입니다. 소스 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 소스 연결의 이름이 설명적인지 확인합니다. |
| `description` | 소스 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 소스에 해당하는 연결 사양 ID입니다. |
| `data.format` | 의 형식 [!DNL Pendo] 수집할 데이터입니다. 현재 지원되는 데이터 형식은 `json`. |

**응답**

성공적인 응답은 고유 식별자(`id`) 내의 아무 곳에나 삽입할 수 있습니다. 이 ID는 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
    "id": "76b968ff-3ff0-4e98-98bb-f3205d4d370c",
    "etag": "\"0301c198-0000-0200-0000-63f32ba50000\""
}
```

### 대상 XDM 스키마 만들기 {#target-schema}

Platform에서 소스 데이터를 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 그런 다음 대상 스키마를 사용하여 소스 데이터가 포함된 Platform 데이터 세트를 만듭니다.

대상 XDM 스키마는에 대한 POST 요청을 수행하여 만들 수 있습니다 [스키마 레지스트리 API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

대상 XDM 스키마를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [api를 사용하여 스키마 만들기](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 대상 데이터 세트 만들기 {#target-dataset}

에 대한 POST 요청을 수행하여 대상 데이터 세트를 만들 수 있습니다 [카탈로그 서비스 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)페이로드 내에 대상 스키마의 ID를 제공하는 것이 좋습니다.

대상 데이터 세트를 만드는 방법에 대한 자세한 단계는 다음 사항에 대한 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 대상 연결 만들기 {#target-connection}

대상 연결은 수집된 데이터를 저장할 대상에 대한 연결을 나타냅니다. 대상 연결을 만들려면 데이터 레이크에 해당하는 고정 연결 사양 ID를 제공해야 합니다. 이 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

이제 대상 스키마에서 대상 데이터 세트와 데이터 레이크에 대한 연결 사양 ID의 고유 식별자가 있습니다. 이러한 식별자를 사용하여 [!DNL Flow Service] 인바운드 소스 데이터를 포함할 데이터 세트를 지정하는 API입니다.

**API 형식**

```https
POST /targetConnections
```

**요청**

다음 요청은에 대한 대상 연결을 만듭니다 [!DNL Pendo]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for Pendo",
      "description": "Streaming Target Connection for Pendo",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "https://ns.adobe.com/extconndev/schemas/b48de0b204046e65a4c50232e7946401946b4c519fd7c172",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "63dca52231a6031c07280614"
      }
  }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `name` | 대상 연결의 이름입니다. 대상 연결에 대한 정보를 조회하는 데 사용할 수 있으므로 대상 연결의 이름이 설명적인지 확인합니다. |
| `description` | Target 연결에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `connectionSpec.id` | 데이터 레이크에 해당하는 연결 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 의 형식 [!DNL Pendo] 수집할 데이터입니다. |
| `params.dataSetId` | 이전 단계에서 검색된 대상 데이터 세트 ID입니다. |

**응답**

성공적인 응답은 새 대상 연결의 고유 식별자(`id`). 이 ID는 이후 단계에서 필요합니다.

```json
{
    "id": "c63978c1-df7e-4611-aa32-3657eab5704b",
    "etag": "\"7f0045f1-0000-0200-0000-63f32c9d0000\""
}
```

### 매핑 만들기 {#mapping}

소스 데이터를 대상 데이터 세트에 수집하려면 먼저 대상 데이터 세트가 준수하는 대상 스키마에 매핑해야 합니다. 이것은 POST 요청을 수행하여에 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) (요청 페이로드 내에 정의된 데이터 매핑 사용)

**API 형식**

```http
POST /conversion/mappingSets
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "outputSchema": {
          "schemaRef": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/945546112b746524bfd9f1264b26c2b7d8e7f5b7fadb953a",
              "contentType": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
    "mappings": [
        {
            "destinationXdmPath": "_extconndev.accountid",
            "sourceAttribute": "accountId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.uniqueid",
            "sourceAttribute": "uniqueId",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.name1",
            "sourceAttribute": "properties.guideProperties.name",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.timestamp1",
            "sourceAttribute": "timestamp",
            "identity": false,
            "version": 0
        },
        {
            "destinationXdmPath": "_extconndev.visitorid",
            "sourceAttribute": "visitorId",
            "identity": false,
            "version": 0
        }
    ]
  }'
```

| 속성 | 설명 |
| --- | --- |
| `outputSchema.schemaRef.id` | 의 ID입니다 [target XDM 스키마](#target-schema) 이전 단계에서 생성된 . |
| `mappings.sourceType` | 매핑되는 소스 특성 유형입니다. |
| `mappings.source` | 대상 XDM 경로에 매핑해야 하는 소스 속성입니다. |
| `mappings.destination` | 소스 속성이 매핑되는 대상 XDM 경로입니다. |

**응답**

성공적인 응답은 고유 식별자(`id`). 이 값은 이후 단계에서 데이터 흐름을 만드는 데 필요합니다.

```json
{
    "id": "a126ae1a1d134c4b82bd00c2d01a039e",
    "version": 0,
    "createdDate": 1676881164541,
    "modifiedDate": 1676881164541,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 흐름 만들기 {#flow}

에서 데이터를 가져오는 마지막 단계 [!DNL Pendo] 플랫폼 목표는 데이터 흐름을 만드는 것입니다. 현재까지는 다음 필수 값이 준비되었습니다.

* [소스 연결 ID](#source-connection)
* [Target 연결 ID](#target-connection)
* [매핑 ID](#mapping)

데이터 흐름은 소스에서 데이터를 예약하고 수집합니다. 페이로드 내에서 이전에 언급된 값을 제공하는 동안 POST 요청을 수행하여 데이터 흐름을 만들 수 있습니다.

**API 형식**

```http
POST /flows
```

**요청**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for Pendo",
      "description": "Streaming Dataflow for Pendo",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
      ],
      "targetConnectionIds": [
          "df7c660e-3484-463b-b01a-1835e9b04ac9"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bae11501021646e58cecc1182451af22",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 데이터 흐름의 이름입니다. 데이터 흐름에서 정보를 조회하는 데 사용할 수 있으므로 데이터 흐름의 이름이 설명적인지 확인합니다. |
| `description` | 데이터 플로우에 대한 자세한 정보를 제공하기 위해 포함할 수 있는 선택적 값입니다. |
| `flowSpec.id` | 데이터 흐름을 만드는 데 필요한 흐름 사양 ID입니다. 이 고정 ID는 다음과 같습니다. `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 흐름 사양 ID의 해당 버전입니다. 이 값의 기본값은 입니다. `1.0`. |
| `sourceConnectionIds` | 다음 [소스 연결 ID](#source-connection) 이전 단계에서 생성된 . |
| `targetConnectionIds` | 다음 [target 연결 ID](#target-connection) 이전 단계에서 생성된 . |
| `transformations` | 이 속성에는 데이터에 적용해야 하는 다양한 변형이 포함되어 있습니다. 이 속성은 XDM 규격 이외의 데이터를 Platform에 가져올 때 필요합니다. |
| `transformations.name` | 변환에 지정된 이름입니다. |
| `transformations.params.mappingId` | 다음 [매핑 ID](#mapping) 이전 단계에서 생성된 . |
| `transformations.params.mappingVersion` | 매핑 ID의 해당 버전입니다. 이 값의 기본값은 입니다. `0`. |

**응답**

성공적인 응답은 ID(`id`)을 만들 수 있습니다. 이 ID를 사용하여 데이터 흐름을 모니터링, 업데이트 또는 삭제할 수 있습니다.

```json
{
    "id": "c341617b-e143-43d5-aff1-da02b3e028b6",
    "etag": "\"9c01173c-0000-0200-0000-63f32d7c0000\""
}
```

### 스트리밍 끝점 URL 가져오기 {#get-streaming-url}

이제 데이터 흐름이 만들어지면 스트리밍 끝점 URL을 검색할 수 있습니다. 이 끝점 URL을 사용하여 소스를 웹 후크에 가입하여 소스가 Experience Platform과 통신할 수 있도록 합니다.

스트리밍 끝점 URL을 검색하려면 에 GET 요청을 수행하십시오 `/flows` 엔드포인트 및 데이터 흐름의 ID를 제공합니다.

**API 형식**

```http
GET /flows/{FLOW_ID}
```

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/4982698b-e6b3-48c2-8dcf-040e20121fd2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 끝점 URL을 다음으로 표시된 데이터 플로우에 대한 정보를 반환합니다 `inletUrl`. 자세한 내용은 [Webhook 설정](../../../ui/create/analytics/pendo-webhook.md#get-streaming-endpoint-url) 페이지에서 필요한 값을 가져옵니다.

```json
{
    "items": [
        {
            "id": "d947e6a9-ea53-42c4-985c-c9379265491f",
            "createdAt": 1676875325841,
            "updatedAt": 1676875331938,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Streaming Dataflow for Pendo",
            "description": "Streaming Dataflow for Pendo",
            "flowSpec": {
                "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "etag": "\"9801a366-0000-0200-0000-63f2f92c0000\"",
            "sourceConnectionIds": [
                "339d60a5-9ff6-4eba-8197-e8887eeb3c08"
            ],
            "targetConnectionIds": [
                "df7c660e-3484-463b-b01a-1835e9b04ac9"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "339d60a5-9ff6-4eba-8197-e8887eeb3c08",
                        "connectionSpec": {
                            "id": "6ff5654f-19d5-427d-bd3e-c0ebc802389a",
                            "version": "1.0"
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "df7c660e-3484-463b-b01a-1835e9b04ac9",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "inletUrl": "https://dcs.adobedc.net/collection/e389c18dbc7f5de8b95df07b1b89d76ddd9b1e88d5423abc71b6ac9161491373"
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "bae11501021646e58cecc1182451af22",
                        "mappingVersion": 0
                    }
                }
            ],
            "runs": "/runs?property=flowId==4d90b316-1c9b-469d-935f-5a27d5deefdf",
            "providerRefId": "19d9fb14-9cb9-42a5-bb8b-23dc545e766a",
            "lastOperation": {
                "started": 0,
                "updated": 0,
                "operation": "enable"
            },
            "lastRunDetails": {
                "id": "d6972216-2332-41f6-8ed3-2ac82e6550b7",
                "state": "partialSuccess",
                "startedAtUTC": 1676862000000,
                "completedAtUTC": 1676867880000
            }
        }
    ]
}
```

## 부록 {#appendix}

다음 섹션에서는 데이터 흐름을 모니터링, 업데이트 및 삭제할 수 있는 단계에 대한 정보를 제공합니다.

### 데이터 흐름 모니터링 {#monitor-dataflow}

데이터 흐름을 만든 후에는 데이터 흐름을 통해 수집 중인 데이터를 모니터링하여 흐름 실행, 완료 상태 및 오류에 대한 정보를 볼 수 있습니다. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 소스 데이터 흐름 모니터링](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 데이터 흐름 업데이트 {#update-dataflow}

PATCH 요청을 수행하여 데이터 흐름의 세부 정보(예: 이름 및 설명)와 해당 실행 일정 및 관련 매핑 세트를 업데이트합니다 `/flows` 끝점 [!DNL Flow Service] API, 데이터 흐름의 ID를 제공합니다. PATCH 요청을 만들 때 데이터 흐름의 고유한 정보를 제공해야 합니다 `etag` 에서 `If-Match` 헤더. 전체 API 예는 다음 안내서를 참조하십시오. [api를 사용하여 소스 데이터 흐름 업데이트](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 계정 업데이트 {#update-account}

에 PATCH 요청을 수행하여 소스 계정의 이름, 설명 및 자격 증명을 업데이트합니다 [!DNL Flow Service] 기본 연결 ID를 쿼리 매개 변수로 제공하는 동안 API입니다. PATCH 요청을 만들 때 소스 계정의 고유한 `etag` 에서 `If-Match` 헤더. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 소스 계정 업데이트](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 데이터 흐름 삭제 {#delete-dataflow}

에 DELETE 요청을 수행하여 데이터 흐름을 삭제합니다. [!DNL Flow Service] 삭제할 데이터 흐름의 ID를 쿼리 매개 변수의 일부로 제공하는 API입니다. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 데이터 흐름 삭제](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 계정 삭제 {#delete-account}

에 DELETE 요청을 수행하여 계정을 삭제합니다. [!DNL Flow Service] 삭제할 계정의 기본 연결 ID를 제공하는 동안 API가 제공됩니다. 전체 API 예는 다음 안내서를 참조하십시오. [API를 사용하여 소스 계정 삭제](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).