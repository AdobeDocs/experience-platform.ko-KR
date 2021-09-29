---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;데이터 세트 활성화
title: API를 사용하여 프로필 업데이트에 대한 데이터 세트 활성화
type: Tutorial
description: 이 자습서에서는 실시간 고객 프로필 데이터를 업데이트하기 위해 Adobe Experience Platform API를 사용하여 "업그레이드" 기능이 있는 데이터 세트를 활성화하는 방법을 보여줍니다.
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---


# API를 사용하여 프로필 업데이트에 대한 데이터 세트 활성화

이 자습서에서는 실시간 고객 프로필 데이터를 업데이트하기 위해 &quot;업데이트&quot; 기능이 있는 데이터 세트를 활성화하는 프로세스에 대해 설명합니다. 여기에는 새 데이터 세트를 만들고 기존 데이터 세트를 구성하는 단계가 포함됩니다.

## 시작하기

이 자습서에서는 프로필 사용 데이터 세트 관리와 관련된 여러 Adobe Experience Platform 서비스를 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 다음 관련 DNL 플랫폼 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Catalog Service]](../../catalog/home.md): 및 에 대한 데이터 세트를 만들고 구성할 수 있는 RESTful API [!DNL Real-time Customer Profile] 입니다  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다.
- [일괄 처리 수집](../../ingestion/batch-ingestion/overview.md)

다음 섹션에서는 플랫폼 API를 성공적으로 호출하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서에서 [예제 API 호출](../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법 섹션을 참조하십시오.

### 필수 헤더에 대한 값을 수집합니다

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에 필요한 각 헤더에 대한 값을 제공합니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 `Content-Type` 헤더가 필요합니다. 필요한 경우 샘플 요청에 이 헤더에 대한 올바른 값이 표시됩니다.

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 `x-sandbox-name` 헤더가 필요합니다. [!DNL Platform]의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

## 프로필 업데이트를 위해 활성화된 데이터 세트 만들기

새 데이터 세트를 만들 때 프로필에 대해 해당 데이터 세트를 활성화하고 생성 시 업데이트 기능을 활성화할 수 있습니다.

>[!NOTE]
>
>새 프로필 사용 데이터 세트를 만들려면 프로필에 대해 활성화된 기존 XDM 스키마의 ID를 알고 있어야 합니다. 프로필 사용 스키마를 조회 또는 만드는 방법에 대한 자세한 내용은 스키마 레지스트리 API](../../xdm/tutorials/create-schema-api.md)를 사용하여 스키마를 만드는 자습서를 참조하십시오.[

프로필 및 업데이트에 대해 활성화된 데이터 집합을 만들려면 `/dataSets` 종단점에 대한 POST 요청을 사용하십시오.

**API 형식**

```http
POST /dataSets
```

**요청**

요청 본문에 `tags` 아래에 `unifiedProfile`을 포함하면 생성 시 [!DNL Profile]에 대해 데이터 세트가 활성화됩니다. `unifiedProfile` 배열 내에서 `isUpsert:true`을 추가하면 데이터 집합에 업데이트를 지원하는 기능이 추가됩니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "fields":[],
        "schemaRef" : {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
          "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
        },
        "tags" : {
          "unifiedProfile": [
            "enabled:true",
            "isUpsert:true"
          ]
        }
      }'
