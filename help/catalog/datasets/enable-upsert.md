---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;데이터 세트 활성화
title: API를 사용하여 프로필 업데이트에 대한 데이터 세트 활성화
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필 데이터를 업데이트하기 위해 Adobe Experience Platform API를 사용하여 "업그레이드" 기능이 있는 데이터 세트를 활성화하는 방법을 보여줍니다.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 1e83bc3eb2a2cc10ab945aebeef66d5108b568ea
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 1%

---

# API를 사용하여 프로필 업데이트에 대한 데이터 세트 활성화

이 자습서에서는 실시간 고객 프로필 데이터를 업데이트하기 위해 &quot;업데이트&quot; 기능이 있는 데이터 세트를 활성화하는 프로세스에 대해 설명합니다. 여기에는 새 데이터 세트를 만들고 기존 데이터 세트를 구성하는 단계가 포함됩니다.

>[!NOTE]
>
>업로드 워크플로우는 일괄 처리에만 작동합니다. 스트리밍 수집 **not** 지원됨.

## 시작하기

이 자습서에서는 프로필 사용 데이터 세트 관리와 관련된 여러 Adobe Experience Platform 서비스를 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 이러한 관련 설명서에 대한 설명서를 검토하십시오 [!DNL Platform] 서비스:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Catalog Service]](../../catalog/home.md): 데이터 세트를 만들고 구성할 수 있는 RESTful API [!DNL Real-time Customer Profile] 및 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.
- [일괄 수집](../../ingestion/batch-ingestion/overview.md): 배치 수집 API를 사용하면 데이터를 배치 파일로 Experience Platform에 수집할 수 있습니다.

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 요청이 필요합니다 `Content-Type` 헤더. 필요한 경우 샘플 요청에 이 헤더에 대한 올바른 값이 표시됩니다.

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 다음이 필요합니다. `x-sandbox-name` 작업을 수행할 샌드박스의 이름을 지정하는 헤더입니다. 샌드박스에 대한 자세한 내용은 [!DNL Platform]를 참조하고 [샌드박스 개요 설명서](../../sandboxes/home.md).

## 프로필 업데이트를 위해 활성화된 데이터 세트 만들기

새 데이터 세트를 만들 때 프로필에 대해 해당 데이터 세트를 활성화하고 생성 시 업데이트 기능을 활성화할 수 있습니다.

>[!NOTE]
>
>새 프로필 사용 데이터 세트를 만들려면 프로필에 대해 활성화된 기존 XDM 스키마의 ID를 알고 있어야 합니다. 프로필 사용 스키마를 조회 또는 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [스키마 레지스트리 API를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md).

프로필 및 업데이트에 대해 활성화된 데이터 세트를 만들려면 다음에 대한 POST 요청을 사용하십시오 `/dataSets` 엔드포인트.

**API 형식**

```http
POST /dataSets
```

**요청**

다음을 모두 포함합니다 `unifiedIdentity` 그리고 `unifiedProfile` 아래에 `tags` 요청 본문에서 데이터 집합은 [!DNL Profile] 창조 시. 내 `unifiedProfile` 배열, 추가 `isUpsert:true` 는 데이터 세트에서 업데이트를 지원하는 기능을 추가합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "Sample dataset",
        "description: "A sample dataset with a sample description.",
        "fields": [],
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
            "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags": {
            "unifiedIdentity": [
                "enabled: true"
            ],
            "unifiedProfile": [
                "enabled: true",
                "isUpsert: true"
            ]
        }
      }'
