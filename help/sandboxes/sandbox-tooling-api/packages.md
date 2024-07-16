---
title: 샌드박스 도구 패키지 API 끝점
description: 샌드박스 도구 API의 /packages 끝점을 사용하면 Adobe Experience Platform에서 패키지를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 8ff9c50b4999a49413f8c45274815225ba58361c
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 6%

---

# 패키지 끝점

샌드박스 도구 를 사용하면 객체라고도 하는 다양한 객체를 선택하여 패키지로 내보낼 수 있습니다. 패키지는 단일 아티팩트 또는 여러 아티팩트(예: 데이터 세트 또는 스키마)로 구성될 수 있습니다. 패키지에 포함된 모든 아티팩트는 동일한 샌드박스의 아티팩트여야 합니다.

샌드박스 도구 API의 `/packages` 끝점을 사용하면 패키지 게시 및 샌드박스로 패키지 가져오기를 포함하여 조직의 패키지를 프로그래밍 방식으로 관리할 수 있습니다.

## 패키지 만들기 {#create}

패키지 이름 및 패키지 유형에 대한 값을 제공하는 동안 `/packages` 끝점에 POST 요청을 하여 다중 아티팩트 패키지를 만들 수 있습니다.

**API 형식**

```http
POST /packages/
```

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "name": "acme",
      "description": "Acme Business Group",
      "packageType": "PARTIAL",    
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      },
      "expiry": "2023-05-20T20:05:10Z",
      "artifacts": [
        {
          "id": "27115daa-c92b-4f17-a077-d65ffeb0c525",
          "type": "PROFILE_SEGMENT",
          "title": "Acme Profile Segment"
        }      
      ]
  }'
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `name` | 패키지의 이름입니다. | 문자열 | 예 |
| `description` | 패키지에 대한 자세한 내용을 제공하는 설명입니다. | 문자열 | 아니요 |
| `packageType` | 패키지에 특정 아티팩트를 포함하고 있음을 나타내는 패키지 형식은 **PARTIAL**&#x200B;입니다. | 문자열 | 예 |
| `sourceSandbox` | 패키지의 소스 샌드박스. | 문자열 | 아니요 |
| `expiry` | 패키지의 만료 날짜를 정의하는 타임스탬프. 기본값은 생성일로부터 90일입니다. 응답 만료 필드는 epoch UTC 시간이 됩니다. | 문자열(UTC 타임스탬프 형식) | 아니요 |
| `artifacts` | 패키지로 내보낼 아티팩트 목록입니다. `packageType`이(가) `FULL`인 경우 `artifacts` 값은 **null** 또는 **empty**&#x200B;여야 합니다. | 배열 | 아니요 |

**응답**

응답이 성공하면 새로 만든 패키지가 반환됩니다. 응답에는 해당 패키지 ID와 상태, 만료 및 아티팩트 목록에 대한 정보가 포함됩니다.

```json
{
    "id": "209f886b00444eac9bb5836fe32e7681",
    "version": 0,
    "createdDate": 1684475012105,
    "modifiedDate": 1684475012105,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "requestId": "devxa54a6b56d04f46119d9e3cc006fcc1cb",
    "userId": "platform_exim",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "cjm-mr",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1684613110000,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## 패키지 업데이트 {#update}

`/packages` 끝점에 대한 PUT 요청을 수행하여 패키지를 업데이트할 수 있습니다.

### 패키지에 아티팩트 추가 {#add-artifacts}

패키지에 아티팩트를 추가하려면 `id`을(를) 제공하고 `action`에 대해 **ADD**&#x200B;을(를) 포함해야 합니다.

**API 형식**

```http
PUT /packages/
```

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "ADD",
      "expiry": "2023-05-20T20:05:10Z", 
      "artifacts": [
        {
         "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
         "type": "JOURNEY"
        }      
      ]
  }'
```

