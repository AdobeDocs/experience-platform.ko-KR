---
keywords: Experience Platform;홈;인기 항목;데이터 세트;데이터 세트 만들기;데이터 세트 만들기;데이터 세트 활성화
solution: Experience Platform
title: API에서 데이터 세트 만들기
description: 이 문서에서는 카탈로그 서비스 API에서 데이터 세트 개체를 만드는 방법을 다룹니다.
exl-id: f3e5de7f-1781-4898-ac42-063eb51e661a
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# API에서 데이터 세트 만들기

을 사용하여 데이터 세트를 만들려면 [!DNL Catalog] API, 다음을 알고 있어야 합니다. `$id` 값 [!DNL Experience Data Model] 데이터 세트가 기반으로 삼을 XDM (XDM) 스키마. 스키마 ID가 있으면에서 POST 요청을 하여 데이터 세트를 생성할 수 있습니다. `/datasets` 의 엔드포인트 [!DNL Catalog] API.

>[!NOTE]
>
>이 문서는에서 데이터 세트 개체를 만드는 방법만 다룹니다. [!DNL Catalog]. 데이터 세트를 만들고 채우고 모니터링하는 방법에 대한 전체 단계는 다음을 참조하십시오 [튜토리얼](../datasets/create.md).

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
| `schemaRef.id` | URI `$id` 데이터 세트가 기반으로 삼을 XDM 스키마 값. |
| `schemaRef.contentType` | 스키마의 형식 및 버전을 나타냅니다. 의 섹션을 참조하십시오. [스키마 버전 관리](../../xdm/api/getting-started.md#versioning) 자세한 내용은 XDM API 안내서 를 참조하십시오. |

>[!NOTE]
>
>이 예에서는 [Apache Parquet](https://parquet.apache.org/docs/) 파일 형식 `containerFormat` 속성. JSON 파일 형식을 사용하는 예제는 [일괄 처리 수집 개발자 안내서](../../ingestion/batch-ingestion/api-overview.md).

**응답**

성공적인 응답은 HTTP 상태 201(생성됨)과, 형식으로 새로 생성된 데이터 세트의 ID가 포함된 배열로 구성된 응답 개체를 반환합니다 `"@/datasets/{DATASET_ID}"`. 데이터 세트 ID는 API 호출에서 데이터 세트를 참조하는 데 사용되는 읽기 전용 시스템 생성 문자열입니다.

```JSON
[
    "@/dataSets/5c8c3c555033b814b69f947f"
]
```
