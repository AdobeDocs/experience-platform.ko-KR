---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 세트 만들기
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---


# 데이터 세트 만들기

API를 사용하여 데이터 세트를 만들려면 데이터 [!DNL Catalog] 를 기반으로 하는 XDM(스키마) `$id` [!DNL Experience Data Model] 값을 알고 있어야 합니다. 스키마 ID가 있는 경우 API의 종단점에 POST을 요청하여 데이터 세트 `/datasets` 를 만들 수 [!DNL Catalog] 있습니다.

>[!NOTE]
>
>이 문서에서는 데이터 세트 개체를 만드는 방법만 다룹니다 [!DNL Catalog]. 데이터 세트를 생성, 채우기 및 모니터링하는 방법에 대한 자세한 내용은 다음 [자습서를 참조하십시오](../datasets/create.md).

**API 형식**

```HTTP
POST /dataSets
```

**요청**

다음 요청은 이전에 정의된 스키마를 참조하는 데이터 세트를 만듭니다.

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

| 속성 | 설명 |
| --- | --- |
| `name` | 만들 데이터 집합의 이름입니다. |
| `schemaRef.id` | 데이터 세트에 기준이 되는 XDM 스키마의 URI `$id` 값입니다. |

>[!NOTE]
>
>이 예에서는 속성에 [쪽모이](https://parquet.apache.org/documentation/latest/) 세공 파일 형식을 `containerFormat` 사용합니다. JSON 파일 형식을 사용하는 예는 [일괄 처리 통합 개발자 안내서에서 확인할 수 있습니다](../../ingestion/batch-ingestion/api-overview.md).

**응답**

성공적인 응답은 HTTP Status 201(Created)과 새로 만든 데이터 집합의 ID가 포함된 배열로 구성된 응답 개체를 반환합니다 `"@/datasets/{DATASET_ID}"`. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