| 속성 | 설명 | 유형 | 필수 |
| --- | --- | --- | --- |
| `id` | 업데이트할 패키지의 ID입니다. | 문자열 | 예 |
| `action` | 패키지에 아티팩트를 추가하려면 작업 값이 **ADD**&#x200B;여야 합니다. 이 작업은 **PARTIAL** 패키지 형식에서만 지원됩니다. | 문자열 | 예 |
| `artifacts` | 패키지에 추가될 아티팩트 목록입니다. 목록이 **null**&#x200B;이거나 **empty**&#x200B;인 경우 패키지에 변경 내용이 없습니다. 아티팩트는 패키지에 추가되기 전에 중복 제거됩니다. | 배열 | 아니요 |
| `expiry` | 패키지의 만료 날짜를 정의하는 타임스탬프. 페이로드에 만료가 지정되지 않은 경우 기본값은 PUT API가 호출된 시간으로부터 90일입니다. 응답 만료 필드는 epoch UTC 시간이 됩니다. | 문자열(UTC 타임스탬프 형식) | 아니요 |

**응답**

응답이 성공하면 업데이트된 패키지가 반환됩니다. 응답에는 해당 패키지 ID와 상태, 만료 및 아티팩트 목록에 대한 정보가 포함됩니다.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 4,
    "createdDate": 1684235842000,
    "modifiedDate": 1684475861366,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },     
    "packageType": "PARTIAL",
    "expiry": 1692251861352,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### 패키지에서 아티팩트 삭제 {#delete-artifacts}

패키지에서 아티팩트를 삭제하려면 `id`을(를) 제공하고 `action`에 대한 **DELETE**&#x200B;을(를) 포함해야 합니다.


**API 형식**

```http
PUT /packages/
```

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "DELETE",
      "artifacts": [
        {
          "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29@1647559351683",
          "type": "JOURNEY"
        }      
      ]
  }'
```

| 속성 | 설명 | 유형 | 필수 |
| --- | --- | --- | --- |
| `id` | 업데이트할 패키지의 ID입니다. | 문자열 | 예 |
| `action` | 패키지에서 아티팩트를 삭제하려면 작업 값이 **DELETE**&#x200B;여야 합니다. 이 작업은 **PARTIAL** 패키지 형식에서만 지원됩니다. | 문자열 | 예 |
| `artifacts` | 패키지에서 삭제할 아티팩트 목록입니다. 목록이 **null**&#x200B;이거나 **empty**&#x200B;인 경우 패키지에 변경 내용이 없습니다. | 배열 | 아니요 |

**응답**

응답이 성공하면 업데이트된 패키지가 반환됩니다. 응답에는 해당 패키지 ID와 상태, 만료 및 아티팩트 목록에 대한 정보가 포함됩니다.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 5,
    "createdDate": 1684235842000,
    "modifiedDate": 1684478830416,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",     
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },      
    "packageType": "PARTIAL",
    "expiry": 1692254830403,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

### 패키지의 메타데이터 필드 업데이트 {#update-metadata}

>[!NOTE]
>
>**UPDATE** 작업은 패키지의 패키지 메타데이터 필드를 업데이트하는 데 사용되며 **UNABLE**&#x200B;은(는) 패키지에 아티팩트를 추가/삭제하는 데 사용됩니다.

패키지의 메타데이터 필드를 업데이트하려면 `id`을(를) 제공하고 `action`에 대해 **UPDATE**&#x200B;을(를) 포함해야 합니다.

**API 형식**

```http
PUT /packages/
```

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
      "id": "6fa50baedd344a278129a87e68cc9dc7",
      "action": "UPDATE",
      "name": "acme",
      "description": "Acme Business Group",  
      "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
      }
  }'
```

| 속성 | 설명 | 유형 | 필수 |
| --- | --- | --- | --- |
| `id` | 업데이트할 패키지의 ID입니다. | 문자열 | 예 |
| `action` | 패키지의 메타데이터 필드를 업데이트하려면 작업 값이 **UPDATE**&#x200B;여야 합니다. 이 작업은 **PARTIAL** 패키지 형식에서만 지원됩니다. | 문자열 | 예 |
| `name` | 업데이트된 패키지 이름. 중복 패키지 이름은 허용되지 않습니다. | 배열 | 예 |
| `sourceSandbox` | Source 샌드박스는 요청 헤더에 지정된 것과 동일한 조직에 속해야 합니다. | 문자열 | 예 |

