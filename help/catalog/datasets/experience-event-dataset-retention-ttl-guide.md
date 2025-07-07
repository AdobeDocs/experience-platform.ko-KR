---
title: TTL을 사용하여 데이터 레이크에서 경험 이벤트 데이터 세트 유지 관리
description: Adobe Experience Platform API의 TTL(Time-To-Live) 구성을 사용하여 데이터 레이크에서 경험 이벤트 데이터 세트 보존을 평가, 설정 및 관리하는 방법을 알아봅니다. 이 안내서에서는 TTL 행 수준 만료가 데이터 보존 정책을 지원하고, 스토리지 효율성을 최적화하고, 효과적인 데이터 수명주기 관리를 보장하는 방법을 설명합니다. 또한 TTL을 효과적으로 적용하는 데 도움이 되는 사용 사례와 모범 사례를 제공합니다.
exl-id: d688d4d0-aa8b-4e93-a74c-f1a1089d2df0
source-git-commit: 65a132609bc30233ac9f7efbe1981d4f75f3acb9
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---

# TTL을 사용하여 데이터 레이크에서 경험 이벤트 데이터 세트 유지 관리

효율적인 데이터 관리는 최적의 성능, 비용 제어 및 데이터 무결성을 위해 매우 중요합니다. TTL(Experience Event Dataset Retention Time-To-Live)을 사용하여 행 수준 만료를 적용하므로 최적의 스토리지 효율성과 데이터 관련성을 보장하면서 데이터 레이크의 데이터 세트에서 오래된 레코드를 자동으로 제거할 수 있습니다.

이 안내서에서는 카탈로그 서비스 API를 사용하여 TTL을 평가, 설정 및 관리하는 방법을 설명합니다. TTL을 적용하는 시기와 이유, API 호출을 사용하여 TTL 값을 구성하고 업데이트하는 방법, 효과적인 구현을 위한 모범 사례에 대해 알아봅니다.

>[!IMPORTANT]
>
>TTL은 데이터 수명주기 관리 및 스토리지 효율성을 최적화하기 위해 설계되었습니다. 규정 준수 툴이 아니므로 규정 요구 사항에 의존해서는 안 됩니다. 규정 준수를 위해서는 보다 광범위한 데이터 거버넌스 전략이 필요한 경우가 많습니다.

## 행 수준 데이터 관리에 TTL을 사용하는 이유

데이터 세트 규모가 커짐에 따라 성능 보존, 비용 제어 및 데이터 관련 유지를 위해 효율적인 데이터 관리가 점점 더 중요해지고 있습니다. TTL 기반 행 수준 데이터 만료는 수작업 없이 오래된 레코드를 제거하여 스토리지 최적화와 시스템 효율성을 향상시켜 데이터 정리를 자동화합니다.

TTL은 시간이 지남에 따라 관련성을 잃는 시간에 민감한 데이터를 관리할 때 유용합니다. 다음과 같은 작업을 수행해야 하는 경우 TTL 구현을 고려하십시오.

- 오래된 레코드를 자동으로 제거하여 스토리지 비용 절감
- 관련이 없는 데이터를 최소화하여 쿼리 성능을 개선합니다.
- 관련 정보만 유지하여 데이터 위생을 유지합니다.
- 데이터 보존을 최적화하여 비즈니스 목표를 지원합니다.

>[!NOTE]
>
>경험 이벤트 데이터 세트 유지 는 데이터 레이크에 저장된 이벤트 데이터에 적용됩니다. Real-Time Customer Data Platform에서 보존을 관리하는 경우 데이터 레이크 보존 설정과 함께 [경험 이벤트 만료](../../profile/event-expirations.md) 및 [익명 프로필 만료](../../profile/pseudonymous-profiles.md)을 사용하는 것이 좋습니다.

TTL 구성을 사용하여 권한에 따라 저장소를 최적화합니다. 프로필 저장소 데이터(Real-Time CDP에서 사용)는 30일 후에 부실 상태로 간주되어 제거될 수 있지만 데이터 레이크의 동일한 이벤트 데이터는 analytics 및 Data Distiller 사용 사례에 대해 12~13개월(또는 자격 기준에 따라 더 오래) 동안 사용할 수 있습니다.

>[!TIP]
>
>권한은 Adobe 구독 및 라이선스 계약에 의해 정의된 스토리지 및 유지 수당을 의미합니다.

### 업계 사례 {#industry-example}

