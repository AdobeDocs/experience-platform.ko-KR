---
title: ID 그래프 연결 규칙 문제 해결 설명서
description: ID 그래프 연결 규칙의 일반적인 문제를 해결하는 방법을 알아봅니다.
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: 7174c2c0d8c4ada8d5bba334492bad396c1cfb34
workflow-type: tm+mt
source-wordcount: '3286'
ht-degree: 0%

---

# ID 그래프 연결 규칙에 대한 문제 해결 안내서

>[!AVAILABILITY]
>
>ID 그래프 연결 규칙은 현재 제한적 가용성입니다. 개발 샌드박스의 기능에 액세스하는 방법에 대한 자세한 내용은 Adobe 계정 팀에 문의하십시오.

ID 그래프 연결 규칙을 테스트하고 유효성을 검사할 때 데이터 수집 및 그래프 비헤이비어와 관련된 몇 가지 문제가 발생할 수 있습니다. ID 그래프 연결 규칙을 사용하여 작업할 때 발생할 수 있는 몇 가지 일반적인 문제를 해결하는 방법을 배우려면 이 문서를 참조하십시오.

## 데이터 수집 흐름 개요 {#data-ingestion-flow-overview}

다음 다이어그램은 데이터가 Adobe Experience Platform 및 애플리케이션으로 유입되는 방식을 단순하게 보여 줍니다. 이 페이지의 내용을 더 잘 이해하려면 이 다이어그램을 참조로 사용하십시오.

![ID 서비스에서 데이터 수집이 어떻게 진행되는지 보여 주는 다이어그램입니다.](../images/troubleshooting/dataflow_in_identity.png)

다음 요인에 유의해야 합니다.

* 데이터 스트리밍의 경우, 데이터가 전송될 때 실시간 고객 프로필, ID 서비스 및 데이터 레이크가 데이터 처리를 시작합니다. 그러나 데이터 처리를 완료하는 데 걸리는 지연은 서비스에 따라 다릅니다. 일반적으로 데이터 레이크는 프로필 및 ID에 비해 처리 시간이 오래 걸립니다.
   * 두 시간 후에도 데이터 세트에 대해 쿼리를 실행할 때 데이터가 표시되지 않으면 데이터가 Experience Platform에 수집되지 않았을 수 있습니다.
* 배치 데이터의 경우, 모든 데이터가 먼저 데이터 레이크로 이동한 다음, 데이터 세트가 프로필 및 ID에 대해 활성화된 경우 데이터가 프로필 및 ID에 전파됩니다.
* 수집 관련 문제의 경우 정확한 디버깅 및 문제 해결을 위해 서비스 수준에서 문제를 분리하는 것이 중요합니다. 고려해야 할 세 가지 잠재적 문제 유형이 있습니다.

| 수집 문제 유형 | 데이터가 데이터 레이크에서 수집됩니까? | 데이터가 프로필에서 수집됩니까? | ID 서비스에서 데이터가 수집됩니까? |
| --- | --- | --- | --- |
| 일반 수집 문제 | 아니요 | 아니요 | 아니요 |
| 그래프 문제 | 예 | 예 | 아니요 |
| 프로필 조각 문제 | 예 | 아니요 | 예 |

## 데이터 수집 문제 {#data-ingestion-issues}

>[!NOTE]
>
>* 이 섹션에서는 데이터가 데이터 레이크에 성공적으로 수집되었으며 데이터가 처음부터 Experience Platform에 수집되지 않도록 하는 구문 또는 기타 오류가 없다고 가정합니다.
>
>* 이 예제에서는 ECID를 쿠키 네임스페이스로 사용하고 CRMID를 개인 네임스페이스로 사용합니다.

### 내 ID가 ID 서비스에 수집되지 않습니다.{#my-identities-are-not-getting-ingested-into-identity-service}

이 문제가 발생할 수 있는 이유에는 다음과 같은 다양한 이유가 있습니다.