```

| 속성 | 설명 |
|---|---|
| `schemaRef.id` | 데이터 세트가 기반으로 할 [!DNL Profile] 사용 스키마 ID입니다. |
| `{TENANT_ID}` | IMS 조직에 속하는 리소스를 포함하는 [!DNL Schema Registry] 내의 네임스페이스입니다. 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 섹션을 참조하십시오. |

**응답**

성공적인 응답에는 새로 만든 데이터 세트의 ID가 포함된 배열이 `"@/dataSets/{DATASET_ID}"` 형식으로 표시됩니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 기존 데이터 세트 구성 {#configure-an-existing-dataset}

다음 단계에서는 업데이트(&quot;업데이트&quot;) 기능을 위해 기존 프로필 사용 데이터 세트를 구성하는 방법을 설명합니다.

>[!NOTE]
>
>&quot;업데이트&quot;에 대해 기존 프로필 사용 데이터 세트를 구성하려면 먼저 프로필에 대한 데이터 세트를 비활성화한 다음 `isUpsert` 태그와 함께 다시 활성화해야 합니다. 기존 데이터 세트가 프로필에 대해 활성화되어 있지 않으면 [프로필에 대한 데이터 세트를 활성화 및 업데이트하는 단계로 직접 진행할 수 있습니다](#enable-the-dataset). 확실하지 않은 경우 다음 단계는 데이터 세트가 이미 활성화되어 있는지 확인하는 방법을 보여 줍니다.

### 프로필에 대해 데이터 세트가 활성화되어 있는지 확인

[!DNL Catalog] API를 사용하여 기존 데이터 세트를 검사하여 [!DNL Real-time Customer Profile]에서 사용할 수 있는지 확인할 수 있습니다. 다음 호출은 ID별로 데이터 집합에 대한 세부 사항을 검색합니다.

**API 형식**

```http
GET /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 검사할 데이터 세트의 ID입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "{DATASET_NAME}",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
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

`tags` 속성 아래에 `unifiedProfile` 값이 `enabled:true` 인 것을 볼 수 있습니다. 따라서 이 데이터 세트에 대해 [!DNL Real-time Customer Profile]이 활성화되어 있습니다.

### 프로필에 대한 데이터 세트 비활성화

업데이트에 대해 프로필 사용 가능한 데이터 세트를 구성하려면 먼저 `unifiedProfile` 태그를 비활성화한 다음 `isUpsert` 태그와 함께 다시 활성화해야 합니다. 이 작업은 한 번은 비활성화하고, 한 번은 다시 활성화하기 위해 두 개의 PATCH 요청을 사용하여 수행됩니다.

>[!WARNING]
>
>비활성화되어 있는 동안 데이터 집합에 수집된 데이터는 프로필 저장소에 수집되지 않습니다. 프로필에 대해 다시 활성화될 때까지 데이터 집합에 데이터를 섭취하지 않는 것이 좋습니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

첫 번째 PATCH 요청 본문에는 태그를 비활성화하기 위해 `value` 를 `enabled:false`(으)로 설정하는 `path`이 포함됩니다.`unifiedProfile`

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "replace", "path": "/tags/unifiedProfile", "value": ["enabled:false"] },
      ]'
```

****
응답성공적인 PATCH 요청은 HTTP 상태 200(OK) 및 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 이제 `unifiedProfile` 태그를 사용할 수 없습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 프로필 및 업데이트를 위한 데이터 세트 활성화 {#enable-the-dataset}

기존 데이터 세트는 단일 PATCH 요청을 사용하여 프로필 및 속성 업데이트를 활성화할 수 있습니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

요청 본문에는 `path` ~ `unifiedProfile` 설정이 포함되어 `enabled` 및 `isUpsert` 태그를 포함하도록 `value` 가 포함되어 있으며, 둘 다 `true` 로 설정됩니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true","isUpsert:true"] },
      ]'
```

****
응답성공적인 PATCH 요청은 HTTP 상태 200(OK) 및 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 이제 `unifiedProfile` 태그가 활성화되고 특성 업데이트에 대해 구성되었습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 다음 단계

이제 프로필 및 업데이트를 지원하는 데이터 세트를 일괄 처리 및 스트리밍 수집 워크플로우에서 사용하여 프로필 데이터를 업데이트할 수 있습니다. Adobe Experience Platform으로 데이터를 수집하는 방법에 대한 자세한 내용은 [데이터 수집 개요](../../ingestion/home.md)를 읽어 보십시오.
