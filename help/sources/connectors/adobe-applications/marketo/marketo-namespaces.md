---
title: B2B 네임스페이스 및 스키마
description: 이 문서에서는 B2B 소스 커넥터를 만들 때 필요한 사용자 지정 네임스페이스에 대한 개요를 제공합니다.
exl-id: f1592be5-987e-41b8-9844-9dea5bd452b9
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1717'
ht-degree: 5%

---

# B2B 네임스페이스 및 스키마

>[!NOTE]
>
>Adobe Experience Platform UI의 템플릿을 사용하여 B2B 및 B2C 데이터에 대한 에셋을 신속하게 만들 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [platform UI에서 템플릿 사용](../../../tutorials/ui/templates.md).

이 문서에서는 B2B 소스에서 사용할 네임스페이스 및 스키마에 대한 기본 설정에 대한 정보를 제공합니다. 이 문서에서는 B2B 네임스페이스 및 스키마를 생성하는 데 필요한 Postman 자동화 유틸리티 설정에 대한 세부 정보도 제공합니다.

>[!IMPORTANT]
>
>다음에 대한 액세스 권한이 있어야 합니다. [Adobe Real-time Customer Data Platform 에디션](../../../../rtcdp/b2b-overview.md) B2B 스키마가 참여할 수 있도록 [실시간 고객 프로필](../../../../profile/home.md).

## B2B 네임스페이스 및 스키마 자동 생성 유틸리티 설정

B2B 네임스페이스 및 스키마 자동 생성 유틸리티를 사용하는 첫 번째 단계는 Platform 개발자 콘솔 및 [!DNL Postman] 환경.

- 여기에서 네임스페이스와 스키마 자동 생성 유틸리티 컬렉션 및 환경을 다운로드할 수 있습니다. [GitHub 저장소](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility).
- 필수 헤더에 대한 값을 수집하고 샘플 API 호출을 읽는 방법에 대한 세부 정보를 포함하여 Platform API 사용에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../../landing/api-guide.md).
- Platform API에 대한 자격 증명을 생성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../../landing/api-authentication.md).
- 설정 방법에 대한 자세한 정보 [!DNL Postman] platform API에 대해서는 다음 자습서를 참조하십시오. [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md).

Platform 개발자 콘솔 및 [!DNL Postman] 을(를) 설정하면 이제 적절한 환경 값을 [!DNL Postman] 환경.

다음 표에는 예제 값과 을 채우는 방법에 대한 추가 정보가 포함되어 있습니다. [!DNL Postman] 환경:

| 변수 | 설명 | 예 |
| --- | --- | --- |
| `CLIENT_SECRET` | 를 생성하는 데 사용되는 고유 식별자 `{ACCESS_TOKEN}`. 다음 튜토리얼 참조: [Experience Platform API 인증 및 액세스](../../../../landing/api-authentication.md) 을(를) 검색하는 방법에 대한 자세한 내용은 `{CLIENT_SECRET}`. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON 웹 토큰(JWT)은 {ACCESS_TOKEN}을 생성하는 데 사용되는 인증 자격 증명입니다. 다음 튜토리얼 참조: [Experience Platform API 인증 및 액세스](../../../../landing/api-authentication.md) 를 생성하는 방법에 대한 자세한 내용은 `{JWT_TOKEN}`. | `{JWT_TOKEN}` |
| `API_KEY` | Experience Platform API 호출을 인증하는 데 사용되는 고유 식별자입니다. 다음 튜토리얼 참조: [Experience Platform API 인증 및 액세스](../../../../landing/api-authentication.md) 을(를) 검색하는 방법에 대한 자세한 내용은 `{API_KEY}`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰입니다. 다음 튜토리얼 참조: [Experience Platform API 인증 및 액세스](../../../../landing/api-authentication.md) 을(를) 검색하는 방법에 대한 자세한 내용은 `{ACCESS_TOKEN}`. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | 에 관하여 [!DNL Marketo], 이 값은 고정되어 있으며 항상 다음으로 설정됩니다. `ent_dataservices_sdk`. | `ent_dataservices_sdk` |
| `CONTAINER_ID` | 다음 `global` 컨테이너에는 모든 표준 Adobe 및 Experience Platform 파트너가 제공한 클래스, 스키마 필드 그룹, 데이터 유형 및 스키마가 포함됩니다. 에 관하여 [!DNL Marketo], 이 값은 고정되며 항상 로 설정됩니다. `global`. | `global` |
| `PRIVATE_KEY` | 인증에 사용되는 자격 증명 [!DNL Postman] Experience Platform API에 대한 인스턴스. 개발자 콘솔 설정에 대한 자습서 및 [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md) {PRIVATE_KEY}을(를) 검색하는 방법에 대한 지침입니다. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Adobe I/O에 통합하는 데 사용되는 자격 증명입니다. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | IMS(Identity Management System)는 Adobe 서비스에 인증을 위한 프레임워크를 제공합니다. 에 관하여 [!DNL Marketo], 이 값은 고정되어 있으며 항상 다음과 같이 설정됩니다. `ims-na1.adobelogin.com`. | `ims-na1.adobelogin.com` |
| `IMS_ORG` | 제품 및 서비스를 소유하거나 라이선스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인 엔티티입니다. 다음 튜토리얼 참조: [개발자 콘솔 설정 및 [!DNL Postman]](../../../../landing/postman.md) 을(를) 검색하는 방법에 대한 지침을 보려면 `{ORG_ID}` 정보. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | 사용 중인 가상 샌드박스 파티션의 이름입니다. | `prod` |
| `TENANT_ID` | 만든 리소스의 이름 간격이 제대로 지정되고 조직 내에 포함되어 있는지 확인하는 데 사용되는 ID입니다. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | API 호출을 수행하는 URL 엔드포인트. 이 값은 고정되어 있으며 항상 다음과 같이 설정됩니다. `http://platform.adobe.io/`. | `http://platform.adobe.io/` |

