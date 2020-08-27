---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'API를 사용하여 데이터 세트에 대한 데이터 사용 레이블 관리 '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 2%

---


# API를 사용하여 데이터 세트에 대한 데이터 사용 레이블 관리

[!DNL 데이터 집합 서비스 API] [를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) 사용하면 데이터 집합에 대한 사용 레이블을 적용하고 편집할 수 있습니다. 이것은 Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 [!DNL Catalog Service] API와는 별개입니다.

이 문서에서는 데이터 세트 및 필드를 사용하여 레이블을 관리하는 방법을 설명합니다 [!DNL Dataset Service API]. API 호출을 사용하여 데이터 사용량 레이블을 직접 관리하는 방법에 대한 단계는 [레이블 끝점 안내서](../api/labels.md) 를 [!DNL Policy Service API]참조하십시오.

## 시작하기

이 안내서를 읽기 전에 카탈로그 개발자 안내서의 [시작 섹션에](../../catalog/api/getting-started.md) 설명된 단계에 따라 API를 호출하는 데 필요한 자격 증명을 [!DNL Platform] 수집합니다.

이 문서에 나와 있는 끝점에 대한 호출을 하려면 특정 데이터 세트에 대한 고유한 `id` 값이 있어야 합니다. 이 값이 없는 경우 카탈로그 개체 [를 나열하는](../../catalog/api/list-objects.md) 가이드에서 기존 데이터 집합의 ID를 찾습니다.

## 데이터 세트에 대한 레이블 검색 {#look-up}

API에 GET 요청을 수행하여 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 [!DNL Dataset Service] 있습니다.

**API 형식**

```http
GET /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 조회하려는 데이터 세트의 고유한 `id` 값. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 데이터 세트에 적용된 데이터 사용 레이블을 반환합니다.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `optionalLabels` | 데이터 사용 레이블이 적용된 데이터 세트 내의 개별 필드 목록입니다. |

## 데이터 세트에 레이블 적용 {#apply}

POST 또는 PUT 요청의 페이로드에서 [!DNL Dataset Service] API에 제공하여 데이터 세트에 대한 레이블 세트를 만들 수 있습니다. 이러한 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에서 제공되는 레이블로 바꿉니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만드는 데이터 세트의 고유한 `id` 값입니다. |

**요청**

다음 PUT 요청은 데이터 세트에 대한 기존 레이블과 해당 데이터 세트 내의 특정 필드를 업데이트합니다. 페이로드에서 제공되는 필드는 POST 요청에 필요한 필드와 동일합니다.

>[!IMPORTANT]
>
>종단점에 대한 PUT 요청을 만들 때 올바른 `If-Match` 헤더를 `/datasets/{DATASET_ID}/labels` 제공해야 합니다. 필요한 헤더 사용에 대한 자세한 내용은 [부록 섹션을](#if-match) 참조하십시오.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다. <br/><br/>`option`:필드의 [!DNL Experience Data Model] (XDM) 속성을 포함하는 개체 다음 세 가지 속성이 필요합니다.<ul><li>id</code>:필드와 연결된 스키마의 URI $id</code> 값입니다.</li><li>contentType</code>:스키마의 컨텐츠 유형 및 버전 번호입니다. XDM 조회 요청에 대해 유효한 <a href="../../xdm/api/look-up-resource.md">수락 헤더</a> 중 하나의 형태를 가져야 합니다.</li><li>schemaPath</code>:데이터 집합 스키마 내의 필드 경로입니다.</li></ul>`labels`:필드에 추가할 데이터 사용 레이블 목록입니다. |

**응답**

성공적인 응답은 데이터 세트에 추가된 레이블을 반환합니다.

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

## 데이터 세트에서 레이블 제거 {#remove}

API에 DELETE 요청을 만들어 데이터 세트에 적용된 레이블을 제거할 수 [!DNL Dataset Service] 있습니다.

**API 형식**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 제거할 데이터 세트의 고유한 `id` 값. |

**요청**

다음 요청은 경로에 지정된 데이터 세트에 대한 레이블을 제거합니다.

>[!IMPORTANT]
>
>종단점에 대한 DELETE 요청을 만들 때 올바른 `If-Match` 헤더를 `/datasets/{DATASET_ID}/labels` 제공해야 합니다. 필요한 헤더 사용에 대한 자세한 내용은 [부록 섹션을](#if-match) 참조하십시오.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**응답**

레이블이 제거되었음을 나타내는 성공적인 응답 HTTP 상태 200(확인)입니다. 데이터 세트에 대한 기존 레이블 [을](#look-up) 별도의 호출로 검색하여 확인할 수 있습니다.

## 다음 단계

이 문서를 읽음으로써 [!DNL Dataset Service] API를 사용하여 데이터 세트 및 필드에 대한 데이터 사용 레이블을 관리하는 방법을 학습했습니다.

데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가하면 데이터 인제스트를 시작할 수 있습니다 [!DNL Experience Platform]. 자세한 내용은 [데이터 수집 설명서를 참조하십시오](../../ingestion/home.md).

적용된 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](../policies/overview.md).

데이터 집합 관리에 대한 자세한 내용 [!DNL Experience Platform]은 [데이터 집합 개요를 참조하십시오](../../catalog/datasets/overview.md).

## 부록 {#appendix}

다음 섹션에는 데이터 세트 서비스 API를 사용한 레이블 작업에 대한 추가 정보가 포함되어 있습니다.

### [!DNL If-Match] header {#if-match}

데이터 세트(PUT 및 DELETE)의 기존 레이블을 업데이트하는 API 호출을 수행할 때 데이터 세트 서비스에 있는 데이터 세트 레이블 엔티티의 현재 버전을 나타내는 헤더가 포함되어야 합니다. `If-Match` 데이터 충돌을 방지하기 위해 포함된 `If-Match` 문자열이 해당 데이터 세트에 대해 시스템에서 생성된 최신 버전 태그와 일치하는 경우에만 데이터 집합 엔터티가 업데이트됩니다.

>[!NOTE]
>
>현재 해당 데이터 세트에 대한 레이블이 없는 경우, 새 레이블은 POST 요청을 통해서만 추가할 수 있으며, 이것은 `If-Match` 헤더가 필요하지 않습니다. 데이터 세트에 레이블을 추가하면 나중에 레이블을 업데이트하거나 제거하는 데 사용할 수 있는 `etag` 값이 할당됩니다.

데이터 집합 레이블 엔터티의 최신 버전을 검색하려면 끝점에 [GET](#look-up) 요청을 `/datasets/{DATASET_ID}/labels` 하십시오. 현재 값은 헤더 아래의 응답으로 `etag` 반환됩니다. 기존 데이터 집합 레이블을 업데이트할 때, 이후 PUT 또는 DELETE 요청의 헤더에 해당 값을 사용하기 전에 데이터 세트에 대한 조회 요청을 먼저 수행하는 것이 좋습니다. `etag` `If-Match`