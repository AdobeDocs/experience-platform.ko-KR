---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;개별 프로필;필드;스키마;스키마;스키마 디자인;혼합;작업 세부 사항;프로필 작업
solution: Experience Platform
title: 작업 연락처 세부 정보 혼합
topic-legacy: overview
description: 이 문서에서는 작업 연락처 세부 사항 믹싱에 대한 개요를 제공합니다.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 3%

---

# [!UICONTROL Work Contact Details] 믹싱

>[!NOTE]
>
>여러 혼합물의 이름이 변경되었습니다. 자세한 내용은 [혼합 이름 업데이트](../name-updates.md)에 있는 문서를 참조하십시오.

[!UICONTROL Work Contact Details] 는 클래스의 표준  [[!DNL XDM Individual Profile] 혼합입니다](../../classes/individual-profile.md). 이 혼합은 직장 주소, 직장 이메일, 직장 전화 번호, 그 사람이 속한 조직 등 개인의 직업상 정보를 캡처하는 여러 가지 분야를 제공합니다.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `workAddress` | [우편 주소](../../data-types/postal-address.md) | 사람의 작업 주소를 설명합니다. |
| `workEmail` | [이메일 주소](../../data-types/email-address.md) | 사람의 회사 이메일 주소를 설명합니다. |
| `workPhone` | [전화번호](../../data-types/phone-number.md) | 사람의 직장 전화 번호를 설명합니다. |
| `organizations` | 문자열(배열) | 개인이 구성원으로 있는 조직을 나타내는 자유 형식 문자열 배열입니다. |

혼합에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
