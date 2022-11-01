---
title: 할당량 API 끝점
description: 데이터 위생 API의 /quota 끝점을 사용하면 각 작업 유형에 대한 조직의 월별 할당량 제한에 대해 데이터 위생사용을 모니터링할 수 있습니다.
source-git-commit: 6453ec6c98d90566449edaa0804ada260ae12bf6
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# 할당량 끝점

>[!IMPORTANT]
>
>Adobe Experience Platform의 데이터 위생 기능은 현재 구입한 조직에만 사용할 수 있습니다 **Adobe 의료 보호** 또는 **Adobe 개인 정보 보호 및 보안 차단**.

다음 `/quota` data 위생 API의 종단점을 사용하면 각 작업 유형에 대한 조직의 할당량 제한에 대해 데이터 위생 사용을 모니터링할 수 있습니다.

할당량은 다음과 같은 방법으로 각 데이터 위생 작업 유형에 대해 적용됩니다.

* 소비자 삭제 및 필드 업데이트는 매달 특정 수의 요청으로 제한됩니다.
* 데이터 집합 만료는 만료가 실행될 시기에 관계없이 동시 활성 작업 수에 대한 제한이 있습니다.

## 시작하기

이 안내서에서 사용되는 엔드포인트는 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md) 을 참조하십시오.

* 관련 설명서에 대한 링크
* 이 문서에서 샘플 API 호출을 읽는 안내서
* 모든 Experience Platform API를 성공적으로 호출하는 데 필요한 필수 헤더에 대한 중요한 정보입니다

## 할당량 나열 {#list}

에 GET 요청을 수행하여 조직의 할당량 정보를 볼 수 있습니다 `/quota` 엔드포인트.

**API 형식**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

| 매개 변수 | 설명 |
| --- | --- |
| `{QUOTA_TYPE}` | 검색할 할당량 유형을 지정하는 선택적 쿼리 매개 변수입니다. 없는 경우 `quotaType` 매개 변수가 제공되면 모든 할당량 값이 API 응답으로 반환됩니다. 허용되는 유형 값은 다음과 같습니다.<ul><li>`expirationDatasetQuota`: 데이터 집합 만료</li><li>`deleteIdentityWorkOrderDatasetQuota`: 소비자 삭제</li><li>`fieldUpdateWorkOrderDatasetQuota`: 필드 업데이트</li></ul> |

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

성공적인 응답은 데이터 위생 할당량의 세부 정보를 반환합니다.

```json
{
  "quotas": [
    {
      "name": "expirationDatasetQuota",
      "description": "The number of concurrently active Expiration Dataset Delete Work Order requests for the organization.",
      "consumed": 3154,
      "quota": 10000
    },
    {
      "name": "deleteIdentityWorkOrderQuota",
      "description": "The number of Consumer Delete Work Order requests for the organization for this month.",
      "consumed": 390,
      "quota": 10000
    }
  ]
}
```

| 속성 | 설명 |
| --- | --- |
| `quotas` | 각 데이터 위생 작업 유형에 대한 할당량 정보를 나열합니다. 각 할당량 객체에는 다음 속성이 포함됩니다.<ul><li>`name`: 데이터 위생 작업 유형:<ul><li>`expirationDatasetQuota`: 데이터 집합 만료</li><li>`deleteIdentityWorkOrderDatasetQuota`: 소비자 삭제</li></ul></li><li>`description`: 데이터 위생 작업 유형에 대한 설명입니다.</li><li>`consumed`: 현재 월별 기간에 실행된 이 유형의 작업 수입니다.</li><li>`quota`: 이 작업 형식에 대한 할당량 제한입니다. 소비자 삭제 및 필드 업데이트의 경우 월별 기간마다 실행할 수 있는 작업 수를 나타냅니다. 데이터 세트 만료의 경우 지정된 시간에 동시에 활성화할 수 있는 작업 수를 나타냅니다.</li></ul> |

{style=&quot;table-layout:auto&quot;}
