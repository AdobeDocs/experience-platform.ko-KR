---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;스키마 디자인;혼합;작업 세부 사항;프로필 작업
solution: Experience Platform
title: 작업 연락처 세부 정보 스키마 필드 그룹
topic-legacy: overview
description: 이 문서에서는 작업 연락처 세부 정보 스키마 필드 그룹의 개요를 제공합니다.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 3%

---


# [!UICONTROL Work Contact Details] 스키마 필드 그룹

>[!NOTE]
>
>여러 스키마 필드 그룹의 이름이 변경되었습니다. 자세한 내용은 [필드 그룹 이름 업데이트](../name-updates.md)의 문서를 참조하십시오.

[!UICONTROL Work Contact Details] 는 클래스의 표준 스키마 필드  [[!DNL XDM Individual Profile] 그룹입니다](../../classes/individual-profile.md). 필드 그룹은 직장 주소, 직장 이메일, 직장 전화 번호, 사람이 속한 조직 등 개인 개인에 대한 직업 정보를 수집하는 여러 가지 필드를 제공합니다.

![](../../images/field-groups/work-contact-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `workAddress` | [우편 주소](../../data-types/postal-address.md) | 사람의 작업 주소를 설명합니다. |
| `workEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 회사 이메일 주소를 설명합니다. |
| `workPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 직장 전화 번호를 설명합니다. |
| `organizations` | 문자열(배열) | 개인이 구성원으로 있는 조직을 나타내는 자유 형식 문자열 배열입니다. |

필드 그룹에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
