---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;실시간 고객 데이터 플랫폼;실시간 cdp;b2b;cdp;Customer AI
title: Real-Time CDP B2B 에디션 개요
description: Real-time Customer Data Platform B2B Edition 계정 개요
exl-id: 9b45bba4-fc46-4d69-b36a-5cb91f316612
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B Edition 개요

Adobe Real-time Customer Data Platform(Real-Time CDP)에 구축된 Real-Time CDP B2B Edition은 비즈니스-비즈니스 서비스 모델로 운영되는 마케터를 위해 특별히 빌드되었습니다. 여러 소스의 데이터를 가져와서 사람 및 계정 프로필에 대한 단일 보기로 결합합니다. 이러한 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 그러한 대상을 선택할 수 있습니다.

Real-Time CDP B2B Edition과 B2C 상대방을 구분하는 다양한 Adobe Experience Platform 기능이 개선되었습니다. 여기에는 B2B 사용 사례에 대한 XDM(Experience Data Model) 개선 사항, ID 확인 및 프로필 세그멘테이션으로 업그레이드, 그리고 에 대한 사용자 지정 커넥터 및 대상이 포함됩니다 [!DNL Marketo Engage]. 다음 [!DNL Marketo] 커넥터를 사용하면 B2B 브랜드가 리드를 육성하고 계정 기반 마케팅 작업을 향상시키기 위해 업계 선도적인 B2B 참여 데이터를 행동 정보와 연결할 수 있습니다.

Real-Time CDP B2B Edition을 사용하면 다음 작업을 수행할 수 있습니다.

* 여러 소스에서 수집한 데이터를 하나의 보기로 결합하여 전체적인 사람 및 계정 프로필을 생성합니다.
* 통합 계정 프로필의 중앙 저장소에서 모든 교차 소스 데이터를 보강, 세그먼트화하고 내보냅니다.
* 중앙 집중식 프로세스의 모든 단계에서 사용할 수 있는 데이터 거버넌스 도구를 사용하여 데이터를 관리하여 데이터가 법적 규정 및 비즈니스 정책을 준수하는지 확인합니다.

Real-Time CDP B2B Edition에 대한 향상된 기능에 대한 보다 포괄적인 세부 사항은 아래 섹션으로 나누어져 있습니다.

## XDM

Real-Time CDP B2B Edition은 B2B 목적으로 데이터를 캡처하고 구조화하는 몇 가지 새로운 XDM 스키마 클래스, 필드 그룹 및 관계 유형을 제공합니다. 다음 사항에 대한 개요를 참조하십시오. [Real-Time CDP B2B 에디션의 XDM](./schemas/b2b.md) 를 참조하십시오.

사전 구성된 B2B 스키마를 사용하여 데이터를 표준화된 실행 가능한 구조로 가져올 수 있습니다. 새로운 스키마 클래스 중 대부분은 다음과 같이 메인스트림 CRM에서 발생하는 스키마 클래스와 거의 직접 매핑됩니다 [!DNL Salesforce], [!DNL Microsoft Dynamics], [!DNL Marketo], 및 기타 B2B 데이터 소스. Real-Time CDP B2B Edition을 사용하면 B2B 소스의 데이터를 감사하기 쉬운 결과를 통해 간편하게 플랫폼으로 가져올 수 있습니다.

이러한 XDM 개선 사항을 사용하면 B2B 중심의 소스 및 대상을 통해 데이터를 보다 효과적으로 수집 및 활성화할 수 있고, 데이터 통합 및 프레젠테이션을 개선하여 보다 다양하고 유연한 사용 사례를 제공할 수 있습니다.

## ID 확인

스키마가 정의되고 해당 스키마를 따르는 데이터를 수집한 후 Real-Time CDP B2B Edition은 강력한 실시간 ID 확인 시스템을 통해 실제 사용자와 비즈니스를 나타내는 소스 레코드를 식별합니다.

ID 확인 시스템은 다음 기능을 제공합니다.

* B2B와 B2C의 사람 레코드 결합
* 여러 수준의 계정 계층
* 다대다, 사용자 간 연결
* 사람 및 계정 ID는 실시간으로 해결됩니다

신원 확인 시스템은 사람들의 다면적인 분류를 지원하기 위해 확장되었다. 이 시스템을 통해 고객은 물론 비즈니스 기회에 대한 리드로도 파악할 수 있습니다.

소스 CRM에 의해 동기화되고 시스템 내의 여러 경로를 통해 연결된 계정 레코드는 Platform에 의해 병합됩니다. 이 시스템은 비즈니스 기회와 관련된 사람들과 고객으로 기록된 사람들을 한데 모읍니다. 또한, 식별이 가능한 경우 이들을 속성으로서 구분도 유지할 수 있습니다.

