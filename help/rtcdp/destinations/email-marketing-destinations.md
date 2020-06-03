---
title: 이메일 마케팅 대상
seo-title: 이메일 마케팅 대상
description: ESP(Email Service Providers)를 사용하면 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
seo-description: ESP(Email Service Providers)를 사용하면 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
translation-type: tm+mt
source-git-commit: 121ae74e9c352b1f6fc12093d815e711ebd817b8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 2%

---


# 이메일 마케팅 대상 {#email-marketing-destinations}

ESP(Email Service Providers)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다. 실시간 고객 데이터 플랫폼은 이메일 마케팅 대상으로 세그먼트를 활성화할 수 있으므로 ESP와 통합됩니다.

캠페인을 위한 이메일 마케팅 대상으로 세그먼트를 전송하려면 Adobe 실시간 CDP가 먼저 대상에 연결해야 합니다.

이메일 마케팅 대상에 연결하는 프로세스는 3단계로 이루어집니다. 각 단계는 이 페이지의 아래에 자세히 설명되어 있습니다.

아래 섹션에 설명된 연결 대상 플로우에서 Amazon S3 또는 SFTP에 연결합니다. 실시간 CDP는 세그먼트를 `.csv` 또는 `.txt` 파일로 내보내 원하는 위치에 전달합니다. 실시간 CDP에서 활성화된 스토리지 위치에서 이메일 마케팅 플랫폼에서 데이터를 가져올 수 있도록 예약합니다. 데이터를 가져오는 프로세스는 각 파트너마다 다릅니다. 자세한 내용은 개별 대상 아티클을 참조하십시오.

## 1단계 - 연결 대상 {#connect-destination}

1. [ **[!UICONTROL 연결] > [대상]**]에서 연결할 이메일 마케팅 대상을 선택한 다음 **[!UICONTROL 연결 대상을 선택합니다]**.

   ![대상에 연결](/help/rtcdp/destinations/assets/connect-destination-1.png)

2. Connect 마법사에서 저장소 위치에 대한 **[!UICONTROL 연결 유형을]** 선택합니다. Amazon **S3**, 암호가 **있는 SFTP**, **SSH 키가 있는** SFTP중에서 선택할 수 있습니다. 연결 유형에 따라 아래 정보를 입력한 다음 **[!UICONTROL Connect를 선택합니다]**.

S3 **연결의**&#x200B;경우 액세스 키 ID와 비밀 액세스 키를 제공해야 합니다.

암호 **가** 연결된 SFTP의 경우 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.

SSH 키 **** 연결이 있는 SFTP의 경우 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

## 2단계 - 내보낸 파일에서 대상 특성으로 사용할 스키마 필드를 선택합니다. {#destination-attributes}

이 단계에서는 이메일 마케팅 대상으로 내보낼 필드를 선택합니다.

![대상 속성](/help/rtcdp/destinations/assets/destination-attributes.png)

### ID {#identity}

조합 스키마에서 고유 식별자를 선택하는 것이 [좋습니다](../../profile/home.md#profile-fragments-and-union-schemas). 사용자 ID가 꺼져 있는 필드입니다. 일반적으로 이 필드는 이메일 주소이지만 충성도 프로그램 ID 또는 전화 번호일 수도 있습니다. 통합 스키마에서 가장 일반적인 고유 식별자 및 XDM 필드는 아래 표를 참조하십시오.

| 고유 식별자 | 통합 스키마의 XDM 필드 |
---------|----------
| 이메일 주소 | `personalEmail.address` |
| 전화 | `mobilePhone.number` |
| 충성도 프로그램 ID | `Customer-defined XDM field` |

### 기타 대상 속성

스키마 필드 선택기에서 이메일 대상으로 내보낼 다른 필드를 선택합니다. 몇 가지 권장 옵션은 다음과 같습니다.

| 스키마 | XDM 필드 |
---------|----------
| 이름 | `person.name.firstName` |
| 성 | `person.name.lastName` |
| 전화 | `mobilePhone.number` |
| 주소 구/군/시 | `homeAddress.city` |
| 주소 상태 | `homeAddress.stateProvince` |
| 주소 우편 번호 | `homeAddress.postalCode` |
| 생일 | `person.birthDayAndMonth` |

## 3단계 - 스토리지 위치의 데이터를 대상으로 가져오기

저장소 위치에서 대상으로 데이터를 가져오는 방법에 대한 자세한 내용은 개별 이메일 마케팅 대상 문서를 참조하십시오.

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Furnar](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## 이메일 마케팅 대상에 세그먼트 활성화

이메일 마케팅 대상으로 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).