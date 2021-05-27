---
keywords: Experience Platform;홈;인기 항목;샌드박스 개발자 안내서
solution: Experience Platform
title: 샌드박스 관리 API 끝점
topic-legacy: developer guide
description: 샌드박스 API의 /sandboxes 종단점을 사용하면 Adobe Experience Platform에서 샌드박스를 프로그래밍 방식으로 관리할 수 있습니다.
source-git-commit: f84898a87a8a86783220af7f74e17f464a780918
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 2%

---

# 샌드박스 관리 끝점

Adobe Experience Platform의 샌드박스는 프로덕션 환경에 영향을 주지 않고 기능을 테스트하고, 실험을 실행하고, 사용자 지정 구성을 만들 수 있는 분리된 개발 환경을 제공합니다. [!DNL Sandbox] API의 `/sandboxes` 종단점을 사용하면 Platform의 샌드박스를 프로그래밍 방식으로 관리할 수 있습니다.

## 시작하기

이 안내서에 사용된 API 엔드포인트는 [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml)의 일부입니다. 계속하기 전에 [시작 안내서](./getting-started.md)에서 관련 설명서에 대한 링크, 이 문서에서 샘플 API 호출을 읽는 방법에 대한 안내서, 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보를 검토하십시오.

## 샌드박스 목록 검색 {#list}

`/sandboxes` 종단점에 GET 요청을 하여 IMS 조직에 속하는 모든 샌드박스(활성 또는 기타 다른 항목)를 나열할 수 있습니다.

