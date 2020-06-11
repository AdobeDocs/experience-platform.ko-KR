---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'API를 사용하여 데이터 사용 레이블 관리 '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 3%

---


# API를 사용하여 데이터 사용 레이블 관리

데이터 집합 서비스 API를 사용하면 데이터 집합에 대한 사용 레이블을 프로그래밍 방식으로 관리할 수 있습니다. Adobe Experience Platform의 데이터 카탈로그 기능의 일부이지만 데이터 세트 메타데이터를 관리하는 카탈로그 서비스 API와는 별개입니다.

이 문서에서는 데이터 세트 서비스 API를 사용하여 데이터 세트 및 필드 수준에서 데이터 사용 레이블을 관리하는 방법에 대해 설명합니다.

## 시작하기

이 안내서를 읽기 전에 카탈로그 개발자 안내서의 [시작 섹션에](../../catalog/api/getting-started.md) 설명된 단계에 따라 API를 호출하는 데 필요한 자격 증명을 [!DNL Platform] 수집합니다.

아래 섹션에 나와 있는 끝점에 대한 호출을 하려면 특정 데이터 세트에 대한 고유한 `id` 값이 있어야 합니다. 이 값이 없는 경우 카탈로그 개체 [를 나열하는](../../catalog/api/list-objects.md) 가이드에서 기존 데이터 집합의 ID를 찾습니다.

## 데이터 세트에 대한 레이블 검색 {#lookup}

GET 요청을 수행하여 기존 데이터 세트에 적용된 데이터 사용 레이블을 조회할 수 있습니다.

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

## 데이터 세트에 레이블 적용

POST 또는 PUT 요청의 페이로드에 제공하여 데이터 세트에 대한 레이블 세트를 만들 수 있습니다. 이러한 방법 중 하나를 사용하면 기존 레이블을 덮어쓰고 페이로드에서 제공되는 레이블로 바꿉니다.

**API 형식**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 만드는 데이터 세트의 고유한 `id` 값입니다. |

**요청**

다음 POST 요청에서는 데이터 세트 내의 특정 필드뿐만 아니라 데이터 세트에 일련의 레이블을 추가합니다. 페이로드에서 제공되는 필드는 PUT 요청에 필요한 필드와 동일합니다.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
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
| `optionalLabels` | 레이블을 추가할 데이터 세트 내의 개별 필드 목록입니다. 이 배열의 각 항목에는 다음 속성이 있어야 합니다. <br/><br/>`option`: 필드의 XDM(경험 데이터 모델) 특성을 포함하는 객체입니다. 다음 세 가지 속성이 필요합니다.<ul><li>id</code>: 필드와 연결된 스키마의 URI $id</code> 값입니다.</li><li>contentType</code>: 스키마의 컨텐츠 유형 및 버전 번호입니다. XDM 조회 요청에 대해 유효한 <a href="../../xdm/api/look-up-resource.md">수락 헤더</a> 중 하나의 형태를 가져야 합니다.</li><li>schemaPath</code>: 데이터 집합 스키마 내의 필드 경로입니다.</li></ul>`labels`: 필드에 추가할 데이터 사용 레이블 목록입니다. |

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

**API 형식**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 매개 변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 레이블을 삭제할 데이터 세트의 고유한 `id` 값. |

**요청**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

레이블이 삭제되었음을 나타내는 성공적인 응답 HTTP 상태 200(확인)입니다. 데이터 세트에 대한 기존 레이블 [을](#lookup) 별도의 호출로 검색하여 확인할 수 있습니다.

## 다음 단계

이제 데이터 세트 및 필드 수준에서 데이터 사용 레이블을 추가했으므로 경험 플랫폼에 데이터를 인제스트할 수 있습니다. 자세한 내용은 [데이터 수집 설명서를 참조하십시오](../../ingestion/home.md).

적용된 레이블을 기반으로 데이터 사용 정책을 정의할 수도 있습니다. 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](../policies/overview.md).

데이터 집합 관리에 대한 자세한 내용 [!DNL Experience Platform]은 [데이터 집합 개요를 참조하십시오](../../catalog/datasets/overview.md).