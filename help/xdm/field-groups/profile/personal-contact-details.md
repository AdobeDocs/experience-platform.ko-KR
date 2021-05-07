---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;개인 정보;스키마 디자인;필드 그룹;필드 그룹;Field group;home;popular topics;schema;fields;schemas;personal details;Schema design;field group;
solution: Experience Platform
title: 개인 연락처 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 개인 연락처 세부 정보 스키마 필드 그룹의 개요를 제공합니다.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 6%

---


# [!UICONTROL Personal Contact Details] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)의 문서를 참조하십시오.

[!UICONTROL Personal Contact Details] 개인 사용자에 대한 연락처 정보를  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 설명하는 클래스의 표준 스키마 필드 그룹입니다.

![](../../images/field-groups/personal-contact-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `faxPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 팩스 번호를 설명합니다. |
| `homeAddress` | [우편 주소](../../data-types/postal-address.md) | 개인의 주거 주소를 설명합니다. |
| `homePhone` | [전화번호](../../data-types/phone-number.md) | 개인의 집 전화 번호를 설명합니다. |
| `mobilePhone` | [전화번호](../../data-types/phone-number.md) | 사람의 휴대폰 번호를 설명합니다. |
| `personalEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 이메일 주소를 설명합니다. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
