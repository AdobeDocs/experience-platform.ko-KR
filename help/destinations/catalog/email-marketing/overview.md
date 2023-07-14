---
keywords: 이메일;이메일;이메일;이메일 대상
title: 이메일 마케팅 대상 개요
type: Tutorial
description: ESP(이메일 서비스 공급자)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다. Experience Platform 대상으로 지원되는 ESP에 대해 알아봅니다.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 5%

---

# 이메일 마케팅 대상 개요 {#email-marketing-destinations}

## 개요 {#overview}

ESP(이메일 서비스 공급자)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다. Adobe Experience Platform은 이메일 마케팅 대상에 대한 대상을 활성화할 수 있도록 하여 ESP와 통합됩니다.

## 지원되는 이메일 마케팅 대상 {#supported-destinations}

Adobe Experience Platform은 다음과 같은 이메일 마케팅 대상을 지원합니다.

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Mailchimp 관심 카테고리](mailchimp-interest-categories.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(파일) Oracle Eloqua](oracle-eloqua.md)
* [(파일) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## 새 이메일 마케팅 대상에 연결 {#connect-destination}

캠페인을 위한 이메일 마케팅 대상으로 대상자를 보내려면 먼저 Platform이 대상에 연결해야 합니다. 다음을 참조하십시오. [대상 만들기 튜토리얼](../../ui/connect-destination.md) 새 대상 설정에 대한 자세한 정보.

## 이메일 마케팅 대상으로 대상자를 활성화할 때의 모범 사례 {#best-practices}

### ID 선택 {#identity}

Adobe은 다음 위치에서 고유 식별자를 선택할 것을 권장합니다. [유니온 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 사용자 ID를 키로 사용하는 필드입니다. 가장 일반적으로 이 필드는 이메일 주소이지만 고객 충성도 프로그램 ID 또는 전화번호일 수도 있습니다. 스키마에서 가장 일반적인 고유 식별자 및 해당 XDM 필드는 아래 표를 참조하십시오.

| 고유 식별자 | 통합 스키마의 XDM 필드 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| 전화 | `mobilePhone.number` |
| 고객 충성도 프로그램 ID | `Customer-defined XDM field` |

{style="table-layout:auto"}

### 기타 대상 속성 {#other-destination-attributes}

스키마 필드 선택기에서 이메일 대상으로 내보낼 다른 필드를 선택합니다. 몇 가지 권장 옵션은 다음과 같습니다.

| 스키마 | XDM 필드 |
|------ | ---------|
| 이름 | `person.name.firstName` |
| 성 | `person.name.lastName` |
| 전화 | `mobilePhone.number` |
| 주소 구/군/시 | `homeAddress.city` |
| 주소 상태 | `homeAddress.stateProvince` |
| 주소 우편 번호 | `homeAddress.postalCode` |
| 생일 | `person.birthDayAndMonth` |
| 세그먼트 멤버십 | `segmentMembership.status` |

{style="table-layout:auto"}

## 이메일 마케팅 대상에 대상자 활성화 {#activate}

카탈로그의 일부 이메일 마케팅 대상은 대상과의 API 통합을 통해 스트리밍 방식으로 프로필을 내보냅니다.

다른 대상은 파일을 클라우드 스토리지 위치로 내보냅니다. 내보내기가 완료되면 클라우드 스토리지 위치에서 이메일 마케팅 대상으로 데이터를 가져와야 합니다.

다음 링크를 따르십시오. [지원되는 이메일 마케팅 대상](#supported-destinations) 섹션을 통해 각 이메일 마케팅 대상에 대해 대상자를 활성화하는 방법을 알아보십시오.

## 추가 리소스 {#additional-resources}

* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md)
* [플로우 서비스 API를 사용하여 이메일 마케팅 대상 만들기 및 데이터 활성화](../../api/connect-activate-batch-destinations.md)
