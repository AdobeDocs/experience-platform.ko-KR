---
title: 샌드박스 도구 패키지 API 끝점
description: 샌드박스 도구 API의 /packages 끝점을 사용하면 Adobe Experience Platform에서 패키지를 프로그래밍 방식으로 관리할 수 있습니다.
exl-id: 46efee26-d897-4941-baf4-d5ca0b8311f0
source-git-commit: 1d8c29178927c7ee3aceb0b68f97baeaefd9f695
workflow-type: tm+mt
source-wordcount: '2933'
ht-degree: 8%

---

# 패키지 끝점

샌드박스 도구 를 사용하면 객체라고도 하는 다양한 객체를 선택하여 패키지로 내보낼 수 있습니다. 패키지는 단일 아티팩트 또는 여러 아티팩트(예: 데이터 세트 또는 스키마)로 구성될 수 있습니다. 패키지에 포함된 모든 아티팩트는 동일한 샌드박스의 아티팩트여야 합니다.

샌드박스 도구 API의 `/packages` 끝점을 사용하면 패키지 게시 및 샌드박스로 패키지 가져오기를 포함하여 조직의 패키지를 프로그래밍 방식으로 관리할 수 있습니다.

## 패키지 만들기 {#create}

패키지 이름 및 패키지 유형에 대한 값을 제공하는 동안 `/packages` 끝점에 대한 POST 요청을 수행하여 다중 아티팩트 패키지를 만들 수 있습니다.

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
| `sourceSandbox` | 패키지의 소스 샌드박스. | 오브젝트 | 아니요 |
| `expiry` | 패키지의 만료 날짜를 정의하는 타임스탬프. 기본값은 생성일로부터 90일입니다. 응답 만료 필드는 epoch UTC 시간이 됩니다. | 문자열(UTC 타임스탬프 형식) | 아니요 |
| `artifacts` | 패키지로 내보낼 아티팩트 목록입니다. `artifacts`이(가) **인 경우** 값은 **null** 또는 `packageType`empty`FULL`여야 합니다. | 배열 | 아니요 |

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

샌드박스 도구 API에서 `/packages` 끝점을 사용하여 패키지를 업데이트합니다.

### 패키지에 아티팩트 추가 {#add-artifacts}

패키지에 아티팩트를 추가하려면 `id`을(를) 제공하고 **에 대해** ADD`action`을(를) 포함해야 합니다.

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
| `artifacts` | 패키지에 추가될 아티팩트 목록입니다. 목록이 **null**&#x200B;이거나 **empty**&#x200B;인 경우 패키지에 변경 내용이 없습니다. 아티팩트는 패키지에 추가되기 전에 중복 제거됩니다. 지원되는 객체의 전체 목록은 아래 표를 참조하십시오. | 배열 | 아니요 |
| `expiry` | 패키지의 만료 날짜를 정의하는 타임스탬프. 페이로드에 만료가 지정되지 않은 경우 기본값은 PUT API가 호출된 시간으로부터 90일입니다. 응답 만료 필드는 epoch UTC 시간이 됩니다. | 문자열(UTC 타임스탬프 형식) | 아니요 |

현재 지원되는 아티팩트 유형은 다음과 같습니다.

| 아티팩트 | 플랫폼 | 오브젝트 | 부분 흐름 | 전체 샌드박스 |
| --- | --- | --- | --- | --- |
| `JOURNEY` | Adobe Journey Optimizer | 여정 | 예 | 아니요 |
| `ID_NAMESPACE` | 고객 데이터 플랫폼 | ID | 예 | 예 |
| `REGISTRY_DATATYPE` | 고객 데이터 플랫폼 | 데이터 유형 | 예 | 예 |
| `REGISTRY_CLASS` | 고객 데이터 플랫폼 | 클래스 | 예 | 예 |
| `REGISTRY_MIXIN` | 고객 데이터 플랫폼 | 필드 그룹 | 예 | 예 |
| `REGISTRY_SCHEMA` | 고객 데이터 플랫폼 | 스키마 | 예 | 예 |
| `CATALOG_DATASET` | 고객 데이터 플랫폼 | 데이터 세트 | 예 | 예 |
| `DULE_CONSENT_POLICY` | 고객 데이터 플랫폼 | 동의 및 거버넌스 정책 | 예 | 예 |
| `PROFILE_SEGMENT` | 고객 데이터 플랫폼 | 대상자 | 예 | 예 |
| `FLOW` | 고객 데이터 플랫폼 | 소스 데이터 흐름 | 예 | 예 |

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

패키지에서 아티팩트를 삭제하려면 `id`을(를) 제공하고 **에 대한** DELETE`action`을(를) 포함해야 합니다.

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

