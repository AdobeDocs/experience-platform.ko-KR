---
keywords: 전자 메일;전자 메일;전자 메일;전자 메일 대상
title: 이메일 마케팅 대상 개요
type: Tutorial
description: ESP(Email Service Providers)를 사용하면 이메일 캠페인을 전송하는 것과 같은 이메일 마케팅 활동을 관리할 수 있습니다.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: a21abb44bb9cbe6fefa0ff70a1ff19e31cc0c7de
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# 이메일 마케팅 대상 개요 {#email-marketing-destinations}

ESP(Email Service Providers)를 사용하면 이메일 캠페인을 전송하는 것과 같은 이메일 마케팅 활동을 관리할 수 있습니다. Adobe Experience Platform은 이메일 마케팅 대상으로 세그먼트를 활성화할 수 있으므로 ESP와 통합됩니다.

캠페인을 위한 이메일 마케팅 대상에 세그먼트를 보내려면, 플랫폼이 먼저 대상에 연결해야 합니다.

이메일 마케팅 대상에 연결하는 것은 3단계 프로세스입니다([대상](#connect-destination) 구성, [세그먼트 활성화](#select-segments), [스토리지 위치의 데이터를 대상](#import-data-into-destination)으로 가져오기). 각 단계는 이 페이지의 아래에 자세히 설명되어 있습니다.

아래 섹션에 설명된 연결 대상 플로우에서 [!DNL Amazon S3] 또는 [!DNL SFTP]에 연결합니다. Platform은 세그먼트를 `.csv` 파일로 내보내고 원하는 위치로 전달합니다. [!DNL Platform]에서 활성화된 저장소 위치에서 이메일 마케팅 플랫폼에서 데이터를 가져오도록 예약합니다. 데이터를 가져오는 프로세스는 각 파트너마다 다릅니다. 자세한 내용은 개별 대상 아티클을 참조하십시오.

## 대상 {#connect-destination} 구성

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;에서 연결할 이메일 마케팅 대상을 선택한 다음 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![대상에 연결](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

**[!UICONTROL 계정]** 단계에서 이전에 이메일 마케팅 대상에 대한 연결을 설정한 경우 **[!UICONTROL 기존 계정]**&#x200B;을 선택하고 기존 연결을 선택합니다. 또는 **[!UICONTROL 새 계정]**&#x200B;을 선택하여 이메일 마케팅 대상에 새 연결을 설정할 수 있습니다. **[!UICONTROL 연결 유형]** 선택기에서 [!UICONTROL Amazon S3], [!UICONTROL Azure Blob], [!UICONTROL SFTP(암호] 포함) 또는 [!UICONTROL SFTP(SSH 키]) 중에서 선택할 수 있습니다. 연결 유형에 따라 아래 정보를 입력한 다음 **[!UICONTROL Connect]**&#x200B;를 선택합니다.

- **S3 연결**&#x200B;의 경우 Amazon 액세스 키 ID 및 비밀 액세스 키를 제공해야 합니다.
- 암호&#x200B;**연결이 있는** SFTP의 경우 SFTP 서버에 대한 도메인, 포트, 사용자 이름 및 암호를 제공해야 합니다.
- **SFTP에서 SSH 키** 연결을 사용하려면 SFTP 서버에 대해 도메인, 포트, 사용자 이름 및 SSH 키를 제공해야 합니다.

원할 경우, **[!UICONTROL 키]** 섹션 아래의 내보낸 파일에 암호화를 추가하기 위해 RSA 형식 공개 키를 첨부할 수 있습니다. 공개 키는 [!DNL Base64] 인코딩 문자열로 작성해야 합니다.

**[!UICONTROL 인증]** 단계에서 새 대상에 대한 이름 및 설명과 내보낸 파일의 파일 형식을 입력합니다.

이전 단계에서 저장소 옵션으로 Amazon S3를 선택한 경우 파일이 배달될 클라우드 저장소 대상에 버킷 이름과 폴더 경로를 삽입합니다. [SFTP 저장소] 옵션의 경우 파일을 배달할 폴더 경로를 삽입합니다.

이 단계에서는 이 대상에 적용할 마케팅 작업을 선택할 수도 있습니다. 마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

![이메일 설정 단계](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## 대상 내보내기에 포함할 세그먼트 구성원 선택 {#select-segments}

**[!UICONTROL 세그먼트 선택]** 페이지에서 대상에 보낼 세그먼트를 선택합니다. 아래 섹션에서 필드에 대한 자세한 내용을 살펴보십시오.

![세그먼트 선택](../../assets/common/email-select-segments.png)

## 파일 이름 구성

세그먼트 일정 및 파일 이름 편집 옵션에 대한 자세한 내용은 대상 활성화 자습서의 [구성](../../ui/activate-destinations.md#configure) 단계를 참조하십시오.

## 특성 선택 - 내보낸 파일에서 대상 특성으로 사용할 스키마 필드를 선택합니다 {#destination-attributes}

이 단계에서는 이메일 마케팅 대상으로 내보낼 필드를 선택하고 필수 필드를 표시합니다.
이 단계에 대한 자세한 내용은 활성화 대상 자습서에서 [특성 선택](../../ui/activate-destinations.md#select-attributes) 단계를 참조하십시오.

## ID {#identity}

Adobe에서는 [union schema](../../../profile/home.md#profile-fragments-and-union-schemas)에서 고유한 식별자를 선택하는 것이 좋습니다. 사용자 ID가 꺼져 있는 필드입니다. 일반적으로 이 필드는 이메일 주소이지만 충성도 프로그램 ID 또는 전화 번호일 수도 있습니다. 스키마의 가장 일반적인 고유 식별자 및 해당 XDM 필드에 대해서는 아래 표를 참조하십시오.

| 고유 식별자 | 통합 스키마의 XDM 필드 |
----------------- | ---------------------------
| Email Address | `personalEmail.address` |
| 전화 | `mobilePhone.number` |
| 충성도 프로그램 ID | `Customer-defined XDM field` |

## 기타 대상 특성

스키마 필드 선택기에서 이메일 대상으로 내보낼 다른 필드를 선택합니다. 몇 가지 권장 옵션은 다음과 같습니다.

| 스키마 | XDM 필드 |
------ | ---------
| 이름 | `person.name.firstName` |
| 성 | `person.name.lastName` |
| 전화 | `mobilePhone.number` |
| 주소 구/군/시 | `homeAddress.city` |
| 주소 상태 | `homeAddress.stateProvince` |
| 주소 우편 번호 | `homeAddress.postalCode` |
| 생일 | `person.birthDayAndMonth` |
| 세그먼트 멤버십 | `segmentMembership.status` |

## 저장소 위치의 데이터를 대상 {#import-data-into-destination}으로 가져오기

개별 이메일 마케팅 대상 아티클에서 스토리지 위치의 데이터를 대상으로 가져오는 방법을 알아봅니다.

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle 언변](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Salesforce Marketing Cloud](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## 이메일 마케팅 대상에 세그먼트 활성화

이메일 마케팅 대상에 세그먼트를 활성화하는 방법에 대한 지침은 [대상 프로파일 및 세그먼트를 활성화하기를 참조하십시오](../../ui/activate-destinations.md).

## 추가 리소스

- [대상에 데이터 활성화](../../ui/activate-destinations.md)
- [이메일 마케팅 대상을 만들고 Flow Service API를 사용하여 데이터를 활성화합니다.](../../api/email-marketing.md)