**응답**

응답이 성공하면 업데이트된 패키지가 반환됩니다. 응답에는 해당 패키지 ID와 설명, 상태, 만료 및 아티팩트 목록에 대한 정보가 포함됩니다.

```json
{
    "id": "6fa50baedd344a278129a87e68cc9dc7",
    "version": 6,
    "createdDate": 1684235842000,
    "modifiedDate": 1684479094129,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",    
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "packageType": "PARTIAL",
    "expiry": 1692255094127,
    "status": "DRAFT",    
    "artifactsList": [
        {
            "id": "d8d8ed6d-696a-40bd-b4fe-ca053ec94e29",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ]
}
```

## 패키지 삭제 {#delete}

패키지를 삭제하려면 `/packages` 끝점에 DELETE 요청을 하고 삭제할 패키지의 ID를 지정하십시오.

**API 형식**

```http
DELETE /packages/{PACKAGE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| {PACKAGE_ID} | 삭제할 패키지의 ID입니다. |

**요청**

다음 요청은 ID가 {PACKAGE_ID}인 패키지를 삭제합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

성공적인 응답은 패키지 ID가 삭제되었음을 보여 주는 이유를 반환합니다.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## 패키지 Publish {#publish}

패키지를 샌드박스로 가져오려면 게시해야 합니다. 게시할 패키지의 ID를 지정하는 동안 `/packages` 끝점에 GET 요청을 만듭니다.

**API 형식**

```http
GET /packages/{PACKAGE_ID}/export
```

| 매개변수 | 설명 |
| --- | --- |
| {PACKAGE_ID} | 게시하려는 패키지의 ID입니다. |

**요청**

다음 요청은 ID가 {PACKAGE_ID}인 패키지를 게시합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

| 속성 | 설명 | 유형 | 필수 |
| --- | --- | --- | --- |
| `expiryPeriod` | 이 사용자가 지정한 기간은 패키지가 게시된 시점부터 패키지 만료 날짜(일)를 정의합니다. 이 값은 음수가 아니어야 합니다.<br> 값을 지정하지 않으면 게시 날짜로부터 기본값이 90일(일)로 계산됩니다. | 정수 | 아니요 |

**응답**

성공한 응답은 게시된 패키지를 반환합니다.

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## 패키지 조회 {#look-up-package}

요청 경로에 패키지의 해당 ID를 포함하는 `/packages` 끝점에 대한 GET 요청을 수행하여 개별 패키지를 조회할 수 있습니다.

**API 형식**

```http
GET /packages/{PACKAGE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| {PACKAGE_ID} | 조회할 패키지의 ID입니다. |

**요청**

다음 요청은 {PACKAGE_ID}에 대한 정보를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

성공한 응답은 쿼리된 패키지 ID에 대한 세부 정보를 반환합니다. 응답에는 이름, 설명, 게시 날짜 및 만료 날짜, 패키지의 소스 샌드박스 및 아티팩트 목록이 포함됩니다.

```json
{
    "id": "8f585fad94d042cd82dbcba594108a41",
    "version": 2,
    "createdDate": 1685597784000,
    "modifiedDate": 1685597810000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "tenantId": "c875b077162b40409c1327b16da99c1b",
    "name": "acme",
    "description": "Acme Business Group",
    "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
    "packageType": "PARTIAL",
    "expiry": 1693373810000,
    "publishDate": 1685597810000,
    "status": "PUBLISHED",
    "artifactsList": [
        {
            "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        },
        {
            "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
            "type": "JOURNEY",
            "found": false,
            "count": 0
        }
    ],
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    }
}
```

## 패키지 나열 {#list-packages}

`/packages` 끝점에 대한 GET 요청을 통해 조직의 모든 패키지를 나열할 수 있습니다.

**API 형식**

```http
GET /packages/?{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --- | --- |
| {QUERY_PARAMS} | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](./appendix.md)의 섹션을 참조하십시오. |

**요청**

다음 요청은 {QUERY_PARAMS}을(를) 기반으로 패키지의 정보를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/?property=status==DRAFT,PUBLISHED&property=createdDate>=2023-05-11T18:29:59.999Z&property=createdDate<=2023-05-16T18:29:59.999Z&start=0&orderby=-createdDate&limit=20 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 이름, 상태, 만료 및 객체 목록과 같은 세부 사항을 포함하여 조직에 속하는 패키지 목록을 반환합니다.

```json
{
    "totalElements": 109,
    "currentPage": 0,
    "totalPages": 6,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "8f585fad94d042cd82dbcba594108a41",
            "version": 2,
            "createdDate": 1685597784000,
            "modifiedDate": 1685597810000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "c875b077162b40409c1327b16da99c1b",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693373810000,
            "publishDate": 1685597810000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "f4f57771-2bd2-469a-9c13-8d803eeb6515",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                },
                {
                    "id": "7f4caca7-a477-400d-a41e-c4735f8e780d",
                    "type": "JOURNEY",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        },
        {
            "id": "0d7e427ce4cb4dc1b78e30ef61b125c1",
            "version": 2,
            "createdDate": 1685555213000,
            "modifiedDate": 1685555275000,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "tenantId": "7d7d8bbe3c7c4a8ea701cc5e42c57aeb",
            "name": "acme",
            "description": "Acme Business Group",
            "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg",
            "packageType": "PARTIAL",
            "expiry": 1693331275000,
            "publishDate": 1685555275000,
            "status": "PUBLISHED",
            "artifactsList": [
                {
                    "id": "626a9669a9f5b818db270e95",
                    "type": "CATALOG_DATASET",
                    "found": false,
                    "count": 0
                }
            ],
            "sourceSandbox": {
                "name": "acme-sandbox",
                "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
            }
        }
    ]
}
```

## 패키지 가져오기 {#import}

이 끝점은 지정된 대상 샌드박스에서 충돌하는 개체를 가져오는 데 사용됩니다. 충돌하는 오브젝트는 대상 샌드박스에 이미 존재하는 유사한 오브젝트를 나타냅니다.

**API 형식**

```http
GET /packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName
```

| 매개변수 | 설명 |
| --- | --- |
| {PACKAGE_ID} | 조회할 패키지의 ID입니다. |

**요청**

다음 요청은 {PACKAGE_ID}을(를) 가져옵니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

충돌은 응답에서 반환됩니다. 응답에는 원래 패키지와 `alternatives` 조각이 순위별로 정렬된 배열로 표시됩니다.

응답 보기+++

```json
[
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/176f33f6a8ff6542de1256f8dc01cce4be1b3a68fd5f5bc5",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686403052050"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/1b37c3403e4e12c7aa46ea9dfe380a9f2b72d4da9db62b46",
                "type": "REGISTRY_SCHEMA",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870_1686218766627"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_SCHEMA::https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c"
    },
    {
        "artifact": {
            "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
            "type": "REGISTRY_CLASS",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/1dd81d61cdaa89a89382d0a424db77494475bd1db3105feb",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686564843736"
            },
            {
                "id": "https://ns.adobe.com/cjmstage/classes/2511fb5396a630b2cd3d5d9e9b69d42ce66a4289db8ac917",
                "type": "REGISTRY_CLASS",
                "found": false,
                "count": 0,
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870_1686408152916"
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::REGISTRY_CLASS::https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26"
    },
    {
        "artifact": {
            "id": "4d4c874ec3344d64bf8b3160e60ac78b",
            "type": "MAPPING_SET",
            "found": false,
            "count": 0,
            "messages": [
                {
                    "status": "FOUND",
                    "attempt": 1,
                    "message": "Found object with ID: 4d4c874ec3344d64bf8b3160e60ac78b"
                }
            ]
        },
        "suggestionList": [
            {
                "id": "6b49c959d77c48e9904f7616fe2e7848",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "7b363da9e6704afb9716f57193d5246f",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            },
            {
                "id": "93ca0b4f437c4eaf9f1986408679e965",
                "type": "MAPPING_SET",
                "found": false,
                "count": 0,
                "title": ""
            }
        ],
        "parentID": "745F37C35E4B776E0A49421B@AdobeOrg::prod::MAPPING_SET::4d4c874ec3344d64bf8b3160e60ac78b"
    }
]
```

+++

## 가져오기 제출 {#submit-import}

>[!NOTE]
>
>대체 아티팩트가 대상 샌드박스에 이미 존재한다는 것은 충돌 해결에 내재되어 있습니다.

충돌을 검토하고 `/packages` 끝점에 대한 POST 요청을 통해 대체를 제공한 후 패키지에 대한 가져오기를 제출할 수 있습니다. 결과는 페이로드로 제공되며, 페이로드에 지정된 대로 대상 샌드박스에 대한 가져오기 작업을 시작합니다.

페이로드에서 가져오기 작업에 대해 사용자가 지정한 작업 이름 및 설명도 허용합니다. 사용자가 지정한 이름 및 설명을 사용할 수 없는 경우 패키지 이름 및 설명이 작업 이름 및 설명에 사용됩니다.

**API 형식**

```http
POST /packages/import
```

**요청**

다음 요청은 가져올 패키지를 검색합니다. 페이로드는 항목이 존재하는 경우 키는 패키지에서 제공된 `artifactId`이고 대체 값은 값인 대체 맵입니다. 맵 또는 페이로드가 **empty**&#x200B;인 경우 대체가 수행되지 않습니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/import/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d'{
       "id": "09484a599f5f4a5faa43986643964615",
       "name": "acme",
       "description": "Acme Business Group",
       "destinationSandbox": {
         "name": "cjm-mr",
         "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
     },
     "alternatives": {
       "https://ns.adobe.com/cjmstage/schemas/ac33bbd22eb4ad6656e1c7e12e9f520261fb39fd28a902a9": {
         "id": "https://ns.adobe.com/cjmstage/schemas/a3b935344685afad4e52c753161cf673ec23d4fb1b3e9ce",
         "type": "REGISTRY_SCHEMA"
       }
     }
  }'
```