예를 들어, 비디오 보기, 검색 및 권장 사항과 같은 사용자 상호 작용을 추적하는 비디오 스트리밍 서비스를 고려해 보십시오. 최근 참여 데이터는 개인화에 중요하지만, 이전 활동 로그(예: 1년 이상의 상호 작용)는 관련성을 잃게 됩니다. Experience Platform은 행 수준 만료를 사용하여 오래된 로그를 자동으로 제거하여 현재 및 의미 있는 데이터만 분석 및 권장 사항에 사용하도록 합니다.

## TTL 적합성 평가 {#evaluate-ttl-suitability}

보존 정책을 적용하기 전에 데이터 세트가 행 수준 만료에 적합한 후보인지 평가합니다. 다음 사항을 고려하십시오.

- 시간에 따른 데이터 관련성: 이전 데이터가 가치를 제공합니까, 아니면 더 이상 쓸모가 없어집니까?
- 다운스트림 프로세스에 미치는 영향: 데이터를 제거하면 보고, 분석 또는 통합에 영향을 줍니까?
- 저장 비용 대 보존 가치: 이전 데이터의 가치가 저장 비용을 정당화합니까?

장기 분석 또는 비즈니스 운영을 위해 기록 기록이 필수인 경우 TTL이 올바른 접근 방식이 아닐 수 있습니다. 이러한 요인을 검토하면 데이터 가용성에 부정적인 영향을 주지 않고 TTL이 데이터 유지 요구 사항에 맞게 조정됩니다.

## TTL 설정 우수 사례 {#best-practices}

올바른 TTL 값을 선택하여 경험 이벤트 데이터 세트 유지 정책이 데이터 유지, 스토리지 효율성 및 분석 요구 사항의 균형을 이루도록 합니다. TTL이 너무 짧으면 데이터 손실이 발생할 수 있지만 너무 긴 TTL은 저장 비용과 불필요한 데이터 축적을 증가시킬 수 있습니다. TTL은 데이터 액세스 빈도와 적절한 데이터 유지 기간을 고려하여 데이터 세트의 목적에 맞게 조정되어야 합니다.

아래 표는 데이터 세트 유형 및 사용 패턴을 기반으로 하는 일반적인 TTL 권장 사항을 제공합니다.

| 데이터 세트 유형 | 권장 TTL | 일반적인 사용 사례 |
|-----------------------------|------------------------|-------------------|
| 자주 액세스하는 데이터 세트 | 30-90일 | 사용자 참여 로그, 웹 사이트 클릭스트림 데이터, 단기 캠페인 성과 데이터. |
| 아카이브 데이터 세트 | 1년 이상 | 금융 거래 로그, 규정 준수 데이터, 장기 추세 분석, 머신 러닝 교육 데이터 세트. |
| 앱 관리 데이터 세트 | 최장 13개월 | 시스템 관리 데이터 세트에는 사전 정의된 TTL 제한이 있으며, 이 제한은 시스템에서 지정한 제한을 준수하도록 자동으로 적용됩니다. |
| 고객 관리 데이터 세트 | 30일 - 최대 TTL | UI, API 또는 Data Distiller을 통해 생성된 데이터 세트. TTL은 최소 30일이어야 하며 정의된 최대 TTL 이내여야 합니다. |

TTL 설정을 정기적으로 검토하여 스토리지 정책, 분석 요구 사항 및 비즈니스 요구 사항에 맞게 계속 조정할 수 있습니다.

### TTL 설정 시 주요 고려 사항 {#key-considerations}

다음 모범 사례에 따라 TTL 설정이 데이터 유지 전략에 부합하는지 확인하십시오.

- 감사 TTL은 정기적으로 변경됩니다. 모든 TTL 업데이트는 감사 이벤트를 트리거합니다. 감사 로그를 사용하여 규정 준수, 데이터 거버넌스 및 문제 해결 목적의 TTL 수정 사항을 추적합니다.
- 데이터를 무기한 유지해야 하는 경우 TTL을 비활성화합니다. TTL을 사용하지 않도록 설정하려면 `ttlValue`을(를) `null`(으)로 설정하십시오. 이렇게 하면 자동 만료가 방지되며 모든 레코드가 영구적으로 유지됩니다. 이 변경 작업을 수행하기 전에 스토리지 관련 사항을 고려하십시오.

## TTL 제한 사항 {#limitations}

TTL을 사용할 때는 다음 제한 사항에 유의하십시오.

