---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Flow Service API를 사용하여 광고 시스템 살펴보기
topic: overview
translation-type: tm+mt
source-git-commit: b9c5afe62ea91e5b7f8ad6c3c6eb1bf834cf7ec8

---


# Flow Service API를 사용하여 광고 시스템 살펴보기

Flow Service는 Adobe Experience Platform에서 다양한 소스의 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서에서는 Flow Service API를 사용하여 광고 시스템을 탐색합니다.

## 시작하기

이 가이드는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../home.md):Adobe Experience Platform을 사용하면 다양한 소스에서 데이터를 인제스트할 수 있을 뿐만 아니라 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다.
* [샌드박스](../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 Flow Service API를 사용하여 광고 시스템에 성공적으로 연결하기 위해 알아야 할 추가 정보를 제공합니다.

### 필요한 자격 증명 수집

이 자습서에서는 데이터를 인제스트할 타사 광고 애플리케이션과 원활하게 연결되어 있어야 합니다. 유효한 연결에는 응용 프로그램의 연결 사양 ID 및 연결 ID가 포함됩니다. 광고 연결 만들기 및 이러한 값 검색에 대한 자세한 내용은 광고 소스를 플랫폼에 [연결 자습서를](../../api/create/advertising/ads.md) 참조하십시오.

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답에서 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform 문제 해결 안내서에서 API 호출 [예를 읽는](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

플랫폼 API를 호출하려면 먼저 [인증 자습서를](../../../../tutorials/authentication.md)완료해야 합니다. 인증 튜토리얼을 완료하면 다음과 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값이 제공됩니다.

* 인증:베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Flow Service에 속한 리소스를 비롯하여 Experience Platform의 모든 리소스는 특정 가상 샌드박스로 분리됩니다. 플랫폼 API에 대한 모든 요청에는 작업이 수행될 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* 컨텐츠 유형: `application/json`

## 데이터 테이블 살펴보기

광고 시스템에 대한 기본 연결을 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 Platform에서 검사하거나 인제스트할 테이블의 경로를 찾습니다.

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
    'http://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 광고 시스템에 대한 일련의 표입니다. Platform(플랫폼)으로 가져올 표를 찾아 다음 단계에서 제공해야 하므로 해당 `path` 속성을 기록해 두십시오.

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

광고 시스템에서 테이블 구조를 검사하려면 테이블의 경로를 쿼리 매개 변수로 지정하는 동안 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 광고 시스템의 연결 ID. |
| `{TABLE_PATH}` | 광고 시스템 내의 표 경로입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2484f2df-c057-4ab5-84f2-dfc0577ab592/explore?objectType=table&object=v201809.AD_PERFORMANCE_REPORT' \
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

이 튜토리얼을 따라 광고 시스템을 살펴보고 플랫폼으로 가져올 테이블의 경로를 확인했으며 해당 구조에 대한 정보를 얻으셨습니다. 다음 튜토리얼에서 이 정보를 사용하여 광고 시스템에서 데이터를 [수집하고 플랫폼으로 가져올 수 있습니다](../collect/advertising.md).
