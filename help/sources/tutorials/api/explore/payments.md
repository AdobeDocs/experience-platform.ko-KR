---
keywords: Experience Platform;홈;인기 항목;결제
solution: Experience Platform
title: Flow Service API를 사용한 결제 시스템 탐색
topic-legacy: overview
description: 이 자습서에서는 Flow Service API를 사용하여 결제 애플리케이션을 탐색합니다.
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 2%

---

# 을 사용하여 결제 시스템 탐색 [!DNL Flow Service] API

[!DNL Flow Service] Adobe Experience Platform 내의 다양한 소스에서 고객 데이터를 수집하고 중앙 집중화하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스를 연결할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.

이 자습서에서는 [!DNL Flow Service] 결제 애플리케이션을 탐색하기 위한 API

## 시작하기

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [샌드박스](../../../../sandboxes/home.md): [!DNL Experience Platform] 단일 파티션을 생성하는 가상 샌드박스 제공 [!DNL Platform] 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 별도의 가상 환경으로 인스턴스를 구축할 수 있습니다.

다음 섹션에서는 를 사용하여 지급 애플리케이션에 성공적으로 접속하기 위해 알아야 할 추가 정보를 제공합니다. [!DNL Flow Service] API.

### 필요한 자격 증명 수집

이 자습서에서는 데이터를 수집하려는 타사 결제 애플리케이션과 유효한 연결이 필요합니다. 유효한 연결에는 애플리케이션의 연결 사양 ID 및 연결 ID가 포함됩니다. 결제 연결 생성 및 이러한 값 검색에 대한 자세한 내용은 [결제 소스를 플랫폼에 연결](../../api/create/payments/paypal.md) 자습서입니다.

### 샘플 API 호출 읽기

이 자습서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환되는 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 에서 [!DNL Experience Platform] 문제 해결 가이드.

### 필수 헤더에 대한 값을 수집합니다

을 호출하려면 [!DNL Platform] API를 먼저 완료해야 합니다. [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 모든 히트에 필요한 각 헤더에 대한 값이 제공됩니다 [!DNL Experience Platform] 아래에 표시된 대로 API 호출:

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

의 모든 리소스 [!DNL Experience Platform]에 속했던 것 포함 [!DNL Flow Service]은 특정 가상 샌드박스로 구분됩니다. 에 대한 모든 요청 [!DNL Platform] API에는 작업이 발생할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* x-sandbox-name: `{SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 데이터 테이블 탐색

결제 시스템에 대한 연결 ID를 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 검사하거나 수집할 테이블의 경로를 찾습니다 [!DNL Platform].

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 지급 기준 연결의 ID입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 결제 시스템에서 일련의 테이블을 반환합니다. 가져올 테이블을 찾으십시오 [!DNL Platform] 그리고 그것을 주목하세요 `path` 속성을 확인하기 위해 다음 단계에서 제공해야 하므로 속성을 검사합니다.

```json
[
    {
        "type": "table",
        "name": "PayPal.Billing_Plans",
        "path": "PayPal.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Billing_Plans_Payment_Definition",
        "path": "PayPal.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "PayPal.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "PayPal.Catalog_Products",
        "path": "PayPal.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect 테이블 구조

결제 시스템에서 테이블의 구조를 검사하려면 테이블의 경로를 질의 매개변수로 지정하는 동안 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 결제 시스템의 연결 ID입니다. |
| `{TABLE_PATH}` | 결제 시스템 내의 테이블 경로. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 테이블의 구조를 반환합니다. 각 테이블의 열에 대한 세부 사항은 `columns` 배열입니다.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 다음 단계

이 자습서를 따라 결제 시스템을 살펴보고 수집할 테이블의 경로를 찾았습니다 [!DNL Platform], 및에서 해당 구조에 대한 정보를 얻습니다. 이 정보는 다음 자습서에서 사용할 수 있습니다 [결제 시스템에서 데이터를 수집하여 플랫폼으로 가져오기](../collect/payments.md).