- **TTL을 사용한 경험 이벤트 데이터 세트 보존은 데이터 세트 삭제가 아닌 행 수준 만료**&#x200B;에 적용됩니다. TTL은 정의된 보존 기간에 따라 레코드를 제거하지만 전체 데이터 세트를 삭제하지는 않습니다. 데이터 집합을 제거하려면 [데이터 집합 만료 끝점](../../hygiene/api/dataset-expiration.md) 또는 수동 삭제를 사용하십시오.
- **TTL 구성은 명시적으로 비활성화될 때까지 활성 상태로 유지됩니다**. 구성은 비활성화하기 전까지 계속 적용됩니다. TTL을 비활성화하면 만료가 중지되고 데이터 세트의 모든 레코드가 유지됩니다.
- **TTL은 준수 도구가 아닙니다**. TTL은 스토리지 및 라이프사이클 관리를 최적화하는 반면, 규정 준수를 보장하기 위해 광범위한 거버넌스 전략을 구현해야 합니다.

## TTL 적용 전 데이터 세트 크기 및 관련성 분석 {#analyze-dataset-size}

TTL을 적용하기 전에 쿼리를 사용하여 데이터 세트 크기와 관련성을 분석하십시오. 타깃팅된 쿼리(예: 특정 날짜 범위 내의 레코드 계산)를 실행하여 다양한 TTL 값의 영향을 미리 봅니다. 그런 다음 이 정보를 사용하여 데이터 유틸리티와 비용 효율성의 균형을 맞추는 최적의 보존 기간을 선택합니다.

![경험 이벤트 데이터 세트에서 TTL을 구현하기 위한 시각적 워크플로우입니다. 데이터 수명 및 제거 영향을 평가하고, 쿼리를 통해 TTL 설정을 확인하고, 카탈로그 서비스 API를 통해 TTL을 구성하고, TTL 영향을 지속적으로 모니터링하고 조정하는 단계가 포함됩니다.](../images/datasets/dataset-retention-ttl-guide/manage-experience-event-dataset-retention-in-the-data-lake.png)

타깃팅된 쿼리를 실행하면 다양한 TTL 구성에서 유지하거나 제거할 데이터의 양을 결정하는 데 도움이 됩니다. 예를 들어 다음 SQL 쿼리는 지난 30일 이내에 생성된 레코드 수를 계산합니다.

```sql
SELECT COUNT(1) FROM [datasetName] WHERE timestamp > date_sub(now(), INTERVAL 30 DAY);
```

다양한 시간 간격으로 유사한 쿼리를 실행하면 TTL 설정의 유효성을 확인하고 스토리지 효율성과 데이터 액세스 가능성 간의 균형을 유지할 수 있습니다.

## TTL 관리 시작

카탈로그 서비스 API를 사용하여 경험 이벤트 데이터 세트 보존을 평가, 설정 및 관리하려면 먼저 요청 형식을 올바르게 지정하는 방법을 이해해야 합니다. 여기에는 API 경로 확인, 필수 헤더 제공 및 요청 페이로드 서식 지정 등이 포함됩니다. 자세한 내용은 [카탈로그 서비스 API 시작 안내서](../api/getting-started.md)를 참조하세요.

>[!NOTE]
>
>이 문서에서는 데이터 세트 자체를 그대로 유지하면서 데이터 세트 내에서 만료된 개별 행을 삭제하는 행 수준 만료를 다룹니다. 전체 데이터 세트를 제거하고 별도의 기능으로 관리되는 데이터 세트 만료에는 적용되지 않습니다. 데이터 세트 수준 만료는 [데이터 세트 만료 API 설명서](../../hygiene/api/dataset-expiration.md)를 참조하세요.

### TTL 제한 사항 확인 {#check-ttl-constraints}

데이터 위생 API `/ttl/{DATASET_ID}` 끝점을 사용하여 TTL 구성을 계획합니다. 이 끝점은 데이터 집합 형식에 대한 권장 값(`defaultValue`)과 함께 조직에 대해 지원되는 최소 및 최대 TTL 값을 반환합니다.

