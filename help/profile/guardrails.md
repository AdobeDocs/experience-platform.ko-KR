---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;보호 기능;지침;제한;엔티티;기본 엔티티;차원 엔티티;
title: 실시간 고객 프로필 데이터에 대한 기본 보호 기능
solution: Experience Platform
product: experience platform
type: Documentation
description: 'Adobe Experience Platform은 기존의 관계형 데이터 모델과 다른 고도로 비정규화된 하이브리드 데이터 모델을 사용합니다. 이 문서는 최적의 시스템 성능을 위해 프로필 데이터를 모델링하는 데 도움이 되는 기본 사용 및 속도 제한을 제공합니다. '
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 8a343ad275dcfc33eb304e3fc19d375b81277448
workflow-type: tm+mt
source-wordcount: '1941'
ht-degree: 5%

---

# 기본 보호 기능 [!DNL Real-time Customer Profile] 데이터

Adobe Experience Platform을 사용하면 실시간 고객 프로필 형태로 행동 인사이트와 고객 속성을 기반으로 개인화된 크로스 채널 경험을 제공할 수 있습니다. 프로필에 대한 이러한 새로운 접근 방식을 지원하기 위해 Experience Platform은 기존의 관계형 데이터 모델과 다른 고도로 비정규화된 하이브리드 데이터 모델을 사용합니다.

이 문서는 최적의 시스템 성능을 위해 프로필 데이터를 모델링하는 데 도움이 되는 기본 사용 및 속도 제한을 제공합니다. 다음 보호 기능을 검토할 때 데이터를 올바르게 모델링했다고 가정합니다. 데이터를 모델링하는 방법에 대한 질문이 있는 경우 고객 서비스 담당자에게 문의하십시오.

>[!NOTE]
>
>대부분의 고객은 이러한 기본 제한을 초과하지 않습니다. 사용자 지정 제한에 대해 알아보려면 고객 지원 담당자에게 문의하십시오.

## 시작하기

다음 Experience Platform 서비스는 실시간 고객 프로필 데이터 모델링과 관련되어 있습니다.

* [[!DNL Real-time Customer Profile]](home.md): 여러 소스의 데이터를 사용하여 통합 소비자 프로필을 만들 수 있습니다.
* [ID](../identity-service/home.md): 플랫폼에 수집하여 다양한 데이터 소스에서 ID를 전달합니다.
* [스키마](../xdm/home.md): XDM(Experience Data Model) 스키마는 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [세그먼트](../segmentation/home.md): 플랫폼 내의 세그먼테이션 엔진은 고객 행동과 속성을 기반으로 고객 프로필에서 세그먼트를 만드는 데 사용됩니다.

## 제한 유형

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

* **소프트 제한:** 소프트 한도를 넘지 않을 수 있지만, 소프트 한계는 시스템 성능에 대한 권장 지침을 제공합니다.

* **하드 제한:** 하드 제한은 절대 최대값을 제공합니다.

>[!NOTE]
>
>이 문서에 설명된 제한은 지속적으로 개선되고 있습니다. 업데이트를 정기적으로 확인하십시오. 사용자 지정 제한에 대해 알아보려면 고객 지원 담당자에게 문의하십시오.

## 데이터 모델 제한

