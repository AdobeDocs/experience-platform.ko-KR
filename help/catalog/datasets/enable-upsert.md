---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;데이터 세트 활성화
title: API를 사용하여 프로필 업데이트에 대한 데이터 세트 활성화
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform API를 사용하여 "업데이트" 기능이 있는 데이터 세트를 활성화하여 실시간 고객 프로필 데이터를 업데이트하는 방법을 보여줍니다.
exl-id: fc89bc0a-40c9-4079-8bfc-62ec4da4d16a
source-git-commit: 6985ebf8705130636abdc50b5c3f50299a60f2aa
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 10%

---

# API를 사용하여 프로필 업데이트에 대한 데이터 세트 활성화

이 튜토리얼에서는 실시간 고객 프로필 데이터를 업데이트하기 위해 &quot;업데이트&quot; 기능으로 데이터 세트를 활성화하는 프로세스에 대해 설명합니다. 여기에는 새 데이터 세트를 만들고 기존 데이터 세트를 구성하는 단계가 포함됩니다.

>[!NOTE]
>
>이 자습서에 설명된 워크플로우는 일괄 처리에 대해서만 작동합니다. 스트리밍 수집 업데이트에 대해서는 다음 안내서를 참조하십시오. [데이터 준비를 사용하여 실시간 고객 프로필에 부분 행 업데이트 보내기](../../data-prep/upserts.md).

## 시작하기

이 자습서에서는 프로필 사용 데이터 세트 관리와 관련된 여러 Adobe Experience Platform 서비스에 대한 작업 이해가 필요합니다. 이 튜토리얼을 시작하기 전에 관련 설명서를 검토하십시오. [!DNL Platform] 서비스:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
- [[!DNL Catalog Service]](../../catalog/home.md): 데이터 세트를 만들고 이를 구성할 수 있는 RESTful API입니다. [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): [!DNL Platform]이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
- [일괄 처리 수집](../../ingestion/batch-ingestion/overview.md): 일괄 처리 수집 API 를 사용하면 데이터를 일괄 처리 파일로 Experience Platform에 수집할 수 있습니다.