자세한 내용은 Adobe Developer [데이터 위생 API](https://developer.adobe.com/experience-platform-apis/references/data-hygiene/#operation/getTtl) 설명서를 참조하십시오.

[데이터 세트에 현재 적용된 TTL을 확인](#check-applied-ttl-values)하려면 대신 [카탈로그 서비스 API](https://developer.adobe.com/experience-platform-apis/references/catalog/) `/dataSets/{DATASET_ID}` 끝점에 GET을 요청하세요.

>[!TIP]
>
>카탈로그 서비스 API의 Experience Platform 게이트웨이 URL 및 기본 경로는 `https://platform.adobe.io/data/foundation/catalog`입니다. 데이터 위생 API의 기본 경로는 `https://platform.adobe.io/data/core/hygiene`입니다.

**API 형식**

```http
GET /ttl/{DATASET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | 데이터 세트를 고유하게 식별하는 시스템 생성 문자열입니다. 데이터 집합 ID를 찾으려면 `/datasets` 끝점을 사용하십시오. 관련 데이터 세트의 응답을 필터링하는 방법에 대한 지침은 [목록 카탈로그 개체 API 안내서](../api/list-objects.md)를 참조하십시오. |

**요청**

다음 요청은 특정 데이터 세트에 대한 조직의 TTL 제약 조건을 검색합니다.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/ttl/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'x-sandbox-id: {SANDBOX_ID}'
```

**응답**

성공적인 응답은 데이터 집합에 대한 제안된 TTL(`defaultValue`)과 함께 조직의 권한에 따른 권장, 최대 및 최소 TTL 값을 반환합니다. 이 `defaultValue`은(는) 지침에만 제공되는 권장 TTL 기간입니다. 사용자가 명시적으로 구성하지 않으면 적용되지 않습니다. 응답에는 이미 설정되었을 수 있는 사용자 지정 TTL 값이 포함되지 않습니다. 데이터 집합에 대한 현재 TTL을 보려면 GET `/catalog/dataSets/{DATASET_ID}` 끝점을 사용하십시오.

+++응답을 보려면 선택

```json
{
  "extensions": {
    "adobe_lakeHouse": {
      "rowExpiration": {
        "defaultValue": "P12M",
        "maxValue": "P12M",
        "minValue": "P7D"
      }
    }
  }
}
```

+++

| 속성 | 설명 |
|--------------|-------------|
| `defaultValue` | 데이터 세트에 대한 권장 TTL 값입니다. 이 값은 **자동으로 적용되지 않습니다**. TTL을 적용하려면 명시적으로 TTL을 설정해야 합니다. |
| `maxValue` | 조직의 권한 부여에 허용되는 최대 TTL 기간입니다. 일반적으로 이 기간은 10년(`P10Y`)입니다. |
| `minValue` | 조직의 권한 부여에 허용되는 최소 TTL 기간입니다. 일반적으로 이 기간은 30일(`P30D`)입니다. |

### 적용된 TTL 값을 확인하는 방법 {#check-applied-ttl-values}

데이터 세트에 적용된 현재 TTL 값을 확인하려면 다음 API 호출을 사용하십시오.

```http
GET /dataSets/{DATASET_ID}
```

이 호출은 `ttlValue` 섹션의 현재 `extensions.adobe_lakeHouse.rowExpiration`(설정된 경우)을(를) 반환합니다.

**요청**

다음 요청은 특정 데이터 세트에 대한 조직의 TTL 값을 검색합니다.

```shell
curl -X GET \
https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답에는 데이터 집합에 적용된 현재 TTL 구성이 포함된 `extensions` 개체가 포함됩니다. 아래 응답 예제는 간결성을 위해 잘립니다.

```json
{
    "{DATASET_ID}": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M",
            }
            }
        }
        ...
    }
}
```

### 데이터 세트에 대한 TTL 설정 또는 업데이트 {#set-update-ttl}

>[!IMPORTANT]
>
>TTL 기반 행 수준 만료는 시계열 스키마를 사용하는 이벤트 데이터 세트에만 적용할 수 있습니다. 여기에는 표준 XDM ExperienceEvent 클래스를 기반으로 한 데이터 세트와 시계열 스키마(`https://ns.adobe.com/xdm/data/time-series`)를 확장하는 사용자 지정 스키마가 포함됩니다.
>
>TTL을 적용하기 전에 스키마 레지스트리 API를 사용하여 `meta:extends` 속성을 확인하여 데이터 집합의 스키마에 올바른 확장이 포함되어 있는지 확인하십시오. 이 작업을 수행하는 방법에 대한 지침은 [스키마 끝점 설명서](../../xdm/api/schemas.md#lookup)를 참조하십시오.

새 TTL 을 설정하거나 동일한 API 방법을 사용하여 기존 TTL 을 업데이트하여 경험 이벤트 데이터 세트 유지 를 구성할 수 있습니다. TTL을 적용하거나 조정하려면 `/v2/datasets/{DATASET_ID}` 끝점에 대한 PATCH 요청을 사용하십시오.

**API 형식**

```http
PATCH /v2/datasets/{DATASET_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{DATASET_ID}` | TTL 값을 업데이트할 데이터 세트의 ID입니다. |

**요청**

아래 예제에서는 `ttlValue`이(가) `P3M`(으)로 설정되어 있습니다. 즉, 3개월 이상 지난 레코드는 자동으로 삭제됩니다. 비즈니스 요구 사항에 맞게 보존 기간을 조정하십시오(예: 6개월 `P6M` 또는 1년 `P12M`).

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P3M"  // A 3 month retention period
            }
        }
    }
}
```

| 속성 | 설명 |
|----------------------------------|-------------|
| `rowExpiration.ttlValue` | 데이터 세트의 레코드가 자동으로 제거되기 전 기간을 정의합니다. ISO-8601 기간 형식을 사용합니다(예: 3개월 동안 `P3M`, 30일 동안 `P30D`). |

**응답**

성공적인 응답은 업데이트된 데이터 세트에 대한 참조를 반환하지만 TTL 설정을 명시적으로 포함하지는 않습니다. TTL 구성을 확인하려면 후속 `GET /dataSets/{DATASET_ID}` 요청을 만듭니다.

```JSON
[
  "@/dataSets/{DATASET_ID}"
]
```

#### 예시 상황 {#example-scenario}

개인화를 위해 새로운 참여 데이터를 보장하기 위해 처음에 TTL을 3개월로 설정하는 비디오 스트리밍 플랫폼을 고려하십시오. 그러나 후속 분석에서 이전 상호 작용이 여전히 중요한 통찰력을 제공한다고 밝혀지면 다음 요청을 통해 TTL을 6개월로 연장할 수 있습니다.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/catalog/v2/datasets/{DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "extensions": {
        "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P6M"  // Extend to 6 months
            }
        }
    }
}
```

