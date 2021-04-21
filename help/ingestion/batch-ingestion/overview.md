---
keywords: Experience Platform;홈;인기 항목;데이터 통합;일괄 처리;데이터 집합 활성화;일괄 처리 통합 개요;개요;일괄 처리 통합 개요;Analytics;Mobizing topics
solution: Experience Platform
title: 일괄 처리 통합 개요
topic-legacy: overview
description: 'Adobe Experience Platform 데이터 통합 API를 사용하면 데이터를 플랫폼에 일괄 파일로 통합할 수 있습니다. 인제스트되는 데이터는 CRM 시스템의 플랫 파일(예: 쪽모이 세공 항목 파일)의 프로필 데이터이거나 XDM(Experience Data Model) 레지스트리에서 알려진 스키마를 따르는 데이터일 수 있습니다.'
exl-id: ffd1dc2d-eff8-4ef7-a26b-f78988f050ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 2%

---

# 일괄 처리 통합 개요

Adobe Experience Platform 데이터 통합 API를 사용하면 데이터를 플랫폼에 일괄 파일로 통합할 수 있습니다. 인제스트되는 데이터는 CRM 시스템의 플랫 파일(예: 쪽모이 세공 항목 파일)의 프로필 데이터이거나 [!DNL Experience Data Model] (XDM) 레지스트리에서 알려진 스키마를 따르는 데이터일 수 있습니다.

[데이터 통합 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)는 이러한 API 호출에 대한 추가 정보를 제공합니다.

다음 다이어그램은 배치 처리 프로세스에 대한 개요를 설명합니다.

![](../images/batch-ingestion/overview/batch_ingestion.png)

## API 사용

[!DNL Data Ingestion] API를 사용하면 3가지 기본 단계를 통해 데이터를 배치(단일 단위로 인제스트할 하나 이상의 파일로 구성된 데이터 단위)로 [!DNL Experience Platform]에 인제스트할 수 있습니다.

1. 새 배치를 만듭니다.
2. 데이터의 XDM 스키마와 일치하는 지정된 데이터 세트에 파일을 업로드합니다.
3. 배치의 끝을 신호합니다.


### [!DNL Data Ingestion] 사전 요구 사항

- 업로드할 데이터는 쪽모이 세공된 데이터 또는 JSON 형식이어야 합니다.
- [[!DNL Catalog services]](../../catalog/home.md)에서 만든 데이터 집합입니다.
- Portable 파일의 내용은 업로드되는 데이터 집합의 스키마 하위 집합과 일치해야 합니다.
- 인증 후 고유한 액세스 토큰을 사용하십시오.

### 일괄 통합 우수 사례

- 권장되는 일괄 처리 크기는 256MB에서 100GB 사이입니다.
- 각 일괄 처리에는 최대 1,500개의 파일이 포함되어야 합니다.

