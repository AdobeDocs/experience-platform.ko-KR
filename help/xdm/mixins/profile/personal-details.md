---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: 프로필 개인 정보 혼합
topic: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 8%

---


# [!UICONTROL 프로필 개인 세부 정보] 혼합

[!UICONTROL 프로필 개인 세부 사항은] 학급 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md)의 표준 혼합입니다. 이 혼합은 루트 수준 개체를 제공하며, 이 하위 필드는 개별 사용자에 대한 연락처 정보를 설명합니다. `person`

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `faxPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 팩스 번호를 설명합니다. |
| `homeAddress` | [우편 주소](../../data-types/postal-address.md) | 개인의 거주지 주소를 설명합니다. |
| `homePhone` | [전화번호](../../data-types/phone-number.md) | 개인의 집 전화 번호를 설명합니다. |
| `mobilePhone` | [전화번호](../../data-types/phone-number.md) | 개인의 휴대폰 번호를 설명합니다. |
| `personalEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 이메일 주소를 설명합니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
