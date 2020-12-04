---
keywords: Experience Platform;home;popular topics;dataset;Dataset;create a dataset;create dataset
solution: Experience Platform
title: API를 사용하여 데이터 세트 만들기
topic: datasets
description: 이 문서에서는 Adobe Experience Platform API를 사용하여 데이터 세트를 만들고 파일을 사용하여 데이터 세트에 채우는 일반적인 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 1%

---


# API를 사용하여 데이터 세트 만들기

이 문서에서는 Adobe Experience Platform API를 사용하여 데이터 세트를 만들고 파일을 사용하여 데이터 세트에 채우는 일반적인 단계를 제공합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대한 작업 이해를 필요로 합니다.

* [일괄 처리](../../ingestion/batch-ingestion/overview.md): [!DNL Experience Platform] 데이터를 일괄 처리 파일로 인제스트할 수 있습니다.
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):고객 경험 데이터를 [!DNL Experience Platform] 구성하는 표준화된 프레임워크
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 API를 성공적으로 호출하기 위해 알아야 할 추가 정보를 [!DNL Platform] 제공합니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출 설명서에 사용된 규칙에 대한 자세한 내용은 문제 해결 안내서의 예제 API 호출 [을 읽는](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 [!DNL Experience Platform] 참조하십시오.

### 필수 헤더에 대한 값 수집

API를 호출하려면 [!DNL Platform] 먼저 [인증 자습서를 완료해야 합니다](../../tutorials/authentication.md). 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

의 모든 리소스 [!DNL Experience Platform] 는 특정 가상 샌드박스와 분리됩니다. API에 대한 모든 [!DNL Platform] 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>의 샌드박스에 대한 자세한 내용 [!DNL Platform]은 [샌드박스 개요 설명서를 참조하십시오](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* 컨텐츠 유형:application/json

## 자습서

데이터 세트를 만들려면 스키마를 먼저 정의해야 합니다. 스키마는 데이터를 나타내는 데 도움이 되는 규칙 세트입니다. 스키마는 데이터 구조를 설명하는 것 외에도 시스템 간에 이동할 때 적용할 수 있고 데이터를 검증하는 데 사용할 수 있는 제한과 기대를 제공합니다.

이러한 표준 정의를 사용하면 출처에 관계없이 데이터를 일관되게 해석할 수 있고 애플리케이션 간에 번역이 필요하지 않습니다. 스키마 구성에 대한 자세한 내용은 스키마 구성 [기본 사항에 대한 안내서를 참조하십시오](../../xdm/schema/composition.md)

## 데이터 집합 스키마 검색

이 자습서는 [스키마 레지스트리 API 자습서](../../xdm/tutorials/create-schema-api.md) 종료 지점에서 시작하여 해당 자습서 동안 생성된 충성도 멤버 스키마를 사용합니다.

튜토리얼을 완료하지 않은 경우 여기에서 시작하여 필요한 스키마를 만든 경우에만 이 데이터 세트 자습서로 계속하십시오. [!DNL Schema Registry]

다음 호출을 사용하여 [!DNL Schema Registry] API 자습서 중 만든 충성도 멤버 스키마를 볼 수 있습니다.

**API 형식**

```HTTP
GET /tenant/schemas/{schema meta:altId or URL encoded $id URI}
```

**요청**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

응답 개체의 형식은 요청에 전송된 수락 헤더에 따라 다릅니다. 이 응답의 개별 속성은 공간에 대해 최소화되었습니다.

```JSON
{
    "type": "object",
    "title": "Loyalty Members",
    "description": "Information for all members of the loyalty program",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/bb118e507bb848fd85df68fedea70c62"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9",
    "meta:xdmType": "object",
    "properties": {
        "repositoryCreatedBy": {},
        "repositoryLastModifiedBy": {},
        "createdByBatchID": {},
        "modifiedByBatchID": {},
        "_repo": {},
        "identityMap": {},
        "_id": {},
        "timeSeriesEvents": {},
        "person": {},
        "homeAddress": {},
        "personalEmail": {},
        "homePhone": {},
        "mobilePhone": {},
        "faxPhone": {},
        "_{TENANT_ID}": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "loyalty": {
                    "title": "Loyalty",
                    "description": "Loyalty Info",
                    "type": "object",
                    "meta:xdmType": "object",
                    "meta:referencedFrom": "https://ns.adobe.com/{TENANT_ID}/datatypes/49b594dabe6bec545c8a6d1a0991a4dd",
                    "properties": {
                        "loyaltyId": {
                            "title": "Loyalty Identifier",
                            "type": "string",
                            "description": "Loyalty Identifier.",
                            "meta:xdmType": "string"
                        },
                        "loyaltyLevel": {
                            "title": "Loyalty Level",
                            "type": "string",
                            "meta:xdmType": "string"
                        },
                        "loyaltyPoints": {
                            "title": "Loyalty Points",
                            "type": "integer",
                            "description": "Loyalty points total.",
                            "meta:xdmType": "int"
                        },
                        "memberSince": {
                            "title": "Member Since",
                            "type": "string",
                            "format": "date-time",
                            "description": "Date the member joined the Loyalty Program.",
                            "meta:xdmType": "date-time"
                        }
                    }
                }
            }
        }
    },
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "version": "1.4",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1551836845496,
        "repo:lastModifiedDate": 1551843052271,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## 데이터 세트 만들기

충성도 멤버 스키마를 사용하여 스키마를 참조하는 데이터 세트를 만들 수 있습니다.

**API 형식**

```HTTP
POST /dataSets
```

**요청**

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

>[!NOTE]
>
>이 자습서에서는 모든 예에 대해 [쪽모이](https://parquet.apache.org/documentation/latest/) 세공 파일 형식을 사용합니다. JSON 파일 형식을 사용하는 예는 [일괄 처리 통합 개발자 안내서에서 확인할 수 있습니다](../../ingestion/batch-ingestion/api-overview.md)

**응답**

성공적인 응답은 HTTP Status 201(Created)과 새로 만든 데이터 집합의 ID가 포함된 배열로 구성된 응답 개체를 반환합니다 `"@/datasets/{DATASET_ID}"`. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```

## 일괄 처리 만들기

데이터 세트에 데이터를 추가하려면 먼저 데이터 세트에 연결된 배치를 만들어야 합니다. 그런 다음 배치를 업로드하는 데 사용합니다.

**API 형식**

```HTTP
POST /batches
```

**요청**

요청 본문에는 &quot;datasetId&quot; 필드가 포함되어 있는데, 이 필드의 값은 이전 단계에서 생성된 `{DATASET_ID}` 것입니다.

```SHELL
curl -X POST 'https://platform.adobe.io/data/foundation/import/batches' \
  -H 'accept: application/json' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key : {API_KEY}' \
  -H 'content-type: application/json' \
  -d '{
        "datasetId":"5c8c3c555033b814b69f947f"
      }'
```

**응답**

성공적인 응답은 HTTP Status 201(Created)과 시스템에서 생성된 문자열, 읽기 전용 등 새로 만든 일괄 처리 `id`의 세부 사항이 포함된 응답 개체를 반환합니다.

```JSON
{
    "id": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "imsOrg": "{IMS_ORG}",
    "updated": 1552694873602,
    "status": "loading",
    "created": 1552694873602,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "5c8c3c555033b814b69f947f"
        }
    ],
    "version": "1.0.0",
    "tags": {
        "acp_producer": [
            "{CREATED_CLIENT}"
        ],
        "acp_stagePath": [
            "{CREATED_CLIENT}/stage/5d01230fc78a4e4f8c0c6b387b4b8d1c"
        ],
        "use_plan_b_batch_status": [
            "false"
        ]
    },
    "createdUser": "{CREATED_BY}",
    "updatedUser": "{CREATED_BY}",
    "externalId": "5d01230fc78a4e4f8c0c6b387b4b8d1c",
    "createdClient": "{CREATED_CLIENT}",
    "inputFormat": {
        "format": "parquet"
    }
}
```

## 일괄 처리에 파일 업로드

업로드용 새 일괄 처리를 성공적으로 만든 후 이제 특정 데이터 세트에 파일을 업로드할 수 있습니다. 데이터 세트를 정의할 때 파일 형식을 쪽모이 세공기로 지정했다는 점을 기억해야 합니다. 따라서 업로드하는 파일은 해당 형식이어야 합니다.

>[!NOTE]
>
>지원되는 최대 데이터 업로드 파일은 512MB입니다. 데이터 파일이 이보다 큰 경우 한 번에 하나씩 업로드하려면 512MB 이하의 청크로 분할해야 합니다. 동일한 배치 ID를 사용하여 각 파일에 대해 이 단계를 반복하여 동일한 일괄 처리에 있는 각 파일을 업로드할 수 있습니다. 일괄 처리의 일부로 업로드할 수 있는 파일의 경우 수에 제한이 없습니다.

**API 형식**

```http
PUT /batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BATCH_ID}` | 업로드하려는 배치 `id` 의 이름입니다. |
| `{DATASET_ID}` | 일괄 처리 `id` 가 유지될 데이터 세트. |
| `{FILE_NAME}` | 업로드하려는 파일의 이름입니다. |

**요청**

```SHELL
curl -X PUT 'https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c/datasets/5c8c3c555033b814b69f947f/files/loyaltyData.parquet' \
  -H 'content-type: application/octet-stream' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  --data-binary '@{FILE_PATH_AND_NAME}.parquet'
```

**응답**

파일을 업로드하면 빈 응답 본문과 HTTP 상태 200(OK)이 반환됩니다.

## 신호 배치 완료

모든 데이터 파일을 일괄 처리에 업로드한 후 일괄 처리를 완료하도록 신호를 보낼 수 있습니다. 신호 완료 시 서비스가 업로드된 파일에 대한 [!DNL Catalog] `DataSetFile` 항목을 만들고 이전에 생성된 일괄 처리에 연결합니다. 일괄 처리 [!DNL Catalog] 가 성공적으로 표시되어 현재 사용 가능한 데이터에서 작동할 수 있는 모든 다운스트림 흐름을 트리거합니다.

**API 형식**

```HTTP
POST /batches/{BATCH_ID}?action=COMPLETE
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BATCH_ID}` | 표시된 배치 `id` 의 완료 |

**요청**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/5d01230fc78a4e4f8c0c6b387b4b8d1c?action=COMPLETE" \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**응답**

성공적으로 일괄 처리를 완료하면 빈 응답 본문과 HTTP 상태 200(OK)이 반환됩니다.

## 통합 모니터링

데이터 크기에 따라 배치는 인제스트하는 데 다양한 시간이 소요됩니다. 배치 ID가 포함된 `batch` 요청 매개 변수를 요청에 추가하여 일괄 처리 상태를 모니터링할 수 `GET /batches` 있습니다. API는 배치의 통합 상태를 데이터 세트에 폴링하여 응답의 `status` 가 완료(&quot;성공&quot; 또는 &quot;실패&quot;)를 나타냅니다.

**API 형식**

```HTTP
GET /batches?batch={BATCH_ID}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BATCH_ID}` | 모니터링할 배치 `id` 의 이름입니다. |

**요청**

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?batch=5d01230fc78a4e4f8c0c6b387b4b8d1c' \
  -H 'x-api-key : {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMG_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**응답**

긍정적인 응답은 값이 포함된 `status` 속성을 가진 개체를 `success`반환합니다.

```JSON
{
    "5b7129a879323401ef2a6486": {
        "imsOrg": "{IMS_ORG}",
        "created": 1534142888068,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1534142955152,
        "replay": {},
        "status": "success",
        "errors": [],
        "version": "1.0.3",
        "availableDates": {},
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "metrics": {
            "startTime": 1534142943819,
            "endTime": 1534142951760,
            "recordsRead": 108,
            "recordsWritten": 108
        }
    }
}
```

음수 응답은 해당 속성에 값이 있는 객체 `"failed"` 를 반환하고 관련 오류 `"status"` 메시지를 포함합니다.

```JSON
{
    "5b96ce65badcf701e51f075d": {
        "imsOrg": "{IMS_ORG}",
        "status": "failed",
        "relatedObjects": [
            {
                "type": "batch",
                "id": "29285e08378f4a41827e7e70fb7cb8f0"
            }
        ],
        "replay": {},
        "availableDates": {},
        "metrics": {
            "startTime": 1536610322329,
            "endTime": 1536610438083,
            "recordsRead": 4004,
            "recordsWritten": 4004,
            "failureReason": "Job aborted due to stage failure: Task 0 in stage 1.0 failed 4 times,:"
        },
        "errors": [
            {
                "code": "0070000017",
                "description": "Unknown error occurred."
            },
            {
                "code": "unknown",
                "description": "Job aborted."
            }
        ],
        "created": 1536609893629,
        "createdClient": "{CREATED_CLIENT}",
        "createdUser": "{CREATED_BY}",
        "updatedUser": "{CREATED_BY}",
        "updated": 1536610442814,
        "version": "1.0.5"
    }
}
```

>[!NOTE]
>
>권장되는 폴링 간격은 2분입니다.

## 데이터 세트에서 데이터 읽기

배치 ID를 사용하여 데이터 액세스 API를 사용하여 일괄 처리에 업로드된 모든 파일을 다시 읽고 확인할 수 있습니다. 응답에서는 일괄 처리에서 파일을 참조하는 파일 ID 목록이 포함된 배열을 반환합니다.

데이터 액세스 API를 사용하여 이름, 크기(바이트) 및 링크를 반환하여 파일이나 폴더를 다운로드할 수도 있습니다.

데이터 액세스 API 작업에 대한 자세한 단계는 [데이터 액세스 개발자 안내서를 참조하십시오](../../data-access/home.md).

## 데이터 집합 스키마 업데이트

만든 데이터 세트에 필드를 추가하고 추가 데이터를 인제스트할 수 있습니다. 이렇게 하려면 먼저 새 데이터를 정의하는 추가 속성을 추가하여 스키마를 업데이트해야 합니다. PATCH 및/또는 PUT 작업을 사용하여 기존 스키마를 업데이트할 수 있습니다.

스키마 업데이트에 대한 자세한 내용은 스키마 [레지스트리 API 개발자 안내서를 참조하십시오](../../xdm/api/getting-started.md).

스키마를 업데이트한 후에는 이 튜토리얼의 단계를 다시 수행하여 수정된 스키마를 준수하는 새 데이터를 인제스트할 수 있습니다.

스키마 진화는 순전히 부가적이라는 것을 기억해야 합니다. 이는 스키마 변경이 레지스트리에 저장되고 데이터 섭취에 사용된 후에는 새로운 변경 사항을 적용할 수 없다는 의미입니다. Adobe Experience Platform에서 사용할 스키마 작성에 대한 우수 사례에 대한 자세한 내용은 스키마 구성 [기본 사항에 대한 안내서를 참조하십시오](../../xdm/schema/composition.md).