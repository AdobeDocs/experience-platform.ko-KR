---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: 연락처 세부 정보 혼합
topic: overview
description: 이 문서에서는 작업 연락처 세부 사항 혼합에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 3%

---


# [!UICONTROL 작업 연락처 세부 정보] 혼합

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트에](../name-updates.md) 대한 문서를 참조하십시오.

[!UICONTROL [작업 연락처 세부 사항] ]은 [[!DNL XDM Individual Profile] 클래스](../../classes/individual-profile.md)의 표준 믹스인입니다. 이 혼합물은 작업장 주소, 작업이메일, 직장 전화 번호, 그리고 그 사람이 속한 조직과 같은 개인의 직업적 정보를 캡처하는 여러 가지 분야를 제공합니다.

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