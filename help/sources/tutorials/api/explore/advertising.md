---
keywords: Experience Platform;홈;인기 주제;광고 시스템;광고 시스템
solution: Experience Platform
title: Flow Service API를 사용하여 광고 시스템 탐색
topic-legacy: overview
description: Flow Service는 Adobe Experience Platform 내의 다양한 종류의 소스로부터 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다. 이 자습서에서는 Flow Service API를 사용하여 광고 시스템을 탐색합니다.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: 8aa8dfcc4f8a36d0898a9cc079bd98b89e3589a1
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 광고 시스템 살펴보기

생성된 기본 연결을 통해 고유한 기본 연결 ID를 사용하여 소스의 데이터 구조 및 콘텐츠를 탐색하고 탐색할 수 있습니다. 이를 통해 데이터 흐름을 만들어 Adobe Experience Platform으로 가져오기 전에 특정 항목, 각각의 데이터 유형 및 형식을 식별할 수 있습니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)를 사용합니다. 광고 시스템을 살펴보십시오.

## 시작

>[!IMPORTANT]

이 자습서를 사용하려면 광고 소스에 대한 고유한 기본 연결 ID가 있어야 합니다. 이 ID가 없는 경우 광고 소스를 Platform](../../api/create/advertising/ads.md)에 연결 자습서에서 자습서를 참조하십시오.[

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 에서는 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이  [!DNL Platform] 되는 단일 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 광고 시스템에 성공적으로 연결하기 위해 알고 있어야 하는 추가 정보를 제공합니다.

### 플랫폼 API 사용

플랫폼 API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../../landing/api-guide.md)의 안내서를 참조하십시오.

## 데이터 테이블 탐색

광고 시스템에 대한 기본 연결을 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 검사하거나 [!DNL Platform]에 수집할 테이블의 경로를 찾습니다.

**API 형식**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 광고 시스템에 대한 기본 연결의 ID입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 광고 시스템에서 로의 테이블 배열입니다. [!DNL Platform]에 가져올 테이블을 찾고 `path` 속성을 기록해 두십시오. 이 표를 다음 단계에서 제공하여 구조를 검사해야 합니다.

```json
[
    {
        "type": "table",
        "name": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "path": "v201809.ACCOUNT_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "path": "v201809.ADGROUP_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "path": "v201809.AD_CUSTOMIZERS_FEED_ITEM_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "v201809.AD_PERFORMANCE_REPORT",
        "path": "v201809.AD_PERFORMANCE_REPORT",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect 테이블 구조

광고 시스템에서 테이블의 구조를 검사하려면 테이블의 경로를 쿼리 매개 변수로 지정하는 동안 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 광고 시스템의 연결 ID입니다. |
| `{TABLE_PATH}` | 광고 시스템 내의 표 경로입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 테이블 구조를 반환합니다. 각 테이블의 열에 대한 세부 사항은 `columns` 배열의 요소 내에 있습니다.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "CallOnlyPhoneNumber",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "AdGroupId",
                "type": "long",
                "xdm": {
                    "type": "integer",
                    "minimum": -9007199254740992,
                    "maximum": 9007199254740991
                }
            },
            {
                "name": "AdGroupName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Date",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
        ]
    }
}
```

## 다음 단계

이 자습서에 따라 광고 시스템을 살펴보고 [!DNL Platform]에 가져올 테이블의 경로를 찾은 후 해당 구조에 대한 정보를 얻습니다. 이 정보는 다음 자습서에서 [광고 시스템에서 데이터를 수집하고 Platform](../collect/advertising.md)로 가져올 수 있습니다.
