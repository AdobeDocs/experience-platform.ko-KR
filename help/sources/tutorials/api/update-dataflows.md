---
title: 흐름 서비스 API를 사용하여 데이터 흐름 업데이트
description: 흐름 서비스 API를 사용하여 이름, 설명 및 일정을 포함한 데이터 흐름 방법을 알아봅니다.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 2%

---

# 흐름 서비스 API를 사용하여 데이터 흐름 업데이트

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 기본 정보, 일정 및 매핑 세트를 포함하여 데이터 흐름을 업데이트하는 단계를 다룹니다.

>[!TIP]
>
>소스 연결 및 대상 연결을 단일 데이터 흐름에 매핑해야 합니다. 변경 사항은 해당 데이터 흐름에 반영되지 않으므로 소스 및 타겟 연결을 별도로 업데이트해서는 안 됩니다. 사용 사례에서 소스 및 타겟 연결을 업데이트해야 하는 경우 새 소스 및 타겟 연결 쌍과 새 데이터 흐름을 만들어야 합니다.

## 시작하기

이 자습서를 사용하려면 유효한 흐름 ID가 있어야 합니다. 올바른 흐름 ID가 없는 경우 [소스 개요](../../home.md)에서 선택한 커넥터를 선택하고 이 자습서를 시도하기 전에 설명된 단계를 따르십시오.

또한 이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 데이터 흐름 세부 정보 조회

데이터 흐름을 업데이트하는 첫 번째 단계는 흐름 ID를 사용하여 데이터 흐름 세부 정보를 검색하는 것입니다. `/flows` 끝점에 대한 GET 요청을 수행하면 기존 데이터 흐름의 현재 세부 정보를 볼 수 있습니다.

**API 형식**

```http
GET /flows/{FLOW_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{FLOW_ID}` | 검색할 데이터 흐름의 고유한 `id` 값입니다. |

**요청**

다음 요청은 플로우 ID에 대한 업데이트된 정보를 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 버전, 일정 및 고유 식별자(`id`)를 포함하여 데이터 흐름의 현재 세부 정보를 반환합니다.

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## 데이터 흐름 업데이트

데이터 흐름의 실행 일정, 이름 및 설명을 업데이트하려면 흐름 ID, 버전 및 사용할 새 일정을 제공하는 동안 [!DNL Flow Service] API에 대한 PATCH 요청을 수행합니다.

>[!IMPORTANT]
>
>PATCH 요청을 수행할 때 `If-Match` 헤더가 필요합니다. 이 헤더의 값은 업데이트할 연결의 고유한 버전입니다. 데이터 흐름이 성공적으로 업데이트될 때마다 etag 값이 업데이트됩니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 플로우 실행 일정과 데이터 흐름의 이름 및 설명을 업데이트합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| 속성 | 설명 |
| --------- | ----------- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. |
| `value` | 매개 변수를 업데이트할 새 값입니다. |

**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 흐름 ID를 제공하면서 [!DNL Flow Service] API에 대한 GET 요청을 만들어 업데이트를 확인할 수 있습니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## 매핑 업데이트

[!DNL Flow Service] API에 대한 PATCH 요청을 만들고 `mappingId` 및 `mappingVersion`에 대해 업데이트된 값을 제공하여 기존 데이터 흐름의 매핑 집합을 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /flows/{FLOW_ID}
```

**요청**

다음 요청은 데이터 흐름의 매핑 세트를 업데이트합니다.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| 속성 | 설명 |
| --- | --- |
| `op` | 데이터 흐름을 업데이트하는 데 필요한 작업을 정의하는 데 사용되는 작업 호출입니다. 작업에는 `add`, `replace` 및 `remove`이(가) 포함됩니다. |
| `path` | 플로우에서 업데이트할 부분을 정의합니다. 이 예제에서는 `transformations`을(를) 업데이트하는 중입니다. |
| `value.name` | 업데이트할 속성의 이름입니다. |
| `value.params.mappingId` | 데이터 흐름의 매핑 세트를 업데이트하는 데 사용할 새 매핑 ID입니다. |
| `value.params.mappingVersion` | 업데이트된 매핑 ID와 연결된 새 매핑 버전입니다. |

**응답**

성공적인 응답은 흐름 ID와 업데이트된 etag를 반환합니다. 흐름 ID를 제공하면서 [!DNL Flow Service] API에 대한 GET 요청을 만들어 업데이트를 확인할 수 있습니다.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## 다음 단계

이 자습서에 따라 [!DNL Flow Service] API를 사용하여 데이터 흐름의 기본 정보, 일정 및 매핑 세트를 업데이트했습니다. 소스 커넥터 사용에 대한 자세한 내용은 [소스 개요](../../home.md)를 참조하십시오.