패키지의 메타데이터 필드를 업데이트하려면 `id`을(를) 제공하고 **에 대해** UPDATE`action`을(를) 포함해야 합니다.

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
| `sourceSandbox` | Source 샌드박스는 요청 헤더에 지정된 것과 동일한 조직에 속해야 합니다. | 오브젝트 | 예 |

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

패키지를 삭제하려면 `/packages` 끝점에 대한 DELETE 요청을 만들고 삭제할 패키지의 ID를 지정하십시오.

**API 형식**

```http
DELETE /packages/{PACKAGE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{PACKAGE_ID}` | 삭제할 패키지의 ID입니다. |

**요청**

다음 요청은 ID가 {PACKAGE_ID}인 패키지를 삭제합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 패키지 ID가 삭제되었음을 보여 주는 이유를 반환합니다.

```json
{
    "reason": "Package d30e0424a37b46ada6a5cf37f47a86ff deleted"
}
```

## 패키지 게시 {#publish}

패키지를 샌드박스로 가져오려면 게시해야 합니다. 게시할 패키지의 ID를 지정하는 동안 `/packages` 끝점에 GET 요청을 만듭니다.

**API 형식**

```http
GET /packages/{PACKAGE_ID}/export
```

| 매개변수 | 설명 |
| --- | --- |
| `{PACKAGE_ID}` | 게시하려는 패키지의 ID입니다. |

**요청**

다음 요청은 ID가 {PACKAGE_ID}인 패키지를 게시합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}\export \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
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
| `{PACKAGE_ID}` | 조회할 패키지의 ID입니다. |

**요청**

다음 요청은 {PACKAGE_ID}에 대한 정보를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](./appendix.md)의 섹션을 참조하십시오. |

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
| `{PACKAGE_ID}` | 조회할 패키지의 ID입니다. |

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

+++응답 보기

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
    "correlationId": "48effe5e-1bef-4250-9c71-23b93ef5d285",
    "jobId": "18abab44e25f40c284a4bd6e8f52fd29"
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
| `{PACKAGE_ID}` | 패키지의 ID입니다. |

**요청**

다음 요청은 {PACKAGE_ID}에 대한 모든 종속 개체를 나열합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/children \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

패키지의 ID와 대상 샌드박스 이름을 지정하는 동안 `/packages` 끝점에 대한 GET 요청을 수행하여 패키지 아티팩트를 가져올 수 있는 권한이 있는지 확인할 수 있습니다.

**API 형식**

```http
GET /packages/preflight/{packageId}?targetSandbox=<sandbox_name
```

| 매개변수 | 설명 |
| --- | --- |
| `{PACKAGE_ID}` | 가져오려는 패키지의 ID입니다. |

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

+++응답 보기

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
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](./appendix.md)의 섹션을 참조하십시오. |

**요청**

다음 요청은 성공한 모든 가져오기 작업을 나열합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/jobs?property=requestType==IMPORT&property=jobStatus==SUCCESS&orderby=createdDate&start=0&limit=5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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

## 조직 간 패키지 공유 {#org-linking}

샌드박스 도구 API의 `/handshake` 끝점을 사용하면 다른 조직과 협력하여 패키지를 공유할 수 있습니다.

### 공유 요청 보내기 {#send-request}

`/handshake/bulkCreate` 끝점에 POST 요청을 하여 공유 승인을 위해 대상 파트너 조직에 요청을 보냅니다. 비공개 패키지를 공유하려면 먼저 이 작업이 필요합니다.

**API 형식**

```http
POST /handshake/bulkCreate
```

**요청**

다음 요청은 대상 파트너 조직과 소스 조직 간에 공유 승인을 시작합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/handshake/bulkCreate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "targetIMSOrgIds":["acme@AdobeOrg"],
      "sourceIMSDetails":{
        "id":"acme@AdobeOrg",
        "name":"acme_org"
      } 
  }' 
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `targetIMSOrgIds` | 공유 요청을 보낼 대상 조직의 목록입니다. | 배열 | 예 |
| `sourceIMSDetails` | 소스 조직에 대한 세부 정보. | 오브젝트 | 예 |

**응답**

성공적인 응답이 공유 요청에 대한 세부 정보를 반환합니다.

```json
{
    "successfulRequests": {
        "acme@AdobeOrg": {
            "id": "{ID}",
            "version": 0,
            "createdDate": 1724938816798,
            "modifiedDate": 1724938816798,
            "createdBy": "{CREATED_BY}",
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va6",
            "sourceIMSOrgName": "{SOURCE_NAME}",
            "status": "APPROVAL_PENDING",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{ORG_ID}",
            "statusHistory": "[{\"actionTakenBy\":\"acme@98ff67fa661fdf6549420b.e\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724938816885}]",
            "linkingId": "{LINKING_ID}"
        }
    },
    "failedRequests": {}
}
```