| 속성 | 설명 | 유형 | 필수 |
| --- | --- | --- | --- |
| `alternatives` | `alternatives`은(는) 소스 샌드박스 아티팩트와 기존 대상 샌드박스 아티팩트의 매핑을 나타냅니다. 이미 존재하기 때문에 가져오기 작업은 대상 샌드박스에서 이러한 아티팩트를 생성하지 않습니다. | 문자열 | 아니요 |

**응답**

```json
{
    "name": "acme",
    "description": "Acme Business Group",
    "visibility": "TENANT",
    "sourceSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "destinationSandbox":
    {
        "name": "acme-sandbox",
        "imsOrgId": "5C1328435BF324E90A49402A@AdobeOrg"
    },
    "type": "PARTIAL",
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285"
}
```

## 모든 종속 개체 나열 {#dependent-objects}

패키지의 ID를 지정하는 동안 `/packages` 끝점에 대한 POST 요청을 수행하여 내보낸 개체에 대한 모든 종속 개체를 패키지에 나열합니다.

**API 형식**

```http
POST /packages/{PACKAGE_ID}/children
```

| 매개변수 | 설명 |
| --- | --- |
| {PACKAGE_ID} | 패키지의 ID입니다. |

**요청**

다음 요청은 {PACKAGE_ID}에 대한 모든 종속 개체를 나열합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import?targetSandbox=targetSandboxName \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d'[
      {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "type": "REGISTRY_SCHEMA"
      },
      {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "type": "REGISTRY_CLASS"
      }
  ]'
