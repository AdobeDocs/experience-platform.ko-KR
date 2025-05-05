---
keywords: Experience Platform;홈;인기 항목;샌드박스 개발자 안내서
solution: Experience Platform
title: 샌드박스 관리 API 엔드포인트
description: 샌드박스 API의 /sandboxes 끝점을 사용하면 Adobe Experience Platform에서 샌드박스를 프로그래밍 방식으로 관리할 수 있습니다.
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 3%

---

# 샌드박스 관리 엔드포인트

Adobe Experience Platform의 샌드박스는 프로덕션 환경에 영향을 주지 않고 기능을 테스트하고 실험을 실행하며 사용자 지정 구성을 만들 수 있는 격리된 개발 환경을 제공합니다. [!DNL Sandbox] API의 `/sandboxes` 끝점을 사용하면 Experience Platform에서 샌드박스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 가이드에 사용된 API 끝점은 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)를 검토하여 관련 문서에 대한 링크, 이 문서의 샘플 API 호출 읽기 지침 및 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요 정보를 확인하십시오.

## 샌드박스 목록 검색 {#list}

`/sandboxes` 끝점에 GET 요청을 하여 조직에 속한 모든 샌드박스(활성 또는 기타)를 나열할 수 있습니다.

**API 형식**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 결과를 필터링 기준으로 사용할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](./appendix.md#query)의 섹션을 참조하십시오. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

응답이 성공하면 `name`, `title`, `state` 및 `type`과(와) 같은 세부 정보를 포함하여 조직에 속한 샌드박스 목록이 반환됩니다.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| 속성 | 설명 |
| --- | --- |
| `name` | 샌드박스의 이름. 이 속성은 API 호출에서 조회 목적으로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <br/><ul><li>`creating`: 샌드박스가 만들어졌지만 시스템에 의해 아직 프로비저닝되고 있습니다.</li><li>`active`: 샌드박스가 만들어지고 활성 상태입니다.</li><li>`failed`: 오류로 인해 시스템에서 샌드박스를 프로비저닝할 수 없어 샌드박스가 비활성화되었습니다.</li><li>`deleted`: 샌드박스를 수동으로 사용하지 않도록 설정했습니다.</li></ul> |
| `type` | 샌드박스 유형. 현재 지원되는 샌드박스 유형은 `development` 및 `production`입니다. |
| `isDefault` | 이 샌드박스가 조직의 기본 프로덕션 샌드박스인지 여부를 나타내는 부울 속성. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자. 버전 제어 및 캐싱 효율성에 사용되며 이 값은 샌드박스가 변경될 때마다 업데이트됩니다. |

## 샌드박스 조회 {#lookup}

요청 경로에 샌드박스의 `name` 속성이 포함된 GET 요청을 만들어 개별 샌드박스를 조회할 수 있습니다.

**API 형식**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 조회할 샌드박스의 `name` 속성입니다. |

**요청**

다음 요청은 &quot;dev-2&quot;라는 샌드박스를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**응답**

성공한 응답은 `name`, `title`, `state` 및 `type`을(를) 포함하여 샌드박스의 세부 정보를 반환합니다.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| 속성 | 설명 |
| --- | --- |
| `name` | 샌드박스의 이름. 이 속성은 API 호출에서 조회 목적으로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <ul><li>**만들기**: 샌드박스가 만들어졌지만 시스템에 의해 아직 프로비저닝되고 있습니다.</li><li>**활성**: 샌드박스가 만들어지고 활성 상태입니다.</li><li>**실패**: 오류로 인해 시스템에서 샌드박스를 프로비저닝할 수 없으며 비활성화되었습니다.</li><li>**삭제됨**: 샌드박스가 수동으로 비활성화되었습니다.</li></ul> |
| `type` | 샌드박스 유형. 현재 지원되는 샌드박스 유형은 `development` 및 `production`입니다. |
| `isDefault` | 이 샌드박스가 조직의 기본 샌드박스인지 여부를 나타내는 부울 속성. 일반적으로 프로덕션 샌드박스입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자. 버전 제어 및 캐싱 효율성에 사용되며 이 값은 샌드박스가 변경될 때마다 업데이트됩니다. |

## 샌드박스 만들기 {#create}

>[!NOTE]
>
>새 샌드박스가 만들어지면 새 샌드박스 사용을 시작하려면 먼저 [Adobe Admin Console](https://adminconsole.adobe.com/)에서 제품 프로필에 새 샌드박스를 추가해야 합니다. 제품 프로필에 샌드박스를 프로비저닝하는 방법에 대한 자세한 내용은 [제품 프로필에 대한 권한 관리](../../access-control/ui/permissions.md)에 대한 설명서를 참조하십시오.

`/sandboxes` 끝점에 대한 POST 요청을 만들어 새 개발 또는 프로덕션 샌드박스를 만들 수 있습니다.

### 개발 샌드박스 만들기

개발 샌드박스를 만들려면 요청 페이로드에 `development` 값이 있는 `type` 특성을 제공해야 합니다.

**API 형식**

```http
POST /sandboxes
```

**요청**

다음 요청은 &quot;acme-dev&quot;라는 새 개발 샌드박스를 생성합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 향후 요청에서 샌드박스에 액세스하는 데 사용할 식별자. 이 값은 고유해야 하며 가능한 한 수사적으로 만드는 것이 좋습니다. 이 값에는 공백이나 특수 문자를 사용할 수 없습니다. |
| `title` | Experience Platform 사용자 인터페이스에서 표시 목적으로 사용되는 사람이 인식할 수 있는 이름. |
| `type` | 만들 샌드박스 유형입니다. 비프로덕션 샌드박스의 경우 이 값은 `development`이어야 합니다. |

**응답**

성공한 응답은 새로 만든 샌드박스의 세부 정보를 반환하며 해당 `state`이(가) &quot;만들기&quot; 중임을 표시합니다.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>샌드박스는 시스템에서 프로비저닝되는 데 약 30초가 걸리고 그 후 `state`이(가) &quot;활성&quot; 또는 &quot;실패&quot;됩니다.

### 프로덕션 샌드박스 만들기

프로덕션 샌드박스를 만들려면 요청 페이로드에 `production` 값이 있는 `type` 특성을 제공해야 합니다.

**API 형식**

```http
POST /sandboxes
```

**요청**

다음 요청은 &quot;acme&quot;라는 새 프로덕션 샌드박스를 생성합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 향후 요청에서 샌드박스에 액세스하는 데 사용할 식별자. 이 값은 고유해야 하며 가능한 한 수사적으로 만드는 것이 좋습니다. 이 값에는 공백이나 특수 문자를 사용할 수 없습니다. |
| `title` | Experience Platform 사용자 인터페이스에서 표시 목적으로 사용되는 사람이 인식할 수 있는 이름. |
| `type` | 만들 샌드박스 유형입니다. 프로덕션 샌드박스의 경우 이 값은 `production`이어야 합니다. |

**응답**

성공한 응답은 새로 만든 샌드박스의 세부 정보를 반환하며 해당 `state`이(가) &quot;만들기&quot; 중임을 표시합니다.

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>샌드박스는 시스템에서 프로비저닝되는 데 약 30초가 걸리고 그 후 `state`이(가) &quot;활성&quot; 또는 &quot;실패&quot;됩니다.

## 샌드박스 업데이트 {#put}

요청 경로에 샌드박스의 `name`이(가) 포함된 PATCH 요청과 요청 페이로드에서 업데이트할 속성을 만들어 샌드박스에 있는 하나 이상의 필드를 업데이트할 수 있습니다.

>[!NOTE]
>
>현재 샌드박스의 `title` 속성만 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 업데이트할 샌드박스의 `name` 속성입니다. |

**요청**

다음 요청은 &quot;acme&quot;라는 샌드박스의 `title` 속성을 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**응답**

성공한 응답은 새로 업데이트된 샌드박스의 세부 정보와 함께 HTTP 상태 200(OK)을 반환합니다.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## 샌드박스 재설정 {#reset}

샌드박스에는 샌드박스에서 기본값이 아닌 모든 리소스를 삭제하는 &quot;공장 재설정&quot; 기능이 있습니다. 요청 경로에 샌드박스의 `name`을(를) 포함하는 PUT 요청을 만들어 샌드박스를 재설정할 수 있습니다.

**API 형식**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 재설정할 샌드박스의 `name` 속성입니다. |
| `validationOnly` | 실제 요청을 하지 않고 샌드박스 재설정 작업에 대해 사전 확인을 수행할 수 있는 선택적 매개 변수입니다. 이 매개 변수를 `validationOnly=true`(으)로 설정하여 재설정하려는 샌드박스에 Adobe Analytics, Adobe Audience Manager 또는 세그먼트 공유 데이터가 포함되어 있는지 확인합니다. |

**요청**

다음 요청은 &quot;acme-dev&quot;라는 샌드박스를 재설정합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `action` | 샌드박스를 재설정하려면 이 매개 변수를 &quot;reset&quot; 값으로 요청 페이로드에 제공해야 합니다. |

**응답**

>[!NOTE]
>
>샌드박스가 재설정되면 시스템에서 프로비저닝하는 데 약 30초가 소요됩니다.

성공한 응답은 업데이트된 샌드박스의 세부 정보를 반환하며 해당 `state`이(가) &quot;재설정 중&quot;임을 표시합니다.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

Adobe Analytics Adobe Audience Manager 기본 프로덕션 샌드박스와 사용자가 만든 모든 프로덕션 샌드박스는 ID 그래프 내에서 호스팅되는 것이 [CDA(Cross Device Analytics)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=ko) 기능에도 사용되는 경우 또는 ID 그래프 내에서 호스팅되는 것이 [PBD(People Based Destinations)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=ko) 기능에도 사용되는 경우 재설정할 수 없습니다.

다음은 샌드박스가 재설정되지 않도록 할 수 있는 가능한 예외 목록입니다.

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

`ignoreWarnings` 매개 변수를 요청에 추가하여 [!DNL Audience Manager] 또는 [!DNL Audience Core Service]과(와) 공유하는 양방향 세그먼트에 사용되는 프로덕션 샌드박스를 재설정할 수 있습니다.

**API 형식**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 매개변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 재설정할 샌드박스의 `name` 속성입니다. |
| `ignoreWarnings` | 유효성 검사를 건너뛰고 [!DNL Audience Manager] 또는 [!DNL Audience Core Service]과(와) 공유하는 양방향 세그먼트에 사용되는 프로덕션 샌드박스를 강제로 다시 설정할 수 있는 선택적 매개 변수입니다. 이 매개 변수는 기본 프로덕션 샌드박스에 적용할 수 없습니다. |

**요청**

다음 요청은 &quot;acme&quot;라는 프로덕션 샌드박스를 재설정합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**응답**

성공한 응답은 업데이트된 샌드박스의 세부 정보를 반환하며 해당 `state`이(가) &quot;재설정 중&quot;임을 표시합니다.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## 샌드박스 삭제 {#delete}

>[!IMPORTANT]
>
>기본 프로덕션 샌드박스를 삭제할 수 없습니다.

요청 경로에 샌드박스의 `name`을(를) 포함하는 DELETE 요청을 만들어 샌드박스를 삭제할 수 있습니다.

>[!NOTE]
>
>이 API 호출을 수행하면 샌드박스의 `status` 속성이 &quot;삭제됨&quot;으로 업데이트되고 비활성화됩니다. GET 요청은 삭제된 후에도 샌드박스의 세부 정보를 검색할 수 있습니다.

**API 형식**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 매개변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 삭제할 샌드박스의 `name`입니다. |
| `validationOnly` | 실제 요청을 하지 않고 샌드박스 삭제 작업에 대해 사전 확인을 수행할 수 있는 선택적 매개 변수입니다. 이 매개 변수를 `validationOnly=true`(으)로 설정하여 재설정하려는 샌드박스에 Adobe Analytics, Adobe Audience Manager 또는 세그먼트 공유 데이터가 포함되어 있는지 확인합니다. |
| `ignoreWarnings` | 유효성 검사를 건너뛰고 [!DNL Audience Manager] 또는 [!DNL Audience Core Service]과(와) 공유하는 양방향 세그먼트에 사용되는 사용자가 만든 프로덕션 샌드박스를 강제로 삭제할 수 있는 선택적 매개 변수입니다. 이 매개 변수는 기본 프로덕션 샌드박스에 적용할 수 없습니다. |

**요청**

다음 요청은 &quot;acme&quot;라는 프로덕션 샌드박스를 삭제합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**응답**

성공한 응답이 샌드박스의 업데이트된 세부 정보를 반환하여 해당 `state`이(가) &quot;삭제됨&quot;임을 표시합니다.

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