### 수신된 공유 요청 승인 {#approve-requests}

`/handshake/action` 끝점에 대한 POST 요청을 만들어 대상 파트너 조직의 공유 요청을 승인합니다. 승인 후 소스 파트너 조직은 비공개 패키지를 공유할 수 있습니다.

**API 형식**

```http
POST /handshake/action
```

**요청**

다음 요청은 대상 파트너 조직의 공유 요청을 승인합니다.

```shell
curl -X POST  \
  https://platform.adobe.io/data/foundation/exim/handshake/action \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "linkingID":"{LINKING_ID}",
      "status":"APPROVED",
      "reason":"Done",
      "targetIMSOrgDetails":{
          "id":"acme@AdobeOrg",
          "name":"acme",
          "region":"va7"
      }
  }'
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `linkingID` | 응답 중인 공유 요청의 ID입니다. | 문자열 | 예 |
| `status` | 공유 요청에 대해 수행되는 작업입니다. 허용되는 값은 `APPROVED` 또는 `REJECTED`입니다. | 문자열 | 예 |
| `reason` | 작업이 수행되는 이유입니다. | 문자열 | 예 |
| `targetIMSOrgDetails` | ID 값이 대상 조직의 **ID**, 이름 값이 대상 조직의 **NAME**, 지역 값이 대상 조직 **REGION**&#x200B;인 대상 조직에 대한 세부 정보입니다. | 오브젝트 | 예 |

**응답**

성공적인 응답은 승인된 공유 요청에 대한 세부 정보를 반환합니다.

```json
{
    "id": "{ID}",
    "version": 1,
    "createdDate": 1726737474000,
    "modifiedDate": 1726737541731,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "sourceRegion": "va7",
    "targetRegion": "va7",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetOrgName": "{TARGET_ORG}",
    "status": "APPROVED",
    "createdByName": "{CREATED_BY}",
    "modifiedByIMSOrgId": "{MODIFIED_BY}",
    "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"acme@AdobeOrg\",\"action\":\"INITIATED\",\"actionTimeStamp\":1726737474450,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":null,\"actionTakenByImsOrgID\":\"745F37C35E4B776E0A49421B@AdobeOrg\",\"action\":\"APPROVED\",\"actionTimeStamp\":1726737541818,\"reason\":\"Done\"}]",
    "linkingId": "{LINKING_ID}"
}
```

### 나가는/들어오는 공유 요청 나열 {#outgoing-and-incoming-requests}

`handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING` 끝점에 GET 요청을 하여 나가는 공유 요청과 들어오는 공유 요청을 나열합니다.

**API 형식**

```http
GET handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING
```

| 매개변수 | 수락됨/기본값 |
| --- | --- |
| `property` | 상태 등 필터링 기준으로 사용할 속성을 지정합니다. 상태에 사용할 수 있는 값은 `APPROVED`, `REJECTED` 및 `IN_PROGRESS`입니다. |
| `start` | 시작의 기본값은 `0`입니다. |
| `limit` | 제한의 기본값은 `20`입니다. |
| `orderBy` | 레코드를 오름차순 또는 내림차순으로 정렬합니다. |
| `requestType` | `INCOMING` 또는 `OUTGOING`을(를) 허용합니다. |

**요청**

다음 요청은 나가는 모든 공유 요청과 들어오는 공유 요청의 목록을 반환합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/handshake/list?property=status%3D%3DAPPROVED&requestType=INCOMING \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id:{ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**응답**

성공적인 응답은 발신 및 수신 공유 요청 목록과 세부 정보를 반환합니다.

```json
{
    "totalElements": 1,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "version": 1,
            "createdDate": 1724929446000,
            "modifiedDate": 1724929617000,
            "modifiedBy": "{MODIFIED_BY}",
            "sourceIMSOrgId": "{ORG_ID}",
            "targetIMSOrgId": "{TARGET_ID}",
            "sourceRegion": "va7",
            "targetRegion": "va6",
             "sourceOrgName": "{SOURCE_ORG}",
            "targetOrgName": "{TARGET_ORG}",
            "status": "APPROVED",
            "createdByName": "{CREATED_BY}",
            "modifiedByName": "{MODIFIED_BY}",
            "modifiedByIMSOrgId": "{MODIFIED_BY}",
            "statusHistory": "[{\"actionTakenBy\":\"{ACTION_BY}\",\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"INITIATED\",\"actionTimeStamp\":1724929442467,\"reason\":null},{\"actionTakenBy\":null,\"actionTakenByName\":\"{NAME}\",\"actionTakenByImsOrgID\":\"{ORG_ID}\",\"action\":\"APPROVED\",\"actionTimeStamp\":1724929617531,\"reason\":\"Done\"}]",
            "linkingId": "{LINKING_ID}"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

## 패키지 전송

샌드박스 도구 API의 `/transfer` 끝점을 사용하여 새 패키지 공유 요청을 가져오고 만듭니다.

### 새 공유 요청 {#share-request}

패키지 ID와 대상 조직의 ID를 제공하는 동안 `/transfer` 끝점에 대한 POST 요청을 만들어 게시된 원본 조직의 패키지를 가져와 대상 조직과 공유합니다.

**API 형식**

```http
POST /transfer
```

**요청**

다음 요청은 소스 조직 패키지를 가져와 타겟 조직과 공유합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "packageId": "{PACKAGE_ID}",
      "targets": [
          {
              "imsOrgId": "{TARGET_IMS_ORG}"
          }
      ]
  }'
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `packageId` | 공유할 패키지의 ID입니다. | 문자열 | 예 |
| `targets` | 패키지화할 공유 조직 목록입니다. | 배열 | 예 |

