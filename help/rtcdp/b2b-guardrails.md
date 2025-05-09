---
keywords: 프로필;실시간 고객 프로필;문제 해결;가드레일;지침;제한;엔티티;기본 엔티티;차원 엔티티;RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;b2b;cdp;
title: Real-Time Customer Data Platform B2B edition의 기본 보호
type: Documentation
description: Adobe Experience Platform은 기존의 관계형 데이터 모델과 다른 고도로 비정규화된 하이브리드 데이터 모델을 사용합니다. 이 문서에서는 Adobe Real-Time Customer Data Platform B2B edition을 사용하여 최적의 시스템 성능을 위해 데이터를 모델링하는 데 도움이 되는 기본 사용 및 속도 제한을 제공합니다.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: bc399f3af0524232671af780ea1380f1a71a5b7e
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---

# Real-Time Customer Data Platform B2B edition의 기본 보호

>[!NOTE]
>
>이 문서에 설명된 제한 사항은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

Real-Time Customer Data Platform B2B edition을 사용하면 행동 통찰력 및 고객 속성을 기반으로 개인화된 크로스 채널 경험을 실시간 고객 프로필 및 계정 프로필의 형태로 제공할 수 있습니다. 프로필에 대한 이러한 새로운 접근 방식을 지원하기 위해 Experience Platform은 기존의 관계형 데이터 모델과 다른 고도로 비정규화된 하이브리드 데이터 모델을 사용합니다.

