---
title: 위치 클래스
description: XDM(경험 데이터 모델)의 Location 클래스에 대해 알아봅니다.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 7%

---

# [!UICONTROL 위치] 클래스

XDM(Experience Data Model)에서 [!UICONTROL Location] 클래스는 여행관이나 스포츠 경기장과 같은 라이브 이벤트 위치 정보를 캡처합니다.

![위치 클래스 구조](../images/classes/location.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| [!UICONTROL 식별자] | `_id` | [!UICONTROL 문자열] | 레코드에 대한 시스템에서 생성한 고유한 문자열 식별자. 이 필드는 개별 레코드의 고유성을 추적하고, 데이터 중복을 방지하고, 다운스트림 서비스에서 해당 레코드를 조회하는 데 사용됩니다.<br><br>이 필드는 시스템에서 생성되므로 데이터를 수집하는 동안 명시적 값을 제공할 필요가 없습니다. 그러나 원하는 경우 고유한 ID 값을 제공하도록 선택할 수 있습니다. |
| [!UICONTROL 위치 식별자] | `locationID` | [!UICONTROL 문자열] | 위치에 대한 고유 식별자. |
| [!UICONTROL 위치 이름] | `locationName` | [!UICONTROL 문자열] | 위치의 이름입니다. |

위치에 대한 자세한 내용을 설명하기 위해 클래스를 [[!UICONTROL Location] 필드 그룹](../field-groups/location/healthcare-location.md)(으)로 확장할 수 있습니다.
