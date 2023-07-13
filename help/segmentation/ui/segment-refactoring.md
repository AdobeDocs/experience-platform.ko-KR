---
solution: Experience Platform
title: 리팩터링된 세그멘테이션 시간 제한 UI 안내서
description: 세그먼트 빌더는 프로필 데이터 요소와 상호 작용할 수 있는 풍부한 작업 공간을 제공합니다. 작업 공간에서는 데이터 속성을 표시하는 데 사용되는 드래그 앤 드롭 타일과 같은 규칙을 작성하고 편집할 수 있는 직관적인 컨트롤을 제공합니다.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 시간 제한 리팩터링

Adobe Experience Platform용 2020년 10월 릴리스에는 OR 및 AND 논리 연산자의 사용에 새로운 제한을 추가하는 Adobe Experience Platform 세분화 서비스의 성능 변경 사항이 도입되었습니다. 이러한 변경 사항은 세그먼트 빌더 UI를 사용하여 새로 만들어지거나 편집된 세그먼트에 영향을 줍니다. 이 안내서에서는 이러한 변경 사항을 완화하는 방법을 설명합니다.

2020년 10월 릴리스 이전에는 모든 규칙 수준, 그룹 수준 및 이벤트 수준 시간 제한이 동일한 타임스탬프를 중복 참조했습니다. 시간 제약 사용을 명확히 하기 위해 규칙 수준 및 그룹 수준 시간 제약을 제거하였다. 이러한 변경 사항을 수용하기 위해 모든 시간 제한을 이벤트 수준 시간 제한으로 다시 작성해야 합니다.

이전에는 개별 이벤트에 여러 시간 제한 규칙이 첨부되어 있을 수 있었습니다.

![세그먼트 빌더에서 시간 구속의 이전 스타일이 강조 표시됩니다.](../images/ui/segment-refactoring/former-time-constraint.png)

알 수 있듯이 이 세그먼트에는 규칙 수준에 대한 두 가지 제한( )이 있습니다.[!UICONTROL 오늘]&quot;및&quot;에 대한 기타[!UICONTROL 어제]&quot;.

이전 세그먼트는 다음 세그먼트와 같습니다. 이벤트 수준 시간 제약 조건은 모두 AND 연산자를 사용하여 연결되었습니다. 첫 번째 이벤트 수준 시간 제약 조건은 이름이 &quot;Training&quot;이고 오늘 발생하는 클릭 이벤트를 참조하는 반면 두 번째 이벤트 수준 시간 제약 조건은 이름이 &quot;Pets&quot;이고 어제 발생한 클릭 이벤트를 참조합니다.

![시간 제한의 새로운 스타일은 세그먼트 빌더에서 강조 표시됩니다.](../images/ui/segment-refactoring/time-constraint-1.png) ![시간 제한의 새로운 스타일은 세그먼트 빌더에서 강조 표시됩니다.](../images/ui/segment-refactoring/time-constraint-2.png)

이러한 시간 제약의 리팩터링은 OR 연산자를 사용하여 연결되는 시간 제약에도 영향을 미친다.
