---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: 프로필 작업 세부 정보 혼합
topic: overview
description: 이 문서에서는 XDM 개별 프로필 클래스에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 4%

---


# [!UICONTROL 프로필 작업 세부 정보] 혼합

[!UICONTROL 프로필 작업 세부 사항은] 클래스 [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md)의 표준 믹스인입니다. 이 혼합물은 작업장 주소, 작업이메일, 직장 전화 번호, 그리고 그 사람이 속한 조직과 같은 개인의 직업적 정보를 캡처하는 여러 가지 분야를 제공합니다.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `workAddress` | [우편 주소](../../data-types/postal-address.md) | 사람의 회사 주소를 설명합니다. |
| `workEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 회사 이메일 주소를 설명합니다. |
| `workPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 직장 전화 번호를 설명합니다. |
| `organizations` | 문자열(배열) | 개인이 속한 조직을 나타내는 자유 형식 문자열 배열. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)