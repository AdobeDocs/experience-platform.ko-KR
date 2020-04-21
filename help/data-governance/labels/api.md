---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'API를 사용하여 데이터 사용 레이블 관리 '
topic: developer guide
translation-type: tm+mt
source-git-commit: cac6ab568f030cf86ee68a1df9e45a3ac9d421cb

---


# API를 사용하여 데이터 사용 레이블 관리

이 문서에서는 Catalog Service API를 사용하여 데이터 세트 및 필드 수준에서 데이터 사용 레이블을 관리하는 방법에 대해 설명합니다.

## 시작하기

이 안내서를 읽기 전에 카탈로그 서비스 개요를 [](../../catalog/home.md) 참조하여 서비스에 대한 보다 강력한 소개를 확인하시기 바랍니다. 또한 카탈로그 개발자 안내서의 [시작 섹션에](../../catalog/api/getting-started.md) 설명된 단계에 따라 카탈로그 API를 호출하는 데 필요한 자격 증명을 수집해야 합니다.

아래 섹션에 설명된 끝점에 대한 호출을 하려면 특정 데이터 세트에 대한 고유한 `id` 값이 있어야 합니다. 이 값이 없는 경우, 기존 데이터 집합의 ID를 찾으려면 카탈로그 개체 [](../../catalog/api/list-objects.md) 목록에 대한 개발자 가이드 섹션을 참조하십시오.

## 데이터 세트에 대한 레이블 찾기 {#lookup}

GET 요청을 수행하여 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /dataSets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 조회하려는 데이터 집합의 고유한 `id` 값. |

**요청**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
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
| `optionalLabels` | 데이터 사용 레이블이 적용된 데이터 집합 내의 개별 필드 목록입니다. |

## 데이터 세트에 레이블 적용

POST 또는 PUT 요청의 페이로드에 제공하여 데이터 세트에 대한 레이블 세트를 만들 수 있습니다. 이러한 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에서 제공되는 레이블로 바꿉니다.

**API 형식**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만들 데이터 집합의 고유 `id` 값입니다. |

**요청**

다음 POST 요청은 데이터 세트에 일련의 레이블뿐만 아니라 해당 데이터 세트 내의 특정 필드를 추가합니다. 페이로드에 제공된 필드는 PUT 요청에 필요한 필드와 동일합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다. <br/><br/>`option`:필드의 XDM(경험 데이터 모델) 특성이 포함된 개체입니다. 다음 세 가지 속성이 필요합니다.<ul><li>id</code>:필드와 연결된 스키마의 URI $id</code> 값입니다.</li><li>contentType</code>:스키마의 컨텐츠 유형 및 버전 번호입니다. 이렇게 하려면 XDM 조회 요청에 대해 유효한 <a href="../../xdm/api/look-up-resource.md">승인 헤더</a> 중 하나를 사용해야 합니다.</li><li>schemaPath</code>:데이터 집합 스키마 내의 필드 경로입니다.</li></ul>`labels`:필드에 추가할 데이터 사용 레이블 목록입니다. |

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

## 데이터 세트에 대한 레이블 삭제

DELETE 요청을 수행하여 데이터 세트에 적용된 레이블을 삭제할 수 있습니다.

>[!NOTE] 이 작업은 상위 데이터 집합을 삭제하도록 준비하는 경우에만 사용해야 합니다.

**API 형식**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 삭제할 데이터 집합의 고유 `id` 값. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답 HTTP 상태 200(확인)은 레이블이 삭제되었음을 나타냅니다. 별도의 호출에서 데이터 세트에 대한 기존 레이블을 [](#lookup) 검색하여 확인할 수 있습니다.

## 다음 단계

이제 데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가했으므로 데이터를 Experience Platform으로 인제스트할 수 있습니다. 자세한 내용은 [데이터 수집 설명서를](../../ingestion/home.md)참조하십시오.

적용된 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요를](../policies/overview.md)참조하십시오.