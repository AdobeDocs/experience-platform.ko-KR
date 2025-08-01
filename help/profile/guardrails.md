---
title: 실시간 고객 프로필 데이터 및 세분화를 위한 기본 보호
solution: Experience Platform
product: experience platform
type: Documentation
description: Real-Time CDP 기능의 최적 사용을 보장하기 위해 프로필 데이터 및 세분화에 대한 성능 및 시스템 적용 가드레일에 대해 알아봅니다.
exl-id: 33ff0db2-6a75-4097-a9c6-c8b7a9d8b78c
source-git-commit: 1536201961211aeb747e418794196c146d86e869
workflow-type: tm+mt
source-wordcount: '2636'
ht-degree: 2%

---

# [!DNL Real-Time Customer Profile] 데이터 및 세분화에 대한 기본 보호 기능

Adobe Experience Platform을 사용하면 행동 통찰력 및 고객 속성을 기반으로 개인화된 크로스 채널 경험을 실시간 고객 프로필 형태로 제공할 수 있습니다. 프로필에 대한 이러한 새로운 접근 방식을 지원하기 위해 Experience Platform은 기존의 관계형 데이터 모델과 다른 고도로 비정규화된 하이브리드 데이터 모델을 사용합니다.

>[!IMPORTANT]
>
>이 보호 기능 페이지 외에 실제 사용 제한에 대해 판매 주문에서 라이선스 자격 및 해당 [제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions.html)을(를) 확인하십시오.

이 문서는 최적의 시스템 성능을 위해 프로필 데이터를 모델링하는 데 도움이 되는 기본 사용 및 속도 제한을 제공합니다. 다음 가드레일을 검토할 때 데이터를 올바르게 모델링했다고 가정합니다. 데이터 모델링 방법에 대한 질문이 있는 경우 고객 서비스 담당자에게 문의하십시오.

>[!NOTE]
>
>대부분의 고객은 이러한 기본 제한을 초과하지 않습니다. 사용자 지정 제한에 대해 알아보려면 고객 지원 센터 담당자에게 문의하십시오.

## 시작

다음 Experience Platform 서비스는 실시간 고객 프로필 데이터 모델링과 관련되어 있습니다.

* [[!DNL Real-Time Customer Profile]](home.md): 여러 소스의 데이터를 사용하여 통합 소비자 프로필을 만듭니다.
* [ID](../identity-service/home.md): Bridge ID가 Experience Platform에 수집될 때 서로 다른 데이터 소스의 ID입니다.
* [스키마](../xdm/home.md): XDM(Experience Data Model) 스키마는 Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [대상](../segmentation/home.md): Experience Platform의 세그먼테이션 엔진은 고객 행동 및 특성을 기반으로 고객 프로필에서 대상을 만드는 데 사용됩니다.

## 제한 유형

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

| 보호 유형 | 설명 |
| -------------- | ----------- |
| **성능 보호(소프트 제한)** | 성능 보호는 사용 사례의 범위와 관련된 사용 제한입니다. 성능 가드레일을 초과하면 성능 저하 및 지연이 발생할 수 있습니다. Adobe은 이러한 성능 저하에 대한 책임이 없습니다. 성능 가드레일을 지속적으로 초과하는 고객은 성능 저하를 방지하기 위해 추가 용량의 라이센스를 선택할 수 있습니다. |
| **시스템 적용 보호 기능(하드 제한)** | 시스템에서 적용되는 가드레일은 Real-Time CDP UI 또는 API에 의해 적용됩니다. 이는 UI 및 API가 귀하를 차단하거나 오류를 반환하므로 초과할 수 없는 제한입니다. |

{style="table-layout:auto"}

>[!NOTE]
>
>이 문서에 설명된 제한 사항이 지속적으로 개선되고 있습니다. 업데이트를 정기적으로 확인하십시오. 사용자 지정 제한에 대한 자세한 내용은 고객 지원 센터에 문의하십시오.

## 데이터 모델 제한

