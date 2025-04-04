---
title: Adobe Experience Platform 릴리스 노트 2021년 11월
description: Adobe Experience Platform에 대한 2021년 11월 릴리스 정보입니다.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 21%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2021년 11월 17일 목요일**

## 새로운 기능

Adobe Experience Platform의 새로운 기능:

- [Real-Time Customer Data Platform B2B 에디션](#B2B)
- [(Beta) 애드혹 활성화 API를 통해 대상 세그먼트를 배치 대상으로 활성화합니다](#ad-hoc-activation)

## 기존 기능 업데이트

Adobe Experience Platform의 기존 기능 업데이트:

- [기여도 AI](#attribution-ai)
- [고객 AI](#customer-ai)

### Real-Time Customer Data Platform B2B 에디션 {#B2B}

**릴리스 날짜: 2021년 11월 12일 토요일**

Real-Time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B 에디션은 business-to-business 서비스 모델에서 운영하는 마케터를 위해 특별히 설계되었습니다. 여러 소스의 데이터를 함께 가져와서 사람 및 계정 프로필의 단일 보기로 결합합니다. 마케터는 이 통합 데이터를 통해 특정 대상자를 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상자를 참여시킬 수 있습니다.

Real-Time CDP B2B edition과 B2C 대응체를 구분하는 다양한 Adobe Experience Platform 기능에 대한 개선 사항이 있습니다. B2B 사용 사례용 XDM(Experience Data Model) 개선 사항, ID 확인 및 프로필 세분화로의 업그레이드, Marketo Engage에 대한 사용자 지정 커넥터 및 대상 등이 포함됩니다. Marketo 커넥터를 사용하면 B2B 브랜드가 리드를 육성하고 계정 기반 마케팅 작업을 향상시키기 위해 업계 최고의 B2B 참여 데이터를 행동 정보와 연결할 수 있습니다.

-[새로운 B2B 및 B2P 에디션](#editions)
-[새로운 Marketo 데이터 소스 및 대상 커넥터](#marketo)
-[표준 B2B XDM](#XDM)

### 새로운 B2B 및 B2P 에디션 {#editions}

Real-Time CDP 및 Experience Platform Activation 제품 모두에 B2B 데이터와 기능을 제공하는 새로운 B2B 및 B2P 에디션을 구입할 수 있습니다.

Real-Time CDP B2B edition에 대한 자세한 내용은 [개요](../../rtcdp/overview.md)를 참조하세요.

### 새로운 Marketo 데이터 소스 및 대상 커넥터 {#marketo}

새로운 Marketo 데이터 소스 및 대상 커넥터는 Marketo 데이터를 Experience Platform으로 스트리밍하고 Experience Platform 대상자를 다시 Marketo으로 스트리밍합니다. 모든 Experience Platform 사용자가 사용할 수 있습니다.

| 기능 | 설명 |
|----------|-------------|
| Marketo Engage 소스 커넥터 | [Marketo Engage 소스 커넥터](../../sources/connectors/adobe-applications/marketo/marketo.md)를 통해 마케터는 하나 이상의 Marketo 인스턴스에서 Adobe Experience Platform 인스턴스로 데이터를 원활하게 수집할 수 있으며 리드 관리 및 B2B 마케터를 위한 완전한 솔루션을 제공합니다. |
| Marketo Engage 대상 | [Marketo 대상](../../destinations/catalog/adobe/marketo-engage.md)을(를) 사용하면 마케터가 Adobe Experience Platform에서 만든 세그먼트를 정적 목록으로 표시되는 Marketo으로 푸시할 수 있습니다. |

### 표준 B2B XDM {#XDM}

표준 B2B XDM 클래스, 필드 그룹 및 데이터 유형은 모든 Experience Platform 사용자가 사용할 수 있습니다.

| 기능 | 설명 |
|-----------|--------------|
| 표준 B2B XDM 클래스 | Real-Time Customer Data Platform B2B edition은 계정, 기회, 캠페인 등과 같은 필수 B2B 데이터 엔티티에 대한 세부 정보를 캡처하는 여러 표준 XDM을 제공합니다. |

B2B 데이터 엔터티를 캡처하는 방법에 대한 자세한 내용은 [Real-Time Customer Data Platform B2B edition의 스키마](../../rtcdp/schemas/b2b.md) 설명서를 참조하십시오.

### (Beta) 애드혹 활성화 API를 통해 대상 세그먼트를 배치 대상으로 활성화합니다 {#ad-hoc-activation}

임시 활성화 API를 사용하면 마케터가 즉각적인 활성화가 필요한 상황에 대해 대상 세그먼트를 빠르고 효율적으로 프로그래밍 방식으로 활성화할 수 있습니다. 임시 대상 활성화는 [일괄 파일 기반 대상](../../destinations/destination-types.md#file-based)에서만 지원되며 현재 Beta 상태입니다. 자세한 내용은 [임시 활성화 API 설명서](../../destinations/api/ad-hoc-activation-api.md)를 참조하십시오.

### 기여도 AI {#attribution-ai}

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
|-----------|---------------|
| 여러 데이터 세트 지원 | 이제 기여도 AI는 각 데이터 세트를 매핑 및 결합하지 않고도 UI에서 직접 여러 데이터 세트를 쉽게 수집할 수 있습니다. 이 새로운 시간 절약 기능은 여러 데이터 세트에서 더 풍부한 데이터를 통해 보다 강력하고 정확한 점수를 제공합니다. |
| 미디어 채널 및 캠페인 필드 매핑 | 이제 기여도 AI가 미디어 채널 및 캠페인 필드의 매핑을 지원합니다. 데이터 세트 간 미디어 채널 매핑은 Attribution AI에서 파생된 통찰력을 향상시키고 해석하기 쉬운 보다 명확한 결과를 제공하는 데 도움이 됩니다. |

기여도 AI에 대한 자세한 내용은 [기여도 AI 설명서](../../intelligent-services/attribution-ai/overview.md)를 참조하십시오.

### 고객 AI {#customer-ai}

Real-Time Customer Data Platform에서 사용할 수 있는 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

**업데이트된 기능**

| 기능 | 설명 |
|-----------|-------------|
| 여러 데이터 세트 지원 | 이제 고객 AI는 각 데이터 세트를 매핑하고 연결할 필요 없이 UI에서 직접 여러 데이터 세트를 쉽게 수집할 수 있습니다. 이 새로운 시간 절약 기능은 여러 데이터 세트에서 더 풍부한 데이터를 통해 보다 강력하고 정확한 점수를 제공합니다. |
| 사용자 지정 프로필 속성 | 이제 Customer AI는 표준 이벤트 필드 외에 데이터의 사용자 지정 프로필 데이터 세트 필드(타임스탬프 포함) 정의를 지원합니다. 이 옵션을 사용하면 영향력이 있다고 간주하는 프로필 속성을 더 추가할 수 있으므로 모델의 품질을 향상시키고 보다 정확한 결과를 제공할 수 있습니다. |

Customer AI에 대한 자세한 내용은 [Customer AI 설명서](../../intelligent-services/customer-ai/overview.md)를 참조하십시오.