## 데이터 세트 보존 정책 FAQ {#faqs}

이 FAQ는 데이터 세트 보존 작업, TTL 변경의 즉각적인 영향, 복구 옵션 및 플랫폼 서비스별로 보존 기간이 어떻게 다른지에 대한 실용적인 질문을 다룹니다.

### 보존 정책 규칙을 적용할 수 있는 데이터 세트 유형은 무엇입니까?

+++답변
시계열 동작을 사용하는 모든 데이터 세트에 TTL 기반 보존 정책을 적용할 수 있습니다. 여기에는 표준 XDM ExperienceEvent 클래스를 기반으로 한 데이터 세트와 시계열 데이터를 캡처하도록 디자인된 사용자 지정 스키마가 포함됩니다.

행 수준 만료를 사용하려면 다음 기술 조건이 필요합니다.

- 스키마는 시계열 데이터를 캡처하도록 디자인되어야 합니다.
- 스키마에 만료를 평가하는 데 사용되는 타임스탬프 필드가 포함되어야 합니다.
- 데이터 세트는 일반적으로 XDM ExperienceEvent 클래스를 사용하거나 확장하는 이벤트 수준 데이터를 저장해야 합니다.
- TTL 설정이 `extensions.adobe_lakeHouse.rowExpiration`을(를) 통해 적용되므로 데이터 집합은 카탈로그 서비스에 등록되어야 합니다.
- TTL 값은 ISO-8601 기간 형식(예: `P30D`, `P6M`, `P1Y`)을 사용해야 합니다.
+++

### 데이터 세트 유지 작업이 데이터 레이크 서비스에서 데이터를 삭제하는 데 얼마나 걸립니까?

+++답변
데이터 세트 TTL은 30일마다 평가 및 처리되며 만료된 모든 레코드를 삭제합니다. 이벤트가 30일 이상 전(수집 날짜 > 30일)에 Experience Platform에 수집되고 이벤트 날짜가 정의된 유지 기간(TTL)을 초과하는 경우 만료된 것으로 간주됩니다.
+++

<!-- ### How soon will the Dataset Retention job delete data from Profile services?

+++Answer
Once a retention policy is set, existing events that already exceed the newly defined TTL are immediately deleted. Newer events remain until their timestamps surpass the retention period.

For example, if you apply a 30-day expiration policy on May 15th, the following occurs:

- New events receive a 30-day expiration as they are ingested.
- Existing events with a timestamp older than April 15th are immediately deleted.
- Existing events with a timestamp after April 15th are set to expire 30 days after their timestamp (for example, an event from April 18th would be deleted on May 18th).
+++ -->