다음 가드레일은 실시간 고객 프로필 데이터를 모델링할 때 권장되는 제한을 제공합니다. 기본 엔터티 및 차원 엔터티에 대한 자세한 내용은 부록의 [엔터티 형식](#entity-types)에 대한 섹션을 참조하십시오.

![Adobe Experience Platform의 프로필 데이터에 대한 서로 다른 보호 기능을 보여 주는 다이어그램입니다.](./images/guardrails/profile-guardrails.png)

### 기본 엔티티 보호

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| XDM 개별 프로필 클래스 데이터 세트 | 20 | 성능 보호 | XDM 개별 프로필 클래스를 활용하는 데이터 세트는 최대 20개까지 사용하는 것이 좋습니다. |
| XDM ExperienceEvent 클래스 데이터 세트 | 20 | 성능 보호 | XDM ExperienceEvent 클래스를 활용하는 데이터 세트는 최대 20개까지 사용하는 것이 좋습니다. |
| 프로필에 대해 Adobe Analytics 보고서 세트 데이터 세트 활성화됨 | 1 | 성능 보호 | 프로필에 대해 최대 1개의 Analytics 보고서 세트 데이터 세트를 활성화해야 합니다. 프로필에 대해 여러 Analytics 보고서 세트 데이터 세트를 활성화하려고 하면 데이터 품질에 의도하지 않은 결과가 발생할 수 있습니다. 자세한 내용은 부록의 [Adobe Analytics 데이터 세트](#aa-datasets)에 대한 섹션을 참조하십시오. |
| 다중 엔티티 관계 | 5 | 성능 보호 | 기본 엔티티와 차원 엔티티 간에 최대 5개의 다중 엔티티 관계가 정의되는 것이 좋습니다. 기존 관계가 제거되거나 비활성화될 때까지 추가 관계 매핑을 수행하지 마십시오. |
| 다중 엔티티 관계에 사용되는 ID 필드의 JSON 깊이 | 4 | 성능 보호 | 다중 엔티티 관계에 사용되는 ID 필드에 대한 권장 최대 JSON 깊이는 4입니다. 즉, 많이 중첩된 스키마에서 4개 수준 이상 깊게 중첩된 필드를 관계의 ID 필드로 사용하면 안 됩니다. |
| 프로필 조각의 배열 카디널리티 | &lt;=500 | 성능 보호 | 프로필 조각(시간에 구애받지 않는 데이터)에서 최적의 배열 카디널리티는 &lt;=500입니다. |
| ExperienceEvent의 배열 카디널리티 | &lt;=10 | 성능 보호 | ExperienceEvent(시계열 데이터)에서 최적의 배열 카디널리티는 10 미만입니다. |
| 개별 프로필 ID 그래프의 ID 수 | 50 | 시스템 강제 보호 | **개별 프로필에 대한 ID 그래프의 최대 ID 수는 50개입니다.** ID가 50개를 초과하는 프로필은 세분화, 내보내기 및 조회에서 제외됩니다. 자세한 내용은 [ID 삭제 논리 이해](../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

### Dimension 엔티티 보호

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| [!DNL XDM Individual Profile]개가 아닌 엔터티에 대해 허용되는 시계열 데이터가 없습니다. | 0 | 시스템 강제 보호 | **시계열 데이터는 Profile Service에서 [!DNL XDM Individual Profile]이(가) 아닌 엔터티에 사용할 수 없습니다.** 시계열 데이터 세트가 [!DNL XDM Individual Profile]이(가) 아닌 ID와 연결된 경우 [!DNL Profile]에 대해 데이터 세트를 사용할 수 없습니다. |
| 중첩 관계 없음 | 0 | 성능 보호 | [!DNL XDM Individual Profile]이 아닌 두 스키마 간에 관계를 만들면 안 됩니다. [!DNL Profile] 유니온 스키마에 포함되지 않은 스키마에는 관계를 만드는 기능을 사용하지 않는 것이 좋습니다. |
| 기본 ID 필드에 대한 JSON 깊이 | 4 | 성능 보호 | 기본 ID 필드에 대한 권장 최대 JSON 깊이는 4입니다. 즉, 높은 수준으로 중첩된 스키마에서는 필드가 4개 수준 이상 깊게 중첩된 경우 이 필드를 기본 ID로 선택하면 안 됩니다. 네 번째 중첩된 수준에 있는 필드는 기본 ID로 사용할 수 있습니다. |

{style="table-layout:auto"}

## 데이터 크기 제한

다음 가드레일은 데이터 크기를 나타내며 의도한 대로 수집, 저장 및 쿼리할 수 있는 데이터에 대한 권장 제한을 제공합니다. 기본 엔터티 및 차원 엔터티에 대한 자세한 내용은 부록의 [엔터티 형식](#entity-types)에 대한 섹션을 참조하십시오.

>[!NOTE]
>
>데이터 크기는 수집 시 JSON에서 압축되지 않은 데이터로 측정됩니다.

### 기본 엔티티 보호

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| 최대 ExperienceEvent 크기 | 10KB | 시스템 강제 보호 | **이벤트의 최대 크기는 10KB입니다.** 수집은 계속되지만 10KB보다 큰 이벤트는 모두 삭제됩니다. |
| 최대 프로필 레코드 크기 | 100KB | 시스템 강제 보호 | **프로필 레코드의 최대 크기는 100KB입니다.** 수집은 계속되지만 100KB보다 큰 프로필 레코드는 삭제됩니다. |
| 최대 프로필 조각 크기 | 50MB | 시스템 강제 보호 | **단일 프로필 조각의 최대 크기는 50MB입니다.50MB보다 큰**&#x200B;프로필 조각[에 대해 ](#profile-fragments) 세분화, 내보내기 및 조회가 실패할 수 있습니다. |
| 최대 프로필 스토리지 크기 | 50MB | 성능 보호 | **저장된 프로필의 최대 크기는 50MB입니다.** 50MB가 넘는 프로필에 새 [프로필 조각](#profile-fragments)을 추가하는 것은 시스템 성능에 영향을 줍니다. 예를 들어 프로필에는 50MB인 단일 조각이 포함되거나 결합된 총 크기가 50MB인 여러 데이터 세트에 여러 조각을 포함할 수 있습니다. 단일 조각이 50MB보다 크거나 총 조각이 50MB를 초과하는 여러 조각을 사용하여 프로필을 저장하려고 하면 시스템 성능에 영향을 줍니다. |
| 하루에 수집된 프로필 또는 ExperienceEvent 배치 수 | 90 | 성능 보호 | **하루에 수집할 수 있는 프로필 또는 ExperienceEvent 일괄 처리의 최대 수는 90개입니다.** 이는 매일 수집된 프로필 및 ExperienceEvent 배치의 합계가 90개를 초과할 수 없음을 의미합니다. 추가 배치를 수집하면 시스템 성능에 영향을 줍니다. |
| 프로필 레코드당 ExperienceEvents 수 | 5000 | 성능 보호 | **프로필 레코드당 최대 ExperienceEvents 수는 5000개입니다.ExperienceEvents가 5000개가 넘는** 프로필은 세그먼테이션과 함께 사용할 때 **최신** 5000 ExperienceEvents만 사용합니다. |

{style="table-layout:auto"}

### Dimension 엔티티 보호

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| 모든 차원 엔티티에 대한 총 크기 | 5GB | 성능 보호 | 모든 차원 엔티티에 대해 권장되는 총 크기는 5GB입니다. 큰 차원 엔티티를 수집하면 시스템 성능에 영향을 줄 수 있습니다. 예를 들어 10GB 제품 카탈로그를 차원 엔티티로 로드하려는 시도는 권장되지 않습니다. |
| 차원 엔티티 스키마당 데이터 세트 | 5 | 성능 보호 | 각 차원 엔티티 스키마와 연결된 데이터 세트는 최대 5개가 권장됩니다. 예를 들어 &quot;제품&quot;에 대한 스키마를 만들고 5개의 기여 데이터 세트를 추가하는 경우 제품 스키마에 연결된 여섯 번째 데이터 세트를 만들면 안 됩니다. |
| 일별로 수집된 Dimension 엔티티 배치 | 엔티티당 4개 | 성능 보호 | 하루에 수집되는 최대 차원 엔티티 배치 권장 수는 엔티티당 4개입니다. 예를 들어 제품 카탈로그에 대한 업데이트를 하루에 최대 4번까지 수집할 수 있습니다. 동일한 엔티티에 대해 추가 차원 엔티티 배치를 수집하면 시스템 성능에 영향을 줄 수 있습니다. |

{style="table-layout:auto"}

## 세그먼테이션 보호 {#segmentation-guardrails}

이 섹션에 설명된 보호 기능은 조직이 Experience Platform 내에서 만들 수 있는 대상의 수와 특성뿐만 아니라 대상을 대상에 매핑하고 활성화하는 방법에 대해 설명합니다.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| 샌드박스당 대상 | 4000 | 성능 보호 | 샌드박스당 최대 4000개의 **활성** 대상을 가질 수 있습니다. 각 **개별** 샌드박스에 4000개 미만의 대상이 있는 한 조직당 4000개 이상의 대상을 가질 수 있습니다. 여기에는 일괄 처리, 스트리밍 및 에지 대상이 포함됩니다. 추가 대상을 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. 세그먼트 빌더를 통해 [대상자 만들기](/help/segmentation/ui/segment-builder.md)에 대해 자세히 알아보세요. |
| 샌드박스당 Edge 대상 | 150 | 성능 보호 | 샌드박스당 최대 150개의 **활성** Edge 대상을 가질 수 있습니다. 각 **개별** 샌드박스에 150개 미만의 Edge 대상이 있는 한 조직당 150개 이상의 Edge 대상을 가질 수 있습니다. 추가 Edge 대상을 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. [Edge 대상](/help/segmentation/methods/edge-segmentation.md)에 대해 자세히 알아보세요. |
| 모든 샌드박스에서 Edge 처리량 | 1500RPS | 성능 보호 | Edge 세그멘테이션은 프로덕션 및 개발 샌드박스에서 Adobe Experience Platform Edge Network으로 들어가는 초당 1500개의 인바운드 이벤트의 결합된 최대 값을 지원합니다. Edge 세그먼테이션은 Adobe Experience Platform Edge Network에 들어간 후 인바운드 이벤트를 처리하는 데 최대 350밀리초가 걸릴 수 있습니다. [Edge 대상](/help/segmentation/methods/edge-segmentation.md)에 대해 자세히 알아보세요. |
| 샌드박스당 스트리밍 대상 | 500 | 성능 보호 | 샌드박스당 최대 500개의 **활성** 스트리밍 대상을 가질 수 있습니다. 각 **개별** 샌드박스에 500개 미만의 스트리밍 대상이 있는 한 조직당 500개 이상의 스트리밍 대상을 가질 수 있습니다. 여기에는 스트리밍 대상과 에지 대상이 모두 포함됩니다. 스트리밍 대상을 추가로 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. [스트리밍 대상](/help/segmentation/methods/streaming-segmentation.md)에 대해 자세히 알아보세요. |
| 모든 샌드박스에서 스트리밍 처리량 | 1500RPS | 성능 보호 | 스트리밍 세그멘테이션은 프로덕션 및 개발 샌드박스에서 초당 1500개의 인바운드 이벤트의 결합된 최대 값을 지원합니다. 스트리밍 세분화는 프로필 멤버십에 자격을 부여하는 데 최대 5분이 걸릴 수 있습니다. [스트리밍 대상](/help/segmentation/methods/streaming-segmentation.md)에 대해 자세히 알아보세요. |
| 샌드박스당 배치 대상 | 4000 | 성능 보호 | 샌드박스당 최대 4000개의 **활성** 일괄 처리 대상을 가질 수 있습니다. 각 **개별** 샌드박스에 4000개 미만의 배치 대상이 있는 한 조직당 4000개 이상의 배치 대상이 있을 수 있습니다. 추가 배치 대상을 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. |
| 샌드박스당 계정 대상자 | 50 | 시스템 강제 보호 | 샌드박스에서 최대 50개의 계정 대상을 만들 수 있습니다. 샌드박스에서 대상 50개에 도달하면 새 계정 대상을 만들 때 **[!UICONTROL 대상 만들기]** 컨트롤이 비활성화됩니다. [계정 대상자](/help/segmentation/types/account-audiences.md)에 대해 자세히 알아보세요. |
| 샌드박스당 게시된 컴포지션 | 10 | 성능 보호 | 샌드박스에 최대 10개의 컴포지션이 게시될 수 있습니다. UI 가이드의 [대상 구성에 대해 자세히 알아보세요](/help/segmentation/ui/audience-composition.md). |
| 최대 대상자 크기 | 30% | 성능 보호 | 대상자의 권장 최대 멤버십은 시스템 총 프로필 수의 30%입니다. 프로필의 30% 이상이 멤버이거나 큰 대상이 여러 개인 대상을 만드는 것은 가능하지만 시스템 성능에 영향을 줍니다. |
| 유연한 대상 평가 실행 | 연간 50개(프로덕션 샌드박스)<br/>연간 100개(개발 샌드박스) | 시스템 강제 보호 | **프로덕션** 샌드박스당 연간 최대 50개의 유연한 대상 평가 실행이 있습니다. **개발** 샌드박스당 연간 최대 100개의 유연한 대상 평가 실행이 있습니다. |
| 유연한 대상 평가 실행 | 일별 2개 | 시스템 강제 보호 | 샌드박스당 하루에 최대 2회의 실행이 있습니다. |
| 유연한 대상 평가 실행당 대상 | 20 | 시스템 강제 보호 | 유연한 대상 평가 실행당 최대 20개의 대상을 가질 수 있습니다. |

{style="table-layout:auto"}

## 예상 가용성

다음 섹션에서는 Real-Time CDP 대상과 같은 다운스트림 서비스의 대상 및 병합 정책에 대한 **예상** 가용성에 대해 간략히 설명합니다.

| 샌드박스 유형 | 시간 |
| ------------ | ---- |
| 기존 샌드박스 | 1시간 |
| 새 샌드박스 | 2시간 |
| 샌드박스를 새로 재설정 | 2시간 |

{style="table-layout:auto"}

## 부록

이 섹션에서는 이 문서의 제한에 대한 추가 세부 정보를 제공합니다.

### 엔티티 유형

[!DNL Profile] 저장소 데이터 모델은 [기본 엔터티](#primary-entity) 및 [차원 엔터티](#dimension-entity)의 두 가지 핵심 엔터티 유형으로 구성됩니다.

#### 기본 엔티티

기본 엔티티 또는 프로필 엔티티는 데이터를 함께 병합하여 개인에 대한 &quot;단일 신뢰할 수 있는 소스&quot;를 구성합니다. 이러한 통합 데이터는 &quot;결합 보기&quot;라고 하는 것을 사용하여 표시됩니다. 유니온 조회는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 유니온 스키마로 집계합니다. [!DNL Real-Time Customer Profile]에 대한 유니온 스키마는 모든 프로필 특성 및 동작 이벤트의 컨테이너 역할을 하는 비정규화된 하이브리드 데이터 모델입니다.

&quot;레코드 데이터&quot;라고도 하는 시간 독립적 특성은 [!DNL XDM Individual Profile]을(를) 사용하여 모델링되지만 &quot;이벤트 데이터&quot;라고도 하는 시계열 데이터는 [!DNL XDM ExperienceEvent]을(를) 사용하여 모델링됩니다. 레코드 및 시계열 데이터가 Adobe Experience Platform에서 수집되면 [!DNL Real-Time Customer Profile]을(를) 트리거하여 사용할 수 있도록 설정된 데이터 수집을 시작합니다. 상호 작용과 세부 사항이 많을수록 개별 프로필이 더 강력해집니다.

![레코드 데이터와 시계열 데이터 간의 차이점을 요약한 인포그래픽입니다.](images/guardrails/profile-entity.png)

#### Dimension 엔티티

프로필 데이터를 유지 관리하는 프로필 데이터 저장소는 관계형 저장소가 아니지만, 프로필에서는 단순하고 직관적인 방식으로 대상자를 만들 수 있도록 작은 차원 엔티티와의 통합을 허용합니다. 이 통합을 [다중 엔티티 세그멘테이션](../segmentation/tutorials/multi-entity-segmentation.md)이라고 합니다.

또한 조직은 상점, 제품 또는 속성과 같이 개인 이외의 항목을 설명하는 XDM 클래스를 정의할 수도 있습니다. XDM 개별 프로필 클래스 이외의 XDM 클래스를 사용하여 모델링되는 이러한 스키마는 &quot;차원 엔티티&quot;(&quot;조회 엔티티&quot;라고도 함)라고 하며 시계열 데이터를 포함하지 않습니다. 차원 엔터티를 나타내는 스키마는 [스키마 관계](../xdm/tutorials/relationship-ui.md)을 사용하여 프로필 엔터티에 연결됩니다.

Dimension 엔티티는 다중 엔티티 세그먼트 정의를 지원 및 간소화하는 조회 데이터를 제공하며 세그먼테이션 엔진이 최적의 처리를 위해 전체 데이터 세트를 메모리에 로드할 수 있을 만큼 작아야 합니다(빠른 포인트 조회).

![프로필 엔터티가 차원 엔터티로 구성되어 있음을 보여 주는 인포그래픽입니다.](images/guardrails/profile-and-dimension-entities.png)

### 프로필 조각

이 문서에는 &quot;프로필 조각&quot;을 참조하는 몇 가지 보호 기능이 있습니다. Experience Platform에서는 여러 프로필 조각이 함께 병합되어 실시간 고객 프로필이 구성됩니다. 각 조각은 고유한 기본 ID와 주어진 데이터 세트 내의 해당 ID에 대한 해당 레코드 또는 전체 이벤트 데이터 세트를 나타냅니다. 프로필 조각에 대한 자세한 내용은 [프로필 개요](home.md#profile-fragments-vs-merged-profiles)를 참조하세요.

### 병합 정책 {#merge-policies}

여러 소스에서 데이터를 결합할 때 병합 정책은 Experience Platform에서 데이터의 우선 순위를 결정하는 데 사용하는 규칙이며, 이러한 통합 보기를 만들기 위해 결합할 데이터와 데이터를 결정합니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 단일 고객과 관련된 여러 프로필 조각이 있습니다. 이러한 조각을 Experience Platform에 수집하면 해당 고객을 위한 단일 프로필을 만들기 위해 함께 병합됩니다. 여러 소스의 데이터가 충돌하는 경우 병합 정책이 개인에 대해 프로필에 포함할 정보를 결정합니다. 샌드박스당 `_xdm.context.profile` 스키마를 사용하는 최대 5개의 병합 정책이 허용됩니다. 병합 정책에 대한 자세한 내용은 [병합 정책 개요](merge-policies/overview.md)를 참조하십시오.

### Experience Platform의 Adobe Analytics 보고서 세트 데이터 세트 {#aa-datasets}

모든 데이터 충돌이 해결되면 프로필에 대해 여러 보고서 세트를 활성화할 수 있습니다. 데이터 준비 기능을 사용하여 eVar, 목록 및 Prop 간의 데이터 충돌을 해결할 수 있습니다. 데이터 준비 기능을 사용하는 방법에 대한 자세한 내용은 [Adobe Analytics 커넥터 UI 안내서](../sources/tutorials/ui/create/adobe-applications/analytics.md)를 참조하십시오.

## 다음 단계

Real-Time CDP 제품 설명 문서의 기타 Experience Platform 서비스 보호, 종단 간 지연 정보 및 라이선스 정보에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Real-Time CDP 보호 기능](/help/rtcdp/guardrails/overview.md)
* 다양한 Experience Platform 서비스에 대한 [전체 지연 다이어그램](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=ko#end-to-end-latency-diagrams).
* [Real-Time Customer Data Platform(B2C Edition - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform(B2P - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform(B2B - Prime 및 Ultimate 패키지)](https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
