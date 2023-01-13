---
title: 데이터 위생 API를 사용하여 레코드 삭제
description: Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
exl-id: d80a4be3-e072-4bb4-a56d-b34a20f88c78
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# 데이터 위생 API를 사용하여 레코드 삭제

<!-- >[!IMPORTANT]
>
>This endpoint represents the beta functionality for record deletes. For the latest functionality, please use the [`/workorder` endpoint](./workorder.md) instead. -->

데이터 위생 API를 사용하면 Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제할 수 있습니다.

와 동일한 루트 경로를 통해 API에 액세스할 수 있습니다 [Privacy Service API](../../privacy-service/api/overview.md): `https://platform.adobe.io/data/core/privacy/`

## 시작하기

이 섹션에서는 데이터 위생 API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.

### 필수 헤더에 대한 값을 수집합니다

데이터 위생 API를 호출하려면 먼저 인증 자격 증명을 수집해야 합니다. 이는 Privacy Service API에 액세스하는 데 사용되는 것과 동일한 자격 증명입니다. 자세한 내용은 [API 개요](./overview.md#getting-started) 데이터 위생 API에 필요한 각 헤더에 대한 값을 생성하려면 아래에 표시된 대로 다음을 수행합니다.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

### 샘플 API 호출 읽기

이 문서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 [예제 API 호출을 읽는 방법](../../landing/api-guide.md#sample-api) Experience Platform API에 대한 시작 안내서에서 를 참조하십시오.

## 삭제 작업 만들기

POST 요청을 수행하여 삭제 작업을 만들 수 있습니다.

**API 형식**

```http
POST /jobs
```

**요청**

요청 페이로드는 요청의 페이로드와 유사하게 구조화됩니다 [Privacy Service API에서 요청 삭제](../../privacy-service/api/privacy-jobs.md#access-delete). 여기에는 다음이 포함됩니다 `users` 객체를 사용하여 데이터를 삭제할 사용자를 나타내는 배열입니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{ORG_ID}"
          }
        ],
        "users": [
          {
            "key": "John Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "email",
                "value": "johnd@example.com",
                "type": "standard",
              },
              {
                "namespace": "ECID",
                "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
                "type": "standard"
              }
            ]
          },
          {
            "key": "Jane Doe",
            "action": [
              "delete"
            ],
            "userIDs": [
              {
                "namespace": "Loyalty ID",
                "value": "30583967185734",
                "type": "custom"
              }
            ]
          }
        ]
      }'
```

| 속성 | 설명 |
| --- | --- |
| `companyContexts` | 조직에 대한 인증 정보가 포함된 배열입니다. 여기에는 다음 속성을 갖는 단일 개체가 포함되어야 합니다. <ul><li>`namespace`: 을(를) 로 설정해야 합니다. `imsOrgID`.</li><li>`value`: IMS 조직 ID입니다. 이 값은 `x-gw-ims-org-id` 헤더.</li></ul> |
| `users` | 삭제할 정보가 있는 하나 이상의 사용자 컬렉션이 포함된 배열입니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`: 응답 데이터에서 개별 작업 ID를 평가하는 데 사용되는 사용자의 식별자입니다. 참조하거나 나중에 조회할 수 있도록 이 값에 대해 고유하고 쉽게 식별 가능한 문자열을 선택하는 것이 좋습니다.</li><li>`action`: 사용자의 데이터에 수행할 원하는 작업을 나열하는 배열입니다. 단일 문자열 값을 포함해야 합니다. `delete`.</li><li>`userIDs`: 사용자의 ID 컬렉션입니다. 한 사용자가 사용할 수 있는 ID의 수는 9개로 제한됩니다. 각 ID에는 다음 속성이 포함되어 있습니다. <ul><li>`namespace`: 다음 [id 네임스페이스](../../identity-service/namespaces.md) 를 ID와 연결된 경우에만 해당됩니다. 다음 항목을 지정할 수 있습니다. [표준 네임스페이스](../../privacy-service/api/appendix.md#standard-namespaces) 플랫폼에서 인식하거나 조직에서 정의한 사용자 정의 네임스페이스가 될 수 있습니다. 사용되는 네임스페이스 유형은 `type` 속성을 사용합니다.</li><li>`value`: ID 값입니다.</li><li>`type`: 을(를) 로 설정해야 합니다. `standard` 전역적으로 인식되는 네임스페이스를 사용하는 경우 또는 `custom` 조직에서 정의한 네임스페이스를 사용하는 경우.</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}

**응답**

성공적인 응답은 생성된 작업의 세부 정보를 반환합니다.

```json
{
  "requestId": "16318094870430026RX-334",
  "totalRecords": 2,
  "jobs": [
    {
      "jobId": "c9b5fd82-db14-4c27-8bec-64a06e1fbda4",
      "customer": {
        "user": {
          "key": "John Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "email",
              "value": "johnd@example.com",
              "type": "standard",
              "namespaceId": 6,
              "isDeletedClientSide": false
            },
            {
              "namespace": "ECID",
              "value": "9cbefef1-dd44-4411-87db-2d387bf882bc",
              "type": "standard",
              "namespaceId": 4,
              "isDeletedClientSide": false
            }
          ]
        }
      }
    },
    {
      "jobId": "8ddc8e73-cecc-4be3-ae44-cdba127f7c70",
      "customer": {
        "user": {
          "key": "Jane Doe",
          "action": ["delete"],
          "userIDs": [
            {
              "namespace": "Loyalty ID",
              "value": "30583967185734",
              "type": "custom",
              "isDeletedClientSide": false
            }
          ]
        }
      }
    }
  ]
}
```
