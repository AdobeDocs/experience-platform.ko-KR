---
title: 데이터 위생 API(알파)
description: Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제하는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: dd8978566730975f0bde36f3af490cd33362b3ba
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 1%

---

# 데이터 위생 API(알파)

>[!IMPORTANT]
>
>데이터 위생 API는 현재 알파 상태이며 조직에서 아직 액세스할 수 없습니다. 이 문서에 설명된 기능은 변경될 수 있습니다.

데이터 위생 API를 사용하면 Adobe Experience Platform에서 고객의 저장된 개인 데이터를 프로그래밍 방식으로 수정하거나 삭제할 수 있습니다. Privacy Service API와 달리, 이러한 작업은 법적 개인 정보 보호 규정에 연결할 필요가 없으며 데이터를 깨끗하고 정확하게 유지하는 데 순전히 사용할 수 있습니다.

## 시작하기

이 섹션에서는 데이터 위생 API를 호출하기 전에 알아야 하는 핵심 개념을 소개합니다.

### 필수 헤더에 대한 값을 수집합니다

데이터 위생 API를 호출하려면 먼저 인증 자격 증명을 수집해야 합니다. 이는 Privacy Service API에 액세스하는 데 사용되는 것과 동일한 자격 증명입니다. 데이터 위생 API에 필요한 각 헤더에 대한 값을 생성하려면 Privacy Service API에 대한 [시작 안내서](./api/getting-started.md)를 따르십시오.

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

페이로드(POST, PUT, PATCH)이 포함된 모든 요청에는 추가 헤더가 필요합니다.

* `Content-Type: application/json`

### 샘플 API 호출 읽기

이 문서에서는 요청 형식을 지정하는 방법을 보여주는 예제 API 호출을 제공합니다. 샘플 API 호출에 대한 설명서에 사용된 규칙에 대한 자세한 내용은 Experience Platform API에 대한 시작 안내서에서 [예제 API 호출](../landing/api-guide.md#sample-api)를 읽는 방법 섹션을 참조하십시오.

## 삭제 작업 만들기

POST 요청을 수행하여 삭제 작업을 만들 수 있습니다.

**API 형식**

```http
POST /jobs
```

**요청**

요청 페이로드는 Privacy Service API](./api/privacy-jobs.md#access-delete)에서 [삭제 요청의 요청과 유사하게 구조화됩니다. 여기에는 데이터를 삭제할 사용자를 나타내는 `users` 배열이 포함되어 있습니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "companyContexts": [
          {
            "namespace": "imsOrgID",
            "value": "{IMS_ORG}"
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
| `companyContexts` | 조직에 대한 인증 정보가 포함된 배열입니다. 여기에는 다음 속성을 갖는 단일 개체가 포함되어야 합니다. <ul><li>`namespace`: 를 로 설정해야  `imsOrgID`합니다.</li><li>`value`: IMS 조직 ID입니다. 이 값은 `x-gw-ims-org-id` 헤더에 제공된 값과 동일합니다.</li></ul> |
| `users` | 삭제할 정보가 있는 하나 이상의 사용자 컬렉션이 포함된 배열입니다. 각 사용자 객체에는 다음 정보가 포함됩니다. <ul><li>`key`: 응답 데이터에서 개별 작업 ID를 평가하는 데 사용되는 사용자의 식별자입니다. 참조하거나 나중에 조회할 수 있도록 이 값에 대해 고유하고 쉽게 식별 가능한 문자열을 선택하는 것이 좋습니다.</li><li>`action`: 사용자의 데이터에 수행할 원하는 작업을 나열하는 배열입니다. 단일 문자열 값을 포함해야 합니다. `delete`</li><li>`userIDs`: 사용자의 ID 컬렉션입니다. 한 사용자가 사용할 수 있는 ID의 수는 9개로 제한됩니다. 각 ID에는 다음 속성이 포함되어 있습니다. <ul><li>`namespace`: ID [와 ](../identity-service/namespaces.md) 연결된 ID 이름 Platform에서 인식하는 [표준 네임스페이스](./api/appendix.md#standard-namespaces)이거나 조직에서 정의한 사용자 지정 네임스페이스일 수 있습니다. 사용된 네임스페이스 유형은 `type` 속성에 반영해야 합니다.</li><li>`value`: ID 값입니다.</li><li>`type`: 전역적으로 인식되는 네임스페이스를 사용하는  `standard` 경우, 또는 조직에서 정의한 네임스페이스를 사용하는  `custom` 경우 로 설정해야 합니다.</li></ul></li></ul> |

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