512MB보다 큰 파일을 업로드하려면 파일을 더 작은 청크로 나누어야 합니다. 큰 파일을 업로드하는 방법은 [여기](#large-file-upload---create-file)에서 찾을 수 있습니다.

### 샘플 API 호출 읽기

이 안내서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증:Bearer `{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 헤더가 필요합니다.

- 컨텐츠 유형:application/json

### 일괄 처리 만들기

데이터를 데이터 세트에 추가하려면 먼저 데이터를 일괄 처리에 연결해야 하며, 나중에 지정된 데이터 세트에 업로드됩니다.

```http
POST /batches
```

**요청**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Content-Type: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{ 
          "datasetId": "{DATASET_ID}" 
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `datasetId` | 파일을 업로드할 데이터 세트의 ID입니다. |

**응답**

```JSON
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `id` | 방금 만든(후속 요청에서 사용) 일괄 처리의 ID. |
| `relatedObjects.id` | 파일을 업로드할 데이터 세트의 ID입니다. |

## 파일 업로드

업로드용 새 일괄 처리를 만든 후 파일을 특정 데이터 세트에 업로드할 수 있습니다.

작은 파일 업로드 API를 사용하여 파일을 업로드할 수 있습니다. 그러나 파일이 너무 크고 게이트웨이 제한이 초과된 경우(예: 확장된 시간 초과, 본문 크기 요청 초과 및 기타 제한) [대용량 파일 업로드 API로 전환할 수 있습니다. 이 API는 대용량 파일 업로드 완료 API 호출을 사용하여 파일을 청크로 업로드하고 데이터를 함께 결합합니다.

>[!NOTE]
>
>아래 예제는 [Apache Parided](https://parquet.apache.org/documentation/latest/) 파일 형식을 사용합니다. JSON 파일 형식을 사용하는 예제는 [일괄 처리 통합 개발자 가이드](./api-overview.md)에서 찾을 수 있습니다.

### 작은 파일 업로드

일괄 처리가 만들어지면 기존 데이터 세트에 데이터를 업로드할 수 있습니다.  업로드되는 파일은 참조된 XDM 스키마와 일치해야 합니다.

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 배치의 ID. |
| `{DATASET_ID}` | 파일을 업로드할 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 데이터 세트에 표시될 파일의 이름입니다. |

**요청**

```SHELL
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 데이터 세트에 업로드할 파일의 경로와 파일 이름입니다. |

**응답**

```JSON
#Status 200 OK, with empty response body
```

### 대용량 파일 업로드 - 파일 만들기

큰 파일을 업로드하려면 파일을 작은 청크로 분할하고 한 번에 하나씩 업로드해야 합니다.

```http
POST /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}?action=initialize
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 배치의 ID. |
| `{DATASET_ID}` | 파일을 수집하는 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 데이터 세트에 표시될 파일의 이름입니다. |

**요청**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet?action=initialize" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**응답**

```JSON
#Status 201 CREATED, with empty response body
```

### 대용량 파일 업로드 - 후속 부품 업로드

파일을 만든 후 파일의 각 섹션에 대해 PATCH 요청을 반복하여 모든 후속 청크를 업로드할 수 있습니다.

```http
PATCH /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 배치의 ID. |
| `{DATASET_ID}` | 파일을 업로드할 데이터 세트의 ID입니다. |
| `{FILE_NAME}` | 데이터 세트에 표시될 파일의 이름입니다. |

**요청**

```SHELL
curl -X PATCH "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/part1=a/part2=b/{FILE_NAME}.parquet" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "Content-Range: bytes {CONTENT_RANGE}" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

| 속성 | 설명 |
| -------- | ----------- |
| `{FILE_PATH_AND_NAME}` | 데이터 세트에 업로드할 파일의 경로와 파일 이름입니다. |

**응답**

```JSON
#Status 200 OK, with empty response
```

## 신호 일괄 완료

모든 파일이 일괄 처리에 업로드되면 일괄 처리를 완료하도록 신호를 보낼 수 있습니다. 이렇게 하면 완료된 파일에 대해 [!DNL Catalog] DataSetFile 항목이 만들어지고 위에서 생성된 일괄 처리와 연결됩니다. 그런 다음 [!DNL Catalog] 일괄 처리가 성공적으로 표시되어 다운스트림으로 흘러 사용 가능한 데이터를 인제스트합니다.

**요청**

```http
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 데이터 세트에 업로드할 일괄 처리의 ID. |

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**응답**

```JSON
#Status 200 OK, with empty response
```

## 일괄 처리 상태 확인

파일이 일괄 처리로 업로드되기를 기다리는 동안 일괄 처리 상태를 확인하여 진행 상태를 확인할 수 있습니다.

**API 형식**

```http
GET /batch/{BATCH_ID}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{BATCH_ID}` | 체크되고 있는 배치의 ID. |

**요청**

```shell
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

**응답**

```JSON
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `{USER_ID}` | 배치를 만들거나 갱신한 사용자의 ID. |

`"status"` 필드는 요청된 일괄 처리의 현재 상태를 보여 주는 필드입니다. 배치에는 다음 상태 중 하나가 있을 수 있습니다.

## 일괄 처리 상태

| 상태 | 설명 |
| ------ | ----------- |
| 포기 | 배치가 예상 기간에 완료되지 않았습니다. |
| 중단됨 | 중단 작업에는 지정된 일괄 처리에 대해 **명시적으로**&#x200B;이(가) 호출되었습니다(일괄 인제스트 API를 통해). 일괄 처리가 &quot;불러오기&quot; 상태에 있으면 일괄 처리를 중단할 수 없습니다. |
| 활성 | 배치가 성공적으로 홍보되었으며 다운스트림 소비에 사용할 수 있습니다. 이 상태는 &quot;성공&quot;과 혼용하여 사용할 수 있습니다. |
| 삭제됨 | 일괄 처리에 대한 데이터가 완전히 제거되었습니다. |
| 실패 | 잘못된 구성 및/또는 잘못된 데이터로 인해 발생하는 터미널 상태입니다. 실패한 일괄 처리에 대한 데이터가 **표시되지 않습니다**. 이 상태는 &quot;실패&quot;와 혼용하여 사용할 수 있습니다. |
| 비활성 | 배치가 성공적으로 홍보되었지만 되돌려졌거나 만료되었습니다. 해당 배치를 더 이상 다운스트림 소비에 사용할 수 없습니다. |
| 로드됨 | 배치에 대한 데이터가 완료되고 배치가 홍보할 준비가 되었습니다. |
| 로드 중 | 이 일괄 처리에 대한 데이터가 업로드되고 현재 **이(가) 홍보될 준비가 되지 않았습니다.** |
| 다시 시도 중 | 이 일괄 처리에 대한 데이터를 처리하고 있습니다. 그러나 시스템 오류 또는 일시적인 오류로 인해 일괄 처리가 실패하여 이 일괄 처리를 다시 시도하고 있습니다. |
| 단계 | 배치에 대한 프로모션 프로세스의 스테이징 단계가 완료되었으며 통합 작업이 실행되었습니다. |
| 스테이징 | 일괄 처리에 대한 데이터가 처리 중입니다. |
| 교착 상태 | 일괄 처리에 대한 데이터가 처리 중입니다. 그러나 여러 차례의 재시도 후 일괄 프로모션이 중단됩니다. |
