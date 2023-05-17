---
description: 대상에 대한 HTTP 요청을 그룹화하고 일괄 처리하는 방법을 결정하기 위해 집계 정책을 설정하는 방법을 알아봅니다.
title: 집계 정책
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# 집계 정책

데이터를 API 엔드포인트로 내보낼 때 효율성을 최대화하려면 다양한 설정을 사용하여 내보낸 프로필을 더 큰 배치나 작은 배치로 집계하고 ID 및 기타 사용 사례별로 그룹화할 수 있습니다. 또한 API 끝점의 다운스트림 제한(비율 제한, API 호출당 ID 수 등)으로 데이터 내보내기를 조정할 수 있습니다.

구성 가능한 집계를 사용하여 Destination SDK에서 제공하는 설정을 자세히 살펴보거나 최상의 노력 집계를 사용하여 Destination SDK에게 API 호출을 가능한 한 많이 배치하도록 하십시오.

Destination SDK을 사용하여 실시간(스트리밍) 대상을 작성할 때 내보낸 프로필을 결과 내보내기에 결합하는 방법을 구성할 수 있습니다. 이 동작은 집계 정책 설정에 의해 결정됩니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서를 참조하십시오. [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration).

를 통해 집계 정책 설정을 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 집계 정책 설정에 대해 설명합니다.

이 문서를 읽은 후 다음 문서를 참조하십시오. [템플릿 사용](../../functionality/destination-server/message-format.md#using-templating) 그리고 [집계 키 예](../../functionality/destination-server/message-format.md#template-aggregation-key) 선택한 집계 정책을 기반으로 메시지 변환 템플릿에 집계 정책을 포함하는 방법을 이해합니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 아니요 |

## 최상의 노력 집계 {#best-effort-aggregation}

최상의 노력 집계는 요청당 프로필 수를 줄이고, 데이터가 많은 요청이 적은 것보다 적은 데이터로 더 많은 요청을 받는 대상에 가장 적합합니다.

아래 예제 구성은 최상의 작업 집계 구성을 보여줍니다. 구성 가능한 집계의 예는 [구성 가능한 합계](#configurable-aggregation) 섹션을 참조하십시오. 최상의 작업 집계에 적용할 수 있는 매개 변수가 아래 표에 설명되어 있습니다.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `aggregationType` | 문자열 | 대상이 사용해야 하는 집계 정책 유형을 나타냅니다. 지원되는 합계 유형: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | 정수 | Experience Platform은 내보낸 여러 프로필을 단일 HTTP 호출로 집계할 수 있습니다. <br><br>이 값은 단일 HTTP 호출에서 엔드포인트가 수신해야 하는 최대 프로필 수를 나타냅니다. 이는 최상의 노력 집계에 해당합니다. 예를 들어 값 100을 지정하는 경우 Platform은 호출 시 100보다 작은 수의 프로필을 전송할 수 있습니다. <br><br> 서버가 요청당 여러 사용자를 허용하지 않는 경우 이 값을 로 설정하십시오 `1`. |
| `bestEffortAggregation.splitUserById` | 부울 | 대상에 대한 호출이 ID로 분할되어야 하는 경우 이 플래그를 사용합니다. 이 플래그를 로 설정 `true` 서버가 호출당 하나의 ID만 허용하는 경우 지정된 id 네임스페이스에 대해 을(를) 허용합니다. |

{style="table-layout:auto"}

>[!TIP]
>
>API 엔드포인트가 API 호출당 100개 미만의 프로필을 허용하는 경우 최상의 노력 집계를 사용하십시오.

## 구성 가능한 집계 {#configurable-aggregation}

구성 가능한 집계는 동일한 호출에 수천 개의 프로필을 사용하는 대규모 배치를 사용하는 것이 가장 좋습니다. 또한 이 옵션을 사용하면 복잡한 집계 규칙을 기반으로 내보낸 프로필을 집계할 수 있습니다.

아래 예제 구성은 구성 가능한 집계 구성을 보여줍니다. 최상의 작업 집계의 예는 를 참조하십시오. [최상의 작업 집계](#best-effort-aggregation) 섹션을 참조하십시오. 구성 가능한 합계에 적용할 수 있는 매개 변수가 아래 표에 설명되어 있습니다.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `aggregationType` | 문자열 | 대상이 사용해야 하는 집계 정책 유형을 나타냅니다. 지원되는 합계 유형: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | 부울 | 대상에 대한 호출이 ID로 분할되어야 하는 경우 이 플래그를 사용합니다. 이 플래그를 로 설정 `true` 서버가 호출당 하나의 ID만 허용하는 경우 지정된 id 네임스페이스에 대해 을(를) 허용합니다. |
| `configurableAggregation.maxBatchAgeInSecs` | 정수 | 와 함께 사용됩니다. `maxNumEventsInBatch`로 지정하는 경우 이 매개 변수는 엔드포인트에 API 호출을 전송할 때까지 Experience Platform이 대기하는 시간을 결정합니다. <ul><li>최소 값(초): 1800년</li><li>최대 값(초): 3600년</li></ul> 예를 들어, 두 매개 변수 모두에 대해 최대값을 사용하는 경우 Experience Platform은 API 호출을 수행하기 전에 자격을 갖춘 프로필이 10000 전까지 또는 3600초 동안 대기합니다. 이때 먼저 발생합니다. |
| `configurableAggregation.maxNumEventsInBatch` | 정수 | 와 함께 사용됩니다. `maxBatchAgeInSecs`, 이 매개 변수는 API 호출에서 집계해야 하는 정규화된 프로필 수를 결정합니다. <ul><li>최소값: 1000년</li><li>최대값: 10000</li></ul> 예를 들어, 두 매개 변수 모두에 대해 최대값을 사용하는 경우 Experience Platform은 API 호출을 수행하기 전에 자격을 갖춘 프로필이 10000 전까지 또는 3600초 동안 대기합니다. 이때 먼저 발생합니다. |
| `configurableAggregation.aggregationKey` | - | 아래 설명된 매개 변수를 기반으로 대상에 매핑된 내보낸 프로필을 집계할 수 있습니다. |
| `configurableAggregation.aggregationKey.includeSegmentId` | 부울 | 이 매개 변수를 로 설정 `true` 대상으로 내보낸 프로필을 세그먼트 ID별로 그룹화하려면 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 부울 | 이 매개 변수와 `includeSegmentId` to `true`: 대상에 내보낸 프로필을 세그먼트 ID 및 세그먼트 상태별로 그룹화하려면 |
| `configurableAggregation.aggregationKey.includeIdentity` | 부울 | 이 매개 변수를 로 설정 `true` id 네임스페이스로 대상에 내보낸 프로필을 그룹화하려는 경우. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 부울 | 이 매개 변수를 로 설정 `true` 내보낸 프로필을 단일 ID(GAID, IDFA, 전화 번호, 이메일 등)를 기반으로 그룹으로 집계하려면 |
| `configurableAggregation.aggregationKey.groups` | 어레이 | 대상으로 내보낸 프로필을 ID 네임스페이스 그룹으로 그룹화하려면 ID 그룹 목록을 만듭니다. 예를 들어 IDFA 및 GAID 모바일 식별자를 포함하는 프로필을 위의 예에 표시된 구성을 사용하여 대상에 대한 한 호출과 이메일을 다른 호출로 결합할 수 있습니다. |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상에 대한 집계 정책을 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증 구성](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [배치 구성](batch-configuration.md)
* [내역 프로필 자격](historical-profile-qualifications.md)