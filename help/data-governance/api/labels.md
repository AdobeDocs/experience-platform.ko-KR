---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 레이블 API 끝점
topic-legacy: developer guide
description: 정책 서비스 API를 사용하여 Experience Platform에서 데이터 사용 레이블을 관리하는 방법을 알아봅니다.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 레이블 끝점

데이터 사용 레이블을 사용하면 해당 데이터에 적용될 수 있는 사용 정책에 따라 데이터를 분류할 수 있습니다. [!DNL Policy Service API]의 `/labels` 종단점을 사용하면 경험 애플리케이션 내의 데이터 사용량 레이블을 프로그래밍 방식으로 관리할 수 있습니다.

>[!NOTE]
>
>`/labels` 끝점은 데이터 사용 레이블을 검색, 만들기 및 업데이트하는 데만 사용됩니다. API 호출을 사용하여 데이터 세트 및 필드에 레이블을 추가하는 방법에 대한 단계는 [데이터 세트 레이블 관리](../labels/dataset-api.md)에 대한 안내서를 참조하십시오.

## 시작하기

이 안내서에 사용된 API 끝점은 [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)의 일부입니다. 계속하기 전에 [시작하기 안내서](getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 [!DNL Experience Platform] API를 성공적으로 호출하기 위해 필요한 필수 헤더에 대한 중요 정보를 검토하십시오.

## 레이블 목록 {#list} 검색

각각 `/labels/core` 또는 `/labels/custom`에 GET 요청을 하여 모든 `core` 또는 `custom` 레이블을 나열할 수 있습니다.

**API 형식**

```http
GET /labels/core
GET /labels/custom
```

**요청**

다음 요청은 조직에서 만든 모든 사용자 지정 레이블을 나열합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 시스템에서 검색된 사용자 지정 레이블 목록을 반환합니다. 위의 예제 요청이 `/labels/custom`에 수행되었으므로 아래 응답에는 사용자 지정 레이블만 표시됩니다.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## 레이블 {#look-up} 검색

[!DNL Policy Service] API에 대한 GET 요청 경로에 해당 레이블의 `name` 속성을 포함하여 특정 레이블을 조회할 수 있습니다.

**API 형식**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 조회할 사용자 지정 레이블의 `name` 속성. |

**요청**

다음 요청은 경로에 지정된 사용자 지정 레이블 `L2`을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용자 지정 레이블의 세부 정보를 반환합니다.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## 사용자 지정 레이블 {#create-update} 만들기 또는 업데이트

사용자 지정 레이블을 만들거나 업데이트하려면 [!DNL Policy Service] API에 PUT 요청을 해야 합니다.

**API 형식**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 사용자 지정 레이블의 `name` 속성입니다. 이 이름의 사용자 지정 레이블이 없으면 새 레이블이 만들어집니다. 레이블이 있으면 해당 레이블이 업데이트됩니다. |

**요청**

다음 요청은 고객의 선택된 결제 계획과 관련된 정보가 포함된 데이터를 설명하는 새 레이블인 `L3`을 만듭니다.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 레이블에 대한 고유한 문자열 식별자입니다. 이 값은 조회 목적으로 사용되며 데이터 세트 및 필드에 레이블을 적용할 때 짧고 간결한 것이 좋습니다. |
| `category` | 레이블의 카테고리. 사용자 지정 레이블에 대한 고유한 카테고리를 만들 수 있지만 UI에 레이블을 표시하려면 `Custom`을 사용하는 것이 좋습니다. |
| `friendlyName` | 표시 목적으로 사용되는 레이블의 친숙한 이름입니다. |
| `description` | (선택 사항) 추가 컨텍스트를 제공하는 레이블의 설명입니다. |

**응답**

성공적인 응답은 기존 레이블이 업데이트된 경우 HTTP 코드 200(OK)을 사용하는 사용자 지정 레이블의 세부 사항을 반환하고 새 레이블을 만든 경우에는 201(만들기)을 반환합니다.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## 다음 단계

이 안내서에서는 정책 서비스 API에서 `/labels` 끝점의 사용에 대해 다룹니다. 데이터 집합 및 필드에 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 집합 레이블 API 안내서](../labels/dataset-api.md)를 참조하십시오.
