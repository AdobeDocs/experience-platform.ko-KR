---
keywords: Experience Platform;홈;인기 항목;카탈로그;api;개체 업데이트
solution: Experience Platform
title: 카탈로그 개체 업데이트
description: PATCH 요청의 경로에 ID를 포함하여 카탈로그 개체의 일부를 업데이트할 수 있습니다. 이 문서에서는 카탈로그 개체에 대한 PATCH 작업을 수행하기 위한 필드 사용 및 JSON 패치 표기법 사용에 대해 설명합니다.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 카탈로그 개체 업데이트

[!DNL Catalog] 개체의 ID를 PATCH 요청 경로에 포함하여 개체의 일부를 업데이트할 수 있습니다. 이 문서에서는 카탈로그 개체에서 PATCH 작업을 수행하는 두 가지 방법을 다룹니다.

* 필드 사용
* JSON 패치 표기법 사용

>[!NOTE]
>
>개체에 대한 PATCH 작업은 상호 관련된 개체를 나타내는 확장 가능한 필드를 수정할 수 없습니다. 상호 관련된 객체를 직접 수정해야 합니다.

## 필드를 사용하여 업데이트

다음 예제 호출에서는 필드 및 값을 사용하여 개체를 업데이트하는 방법을 보여 줍니다.

**API 형식**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 업데이트할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 집합의 `name` 및 `description` 필드를 페이로드에 제공된 값으로 업데이트합니다. 업데이트하지 않을 개체 필드는 페이로드에서 제외할 수 있습니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**응답**

성공적인 응답은 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에서 전송된 ID와 일치해야 합니다. 이제 이 데이터 세트에 대한 GET 요청을 수행하면 `name` 및 `description`만 업데이트되고 다른 모든 값은 변경되지 않은 상태로 표시됩니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## JSON 패치 표기법을 사용한 업데이트 {#patch-notation}

다음 예제 호출은 [RFC-6902](https://tools.ietf.org/html/rfc6902)에 설명된 대로 JSON 패치를 사용하여 개체를 업데이트하는 방법을 보여 줍니다.

JSON 패치 구문에 대한 자세한 내용은 [API 기본 사항 안내서](../../landing/api-fundamentals.md#json-patch)를 참조하십시오.

**API 형식**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{OBJECT_TYPE}` | 업데이트할 [!DNL Catalog] 개체의 형식입니다. 유효한 오브젝트는 다음과 같습니다. <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 업데이트할 특정 개체의 식별자입니다. |

**요청**

다음 요청은 데이터 집합의 `name` 및 `description` 필드를 각 JSON 패치 개체에 제공된 값으로 업데이트합니다. JSON 패치를 사용하는 경우 Content-Type 헤더도 `application/json-patch+json`(으)로 설정해야 합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**응답**

성공한 응답은 업데이트된 개체의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에서 전송된 ID와 일치해야 합니다. 이제 이 개체에 대해 GET 요청을 수행하면 `name` 및 `description`만 업데이트되고 다른 모든 값은 변경되지 않은 상태로 표시됩니다.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## PATCH v2 표기법을 사용한 업데이트 {#patch-v2-notation}

`/v2/dataSets/{DATASET_ID}` 끝점은 복잡하거나 깊게 중첩된 데이터 집합 특성을 업데이트하는 보다 유연한 방법을 제공합니다.

일반적으로 `a.b.c.d`과(와) 같이 많이 중첩된 필드를 업데이트할 때는 경로의 각 수준이 이미 존재해야 합니다. 레벨이 누락된 경우 최종 값을 설정하기 전에 각 레벨을 수동으로 생성해야 합니다. 이 경우 여러 작업을 수행해야 하므로 복잡성이 가중되고 실수 가능성이 증가합니다.

`/v2/dataSets/{DATASET_ID}` 끝점은 경로에 누락된 수준을 자동으로 만듭니다. `d`을(를) 설정하기 전에 수동으로 `b` 및 `c`을(를) 확인하고 추가하는 대신 PATCH `v2` 작업에서 이를 수행합니다.

`/v2/dataSets/{DATASET_ID}` 끝점으로 PATCH 요청을 보낼 때는 최종 구조만 전송하면 되며 시스템이 업데이트를 적용하기 전에 누락된 부분을 채웁니다.

>[!NOTE]
>
>`If-Match` 및 `If-None-Match` 헤더는 `/v2/dataSets/{id}` 끝점에 대해 선택 사항입니다. PATCH은 이 끝점에 대한 요청을 통해 업데이트를 동적으로 병합하므로 최신 데이터 세트 버전을 검색하지 않고도 수정할 수 있습니다. 이렇게 하면 동시 업데이트로 인한 데이터 손실 위험이 줄어들지만 `If-Match`을(를) 최신 `etag`과(와) 함께 사용하여 변경 내용이 특정 버전에만 적용되도록 할 수 있습니다. 또는 마지막으로 알려진 버전 이후에 데이터 집합이 변경되지 않은 경우 `If-None-Match`에서 업데이트를 금지합니다.

**API 형식**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 업데이트할 데이터 세트의 식별자입니다. |

**요청**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**응답**

성공적인 응답은 업데이트된 데이터 세트의 ID가 포함된 배열을 반환하며, 이 ID는 PATCH 요청에서 전송된 ID와 일치해야 합니다. 이제 이 개체에 대해 GET 요청을 수행하면 이전에 수동으로 만드는 단계를 수행하지 않고도 `extensions.adobe_lakeHouse.rowExpiration` 개체가 만들어진 것으로 표시됩니다.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### 업데이트 전후의 예제 데이터 세트

아래 예제 JSON은 PATCH 요청의 데이터 세트 구조 **이전**&#x200B;을 보여 줍니다. 여기서 `extensions.adobe_lakeHouse.rowExpiration` 개체는 데이터 세트에 없습니다.

+++예를 보려면 선택

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

다음 JSON은 PATCH 요청의 데이터 세트 구조 **after**&#x200B;를 보여 줍니다. 업데이트는 이전 수동 만들기 단계 없이 누락된 `extensions.adobe_lakeHouse.rowExpiration` 개체를 자동으로 만듭니다. 이 예에서는 `/v2/` PATCH 요청을 통해 여러 작업을 수행할 필요가 없어지고 업데이트가 더 간단해지고 효율화되는 방법을 보여 줍니다.


+++예를 보려면 선택

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
