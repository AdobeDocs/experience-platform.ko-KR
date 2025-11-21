---
keywords: RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;b2b;cdp;고객 AI
title: Real-Time CDP B2B edition 개요
description: Real-Time Customer Data Platform B2B Edition 계정 개요
feature: Get Started, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 4%

---

# Real-Time Customer Data Platform B2B edition 개요

Adobe Real-Time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B edition은 B2B 서비스 모델에서 작동하는 마케터를 위해 특별히 빌드되었습니다. 여러 소스의 데이터를 함께 가져와서 사람 및 계정 프로필의 단일 보기로 결합합니다. 마케터는 이 통합 데이터를 통해 특정 대상자를 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상자를 참여시킬 수 있습니다.

Real-Time CDP B2B edition과 B2C 대응체를 구분하는 다양한 Adobe Experience Platform 기능에 대한 개선 사항이 있습니다. 여기에는 B2B 사용 사례용 XDM(Experience Data Model) 개선, ID 확인 및 프로필 세분화로의 업그레이드, [!DNL Marketo Engage]의 사용자 지정 커넥터 및 대상이 포함됩니다. [!DNL Marketo] 커넥터를 사용하면 B2B 브랜드가 리드를 육성하고 계정 기반 마케팅 작업을 향상시키기 위해 업계 최고의 B2B 참여 데이터를 행동 정보와 연결할 수 있습니다.

Real-Time CDP B2B edition을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 여러 소스에서 수집된 데이터를 단일 보기로 결합하여 전체적인 사람 및 계정 프로필을 만들 수 있습니다.
* 통합 계정 프로필의 중앙 집중식 저장소에서 모든 크로스 소스 데이터를 보강, 세그먼트화 및 내보냅니다.
* 중앙 집중화 프로세스의 모든 단계에서 사용할 수 있는 데이터 거버넌스 도구를 사용하여 데이터를 관리하여 데이터가 법적 규정 및 비즈니스 정책을 준수하도록 합니다.

Real-Time CDP B2B edition의 개선 사항에 대한 보다 포괄적인 세부 정보는 아래 섹션으로 나뉩니다.

## XDM

Real-Time CDP B2B edition은 특히 B2B 목적을 위해 데이터를 캡처하고 구조화하는 몇 가지 새로운 XDM 스키마 클래스, 필드 그룹 및 관계 유형을 제공합니다. 이러한 각 개선 사항에 대한 자세한 내용은 Real-Time CDP B2B edition의 [XDM에 대한 개요](./schemas/b2b.md)를 참조하십시오.

사전 구성된 B2B 스키마를 사용하면 표준화되고 실행 가능한 구조로 데이터를 가져올 수 있습니다. 많은 새 스키마 클래스는 [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo] 및 기타 B2B 데이터 소스와 같은 주요 CRM에서 발생하는 클래스에 거의 직접 매핑됩니다. Real-Time CDP B2B edition을 사용하면 B2B 소스의 데이터를 감사하기 쉬운 결과와 간단한 방법으로 Experience Platform으로 가져올 수 있습니다.

이러한 XDM 개선 사항을 통해 B2B 중심 소스 및 대상을 통해 데이터를 더 잘 수집 및 활성화할 수 있으므로 데이터 통합 및 프레젠테이션을 향상시켜 보다 다양하고 유연한 사용 사례를 제공할 수 있습니다.

## ID 확인

스키마가 정의되고 데이터가 해당 스키마에 따라 수집되면 Real-Time CDP B2B edition은 강력한 실시간 ID 확인 시스템을 통해 실제 사용자와 비즈니스를 나타내는 소스 레코드를 식별합니다.

ID 확인 시스템은 다음과 같은 기능을 제공합니다.

* B2B 및 B2C 사람 레코드 결합
* 여러 수준의 계정 계층 구조
* 다대다, 사람 대 계정 연결
* 직원 및 계정 ID는 실시간으로 확인됩니다

정체성 확인 시스템은 보다 다각적인 사람 분류를 지원하기 위해 확장되었다. 이 시스템을 통해 사람은 고객은 물론 비즈니스 기회에서 잠재 고객으로 식별될 수 있습니다.

소스 CRM에 의해 동기화되고 시스템 내의 여러 경로를 통해 연결된 계정 레코드는 Experience Platform에 의해 병합됩니다. 시스템은 비즈니스 기회와 연계된 사용자와 고객으로 기록된 사용자를 통합하지만, 식별 가능한 경우 이들 간의 차이를 속성으로 유지할 수도 있습니다.

