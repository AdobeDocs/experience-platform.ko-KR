---
keywords: RTCDP;CDP;Real-time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;cdp;rtcdp
title: Real-time Customer Data Platform B2B Edition의 사용 사례 예
description: 이 샘플 시나리오는 Adobe Real-Time Customer Data Platform B2B 에디션 구현 구성에 대한 예제를 제공합니다.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Real-time Customer Data Platform B2B Edition의 사용 사례 예

Real-time Customer Data Platform B2B Edition은 기존 Real-Time CDP 및 Adobe Experience Platform 오퍼링을 확장하여 B2B 데이터 및 워크플로우를 지원합니다. 이 문서에서는 B2B Edition에서 제공하는 추가적인 이점을 보여주는 사용 사례를 제공합니다. 자동 프로필 변수에는 다음이 포함됩니다.

- 서로 다른 분산된 데이터 소스의 개인 및 계정 데이터를 통합하여 고객을 더 잘 이해하고 더 정확한 세그멘테이션을 가능하게 하는 포괄적인 보기를 생성합니다. 다음 문서를 참조하십시오. [xdm 스키마 관계 만들기](./schemas/b2b.md) 추가 정보를 위해 다양한 B2B 소스와 함께 사용하기 위한.
- 관련 엔티티의 속성을 기반으로 대상을 세그먼트화합니다. 여기에는 계정, 기회, 캠페인 및 마케팅 목록이 포함됩니다. 세그먼트는 더 이상 개인 속성 및 경험 이벤트로 제한되지 않습니다. 자세한 내용은 [B2B 세그먼테이션 설명서](./segmentation/b2b.md) b2B 특정 대상을 만드는 더 많은 예를 보려면 다음을 수행하십시오.
- 기본적으로 여러 계정과 관련된 한 사람의 사용 사례를 지원합니다.

## 사용 사례

기술 회사인 Bodea는 새로운 제품을 가지고 있으며 이메일 및 LinkedIn 광고 캠페인으로 고객을 동시에 타겟팅하고 싶어한다. 마케팅 캠페인의 효율성을 극대화하기 위해, 보데아는 또한 이전에 자사 제품에 100만 달러 이상을 소비했고 지난 달에 새 제품 페이지를 방문한 기존 계정과 관련된 사람들을 타겟팅하기를 원한다.

그러나, 보데아는 두 개의 사업분야를 가지고 있다. 보데아의 첫 번째 사업인 &quot;라인 1&quot;은 자동차 산업을 위한 소프트웨어를 만든다. 2호선은 자동차 부품을 만드는 3D 프린터를 판다. Bodea의 두 사업 라인의 결과로, Bodea의 고객 계정에서 생성된 수익 데이터는 단일 보기에서 통일되지 않습니다.

각 사업부에는 자체 판매 시스템이 있습니다. &quot;CRM 1&quot; 및 &quot;CRM 2&quot;. 이러한 CRM 영업 시스템은 모두 고유한 마케팅 자동화 플랫폼 &quot;Marketo 1&quot; 및 &quot;Marketo 2&quot;에 연결됩니다. CRM 1의 데이터는 Marketo 1에만 동기화되고 CRM2의 데이터는 Marketo 2에만 동기화됩니다. 궁극적으로 데이터는 다양한 기업 정보 사일로에 유지됩니다.

## 현재 데이터 상태

Bodea의 사업이 Townsend에 매각됨에 따라, Townsend 비즈니스 데이터는 각 판매 시스템에서 두 개의 개별 계정으로 기록됩니다.

Marketo 1에서 Townsend는 계정 1로 기록됩니다. CRM 1에는 두 명의 관련 사용자(p1@townsend.com 및 p2@townsend.com)과 20만 달러(&quot;Opportunity 1&quot;)의 비공개 영업 기회가 있습니다. 이 데이터는 CRM 1에서 Marketo 1으로 동기화됩니다.

Marketo 2에서 Townsend는 계정 2로 기록됩니다. 계정 2에는 CRM 2에 2명의 관련 담당자(p2@townsend.com 및 p3@townsend.com)과 1개의 비공개 영업 기회가 90만 달러(&quot;Opportunity 2&quot;)입니다. 이 데이터는 CRM 2에서 Marketo 2으로 동기화됩니다.

통합 및 추가적인 기업 제어 목적으로, Bodea는 또한 기본 데이터 관리(MDM) 시스템을 보유하고 있으며, 이 시스템은 Marketo 1의 계정 1(및 CRM 1)과 Marketo 2(및 CRM 2)의 계정 2가 동일한 회사임을 나타내는 레코드를 유지 관리합니다.

지난 달에 `p2@townsend.com` 새 제품 페이지를 방문했고 웹 방문이 Marketo 1에 의해 기록됩니다.

![계정 정보 다이어그램](./assets/account-info.png)

## 문제

Line 1은 새로운 소프트웨어 제품을 출시했으며, Bodea의 기존 최상위 고객을 대상으로 상향 판매하려고 합니다. Bodea는 해당 특정 타겟 대상자를 염두에 두고 마케팅 캠페인을 시작합니다.

