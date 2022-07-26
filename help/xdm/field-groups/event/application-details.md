---
title: 응용 프로그램 세부 정보 스키마 필드 그룹
description: 이 문서에서는 응용 프로그램 세부 정보 스키마 필드 그룹에 대한 개요를 제공합니다.
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 4%

---

# [!UICONTROL 애플리케이션 세부 정보] 스키마 필드 그룹

[!UICONTROL 애플리케이션 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `application` 충돌, 기능 사용, 시작 및 업그레이드와 같은 애플리케이션 관련 세부 사항을 캡처하는 스키마에 대한 개체입니다.

![](../../images/field-groups/application-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `application` | [[!UICONTROL 애플리케이션]](../../data-types/financial-account.md) | 애플리케이션 이름, 앱 버전, 설치, 시작, 충돌 및 종료를 비롯하여 이벤트와 관련된 애플리케이션 정보를 캡처합니다. 이벤트(예: 전송 중인 푸시 알림의 대상 등)나 이벤트를 시작한 애플리케이션(예: 클릭 또는 로그인)일 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

필드 그룹에 대한 자세한 내용은 [공용 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
