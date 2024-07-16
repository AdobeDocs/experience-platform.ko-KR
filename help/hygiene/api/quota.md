---
title: 할당량 API 끝점
description: 데이터 위생 API의 /quota 끝점을 사용하면 각 작업 유형에 대한 조직의 월별 할당량 제한에 대해 고급 데이터 수명 주기 관리 사용을 모니터링할 수 있습니다.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 48a83e2b615fc9116a93611a5e6a8e7f78cb4dee
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---

# 할당량 끝점

데이터 위생 API의 `/quota` 끝점을 사용하면 각 작업 유형에 대한 조직의 할당량 제한에 대해 고급 데이터 수명 주기 관리 사용을 모니터링할 수 있습니다.

할당량은 다음과 같은 방법으로 각 데이터 라이프사이클 작업 유형에 적용됩니다.

* 레코드 삭제 및 업데이트는 매월 특정 수의 요청으로 제한됩니다.
* 데이터 세트 만료에는 만료를 실행할 시기에 관계없이 동시에 활성 상태인 작업 수에 대한 일정한 제한이 있습니다.

## 시작하기

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md)에서 다음 정보를 검토하십시오.

* 관련 설명서 링크
* 이 문서의 샘플 API 호출 읽기에 대한 안내서
* 모든 Experience Platform API를 호출하는 데 필요한 필수 헤더와 관련된 중요 정보

## 할당량 나열 {#list}

`/quota` 끝점에 대한 GET 요청을 수행하면 조직의 할당량 정보를 볼 수 있습니다.

**API 형식**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 매개변수 | 설명 |
| --- | --- |
| `{QUOTA_TYPE}` | 검색할 할당량의 유형을 지정하는 선택적 쿼리 매개 변수입니다. `quotaType` 매개 변수를 제공하지 않으면 모든 할당량 값이 API 응답에서 반환됩니다. 허용되는 유형 값은 다음과 같습니다.<ul><li>`datasetExpirationQuota`: 이 개체는 조직에 대해 동시에 활성화된 데이터 세트 만료 수와 만료의 총 허용량을 표시합니다. </li><li>`dailyConsumerDeleteIdentitiesQuota`: 이 개체는 조직에서 오늘 수행한 총 레코드 삭제 요청 수와 총 일별 허용량을 표시합니다.<br>참고: 수락된 요청만 계산됩니다. 작업 주문이 유효성 검사에 실패하여 거부된 경우 이러한 ID 삭제는 할당량에 포함되지 않습니다.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: 이 개체는 이번 달에 조직에서 수행한 총 레코드 삭제 요청 수와 총 월별 수당을 표시합니다.</li><li>`monthlyUpdatedFieldIdentitiesQuota`: 이 개체는 이번 달에 조직에서 수행한 총 레코드 업데이트 요청 수와 총 월별 수당을 표시합니다.</li></ul> |

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/quota \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
```

**응답**

성공적인 응답은 데이터 라이프사이클 할당량에 대한 세부 정보를 반환합니다.

```json
{
  "quotas": [
    {
      "name": "datasetExpirationQuota",
      "description": "The number of concurrently active Expiration Dataset Delete in all workorder requests for the organization.",
      "consumed": 12,
      "quota": 50
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for today.",
      "consumed": 0,
      "quota": 600000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all workorder requests for the organization for this month.",
      "consumed": 841,
      "quota": 600000
    },
    {
      "name": "monthlyUpdatedFieldIdentitiesQuota",
      "description": "The consumed number of updated identities in all workorder requests for the organization for this month.",
      "consumed": 0,
      "quota": 0
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `quotas` | 각 데이터 라이프사이클 작업 유형에 대한 할당량 정보를 나열합니다. 각 할당량 개체에는 다음 속성이 포함되어 있습니다.<ul><li>`name`: 데이터 주기 작업 유형:<ul><li>`expirationDatasetQuota`: 데이터 세트 만료</li><li>`deleteIdentityWorkOrderDatasetQuota`: 레코드 삭제</li></ul></li><li>`description`: 데이터 수명 주기 작업 유형에 대한 설명입니다.</li><li>`consumed`: 현재 기간에 실행된 이 형식의 작업 수입니다. 객체 이름은 할당량 기간을 나타냅니다.</li><li>`quota`: 조직의 이 작업 유형에 대한 할당입니다. 레코드 삭제 및 업데이트의 경우 할당량은 각 월별 기간에 대해 실행할 수 있는 작업 수를 나타냅니다. 데이터 세트 만료의 경우 할당량은 지정된 시간에 동시에 활성화할 수 있는 작업 수를 나타냅니다.</li></ul> |

{style="table-layout:auto"}