**응답**

성공적인 응답은 요청된 패키지의 세부 정보와 공유 상태를 반환합니다.

```json
[
    {
        "id": "{ID}",
        "version": 0,
        "createdDate": 1726480559313,
        "modifiedDate": 1726480559313,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "sourceIMSOrgId": "{ORG_ID}",
        "targetIMSOrgId": "{TARGET_ID}",
        "packageId": "{PACKAGE_ID}",
        "status": "PENDING",
        "initiatedBy": "acme@3ec9197a65a86f34494221.e",
        "requestType": "PRIVATE"
    }
]
```

### ID로 공유 요청 가져오기 {#fetch-transfer-by-id}

전송 ID를 제공하는 동안 `/transfer/{TRANSFER_ID}` 끝점에 대한 GET 요청을 수행하여 공유 요청의 세부 정보를 가져옵니다.

**API 형식**

```http
GET /transfer/{TRANSFER_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{TRANSFER_ID}` | 가져오려는 전송 ID입니다. |

**요청**

다음 요청은 ID가 {TRANSFER_ID}인 전송을 가져옵니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/0c843180a64c445ca1beece339abc04b \
  -H 'x-api-key: {API__KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**응답**

성공 응답이 공유 요청의 세부 정보를 반환합니다.

```json
{
    "id": "{ID}",
    "sourceIMSOrgId": "{ORG_ID}",
    "sourceOrgName": "{SOURCE_ORG}",
    "targetIMSOrgId": "{TARGET_ID}",
    "targetOrgName": "{TARGET_ORG}",
    "packageId": "{PACKAGE_ID}",
    "packageName": "{PACKAGE_NAME}",
    "status": "COMPLETED",
    "initiatedBy": "{INITIATED_BY}",
    "createdDate": 1724442856000,
    "requestType": "PRIVATE"
}
```

### 공유 목록 가져오기 {#transfers-list}

`/transfer/list?{QUERY_PARAMETERS}` 끝점에 대한 GET 요청을 만들고 필요에 따라 쿼리 매개 변수를 변경하여 전송 요청 목록을 가져옵니다.

**API 형식**

```http
GET `/transfer/list?{QUERY_PARAMETERS}`
```

| 매개변수 | 수락됨/기본값 |
| --- | --- |
| `property` | 상태 등 필터링 기준으로 사용할 속성을 지정합니다. 상태에 사용할 수 있는 값은 `COMPLETED`, `PENDING`, `IN_PROGRESS`, `FAILED`입니다. |
| `start` | 시작의 기본값은 `0`입니다. |
| `limit` | 제한의 기본값은 `20`입니다. |
| `orderBy` | 순서 지정은 `createdDate` 필드만 허용합니다. |

**요청**

다음 요청은 제공된 검색 매개 변수에서 전송 요청 목록을 가져옵니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status==COMPLETED&start=0&limit=2&orderBy=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'
```

**응답**

성공적인 응답은 제공된 검색 매개 변수에서 모든 전송 요청 목록을 반환합니다.

```json
{
    "totalElements": 43,
    "currentPage": 0,
    "totalPages": 22,
    "hasPreviousPage": false,
    "hasNextPage": true,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726129077000,
            "createdDate": 1726129062000,
            "requestType": "PRIVATE"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_ORG}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "{PACKAGE_NAME}",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1726066046000,
            "createdDate": 1726065936000,
            "requestType": "PRIVATE"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

### 패키지 가용성을 비공개에서 공개로 업데이트 {#update-availability}

