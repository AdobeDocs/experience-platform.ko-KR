---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Configure a dataset for Profile and Identity Service using APIs
topic: tutorial
translation-type: tm+mt
source-git-commit: 93aae0e394e1ea9b6089d01c585a94871863818e
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 1%

---


# Configure a dataset for Profile and Identity Service using APIs

This tutorial covers the process of enabling a dataset for use in Real-time Customer Profile and Identity Service, broken down into the following steps:

1. Enable a dataset for use in Real-time Customer Profile, using one of two options:
   - [새 데이터 집합 만들기](#create-a-dataset-enabled-for-profile-and-identity)
   - [기존 데이터 세트 구성](#configure-an-existing-dataset)
1. [데이터를 데이터 세트에 인제스트](#ingest-data-into-the-dataset)
1. [Confirm data ingest by Real-time Customer Profile](#confirm-data-ingest-by-real-time-customer-profile)
1. [ID 서비스별 데이터 인제스트 확인](#confirm-data-ingest-by-identity-service)

## 시작하기

This tutorial requires a working understanding of the various Adobe Experience Platform services involved in managing Profile-enabled datasets. Before beginning this tutorial, please review the documentation for these related Platform services:

- [실시간 고객 프로필](../home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [ID 서비스](../../identity-service/home.md): 수집되는 여러 데이터 소스의 ID를 Platform으로 연결하여 실시간 고객 프로파일을 활성화합니다.
- [카탈로그 서비스](../../catalog/home.md): 데이터 세트를 만들고 실시간 고객 프로필 및 ID 서비스에 대해 구성할 수 있는 RESTful API.
- [XDM(Experience Data Model)](../../xdm/home.md): Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

다음 섹션에서는 Platform API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 제공합니다.

### Reading sample API calls

This tutorial provides example API calls to demonstrate how to format your requests. These include paths, required headers, and properly formatted request payloads. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서의 예제 API 호출 [](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 읽기 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

Platform API를 호출하려면 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

- 인증: 무기명 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 헤더가 필요합니다.

- Content-Type: application/json

Experience Platform의 모든 리소스는 특정 가상 샌드박스와 분리됩니다. All requests to Platform APIs require a header that specifies the name of the sandbox the operation will take place in. For more information on sandboxes in Platform, see the [sandbox overview documentation](../../sandboxes/home.md).

- x-sandbox-name: `{SANDBOX_NAME}`

## 프로필 및 ID에 대해 활성화된 데이터 집합 만들기 {#create-a-dataset-enabled-for-profile-and-identity}

실시간 고객 프로필 및 ID 서비스를 만들 때 또는 데이터 세트를 만든 후 언제든지 데이터 세트를 활성화할 수 있습니다. If you would like to enable a dataset that has already been created, follow the steps for [configuring an existing dataset](#configure-an-existing-dataset) found later in this document. 새 데이터 세트를 만들려면 실시간 고객 프로필에 대해 활성화된 기존 XDM 스키마의 ID를 알고 있어야 합니다. 프로필 사용 스키마를 찾거나 만드는 방법에 대한 자세한 내용은 스키마 레지스트리 API를 사용하여 스키마 [만들기에 대한 자습서를 참조하십시오](../../xdm/tutorials/create-schema-api.md). The following call to the Catalog API enables a dataset for Profile and Identity Service.

**API 형식**

```http
POST /dataSets
```

**요청**

By including `unifiedProfile` and `unifiedIdentity` under `tags` in the request body, the dataset will be immediately enabled for Profile and Identity Service, respectively. The values of these tags must be an array containing the string `"enabled:true"`.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fileDescription" : {
    "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
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
| `schemaRef.id` | The ID of the Profile-enabled schema upon which the dataset will be based. |
| `{TENANT_ID}` | The namespace within the Schema Registry which contains resources belonging to your IMS Organization. See the [TENANT_ID](../../xdm/api/getting-started.md#know-your-tenant-id) section of the Schema Registry developer guide for more information. |

**응답**

A successful response shows an array containing the ID of the newly created dataset in the form of `"@/dataSets/{DATASET_ID}"`. Once you have successfully created and enabled a dataset, please proceed to the steps for [uploading data](#upload-data-to-the-dataset).

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
] 
```

## 기존 데이터 세트 구성 {#configure-an-existing-dataset}

The following steps cover how to enable a previously created dataset for Real-time Customer Profile and Identity Service. If you have already created a Profile-enabled dataset, please proceed to the steps for [ingesting data](#ingest-data-into-the-dataset).

### Check if the dataset is enabled {#check-if-the-dataset-is-enabled}

Using the Catalog API, you can inspect an existing dataset to determine whether it is enabled for use in Real-time Customer Profile and Identity Service. The following call retrieves the details of a dataset by ID.

**API 형식**

```http
GET /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DATASET_ID}` | 검사하려는 데이터 집합의 ID입니다. |

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
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
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

Under the `tags` property, you can see that `unifiedProfile` and `unifiedIdentity` are both present with the value `enabled:true`. 따라서 이 데이터 세트에 대해 실시간 고객 프로필 및 ID 서비스가 각각 활성화됩니다.

### Enable the dataset {#enable-the-dataset}

If the existing dataset has not been enabled for Profile or Identity Service, you can enable it by making a PATCH request using the dataset ID.

**API 형식**

```http
PATCH /dataSets/{DATASET_ID}
```

| 매개 변수 | 설명 |
|---|---|
| `{DATASET_ID}` | The ID of a dataset you want to update. |

**요청**

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b020a27e7040801dedbf46e \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags" : {
        "unifiedProfile": ["enabled:true"],
        "unifiedIdentity": ["enabled:true"]
    }
  }'
```

The request body includes a `tags` property, which contains two sub-properties: `"unifiedProfile"` and `"unifiedIdentity"`. The values of these sub-properties are arrays containing the string `"enabled:true"`.

**Response**
A successful PATCH request returns HTTP Status 200 (OK) and an array containing the ID of the updated dataset. This ID should match the one sent in the PATCH request. The `"unifiedProfile"` and `"unifiedIdentity"` tags have now been added and the dataset is enabled for use by Profile and Identity services.

```json
[
    "@/dataSets/5b020a27e7040801dedbf46e"
]
```

## 데이터를 데이터 세트에 인제스트 {#ingest-data-into-the-dataset}

Both Real-time Customer Profile and Identity Service consume XDM data as it is being ingested into a dataset. 데이터 세트에 데이터를 업로드하는 방법에 대한 지침은 API를 사용하여 데이터 세트 [를 만드는 방법에 대한 자습서를 참조하십시오](../../catalog/datasets/create.md). When planning what data to send to your Profile-enabled dataset, consider the following best practices:

- Include any data you want to use as audience segment criteria.
- Include as many identifiers as you can ascertain from your profile data to maximize your identity graph. This allows Identity Service to stitch identities across datasets more effectively.

## Confirm data ingest by Real-time Customer Profile {#confirm-data-ingest-by-real-time-customer-profile}

When uploading data to a new dataset for the first time, or as part of a process involving a new ETL or data source, it is recommended to carefully check the data to ensure it has been uploaded as expected. Using the Real-time Customer Profile Access API, you can retrieve batch data as it gets loaded into a dataset. If you are unable to retrieve any of the entities you expect, your dataset may not be enabled for Real-time Customer Profile. 데이터 세트가 활성화되었는지 확인한 후 소스 데이터 형식 및 식별자가 기대를 충족하는지 확인하십시오. For detailed instructions on how to use the Real-time Customer Profile API to access Profile data, please follow the [entities endpoint guide](../api/entities.md), also known as the &quot;Profile Access API&quot;.

## ID 서비스별 데이터 인제스트 확인 {#confirm-data-ingest-by-identity-service}

둘 이상의 ID를 포함하는 수집되는 각 데이터 조각은 개인 ID 그래프에 링크를 만듭니다. ID 그래프 및 ID 데이터에 대한 자세한 내용은 ID [서비스 개요를 읽어 보시기 바랍니다](../../identity-service/home.md).