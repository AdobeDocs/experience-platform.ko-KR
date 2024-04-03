---
title: 상태 목록 컬렉션 종료 데이터 유형
description: 상태 목록 끝 컬렉션 데이터 유형 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 5%

---

# [!UICONTROL 상태 끝 목록] 데이터 유형

상태 목록 끝 컬렉션 데이터 유형 데이터 유형은 다양한 플레이어 속성의 끝 상태와 관련된 정보를 나타내기 위해 디자인된 XDM(경험 데이터 모델) 데이터 유형입니다. 여기에는 다음이 포함됩니다. [!UICONTROL 플레이어 상태 이름] 특정 속성 상태를 나타내는 속성(예: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;). 이 데이터 유형을 사용하여 다양한 플레이어 상태의 초기 조건을 캡처하고 설명합니다.

![상태 목록 끝 컬렉션 데이터 형식 다이어그램입니다.](../images/data-types/list-of-states-end-collection.png)

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|--------------------------------|--------------|-----------|-----------|-------------------------------------------------|
| [!UICONTROL 플레이어 상태 이름] | `name` | 문자열 | 아니요 | 플레이어 상태의 이름입니다. 열거됨: 각각의 의미가 있는 &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; |

{style="table-layout:auto"}
