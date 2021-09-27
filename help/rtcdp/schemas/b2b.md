---
title: 실시간 고객 데이터 플랫폼 B2B 에디션의 스키마
description: 실시간 고객 데이터 플랫폼 B2B 에디션에서 XDM(Experience Data Model) 스키마의 역할에 대한 개요입니다.
source-git-commit: a8c322cfe02c7a005275ec33e5dac92d2f76667a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 실시간 고객 데이터 플랫폼 B2B 에디션의 스키마

실시간 고객 데이터 플랫폼 B2B Edition은 계정, 기회, 캠페인 등과 같은 필수 B2B 데이터 엔티티에 대한 세부 사항을 캡처하는 몇 가지 표준 [XDM(Experience Data Model) 클래스](../../xdm/schema/composition.md#class)를 제공합니다. 또한 실시간 CDP B2B Edition을 사용하면 이러한 스키마 간에 다대다 관계를 정의하여 고급 세그멘테이션 사용 사례에 참여할 수 있습니다.

실시간 CDP B2B Edition에서는 다음과 같은 표준 클래스가 제공됩니다.

* [XDM 비즈니스 계정](../../xdm/classes/b2b/business-account.md)
* [XDM 비즈니스 계정 담당자 관계](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM 비즈니스 캠페인](../../xdm/classes/b2b/business-campaign.md)
* [XDM 비즈니스 캠페인 구성원](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM 비즈니스 기회](../../xdm/classes/b2b/business-opportunity.md)
* [XDM 비즈니스 기회 개인 관계](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM 비즈니스 마케팅 목록](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM 비즈니스 마케팅 목록 구성원](../../xdm/classes/b2b/business-marketing-list-members.md)

두 스키마 간에 다대다 관계를 만드는 방법에 대한 단계는 [B2B 스키마 관계 정의](../../xdm/tutorials/relationship-b2b.md)에 있는 자습서를 참조하십시오.

B2B 소스 연결을 사용하는 경우 도구를 사용하여 필요한 스키마와 이 스키마 간의 관계를 자동으로 생성할 수 있습니다. 자세한 내용은 소스 설명서에서 [B2B 네임스페이스](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)에 대한 안내서를 참조하십시오.
