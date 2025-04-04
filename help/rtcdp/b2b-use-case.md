---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;cdp;rtcdp
title: Real-Time Customer Data Platform B2B edition의 사용 사례 예
description: 이 샘플 시나리오는 Adobe Real-Time Customer Data Platform B2B 에디션 구현 구성에 대한 예제를 제공합니다.
feature: Get Started, Use Cases, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 2%

---

# Real-Time Customer Data Platform B2B edition의 사용 사례 예

Real-Time Customer Data Platform B2B edition은 기존 Real-Time CDP 및 Adobe Experience Platform 오퍼링을 확장하여 B2B 데이터 및 워크플로를 지원합니다. 이 문서에서는 B2B edition에서 제공하는 추가 이점을 보여 주는 예제 사용 사례를 제공합니다. 자동 프로필 변수에는 다음이 포함됩니다.

- 서로 다른 분산된 데이터 소스의 개인 및 계정 데이터를 결합하여 고객을 더 잘 이해하고 더 정확한 세분화를 가능하게 하는 포괄적인 보기를 생성합니다. 자세한 내용은 다양한 B2B 소스와 함께 사용하기 위한 [XDM 스키마 관계 만들기](./schemas/b2b.md)에 대한 설명서를 참조하십시오.
- 관련 엔티티의 속성을 기반으로 대상을 세그먼트화합니다. 여기에는 계정, 영업 기회, 캠페인 및 마케팅 목록이 포함됩니다. 대상은 더 이상 개인 속성 및 경험 이벤트에만 국한되지 않습니다. B2B 관련 대상을 만드는 방법에 대한 자세한 예는 [B2B 세그멘테이션 설명서](./segmentation/b2b.md)를 참조하십시오.
- 여러 계정과 관련된 한 사람의 사용 사례를 기본적으로 지원합니다.

## 활용 사례

기술기업 보데아는 신제품을 보유하고 있으며 이메일과 링크드인 광고 캠페인으로 동시에 고객을 공략하고자 한다. Bodea는 마케팅 캠페인의 효율성을 극대화하기 위해 이전에 자사 제품에 100만 달러 이상을 소비하고 지난 달 새 제품 페이지를 방문한 기존 계정과 관련된 사람들을 타겟팅하려고 합니다.

하지만, 보데아는 두 가지 다른 사업 분야를 가지고 있습니다. Bodea의 첫 번째 사업 라인 &quot;라인 1&quot;은 자동차 산업을 위한 소프트웨어를 만듭니다. 2차 사업 라인 &#39;라인 2&#39;는 자동차 부품을 만드는 3D 프린터를 판매하고 있다. Bodea의 두 가지 사업 부문의 결과, Bodea의 고객 계정에서 발생하는 수익 데이터는 단일한 관점에서 통일되지 않는다.

각 사업부에서는 &quot;CRM 1&quot; 및 &quot;CRM 2&quot;와 같은 자체 판매 시스템을 가지고 있습니다. 이러한 CRM 영업 시스템 모두 자체 마케팅 자동화 플랫폼 &quot;Marketo 1&quot; 및 &quot;Marketo 2&quot;에 연결되어 있습니다. CRM 1의 데이터는 Marketo 1에만 동기화되고 CRM 2의 데이터는 Marketo 2에만 동기화됩니다. 궁극적으로, 데이터는 다양한 기업 정보 사일로에 보관됩니다.

## 현재 데이터 상황

Bodea의 두 가지 영업 라인이 모두 Townsend 회사에 판매됨에 따라, Townsend 비즈니스 데이터는 각 영업 시스템에서 두 개의 별도 계정으로 기록됩니다.

Marketo 1에서는 Townsend가 계정 1로 기록됩니다. CRM 1에 2명의 관련자(p1@townsend.com 및 p2@townsend.com)와 1개의 마감 영업 기회 $200k(&quot;Opportunity 1&quot;)가 있습니다. 해당 데이터는 CRM 1에서 Marketo 1로 동기화됩니다.

Marketo 2에서는 Townsend가 계정 2로 기록됩니다. 또한 계정 2에는 CRM 2에 2명의 관련자(p2@townsend.com 및 p3@townsend.com)와 1개의 마감 영업 기회인 90만 달러(&quot;Opportunity 2&quot;)가 있습니다. 해당 데이터는 CRM 2에서 Marketo 2로 동기화됩니다.

통합 및 추가적인 기업 통제를 위해 Bodea는 Marketo 1의 계정 1(및 CRM 1)과 Marketo 2의 계정 2(및 CRM 2)가 동일한 회사임을 나타내는 기록을 유지 관리하는 기본 데이터 관리 (MDM) 시스템을 갖습니다.

지난 달에 `p2@townsend.com`님이 새 제품 페이지를 방문했으며 웹 방문은 Marketo 1에 의해 기록되었습니다.

![계정 정보 다이어그램](./assets/account-info.png)

## 문제

Line 1은 새로운 소프트웨어 제품을 출시했으며 Bodea의 기존 상위 계층 고객 기반에 업셀하고자 합니다. Bodea는 특정 타겟 대상자를 염두에 두고 마케팅 캠페인을 시작합니다.

