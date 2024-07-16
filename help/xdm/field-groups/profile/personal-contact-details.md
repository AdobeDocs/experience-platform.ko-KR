---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;개인 세부 정보;스키마 디자인;필드 그룹;필드 그룹;
solution: Experience Platform
title: 개인 연락처 세부 정보 스키마 필드 그룹
description: 개인 연락처 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 2%

---


# [!UICONTROL 개인 연락처 정보] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)에 대한 문서를 참조하십시오.

[!UICONTROL 개인 연락처 정보]은(는) 개별 사용자의 연락처 정보를 설명하는 [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)의 표준 스키마 필드 그룹입니다.

![](../../images/field-groups/personal-contact-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `faxPhone` | [전화 번호](../../data-types/phone-number.md) | 사용자의 팩스 번호를 설명합니다. |
| `homeAddress` | [우편 주소](../../data-types/postal-address.md) | 사용자의 거주 주소를 설명합니다. |
| `homePhone` | [전화 번호](../../data-types/phone-number.md) | 사용자의 집 전화 번호를 설명합니다. |
| `mobilePhone` | [전화 번호](../../data-types/phone-number.md) | 사용자의 휴대폰 번호를 설명합니다. |
| `personalEmail` | [전자 메일 주소](../../data-types/email-address.md) | 개인의 이메일 주소를 설명합니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