```

**응답**

성공한 응답은 개체에 대한 하위 목록을 반환합니다.

```json
[
    {
        "id": "4d4c874ec3344d64bf8b3160e60ac78b",
        "title": "4d4c874ec3344d64bf8b3160e60ac78b",
        "type": "MAPPING_SET",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
                "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
                "type": "REGISTRY_SCHEMA"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/schemas/20121c2110bb2c6a585baabe5f82994577da1f7d0628234c",
        "title": "Dean Dataset 1 - adhoc schema - 1618950408870",
        "type": "REGISTRY_SCHEMA",
        "children": [
            {
                "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
                "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
                "type": "REGISTRY_CLASS"
            }
        ]
    },
    {
        "id": "https://ns.adobe.com/cjmstage/classes/24c1525f4f06fae2d203c6b78e26ae479ec4541c2c0d6b26",
        "title": "Dean Dataset 1 - Adhoc class - 1618950408870",
        "type": "REGISTRY_CLASS",
        "children": []
    }
]
```

## 모든 패키지 아티팩트를 가져오려면 역할 기반 권한 확인 {#role-based-permissions}

패키지 ID 및 대상 샌드박스 이름을 지정하는 동안 `/packages` 끝점에 대한 GET 요청을 수행하여 패키지 아티팩트를 가져올 수 있는 권한이 있는지 확인할 수 있습니다.

**API 형식**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| 매개변수 | 설명 |
| --- | --- |
| {PACKAGE_ID} | 가져오려는 패키지의 ID입니다. |

**요청**

다음 요청은 {PACKAGE_ID} 및 샌드박스에 대한 권한을 확인합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/preflight/{PACKAGE_ID}?targetSandbox=<sandbox_name> \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 필요한 권한 목록, 누락된 권한, 아티팩트 유형 및 생성 허용 여부에 대한 결정 등 타겟 샌드박스에 대한 리소스 권한을 반환합니다.

응답 보기+++

```json
{
  "packageID": "b7bda68eb1214c86824f1d7204616e51",
  "targetSandboxName": "acme-sandbox",
  "permissionResponse": [
    {
      "artifactID": "4aca57b6-8b83-450b-a460-e8a07ca79a44",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "Schema",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read"
            ]
          },
          {
            "palmResourceType": "Segment",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Composition",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Query",
            "resourcePermissions": [
              "write"
            ]
          },
          {
            "palmResourceType": "SegmentDashboard",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": []
      },
      "artifactType": "PROFILE_SEGMENT",
      "creationAllowed": true
    },
    {
      "artifactID": "36bb82bc-a00d-4d6b-a598-227d43e027c1",
      "requiredPermissions": {
        "resources": [
          {
            "palmResourceType": "Sandbox",
            "resourcePermissions": [
              "view"
            ]
          },
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "read",
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "missingPermissions": {
        "resources": [
          {
            "palmResourceType": "ProfileConfig",
            "resourcePermissions": [
              "write",
              "delete"
            ]
          },
          {
            "palmResourceType": "Dataset",
            "resourcePermissions": [
              "read"
            ]
          }
        ]
      },
      "artifactType": "PROFILE_MERGE",
      "creationAllowed": false
    }
  ]
}
```

+++

## 내보내기/가져오기 작업 나열 {#list-jobs}

`/packages` 끝점에 대한 GET 요청을 수행하여 현재 내보내기/가져오기 작업을 나열할 수 있습니다.

**API 형식**

```http
GET /packages/jobs?{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --- | --- |
| {QUERY_PARAMS} | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](./appendix.md)의 섹션을 참조하십시오. |