다음 섹션에서는 Platform API를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 문서에 사용된 규칙에 대한 자세한 내용은 [ 문제 해결 안내서의 ](../../landing/troubleshooting.md#how-do-i-format-an-api-request)예제 API 호출을 읽는 방법[!DNL Experience Platform] 섹션을 참조하세요.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 튜토리얼](https://www.adobe.com/go/platform-api-authentication-en)을 완료해야 합니다. 인증 튜토리얼을 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출의 필수 헤더 각각에 대한 값이 제공됩니다.

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

페이로드가 포함된 모든 요청(POST, PUT, PATCH)에는 추가 항목이 필요합니다 `Content-Type` 머리글입니다. 이 헤더에 대한 정확한 값이 필요한 경우 샘플 요청에 표시됩니다.

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 `x-sandbox-name` 작업이 수행될 샌드박스의 이름을 지정하는 헤더입니다. 의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

## 프로필 업데이트를 위해 활성화된 데이터 세트 만들기

새 데이터 세트를 만들 때 프로필에 대해 해당 데이터 세트를 활성화하고 생성 시 업데이트 기능을 활성화할 수 있습니다.

>[!NOTE]
>
>새 프로필 활성화 데이터 세트를 만들려면 프로필에 대해 활성화된 기존 XDM 스키마의 ID를 알고 있어야 합니다. 프로필 활성화 스키마를 조회하거나 만드는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [스키마 레지스트리 API를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md).

프로필 및 업데이트에 대해 사용할 수 있는 데이터 세트를 만들려면 다음에 대한 POST 요청을 사용하십시오. `/dataSets` 엔드포인트.

**API 형식**

```http
POST /dataSets
```

**요청**

다음 두 가지를 모두 포함 `unifiedIdentity` 및 `unifiedProfile` 아래에 `tags` 요청 본문에서 데이터 세트를 활성화할 수 있습니다. [!DNL Profile] 창조되었을 때. 다음 범위 내 `unifiedProfile` 배열, 추가 `isUpsert:true` 업데이트를 지원하는 데이터 세트에 대한 기능을 추가합니다.

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
| `schemaRef.id` | 의 ID [!DNL Profile]-데이터 세트가 기반으로 삼을 스키마 활성화됨. |
| `{TENANT_ID}` | 내의 네임스페이스 [!DNL Schema Registry] 조직에 속한 리소스를 포함합니다. 다음을 참조하십시오. [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 의 섹션 [!DNL Schema Registry] 개발자 안내서 를 참조하십시오. |

**응답**

성공적인 응답은 새로 생성된 데이터 세트의 ID가 포함된 배열을 `"@/dataSets/{DATASET_ID}"`.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 기존 데이터 세트 구성 {#configure-an-existing-dataset}

다음 단계에서는 업데이트(업데이트) 기능을 위해 기존 프로필 지원 데이터 세트를 구성하는 방법을 다룹니다.

>[!NOTE]
>
>업데이트할 기존 프로필 사용 데이터 세트를 구성하려면 먼저 프로필에 대한 데이터 세트를 비활성화한 다음 와 함께 다시 활성화해야 합니다. `isUpsert` 태그에 가깝게 배치하십시오. 기존 데이터 세트가 프로필에 대해 활성화되지 않은 경우 다음 단계로 직접 진행할 수 있습니다. [프로필 및 업데이트를 위한 데이터 세트 활성화](#enable-the-dataset). 확실하지 않은 경우 다음 단계에서는 데이터 세트가 이미 활성화되어 있는지 확인하는 방법을 보여 줍니다.

### 프로필에 대해 데이터 세트가 활성화되어 있는지 확인

사용 [!DNL Catalog] API를 사용하면 기존 데이터 세트를 검사하여에서 사용할 수 있는지 여부를 확인할 수 있습니다. [!DNL Real-Time Customer Profile]. 다음 호출은 ID별로 데이터 세트의 세부 정보를 검색합니다.

**API 형식**

```http
GET /dataSets/{DATASET_ID}
```

| 매개변수 | 설명 |
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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "{VIEW_ID}",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "{SCHEMA}",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

아래 `tags` 속성, 다음을 확인할 수 있습니다 `unifiedProfile` 이(가) 값과 함께 존재합니다. `enabled:true`. 따라서 [!DNL Real-Time Customer Profile] 은(는) 이 데이터 세트에 대해 활성화됩니다.

### 프로필에 대한 데이터 세트 비활성화

업데이트에 대해 프로필 사용 데이터 세트를 구성하려면 먼저 다음을 비활성화해야 합니다. `unifiedProfile` 및 `unifiedIdentity` 태그를 만든 다음 `isUpsert` 태그에 가깝게 배치하십시오. 이 작업은 두 개의 PATCH 요청을 사용하여 수행되며, 한 번은 비활성화하고 한 번은 다시 활성화합니다.

>[!WARNING]
>
>비활성화되어 있는 동안 데이터 세트에 수집된 데이터는 프로필 스토어에 수집되지 않습니다. 프로필에 대해 다시 활성화될 때까지 데이터 세트로 데이터를 섭취하지 않아야 합니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

상기 제1 PATCH 요청 본문은 `path` 끝 `unifiedProfile` 및 a `path` 끝 `unifiedIdentity`, 설정 `value` 끝 `enabled:false` 태그를 비활성화하기 위해 두 경로 모두에 대해

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

성공적인 PATCH 요청은 HTTP 상태 200(OK)과 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에서 전송된 ID와 일치해야 합니다. 다음 `unifiedProfile` 및 `unifiedIdentity` 이제 태그가 비활성화되었습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

### 프로필 및 업데이트에 대한 데이터 세트 활성화 {#enable-the-dataset}

단일 PATCH 요청을 사용하여 프로필 및 속성 업데이트에 대한 기존 데이터 세트를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>프로필에 대해 데이터 세트를 활성화할 때 데이터 세트가 연결된 스키마가 인지 확인하십시오. **또한** 프로필이 활성화되었습니다. 스키마에서 프로필이 활성화되지 않으면 데이터 세트는 **아님** platform UI 내에서 프로필이 활성화됨으로 표시됩니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

요청 본문에는 `path` 끝 `unifiedProfile` 설정 `value` 다음을 포함 `enabled` 및 `isUpsert` 태그, 둘 다 로 설정됨 `true`, 및 `path` 끝 `unifiedIdentity` 설정 `value` 다음을 포함 `enabled` 태그 설정 대상 `true`.

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

성공적인 PATCH 요청은 HTTP 상태 200(OK)과 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에서 전송된 ID와 일치해야 합니다. 다음 `unifiedProfile` 태그 및 `unifiedIdentity` 이제 태그가 속성 업데이트에 대해 활성화 및 구성되었습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 다음 단계

이제 일괄 처리 수집 워크플로우에서 프로필 및 업데이트 활성화 데이터 세트를 사용하여 프로필 데이터를 업데이트할 수 있습니다. Adobe Experience Platform으로 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../ingestion/home.md).
