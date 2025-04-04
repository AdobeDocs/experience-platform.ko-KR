---
keywords: Experience Platform;홈;인기 항목;광고 시스템;Advertising 시스템
solution: Experience Platform
title: 흐름 서비스 API를 사용하여 Advertising 시스템 살펴보기
description: 플로우 서비스는 Adobe Experience Platform 내의 다양한 개별 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결 가능한 사용자 인터페이스와 RESTful API를 제공합니다. 이 튜토리얼에서는 플로우 서비스 API를 사용하여 광고 시스템을 살펴봅니다.
exl-id: 3016ce1e-12e6-47ce-a4c5-52f8d440f515
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---

# [!DNL Flow Service] API를 사용하여 광고 시스템 살펴보기

이제 기본 연결이 만들어지면 고유한 기본 연결 ID를 사용하여 소스의 데이터 구조 및 콘텐츠를 탐색하고 탐색할 수 있습니다. 이렇게 하면 데이터 흐름을 만들어 Adobe Experience Platform으로 가져오기 전에 특정 항목과 해당 데이터 유형 및 형식을 식별할 수 있습니다.

이 자습서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 광고 시스템을 살펴봅니다.

## 시작하기

>[!IMPORTANT]
>
>이 자습서에서는 광고 소스에 대해 고유한 기본 연결 ID가 있어야 합니다. 이 ID가 없는 경우 [Experience Platform에 광고 소스 연결](../../api/create/advertising/ads.md) 자습서에 대한 자습서를 참조하십시오.

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [원본](../../../home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform]에서는 단일 [!DNL Experience Platform] 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 응용 프로그램을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 광고 시스템에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### Experience Platform API 사용

Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.

## 데이터 테이블 탐색

광고 시스템에 대한 기본 연결을 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. [!DNL Experience Platform]을(를) 검사하거나 수집할 테이블의 경로를 찾으려면 다음 호출을 사용하십시오.

**API 형식**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 광고 시스템에 대한 기본 연결의 ID입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 의 테이블을 광고 시스템에 배열한 것입니다. [!DNL Experience Platform]&#x200B;(으)로 가져올 테이블을 찾고 `path` 속성을 기록해 두십시오. 다음 단계에서 테이블 구조를 검사하기 위해 테이블을 제공해야 합니다.

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

## 테이블 구조 검사

광고 시스템에서 표의 구조를 검사하려면 표의 경로를 쿼리 매개 변수로 지정하면서 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 광고 시스템의 연결 ID입니다. |
| `{TABLE_PATH}` | 광고 시스템 내 표의 경로입니다. |

**요청**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 표의 구조를 반환합니다. 각 테이블의 열에 대한 세부 정보는 `columns` 배열의 요소 내에 있습니다.

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

이 자습서를 통해 광고 시스템을 탐색하고 [!DNL Experience Platform]에 가져올 테이블의 경로를 찾은 다음 해당 테이블의 구조에 대한 정보를 얻었습니다. 다음 자습서에서 이 정보를 사용하여 [광고 시스템에서 데이터를 수집하여 Experience Platform으로 가져오기](../collect/advertising.md)할 수 있습니다.