**API 형식**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 결과를 기준으로 필터링할 선택적 쿼리 매개 변수입니다. 자세한 내용은 [쿼리 매개 변수](./appendix.md#query)의 섹션을 참조하십시오. |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적으로 응답하면 `name`, `title`, `state` 및 `type` 등의 세부 정보를 포함하여 조직에 속하는 샌드박스 목록이 반환됩니다.

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
| `name` | 샌드박스의 이름입니다. 이 속성은 API 호출에서 조회 용도로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다.<br/><ul><li>`creating`:샌드박스가 생성되었지만 시스템에서 계속 프로비저닝되고 있습니다.</li><li>`active`:샌드박스가 만들어지고 활성 상태가 됩니다.</li><li>`failed`:오류로 인해 샌드박스를 시스템에서 프로비저닝할 수 없으며 비활성화되어 있습니다.</li><li>`deleted`:샌드박스를 수동으로 비활성화했습니다.</li></ul> |
| `type` | 샌드박스 유형입니다. 현재 지원되는 샌드박스 유형은 `development` 및 `production`입니다. |
| `isDefault` | 이 샌드박스가 조직의 기본 프로덕션 샌드박스인지 여부를 나타내는 부울 속성입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자입니다. 버전 제어 및 캐싱 효율에 사용되는 경우 샌드박스를 변경할 때마다 이 값이 업데이트됩니다. |

## 샌드박스 찾기 {#lookup}

요청 경로에 샌드박스의 `name` 속성을 포함하는 GET 요청을 만들어 개별 샌드박스를 찾을 수 있습니다.

**API 형식**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 조회할 샌드박스의 `name` 속성. |

**요청**

다음 요청은 &quot;dev-2&quot;라는 샌드박스를 검색합니다.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**응답**

성공적으로 응답하면 `name`, `title`, `state` 및 `type`를 포함하여 샌드박스의 세부 정보가 반환됩니다.

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
| `name` | 샌드박스의 이름입니다. 이 속성은 API 호출에서 조회 용도로 사용됩니다. |
| `title` | 샌드박스의 표시 이름입니다. |
| `state` | 샌드박스의 현재 처리 상태입니다. 샌드박스의 상태는 다음 중 하나일 수 있습니다. <ul><li>**만들기**:샌드박스가 생성되었지만 시스템에서 계속 프로비저닝되고 있습니다.</li><li>**활성**:샌드박스가 만들어지고 활성 상태가 됩니다.</li><li>**실패**:오류로 인해 샌드박스를 시스템에서 프로비저닝할 수 없으며 비활성화되어 있습니다.</li><li>**삭제됨**:샌드박스를 수동으로 비활성화했습니다.</li></ul> |
| `type` | 샌드박스 유형입니다. 현재 지원되는 샌드박스 유형은 다음과 같습니다.`development` 및 `production` |
| `isDefault` | 이 샌드박스가 조직의 기본 샌드박스인지 여부를 나타내는 부울 속성입니다. 일반적으로 프로덕션 샌드박스입니다. |
| `eTag` | 샌드박스의 특정 버전에 대한 식별자입니다. 버전 제어 및 캐싱 효율에 사용되는 경우 샌드박스를 변경할 때마다 이 값이 업데이트됩니다. |

## 샌드박스 만들기 {#create}

`/sandboxes` 종단점에 POST 요청을 하여 새 개발 또는 프로덕션 샌드박스를 만들 수 있습니다.

### 개발 샌드박스 만들기

개발 샌드박스를 만들려면 요청 페이로드에서 `development` 값이 있는 `type` 속성을 제공해야 합니다.

**API 형식**

```http
POST /sandboxes
```

**요청**

다음 요청은 &quot;acme-dev&quot;라는 새 개발 샌드박스를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `name` | 향후 요청에서 샌드박스에 액세스하는 데 사용할 식별자입니다. 이 값은 고유해야 하며, 가장 좋은 방법은 이 값을 가능한 설명적으로 만드는 것입니다. 이 값은 공백이나 특수 문자를 포함할 수 없습니다. |
| `title` | Platform 사용자 인터페이스에서 표시 목적으로 사용되는 사람이 읽을 수 있는 이름입니다. |
| `type` | 만들 샌드박스 유형입니다. 비프로덕션 샌드박스의 경우 이 값은 `development`이어야 합니다. |

**응답**

성공적으로 응답하면 새로 만든 샌드박스의 세부 정보가 반환되고 그 `state`이 &quot;생성 중&quot;임을 알 수 있습니다.

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
>샌드박스는 시스템에서 프로비전되는 데 약 30초 정도 걸리며 그 이후에는 `state`이 &quot;active&quot; 또는 &quot;failed&quot;가 됩니다.

### 프로덕션 샌드박스 만들기

프로덕션 샌드박스를 만들려면 요청 페이로드에서 `production` 값이 있는 `type` 속성을 제공해야 합니다.

**API 형식**

```http
POST /sandboxes
```

**요청**

다음 요청은 &quot;acme&quot;라는 새 프로덕션 샌드박스를 만듭니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | 향후 요청에서 샌드박스에 액세스하는 데 사용할 식별자입니다. 이 값은 고유해야 하며, 가장 좋은 방법은 이 값을 가능한 설명적으로 만드는 것입니다. 이 값은 공백이나 특수 문자를 포함할 수 없습니다. |
| `title` | Platform 사용자 인터페이스에서 표시 목적으로 사용되는 사람이 읽을 수 있는 이름입니다. |
| `type` | 만들 샌드박스 유형입니다. 프로덕션 샌드박스의 경우 이 값은 `production`이어야 합니다. |

**응답**

성공적으로 응답하면 새로 만든 샌드박스의 세부 정보가 반환되고 그 `state`이 &quot;생성 중&quot;임을 알 수 있습니다.

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
>샌드박스는 시스템에서 프로비전되는 데 약 30초 정도 걸리며 그 이후에는 `state`이 &quot;active&quot; 또는 &quot;failed&quot;가 됩니다.

## 샌드박스 업데이트 {#put}

요청 경로에서 샌드박스의 `name` 을 포함하는 PATCH 요청을 만들고 요청 페이로드에서 업데이트할 속성을 만들어 샌드박스에서 하나 이상의 필드를 업데이트할 수 있습니다.

>[!NOTE]
>
>현재 샌드박스의 `title` 속성만 업데이트할 수 있습니다.

**API 형식**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 업데이트할 샌드박스의 `name` 속성. |

**요청**

다음 요청은 &quot;acme&quot;라는 샌드박스의 `title` 속성을 업데이트합니다.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**응답**

성공적인 응답은 새로 업데이트된 샌드박스의 세부 정보와 함께 HTTP 상태 200(OK)을 반환합니다.

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

>[!IMPORTANT]
>
>내에 호스팅된 ID 그래프가 [Cross Device Analytics(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 기능에도 Adobe Analytics에서 사용되고 있거나 이 내에 호스팅된 ID 그래프가 [사람 기반 대상(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 기능에도 Adobe Audience Manager에서 사용되고 있는 경우에는 기본 프로덕션 샌드박스를 재설정할 수 없습니다.

개발 샌드박스에는 샌드박스에서 기본이 아닌 모든 리소스를 삭제하는 &quot;공장 재설정&quot; 기능이 있습니다. 요청 경로에 샌드박스의 `name`을 포함하는 PUT 요청을 만들어 샌드박스를 재설정할 수 있습니다.

**API 형식**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 재설정할 샌드박스의 `name` 속성. |

**요청**

다음 요청은 &quot;acme-dev&quot;라는 샌드박스를 재설정합니다.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| 속성 | 설명 |
| --- | --- |
| `action` | 샌드박스를 재설정하려면 이 매개 변수를 &quot;reset&quot; 값과 함께 요청 페이로드에서 제공해야 합니다. |

**응답**

성공적으로 응답하면 업데이트된 샌드박스의 세부 정보가 반환되고, 해당 `state`이 &quot;재설정&quot;임을 표시합니다.

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

>[!NOTE]
>
>샌드박스가 재설정되면 시스템이 프로비저닝하는 데 약 30초가 소요됩니다. 제공된 경우 샌드박스의 `state`은 &quot;활성&quot; 또는 &quot;실패&quot;가 됩니다.

다음 표에는 샌드박스가 재설정되지 않는 가능한 예외가 포함되어 있습니다.

| 오류 코드 | 설명 |
| --- | --- |
| `2074-400` | 이 샌드박스에 호스팅된 ID 그래프도 CDA(Cross Device Analytics) 기능에 Adobe Analytics에서 사용되기 때문에 이 샌드박스를 재설정할 수 없습니다. |
| `2075-400` | 이 샌드박스에서 호스팅된 ID 그래프도 Adobe Audience Manager에서 PBD(사람 기반 대상) 기능에 사용되고 있으므로 이 샌드박스를 재설정할 수 없습니다. |
| `2076-400` | 이 샌드박스에 호스팅된 ID 그래프도 PBD(People Based Destinations) 기능에 Adobe Audience Manager에서 사용하고 CDA(Cross Device Analytics) 기능용 Adobe Analytics에서도 사용되기 때문에 이 샌드박스를 재설정할 수 없습니다. |
| `2077-400` | 경고:샌드박스 `{SANDBOX_NAME}`는 Adobe Audience Manager 또는 Audience Core Service와 양방향 세그먼트 공유에 사용됩니다. |

## 샌드박스 삭제 {#delete}

>[!IMPORTANT]
>
>기본 프로덕션 샌드박스는 삭제할 수 없습니다.

요청 경로에서 샌드박스의 `name`을 포함하는 DELETE 요청을 만들어 샌드박스를 삭제할 수 있습니다.

>[!NOTE]
>
>이 API를 호출하면 샌드박스의 `status` 속성이 &quot;삭제됨&quot;으로 업데이트되고 비활성화됩니다. GET 요청은 삭제된 후에도 샌드박스의 세부 사항을 검색할 수 있습니다.

**API 형식**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{SANDBOX_NAME}` | 삭제할 샌드박스의 `name` |

**요청**

다음 요청은 &quot;acme-dev&quot;라는 샌드박스를 삭제합니다.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**응답**

성공적인 응답은 샌드박스의 업데이트된 세부 정보를 반환하여 `state`이 &quot;삭제됨&quot;임을 표시합니다.

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
