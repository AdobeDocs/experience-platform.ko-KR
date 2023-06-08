---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;데이터 세트 활성화
title: API를 사용하여 프로필 및 ID 서비스에 대한 데이터 세트 활성화
type: Tutorial
description: 이 자습서에서는 Adobe Experience Platform API를 사용하여 실시간 고객 프로필 및 ID 서비스에 사용할 데이터 세트를 활성화하는 방법을 보여줍니다.
exl-id: a115e126-6775-466d-ad7e-ee36b0b8b49c
source-git-commit: 2226b1878ef3398554b6cf96ff400cc1767a9e4c
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 1%

---

# 다음에 대한 데이터 세트 활성화 [!DNL Profile] 및 [!DNL Identity Service] api 사용

이 자습서에서는 에서 사용할 데이터 세트를 활성화하는 프로세스에 대해 설명합니다 [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service]를 분류하여 다음 단계를 수행합니다.

1. 에서 사용할 데이터 세트 활성화 [!DNL Real-Time Customer Profile], 다음 두 옵션 중 하나를 사용합니다.
   - [새 데이터 세트 만들기](#create-a-dataset-enabled-for-profile-and-identity)
   - [기존 데이터 세트 구성](#configure-an-existing-dataset)
1. [데이터 세트에 데이터 수집](#ingest-data-into-the-dataset)
1. [실시간 고객 프로필로 데이터 수집 확인](#confirm-data-ingest-by-real-time-customer-profile)
1. [ID 서비스에서 데이터 수집 확인](#confirm-data-ingest-by-identity-service)

## 시작하기

이 자습서에서는 프로필 사용 데이터 세트 관리와 관련된 여러 Adobe Experience Platform 서비스에 대한 작업 이해가 필요합니다. 이 튜토리얼을 시작하기 전에 관련 설명서를 검토하십시오. [!DNL Platform] 서비스:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
- [[!DNL Identity Service]](../../identity-service/home.md): 사용 [!DNL Real-Time Customer Profile] 서로 다른 데이터 소스의 id를 브리징하여 [!DNL Platform].
- [[!DNL Catalog Service]](../../catalog/home.md): 데이터 세트를 만들고 이를 구성할 수 있는 RESTful API입니다. [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

다음 섹션에서는 Platform API를 성공적으로 호출하기 위해 알아야 하는 추가 정보를 제공합니다.

### 샘플 API 호출 읽기

이 튜토리얼에서는 요청 형식을 지정하는 방법을 보여 주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 적절한 포맷의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용되는 규칙에 대한 자세한 내용은 의 섹션을 참조하십시오. [예제 API 호출을 읽는 방법](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 다음에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값 수집

을 호출하기 위해 [!DNL Platform] API, 먼저 다음을 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 항목에서 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래와 같이 API 호출:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

페이로드가 포함된 모든 요청(POST, PUT, PATCH)에는 추가 항목이 필요합니다 `Content-Type` 머리글입니다. 이 헤더에 대한 정확한 값이 필요한 경우 샘플 요청에 표시됩니다.

의 모든 리소스 [!DNL Experience Platform] 특정 가상 샌드박스로 격리됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 `x-sandbox-name` 작업이 수행될 샌드박스의 이름을 지정하는 헤더입니다. 의 샌드박스에 대한 자세한 내용 [!DNL Platform], 다음을 참조하십시오. [샌드박스 개요 설명서](../../sandboxes/home.md).

## 프로필 및 ID에 대해 활성화된 데이터 세트 만들기 {#create-a-dataset-enabled-for-profile-and-identity}

데이터 세트를 만든 직후 또는 데이터 세트가 만들어진 후 언제든지 실시간 고객 프로필 및 ID 서비스에 대한 데이터 세트를 활성화할 수 있습니다. 이미 생성된 데이터 세트를 활성화하려면 다음 단계를 수행합니다. [기존 데이터 세트 구성](#configure-an-existing-dataset) 이 문서의 후반부에 있습니다.

>[!NOTE]
>
>새 프로필 활성화 데이터 세트를 만들려면 프로필에 대해 활성화된 기존 XDM 스키마의 ID를 알고 있어야 합니다. 프로필 활성화 스키마를 조회하거나 만드는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [스키마 레지스트리 API를 사용하여 스키마 만들기](../../xdm/tutorials/create-schema-api.md).

프로필에 대해 활성화된 데이터 세트를 만들려면 다음에 대한 POST 요청을 사용할 수 있습니다. `/dataSets` 엔드포인트.

**API 형식**

```http
POST /dataSets
```

**요청**

다음을 포함 `unifiedProfile` 및 `unifiedIdentity` 아래에 `tags` 요청 본문에서 데이터 세트가 즉시 활성화됩니다. [!DNL Profile] 및 [!DNL Identity Service], 각각 이러한 태그의 값은 문자열을 포함하는 배열이어야 합니다 `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/31670881463308a46f7d2cb09762715",
        "contentType": "application/vnd.adobe.xed-full-notext+json; version=1"
    },
    "tags": {
       "unifiedProfile": ["enabled:true"],
       "unifiedIdentity": ["enabled:true"]
    }
  }'
```

| 속성 | 설명 |
|---|---|
| `schemaRef.id` | 의 ID [!DNL Profile]-데이터 세트가 기반으로 삼을 스키마 활성화됨. |
| `{TENANT_ID}` | 내의 네임스페이스 [!DNL Schema Registry] 조직에 속한 리소스를 포함합니다. 다음을 참조하십시오. [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) 의 섹션 [!DNL Schema Registry] 개발자 안내서 를 참조하십시오. |

**응답**

성공적인 응답은 새로 생성된 데이터 세트의 ID가 포함된 배열을 `"@/dataSets/{DATASET_ID}"`. 데이터 세트를 만들고 활성화했으면 의 단계로 진행하십시오. [데이터 업로드](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 기존 데이터 세트 구성 {#configure-an-existing-dataset}

다음 단계는에 대해 이전에 만든 데이터 세트를 활성화하는 방법을 다룹니다 [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service]. 프로필 지원 데이터 세트를 이미 만든 경우 다음 단계로 진행하십시오. [데이터 수집](#ingest-data-into-the-dataset).

### 데이터 세트가 활성화되어 있는지 확인 {#check-if-the-dataset-is-enabled}

사용 [!DNL Catalog] API를 사용하면 기존 데이터 세트를 검사하여에서 사용할 수 있는지 여부를 확인할 수 있습니다. [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service]. 다음 호출은 ID별로 데이터 세트의 세부 정보를 검색합니다.

**API 형식**

```http
GET /dataSets/{DATASET_ID}
```

| 매개변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 검사할 데이터 세트의 ID입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "5b020a27e7040801dedbf46e": {
        "name": "Commission Program Events DataSet",
        "imsOrg": "{ORG_ID}",
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
        "version": "1.0.1",
        "created": 1536536917382,
        "updated": 1539793978215,
        "createdClient": "{CLIENT_CREATED}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "viewId": "5b020a27e7040801dedbf46f",
        "files": "@/dataSets/5b020a27e7040801dedbf46e/views/5b020a27e7040801dedbf46f/files",
        "schema": "@/xdms/context/experienceevent",
        "schemaRef": {
            "id": "https://ns.adobe.com/xdm/context/experienceevent",
            "contentType": "application/vnd.adobe.xed+json"
        }
    }
}
```

아래 `tags` 속성, 다음을 확인할 수 있습니다 `unifiedProfile` 및 `unifiedIdentity` 둘 다 값과 함께 존재합니다. `enabled:true`. 따라서 [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service] 이 데이터 세트에 대해 각각 활성화됩니다.

### 데이터 세트 활성화 {#enable-the-dataset}

기존 데이터 세트가 다음에 대해 활성화되지 않은 경우 [!DNL Profile] 또는 [!DNL Identity Service], 데이터 세트 ID를 사용하여 PATCH 요청을 함으로써 활성화할 수 있습니다.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 업데이트할 데이터 세트의 ID입니다. |

**요청**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type:application/json-patch+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/tags/unifiedProfile", "value": ["enabled:true"] },
        { "op": "add", "path": "/tags/unifiedIdentity", "value": ["enabled:true"] } 
      ]'
```

요청 본문에는 `path` 두 가지 유형의 태그, `unifiedProfile` 및 `unifiedIdentity`. 다음 `value` 각각 문자열을 포함하는 배열입니다. `enabled:true`.

**응답**

성공적인 PATCH 요청은 HTTP 상태 200(OK)과 업데이트된 데이터 세트의 ID가 포함된 배열을 반환합니다. 이 ID는 PATCH 요청에서 전송된 ID와 일치해야 합니다. 다음 `unifiedProfile` 및 `unifiedIdentity` 이제 태그가 추가되었으며 프로필 및 ID 서비스에서 데이터 세트를 사용할 수 있습니다.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 데이터 세트에 데이터 수집 {#ingest-data-into-the-dataset}

모두 [!DNL Real-Time Customer Profile] 및 [!DNL Identity Service] 는 데이터 세트에 수집되는 XDM 데이터를 사용합니다. 데이터를 데이터 세트에 업로드하는 방법에 대한 지침은 의 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../catalog/datasets/create.md). 다음에 보낼 데이터를 계획할 때 [!DNL Profile]-enabled dataset, 다음 모범 사례를 고려하십시오.

- 세분화 기준으로 사용할 데이터를 포함합니다.
- 프로필 데이터에서 확인할 수 있는 만큼의 식별자를 포함하여 ID 그래프를 최대화합니다. 이렇게 하면 [!DNL Identity Service] 을 사용하여 데이터 세트 간에 id를 보다 효과적으로 결합합니다.

## 데이터 수집 확인 기준 [!DNL Real-Time Customer Profile] {#confirm-data-ingest-by-real-time-customer-profile}

데이터를 새 데이터 세트에 처음 업로드할 때, 또는 새 ETL 또는 데이터 소스를 포함하는 프로세스의 일부로 데이터를 예상대로 업로드했는지 주의 깊게 확인하는 것이 좋습니다. 사용 [!DNL Real-Time Customer Profile] API에 액세스하여 데이터 세트에 로드될 때 배치 데이터를 검색할 수 있습니다. 예상한 엔티티를 검색할 수 없는 경우 데이터 세트가 활성화되지 않을 수 있습니다 [!DNL Real-Time Customer Profile]. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 기대를 지원하는지 확인합니다. 사용 방법에 대한 자세한 지침은 [!DNL Real-Time Customer Profile] 액세스할 API [!DNL Profile] 데이터, 다음을 참조하십시오. [엔티티 끝점 안내서](../../profile/api/entities.md), &quot;라고도 함[!DNL Profile Access]&quot;API.

## ID 서비스에서 데이터 수집 확인 {#confirm-data-ingest-by-identity-service}

두 개 이상의 ID를 포함하는 수집된 각 데이터 조각은 개인 ID 그래프에 링크를 만듭니다. ID 그래프와 ID 데이터에 액세스하는 방법에 대한 자세한 내용은 [ID 서비스 개요](../../identity-service/home.md).
