---
keywords: 이메일;이메일;이메일;이메일 대상
title: 이메일 마케팅 대상 개요
type: Tutorial
description: ESP(이메일 서비스 공급자)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: ccbc633bfce8f4f66577b50064c28cfc26cb6dca
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---

# 이메일 마케팅 대상 개요 {#email-marketing-destinations}

## 개요 {#overview}

ESP(이메일 서비스 공급자)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다. Adobe Experience Platform은 세그먼트를 이메일 마케팅 대상에 활성화할 수 있도록 하여 ESP와 통합됩니다.

플랫폼이 세그먼트를 로 내보냅니다. `.csv` 파일을 만든 후 원하는 위치로 배달합니다. 에 활성화된 저장소 위치에서 이메일 마케팅 플랫폼에서의 데이터 가져오기 예약 [!DNL Platform]. 데이터를 가져오는 프로세스는 파트너마다 다릅니다. 자세한 내용은 개별 대상 문서를 참조하십시오.

## 지원되는 이메일 마케팅 대상 {#supported-destinations}

Adobe Experience Platform은 다음과 같은 이메일 마케팅 대상을 지원합니다.

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)
* [SendGrid](sendgrid.md)

## 새 이메일 마케팅 대상에 연결 {#connect-destination}

캠페인을 위해 세그먼트를 이메일 마케팅 대상으로 보내려면 먼저 Platform이 대상에 연결해야 합니다. 다음을 참조하십시오. [대상 만들기 튜토리얼](../../ui/connect-destination.md) 새 대상 설정에 대한 자세한 정보.

## 이메일 마케팅 대상으로 대상자를 활성화할 때의 모범 사례 {#best-practices}

### ID 선택 {#identity}

Adobe은 다음 위치에서 고유 식별자를 선택할 것을 권장합니다. [유니온 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 사용자 ID를 키로 사용하는 필드입니다. 가장 일반적으로 이 필드는 이메일 주소이지만 고객 충성도 프로그램 ID 또는 전화번호일 수도 있습니다. 스키마에서 가장 일반적인 고유 식별자 및 해당 XDM 필드는 아래 표를 참조하십시오.

| 고유 식별자 | 통합 스키마의 XDM 필드 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| 전화 | `mobilePhone.number` |
| 고객 충성도 프로그램 ID | `Customer-defined XDM field` |

### 기타 대상 속성

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

## 저장소 위치에서 대상으로 데이터 가져오기 {#import-data-into-destination}

스토리지 위치에서 대상으로 데이터를 가져오는 방법을 알아보려면 개별 이메일 마케팅 대상 문서를 참조하십시오.

* [Adobe Campaign](adobe-campaign.md)
* [Oracle Eloqua](oracle-eloqua.md)
* [Oracle Responsys](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## 이메일 마케팅 대상에 세그먼트 활성화 {#activate}

이메일 마케팅 대상에 세그먼트를 활성화하는 방법에 대한 지침은 을 참조하십시오. [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md).

## 추가 리소스

* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](../../ui/activate-batch-profile-destinations.md)
* [플로우 서비스 API를 사용하여 이메일 마케팅 대상 만들기 및 데이터 활성화](../../api/connect-activate-batch-destinations.md)