**요청**

다음 요청은 성공한 모든 가져오기 작업을 나열합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

성공한 응답은 성공한 가져오기 작업을 모두 반환합니다.

```json
{
    "totalElements": 42,
    "currentPage": 0,
    "totalPages": 9,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "3c1b92cf47a246d7bfbe6fd507c5d543",
            "name": "acme",
            "updated": 1685973675401,
            "created": 1685973675401,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "ead59d21405f4184a94dd786a1bf040d",
            "name": "acme1",
            "updated": 1685986367198,
            "created": 1685986367198,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "85ddaa3c2f6c475088167cde7a9d4326",
            "name": "acme2",
            "updated": 1686147692568,
            "created": 1686147692568,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "c49a4fcb31954cbd828ece1da096c8f5",
            "name": "acme3",
            "updated": 1686148007586,
            "created": 1686148007586,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        },
        {
            "id": "a3669315baed4cf2af49bf9ce90b8158",
            "name": "acme4",
            "updated": 1686148651910,
            "created": 1686148651910,
            "jobType": "NEW",
            "packageType": "PARTIAL",
            "description": "Acme Business Group",
            "jobStatus": "SUCCESS",
            "visibility": "TENANT",
            "sourceSandBox": "acme-sandbox",
            "targetSandbox": "poc",
            "createdBy": "{CREATED_BY}"
        }
    ]
}
```
