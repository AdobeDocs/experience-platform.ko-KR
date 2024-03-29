---
keywords: Experience Platform;홈;인기 항목;데이터 세트 api;데이터 사용 관리;데이터 사용 api
solution: Experience Platform
title: API를 사용하여 데이터 세트의 데이터 사용 레이블 관리
description: 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와 별개입니다.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 1%

---

# API를 사용하여 데이터 세트의 데이터 사용 레이블 관리

다음 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 에서는 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 과는 별개입니다 [!DNL Catalog Service] 데이터 세트 메타데이터를 관리하는 API.

>[!IMPORTANT]
>
>데이터 세트 수준에서 레이블을 적용하는 것은 데이터 거버넌스 사용 사례에 대해서만 지원됩니다. 데이터에 대한 액세스 정책을 만들려면 다음을 수행해야 합니다 [스키마에 레이블 적용](../../xdm/tutorials/labels.md) 을 참조하십시오. 의 개요 보기 [속성 기반 액세스 제어](../../access-control/abac/overview.md) 추가 정보.

이 문서에서는 다음을 사용하여 데이터 세트 및 필드의 레이블을 관리하는 방법을 다룹니다. [!DNL Dataset Service API]. API 호출을 사용하여 데이터 사용 레이블 자체를 관리하는 방법에 대한 단계는 [labels endpoint 안내서](../api/labels.md) 대상: [!DNL Policy Service API].

## 시작하기

이 안내서를 읽기 전에 [시작 섹션](../../catalog/api/getting-started.md) 를 호출하는 데 필요한 자격 증명을 수집하려면 카탈로그 개발자 안내서에서 를 참조하십시오. [!DNL Platform] API.

이 문서에 설명된 끝점을 호출하려면 고유한 `id` 특정 데이터 세트에 대한 값입니다. 이 값이 없는 경우 의 안내서를 참조하십시오. [카탈로그 개체 나열](../../catalog/api/list-objects.md) 기존 데이터 세트의 ID를 찾습니다.

## 데이터 세트에 대한 레이블 조회 {#look-up}

에 GET 요청을 하여 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다. [!DNL Dataset Service] API.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 조회할 데이터 세트의 값입니다. |

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

전체 데이터 세트에 대한 레이블 세트를 POST 또는 PUT 요청의 페이로드에 제공하여 적용할 수 있습니다. [!DNL Dataset Service] API. 요청 본문은 두 호출에 대해 동일합니다. 개별 데이터 세트 필드에 레이블을 추가할 수 없습니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 만드는 데이터 세트의 값입니다. |

**요청**

아래의 예제 POST 요청은 전체 데이터 세트를 `C1` 레이블. 페이로드에 제공된 필드는 PUT 요청에 필요한 것과 동일합니다.

데이터 세트(PUT)의 기존 레이블을 업데이트하는 API 호출을 수행할 때 `If-Match` 데이터 세트 서비스에 있는 데이터 세트 레이블 엔티티의 현재 버전을 나타내는 헤더를 포함해야 합니다. 데이터 충돌을 방지하기 위해 서비스는 데이터 세트 엔티티가 포함된 경우에만 업데이트합니다 `If-Match` 문자열은 해당 데이터 세트에 대해 시스템에서 생성한 최신 버전 태그와 일치합니다.

>[!NOTE]
>
>해당 데이터 세트에 대한 레이블이 현재 있는 경우 새 레이블은 PUT 요청을 통해서만 추가할 수 있으며, 이 경우 다음이 필요합니다. `If-Match` 머리글입니다. 레이블이 데이터 세트에 추가되면 가장 최근입니다 `etag` 나중에 레이블을 업데이트하거나 제거하려면 값이 필요합니다.<br>PUT 메서드를 실행하기 전에 데이터 세트 레이블에 대한 GET 요청을 수행해야 합니다. 요청에서 수정할 특정 필드만 업데이트하고 나머지는 그대로 두십시오. 또한 PUT 호출이 GET 호출과 동일한 상위 엔티티를 유지하는지 확인합니다. 모든 불일치는 고객에게 오류를 발생시킵니다.

