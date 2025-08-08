---
title: 할당량 API 끝점
description: 데이터 위생 API의 /quota 끝점을 사용하면 각 작업 유형에 대한 조직의 월별 할당량 제한에 대해 고급 데이터 수명 주기 관리 사용을 모니터링할 수 있습니다.
role: Developer
exl-id: 91858a13-e5ce-4b36-a69c-9da9daf8cd66
source-git-commit: 2c2907c5ed38ce4c87b1b73f96e1a0e64586cb97
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 2%

---

# 할당량 끝점

데이터 위생 API의 `/quota` 끝점을 사용하여 조직의 현재 사용 및 제한을 확인하십시오. 할당량은 Privacy and Security Shield 또는 Healthcare Shield와 같은 권한에 따라 다릅니다.

현재 할당량 소비를 모니터링하여 각 작업 유형에 대한 조직의 제한을 준수합니다.

## 시작

이 안내서에 사용된 끝점은 데이터 위생 API의 일부입니다. 계속하기 전에 [개요](./overview.md)에서 다음 정보를 검토하십시오.

* 관련 설명서 링크
* 샘플 API 호출을 읽는 방법
* Experience Platform API 호출에 대한 필수 헤더

## 할당량 및 처리 타임라인 {#quotas}

레코드 삭제 요청은 라이선스 자격에 따라 할당량 및 서비스 수준 예상치를 따릅니다. 이러한 제한은 UI 및 API 기반 삭제 요청 모두에 적용됩니다.

>[!TIP]
>
>이 문서에서는 자격 기반 제한에 대해 사용량을 쿼리하는 방법을 보여 줍니다. 할당량 계층, 레코드 삭제 권한 및 SLA 동작에 대한 자세한 설명은 [UI 기반 레코드 삭제](../ui/record-delete.md#quotas) 또는 [API 기반 레코드 삭제](./workorder.md#quotas) 문서를 참조하십시오.

## 할당량 나열 {#list}

`/quota` 끝점에 대한 GET 요청을 수행하면 조직의 할당량 정보를 볼 수 있습니다.

**API 형식**

```http
GET /quota
GET /quota?quotaType={QUOTA_TYPE}
```

>[!NOTE]
>
>할당량 소비는 매월 1일 00:00 GMT에 일별 및 월별로 재설정됩니다.
>
>수락된 요청만 할당량에 포함됩니다. 거부된 작업 주문은 할당량을 감소시키지 않습니다.

| 매개변수 | 설명 |
| --- | --- |
| `{QUOTA_TYPE}` | 검색할 할당량의 유형을 지정하는 선택적 쿼리 매개 변수입니다. `quotaType` 매개 변수를 제공하지 않으면 모든 할당량 값이 API 응답에서 반환됩니다. 허용되는 값은 다음과 같습니다.<ul><li>`datasetExpirationQuota`: 활성 데이터 세트 만료 수 및 총 허용량입니다.</li><li>`dailyConsumerDeleteIdentitiesQuota`: 오늘 삭제된 레코드 수와 일일 할당량입니다.</li><li>`monthlyConsumerDeleteIdentitiesQuota`: 이번 달에 삭제된 레코드 수와 월별 할당량입니다.</li></ul> |

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
      "description": "The number of concurrently active dataset-expiration delete operations in all work order requests for the organization.",
      "consumed": 11,
      "quota": 75
    },
    {
      "name": "dailyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization for today.",
      "consumed": 314,
      "quota": 700000
    },
    {
      "name": "monthlyConsumerDeleteIdentitiesQuota",
      "description": "The consumed number of deleted identities in all work order requests for the organization this month.",
      "consumed": 2764,
      "quota": 12000000
    }
  ]
}
```

| 속성 | 설명 |
| -------- | ------- |
| `quotas` | 각 데이터 라이프사이클 작업 유형에 대한 할당량 정보를 나열합니다. 각 할당량 개체에는 다음 속성이 포함되어 있습니다.<ul><li>`name`</li><li>`description`</li><li>`consumed`</li><li>`quota`</li></ul> |
| `name` | 할당량 유형 식별자. |
| `description` | 이 할당량이 제한하는 내용에 대한 설명입니다. |
| `consumed` | 현재 사용된 할당량입니다. 소비된 금액은 그 달의 1일에 00:00 GMT 및 00:00 GMT에서 일별 할당량으로 재설정됩니다. |
| `quota` | 조직에 대한 이 할당량 유형의 최대 할당량입니다. |
