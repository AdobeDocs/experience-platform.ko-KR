---
title: 응용 프로그램 세부 정보 스키마 필드 그룹
description: 애플리케이션 세부 정보 스키마 필드 그룹에 대해 알아봅니다.
exl-id: 5df99f9a-b36a-4c2b-a4a4-d3cf054f09b8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 4%

---

# [!UICONTROL 애플리케이션 세부 정보] 스키마 필드 그룹

[!UICONTROL 애플리케이션 세부 정보] 는 의 표준 스키마 필드 그룹입니다. [[!DNL XDM ExperienceEvent] 클래스](../../classes/experienceevent.md). 필드 그룹은 단일 `application` 충돌, 기능 사용, 실행 및 업그레이드 등 애플리케이션 관련 세부 정보를 캡처하는 스키마 객체.

![](../../images/field-groups/application-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `application` | [[!UICONTROL 애플리케이션]](../../data-types/financial-account.md) | 애플리케이션 이름, 앱 버전, 설치, 실행, 충돌 및 종료 등 이벤트와 관련된 애플리케이션 정보를 캡처합니다. 이벤트의 타겟팅된 애플리케이션(예: 전송되는 푸시 알림의 대상) 또는 이벤트를 시작하는 애플리케이션(예: 클릭 또는 로그인)일 수 있습니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-application.schema.json).
