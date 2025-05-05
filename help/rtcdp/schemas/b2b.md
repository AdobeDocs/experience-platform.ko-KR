---
title: Real-time Customer Data Platform B2B 에디션의 스키마
description: Adobe Real-time Customer Data Platform B2B 에디션의 XDM(Experience Data Model) 스키마 역할에 대한 개요입니다.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B 버전" type="Informative" url="https://helpx.adobe.com/kr/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 13%

---

# Real-time Customer Data Platform B2B 에디션의 스키마

Adobe Real-time Customer Data Platform B2B 에디션은 계정, 기회, 캠페인 등 필수 B2B 데이터 엔터티에 대한 세부 정보를 캡처하는 몇 가지 표준 [XDM(경험 데이터 모델) 클래스](../../xdm/schema/composition.md#class)를 제공합니다. 또한 Real-Time CDP B2B 에디션을 사용하면 이러한 스키마 간의 다대일 관계를 정의하여 고급 세분화 사용 사례에 참여할 수 있습니다.

>[!IMPORTANT]
>
>B2B 스키마가 [실시간 고객 프로필](../../profile/home.md)에 참여하려면 Real-Time CDP B2B 에디션에 액세스할 수 있어야 합니다.

Real-Time CDP B2B Edition에서는 다음 표준 클래스가 제공됩니다.

* [XDM 비즈니스 계정](../../xdm/classes/b2b/business-account.md)
* [XDM 비즈니스 계정 사용자 관계](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM 비즈니스 캠페인](../../xdm/classes/b2b/business-campaign.md)
* [XDM 비즈니스 캠페인 멤버](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM 비즈니스 영업 기회](../../xdm/classes/b2b/business-opportunity.md)
* [XDM 비즈니스 영업 기회 사용자 관계](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [XDM 비즈니스 마케팅 목록](../../xdm/classes/b2b/business-marketing-list.md)
* [XDM 비즈니스 마케팅 목록 멤버](../../xdm/classes/b2b/business-marketing-list-members.md)

스키마가 B2B 워크플로우에 어떻게 적합한지 이해하려면 [전체 튜토리얼](../b2b-tutorial.md)을 참조하세요.

두 스키마 간에 다대일 관계를 만드는 방법에 대한 단계는 [B2B 스키마 관계 정의](../../xdm/tutorials/relationship-b2b.md)에 대한 자습서를 참조하십시오.

B2B 소스 연결을 사용하는 경우 도구를 사용하여 필요한 스키마와 스키마 간의 관계를 자동으로 생성할 수 있습니다. 자세한 내용은 소스 설명서의 [B2B 네임스페이스](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md)에 대한 안내서를 참조하십시오.
