---
title: Real-Time Customer Data Platform B2B edition의 스키마
description: Adobe Real-Time Customer Data Platform B2B edition의 XDM(Experience Data Model) 스키마 역할에 대한 개요입니다.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 0191fc8419c696d8cd114a5eb575b8cc0a815a72
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 8%

---

# Real-Time Customer Data Platform B2B edition의 스키마

Adobe Real-Time Customer Data Platform B2B edition은 계정, 기회, 캠페인 등 필수 B2B 데이터 엔터티에 대한 세부 정보를 캡처하는 몇 가지 표준 [XDM(경험 데이터 모델) 클래스](../../xdm/schema/composition.md#class)를 제공합니다. 또한 Real-Time CDP B2B edition을 사용하면 이러한 스키마 간의 다대일 관계를 정의하여 고급 세분화 사용 사례에 참여할 수 있습니다.

>[!IMPORTANT]
>
>B2B 스키마는 Experience Platform 응용 프로그램(예: [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition))에서 사용할 수 있습니다. <br/>그러나 (의 프로필) B2B 스키마가 [실시간 고객 프로필](../../profile/home.md)에 참여하려면 Real-Time CDP B2B edition에 액세스할 수 있어야 합니다.

Real-Time CDP B2B edition에는 다음과 같은 표준 클래스가 제공됩니다.

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


다음 표에는 B2B 스키마의 기본 설정에 대한 정보가 포함되어 있습니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 스키마 이름 | 기본 클래스 | 필드 그룹 | 스키마의 [!DNL Profile] | 기본 ID | 기본 ID 네임스페이스 | 보조 ID | 보조 ID 네임스페이스 | 관계 | 참고 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B 계정 | [XDM 비즈니스 계정](../../xdm/classes/b2b/business-account.md) | XDM 비즈니스 계정 세부 정보 | 활성화됨 | 기본 클래스의 `accountKey.sourceKey` | B2B 계정 | 기본 클래스의 `extSourceSystemAudit.externalKey.sourceKey` | B2B 계정 | <ul><li>XDM 비즈니스 계정 세부 정보 필드 그룹의 `accountParentKey.sourceKey`</li><li>대상 속성: `/accountKey/sourceKey`</li><li>유형: 일대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li></ul> |
| B2B 개인 | [XDM 개별 프로필](../../xdm/classes/individual-profile.md) | <ul><li>XDM 비즈니스 사용자 세부 정보</li><li>XDM 비즈니스 사용자 구성 요소</li><li>IdentityMap</li><li>동의 및 환경 설정 세부 정보</li></ul> | 활성화됨 | XDM 비즈니스 사용자 세부 정보 필드 그룹의 `b2b.personKey.sourceKey` | B2B 개인 | <ol><li>XDM 비즈니스 사용자 세부 정보 필드 그룹의 `extSourceSystemAudit.externalKey.sourceKey`</li><li>XDM 비즈니스 사용자 세부 정보 필드 그룹의 `workEmail.address`</ol></li> | <ol><li>B2B 개인</li><li>이메일</li></ol> | <ul><li>XDM 비즈니스 사용자 구성 요소 필드 그룹의 `personComponents.sourceAccountKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li><li>대상 속성: accountKey.sourceKey</li><li>현재 스키마의 관계 이름: 계정</li><li>참조 스키마의 관계 이름: 사람</li></ul> |
| B2B 기회 | [XDM 비즈니스 영업 기회](../../xdm/classes/b2b/business-opportunity.md) | XDM 비즈니스 영업 기회 세부 정보 | 활성화됨 | 기본 클래스의 `opportunityKey.sourceKey` | B2B 기회 | 기본 클래스의 `extSourceSystemAudit.externalKey.sourceKey` | B2B 기회 | <ul><li>기본 클래스의 `accountKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li><li>대상 속성: `accountKey.sourceKey`</li><li>현재 스키마의 관계 이름: 계정</li><li>참조 스키마의 관계 이름: 기회</li></ul> |
| B2B 영업 기회 사용자 관계 | [XDM 비즈니스 영업 기회 사용자 관계](../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 활성화됨 | 기본 클래스의 `opportunityPersonKey.sourceKey` | B2B 영업 기회 사용자 관계 | | | **첫 번째 관계**<ul><li>기본 클래스의 `personKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: b2b.personKey.sourceKey</li><li>현재 스키마의 관계 이름: 개인</li><li>참조 스키마의 관계 이름: 기회</li></ul>**두 번째 관계**<ul><li>기본 클래스의 `opportunityKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 영업 기회 </li><li>네임스페이스: B2B 영업 기회 </li><li>대상 속성: `opportunityKey.sourceKey`</li><li>현재 스키마의 관계 이름: Opportunity</li><li>참조 스키마의 관계 이름: 사람</li></ul> |
| B2B 캠페인 | [XDM 비즈니스 캠페인](../../xdm/classes/b2b/business-campaign.md) | XDM 비즈니스 캠페인 세부 정보 | 활성화됨 | 기본 클래스의 `campaignKey.sourceKey` | B2B 캠페인 | | |
| B2B 캠페인 멤버 | [XDM 비즈니스 캠페인 멤버](../../xdm/classes/b2b/business-campaign-members.md) | XDM 비즈니스 캠페인 멤버 세부 정보 | 활성화됨 | 기본 클래스의 `ccampaignMemberKey.sourceKey` | B2B 캠페인 멤버 | | | **첫 번째 관계**<ul><li>기본 클래스의 `personKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: `b2b.personKey.sourceKey`</li><li>현재 스키마의 관계 이름: 개인</li><li>참조 스키마의 관계 이름: 캠페인</li></ul>**두 번째 관계**<ul><li>기본 클래스의 `campaignKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 캠페인</li><li>네임스페이스: B2B 캠페인</li><li>대상 속성: `campaignKey.sourceKey`</li><li>현재 스키마의 관계 이름: 캠페인</li><li>참조 스키마의 관계 이름: 사람</li></ul> |
| B2B 마케팅 목록 | [XDM 비즈니스 마케팅 목록](../../xdm/classes/b2b/business-marketing-list.md) | None | 활성화됨 | 기본 클래스의 `marketingListKey.sourceKey` | B2B 마케팅 목록 | None | None | None | 정적 목록이 [!DNL Salesforce]에서 동기화되지 않았으므로 보조 ID가 없습니다. |
| B2B 마케팅 목록 멤버 | [XDM 비즈니스 마케팅 목록 구성원](../../xdm/classes/b2b/business-marketing-list-members.md) | None | 활성화됨 | 기본 클래스의 `marketingListMemberKey.sourceKey` | B2B 마케팅 목록 멤버 | None | None | **첫 번째 관계**<ul><li>기본 클래스의 `PersonKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: `b2b.personKey.sourceKey`</li><li>현재 스키마의 관계 이름: 개인</li><li>참조 스키마의 관계 이름: 마케팅 목록</li></ul>**두 번째 관계**<ul><li>기본 클래스의 `marketingListKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 마케팅 목록</li><li>네임스페이스: B2B 마케팅 목록</li><li>대상 속성: `marketingListKey.sourceKey`</li><li>현재 스키마의 관계 이름: 마케팅 목록</li><li>참조 스키마의 관계 이름: 사람</li></ul> | 정적 목록 멤버가 [!DNL Salesforce]에서 동기화되지 않았으므로 보조 ID가 없습니다. |
| B2B 계정 사용자 관계 | [XDM 비즈니스 계정 사용자 관계](../../xdm/classes/b2b/business-account-person-relation.md) | ID 맵 | 활성화됨 | 기본 클래스의 `accountPersonKey.sourceKey` | B2B 계정 사용자 관계 | None | None | **첫 번째 관계**<ul><li>기본 클래스의 `personKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: `b2b.personKey.SourceKey`</li><li>현재 스키마의 관계 이름: 사람</li><li>참조 스키마의 관계 이름: 계정</li></ul>**두 번째 관계**<ul><li>기본 클래스의 `accountKey.sourceKey`</li><li>유형: 다대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li><li>대상 속성: `accountKey.sourceKey`</li><li>현재 스키마의 관계 이름: 계정</li><li>참조 스키마의 관계 이름: 사람</li></ul> |

{style="table-layout:auto"}