관련 Townsend 정보가 Marketo 1의 계정 1과 Marketo 2의 계정 2로 기록되므로 Bodea의 마케팅 팀은 연결된 정보를 효율적으로 활용할 수 없습니다.

따라서 Bodea의 마케팅 팀은 이러한 새로운 기회를 통해 이러한 회사의 특정 비즈니스 연락처를 효율적으로 타깃팅하지 못하게 됩니다.

지금까지, Townsend는 그들의 모든 계좌에서 보데아 제품에 누적적으로 백만 달러 이상을 소비했습니다. 그러나, 하나의 판매 시스템 내에서 총 지출액이 100만 달러 이상을 넘지 않는 한, 이전 시스템을 사용하여 만들어진 세그먼트에는 Townsend의 사람이 포함되지 않을 것입니다. 매출 데이터는 다른 판매 시스템에서 계정에 분산되기 때문입니다.

Townsend의 지출은 서로 다른 판매 시스템으로 구분되고 개별적 합계가 100만 건을 넘지 않으므로 Marketo 1 또는 Marketo 2에 자격이 있는 사람은 찾지 못할 것입니다.

### Real-Time CDP B2B Edition이 문제를 해결하는 방법

Real-Time CDP B2B Edition을 사용하면 Bodea의 마케팅 팀은 다음을 수행할 수 있습니다.

- 서로 다른 모든 소스(여러 Marketo 및 CRM 인스턴스, 기본 데이터 관리)의 데이터를 Real-Time CDP B2B Edition에 결합합니다.

RT-CDP B2B Edition을 사용하는 Bodea는 Marketo Engage 소스 커넥터를 사용하여 Marketo 1 및 Marketo 2의 B2B 데이터를 Experience Platform으로 가져오고 플랫폼 연결 애플리케이션을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다. 자세한 내용은 [Marketo 소스 커넥터](../sources/connectors/adobe-applications/marketo/marketo.md) 설명서 를 참조하십시오.

CRM1의 B2B 데이터( 사람, 계정, 기회 및 활동 )는 Marketo 1에 동기화됩니다. 마찬가지로 CRM 2의 모든 B2B 데이터는 Marketo 2에 동기화됩니다. Marketo 소스 커넥터를 통해 Adobe Experience Platform에 동기화됩니다. 그러나 Bodea가 CRM의 추가 데이터를 Experience Platform으로 가져오려는 경우 기존 CRM 커넥터를 사용할 수 있습니다.

단순함을 위해 그리고 이 예제의 목적을 위해, 사람들은 이메일에 의해 식별되고 있습니다. 이 예제의 결합된 계정 데이터는 다음과 같습니다.

| 사람 |
|---|
| p1@townsend.com |
| p2@townsend.com (지난 달에 새 제품 페이지를 방문한 사람) |
| p3@townsend.com |

| 기회 (마감) |
|---|
| 영업 기회 1, 2억 달러 |
| 영업 기회 2, 90만 달러 |

- 다양한 마케팅 이니셔티브를 위해 이 집계 데이터를 사용하여 고유한 세그먼트를 만들 수 있습니다. 이 예에서는 세그먼트가

   - 모든 고객에게 100만 달러 이상의 영업 기회 제공
   - 및
   - 지난 달에 제품 페이지를 방문한 적이 있습니다

- Bodea의 새로운 마케팅 캠페인에서 가장 효율적인 수신자인 대상을 만듭니다. 이 예에서 RT-CDP, B2B Edition은 마케터가 식별하는 데 도움이 됩니다 `p2@townsend.com` 을 이 마케팅 캠페인에 적합한 타겟으로 사용할 수 있습니다.

Bodea는 Marketo Engage 및 LinkedIn 대상을 사용하여 마케팅 팀을 위한 종단 간 CXM(고객 경험 관리) 솔루션을 제공합니다. Experience Platform에서 만든 대상자는 정적 목록으로 표시되는 Marketo 대상에 푸시됩니다. 그러면 이 대상이 Marketo 마케팅 캠페인에 자동으로 추가됩니다. 동시에 RT-CDP B2B Edition을 통해 LinkedIn 마케팅 캠페인으로 대상을 보낼 수도 있습니다.

## 다음 단계

이 문서를 읽은 후에는 Real-Time CDP B2B Edition을 사용하여 해결할 수 있는 목표 및 문제 유형에 대해 소개되었습니다.

다음 설명서는 B2B 특정 기능에 대한 이해를 개선하기 위해 권장됩니다.

- [Real-time Customer Data Platform B2B Edition 엔드투엔드 자습서](./b2b-tutorial.md)
- [Real-time Customer Data Platform B2B Edition의 소스](./sources/b2b.md)
- [Real-time Customer Data Platform B2B Edition의 스키마](./schemas/b2b.md)
- [B2B 세그먼테이션 예](./segmentation/b2b.md)
- [계정 프로필 개요](./accounts/account-profile-overview.md)
- [Real-time Customer Data Platform B2B Edition의 대상](./destinations/b2b.md)
- [LinkedIn 일치된 대상 대상 구성](../destinations/catalog/social/linkedin.md)