### 데이터 레이크 및 프로필 서비스에 대해 서로 다른 보존 정책을 설정할 수 있습니까?

+++답변
예. 데이터 레이크 및 프로필 서비스에 대해 서로 다른 보존 정책을 설정할 수 있습니다. 조직의 필요에 따라 프로필 스토어의 보존 기간은 데이터 레이크 보존 기간보다 짧거나 길 수 있습니다.
+++

### 현재 데이터 세트 사용을 확인하려면 어떻게 해야 합니까?

+++답변
[!UICONTROL 데이터 세트] 인벤토리 작업 영역에서 별도의 지표로 데이터 레이크 및 프로필 저장소의 최신 데이터 세트 저장소 크기를 확인할 수 있습니다. 열을 정렬하여 가장 큰 데이터 세트를 식별하고 보존 정책이 적용되는지 확인합니다.

샌드박스 수준 사용법은 라이선스 사용량 대시보드를 참조하십시오. 자세한 내용은 [라이선스 사용 설명서](../../dashboards/guides/license-usage.md)를 참조하세요.
+++

### 데이터 보존 작업이 성공했는지 확인하려면 어떻게 해야 합니까?

+++답변
[데이터 집합 보존 구성 UI](./user-guide.md#data-retention-policy) 또는 데이터 인벤토리 페이지에서 해당 타임스탬프를 확인하여 마지막 데이터 보존 작업을 확인할 수 있습니다.

또는 다음 엔드포인트에 대한 GET 요청을 수행할 수 있습니다.

`GET https://platform.adobe.io/data/foundation/catalog/dataSets/{DATASET_ID}`

응답에는 가장 최근 TTL 작업이 완료된 시간의 Unix 타임스탬프(밀리초)를 나타내는 `extensions.adobe_lakeHouse.rowExpiration.lastCompleted` 속성이 포함됩니다.

내역 데이터 세트 사용 현황 보고는 현재 사용할 수 없습니다.
+++

### 삭제 된 데이터를 복구 할 수 있습니까?

+++답변
아니요. 보존 정책이 적용되면 보존 기간보다 오래된 데이터는 영구적으로 삭제되며 복구할 수 없습니다.
+++

### 데이터 레이크 경험 이벤트 데이터 세트에서 구성할 수 있는 최소 TTL은 얼마입니까?

+++답변
데이터 레이크 경험 이벤트 데이터 세트의 최소 TTL은 30일입니다. 데이터 레이크는 초기 수집 및 처리 중 처리 백업 및 복구 시스템으로서 작동합니다. 따라서 데이터는 수집 후 최소 30일 동안 데이터 레이크에 남아 있어야 만료될 수 있습니다.
+++

### TTL 정책이 허용하는 것보다 더 오래 일부 데이터 레이크 필드를 유지해야 하는 경우 어떻게 합니까?

+++답변
활용률 제한 내에 있는 동안 데이터 세트의 TTL 이상의 특정 필드를 유지하려면 Data Distiller 를 사용하십시오. 파생된 데이터 세트에 필요한 필드만 정기적으로 작성하는 작업을 만듭니다. 이 워크플로우를 통해 중요한 데이터를 장기간 보존하면서 TTL을 단축하고 규정을 준수할 수 있습니다.

자세한 내용은 [SQL 안내서로 파생 데이터 집합 만들기](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md)를 참조하세요.
+++

## 다음 단계 {#next-steps}

행 수준 만료에 대한 TTL 설정을 관리하는 방법을 배웠으므로 다음 설명서를 검토하여 TTL 관리에 대해 더 깊이 이해하십시오.

- 보존 작업: [데이터 수명 주기 UI 안내서](../../hygiene/ui/dataset-expiration.md)를 통해 Experience Platform UI에서 데이터 세트 만료를 예약 및 자동화하거나 데이터 세트 보존 구성을 확인하고 만료된 레코드가 삭제되는지 확인하는 방법을 알아봅니다.
- [데이터 집합 만료 API 끝점 안내서](../../hygiene/api/dataset-expiration.md): 행뿐만 아니라 전체 데이터 집합을 삭제하는 방법을 알아봅니다. 효율적인 데이터 보존을 위해 API를 사용하여 데이터 세트 만료를 예약, 관리 및 자동화하는 방법에 대해 알아봅니다.
- [데이터 사용 정책 개요](../../data-governance/policies/overview.md): 데이터 보존 전략을 더 광범위한 규정 준수 요구 사항 및 마케팅 사용 제한 사항에 맞추는 방법에 대해 알아봅니다.
