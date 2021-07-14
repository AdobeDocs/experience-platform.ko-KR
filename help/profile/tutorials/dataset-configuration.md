---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;데이터 세트 활성화
title: API를 사용하여 프로필 및 ID 서비스에 대한 데이터 세트 구성
topic-legacy: tutorial
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform API를 사용하여 실시간 고객 프로필 및 ID 서비스에 사용할 데이터 세트를 활성화하는 방법을 보여줍니다.
exl-id: 142cb7df-072a-4f3a-8a9c-9a78afb35312
source-git-commit: 453e120fa20232533289ee5ff34821ce8c0c310b
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---

# API를 사용하여 [!DNL Profile] 및 [!DNL Identity Service]에 대한 데이터 세트 구성

이 자습서에서는 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에서 사용할 데이터 세트를 활성화하는 프로세스를 다음 단계로 분류합니다.

1. 다음 두 옵션 중 하나를 사용하여 [!DNL Real-time Customer Profile]에서 사용할 데이터 세트를 활성화합니다.
   - [새 데이터 세트 만들기](#create-a-dataset-enabled-for-profile-and-identity)
   - [기존 데이터 세트 구성](#configure-an-existing-dataset)
1. [데이터 집합에 데이터 수집](#ingest-data-into-the-dataset)
1. [실시간 고객 프로필별로 데이터 수집 확인](#confirm-data-ingest-by-real-time-customer-profile)
1. [ID 서비스별 데이터 수집 확인](#confirm-data-ingest-by-identity-service)

## 시작

이 자습서에서는 [!DNL Profile] 사용 가능한 데이터 세트 관리와 관련된 다양한 Adobe Experience Platform 서비스를 이해하고 있어야 합니다. 이 자습서를 시작하기 전에 다음 관련 [!DNL Platform] 서비스에 대한 설명서를 검토하십시오.

- [[!DNL Real-time Customer Profile]](../home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [[!DNL Identity Service]](../../identity-service/home.md): 로  [!DNL Real-time Customer Profile] 수집되는 다양한 데이터 소스의 ID를 브리징하여  [!DNL Platform]활성화합니다.
- [[!DNL Catalog Service]](../../catalog/home.md): 및 에 대한 데이터 세트를 만들고 구성할 수 있는 RESTful API [!DNL Real-time Customer Profile] 입니다  [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 고객 경험 데이터를  [!DNL Platform] 구성하는 표준화된 프레임워크입니다.

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

## [!DNL Profile] 및 [!DNL Identity]에 대해 활성화된 데이터 집합을 만듭니다. {#create-a-dataset-enabled-for-profile-and-identity}

데이터 세트를 만들 때 또는 데이터 세트를 만든 후 즉시 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에 대해 데이터 세트를 활성화할 수 있습니다. 이미 생성된 데이터 세트를 사용하려면 이 문서의 뒷부분에 있는 [기존 데이터 세트 구성](#configure-an-existing-dataset)에 대한 단계를 따르십시오. 새 데이터 세트를 만들려면 실시간 고객 프로필에 대해 활성화된 기존 XDM 스키마의 ID를 알고 있어야 합니다. 프로필 사용 스키마를 조회 또는 만드는 방법에 대한 자세한 내용은 스키마 레지스트리 API](../../xdm/tutorials/create-schema-api.md)를 사용하여 스키마를 만드는 자습서를 참조하십시오. [ [!DNL Catalog] API를 호출하면 [!DNL Profile] 및 [!DNL Identity Service]에 대한 데이터 세트가 활성화됩니다.

**API 형식**

```http
POST /dataSets
```

**요청**

요청 본문에 `unifiedProfile` 및 `unifiedIdentity` 를 포함하면 각각 [!DNL Profile] 및 [!DNL Identity Service]에 대해 데이터 세트가 즉시 활성화됩니다. `tags` 이러한 태그의 값은 `"enabled:true"` 문자열을 포함하는 배열이어야 합니다.

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
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| 속성 | 설명 |
|---|---|
| `schemaRef.id` | 데이터 세트가 기반으로 할 [!DNL Profile] 사용 스키마 ID입니다. |
| `{TENANT_ID}` | IMS 조직에 속하는 리소스를 포함하는 [!DNL Schema Registry] 내의 네임스페이스입니다. 자세한 내용은 [!DNL Schema Registry] 개발자 가이드의 [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 섹션을 참조하십시오. |

**응답**

성공적인 응답에는 새로 만든 데이터 세트의 ID가 포함된 배열이 `"@/dataSets/{DATASET_ID}"` 형식으로 표시됩니다. 데이터 세트를 만들고 활성화했으면 [데이터 업로드](#upload-data-to-the-dataset)에 대한 단계를 진행하십시오.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 기존 데이터 세트 구성 {#configure-an-existing-dataset}

다음 단계에서는 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에 대해 이전에 만든 데이터 세트를 활성화하는 방법을 설명합니다. 이미 프로필 사용 데이터 세트를 만든 경우 [데이터 수집](#ingest-data-into-the-dataset)에 대한 단계를 진행하십시오.

### 데이터 세트가 활성화되어 있는지 확인합니다 {#check-if-the-dataset-is-enabled}

[!DNL Catalog] API를 사용하여 기존 데이터 세트를 검사하여 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에서 사용할 수 있는지 확인할 수 있습니다. 다음 호출은 ID별로 데이터 집합에 대한 세부 사항을 검색합니다.

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
        "name": "Commission Program Events DataSet",
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "adobe/pqs/table": [
                "unifiedprofileingestiontesteventsdataset"
            ],
            "unifiedProfile": [
                "enabled:true"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "lastBatchId": "6dcd9128a1c84e6aa5177641165e18e4",
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
        "viewId": "5b020a27e7040801dedbf46f",
        "status": "enabled",
        "transforms": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/transforms",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
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

`tags` 속성 아래에 `unifiedProfile` 및 `unifiedIdentity` 값이 모두 `enabled:true` 값과 함께 있는 것을 볼 수 있습니다. 따라서 이 데이터 세트에 대해 각각 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]이 활성화됩니다.

### 데이터 집합 활성화 {#enable-the-dataset}

기존 데이터 세트가 [!DNL Profile] 또는 [!DNL Identity Service]에 대해 활성화되지 않은 경우 데이터 세트 ID를 사용하여 PATCH 요청을 수행하여 활성화할 수 있습니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] }	
      ]'
```

요청 본문에는 `path` 과 `unifiedProfile` 및 `unifiedIdentity` 두 유형의 태그가 포함됩니다. 각 배열의 `value`은(는) `enabled:true` 문자열을 포함하는 배열입니다.

****
응답성공적인 PATCH 요청은 HTTP 상태 200(OK) 및 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에 전송된 ID와 일치해야 합니다. 이제 `unifiedProfile` 및 `unifiedIdentity` 태그가 추가되었으며 데이터 세트가 프로필 및 ID 서비스에서 사용할 수 있도록 설정되어 있습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 데이터 집합에 데이터 수집 {#ingest-data-into-the-dataset}

[!DNL Real-time Customer Profile] 및 [!DNL Identity Service] 모두 XDM 데이터를 데이터 세트에 수집하는 동안 사용합니다. 데이터를 데이터 집합에 업로드하는 방법에 대한 지침은 [API](../../catalog/datasets/create.md)를 사용하여 데이터 세트 만들기에서 자습서를 참조하십시오. [!DNL Profile] 사용 가능한 데이터 세트에 보낼 데이터를 계획할 때 다음 우수 사례를 고려하십시오.

- 대상 세그먼트 기준으로 사용할 데이터를 모두 포함하십시오.
- 프로필 데이터에서 확인할 수 있는 만큼 많은 식별자를 포함시켜 ID 그래프를 극대화합니다. 이를 통해 [!DNL Identity Service]이 데이터 세트 간에 ID를 보다 효과적으로 결합할 수 있습니다.

## [!DNL Real-time Customer Profile]에 의한 데이터 수집 확인 {#confirm-data-ingest-by-real-time-customer-profile}

처음으로 데이터를 새 데이터 세트에 업로드하거나 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로, 데이터가 예상대로 업로드되었는지 확인하기 위해 데이터를 신중하게 확인하는 것이 좋습니다. [!DNL Real-time Customer Profile] Access API를 사용하여 일괄 처리 데이터가 데이터 세트에 로드될 때 검색할 수 있습니다. 원하는 엔터티를 검색할 수 없는 경우 [!DNL Real-time Customer Profile]에 대해 데이터 집합을 사용할 수 없습니다. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 사용자의 기대를 지원하는지 확인합니다. [!DNL Real-time Customer Profile] API를 사용하여 [!DNL Profile] 데이터에 액세스하는 방법에 대한 자세한 지침은 [엔티티 엔드포인트 가이드](../api/entities.md)를 따르며, &quot;[!DNL Profile Access] API&quot;라고도 합니다.

## ID 서비스별 데이터 수집 확인 {#confirm-data-ingest-by-identity-service}

둘 이상의 ID를 포함하는 수집된 각 데이터 조각은 개인 ID 그래프에서 링크를 만듭니다. ID 그래프 및 ID 데이터에 액세스하는 방법에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md)를 읽어 보십시오.
