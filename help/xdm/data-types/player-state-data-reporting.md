---
title: 플레이어 상태 데이터 보고 데이터 유형
description: 플레이어 상태 데이터 보고 XDM(Experience Data Model) 데이터 유형에 대해 알아봅니다.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 4%

---

# [!UICONTROL 플레이어 상태 데이터 보고] 데이터 유형

[!UICONTROL 플레이어 상태 데이터 보고] 는 미디어 플레이어 내의 다양한 상태와 발생을 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 사용 [!UICONTROL 플레이어 상태 데이터 보고] 데이터 형식을 사용하여 전체 화면, 음소거, 자막, PIP(Picture-in-Picture) 및 인포커스 상태 등 다양한 플레이어 상태를 캡처할 수 있습니다. 각 상태에 대해 상태가 설정되었는지 여부, 발생 횟수 및 미디어 재생 중 활성 상태로 유지되는 총 시간을 기록합니다.

![플레이어 상태 데이터 보고 데이터 유형 다이어그램입니다.](../images/data-types/player-state-data-information.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL 플레이어 상태 이름] | `name` | 문자열 | 플레이어 상태의 이름입니다. 열거됨: 각각의 의미가 있는 &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; |
| [!UICONTROL 플레이어 상태 집합] | `isSet` | 부울 | 해당 상태에서 플레이어 상태를 설정할지 여부입니다. |
| [!UICONTROL 플레이어 상태 카운트] | `count` | 정수 | 스트림에 플레이어 상태가 설정된 횟수입니다. |
| [!UICONTROL 플레이어 상태 시간] | `time` | 정수 | 해당 플레이어 상태의 총 기간입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