{style="table-layout:auto"}

### 스크립트 실행

(으)로 [!DNL Postman] 컬렉션 및 환경이 설정되면 이제 [!DNL Postman] 인터페이스.

다음에서 [!DNL Postman] 인터페이스에서 자동 생성기 유틸리티의 루트 폴더를 선택한 다음 를 선택합니다. **[!DNL Run]** 맨 위 머리글에서

![루트 폴더](../images/marketo/root-folder.png)

다음 [!DNL Runner] 인터페이스가 나타납니다. 여기에서 모든 확인란이 선택되었는지 확인한 다음 를 선택합니다. **[!DNL Run Namespaces and Schemas Autogeneration Utility]**.

![런 제너레이터](../images/marketo/run-generator.png)

요청이 성공하면 B2B에 필요한 네임스페이스와 스키마가 만들어집니다.

## B2B 네임스페이스

ID 네임스페이스는 의 구성 요소입니다. [[!DNL Identity Service]](../../../../identity-service/home.md) id의 컨텍스트나 유형을 구별하는 역할을 합니다. 정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다. 다음을 참조하십시오. [네임스페이스 개요](../../../../identity-service/namespaces.md) 추가 정보.

B2B 네임스페이스는 엔티티의 기본 ID에서 사용됩니다.

다음 표에는 B2B 네임스페이스에 대한 기본 설정에 대한 정보가 나와 있습니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 표시 이름 | 신원 기호 | ID 유형 |
| --- | --- | --- |
| B2B 개인 | `b2b_person` | `CROSS_DEVICE` |
| B2B 계정 | `b2b_account` | `B2B_ACCOUNT` |
| B2B 영업 기회 | `b2b_opportunity` | `B2B_OPPORTUNITY` |
| B2B 영업 기회 사용자 관계 | `b2b_opportunity_person_relation` | `B2B_OPPORTUNITY_PERSON` |
| B2B 캠페인 | `b2b_campaign` | `B2B_CAMPAIGN` |
| B2B 캠페인 멤버 | `b2b_campaign_member` | `B2B_CAMPAIGN_MEMBER` |
| B2B 마케팅 목록 | `b2b_marketing_list` | `B2B_MARKETING_LIST` |
| B2B 마케팅 목록 구성원 | `b2b_marketing_list_member` | `B2B_MARKETING_LIST_MEMBER` |
| B2B 계정 사용자 관계 | `b2b_account_person_relation` | `B2B_ACCOUNT_PERSON` |

{style="table-layout:auto"}

## B2B 스키마

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 Platform에 수집하려면 먼저 데이터의 구조를 설명하고 각 필드 내에 포함할 수 있는 데이터 유형에 제약 조건을 제공하는 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다.

디자인 원칙 및 모범 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 [스키마 컴포지션 기본 사항](../../../../xdm/schema/composition.md).

다음 표에는 B2B 스키마의 기본 설정에 대한 정보가 포함되어 있습니다.

>[!NOTE]
>
>표의 전체 내용을 보려면 왼쪽/오른쪽으로 스크롤하십시오.

