---
keywords: Experience Platform;홈;인기 항목;e커머스;e커머스;home;popular topics;eCommerce;
solution: Experience Platform
title: Flow Service API를 사용하여 e커머스 연결 탐색
topic-legacy: overview
description: 이 자습서는 Flow Service API를 사용하여 eCommerce 연결을 탐색합니다.
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# [!DNL Flow Service] API를 사용하여 전자 상거래 연결 살펴보기

[!DNL Flow Service] 는 Adobe Experience Platform 내의 다양한 소스에서 수집한 고객 데이터를 수집하고 중앙에서 관리하는 데 사용됩니다. 이 서비스는 지원되는 모든 소스가 연결되어 있는 사용자 인터페이스와 RESTful API를 제공합니다.

이 자습서는 [!DNL Flow Service] API를 사용하여 제3자 **[!UICONTROL eCommerce]** 연결을 탐색합니다.

## 시작하기

이 가이드를 사용하려면 다음과 같은 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수  [!DNL Platform] 있습니다.
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 디지털 경험 애플리케이션을 개발 및 발전시키는 데 도움이 되도록 단일  [!DNL Platform] 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

다음 섹션에서는 [!DNL Flow Service] API를 사용하여 **[!UICONTROL eCommerce]** 연결에 성공적으로 연결하려면 알아야 할 추가 정보를 제공합니다.

### 연결 ID 얻기

[!DNL Platform] API를 사용하여 **[!UICONTROL eCommerce]** 연결을 탐색하려면 유효한 연결 ID가 있어야 합니다. 작업할 **[!UICONTROL eCommerce]** 연결에 대한 연결이 아직 없는 경우 다음 자습서를 통해 연결을 만들 수 있습니다.

* [Shopify](../create/ecommerce/shopify.md)

### 샘플 API 호출 읽기

이 자습서에서는 요청의 서식을 지정하는 방법을 보여주는 API 호출 예를 제공합니다. 여기에는 경로, 필수 헤더 및 올바른 형식의 요청 페이로드가 포함됩니다. API 응답으로 반환된 샘플 JSON도 제공됩니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [!DNL Experience Platform] 문제 해결 안내서의 [API 호출 예](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)를 읽는 방법에 대한 섹션을 참조하십시오.

### 필수 헤더에 대한 값 수집

[!DNL Platform] API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 [!DNL Experience Platform] API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Flow Service]에 속하는 리소스를 포함하여 [!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 구분됩니다. [!DNL Platform] API에 대한 모든 요청에는 작업이 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

* `x-sandbox-name: {SANDBOX_NAME}`

페이로드(POST, PUT, PATCH)을 포함하는 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* `Content-Type: application/json`

## 데이터 테이블 살펴보기

**[!UICONTROL eCommerce]** 연결 ID를 사용하여 GET 요청을 수행하여 데이터 테이블을 탐색할 수 있습니다. 다음 호출을 사용하여 [!DNL Platform]에 검사 또는 인제스트할 테이블의 경로를 찾습니다.

**API 형식**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 매개 변수 | 설명 |
| --- | --- |
| `{CONNECTION_ID}` | **[!UICONTROL eCommerce]** 연결 ID. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 **[!UICONTROL eCommerce]** 연결에서 표 배열을 반환합니다. [!DNL Platform]에 가져올 테이블을 찾고 해당 `path` 속성을 적어 구조를 검사하기 위해 다음 단계에서 제공해야 합니다.

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect 표 구조

**[!UICONTROL eCommerce]** 연결에서 테이블 구조를 검사하려면 `object` 쿼리 매개 변수 내에서 테이블의 경로를 지정하는 동안 GET 요청을 수행합니다.

**API 형식**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{CONNECTION_ID}` | **[!UICONTROL eCommerce]** 연결의 연결 ID입니다. |
| `{TABLE_PATH}` | **[!UICONTROL eCommerce]** 연결 내의 표 경로입니다. |

**요청**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 지정된 테이블의 구조를 반환합니다. 표의 각 열에 대한 세부 사항은 `columns` 배열의 요소 내에 있습니다.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## 다음 단계

이 튜토리얼을 따라 **[!UICONTROL eCommerce]** 연결을 살펴보고, [!DNL Platform]에 인제스트할 테이블의 경로를 찾았으며, 해당 구조에 대한 정보를 얻었습니다. 다음 자습서에서는 이 정보를 사용하여 [eCommerce 데이터를 수집하고 플랫폼](../collect/ecommerce.md)에 가져올 수 있습니다.