해당 타운센드 정보가 Marketo 1의 계정 1, Marketo 2의 계정 2로 기록되어 있어 보데아의 마케팅팀은 사일로화된 정보를 효율적으로 활용할 수 없다.

이는 Bodea의 마케팅 팀이 이 새로운 기회를 통해 이러한 기업의 특정 비즈니스 담당자를 효율적으로 타겟팅하는 것을 금지합니다.

현재까지, 타운센드는 보데아 제품 전체에 걸쳐 누적 100만 달러 이상을 소비했습니다. 단, 기존 시스템을 사용하여 생성된 대상자는 단일 판매 시스템 내에서 소비한 총 금액이 100만 달러 이상이 아니면 Townsend의 모든 고객을 포함하지 않습니다. 서로 다른 판매 시스템 하의 계정에서 수익 데이터가 고립되기 때문이다.

Townsend의 지출이 서로 다른 판매 시스템으로 나뉘어 있으며 각각 합계가 100만 명을 넘지 않으므로 세그먼트 정의는 Marketo 1 또는 Marketo 2에서 자격을 갖춘 사람을 찾지 못합니다.

### Real-Time CDP B2B edition으로 문제를 해결하는 방법

Real-Time CDP B2B edition을 통해 Bodea의 마케팅 팀은 다음과 같은 작업을 수행할 수 있습니다.

- 모든 개별 소스(여러 Marketo 및 CRM 인스턴스 및 기본 데이터 관리)의 데이터를 Real-Time CDP B2B edition에 결합합니다.

RT-CDP B2B edition을 사용하여 Bodea는 Marketo Engage Source 커넥터를 사용하여 Marketo 1 및 Marketo 2의 B2B 데이터를 Experience Platform으로 가져오고 Experience Platform 연결 애플리케이션을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다. 자세한 내용은 [Marketo 소스 커넥터](../sources/connectors/adobe-applications/marketo/marketo.md) 설명서를 참조하십시오.

CRM1의 B2B 데이터 (사람, 계정, 기회 및 활동 )가 Marketo 1에 동기화됩니다. 마찬가지로 CRM 2의 모든 B2B 데이터가 Marketo 2로 동기화됩니다. 이러한 파일은 Marketo 소스 커넥터를 통해 Adobe Experience Platform에 동기화됩니다. 그러나 Bodea가 CRM의 추가 데이터를 Experience Platform으로 가져오려는 경우 기존 CRM 커넥터를 사용할 수 있습니다.

단순성을 위해 그리고 이 예제의 목적을 위해, 사람들은 그들의 이메일로 식별되고 있다. 이 예제의 결합된 계정 데이터는 다음과 같습니다.

| 사람 |
|---|
| p1@townsend.com |
| p2@townsend.com (지난 달에 새 제품 페이지를 방문했습니다) |
| p3@townsend.com |

| Opportunities (closed-won) |
|---|
| 영업 기회 1, 20 만 달러 |
| 영업 기회 2, 90 만 달러 |

- 다양한 마케팅 이니셔티브에 대해 이 집계 데이터를 사용하여 고유한 대상을 만듭니다. 이 예에서 세그먼트 정의는 다음과 같은 모든 사람을 찾습니다.

   - 연결된 영업 기회(전체 고객)가 가치 100만 달러를 초과함
   - 및
   - 지난 달에 제품 페이지를 방문했습니다.

- Bodea의 새로운 마케팅 캠페인의 가장 효율적인 수신자인 대상자를 만듭니다. 이 예에서는 RT-CDP의 B2B edition을 사용하여 마케터가 `p2@townsend.com`을(를) 이 마케팅 캠페인에 대한 올바른 대상으로 식별할 수 있습니다.

Marketo Engage 및 LinkedIn 대상을 사용하여 Bodea는 마케팅 팀을 위한 엔드 투 엔드 CXM(고객 경험 관리) 솔루션을 제공합니다. Experience Platform에서 만든 대상자는 정적 목록으로 표시되는 Marketo 대상에 푸시됩니다. 그러면 이 대상자는 Marketo 마케팅 캠페인에 자동으로 추가됩니다. 동시에 대상자는 RT-CDP B2B edition에서 LinkedIn 마케팅 캠페인으로 보낼 수도 있습니다.

## 다음 단계

이 문서를 읽은 후에는 Real-Time CDP B2B edition을 사용하여 해결할 수 있는 목표 및 문제 유형에 대해 소개하게 됩니다.

B2B 특정 기능에 대한 이해를 높이려면 다음 설명서를 사용하는 것이 좋습니다.

- [Real-Time Customer Data Platform B2B edition 전체 자습서](./b2b-tutorial.md)
- [Real-Time Customer Data Platform B2B edition의 소스](./sources/b2b.md)
- [Real-Time Customer Data Platform B2B edition의 스키마](./schemas/b2b.md)
- [B2B 세그멘테이션 예](./segmentation/b2b.md)
- [계정 프로필 개요](./accounts/account-profile-overview.md)
- [Real-Time Customer Data Platform B2B edition의 대상](./destinations/b2b.md)
- [LinkedIn Matched Audiences 대상 구성](../destinations/catalog/social/linkedin.md)