| 스키마 이름 | 기본 클래스 | 필드 그룹 | [!DNL Profile] 스키마에서 | 기본 ID | 기본 ID 네임스페이스 | 보조 ID | 보조 ID 네임스페이스 | 관계 | 참고 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| B2B 계정 | [XDM 비즈니스 계정](../../../../xdm/classes/b2b/business-account.md) | XDM 비즈니스 계정 세부 정보 | 활성화됨 | `accountKey.sourceKey` 기본 클래스에서 | B2B 계정 | `extSourceSystemAudit.externalKey.sourceKey` 기본 클래스에서 | B2B 계정 | <ul><li>`accountParentKey.sourceKey` XDM 비즈니스 계정 세부 정보 필드 그룹</li><li>대상 속성: `/accountKey/sourceKey`</li><li>유형: 일대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li></ul> |
| B2B 개인 | [XDM 개별 프로필](../../../../xdm/classes/individual-profile.md) | <ul><li>XDM 비즈니스 사용자 세부 정보</li><li>XDM 비즈니스 사용자 구성 요소</li><li>IdentityMap</li><li>동의 및 환경 설정 세부 정보</li></ul> | 활성화됨 | `b2b.personKey.sourceKey` XDM 비즈니스 사용자 세부 정보 필드 그룹 | B2B 개인 | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` / XDM 비즈니스 사용자 세부 정보 필드 그룹</li><li>`workEmail.address` / XDM 비즈니스 사용자 세부 정보 필드 그룹</ol></li> | <ol><li>B2B 개인</li><li>이메일</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` / XDM 비즈니스 사용자 구성 요소 필드 그룹</li><li>유형: 다대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li><li>대상 속성: accountKey.sourceKey</li><li>현재 스키마의 관계 이름: 계정</li><li>참조 스키마의 관계 이름: 사람</li></ul> |
| B2B 영업 기회 | [XDM 비즈니스 영업 기회](../../../../xdm/classes/b2b/business-opportunity.md) | XDM 비즈니스 영업 기회 세부 정보 | 활성화됨 | `opportunityKey.sourceKey` 기본 클래스에서 | B2B 영업 기회 | `extSourceSystemAudit.externalKey.sourceKey` 기본 클래스에서 | B2B 영업 기회 | <ul><li>`accountKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li><li>대상 속성: `accountKey.sourceKey`</li><li>현재 스키마의 관계 이름: 계정</li><li>참조 스키마의 관계 이름: 기회</li></ul> |
| B2B 영업 기회 사용자 관계 | [XDM 비즈니스 영업 기회 사용자 관계](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) | None | 활성화됨 | `opportunityPersonKey.sourceKey` 기본 클래스에서 | B2B 영업 기회 사용자 관계 | `extSourceSystemAudit.externalKey.sourceKey` 기본 클래스에서 | B2B 영업 기회 사용자 관계 | **첫 번째 관계**<ul><li>`personKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: b2b.personKey.sourceKey</li><li>현재 스키마의 관계 이름: 개인</li><li>참조 스키마의 관계 이름: 기회</li></ul>**두 번째 관계**<ul><li>`opportunityKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 영업 기회 </li><li>네임스페이스: B2B 영업 기회 </li><li>대상 속성: `opportunityKey.sourceKey`</li><li>현재 스키마의 관계 이름: Opportunity</li><li>참조 스키마의 관계 이름: 사람</li></ul> |
| B2B 캠페인 | [XDM 비즈니스 캠페인](../../../../xdm/classes/b2b/business-campaign.md) | XDM 비즈니스 캠페인 세부 정보 | 활성화됨 | `campaignKey.sourceKey` 기본 클래스에서 | B2B 캠페인 | `extSourceSystemAudit.externalKey.sourceKey` 기본 클래스에서 | B2B 캠페인 |
| B2B 캠페인 멤버 | [XDM 비즈니스 캠페인 멤버](../../../../xdm/classes/b2b/business-campaign-members.md) | XDM 비즈니스 캠페인 멤버 세부 정보 | 활성화됨 | `ccampaignMemberKey.sourceKey` 기본 클래스에서 | B2B 캠페인 멤버 | `extSourceSystemAudit.externalKey.sourceKey` 기본 클래스에서 | B2B 캠페인 멤버 | **첫 번째 관계**<ul><li>`personKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: `b2b.personKey.sourceKey`</li><li>현재 스키마의 관계 이름: 개인</li><li>참조 스키마의 관계 이름: 캠페인</li></ul>**두 번째 관계**<ul><li>`campaignKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 캠페인</li><li>네임스페이스: B2B 캠페인</li><li>대상 속성: `campaignKey.sourceKey`</li><li>현재 스키마의 관계 이름: 캠페인</li><li>참조 스키마의 관계 이름: 사람</li></ul> |
| B2B 마케팅 목록 | [XDM 비즈니스 마케팅 목록](../../../../xdm/classes/b2b/business-marketing-list.md) | None | 활성화됨 | `marketingListKey.sourceKey` 기본 클래스에서 | B2B 마케팅 목록 | None | None | None | 정적 목록이에서 동기화되지 않음 [!DNL Salesforce] 따라서 에는 보조 ID가 없습니다. |
| B2B 마케팅 목록 구성원 | [XDM 비즈니스 마케팅 목록 멤버](../../../../xdm/classes/b2b/business-marketing-list-members.md) | None | 활성화됨 | `marketingListMemberKey.sourceKey` 기본 클래스에서 | B2B 마케팅 목록 구성원 | None | None | **첫 번째 관계**<ul><li>`PersonKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: `b2b.personKey.sourceKey`</li><li>현재 스키마의 관계 이름: 개인</li><li>참조 스키마의 관계 이름: 마케팅 목록</li></ul>**두 번째 관계**<ul><li>`marketingListKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 마케팅 목록</li><li>네임스페이스: B2B 마케팅 목록</li><li>대상 속성: `marketingListKey.sourceKey`</li><li>현재 스키마의 관계 이름: 마케팅 목록</li><li>참조 스키마의 관계 이름: 사람</li></ul> | 정적 목록 멤버가에서 동기화되지 않음 [!DNL Salesforce] 따라서 에는 보조 ID가 없습니다. |
| B2B 활동 | [XDM ExperienceEvent](../../../../xdm/classes/experienceevent.md) | <ul><li>WebPage 방문</li><li>새 잠재 고객</li><li>잠재 고객 전환</li><li>목록에 추가</li><li>목록에서 제거</li><li>영업 기회에 추가</li><li>영업 기회에서 제거</li><li>작성된 양식</li><li>링크 클릭수</li><li>이메일 전달됨</li><li>이메일 열림</li><li>이메일 클릭됨</li><li>반송된 이메일</li><li>가볍게 반송된 이메일</li><li>이메일 구독 취소됨</li><li>점수 변경됨</li><li>영업 기회 업데이트됨</li><li>캠페인 진행률 상태 변경됨</li><li>개인 식별자</li><li>Marketo 웹 URL</li><li>즐거운 순간</li><li>Webhook 호출</li><li>캠페인 케이던스 변경</li><li>수익 단계 변경됨</li><li>잠재 고객 병합</li><li>이메일 전송됨</li><li>캠페인 스트림 변경</li><li>Campaign에 추가</li></ul> | 활성화됨 | `personKey.sourceKey` 사용자 식별자 필드 그룹 중 | B2B 개인 | None | None | **첫 번째 관계**<ul><li>`listOperations.listKey.sourceKey` 필드</li><li>유형: 일대일</li><li>참조 스키마: B2B 마케팅 목록</li><li>네임스페이스: B2B 마케팅 목록</li></ul>**두 번째 관계**<ul><li>`opportunityEvent.opportunityKey.sourceKey` 필드</li><li>유형: 일대일</li><li>참조 스키마: B2B 영업 기회</li><li>네임스페이스: B2B 영업 기회</li></ul>**세 번째 관계**<ul><li>`leadOperation.campaignProgression.campaignKey.sourceKey` 필드</li><li>유형: 일대일</li><li>참조 스키마: B2B 캠페인</li><li>네임스페이스: B2B 캠페인</li></ul> | `ExperienceEvent` 는 엔티티와 다릅니다. 경험 이벤트 ID는 활동을 수행한 사용자입니다. |
| B2B 계정 사용자 관계 | [XDM 비즈니스 계정 사용자 관계](../../../../xdm/classes/b2b/business-account-person-relation.md) | ID 맵 | 활성화됨 | `accountPersonKey.sourceKey` 기본 클래스에서 | B2B 계정 사용자 관계 | None | None | **첫 번째 관계**<ul><li>`personKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 개인</li><li>네임스페이스: B2B 개인</li><li>대상 속성: `b2b.personKey.SourceKey`</li><li>현재 스키마의 관계 이름: 사람</li><li>참조 스키마의 관계 이름: 계정</li></ul>**두 번째 관계**<ul><li>`accountKey.sourceKey` 기본 클래스에서</li><li>유형: 다대일</li><li>참조 스키마: B2B 계정</li><li>네임스페이스: B2B 계정</li><li>대상 속성: `accountKey.sourceKey`</li><li>현재 스키마의 관계 이름: 계정</li><li>참조 스키마의 관계 이름: 사람</li></ul> |

{style="table-layout:auto"}

## 다음 단계

연결 방법을 알아보려면 [!DNL Marketo] 데이터를 플랫폼으로 전송하는 방법에 대한 자습서를 참조하십시오. [ui에서 Marketo 소스 커넥터 만들기](../../../tutorials/ui/create/adobe-applications/marketo.md).
