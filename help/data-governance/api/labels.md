---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 레이블 끝점
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 3%

---


# 레이블 끝점

데이터 사용 레이블을 사용하면 해당 데이터에 적용될 수 있는 사용 정책에 따라 데이터를 분류할 수 있습니다. Adobe Experience Application `/labels` 의 종단점을 통해 [!DNL Policy Service API] 사용자 경험 애플리케이션 내에서 데이터 사용 레이블을 프로그래밍 방식으로 관리할 수 있습니다.

>[!NOTE]
>
>끝점은 `/labels` 데이터 사용 레이블을 검색, 만들기 및 업데이트하는 데만 사용됩니다. API 호출을 사용하여 데이터 세트와 필드에 레이블을 추가하는 방법에 대한 단계는 데이터 세트 레이블 [관리에 대한 안내서를 참조하십시오](../labels/dataset-api.md).

## 시작하기

이 안내서에서 사용되는 API 끝점은 이 끝점의 일부입니다 [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). 계속하기 전에 [시작하기 가이드](getting-started.md) 에서 관련 문서 링크, 이 문서에서 샘플 API 호출 읽기 안내서, 모든 API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 검토하십시오 [!DNL Experience Platform] .

## 레이블 목록 검색 {#list}

GET을 각각 또는 `core` 로 요청하여 모든 또는 `custom` 레이블을 나열할 수 `/labels/core` `/labels/custom`있습니다.

**API 형식**

```http
GET /labels/core
GET /labels/custom
```

**요청**

다음 요청에는 조직에서 만든 모든 사용자 지정 레이블이 나열됩니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 시스템에서 검색된 사용자 지정 레이블 목록을 반환합니다. 위의 예제 요청이 작성되었으므로 아래 응답에는 사용자 지정 레이블 `/labels/custom`만 표시됩니다.

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

## 레이블 찾기 {#look-up}

API에 대한 GET 요청 경로에 해당 레이블의 `name` 속성을 포함하여 특정 레이블을 조회할 수 [!DNL Policy Service] 있습니다.

**API 형식**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 조회할 사용자 지정 레이블의 `name` 속성입니다. |

**요청**

다음 요청은 경로에 표시된 대로 사용자 지정 레이블 `L2`을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 사용자 지정 레이블의 세부 사항을 반환합니다.

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

## 사용자 지정 레이블 만들기 또는 업데이트 {#create-update}

사용자 지정 레이블을 만들거나 업데이트하려면 [!DNL Policy Service] API에 PUT 요청을 해야 합니다.

**API 형식**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{LABEL_NAME}` | 사용자 지정 레이블의 `name` 속성입니다. 이 이름의 사용자 지정 레이블이 없으면 새 레이블이 만들어집니다. 존재하는 경우 해당 레이블이 업데이트됩니다. |

**요청**

다음 요청은 고객의 선택한 지불 계획과 관련된 정보가 포함된 데이터를 설명하는 새로운 레이블 `L3`을 만듭니다.

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
| `name` | 레이블에 대한 고유한 문자열 식별자입니다. 이 값은 조회 목적으로 사용되며 데이터 세트와 필드에 레이블을 적용하므로 짧고 간결한 것이 좋습니다. |
| `category` | 레이블의 카테고리. 사용자 지정 레이블에 대한 고유한 카테고리를 만들 수 있지만 UI에 레이블을 표시하려면 사용하는 것이 `Custom` 좋습니다. |
| `friendlyName` | 표시 용도로 사용되는 레이블의 친숙한 이름입니다. |
| `description` | (선택 사항) 추가 컨텍스트를 제공하는 레이블의 설명입니다. |

**응답**

성공적인 응답은 기존 레이블이 업데이트된 경우 HTTP 코드 200(OK)을 사용하여 사용자 지정 레이블의 세부 사항을 반환하고 새 레이블을 만든 경우에는 201(만들기)을 반환합니다.

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

이 안내서에서는 Policy Service API의 `/labels` 끝점 사용에 대해 설명했습니다. 데이터 집합 및 필드에 레이블을 적용하는 방법에 대한 자세한 내용은 [데이터 집합 레이블 API 안내서를 참조하십시오](../labels/dataset-api.md).