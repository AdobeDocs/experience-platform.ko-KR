---
title: 이메일 마케팅 대상
seo-title: 이메일 마케팅 대상
description: ESP(Email Service Providers)를 사용하면 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
seo-description: ESP(Email Service Providers)를 사용하면 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
translation-type: tm+mt
source-git-commit: 570c627672439a5ee0f4215b7bf7915ec3dd2bb3
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 1%

---


# 이메일 마케팅 대상 {#email-marketing-destinations}

ESP(Email Service Providers)를 사용하면 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있습니다. Adobe 실시간 고객 데이터 Platform은 이메일 마케팅 대상으로 세그먼트를 활성화할 수 있도록 함으로써 ESP와 통합됩니다.

캠페인을 위한 이메일 마케팅 대상으로 세그먼트를 전송하려면 Adobe 실시간 CDP가 먼저 대상에 연결되어야 합니다.

이메일 마케팅 대상에 연결하는 프로세스는 3단계로 이루어집니다. 각 단계는 이 페이지의 아래에 자세히 설명되어 있습니다.

아래 섹션에 설명된 연결 대상 플로우에서 Amazon S3 또는 SFTP에 연결합니다. 실시간 CDP는 세그먼트를 `.csv` 또는 `.txt` 파일로 내보내 원하는 위치에 전달합니다. 실시간 CDP에서 활성화된 스토리지 위치에서 이메일 마케팅 플랫폼에서 데이터를 가져올 수 있도록 예약합니다. 데이터를 가져오는 프로세스는 각 파트너마다 다릅니다. 자세한 내용은 개별 대상 아티클을 참조하십시오.

## 1단계 - 연결 대상 {#connect-destination}

1. [ **[!UICONTROL 연결]** ] > **[!UICONTROL 대상]**]에서 연결할 이메일 마케팅 대상을 선택한 다음 **[!UICONTROL Connect 대상을 선택합니다]**.

   ![대상에 연결](/help/rtcdp/destinations/assets/connect-email-marketing.png)

2. 이전에 이메일 마케팅 대상에 대한 연결을 **[!UICONTROL 설정한 경우 인증]** 단계에서 기존 계정 **[!UICONTROL 을]** 선택하고 기존 연결을 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 이메일 마케팅 대상에 새 연결을 설정할 수 있습니다. 연결 유형 **[!UICONTROL 선택기에서]** Amazon S3 **, 암호**&#x200B;가 있는 SFTP **, SSH 키가 있는 SFTP**&#x200B;중에서 선택할 수 ****&#x200B;있습니다. 연결 유형에 따라 아래 정보를 입력한 다음 **[!UICONTROL Connect를 선택합니다]**.

   **S3 연결의**&#x200B;경우 Amazon 액세스 키 ID와 비밀 액세스 키를 제공해야 합니다.

   암호 **가** 연결된 SFTP의 경우 SFTP 서버의 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.

   SSH 키 **** 연결이 있는 SFTP의 경우 SFTP 서버에 대한 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

3. [ **[!UICONTROL 설정]** ] **[!UICONTROL 단계에서 새 대상에 대한]** 이름 **[!UICONTROL 과]** 설명 **[!UICONTROL 과 내보낸 파일에 대한 파일 형식]** 을 입력합니다. <br>
이전 단계에서 저장소 옵션으로 Amazon S3를 선택한 경우, 파일이 배달될 클라우드 스토리지 대상에 **[!UICONTROL 버킷 이름]** 및 **[!UICONTROL 폴더 경로를]** 삽입합니다. SFTP 저장소 옵션의 경우 파일이 배달될 **[!UICONTROL 폴더 경로를]** 삽입합니다. <br>
또한 이 단계에서는 이 대상에 **[!UICONTROL 적용되어야 하는 모든]** 마케팅 사용 사례를 선택할 수 있습니다. 마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](/help/rtcdp/privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](/help/data-governance/policies/overview.md#core-actions). <br>
   ![이메일 설정 단계](/help/rtcdp/destinations/assets/email-setup-step.png)

## 2단계 - 대상 내보내기에 포함할 세그먼트 멤버를 선택합니다. {#select-segments}

세그먼트 **[!UICONTROL 선택]** 페이지에서 대상에 전송할 세그먼트를 선택합니다. 아래 섹션에서 필드에 대한 자세한 내용을 살펴보십시오.

![세그먼트 선택](/help/rtcdp/destinations/assets/email-select-segments.png)

## 3단계 - 내보낸 파일에서 대상 특성으로 사용할 스키마 필드를 선택합니다. {#destination-attributes}

이 단계에서는 이메일 마케팅 대상으로 내보낼 필드를 선택합니다.

![대상 속성](/help/rtcdp/destinations/assets/destination-attributes.png)

### ID {#identity}

조합 스키마에서 고유 식별자를 선택하는 것이 [좋습니다](../../profile/home.md#profile-fragments-and-union-schemas). 사용자 ID가 꺼져 있는 필드입니다. 일반적으로 이 필드는 이메일 주소이지만 충성도 프로그램 ID 또는 전화 번호일 수도 있습니다. 조합 스키마에서 가장 일반적인 고유 식별자 및 XDM 필드는 아래 표를 참조하십시오.

| 고유 식별자 | 통합 스키마의 XDM 필드 |
---------|----------
| Email Address | `personalEmail.address` |
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