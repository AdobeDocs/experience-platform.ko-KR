---
keywords: Experience Platform;홈;인기 항목;데이터 세트 api;데이터 사용 관리;데이터 사용 api
solution: Experience Platform
title: API를 사용하여 데이터 세트에 대한 데이터 사용 레이블 관리
topic-legacy: developer guide
description: 데이터 세트 서비스 API를 사용하면 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와는 별개입니다.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 1%

---

# API를 사용하여 데이터 세트에 대한 데이터 사용 레이블 관리

다음 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 데이터 세트에 대한 사용 레이블을 적용하고 편집할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 이 기능과는 별개입니다 [!DNL Catalog Service] 데이터 세트 메타데이터를 관리하는 API입니다.

>[!IMPORTANT]
>
>데이터 세트 수준에서 레이블을 적용하는 것은 데이터 거버넌스 사용 사례에만 지원됩니다. 데이터에 대한 액세스 정책을 만들려고 하는 경우 다음을 수행해야 합니다 [스키마에 레이블 적용](../../xdm/tutorials/labels.md) 데이터 세트가 기반으로 합니다. 다음 사항에 대한 개요를 참조하십시오. [속성 기반 액세스 제어](../../access-control/abac/overview.md) 추가 정보.

이 문서에서는 [!DNL Dataset Service API]. API 호출을 사용하여 데이터 사용 레이블을 직접 관리하는 방법에 대한 단계는 를 참조하십시오. [레이블 끝점 안내서](../api/labels.md) 대상 [!DNL Policy Service API].

## 시작하기

이 안내서를 읽기 전에 [시작 섹션](../../catalog/api/getting-started.md) 를 호출하는 데 필요한 자격 증명을 수집하기 위한 카탈로그 개발자 가이드의 입니다. [!DNL Platform] API.

이 문서에 설명된 끝점을 호출하려면 고유한 가 있어야 합니다 `id` 값을 지정한 경우 이해할 수 있도록 해줍니다. 이 값이 없는 경우 다음 안내서를 참조하십시오 [카탈로그 객체 나열](../../catalog/api/list-objects.md) 기존 데이터 세트의 ID를 찾습니다.

## 데이터 세트에 대한 레이블 조회 {#look-up}

에 GET 요청을 만들어 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다 [!DNL Dataset Service] API.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 조회할 데이터 세트 값입니다. |

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
| `labels` | 데이터 집합에 적용된 데이터 사용 레이블 목록입니다. |
| `optionalLabels` | 데이터 세트 내에 데이터 사용 레이블이 적용된 개별 필드 목록입니다. |

## 데이터 세트에 레이블 적용 {#apply}

데이터 세트에 대한 레이블 세트를 POST 또는 PUT 요청의 페이로드에 제공하여 만들 수 있습니다 [!DNL Dataset Service] API. 이 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에 제공된 레이블로 대체합니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 고유 `id` 레이블을 만드는 데이터 세트의 값입니다. |

**요청**

아래 PUT 요청 예는 데이터 세트에 대한 기존 레이블과 해당 데이터 세트 내의 특정 필드를 업데이트합니다. 페이로드에 제공된 필드는 POST 요청에 필요한 필드와 동일합니다.

데이터 세트(PUT)의 기존 레이블을 업데이트하는 API를 호출할 때 `If-Match` 데이터 세트 서비스에 있는 데이터 세트 레이블 엔티티의 현재 버전을 나타내는 헤더를 포함해야 합니다. 데이터 충돌을 방지하기 위해 서비스는 포함된 경우 데이터 세트 엔티티만 업데이트합니다 `If-Match` 문자열은 해당 데이터 세트에 대해 시스템에서 생성한 최신 버전 태그와 일치합니다.

>[!NOTE]
>
>현재 해당 데이터 세트에 대한 레이블이 없는 경우 새 레이블은 POST 요청을 통해서만 추가할 수 있으며 이것은 를 필요로 하지 않습니다 `If-Match` 헤더. 데이터 세트에 레이블을 추가하면 `etag` 값은 나중에 레이블을 업데이트하거나 제거하는 데 사용할 수 있습니다.

데이터 세트 레이블 엔티티의 최신 버전을 검색하려면 다음을 수행하십시오 [GET 요청](#look-up) 변환 후 `/datasets/{DATASET_ID}/labels` 엔드포인트. 현재 값은 `etag` 헤더. 기존 데이터 세트 레이블을 업데이트할 때 가장 좋은 방법은 먼저 데이터 집합에 대한 조회 요청을 수행하여 최신 데이터를 가져오는 것입니다 `etag` 값에서 해당 값을 사용하기 전에 `If-Match` 헤더 를 입력합니다.

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
      }'
```

| 속성 | 설명 |
| --- | --- |
| `labels` | 데이터 세트에 추가할 데이터 사용 레이블 목록입니다. |
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다. <br/><br/>`option`: 를 포함하는 개체 [!DNL Experience Data Model] 필드의 (XDM) 속성입니다. 다음 세 가지 속성이 필요합니다.<ul><li>id</code>: URI $id</code> 필드와 연관된 스키마의 값입니다.</li><li>contentType</code>: 스키마의 컨텐츠 유형 및 버전 번호입니다. 이것은 유효한 것 중 하나의 형태를 취합니다 <a href="../../xdm/api/getting-started.md#accept">헤더 수락</a> XDM 조회 요청에 대한 것입니다.</li><li>schemaPath</code>: 데이터 집합 스키마 내의 필드에 대한 경로입니다.</li></ul>`labels`: 필드에 추가할 데이터 사용 레이블 목록입니다. |

**응답**

성공적인 응답은 데이터 세트에 대해 업데이트된 레이블 세트를 반환합니다.

```json
{
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
```

## 다음 단계

이 문서를 읽은 후에는 [!DNL Dataset Service] API. 이제 다음을 정의할 수 있습니다 [데이터 사용 정책](../policies/overview.md) 및 [액세스 제어 정책](../../access-control/abac/ui/policies.md) 적용한 레이블을 기준으로 합니다.

의 데이터 세트 관리에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [데이터 세트 개요](../../catalog/datasets/overview.md).