* [프로필에 대해 데이터 집합을 사용할 수 없습니다](../../catalog/datasets/enable-for-profile.md).
* 이벤트에 ID가 하나만 있으므로 레코드를 건너뜁니다.
* [ID 서비스에서 유효성 검사 오류가 발생했습니다](../guardrails.md#identity-value-validation).
   * 예를 들어 ECID는 최대 길이인 38자를 초과할 수 있습니다.
* 기본적으로 [AAID는 수집되지 않도록 차단됩니다](../guardrails.md#identity-namespace-ingestion).
* [시스템 보호](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated) 때문에 ID가 제거되었습니다.

ID 그래프 연결 규칙의 컨텍스트 내에서, 들어오는 이벤트에 고유 네임스페이스는 같지만 ID 값이 다른 두 개 이상의 ID가 있으므로 ID 서비스에서 레코드가 거부될 수 있습니다. 이 시나리오는 일반적으로 구현 오류로 인해 발생합니다.

두 가지 가정을 사용하여 다음 이벤트를 고려하십시오.

1. 필드 이름 CRMID는 CRMID 네임스페이스와 ID로 표시됩니다.
2. 네임스페이스 CRMID는 고유한 네임스페이스로 정의됩니다.

다음 이벤트는 수집이 실패했음을 나타내는 오류 메시지를 반환합니다.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**문제 해결 단계**

이 오류를 해결하려면 먼저 다음 정보를 수집해야 합니다.

* ID 그래프에서 수집되어야 하는 ID 값(`identity_value`)입니다.
* 이벤트를 전송한 데이터 집합(`dataset_name`)입니다.

그런 다음 [Adobe Experience Platform 쿼리 서비스](../../query-service/home.md)를 사용하고 다음 쿼리를 실행합니다.

>[!TIP]
>
>`dataset_name` 및 `identity_value`을(를) 수집한 정보로 바꾸십시오.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

쿼리를 실행한 후 그래프를 생성해야 하는 이벤트 레코드를 찾은 다음 동일한 행에서 ID 값이 다른지 확인합니다. 예를 보려면 다음 이미지를 확인하십시오.

![이름 없는 쿼리로 인해 네임스페이스가 중복되었습니다.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>두 ID가 정확히 동일하고 이벤트를 스트리밍을 통해 수집하는 경우 ID 및 프로필 모두에서 ID의 중복을 제거합니다.

### 사후 인증 ExperienceEvents는 잘못된 인증된 프로필로 인한 것입니다.

네임스페이스 우선 순위는 이벤트 조각이 기본 ID를 결정하는 방법에 중요한 역할을 합니다.

* 지정된 샌드박스에 대해 [ID 설정](./identity-settings-ui.md)을(를) 구성하고 저장하면 프로필에서 [네임스페이스 우선 순위](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events)을(를) 사용하여 기본 ID를 결정합니다. identityMap의 경우 프로필에서 더 이상 `primary=true` 플래그를 사용하지 않습니다.
* 프로필에서 더 이상 이 플래그를 참조하지 않지만 Experience Platform의 다른 서비스에서는 `primary=true` 플래그를 계속 사용할 수 있습니다.

[인증된 사용자 이벤트](implementation-guide.md#ingest-your-data)를 사용자 네임스페이스에 연결하려면 인증된 모든 이벤트에는 사용자 네임스페이스(CRMID)가 포함되어야 합니다. 즉, 사용자가 로그인한 후에도 인증된 모든 이벤트에 개인 네임스페이스가 계속 존재해야 합니다.

프로필 뷰어에서 프로필을 조회할 때 `primary=true`개의 &#39;이벤트&#39; 플래그가 계속 표시될 수 있습니다. 그러나 이 작업은 무시되며 프로필에서 사용되지 않습니다.

AAID는 기본적으로 차단됩니다. 따라서 [Adobe Analytics 소스 커넥터](../../sources/tutorials/ui/create/adobe-applications/analytics.md)를 사용하는 경우 인증되지 않은 이벤트가 ECID의 기본 ID를 갖도록 ECID가 ECID보다 높은 우선 순위를 갖도록 해야 합니다.

**문제 해결 단계**

1. 인증된 이벤트에 사용자와 쿠키 네임스페이스가 모두 포함되어 있는지 확인하려면 [ID 서비스에 수집되지 않는 데이터에 대한 오류 문제 해결](#my-identities-are-not-getting-ingested-into-identity-service)의 섹션에 설명된 단계를 읽어 보십시오.
2. 인증된 이벤트에 사용자 네임스페이스의 기본 ID(예: CRMID)가 있는지 확인하려면 비결합 병합 정책(개인 그래프를 사용하지 않는 병합 정책)을 사용하여 프로필 뷰어에서 사용자 네임스페이스를 검색합니다. 이 검색은 개인 네임스페이스와 연결된 이벤트만 반환합니다.

### 내 경험 이벤트 조각이 프로필에 수집되지 않습니다. {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

다음을 포함하되 이에 국한되지 않는 다양한 이유로 경험 이벤트 조각이 프로필에 수집되지 않는 이유가 있습니다.

* [프로필에 대해 데이터 집합을 사용할 수 없습니다](../../catalog/datasets/enable-for-profile.md).
* [프로필에서 유효성 검사 오류가 발생했을 수 있습니다](../../xdm/classes/experienceevent.md).
   * 예를 들어 경험 이벤트에는 `_id`과(와) `timestamp`이(가) 모두 포함되어야 합니다.
   * 또한 `_id`은(는) 각 이벤트(레코드)에 대해 고유해야 합니다.

네임스페이스 우선 순위의 컨텍스트에서 프로필은 가장 높은 네임스페이스 우선 순위를 가진 두 개 이상의 ID가 포함된 모든 이벤트를 거부합니다. 예를 들어 GAID가 고유 네임스페이스로 표시되지 않고 GAID 네임스페이스와 다른 ID 값이 있는 두 개의 ID가 모두 들어 있는 경우 프로필은 이벤트를 저장하지 않습니다.

**문제 해결 단계**

데이터가 데이터 레이크로 전송되지만 프로필로 전송되지 않고 단일 이벤트에서 네임스페이스 우선 순위가 가장 높은 두 개 이상의 ID를 전송하기 때문이라고 생각되는 경우 다음 쿼리를 실행하여 동일한 네임스페이스에 대해 전송된 두 개의 다른 ID 값이 있는지 확인할 수 있습니다.

>[!TIP]
>
>다음 쿼리에서 다음을 수행해야 합니다.
>
>* `_testimsorg.identification.core.email`을(를) ID를 보내는 경로로 바꿉니다.
>* `Email`을(를) 우선 순위가 가장 높은 네임스페이스로 바꾸십시오. 수집되지 않는 네임스페이스와 동일합니다.
>* `dataset_name`을(를) 쿼리할 데이터 세트로 바꾸십시오.

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

이 쿼리는 다음을 가정합니다.

* 한 ID는 identityMap에서 전송되고 다른 ID는 ID 설명자에서 전송됩니다. **참고**: XDM(Experience Data Model) 스키마에서 ID 설명자는 ID로 표시된 필드입니다.
* CRMID는 identityMap을 통해 전송됩니다. CRMID를 필드로 보내는 경우 WHERE 절에서 `key='Email'`을(를) 제거하십시오.

## 그래프 동작 관련 문제 {#graph-behavior-related-issues}

이 섹션에서는 ID 그래프의 작동 방식과 관련하여 발생할 수 있는 일반적인 문제에 대해 간략히 설명합니다.

### 인증되지 않은 ExperienceEvents가 잘못된 인증된 프로필에 첨부되고 있습니다.

ID 최적화 알고리즘에서 [가장 최근에 설정된 링크를 적용하고 가장 오래된 링크를 제거합니다](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). 따라서 이 기능을 활성화하면 ECID가 한 개인에서 다른 개인으로 다시 할당(다시 연결)될 수 있습니다. 시간이 지남에 따라 ID가 연결되는 방식을 이해하려면 아래 단계를 따르십시오.

**문제 해결 단계**

>[!NOTE]
>
>다음 단계는 다음과 같은 가정 하에 정보를 검색합니다.
>
>* 단일 데이터 세트가 사용 중입니다(여러 데이터 세트를 쿼리하지 않음).
>
>* [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) 또는 삭제를 수행하는 다른 서비스에 의해 삭제되어 데이터가 데이터 레이크에서 삭제되지 않습니다.

먼저 다음 정보를 수집해야 합니다.

1. 전송된 쿠키 네임스페이스(예: ECID)와 개인 네임스페이스(예: CRMID)의 ID 심볼(namespaceCode)입니다.
1.1. 웹 SDK 구현의 경우 일반적으로 identityMap에 포함된 네임스페이스입니다.
1.2. Analytics 소스 커넥터 구현의 경우 idMap에 포함된 쿠키 식별자입니다. 개인 식별자는 ID로 표시된 eVar 필드입니다.
2. 이벤트가 전송된 데이터 세트(dataset_name)입니다.
3. 조회할 쿠키 네임스페이스의 ID 값(identity_value).

ID 기호(namespaceCode)는 대/소문자를 구분합니다. identityMap에서 주어진 데이터 세트에 대한 모든 ID 기호를 검색하려면 다음 쿼리를 실행합니다.

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

쿠키 식별자의 ID 값을 모를 때 여러 개인 식별자에 연결되었을 쿠키 ID를 검색하려는 경우 다음 쿼리를 실행해야 합니다. 이 쿼리는 ECID를 쿠키 네임스페이스로 가정하고 CRMID를 개인 네임스페이스로 가정합니다.

>[!BEGINTABS]

>[!TAB 웹 SDK 구현]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Analytics 소스 커넥터 구현]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**참고:** personID는 설명자의 경로를 참조합니다. 스키마에서 이 정보를 찾을 수 있습니다.

>[!ENDTABS]

이제 여러 개인 ID에 연결된 쿠키 값을 식별했으므로 결과에서 쿠키 값을 가져와 다음 쿼리에서 사용하여 해당 쿠키 값이 다른 개인 ID에 연결된 시기를 시간순으로 확인합니다.

>[!BEGINTABS]

>[!TAB 웹 SDK 구현]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Analytics 소스 커넥터 구현]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**참고**: 이 예제에서는 `eVar10`이(가) ID로 표시되어 있다고 가정합니다. 구성의 경우 조직의 구현에 따라 eVar을 변경해야 합니다.

>[!ENDTABS]

### ID 최적화 알고리즘이 예상대로 &quot;작동&quot; 중이 아닙니다.

**문제 해결 단계**

[ID 최적화 알고리즘](./identity-optimization-algorithm.md)에 대한 설명서와 지원되는 그래프 구조 유형을 참조하십시오.

* 지원되는 그래프 구조의 예는 [그래프 구성 안내서](./example-configurations.md)를 참조하십시오.
* 지원되지 않는 그래프 구조의 예는 [구현 안내서](./implementation-guide.md#appendix)를 읽을 수도 있습니다. 다음과 같은 두 가지 상황이 발생할 수 있습니다.
   * 모든 프로필에 단일 네임스페이스가 없습니다.
   * [&quot;댕글링 ID&quot;](./implementation-guide.md#dangling-loginid-scenario) 시나리오가 발생합니다. 이 시나리오에서는 ID 서비스가 댕글링 ID가 그래프의 개인 엔티티와 연결되어 있는지 확인할 수 없습니다.

UI의 [그래프 시뮬레이션 도구](./graph-simulation.md)를 사용하여 이벤트를 시뮬레이션하고 고유한 네임스페이스와 네임스페이스 우선 순위 설정을 구성할 수도 있습니다. 이렇게 하면 ID 최적화 알고리즘이 어떻게 동작해야 하는지에 대한 기준선 이해를 돕는 데 도움이 될 수 있습니다.

시뮬레이션 결과가 그래프 동작 예상과 일치하면 [ID 설정](./identity-settings-ui.md)이 시뮬레이션에서 구성한 설정과 일치하는지 확인할 수 있습니다.

### ID 설정을 구성한 후에도 샌드박스에 축소된 그래프가 표시됩니다

ID 그래프는 구성된 고유 네임스페이스와 네임스페이스 우선 순위 _after_&#x200B;를 준수합니다. 설정이 저장되었습니다. 새 설정을 저장하는 _이전_&#x200B;에 존재하는 &quot;축소된&quot; 그래프는 축소된 그래프가 업데이트되도록 새 데이터가 수집될 때까지 영향을 받지 않습니다. 네임스페이스 우선 순위가 변경된 후에도 실시간 고객 프로필에 있는 이벤트 조각의 기본 ID는 업데이트되지 않습니다.

**문제 해결 단계**

[ID 그래프 뷰어](../features/identity-graph-viewer.md)를 사용하여 그래프가 설정 전후에 수집되었는지 여부를 확인할 수 있습니다. ID 서비스에서 그래프를 수집한 시기를 확인하려면 [!UICONTROL 링크 속성]에서 마지막으로 업데이트된 타임스탬프를 검사하십시오. 타임스탬프가 구성 전이면 기능을 활성화하기 전에 &quot;축소된&quot; 그래프가 생성되었음을 나타냅니다.

![예제 그래프가 있는 ID 그래프 뷰어입니다.](../images/troubleshooting/graph_viewer.png)

### 내 샌드박스에 &quot;축소된&quot; 그래프가 몇 개 있는지 알고 싶습니다

ID 및 그래프 수 등 ID 그래프의 상태에 대한 통찰력에 ID 대시보드를 사용합니다. 축소된 그래프 수는 지표 &quot;여러 네임스페이스가 있는 그래프 수&quot;를 참조하십시오. 그래프는 동일한 네임스페이스를 가진 두 개 이상의 ID를 포함합니다. 샌드박스에 데이터가 없고 고유한 네임스페이스(예: CRMID)가 있다고 가정할 경우 두 개 이상의 CRMID가 있는 그래프가 0이어야 합니다. 아래 예에는 두 개 이상의 이메일 주소를 포함하는 두 개의 그래프가 있습니다.

![ID 수, 그래프 수, 네임스페이스별 수, 크기별 그래프 수 및 두 개 이상의 네임스페이스를 가진 그래프의 그래프 수에 대한 지표가 있는 ID 대시보드입니다.](../images/troubleshooting/identity_dashboard.png)

아래 쿼리를 실행하여 데이터 레이크의 [프로필 스냅숏 내보내기 데이터 세트](../../dashboards/query.md)에서 자세한 분류를 찾을 수 있습니다.

>[!NOTE]
>
>* `dataset_name`을(를) 데이터 세트의 실제 이름으로 바꾸십시오.
>
>* 카운트가 정확하게 일치하지 않을 수 있습니다. ID 대시보드는 ID 그래프 수를 기반으로 하며 다음 쿼리는 두 개 이상의 ID가 있는 프로필 수를 기반으로 합니다. 데이터는 서비스에서 독립적으로 처리 및 업데이트됩니다.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

프로필 스냅샷 내보내기 데이터 세트에서 다음 쿼리를 사용하여 &quot;축소된&quot; 그래프에서 샘플 ID를 얻을 수 있습니다.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>위에 나열된 두 쿼리는 샌드박스가 공유 디바이스 중간 접근 방식에 대해 활성화되지 않은 경우 예상 결과를 산출하며 ID 그래프 연결 규칙과 다르게 동작합니다.

## 자주 묻는 질문 {#faq}

이 섹션에서는 ID 그래프 연결 규칙에 대한 FAQ 응답 목록을 간략하게 설명합니다.

## ID 최적화 알고리즘 {#identity-optimization-algorithm}

[ID 최적화 알고리즘](./identity-optimization-algorithm.md)에 대한 FAQ에 대한 답변을 보려면 이 섹션을 참조하십시오.

### 각 비즈니스 유니트에 대한 CRMID(B2C CRMID, B2B CRMID)가 있지만, 모든 프로필에 고유한 네임스페이스가 없습니다. B2C CRMID 및 B2B CRMID를 고유으로 표시하고 ID 설정을 활성화하면 어떻게 됩니까?

이 시나리오는 지원되지 않습니다. 따라서 사용자가 B2C CRMID를 사용하여 로그인하고 다른 사용자가 B2B CRMID를 사용하여 로그인하는 경우 그래프가 축소되는 것을 볼 수 있습니다. 자세한 내용은 구현 페이지의 [단일 사용자 네임스페이스 요구 사항](./implementation-guide.md#single-person-namespace-requirement)에 대한 섹션을 참조하십시오.

### ID 최적화 알고리즘이 축소된 기존 그래프를 &#39;수정&#39;합니까?

축소된 기존 그래프는 새 설정을 저장한 후 이러한 그래프가 업데이트되는 경우에만 그래프 알고리즘의 영향을 받습니다(&#39;fixed&#39;).

### 동일한 디바이스를 사용하여 두 사람이 로그아웃하면 이벤트는 어떻게 됩니까? 모든 이벤트가 마지막으로 인증된 사용자에게 전송됩니까?

* 익명 이벤트(실시간 고객 프로필에서 ECID를 기본 ID로 사용하는 이벤트)는 마지막으로 인증된 사용자에게 전송됩니다. ECID가 (ID 서비스에서) 마지막으로 인증된 사용자의 CRMID에 연결되기 때문입니다.
* 인증된 모든 이벤트(CRMID가 기본 ID로 정의된 이벤트)는 사용자에게 유지됩니다.

자세한 내용은 [경험 이벤트에 대한 기본 ID 확인](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events)에 대한 안내서를 참조하십시오.

### ECID가 한 개인에서 다른 개인으로 전송되는 경우 Adobe Journey Optimizer의 여정은 어떻게 영향을 받습니까?

마지막으로 인증된 사용자의 CRMID는 ECID(공유 장치)에 연결됩니다. ECID는 사용자 행동을 기반으로 한 개인에서 다른 개인으로 재할당할 수 있습니다. 영향은 여정이 구성되는 방식에 따라 다르므로, 고객은 개발 샌드박스 환경에서 여정을 테스트하여 동작을 확인하는 것이 중요합니다.

강조할 주요 사항은 다음과 같습니다.

* 프로필이 여정에 들어오면 ECID 재할당으로 인해 프로필이 여정 중간에 종료되지 않습니다.
   * 여정 종료는 그래프 변경에 의해 트리거되지 않습니다.
* 프로필이 더 이상 ECID와 연결되어 있지 않으면 대상 자격을 사용하는 조건이 있는 경우 여정 경로가 변경될 수 있습니다.
   * ECID를 제거하면 프로필과 연관된 이벤트가 변경될 수 있으며, 이로 인해 대상 자격이 변경될 수 있습니다.
* 여정 재입력은 여정 속성에 따라 다릅니다.
   * 여정 재입력을 비활성화하면 해당 여정에서 프로필이 종료되면 91일 동안(전역 여정 시간 초과 기준) 동일한 프로필이 재입력되지 않습니다.
* 여정이 ECID 네임스페이스로 시작하는 경우 입력하는 프로필과 작업을 수신하는 프로필(예: 이메일, 오퍼)는 여정 설계 방식에 따라 다를 수 있습니다.
   * 예를 들어 작업 간에 대기 조건이 있고 대기 기간 동안 ECID가 전송되는 경우 다른 프로필이 타겟팅될 수 있습니다.
   * 이 기능을 사용하면 ECID가 더 이상 하나의 프로필에 항상 연결되어 있지 않습니다.
   * CRMID(개인 네임스페이스)로 여정을 시작하는 것이 좋습니다.

>[!TIP]
>
>여정은 고유하지 않은 네임스페이스가 다른 사용자에게 다시 할당될 수 있으므로 고유한 네임스페이스가 있는 프로필을 조회해야 합니다.
>
>* ECID 및 고유하지 않은 이메일/전화 네임스페이스는 한 사람에서 다른 사람으로 이동할 수 있습니다.
>* 여정에게 대기 조건이 있고 이러한 고유하지 않은 네임스페이스를 사용하여 여정에서 프로필을 조정하는 경우 여정 메시지가 잘못된 사람에게 전송될 수 있습니다.

## 네임스페이스 우선순위

[네임스페이스 우선 순위](./namespace-priority.md)에 대한 FAQ에 대한 답변은 이 섹션을 참조하십시오.

### 내 ID 설정을 활성화했습니다. 설정을 활성화한 후 사용자 지정 네임스페이스를 추가하려면 내 설정은 어떻게 됩니까?

네임스페이스에는 사람 네임스페이스와 장치/쿠키 네임스페이스의 두 가지 &#39;버킷&#39;이 있습니다. 새로 만든 사용자 지정 네임스페이스는 각 &#39;버킷&#39;에서 우선 순위가 가장 낮으므로 이 새 사용자 지정 네임스페이스가 기존 데이터 수집에 영향을 주지 않습니다.

### 실시간 고객 프로필이 identityMap에서 더 이상 &#39;기본&#39; 플래그를 사용하지 않는 경우 이 값을 계속 보내야 합니까?

예. identityMap의 &#39;기본&#39; 플래그를 다른 서비스에서 사용합니다. 자세한 내용은 [다른 Experience Platform 서비스에 대한 네임스페이스 우선 순위의 의미](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services)에 대한 안내서를 참조하십시오.

### 실시간 고객 프로필의 프로필 레코드 데이터 세트에 네임스페이스 우선 순위가 적용됩니까?

아니요. 네임스페이스 우선 순위는 XDM ExperienceEvent 클래스를 사용하는 경험 이벤트 데이터 세트에만 적용됩니다.

### 이 기능은 그래프당 50개의 ID라는 ID 그래프 가드레일과 어떻게 연동됩니까? 네임스페이스 우선 순위가 이 시스템 정의 가드레일에 영향을 줍니까?

개인 실체 표상을 보장하기 위해 신원 최적화 알고리즘이 우선 적용될 것이다. 그런 다음 그래프가 [ID 그래프 보호](../guardrails.md)(그래프당 50ID)을(를) 초과하려고 하면 이 논리가 적용됩니다. 네임스페이스 우선 순위는 50 ID/그래프 가드레일의 삭제 논리에 영향을 주지 않습니다.

## 테스트

ID 그래프 연결 규칙의 테스트 및 디버깅 기능에 대한 FAQ에 대한 답변을 보려면 이 섹션을 참조하십시오.

### 개발 샌드박스 환경에서 테스트해야 하는 시나리오 중 일부는 무엇입니까?

일반적으로 개발 샌드박스에서 테스트하는 것은 프로덕션 샌드박스에서 실행하려는 사용 사례를 모방해야 합니다. 포괄적인 테스트를 수행할 때 확인할 몇 가지 주요 영역에 대해서는 다음 표를 참조하십시오.

| 테스트 사례 | 테스트 단계 | 예상 결과 |
| --- | --- | --- |
| 정확한 개인 엔티티 표시 | <ul><li>익명 검색 흉내</li><li>동일한 디바이스를 사용하여 두 사람(John, Jane)이 로그인하는 것처럼 가장합니다.</li></ul> | <ul><li>John과 Jane은 모두 해당 속성 및 인증된 이벤트에 연결되어야 합니다.</li><li>마지막으로 인증된 사용자는 익명 브라우징 이벤트에 연결되어야 합니다.</li></ul> |
| 세그먼테이션 | 4개의 세그먼트 정의를 만듭니다(**참고**: 각 세그먼트 정의 쌍에는 일괄 처리 및 다른 스트리밍을 사용하여 평가된 한 쌍이 있어야 합니다.) <ul><li>세그먼트 정의 A: John의 인증된 이벤트 및/또는 속성에 따른 세그먼트 자격.</li><li>세그먼트 정의 B: Jane의 인증된 이벤트 및/또는 속성에 따른 세그먼트 자격.</li></ul> | John과 Jane은 공유 장치 시나리오에 관계없이 항상 해당 세그먼트에 대한 자격이 있어야 합니다. |
| Adobe Journey Optimizer의 대상 자격/단일 여정 | <ul><li>대상 자격 활동(위에서 만든 스트리밍 세분화 등)으로 시작하는 여정을 만듭니다.</li><li>단일 이벤트로 시작하는 여정을 만듭니다. 이 단일 이벤트는 인증된 이벤트여야 합니다.</li><li>이러한 여정을 만들 때 재입력을 비활성화해야 합니다.</li></ul> | <ul><li>공유 장치 시나리오에 관계없이 John과 Jane은 입력해야 하는 각 여정을 트리거해야 합니다.</li><li>ECID가 다시 전송될 때 John과 Jane은 여정에 다시 들어오면 안 됩니다.</li></ul> |

{style="table-layout:auto"}

### 이 기능이 예상대로 작동하는지 확인하려면 어떻게 해야 합니까?

[그래프 시뮬레이션 도구](./graph-simulation.md)를 사용하여 기능이 개별 그래프 수준에서 작동하는지 확인하십시오.

샌드박스 수준에서 기능의 유효성을 검사하려면 ID 대시보드의 [!UICONTROL 여러 네임스페이스에 대한 그래프 개수] 섹션을 참조하십시오.