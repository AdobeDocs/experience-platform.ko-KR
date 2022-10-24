---
title: Real-time Customer Data Platform B2B Edition의 스키마
description: Adobe Real-time Customer Data Platform B2B Edition에서 XDM(Experience Data Model) 스키마의 역할에 대한 개요입니다.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Real-time Customer Data Platform B2B Edition의 스키마

Adobe Real-time Customer Data Platform B2B Edition은 몇 가지 표준을 제공합니다 [XDM(경험 데이터 모델) 클래스](../../xdm/schema/composition.md#class) 계정, 기회, 캠페인 등과 같은 중요한 B2B 데이터 엔티티에 대한 세부 사항을 캡처합니다. 또한 Real-Time CDP B2B Edition을 사용하면 이러한 스키마 간에 다대다 관계를 정의하여 고급 세그먼테이션 사용 사례에 참여할 수 있습니다.

>[!IMPORTANT]
>
>B2B 스키마가 참여하려면 Real-Time CDP B2B Edition에 액세스할 수 있어야 합니다 [실시간 고객 프로필](../../profile/home.md).

다음 표준 클래스는 Real-Time CDP B2B Edition에서 제공됩니다.

* [XDM 비즈니스 계정](../../xdm/classes/b2b/business-account.md)
* [XDM 비즈니스 계정 담당자 관계](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM 비즈니스 캠페인](../../xdm/classes/b2b/business-campaign.md)
* [XDM 비즈니스 캠페인 구성원](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM 비즈니스 기회](../../xdm/classes/b2b/business-opportunity.md)
* [XDM 비즈니스 기회 개인 관계](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM 비즈니스 마케팅 목록](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM 비즈니스 마케팅 목록 구성원](../../xdm/classes/b2b/business-marketing-list-members.md)

스키마가 B2B 워크플로우에 맞는 방식을 이해하려면 [엔드 투 엔드 자습서](../b2b-tutorial.md).

두 스키마 간에 다대다 관계를 만드는 방법에 대한 단계는 [B2B 스키마 관계 정의](../../xdm/tutorials/relationship-b2b.md).

B2B 소스 연결을 사용하는 경우 도구를 사용하여 필요한 스키마와 이 스키마 간의 관계를 자동으로 생성할 수 있습니다. 다음 안내서를 참조하십시오. [B2B 네임스페이스](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) 를 참조하십시오.
