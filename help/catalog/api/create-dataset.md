---
keywords: Experience Platform;홈;인기 항목;데이터 세트;데이터 세트 만들기;데이터 세트 만들기;데이터 세트 활성화
solution: Experience Platform
title: API에서 데이터 세트 만들기
description: 이 문서에서는 카탈로그 서비스 API에서 데이터 세트 개체를 만드는 방법을 다룹니다.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 1%

---

# API에서 데이터 세트 만들기

[!DNL Catalog] API를 사용하여 데이터 세트를 만들려면 데이터 세트가 기반으로 사용될 [!DNL Experience Data Model](XDM) 스키마의 `$id` 값을 알고 있어야 합니다. 스키마 ID가 있으면 [!DNL Catalog] API의 `/datasets` 끝점에 POST 요청을 하여 데이터 집합을 만들 수 있습니다.

>[!NOTE]
>
>이 문서에서는 [!DNL Catalog]에서 데이터 집합 개체를 만드는 방법만 다룹니다. 데이터 집합을 만들고, 채우고, 모니터링하는 방법에 대한 전체 단계는 다음 [자습서](../datasets/create.md)를 참조하십시오.

**API 형식**

```HTTP
POST /dataSets
```

**요청**

다음 요청은 이전에 정의한 스키마를 참조하는 데이터 세트를 만듭니다.

```SHELL
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?requestDataSource=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name":"LoyaltyMembersDataset",
    "schemaRef": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/719c4e19184402c27595e65b931a142b",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 생성할 데이터 세트의 이름입니다. |
| `schemaRef.id` | 데이터 집합이 기반으로 할 XDM 스키마에 대한 URI `$id` 값입니다. |
| `schemaRef.contentType` | 스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오. |

>[!NOTE]
>
>이 예제에서는 `containerFormat` 속성에 대해 [Apache Parquet](https://parquet.apache.org/docs/) 파일 형식을 사용합니다. JSON 파일 형식을 사용하는 예는 [일괄 처리 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md)에서 확인할 수 있습니다.

**응답**

성공한 응답은 HTTP 상태 201(생성됨)과 `"@/datasets/{DATASET_ID}"` 형식의 새로 만든 데이터 집합 ID가 포함된 배열로 구성된 응답 개체를 반환합니다. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
