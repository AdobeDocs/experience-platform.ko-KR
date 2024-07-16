---
title: 상태 목록 컬렉션 시작 데이터 유형
description: 상태 목록 시작 데이터 유형 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: adeb3e91-7266-41ce-b406-f7fd5dbb2236
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---

# [!UICONTROL 상태 시작 목록] 데이터 형식

[!UICONTROL 상태 목록 시작] 데이터 형식은 다양한 플레이어 특성의 시작 상태와 관련된 정보를 나타내기 위해 디자인된 XDM(Experience Data Model) 데이터 형식입니다. 여기에는 특정 특성 상태(예: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;)를 나타내는 [!UICONTROL 플레이어 상태 이름] 속성이 포함됩니다. 이 데이터 유형을 사용하여 다양한 플레이어 상태의 초기 조건을 캡처하고 설명합니다.

![상태 목록 [!UICONTROL 시작] 데이터 형식의 다이어그램입니다.](../images/data-types/list-of-states-start-collection.png)

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 플레이어 상태 이름] | `name` | 문자열 | 아니요 | 플레이어 상태의 이름입니다. 열거됨: 각각의 의미가 있는 &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; |

{style="table-layout:auto"}
