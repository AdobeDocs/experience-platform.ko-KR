---
keywords: Experience Platform;홈;인기 항목;데이터 세트 api;데이터 사용 관리;데이터 사용 api
solution: Experience Platform
title: API를 사용하여 데이터 세트의 데이터 사용 레이블 관리
description: 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와 별개입니다.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 9eda7068eb2a3fd5e59fbeff69c85abfad5ccf39
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 1%

---

# API를 사용하여 데이터 세트의 데이터 사용 레이블 관리

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/)을(를) 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 [!DNL Catalog Service] API와 별개입니다.

>[!IMPORTANT]
>
>데이터 세트 수준에서 레이블을 적용하는 것은 데이터 거버넌스 사용 사례에 대해서만 지원됩니다. 데이터에 대한 액세스 정책을 만들려면 데이터 집합이 기반으로 하는 [스키마에 레이블을 적용](../../xdm/tutorials/labels.md)해야 합니다. 자세한 내용은 [특성 기반 액세스 제어](../../access-control/abac/overview.md)에 대한 개요를 참조하십시오.

이 문서에서는 [!DNL Dataset Service API]을(를) 사용하여 데이터 세트 및 필드의 레이블을 관리하는 방법을 다룹니다. API 호출을 사용하여 데이터 사용 레이블 자체를 관리하는 방법에 대한 단계는 [!DNL Policy Service API]의 [레이블 끝점 안내서](../api/labels.md)를 참조하십시오.

## 시작하기

이 안내서를 읽기 전에 카탈로그 개발자 안내서의 [시작 섹션](../../catalog/api/getting-started.md)에 설명된 단계에 따라 [!DNL Platform] API를 호출하는 데 필요한 자격 증명을 수집합니다.

이 문서에 설명된 끝점을 호출하려면 특정 데이터 세트에 대해 고유한 `id` 값이 있어야 합니다. 이 값이 없으면 [카탈로그 개체 나열](../../catalog/api/list-objects.md)에 대한 안내서를 참조하여 기존 데이터 세트의 ID를 찾으십시오.

## 데이터 세트에 대한 레이블 조회 {#look-up}

[!DNL Dataset Service] API에 대한 GET 요청을 통해 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 조회할 데이터 세트의 고유한 `id` 값입니다. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트에 적용된 데이터 사용 레이블을 반환합니다.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `labels` | 데이터 세트에 적용된 데이터 사용 레이블 목록입니다. |
| `optionalLabels` | 데이터 세트 내에 데이터 사용 레이블이 적용된 개별 필드의 목록입니다. |

## 데이터 세트에 레이블 적용 {#apply}

전체 데이터 세트에 대한 레이블 집합을 POST 또는 PUT 요청의 페이로드에서 [!DNL Dataset Service] API에 제공하여 적용할 수 있습니다. 요청 본문은 두 호출에 대해 동일합니다. 개별 데이터 세트 필드에 레이블을 추가할 수 없습니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만드는 데이터 집합의 고유한 `id` 값입니다. |

**요청**

아래의 예제 POST 요청은 `C1` 레이블로 전체 데이터 세트를 업데이트합니다. 페이로드에 제공된 필드는 PUT 요청에 필요한 것과 동일합니다.

데이터 집합(PUT)의 기존 레이블을 업데이트하는 API를 호출할 때 데이터 집합 서비스에 있는 데이터 집합 레이블 엔터티의 현재 버전을 나타내는 `If-Match` 헤더를 포함해야 합니다. 데이터 충돌을 방지하기 위해 포함된 `If-Match` 문자열이 해당 데이터 세트에 대해 시스템에서 생성된 최신 버전 태그와 일치하는 경우에만 서비스가 데이터 세트 엔터티를 업데이트합니다.

>[!NOTE]
>
>해당 데이터 세트에 대한 레이블이 현재 있는 경우 `If-Match` 헤더가 필요한 PUT 요청을 통해서만 새 레이블을 추가할 수 있습니다. 레이블이 데이터 집합에 추가되면 나중에 레이블을 업데이트하거나 제거하려면 가장 최근 `etag` 값이 필요합니다.<br>PUT 메서드를 실행하기 전에 데이터 집합 레이블에 대한 GET 요청을 수행해야 합니다. 요청에서 수정할 특정 필드만 업데이트하고 나머지는 그대로 두십시오. 또한 PUT 호출이 GET 호출과 동일한 상위 엔티티를 유지하는지 확인합니다. 모든 불일치는 고객에게 오류를 발생시킵니다.