데이터 세트 레이블 엔티티의 최신 버전을 검색하려면 [GET 요청](#look-up) (으)로 `/datasets/{DATASET_ID}/labels` 엔드포인트. 현재 값은 아래 응답에 반환됩니다. `etag` 머리글입니다. 기존 데이터 세트 레이블을 업데이트할 때 가장 좋은 방법은 최신 데이터를 가져오기 위해 먼저 데이터 세트에 대한 조회 요청을 수행하는 것입니다 `etag` 에서 해당 값을 사용하기 전의 값 `If-Match` 후속 PUT 요청의 헤더.

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
| `entityId.namespace` | ID 충돌을 피하는 데 사용됩니다. 다음 `namespace` 은(는) `AEP`. |
| `entityId.id` | 업데이트 중인 리소스의 ID입니다. 이 참조는 `datasetId`. |
| `entityId.type` | 업데이트할 리소스의 유형입니다. 항상 다음과 같습니다. `dataset`. |
| `labels` | 전체 데이터 세트에 추가할 데이터 사용 레이블 목록입니다. |
| `parents` | 다음 `parents` 배열에 다음 목록이 포함됨: `entityId`이 데이터 세트가에서 레이블을 상속합니다. 데이터 세트는 스키마 및/또는 데이터 세트에서 레이블을 상속할 수 있습니다. |

**응답**

성공적인 응답은 데이터 세트에 대해 업데이트된 레이블 세트를 반환합니다.

>[!IMPORTANT]
>
>다음 `optionalLabels` 속성이 POST 요청에서 더 이상 사용되지 않습니다. 더 이상 데이터 세트 필드에 데이터 레이블을 추가할 수 없습니다. 다음 경우에 POST 작업에서 오류가 발생합니다 `optionalLabel` 값이 있습니다. 그러나 PUT 요청 및 을 사용하여 개별 필드에서 레이블을 삭제할 수 있습니다. `optionalLabels` 속성. 자세한 내용은 의 섹션을 참조하십시오. [데이터 세트에서 레이블 제거](#remove).

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

기존 을 업데이트하여 이전에 적용된 모든 필드 레이블을 제거할 수 있습니다 `optionalLabels` 기존 필드 레이블의 하위 집합이 있는 값이나 완전히 제거할 빈 목록이 있습니다. 에 PUT 요청 [!DNL Dataset Service] 이전에 적용된 레이블을 업데이트하거나 제거하는 API입니다.

**API 형식**

```http
PUT /datasets/{DATASET_ID}/labels
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 만드는 데이터 세트의 값입니다. |

**요청**

PUT 작업이 적용되는 아래 데이터 세트에는 속성/개인/속성/주소 필드의 C1 optionalLabel과 /properties/person/properties/name/properties/fullName 필드의 C1, C2 optionalLabels가 있습니다. put 작업 후, 첫 번째 필드에는 레이블이 없고(C1 레이블이 제거됨) 두 번째 필드에는 C1 레이블만 있습니다(C2 레이블이 제거됨)

아래 예제 시나리오에서는 개별 필드에 추가된 레이블을 제거하는 데 PUT 요청을 사용합니다. 요청이 수행되기 전에 `fullName` 필드에 `C1` 및 `C2` 적용된 레이블 및 `address` 필드에 이미 `C1` 레이블이 적용되었습니다. PUT 요청이 기존 레이블을 재정의합니다. `C1, C2` 의 레이블 `fullName` 이 있는 필드 `C1` 을 사용하여 레이블 지정 `optionalLabels.labels` 매개 변수. 또한 요청은 을 재정의합니다. `C1` 의 레이블 `address` 필드 레이블 세트가 비어 있는 필드.

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
| `entityId` | 이는 업데이트할 특정 데이터 세트 엔티티를 식별합니다. 다음 `entityId` 은(는) 다음 세 가지 값을 포함해야 합니다.<br/><br/>`namespace`: ID 충돌을 피하는 데 사용됩니다. 다음 `namespace` 은(는) `AEP`.<br/>`id`: 업데이트 중인 리소스의 ID입니다. 이 참조는 `datasetId`.<br/>`type`: 업데이트 중인 리소스의 유형입니다. 항상 다음과 같습니다. `dataset`. |
| `labels` | 전체 데이터 세트에 추가할 데이터 사용 레이블 목록입니다. |
| `parents` | 다음 `parents` 배열에 다음 목록이 포함됨: `entityId`이 데이터 세트가에서 레이블을 상속합니다. 데이터 세트는 스키마 및/또는 데이터 세트에서 레이블을 상속할 수 있습니다. |
| `optionalLabels` | 이 매개 변수는 데이터 세트 필드에 이전에 적용된 레이블을 제거하는 데 사용됩니다. 레이블을 제거할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다. <br/><br/>`option`: 다음을 포함하는 개체 [!DNL Experience Data Model] (XDM) 필드 속성입니다. 다음 세 가지 속성이 필요합니다.<ul><li><code>ID</code>: URI <code>$id</code> 필드와 연계된 스키마 값.</li><li><code>contentType</code>: 스키마의 콘텐츠 유형 및 버전 번호입니다. 유효한 형식 중 하나를 사용해야 합니다. <a href="../../xdm/api/getting-started.md#accept">Accept 헤더</a> XDM 조회 요청용.</li><li><code>schemaPath</code>: 데이터 세트 스키마 내의 필드에 대한 경로입니다.</li></ul>`labels`: 이 값은 적용된 기존 필드 레이블의 하위 집합을 포함하거나, 기존 필드 레이블을 모두 제거하려면 비워 두어야 합니다. 이제 PUT 또는 POST 메서드는 `optionalLabels` 필드에는 새 레이블이나 수정된 레이블이 있습니다. |

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

이 문서를 읽고 다음을 사용하여 데이터 세트 및 필드의 데이터 사용 레이블을 관리하는 방법을 배웠습니다. [!DNL Dataset Service] API. 이제 다음을 정의할 수 있습니다. [데이터 사용 정책](../policies/overview.md) 및 [액세스 제어 정책](../../access-control/abac/ui/policies.md) 적용한 레이블을 기반으로 합니다.

에서 데이터 세트 관리에 대한 자세한 내용 [!DNL Experience Platform], 다음을 참조하십시오. [데이터 세트 개요](../../catalog/datasets/overview.md).