>[!IMPORTANT]
>
>이 보호 기능 페이지 외에 실제 사용 제한에 대해 판매 주문에서 라이선스 자격 및 해당 [제품 설명](https://helpx.adobe.com/kr/legal/product-descriptions.html)을(를) 확인하십시오.

이 문서는 최적의 시스템 성능을 위해 데이터를 모델링하는 데 도움이 되는 기본 사용 및 속도 제한을 제공합니다. 다음 가드레일을 검토할 때 데이터를 올바르게 모델링했다고 가정합니다. 데이터 모델링 방법에 대한 질문이 있는 경우 고객 서비스 담당자에게 문의하십시오.

>[!INFO]
>
>대부분의 고객은 이러한 기본 제한을 초과하지 않습니다. 사용자 지정 제한에 대해 알아보려면 고객 지원 센터 담당자에게 문의하십시오.

## 제한 유형

이 문서에는 두 가지 유형의 기본 제한이 있습니다.

| 보호 유형 | 설명 |
| -------------- | ----------- |
| **성능 보호(소프트 제한)** | 성능 보호는 사용 사례의 범위와 관련된 사용 제한입니다. 성능 가드레일을 초과하면 성능 저하 및 지연이 발생할 수 있습니다. Adobe은 이러한 성능 저하에 대한 책임이 없습니다. 성능 가드레일을 지속적으로 초과하는 고객은 성능 저하를 방지하기 위해 추가 용량의 라이센스를 선택할 수 있습니다. |
| **시스템 적용 보호 기능(하드 제한)** | 시스템에서 적용되는 가드레일은 Real-Time CDP UI 또는 API에 의해 적용됩니다. 이는 UI 및 API가 귀하를 차단하거나 오류를 반환하므로 초과할 수 없는 제한입니다. |

>[!INFO]
>
>이 문서에 설명된 제한 사항이 지속적으로 개선되고 있습니다. 업데이트를 정기적으로 확인하십시오. 사용자 지정 제한에 대한 자세한 내용은 고객 지원 센터에 문의하십시오.

## 데이터 모델 제한

다음 가드레일은 실시간 고객 프로필 데이터를 모델링할 때 권장되는 제한을 제공합니다. 기본 엔터티 및 차원 엔터티에 대한 자세한 내용은 부록의 [엔터티 형식](#entity-types)에 대한 섹션을 참조하십시오.

### 기본 엔티티 보호

>[!NOTE]
>
>이 섹션에 설명된 데이터 모델 제한은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| Real-Time CDP B2B edition 표준 XDM 클래스 데이터 세트 | 60 | 성능 보호 | Real-Time CDP B2B edition에서 제공하는 표준 Experience Data Model(XDM) 클래스를 활용하는 최대 60개의 데이터 세트가 권장됩니다. B2B 사용 사례에 대한 표준 XDM 클래스의 전체 목록이 필요하면 Real-Time CDP B2B edition 설명서의 [스키마](schemas/b2b.md)를 참조하십시오. <br/><br/>*참고: Experience Platform의 비정규화된 하이브리드 데이터 모델의 특성으로 인해 대부분의 고객은 이 한도를 초과하지 않습니다. 데이터를 모델링하는 방법에 대한 질문이 있거나 사용자 지정 제한에 대한 자세한 내용은 고객 지원 센터에 문의하십시오.* |
| ID 그래프의 개별 계정에 대한 ID 수 | 50 | 성능 보호 | 개별 계정에 대한 ID 그래프의 최대 ID 수는 50개입니다. ID가 50개를 초과하는 프로필은 세그먼테이션, 내보내기 및 조회에서 제외됩니다. |
| 기존 다중 엔티티 관계 | 20 | 성능 보호 | 기본 엔티티와 차원 엔티티 간에 최대 20개의 다중 엔티티 관계가 정의되는 것이 좋습니다. 기존 관계가 제거되거나 비활성화될 때까지 추가 관계 매핑을 수행하지 마십시오. |
| XDM 클래스당 다대일 관계 | 2 | 성능 보호 | XDM 클래스당 최대 2개의 다대일 관계가 정의되는 것이 좋습니다. 기존 관계를 제거하거나 비활성화할 때까지 추가 관계를 만들지 마십시오. 두 스키마 간의 관계를 만드는 방법에 대한 단계는 [B2B 스키마 관계 정의](../xdm/tutorials/relationship-b2b.md)에 대한 자습서를 참조하십시오. |

### Dimension 엔티티 보호

>[!NOTE]
>
>이 섹션에 설명된 데이터 모델 제한은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| 중첩된 레거시 관계 없음 | 0 | 성능 보호 | [!DNL XDM Individual Profile]이 아닌 두 스키마 간에 관계를 만들면 안 됩니다. [!DNL Profile] 유니온 스키마에 속하지 않는 스키마에는 관계를 만드는 것이 **권장되지 않습니다**. |
| B2B 개체만 다대일 관계에 참여할 수 있습니다 | 0 | 시스템 강제 보호 | 시스템은 B2B 개체 간의 다대일 관계만 지원합니다. 다대일 관계에 대한 자세한 내용은 [B2B 스키마 관계 정의](../xdm/tutorials/relationship-b2b.md)에 대한 자습서를 참조하십시오. |
| B2B 개체 간 중첩 관계의 최대 깊이 | 3 | 시스템 강제 보호 | B2B 개체 간의 중첩 관계의 최대 깊이는 3입니다. 즉, 고도로 중첩된 스키마에서는 3개 수준 이상 중첩된 B2B 개체 간의 관계가 없어야 합니다. |
| 각 차원 엔티티에 대한 단일 스키마 | 1 | 시스템 강제 보호 | 각 차원 엔티티에는 단일 스키마가 있어야 합니다. 둘 이상의 스키마에서 생성된 차원 엔티티를 사용하려고 하면 세분화 결과에 영향을 줄 수 있습니다. 다른 차원 엔티티에는 별도의 스키마가 있어야 합니다. |

## 데이터 크기 제한

다음 가드레일은 데이터 크기를 나타내며 의도한 대로 수집, 저장 및 쿼리할 수 있는 데이터에 대한 권장 제한을 제공합니다. 기본 엔터티 및 차원 엔터티에 대한 자세한 내용은 부록의 [엔터티 형식](#entity-types)에 대한 섹션을 참조하십시오.

>[!INFO]
>
>데이터 크기는 수집 시 JSON에서 압축되지 않은 데이터로 측정됩니다.

### 기본 엔티티 보호

>[!NOTE]
>
>이 섹션에 설명된 데이터 크기 제한은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| 일별 XDM 클래스당 수집된 배치 | 45 | 성능 보호 | XDM 클래스당 매일 수집되는 총 배치 수는 45개를 초과할 수 없습니다. 추가 배치를 수집하면 최적의 성능을 저하시킬 수 있습니다. |

### Dimension 엔티티 보호

>[!NOTE]
>
>이 섹션에 설명된 데이터 크기 제한은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| 모든 차원 엔티티에 대한 총 크기 | 5GB | 성능 보호 | 모든 차원 엔티티에 대해 권장되는 총 크기는 5GB입니다. 큰 차원 엔티티를 수집하면 시스템 성능에 영향을 줄 수 있습니다. 예를 들어 10GB 제품 카탈로그를 차원 엔티티로 로드하려는 시도는 권장되지 않습니다. |
| 차원 엔티티 스키마당 데이터 세트 | 5 | 성능 보호 | 각 차원 엔티티 스키마와 연결된 데이터 세트는 최대 5개가 권장됩니다. 예를 들어 &quot;제품&quot;에 대한 스키마를 만들고 5개의 기여 데이터 세트를 추가하는 경우 제품 스키마에 연결된 여섯 번째 데이터 세트를 만들면 안 됩니다. |
| 일별로 수집된 Dimension 엔티티 배치 | 엔티티당 4개 | 성능 보호 | 하루에 수집되는 최대 차원 엔티티 배치 권장 수는 엔티티당 4개입니다. 예를 들어 제품 카탈로그에 대한 업데이트를 하루에 최대 4번까지 수집할 수 있습니다. 동일한 엔티티에 대해 추가 차원 엔티티 배치를 수집하면 시스템 성능에 영향을 줄 수 있습니다. |

## 세그먼테이션 보호

이 섹션에 설명된 보호 기능은 조직이 Experience Platform 내에서 만들 수 있는 대상의 수와 특성뿐만 아니라 대상을 대상에 매핑하고 활성화하는 방법에 대해 설명합니다.

>[!NOTE]
>
>이 섹션에 설명된 세그먼테이션 제한은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

| 가드레일 | 제한 | 제한 유형 | 설명 |
| --------- | ----- | ---------- | ----------- |
| B2B 샌드박스당 세그먼트 정의 | 400 | 성능 보호 | 각 개별 B2B 샌드박스에 400개 미만의 세그먼트 정의가 있는 한 조직에는 총 400개 이상의 세그먼트 정의가 있을 수 있습니다. 추가 세그먼트 정의를 만들려고 하면 시스템 성능에 영향을 줄 수 있습니다. |

## 다음 단계

이 문서에 설명된 제한 사항은 Real-Time Customer Data Platform B2B edition에서 활성화한 변경 사항을 나타냅니다. Real-Time CDP B2B edition에 대한 전체 기본 제한 목록의 경우 이러한 제한을 [실시간 고객 프로필 데이터 설명서](../profile/guardrails.md)에 요약된 일반적인 Adobe Experience Platform 제한과 결합하십시오.

## 부록

이 섹션에서는 이 문서의 제한에 대한 추가 세부 정보를 제공합니다.

### 엔티티 유형

[!DNL Profile] 저장소 데이터 모델은 [기본 엔터티](#primary-entity) 및 [차원 엔터티](#dimension-entity)의 두 가지 핵심 엔터티 유형으로 구성됩니다.

#### 기본 엔티티

기본 엔티티 또는 프로필 엔티티는 데이터를 함께 병합하여 개인에 대한 &quot;단일 신뢰할 수 있는 소스&quot;를 구성합니다. 이러한 통합 데이터는 &quot;결합 보기&quot;라고 하는 것을 사용하여 표시됩니다. 유니온 조회는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 유니온 스키마로 집계합니다. [!DNL Real-Time Customer Profile]에 대한 유니온 스키마는 모든 프로필 특성 및 동작 이벤트의 컨테이너 역할을 하는 비정규화된 하이브리드 데이터 모델입니다.

&quot;레코드 데이터&quot;라고도 하는 시간 독립적 특성은 [!DNL XDM Individual Profile]을(를) 사용하여 모델링되지만 &quot;이벤트 데이터&quot;라고도 하는 시계열 데이터는 [!DNL XDM ExperienceEvent]을(를) 사용하여 모델링됩니다. 레코드 및 시계열 데이터가 Adobe Experience Platform에서 수집되면 [!DNL Real-Time Customer Profile]을(를) 트리거하여 사용할 수 있도록 설정된 데이터 수집을 시작합니다. 상호 작용과 세부 사항이 많을수록 개별 프로필이 더 강력해집니다.

![레코드 데이터와 시계열 데이터 간의 차이점을 요약한 인포그래픽입니다.](../profile/images/guardrails/profile-entity.png)

#### Dimension 엔티티

프로필 데이터를 유지 관리하는 프로필 데이터 저장소는 관계형 저장소가 아니지만, 프로필에서는 단순하고 직관적인 방식으로 대상자를 만들 수 있도록 작은 차원 엔티티와의 통합을 허용합니다. 이 통합을 [다중 엔티티 세그멘테이션](../segmentation/tutorials/multi-entity-segmentation.md)이라고 합니다.

또한 조직은 상점, 제품 또는 속성과 같이 개인 이외의 항목을 설명하는 XDM 클래스를 정의할 수도 있습니다. 이러한 [!DNL XDM Individual Profile]이 아닌 스키마를 &quot;차원 엔터티&quot;(&quot;조회 엔터티&quot;라고도 함)라고 하며 시계열 데이터를 포함하지 않습니다. 차원 엔터티를 나타내는 스키마는 [스키마 관계](../xdm/tutorials/relationship-ui.md)을 사용하여 프로필 엔터티에 연결됩니다.

Dimension 엔티티는 다중 엔티티 세그먼트 정의를 지원 및 간소화하는 조회 데이터를 제공하며 세그먼테이션 엔진이 최적의 처리를 위해 전체 데이터 세트를 메모리에 로드할 수 있을 만큼 작아야 합니다(빠른 포인트 조회).

![프로필 엔터티가 차원 엔터티로 구성되어 있음을 보여 주는 인포그래픽입니다.](../profile/images/guardrails/profile-and-dimension-entities.png)
