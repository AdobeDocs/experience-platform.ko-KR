---
keywords: 이메일;이메일;이메일;이메일 대상
title: 이메일 마케팅 대상 개요
type: Tutorial
description: ESP(이메일 서비스 공급자)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---

# 이메일 마케팅 대상 개요 {#email-marketing-destinations}

## 개요 {#overview}

ESP(이메일 서비스 제공업체)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다. Adobe Experience Platform은 세그먼트를 이메일 마케팅 대상에 활성화할 수 있으므로 ESP와 통합됩니다.

플랫폼은 세그먼트를 `.csv` 파일로 내보내고 기본 위치로 전달합니다. [!DNL Platform]에 활성화된 저장 위치에서 이메일 마케팅 플랫폼에서 데이터 가져오기를 예약합니다. 데이터를 가져오는 프로세스는 파트너마다 다릅니다. 자세한 내용은 개별 대상 문서를 참조하십시오.

## 지원되는 이메일 마케팅 대상 {#supported-destinations}

Adobe Experience Platform은 다음과 같은 이메일 마케팅 대상을 지원합니다.

* [Adobe Campaign](adobe-campaign.md)
* [Oracle 언달라](oracle-eloqua.md)
* [Responsys oracle](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## 새 이메일 마케팅 대상에 연결 {#connect-destination}

캠페인을 위해 이메일 마케팅 대상에 세그먼트를 보내려면 먼저 대상에 연결해야 합니다. 새 대상 설정에 대한 자세한 내용은 [대상 만들기 자습서](../../ui/connect-destination.md)를 참조하십시오.

## 대상을 이메일 마케팅 대상으로 활성화할 때의 모범 사례 {#best-practices}

### ID 선택 {#identity}

Adobe은 [결합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유 식별자를 선택할 것을 권장합니다. 사용자 ID가 키로 사용하는 필드입니다. 가장 일반적으로 이 필드는 이메일 주소이지만 충성도 프로그램 ID 또는 전화 번호일 수도 있습니다. 스키마의 가장 일반적인 고유 식별자 및 XDM 필드에 대해서는 아래 표를 참조하십시오.

| 고유 식별자 | 통합 스키마의 XDM 필드 |
|----------------- | ---------------------------|
| Email Address | `personalEmail.address` |
| 전화 | `mobilePhone.number` |
| 충성도 프로그램 ID | `Customer-defined XDM field` |

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

## 저장소 위치의 데이터를 대상으로 가져오기 {#import-data-into-destination}

개별 이메일 마케팅 대상 문서를 참조하여 스토리지 위치에서 대상으로 데이터를 가져오는 방법을 알아보십시오.

* [Adobe Campaign](adobe-campaign.md)
* [Oracle 언달라](oracle-eloqua.md)
* [Responsys oracle](oracle-responsys.md)
* [Salesforce Marketing Cloud](salesforce-marketing-cloud.md)

## 이메일 마케팅 대상에 세그먼트 활성화 {#activate}

세그먼트를 이메일 마케팅 대상에 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 대상에 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 추가 리소스

* [대상에 데이터 활성화](../../ui/activate-destinations.md)
* [Flow Service API를 사용하여 이메일 마케팅 대상을 만들고 데이터를 활성화합니다](../../api/email-marketing.md)