```

| 속성 | 설명 |
| -------- | ----------- |
| `schemaRef.id` | 의 ID입니다 [!DNL Profile]데이터 세트를 기반으로 할 사용 가능한 스키마. |
| `{TENANT_ID}` | 네임스페이스 [!DNL Schema Registry] 조직에 속하는 리소스를 포함합니다. 자세한 내용은 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 섹션 [!DNL Schema Registry] 개발자 안내서 를 참조하십시오. |

**응답**

성공적인 응답에는 새로 생성된 데이터 세트의 ID가 포함된 배열이 `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 기존 데이터 세트 구성 {#configure-an-existing-dataset}

다음 단계에서는 업데이트(업데이트) 기능을 위해 기존 프로필 사용 데이터 세트를 구성하는 방법을 설명합니다.

>[!NOTE]
>
>업데이트할 기존 프로필 사용 데이터 세트를 구성하려면, 먼저 프로필에 대한 데이터 세트를 비활성화한 다음 과 함께 다시 활성화해야 합니다 `isUpsert` 태그에 가깝게 포함했습니다. 기존 데이터 세트가 프로필에 대해 활성화되어 있지 않으면 다음 단계로 직접 진행할 수 있습니다 [프로필 및 업데이트에 대한 데이터 세트 활성화](#enable-the-dataset). 확실하지 않은 경우 다음 단계는 데이터 세트가 이미 활성화되어 있는지 확인하는 방법을 보여 줍니다.

### 프로필에 대해 데이터 세트가 활성화되어 있는지 확인

사용 [!DNL Catalog] API인 경우 기존 데이터 세트에서 사용할 수 있는지 여부를 확인할 수 있습니다 [!DNL Real-time Customer Profile]. 다음 호출은 ID별로 데이터 집합에 대한 세부 사항을 검색합니다.

**API 형식**

```http
GET /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 검사할 데이터 세트의 ID입니다. |

**요청**

```shell
curl -X GET 'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{ORG_ID}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ],
            "unifiedProfile": [
                "enabled:true"
            ]
        },
        "lastBatchId": "{BATCH_ID}",
        "lastBatchStatus": "success",
        "dule": {},
        "statsCache": {
            "startDate": null,
            "endDate": null
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaMetadata": {
            "primaryKey": [],
            "delta": [],
            "dule": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

아래에 `tags` 속성을 사용하여 `unifiedProfile` 이(가) 값과 함께 표시됩니다 `enabled:true`. 따라서, [!DNL Real-time Customer Profile] 이 데이터 세트에 대해 활성화되어 있습니다.

### 프로필에 대한 데이터 세트 비활성화

업데이트에 대해 프로필 사용 가능한 데이터 세트를 구성하려면 먼저 을 비활성화해야 합니다 `unifiedProfile` 및 `unifiedIdentity` 태그를 만든 다음 함께 다시 활성화합니다 `isUpsert` 태그에 가깝게 포함했습니다. 이 작업은 한 번은 비활성화하고, 한 번은 다시 활성화하기 위해 두 개의 PATCH 요청을 사용하여 수행됩니다.

>[!WARNING]
>
>비활성화되어 있는 동안 데이터 집합에 수집된 데이터는 프로필 저장소에 수집되지 않습니다. 프로필에 대해 다시 활성화될 때까지 데이터 집합에 데이터를 섭취하지 않아야 합니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

제1 PATCH 요청 본문은 `path` to `unifiedProfile` 그리고 `path` to `unifiedIdentity`, 설정 `value` to `enabled:false` 를 사용하도록 선택할 수 있습니다.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "replace", 
            "path": "/tags/unifiedProfile", 
            "value": ["enabled:false"] 
        },
        {
            "op": "replace",
            "path": "/tags/unifiedIdentity",
            "value": ["enabled:false"]
        }
      ]'
```

**응답**

성공적인 PATCH 요청은 HTTP 상태 200(OK) 및 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 다음 `unifiedProfile` 및 `unifiedIdentity` 이제 태그를 사용할 수 없습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 프로필 및 업데이트를 위한 데이터 세트 활성화 {#enable-the-dataset}

기존 데이터 세트는 단일 PATCH 요청을 사용하여 프로필 및 속성 업데이트를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>프로필에 데이터 세트를 활성화할 때 데이터 세트가 연결된 스키마가 인지 확인하십시오 **또한** 프로필 사용. 스키마가 프로필을 사용하지 않으면 데이터 세트가 수행됩니다 **not** 플랫폼 UI에서 프로필 활성화로 표시됩니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

요청 본문은 `path` to `unifiedProfile` 설정 `value` 를 `enabled` 및 `isUpsert` 태그, 둘 다 `true`, 및 `path` to `unifiedIdentity` 설정 `value` 를 `enabled` 태그 설정 `true`.

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { 
            "op": "add", 
            "path": "/tags/unifiedProfile", 
            "value": [
                "enabled:true",
                "isUpsert:true"
            ] 
        },
        {
            "op": "add",
            "path": "/tags/unifiedIdentity",
            "value": [
                "enabled:true"
            ]
        }
      ]'
```

**응답**

성공적인 PATCH 요청은 HTTP 상태 200(OK) 및 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 다음 `unifiedProfile` 태그 및 `unifiedIdentity` 이제 태그 가 활성화되고 속성 업데이트에 대해 구성되었습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 다음 단계

이제 프로필 및 업데이트를 지원하는 데이터 세트를 배치 수집 워크플로우에서 사용하여 프로필 데이터를 업데이트할 수 있습니다. Adobe Experience Platform으로 데이터를 수집하는 방법에 대한 자세한 내용은 [데이터 수집 개요](../../ingestion/home.md).
