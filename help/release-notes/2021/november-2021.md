---
title: Adobe Experience Platform 릴리스 노트 - 2021년 11월
description: Adobe Experience Platform에 대한 2021년 11월 릴리스 노트입니다.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 11월 17일**

## 새로운 기능

Adobe Experience Platform의 새로운 기능:

- [Real-Time Customer Data Platform B2B 에디션](#B2B)
- [(베타) 임시 활성화 API를 통해 대상자 세그먼트를 배치 대상에 활성화합니다](#ad-hoc-activation)

## 기존 기능 업데이트

Adobe Experience Platform의 기존 기능 업데이트:

- [기여도 AI](#attribution-ai)
- [고객 AI](#customer-ai)

### Real-Time Customer Data Platform B2B 에디션 {#B2B}

**릴리스 날짜: 2021년 11월 12일**

Real-time Customer Data Platform(Real-Time CDP)에 구축된 Real-Time CDP B2B Edition은 비즈니스-비즈니스 서비스 모델로 운영되는 마케터를 위해 특별히 빌드되었습니다. 여러 소스의 데이터를 가져와서 사람 및 계정 프로필에 대한 단일 보기로 결합합니다. 이러한 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 그러한 대상을 선택할 수 있습니다.

Real-Time CDP B2B Edition과 B2C 상대방을 구분하는 다양한 Adobe Experience Platform 기능이 개선되었습니다. 여기에는 B2B 사용 사례를 위한 XDM(Experience Data Model) 개선 사항, ID 확인 및 프로필 세그멘테이션으로 업그레이드, Marketo Engage을 위한 사용자 지정 커넥터 및 대상이 포함됩니다. Marketo 커넥터를 사용하면 B2B 브랜드가 업계를 선도하는 B2B 참여 데이터를 행동 정보와 연계하여 리드를 육성하고 계정 기반 마케팅 활동을 향상시킬 수 있습니다.

-[새로운 B2B 및 B2P 버전](#editions)
-[새로운 Marketo 데이터 소스 및 대상 커넥터](#marketo)
-[표준 B2B XDM](#XDM)

### 새로운 B2B 및 B2P 버전 {#editions}

Real-Time CDP 및 Platform Activation 제품 모두에 B2B 데이터 및 기능을 가져오는 새로운 B2B 및 B2P 버전을 구매할 수 있습니다.

Real-Time CDP B2B Edition에 대한 자세한 내용은 다음을 참조하십시오. [개요](../../rtcdp/overview.md).

### 새로운 Marketo 데이터 소스 및 대상 커넥터 {#marketo}

새로운 Marketo 데이터 소스 및 대상 커넥터는 Marketo 데이터를 플랫폼 및 플랫폼 대상으로 다시 Marketo으로 스트리밍합니다. 모든 Platform 사용자가 사용할 수 있습니다.

| 기능 | 설명 |
|----------|-------------|
| Marketo Engage 원본 커넥터 | 다음 [Marketo Engage 원본 커넥터](../../sources/connectors/adobe-applications/marketo/marketo.md) 마케터는 하나 이상의 Marketo 인스턴스에서 Adobe Experience Platform 인스턴스로 데이터를 원활하게 수집할 수 있고 리드 관리 및 B2B 마케터를 위한 완벽한 솔루션을 제공합니다. |
| Marketo Engage 대상 | 다음 [Marketo 대상](../../destinations/catalog/adobe/marketo-engage.md) 마케터는 Adobe Experience Platform에서 만든 세그먼트를 정적 목록으로 표시되는 Marketo에 푸시할 수 있습니다. |

### 표준 B2B XDM {#XDM}

표준 B2B XDM 클래스, 필드 그룹 및 데이터 유형은 모든 플랫폼 사용자가 사용할 수 있습니다.

| 기능 | 설명 |
|-----------|--------------|
| 표준 B2B XDM 클래스 | Real-time Customer Data Platform B2B Edition은 계정, 기회, 캠페인 등과 같은 중요한 B2B 데이터 엔티티에 대한 세부 사항을 캡처하는 여러 표준 XDM을 제공합니다. |

자세한 내용은 [Real-time Customer Data Platform B2B Edition의 스키마](../../rtcdp/schemas/b2b.md) B2B 데이터 엔티티 캡처에 대한 자세한 내용을 보려면 설명서를 참조하십시오.

### (베타) 임시 활성화 API를 통해 대상자 세그먼트를 배치 대상에 활성화합니다 {#ad-hoc-activation}

Ad-hoc 활성화 API를 사용하면 즉시 활성화해야 하는 상황에서 마케터는 빠르고 효율적인 방식으로 대상 세그먼트를 대상으로 프로그래밍 방식으로 활성화할 수 있습니다. 임시 대상 활성화는 [배치 파일 기반 대상](../../destinations/destination-types.md#file-based) 및 은 현재 베타 버전입니다. 자세한 내용은 [ad-hoc 활성화 API 설명서](../../destinations/api/ad-hoc-activation-api.md).

### 기여도 AI {#attribution-ai}

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
|-----------|---------------|
| 여러 데이터 세트 지원 | 이제 Attribution AI은 각 데이터 세트를 매핑하고 결합하지 않고도 UI에서 바로 여러 데이터 세트를 쉽게 수집할 수 있습니다. 이 새로운 시간 절약 기능은 여러 데이터 세트의 데이터를 보다 풍부하게 사용하여 보다 강력하고 정확한 점수를 제공합니다. |
| 미디어 채널 및 캠페인 필드 매핑 | 이제 Attribution AI에서 미디어 채널 및 캠페인 필드 매핑을 지원합니다. 데이터 세트 간 미디어 채널 매핑은 Attribution AI에서 파생된 인사이트를 향상시키고 해석하기 쉬운 결과를 더 명확하게 제공합니다. |

Attribution AI에 대한 자세한 내용은 [Attribution AI 설명서](../../intelligent-services/attribution-ai/overview.md).

### 고객 AI {#customer-ai}

Real-time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

**업데이트된 기능**

| 기능 | 설명 |
|-----------|-------------|
| 여러 데이터 세트 지원 | 이제 고객 AI는 각 데이터 세트를 매핑하고 결합하지 않고도 UI에서 바로 여러 데이터 세트를 쉽게 수집할 수 있습니다. 이 새로운 시간 절약 기능은 여러 데이터 세트의 데이터를 보다 풍부하게 사용하여 보다 강력하고 정확한 점수를 제공합니다. |
| 사용자 지정 프로필 속성 | 이제 Customer AI에서는 표준 이벤트 필드 외에도 데이터에서 사용자 지정 프로필 데이터 세트 필드(타임스탬프 포함)를 정의할 수 있습니다. 이 옵션을 사용하면 모델의 품질을 향상시키고 보다 정확한 결과를 제공할 수 있는 영향력 있는 프로필 속성을 추가할 수 있습니다. |

Customer AI에 대한 자세한 내용은 [Customer AI 설명서](../../intelligent-services/customer-ai/overview.md).