실시간 고객 프로필 데이터를 모델링할 때 다음과 같은 보호 기능이 권장되는 제한을 제공합니다. 기본 엔티티 및 차원 엔티티에 대한 자세한 내용은 [엔티티 유형](#entity-types) 부록.

### 기본 엔티티 보호 기능

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| XDM 개별 프로필 클래스 데이터 세트 | 20 | 소프트 | XDM 개별 프로필 클래스를 활용하는 최대 20개의 데이터 세트가 권장됩니다. |
| XDM ExperienceEvent 클래스 데이터 세트 | 20년 | 소프트 | XDM ExperienceEvent 클래스를 활용하는 최대 20개의 데이터 세트가 권장됩니다. |
| 프로필에 대해 활성화된 Adobe Analytics 보고서 세트 데이터 세트 | 1 | 소프트 | 프로필에 대해 최대 1개의 Analytics 보고서 세트 데이터 세트를 활성화해야 합니다. 프로필에 대해 여러 Analytics 보고서 세트 데이터 세트를 활성화하려고 하면 데이터 품질에 의도하지 않은 결과가 발생할 수 있습니다. 자세한 내용은 [Adobe Analytics 데이터 세트](#aa-datasets) 부록. |
| 다중 엔티티 관계 | 5 | 소프트 | 기본 엔티티와 차원 엔티티 간에 정의된 최대 5개의 다중 엔티티 관계가 권장됩니다. 기존 관계가 제거되거나 비활성화될 때까지 추가 관계 매핑을 수행하지 마십시오. |
| 다중 엔티티 관계에 사용되는 ID 필드에 대한 JSON 깊이 | 4 | 소프트 | 다중 엔티티 관계에 사용되는 ID 필드에 대해 권장되는 최대 JSON 깊이는 4입니다. 즉, 중첩된 스키마에서 4개 수준 이상이 중첩된 필드를 관계에서 ID 필드로 사용하지 않아야 합니다. |
| 프로필 조각의 배열 카디널리티 | &lt;=500 | 소프트 | 프로필 조각의 최적 배열 카디널리티는 시간 독립적인 데이터(시간 구분)이며 &lt;=500입니다. |
| ExperienceEvent의 배열 카디널리티 | &lt;=10 | 소프트 | ExperienceEvent(시계열 데이터)의 최적 배열 카디널리티는 10보다 작습니다. |
| 개별 프로필 ID 그래프의 ID 수 | 50 | 하드 | **개별 프로필에 대한 ID 그래프의 최대 ID 수는 50개입니다.** ID가 50개가 넘는 모든 프로필은 세그멘테이션, 내보내기 및 조회에서 제외됩니다. |

{style=&quot;table-layout:auto&quot;}

### Dimension 엔티티 가드 레일

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 비시계열 데이터는 허용되지 않습니다[!DNL XDM Individual Profile] 개체 | 0 | 하드 | **시계열 데이터는 비직렬로 사용할 수 없습니다[!DNL XDM Individual Profile] 프로필 서비스의 엔티티.** 시계열 데이터 세트가 비-시리즈 데이터 세트와 연결된 경우[!DNL XDM Individual Profile] ID, 데이터 세트에 대해 를 활성화하지 않아야 합니다 [!DNL Profile]. |
| 중첩 관계 없음 | 0 | 소프트 | 두 비-서로 관계를 만들면 안 됩니다[!DNL XDM Individual Profile] 스키마. 관계를 만드는 기능은 의 일부가 아닌 스키마에는 권장되지 않습니다 [!DNL Profile] 결합 스키마. |
| 기본 ID 필드에 대한 JSON 깊이 | 4 | 소프트 | 기본 ID 필드에 대한 권장 최대 JSON 깊이는 4입니다. 즉, 중첩된 스키마에서 4개 수준 이상으로 중첩된 경우 필드를 기본 ID로 선택하면 안 됩니다. 중첩 수준이 4번째인 필드는 기본 ID로 사용할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 크기 제한

데이터 크기를 참조하고 의도한 대로 수집, 저장 및 쿼리할 수 있는 데이터에 대한 권장 제한을 제공합니다. 기본 엔티티 및 차원 엔티티에 대한 자세한 내용은 [엔티티 유형](#entity-types) 부록.

>[!NOTE]
>
>데이터 크기는 수집 시 JSON에서 압축되지 않은 데이터로 측정됩니다.

### 기본 엔티티 보호 기능

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 최대 ExperienceEvent 크기 | 10KB | 하드 | **이벤트의 최대 크기는 10KB입니다.** 수집은 계속되지만 10KB보다 큰 이벤트는 삭제됩니다. |
| 최대 프로필 레코드 크기 | 100KB | 하드 | **프로필 레코드의 최대 크기는 100KB입니다.** 수집은 계속되지만 100KB보다 큰 프로필 레코드는 삭제됩니다. |
| 최대 프로필 조각 크기 | 50MB | 하드 | **단일 프로필 조각의 최대 크기는 50MB입니다.** 세그먼테이션, 내보내기 및 조회는 모든 항목에 대해 실패할 수 있습니다 [프로필 조각](#profile-fragments) 50MB보다 큽니다. |
| 최대 프로필 저장소 크기 | 50MB | 소프트 | **저장된 프로필의 최대 크기는 50MB입니다.** 새로 추가 [프로필 조각](#profile-fragments) 50MB보다 큰 프로필은 시스템 성능에 영향을 줍니다. 예를 들어, 프로필에 50MB의 단일 조각이 포함되어 있거나 총 크기가 50MB인 여러 데이터 세트에 걸쳐 여러 조각을 포함할 수 있습니다. 50MB보다 큰 단일 조각 또는 총 50MB를 초과하는 복합 조각으로 프로필을 저장하려고 하면 시스템 성능에 영향을 줍니다. |
| 일별로 수집된 프로필 또는 ExperienceEvent 배치 수 | 90 | 소프트 | **일별 수집된 프로필 또는 ExperienceEvent 일괄 처리의 최대 수는 90개입니다.** 즉, 매일 수집된 프로필 및 ExperienceEvent 일괄 처리의 합계는 90을 초과할 수 없습니다. 추가 배치를 섭취하는 것은 시스템 성능에 영향을 줍니다. |

{style=&quot;table-layout:auto&quot;}

### Dimension 엔티티 가드 레일

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 모든 차원 엔터티의 총 크기 | 5GB | 소프트 | 모든 차원 엔터티에 대한 권장 총 크기는 5GB입니다. 큰 차원 엔티티를 섭취하는 것은 시스템 성능에 영향을 줄 수 있습니다. 예를 들어 10GB 제품 카탈로그를 차원 엔티티로 로드하려는 것은 권장되지 않습니다. |
| 차원 엔티티 스키마당 데이터 세트 | 5개 | 소프트 | 각 차원 엔티티 스키마와 연결된 최대 5개의 데이터 세트가 권장됩니다. 예를 들어 &quot;제품&quot;에 대한 스키마를 만들고 5개의 기여 데이터 세트를 추가하는 경우, 제품 스키마에 연결된 6번째 데이터 세트를 만들면 안 됩니다. |
| 일별로 수집된 Dimension 엔티티 배치 | 개체당 4개 | 소프트 | 일당 수집된 권장 차원 엔티티 일괄 처리 수는 엔티티당 4개입니다. 예를 들어 제품 카탈로그에 대한 업데이트를 하루에 최대 4회까지 수집할 수 있습니다. 동일한 엔티티에 대한 추가 차원 엔티티 배치를 섭취하는 것은 시스템 성능에 영향을 줄 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

## 세그먼테이션 보호 기능

이 섹션에 설명된 보호 기능은 Experience Platform 내에서 조직에서 만들 수 있는 세그먼트의 개수 및 특성을 참조할 뿐만 아니라 세그먼트를 대상에 매핑하고 활성화할 수 있습니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --- | --- | --- | --- |
| 샌드박스당 세그먼트 수 | 10,000 | 소프트 | 각 개별 샌드박스에 10,000개 미만의 세그먼트가 있는 한, 조직에는 총 10,000개 이상의 세그먼트가 있을 수 있습니다. 추가 세그먼트를 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. |
| 샌드박스당 스트리밍 세그먼트 | 500 | 소프트 | 각 개별 샌드박스에 500개 미만의 스트리밍 세그먼트가 있는 한, 조직에는 총 500개 이상의 스트리밍 세그먼트가 있을 수 있습니다. 추가 스트리밍 세그먼트를 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. |
| 샌드박스당 세그먼트 일괄 처리 | 10,000 | 소프트 | 각 개별 샌드박스에 10,000개 미만의 배치 세그먼트가 있는 한, 조직에는 총 10,000개 이상의 배치 세그먼트가 있을 수 있습니다. 추가 배치 세그먼트를 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

## 부록

이 섹션에서는 이 문서의 제한에 대한 추가 세부 정보를 제공합니다.

### 엔티티 유형

다음 [!DNL Profile] 저장소 데이터 모델은 두 가지 핵심 엔티티 유형으로 구성됩니다.

* **기본 엔터티:** 기본 엔티티 또는 프로필 엔티티는 데이터를 함께 병합하여 개인에 대한 &quot;단일 진실의 소스&quot;를 만듭니다. 이 통합 데이터는 &quot;결합 보기&quot;라고 하는 것을 사용하여 표시됩니다. 결합 보기는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 결합 스키마에 집계합니다. 에 대한 결합 스키마 [!DNL Real-time Customer Profile] 는 모든 프로필 속성 및 행동 이벤트에 대한 컨테이너 역할을 하는 비정규화된 하이브리드 데이터 모델입니다.

   시간 독립적인 속성(&quot;레코드 데이터&quot;라고도 함)은 [!DNL XDM Individual Profile], 시간 시리즈 데이터(&quot;이벤트 데이터&quot;라고도 함)는 를 사용하여 모델링됩니다 [!DNL XDM ExperienceEvent]. 레코드 및 시계열 데이터가 Adobe Experience Platform에서 수집되면 트리거됩니다 [!DNL Real-time Customer Profile] 사용할 수 있도록 활성화된 데이터 수집을 시작합니다. 수집된 상호 작용 및 세부 사항이 많을수록 더 강력한 개별 프로필이 생성됩니다.

   ![](images/guardrails/profile-entity.png)

* **Dimension 엔터티:** 프로필 데이터를 유지 관리하는 프로필 데이터 저장소는 관계형 저장소가 아니지만 Profile에서는 세그먼트를 간소화되고 직관적으로 만들 수 있도록 작은 차원 엔티티와의 통합을 허용합니다. 이 통합을 라고 합니다. [다중 엔티티 세그먼테이션](../segmentation/multi-entity-segmentation.md). 또한 조직은 저장소, 제품 또는 속성과 같이 개인 이외의 항목을 설명하는 XDM 클래스를 정의할 수 있습니다. 이러한 비지원[!DNL XDM Individual Profile] 스키마는 &quot;차원 엔티티&quot;라고 하며, 시계열 데이터를 포함하지 않습니다. Dimension 엔티티는 다중 엔티티 세그먼트 정의를 지원하고 단순화하는 조회 데이터를 제공하며, 세그먼테이션 엔진이 최적의 처리를 위해 전체 데이터 세트를 메모리에 로드할 수 있을 만큼 작아야 합니다(빠른 포인트 조회).

   ![](images/guardrails/profile-and-dimension-entities.png)

### 프로필 조각

이 문서에는 &quot;프로필 조각&quot;을 참조하는 몇 가지 보호 기능이 있습니다. Experience Platform에서 여러 프로필 조각이 병합되어 실시간 고객 프로필을 형성합니다. 각 조각은 고유한 기본 ID와 주어진 데이터 세트 내에서 해당 ID에 대한 해당 레코드 또는 이벤트 데이터를 나타냅니다. 프로필 조각에 대한 자세한 내용은 [프로필 개요](home.md#profile-fragments-vs-merged-profiles).

### 병합 정책 {#merge-policies}

여러 소스에서 데이터를 함께 가져올 때 병합 정책은 Platform이 데이터 우선 순위가 지정되는 방식과 해당 통합 보기를 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 해당 단일 고객과 관련된 여러 프로필 조각이 있습니다. 이러한 조각을 Platform에 수집하면 병합되어 해당 고객에 대한 단일 프로필을 만듭니다. 여러 소스의 데이터가 충돌하면 병합 정책에 따라 개별 프로필에 포함할 정보가 결정됩니다. 병합 정책에 대해 자세히 알아보려면 [정책 병합 개요](merge-policies/overview.md).

### Platform의 Adobe Analytics 보고서 세트 데이터 세트 {#aa-datasets}

프로필에 대해 최대 1개의 Adobe Analytics 보고서 세트 데이터 세트를 활성화해야 합니다. 이것은 소프트 제한입니다. 즉, 프로필에 두 개 이상의 Analytics 데이터 세트를 활성화할 수 있지만, 데이터에 의도하지 않은 결과가 발생할 수 있으므로 권장되지 않습니다. 이것은 Experience Platform의 데이터에 대한 의미 체계 구조를 제공하고 데이터 해석에서 일관성을 허용하는 XDM(Experience Data Model) 스키마, Adobe Analytics의 eVar 및 전환 변수의 사용자 지정 가능한 특성 간의 차이 때문입니다.

예를 들어, Adobe Analytics에서 단일 조직에는 여러 보고서 세트가 있을 수 있습니다. 보고서 세트 A가 eVar 4을 &quot;내부 검색어&quot;로 지정하고 보고서 세트 B가 eVar 4을 &quot;참조 도메인&quot;으로 지정하는 경우 이 값이 모두 프로필의 동일한 필드에 수집되어 혼동 및 데이터 품질이 저하됩니다.