일치하는 식별자는 여러 시스템에서 계정 레코드를 함께 연결하고 병합하는 데 사용됩니다. 계정 계층은 이 프로세스 전체에서 유지됩니다. 차별화 요소는 고객이 계정과 관련이 있는지 여부를 면밀히 살펴보고 필요한 경우 해당 고객과 계정을 분리할 수 있는 기능을 제공합니다.

## 프로필 및 세그멘테이션

Real-Time CDP B2B Edition이 사람, 회사, 속성 및 행동과 관련된 데이터 및 해결된 ID를 수집하면 해당 데이터가 프로필을 구성하는 데 사용됩니다. 그런 다음 다양한 대상으로 활성화할 수 있는 탐색 가능한 대상으로 이러한 프로필을 세그먼트화할 수 있습니다.

올바르게 구현되면 시스템이 이메일 주소와 같이 변경할 수 있는 특성이 아니라 고유한 기본 식별자를 사용하여 사용자를 추적합니다. 즉 어떤 사람이 직업을 바꾸면 시스템이 계속 따라간다는 뜻입니다. 개인이 여전히 동일한 엔티티이지만 대신 새 계정에 연결됩니다. 이 기본 기능은 시스템이 모든 특성 및 동작을 포함하는 개인으로 이러한 사용자를 따르므로 새 계정으로 확장할 수 있는 훌륭한 벡터를 제공합니다.

## B2B 소스

플랫폼을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. 다음 [!DNL Marketo] 소스를 사용하면 B2B 데이터를 플랫폼으로 스트리밍하고 Platform에 연결된 애플리케이션을 사용하여 이 데이터를 최신 상태로 유지할 수 있습니다. 이 확장은 [!DNL Marketo] (여러 인스턴스가 있는 대기업에서 유용하며) 데이터가 병합되는 단일 IMS 조직으로 가져옵니다.

>[!NOTE]
>
>다음 [!DNL Marketo] 소스: **not** Real-Time CDP B2B Edition을 사용해야 합니다.

자세한 내용은 [Real-Time CDP B2B Edition의 소스](./sources/b2b.md) Marketo 및 B2B 데이터를 플랫폼으로 가져오는 방법에 대한 자세한 내용은 설명서를 참조하십시오.

## B2B 대상

Google Customer Match, Facebook, LinkedIn, Marketo Engage, Amazon S3, Google Display &amp; Video 360, Google Ads 및 Google Ad Manager와 같은 Experience Platform 대상을 사용할 수 있으며 Real-Time CDP B2B Edition에서 완전히 지원됩니다. 또한 Marketo Engage 대상은 Platform에서 세그먼트 멤버십 데이터를 스트리밍하여 Marketo의 목록으로 사용할 수 있도록 합니다.

의 개요를 참조하십시오. [Marketo Engage 대상](../destinations/catalog/adobe/marketo-engage.md) 추가 정보.

둘 이상의 CRM을 사용하는 회사의 경우, Real-Time CDP B2B Edition은 Marketo 또는 CRM의 인스턴스를 구분하도록 대상 커넥터를 구성하는 옵션을 제공합니다. 필요한 경우 각 인스턴스에 대상 커넥터를 구성하고 각 CRM 인스턴스에 독립적으로 대상을 보낼 수 있습니다.

## 다음 단계

이제 Real-Time CDP B2B Edition에서 제공하는 마케터의 이점, B2B Edition과 Real-Time CDP의 차이점을 파악하므로 이러한 기능을 고유한 IMS 조직에 적용하는 방법에 대해 학습할 수 있습니다.

Real-Time CDP B2B Edition이 B2B B2B Business Service Model을 통해 어떤 이점을 얻을 수 있는지 알아보려면 다음 설명서를 참조하여 시작하십시오.

* [Real-Time CDP B2B Edition의 사용 사례 예](./b2b-use-case.md)
* [Real-time Customer Data Platform B2B Edition에 대한 종단 간 자습서](./b2b-tutorial.md)
* [데이터를 수집하는 방법](./sources/b2b.md)
* [프로필에 액세스하는 방법](./profile/profile-overview.md)
* [Real-time Customer Data Platform B2B Edition의 스키마](./schemas/b2b.md)
* [세그먼트를 만드는 방법](./segmentation/b2b.md)
* [세그먼트를 대상에 활성화하는 방법](./destinations/b2b.md)
* [데이터 거버넌스 정책을 정의하고 적용하는 방법](./privacy/data-governance-overview.md)