`/packages/update` 끝점에 대한 GET 요청을 수행하여 패키지를 private에서 public으로 변경합니다. 기본적으로 패키지는 비공개 가용성으로 생성됩니다.

**API 형식**

```http
PUT `/packages/update`
```

**요청**

다음 요청은 패키지 가용성을 private에서 public으로 변경합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/exim/packages \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
      "id":"{ID}",
      "action":"UPDATE",
      "packageVisibility":"PUBLIC"
  }'
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `id` | 업데이트할 패키지의 ID입니다. | 문자열 | 예 |
| `action` | 공개 수준을 업데이트하려면 작업 값이 **UPDATE**&#x200B;여야 합니다. | 문자열 | 예 |
| `packageVisbility` | 가시성을 업데이트하려면 packageVisibility 값이 **PUBLIC**&#x200B;이어야 합니다. | 문자열 | 예 |

**응답**

성공적인 응답은 패키지에 대한 세부 정보와 해당 가시성을 반환합니다.

```json
{
    "id": "{ID}",
    "version": 7,
    "createdDate": 1729624618000,
    "modifiedDate": 1729658596340,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "acme",
    "imsOrgId": "{ORG_ID}",
    "packageType": "PARTIAL",
    "expiry": 1737434596325,
    "status": "PUBLISH_FAILED",
    "packageVisibility": "PUBLIC",
    "artifactsList": [
        {
            "id": "{ID}",
            "type": "PROFILE_SEGMENT",
            "found": false,
            "count": 0,
            "title": "Acme Profile Segment"
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "acme-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    }
}
```

### 공개 패키지 가져오기 요청 {#pull-public-package}

`/transfer/pullRequest` 끝점에 대한 POST 요청을 수행하여 공개 가능한 원본 조직에서 패키지를 가져옵니다.

**API 형식**

```http
POST /transfer/pullRequest
```

**요청**

다음 요청은 패키지를 가져오고 해당 가용성을 public으로 설정합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/exim/transfer/pullRequest \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -d '{
      "imsOrgId": "{ORG_ID}",
      "packageId": "{PACKAGE_ID}"
  }'
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `imsOrgId` | 패키지의 소스 조직 ID입니다. | 문자열 | 예 |
| `packageId` | 가져올 패키지의 ID입니다. | 문자열 | 예 |

**응답**

성공한 응답은 가져온 공개 패키지에 대한 세부 정보를 반환합니다.

```json
{
    "id": "{ID}",
    "version": 0,
    "createdDate": 1729658890425,
    "modifiedDate": 1729658890425,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sourceIMSOrgId": "{ORG_ID}",
    "targetIMSOrgId": "{TARGET_ID}",
    "packageId": "{PACKAGE_ID}",
    "status": "PENDING",
    "initiatedBy": "{INITIATED_BY}",
    "pipelineMessageId": "{MESSAGE_ID}",
    "requestType": "PUBLIC"
}
```

### 공개 패키지 나열 {#list-public-packages}

`/transfer/list?{QUERY_PARAMS}` 끝점에 대한 GET 요청을 만들어 공개 가능한 패키지 목록을 가져옵니다.

**API 형식**

```http
GET /transfer/list?{QUERY_PARAMS}
```

| 매개변수 | 수락됨/기본값 |
| --- | --- |
| `property` | 상태 등 필터링 기준으로 사용할 속성을 지정합니다. 상태에 사용할 수 있는 값은 `COMPLETED` 및 `FAILED`입니다. |
| `start` | 시작의 기본값은 `0`입니다. |
| `limit` | 제한의 기본값은 `20`입니다. |
| `orderBy` | 순서 지정은 `createdDate` 필드만 허용합니다. |
| `requestType` | `PUBLIC` 또는 `PRIVATE`을(를) 허용합니다. |

**요청**

다음 요청은 공개 가용성이 있는 패키지 목록을 가져옵니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/transfer/list?property=status%3D%3DCOMPLETED%2CFAILED&requestType=PUBLIC&orderby=-createdDate \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

**응답**

성공적인 응답은 공개 패키지 목록과 세부 정보를 반환합니다.

+++응답 보기