데이터 집합 레이블 엔터티의 최신 버전을 검색하려면 `/datasets/{DATASET_ID}/labels` 끝점에 대해 [GET 요청](#look-up)을 만듭니다. 현재 값은 `etag` 헤더 아래의 응답에서 반환됩니다. 기존 데이터 세트 레이블을 업데이트할 때 가장 좋은 방법은 후속 PUT 요청의 `If-Match` 헤더에서 해당 값을 사용하기 전에 최신 `etag` 값을 가져오기 위해 먼저 데이터 세트에 대한 조회 요청을 수행하는 것입니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| 속성 | 설명 |
| --- | --- |
| `entityId` | 이는 업데이트할 특정 데이터 세트 엔티티를 식별합니다. |
| `entityId.namespace` | ID 충돌을 피하는 데 사용됩니다. `namespace`은(는) `AEP`입니다. |
| `entityId.id` | 업데이트 중인 리소스의 ID입니다. `datasetId`을(를) 참조합니다. |
| `entityId.type` | 업데이트할 리소스의 유형입니다. 항상 `dataset`입니다. |
| `labels` | 전체 데이터 세트에 추가할 데이터 사용 레이블 목록입니다. |
| `parents` | `parents` 배열에 이 데이터 집합이 레이블을 상속할 `entityId`의 목록이 포함되어 있습니다. 데이터 세트는 스키마 및/또는 데이터 세트에서 레이블을 상속할 수 있습니다. |

**응답**

성공적인 응답은 데이터 세트에 대해 업데이트된 레이블 세트를 반환합니다.

>[!IMPORTANT]
>
>`optionalLabels` 속성은 POST 요청에 사용되지 않습니다. 더 이상 데이터 세트 필드에 데이터 레이블을 추가할 수 없습니다. `optionalLabel` 값이 있으면 POST 작업에서 오류가 발생합니다. 그러나 PUT 요청과 `optionalLabels` 속성을 사용하여 개별 필드에서 레이블을 삭제할 수 있습니다. 자세한 내용은 [데이터 집합에서 레이블 제거](#remove)에 대한 섹션을 참조하십시오.

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## 데이터 세트에서 레이블 제거 {#remove}

기존 필드 레이블의 하위 집합으로 기존 `optionalLabels` 값을 업데이트하거나, 빈 목록을 업데이트하여 완전히 제거하여 이전에 적용된 모든 필드 레이블을 제거할 수 있습니다. [!DNL Dataset Service] API에 PUT 요청을 하여 이전에 적용된 레이블을 업데이트하거나 제거합니다.

>[!NOTE]
>
>`labels` 매개 변수에 대해 빈 목록을 제공하여 데이터 집합의 레이블을 완전히 제거할 수 있습니다. 데이터 세트에서 레이블을 유지하는 것은 필수가 아닙니다.

**API 형식**

```http
PUT /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만드는 데이터 집합의 고유한 `id` 값입니다. |

**요청**

PUT 작업이 적용되는 아래 데이터 세트에는 속성/개인/속성/주소 필드의 C1 optionalLabel과 /properties/person/properties/name/properties/fullName 필드의 C1, C2 optionalLabels가 있습니다. put 작업 후, 첫 번째 필드에는 레이블이 없고(C1 레이블이 제거됨) 두 번째 필드에는 C1 레이블만 있습니다(C2 레이블이 제거됨)

아래 예제 시나리오에서는 개별 필드에 추가된 레이블을 제거하는 데 PUT 요청을 사용합니다. 요청이 이루어지기 전에 `fullName` 필드에 `C1` 및 `C2` 레이블이 적용되었으며 `address` 필드에 이미 `C1` 레이블이 적용되었습니다. PUT 요청은 `optionalLabels.labels` 매개 변수를 사용하여 `C1` 레이블이 있는 `fullName` 필드의 기존 레이블 `C1, C2` 레이블을 재정의합니다. 또한 이 요청은 필드 레이블 집합이 비어 있는 `address` 필드의 `C1` 레이블을 재정의합니다.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| 매개변수 | 설명 |
| --- | --- |
| `entityId` | 이는 업데이트할 특정 데이터 세트 엔티티를 식별합니다. `entityId`에는 다음 세 개의 값이 포함되어야 합니다.<br/><br/>`namespace`: ID 충돌을 방지하는 데 사용됩니다. `namespace`은(는) `AEP`입니다.<br/>`id`: 업데이트하는 리소스의 ID입니다. `datasetId`을(를) 참조합니다.<br/>`type`: 업데이트하는 리소스의 유형입니다. 항상 `dataset`입니다. |
| `labels` | 전체 데이터 세트에 추가할 데이터 사용 레이블 목록입니다. |
| `parents` | `parents` 배열에 이 데이터 집합이 레이블을 상속할 `entityId`의 목록이 포함되어 있습니다. 데이터 세트는 스키마 및/또는 데이터 세트에서 레이블을 상속할 수 있습니다. |
| `optionalLabels` | 이 매개 변수는 데이터 세트 필드에 이전에 적용된 레이블을 제거하는 데 사용됩니다. 레이블을 제거할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다. <br/><br/>`option`: 필드의 [!DNL Experience Data Model](XDM) 특성을 포함하는 개체입니다. 다음 세 가지 속성이 필요합니다.<ul><li><code>id</code>: URI <code>$id</code> 필드와 연계된 스키마 값.</li><li><code>contentType</code>: 스키마의 콘텐츠 유형 및 버전 번호입니다. XDM 조회 요청에 대해 유효한 <a href="../../xdm/api/getting-started.md#accept">Accept 헤더</a> 중 하나의 형식을 사용해야 합니다.</li><li><code>schemaPath</code>: 데이터 세트 스키마 내의 필드에 대한 경로입니다.</li></ul>`labels`: 이 값은 적용된 기존 필드 레이블의 하위 집합을 포함하거나, 기존 필드 레이블을 모두 제거하려면 비워 두어야 합니다. 이제 `optionalLabels` 필드에 새 레이블이나 수정된 레이블이 있는 경우 PUT 또는 POST 메서드가 오류를 반환합니다. |

**응답**

성공적인 응답은 데이터 세트에 대해 업데이트된 레이블 세트를 반환합니다.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## 다음 단계

이 문서를 읽고 [!DNL Dataset Service] API를 사용하여 데이터 세트 및 필드의 데이터 사용 레이블을 관리하는 방법을 배웠습니다. 이제 적용한 레이블을 기반으로 [데이터 사용 정책](../policies/overview.md) 및 [액세스 제어 정책](../../access-control/abac/ui/policies.md)을(를) 정의할 수 있습니다.

[!DNL Experience Platform]의 데이터 세트 관리에 대한 자세한 내용은 [데이터 세트 개요](../../catalog/datasets/overview.md)를 참조하십시오.
