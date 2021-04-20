---
keywords: Experience Platform;홈;인기 항목;데이터 집합;데이터 집합;데이터 집합 만들기;데이터 집합 만들기;데이터 집합 사용
solution: Experience Platform
title: API에서 데이터 세트 만들기
topic: developer guide
description: 이 문서에서는 카탈로그 서비스 API에서 데이터 세트 개체를 만드는 방법을 설명합니다.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
translation-type: tm+mt
source-git-commit: 727c9dbd87bacfd0094ca29157a2d0283c530969
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 1%

---

# API에서 데이터 세트 만들기

[!DNL Catalog] API를 사용하여 데이터 집합을 만들려면 데이터 집합의 기반이 되는 [!DNL Experience Data Model](XDM) 스키마의 `$id` 값을 알고 있어야 합니다. 스키마 ID가 있으면 [!DNL Catalog] API의 `/datasets` 끝점에 POST 요청을 하여 데이터 세트를 만들 수 있습니다.

>[!NOTE]
>
>이 문서에서는 [!DNL Catalog]에서 데이터 집합 개체를 만드는 방법에만 다룹니다. 데이터 세트를 생성, 채우기 및 모니터링하는 방법에 대한 전체 단계는 다음 [자습서](../datasets/create.md)를 참조하십시오.

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
    }
}'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 만들 데이터 세트의 이름입니다. |
| `schemaRef.id` | 데이터 세트에 기반이 되는 XDM 스키마의 URI `$id` 값입니다. |
| `schemaRef.contentType` | 스키마의 형식 및 버전을 나타냅니다. 자세한 내용은 XDM API 안내서의 [스키마 버전 관리](../../xdm/api/getting-started.md#versioning)에 대한 섹션을 참조하십시오. |

>[!NOTE]
>
>이 예제에서는 `containerFormat` 속성에 대해 [Apache Parided](https://parquet.apache.org/documentation/latest/) 파일 형식을 사용합니다. JSON 파일 형식을 사용하는 예제는 [일괄 처리 통합 개발자 가이드](../../ingestion/batch-ingestion/api-overview.md)에서 찾을 수 있습니다.

**응답**

성공적인 응답은 HTTP 상태 201(만들어짐)과 새로 만든 데이터 세트의 ID를 `"@/datasets/{DATASET_ID}"` 형식으로 포함하는 배열로 구성된 응답 개체를 반환합니다. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