```json
{
    "totalElements": 14,
    "currentPage": 0,
    "totalPages": 1,
    "hasPreviousPage": false,
    "hasNextPage": false,
    "data": [
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_ORG}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359318000,
            "createdDate": 1729359316000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public package demo",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729359284000,
            "createdDate": 1729359283000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Test Private Flow Final",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284462000,
            "createdDate": 1729275962000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOUCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Fest",
            "status": "FAILED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284104000,
            "createdDate": 1729253854000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "PublicPackageSharing",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284835000,
            "createdDate": 1729253556000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284667000,
            "createdDate": 1729253421000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284957000,
            "createdDate": 1729253143000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package Audit Test",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284562000,
            "createdDate": 1729252975000,
            "requestType": "PUBLIC"
        },
        {
               "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Private Package Test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284262000,
            "createdDate": 1729229755000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Demo Package 1016",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284784000,
            "createdDate": 1729208888000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284934000,
            "createdDate": 1729153097000,
            "requestType": "PUBLIC"
        },
        {
            "id": "{ID}",
            "sourceIMSOrgId": "{ORG_ID}",
            "sourceOrgName": "{SOURCE_NAME}",
            "targetIMSOrgId": "{TARGET_ID}",
            "targetOrgName": "{TARGET_NAME}",
            "packageId": "{PACKAGE_ID}",
            "packageName": "Public Package test 1",
            "status": "COMPLETED",
            "initiatedBy": "{INITIATED_BY}",
            "completedTime": 1729284912000,
            "createdDate": 1729153043000,
            "requestType": "PUBLIC"
        }
    ],
    "nextPage": null,
    "pageSize": null
}
```

+++

## 패키지 페이로드 복사(#package-payload)

요청 경로에 패키지의 해당 ID를 포함하는 `/packages/payload` 끝점에 GET 요청을 만들어 공개 패키지의 페이로드를 복사할 수 있습니다.

**API 형식**

```http
GET /packages/payload/{PACKAGE_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{PACKAGE_ID}` | 복사할 패키지의 ID입니다. |

**요청**

다음 요청은 ID가 {PACKAGE_ID}인 패키지의 페이로드를 가져옵니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/exim/packages/payload/{PACKAGE_ID} \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `imsOrdId` | 패키지가 속한 조직의 ID입니다. | 문자열 | 예 |
| `packageId` | 요청하는 페이로드의 패키지 ID입니다. | 문자열 | 예 |

**응답**

성공적인 응답은 패키지의 페이로드를 반환합니다.

```json
{
    "imsOrgId": "{ORG_ID}",
    "packageId": "{PACKAGE_ID}"
}
```

## 개체 구성 업데이트 마이그레이션

샌드박스 도구 API의 /packages 끝점을 사용하여 개체 구성 업데이트를 마이그레이션합니다.

### 업데이트 작업(#update-operations)

패키지 스냅숏의 지정된 버전 또는 최신 버전을 패키지 ID를 제공하여 `/packages/{packageId}/version/compare` 끝점에 POST 요청을 수행하여 패키지를 가져온 원본 샌드박스 또는 이전에 사용된 대상 샌드박스의 현재 상태와 비교합니다.

***API 형식***

```http
PATCH /packages/{packageId}/version/compare
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `packageId` | 패키지의 ID입니다. | 문자열 | 예 |

**요청**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/compare/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "triggerNew": true,
      "targetSandbox": "{SANDBOX_NAME}"
  }'
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `triggerNew` | 활성 작업이나 완료된 작업이 이미 있는 경우에도 새 비교 계산 작업을 트리거하는 플래그입니다. | 부울 | 아니요 |
| `targetSandbox` | 차이를 계산할 대상 샌드박스의 이름을 나타냅니다. 지정하지 않으면 소스 샌드박스가 대상 샌드박스로 사용됩니다. | 문자열 | 아니요 |

**응답**

이전에 완료된 작업에 대한 성공적인 응답은 이전에 계산된 비교 결과와 함께 작업 개체를 반환합니다. 새로 완료된 작업은 작업 ID를 반환합니다.

+++응답 보기(제출된 작업)

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "c4b7d07ae4c646279e2070a31c50bd5c",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "SUCCESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "deltaPackageVersion": {
            "packageId": "{PACKAGE_ID}",
            "currentVersion": 0,
            "validated": false,
            "rootArtifacts": [
                {
                    "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de",
                    "type": "REGISTRY_SCHEMA",
                    "found": false,
                    "count": 0
                }
            ],
            "eximGraphDelta": {
                "vertices": [],
                "pluginDeltas": [
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 2_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 2_1738766274074",
                                "newValue": "Custom FieldGroup 2"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    },
                    {
                        "sourceArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4"
                        },
                        "targetArtifact": {
                            "id": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
                            "type": "REGISTRY_MIXIN",
                            "found": false,
                            "count": 0,
                            "title": "Custom FieldGroup 4_1738766274074"
                        },
                        "changes": [
                            {
                                "op": "replace",
                                "path": "/title",
                                "oldValue": "Custom FieldGroup 4_1738766274074",
                                "newValue": "Custom FieldGroup 4"
                            },
                            {
                                "op": "replace",
                                "path": "/description",
                                "oldValue": "Description for furnished object",
                                "newValue": ""
                            }
                        ]
                    }
                ]
            }
        },
        "importReplacementMap": {
            "https://ns.adobe.com/sandboxtoolingstage/mixins/9fad8b185640a2db7daf9bb1295543ee8cb5965d80a21e8d": "https://ns.adobe.com/sandboxtoolingstage/mixins/b7fa3024777ef11b68c5121e937d8543677093f4f0e63a5f",
            "5a45f8cd309d5ed5797be9a0af65e89152a51d57a6c74b52": "4ae041fa182d6faf2e7c56463399170d913138a7c5712909",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/b2b7705e770a35341b8bc5ec5e3644d9c7387266777fe4ba": "https://ns.adobe.com/sandboxtoolingstage/schemas/838c4e21ad81543ac14238ac1756012f7f98f0e0bec6b425",
            "https://ns.adobe.com/sandboxtoolingstage/schemas/355f461cbfb662fd0d12d06aeab34e206efcfa5d913604de": "https://ns.adobe.com/sandboxtoolingstage/schemas/9a55692d527169d0239e126137a694ed9db2406c9bcbd06a",
            "8f45c79235c91e7f0c09af676a77d170a34b5ee0ad5de72c": "65d755cc3300674c3cfcec620c59876af07f046884afd359",
            "f04b8e461396ff426f8ba8dc5544f799bf287baa8e0fa5c": "b6fa821ada8cb97cac384f0b0354bbe74209ec97fb6a83a3",
            "https://ns.adobe.com/sandboxtoolingstage/mixins/304ac900943716c8bd99e6aaf6aa840aac91995729f1987f": "https://ns.adobe.com/sandboxtoolingstage/mixins/34c9add91cce4a40d68a0e715c9f0a16048871734f8c8b74",
            "c8304f3cb7986e8c9b613cd8d832125bd867fb4a5aedf67a": "4d21e9bf89ce0042b52d7d41ff177a7697d695e2617d1fc1"
        },
        "schemaFieldMappings": null
    }
}
```

