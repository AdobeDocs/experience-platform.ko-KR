---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;개인 세부 사항;스키마 디자인;혼합;Mixin
solution: Experience Platform
title: 개인 연락처 세부 정보 혼합
topic-legacy: overview
description: 이 문서에서는 개인 연락처 세부 사항 믹싱에 대한 개요를 제공합니다.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---

# [!UICONTROL Personal Contact Details] 믹싱

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL Personal Contact Details] 는 개인 연락처 정보를 설명하는  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) 클래스의 표준 혼합입니다.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `faxPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 팩스 번호를 설명합니다. |
| `homeAddress` | [우편 주소](../../data-types/postal-address.md) | 개인의 주거 주소를 설명합니다. |
| `homePhone` | [전화번호](../../data-types/phone-number.md) | 개인의 집 전화 번호를 설명합니다. |
| `mobilePhone` | [전화번호](../../data-types/phone-number.md) | 사람의 휴대폰 번호를 설명합니다. |
| `personalEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 이메일 주소를 설명합니다. |

혼합에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