일치하는 식별자는 여러 시스템에서 계정 레코드를 함께 연결하고 병합하는 데 사용됩니다. 계정 계층은 이 프로세스 전체에서 유지됩니다. 차별화 요소는 개인이 계정과 연결되어 있는지 여부를 면밀히 조사하고 필요한 경우 계정에서 분리할 수 있는 기능을 제공하는 데 사용됩니다.

## 프로필 및 세분화

Real-Time CDP B2B edition이 데이터를 수집하고 사람, 회사, 속성 및 행동과 관련된 ID를 해결하면 해당 데이터를 사용하여 프로필을 구성합니다. 그런 다음 이러한 프로필을 다양한 대상으로 활성화할 수 있는 탐색 가능한 대상으로 세그먼트화할 수 있습니다.

올바르게 구현되면 시스템에서는 이메일 주소와 같이 변경될 수 있는 속성이 아니라 고유한 기본 식별자를 사용하여 사용자를 추적합니다. 이것은 누군가가 직업을 바꿀 때 시스템이 여전히 그들을 뒤따른다는 것을 의미한다. 동일한 엔티티이지만 대신 새 계정에 연결됩니다. 시스템이 이러한 사람들을 모든 속성과 행동을 포함한 개인으로 따르므로 이 기본 기능은 새 계정으로 확장할 수 있는 훌륭한 벡터를 제공합니다.

## B2B 소스

Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. [!DNL Marketo] 소스를 사용하면 B2B 데이터를 Experience Platform에 스트리밍하고 Experience Platform 연결 응용 프로그램을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다. 여러 개의 [!DNL Marketo] 인스턴스를 지원하며(여러 인스턴스가 있는 대기업에 유익함) 데이터가 병합되는 단일 조직으로 가져옵니다.

>[!NOTE]
>
>Real-Time CDP B2B edition을 사용하는 데 필요한 [!DNL Marketo] 원본은 **not**&#x200B;입니다.

Marketo 및 B2B 데이터를 Experience Platform으로 가져오는 방법에 대한 자세한 내용은 [Real-Time CDP B2B edition의 소스](./sources/b2b.md) 설명서를 참조하십시오.

## B2B 대상

Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads 및 Google Ad Manager와 같은 Real-Time CDP 대상을 Experience Platform B2B edition에서 사용할 수 있으며 완벽하게 지원합니다. 또한 Marketo Engage 대상은 Experience Platform에서 세그먼트 멤버십 데이터를 스트리밍하고 Marketo의 목록으로 사용할 수 있도록 합니다.

자세한 내용은 [Marketo Engage 대상](../destinations/catalog/adobe/marketo-engage.md)에 대한 개요를 참조하십시오.

CRM이 두 개 이상인 회사의 경우 Real-Time CDP B2B edition은 Marketo 또는 CRM의 인스턴스를 분리하도록 대상 커넥터를 구성하는 옵션을 제공합니다. 필요한 경우 각 인스턴스에 대상 커넥터를 구성하고 각 CRM 인스턴스에 독립적으로 대상자를 보낼 수 있습니다.

## 다음 단계

이제 Real-Time CDP B2B edition에서 제공하는 마케터의 이점 및 Real-Time CDP과 비교하여 차이점을 더 잘 이해했으므로 이러한 기능을 조직에 적용하는 방법에 대해 알아볼 수 있습니다.

Real-Time CDP B2B edition이 B2B 서비스 모델에 어떤 이점을 줄 수 있는지 이해하려면 다음 설명서를 참조하여 시작하는 데 도움을 받으십시오.

* [Real-Time CDP B2B edition의 사용 사례 예](./b2b-use-case.md)
* [Real-Time Customer Data Platform B2B edition을 위한 종단간 자습서](./b2b-tutorial.md)
* [데이터 수집 방법](./sources/b2b.md)
* [프로필에 액세스하는 방법](./profile/profile-overview.md)
* [Real-Time Customer Data Platform B2B edition의 스키마](./schemas/b2b.md)
* [대상자를 만드는 방법](./segmentation/b2b.md)
* [대상에 대한 대상자를 활성화하는 방법](./destinations/b2b.md)
* [데이터 거버넌스 정책을 정의하고 적용하는 방법](./privacy/data-governance-overview.md)