+++

+++응답 보기(새로 제출된 작업)

```json
{
    "status": "OK",
    "type": "SUCCESS",
    "ajo": false,
    "message": "Job with ID: {JOB_ID}",
    "object": {
        "id": "aa5cfacf35a8478c8cf44a675fab1c30 ",
        "name": "Compute Job Package: {SNAPSHOT_ID}",
        "description": null,
        "visibility": "TENANT",
        "requestType": "VERSION",
        "expiry": 0,
        "snapshotId": "{SNAPSHOT_ID}",
        "packageVersion": 0,
        "createdTimestamp": 0,
        "modifiedTimestamp": 0,
        "type": "PARTIAL",
        "jobStatus": "IN_PROGRESS",
        "jobType": "COMPUTE",
        "counter": 0,
        "imsOrgId": "{ORG_ID}",
        "sourceSandbox": {
            "name": "prod",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "destinationSandbox": {
            "name": "amanda-1",
            "imsOrgId": "{ORG_ID}",
            "empty": false
        },
        "schemaFieldMappings": null
    }
}
```

+++

### 패키지 버전 업데이트(#package-versioning)

패키지 ID를 제공하여 `/packages/{packageId}/version/save` 끝점에 GET 요청을 수행하여 각 개체에 대해 소스 샌드박스의 최신 스냅숏을 사용하여 패키지를 새 버전으로 업그레이드합니다.

***API 형식***

```http
PATCH /packages/{packageId}/version/save
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `packageId` | 패키지의 ID입니다. | 문자열 | 예 |

**요청**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/version/save/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**응답**

성공적인 응답은 버전 업그레이드에 대한 작업 상태를 반환합니다.

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Version Job Package: {JOB_ID}",
    "description": null,
    "visibility": "TENANT",
    "requestType": "VERSION",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPGRADE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### 패키지 버전 내역 검색(#package-version-history)

`/packages/{packageId}/history` 끝점에 GET 요청을 하고 패키지 ID를 제공하여 타임스탬프 및 수정자를 포함한 패키지의 버전 관리 기록을 검색합니다.

***API 형식***

```http
PATCH /packages/{packageId}/history
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `packageId` | 패키지의 ID입니다. | 문자열 | 예 |

**요청**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/history/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**응답**

성공적인 응답은 패키지의 버전 내역을 반환합니다.

```json
[
    {
        "id": "cb68591a1ed941e191e7f52e33637a26",
        "version": 0,
        "createdDate": 1739516784000,
        "modifiedDate": 1739516784000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 3
    },
    {
        "id": "e26189e6e4df476bb66c3fc3e66a1499",
        "version": 0,
        "createdDate": 1739343268000,
        "modifiedDate": 1739343268000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 2
    },
    {
        "id": "11af34c0eee449ac84ef28c66d9383e3",
        "version": 0,
        "createdDate": 1739343073000,
        "modifiedDate": 1739343073000,
        "createdBy": "{CREATED_BY}",
        "modifiedBy": "{MODIFIED_BY}",
        "imsOrgId": "{ORG_ID}",
        "packageVersion": 1
    }
]
```

### 업데이트 작업 제출(#submit-update)

패키지 ID를 제공하여 `/packages/{packageId}/import` 끝점에 대한 PATCH 요청을 수행하여 새 업데이트를 대상 샌드박스 개체에 푸시합니다.

***API 형식***

```http
PATCH /packages/{packageId}/import
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `packageId` | 패키지의 ID입니다. | 문자열 | 예 |

**요청**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}/import/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
      "id": "50fd94f8072b4f248737a2b57b41058f",
      "name": "Test Update",
      "destinationSandbox": {
        "name": "test-sandbox-sbt",
        "imsOrgId": "{ORG_ID}"
      },
      "overwriteMappings": {
        "https://ns.adobe.com/sandboxtoolingstage/schemas/327a48c83a5359f8160420a00d5a07f0ba8631a1fd466f9e" : {
            "id" : "https://ns.adobe.com/sandboxtoolingstage/schemas/e346bb2cd7b26576cb51920d214aebbd42940a9bf94a75cd",
            "type" : "REGISTRY_SCHEMA"
        }
      }
  }'
```

**응답**

성공적인 응답은 업데이트에 대한 작업 ID를 반환합니다.

```json
{
    "id": "3cec9bae662e43d9b9106fcbf7744a75",
    "name": "Update Job Name",
    "description": "Update Job Description",
    "visibility": "TENANT",
    "requestType": "IMPORT",
    "expiry": 0,
    "snapshotId": "{SNAPSHOT_ID}",
    "packageVersion": 2,
    "createdTimestamp": 0,
    "modifiedTimestamp": 0,
    "type": "PARTIAL",
    "jobStatus": "PENDING",
    "jobType": "UPDATE",
    "counter": 0,
    "imsOrgId": "{ORG_ID}",
    "sourceSandbox": {
        "name": "prod",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "destinationSandbox": {
        "name": "amanda-1",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "schemaFieldMappings": null
}
```

### 업데이트 및 패키지 재정의 비활성화(#disable-update)

패키지 ID를 제공하여 `/packages/{packageId}/?{QUERY_PARAMS}` 끝점에 대한 GET 요청을 수행하여 업데이트가 지원되지 않는 패키지에 대한 업데이트 및 재정의를 비활성화합니다.

***API 형식***

```http
PATCH /packages/{packageId}?{QUERY_PARAMS}
```

| 속성 | 설명 | 유형 | 필수 여부 |
| --- | --- | --- | --- |
| `packageId` | 패키지의 ID입니다. | 문자열 | 예 |
| {QUERY_PARAM} | getCapabilites 쿼리 매개 변수. `true` 또는 `false`(으)로 설정해야 합니다. | 부울 | 예 |

**요청**

```shell
curl -X POST \
  https://platform-stage.adobe.io/data/foundation/exim/packages/{PACKAGE_ID}?getCapabilities=true'/ \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Accept: application/json' \
  -H 'Content-Type: application/json' \
```

**응답**

성공적인 응답은 패키지의 기능 목록을 반환합니다.

```json
{
    "id": "80230dde96574a828191144709bb9b51",
    "version": 3,
    "createdDate": 1749808582000,
    "modifiedDate": 1749808648000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "name": "Ankit_Primary_Descriptor_Test",
    "description": "RestPackage",
    "imsOrgId": "{ORG_ID}",
    "clientId": "usecasebuilder",
    "packageType": "PARTIAL",
    "expiry": 1757584598000,
    "publishDate": 1749808648000,
    "status": "PUBLISHED",
    "packageVisibility": "PRIVATE",
    "latestPackageVersion": 0,
    "packageAccessType": "TENANT",
    "artifactsList": [
        {
            "id": "https://ns.adobe.com/sandboxtoolingstage/schemas/1c767056056de64d8030380d1b9f570d26bc15501a1e0e95",
            "altId": null,
            "type": "REGISTRY_SCHEMA",
            "found": false,
            "count": 0
        }
    ],
    "schemaMapping": {},
    "sourceSandbox": {
        "name": "atul-sandbox",
        "imsOrgId": "{ORG_ID}",
        "empty": false
    },
    "packageCapabilities": {
        "capabilities": [
            "VERSIONABLE"
        ]
    }
}
```
