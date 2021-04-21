---
keywords: Experience Platform;홈;인기 항목;세그먼테이션;세그먼트 빌더;세그먼트 빌더;home;popular topmentation;segmentation builder;segmentation builder
solution: Experience Platform
title: 리팩토링된 세그멘테이션 시간 제한 UI 안내서
topic-legacy: ui guide
description: 세그먼트 빌더는 프로필 데이터 요소와 상호 작용할 수 있는 풍부한 작업 공간을 제공합니다. 작업 영역은 데이터 속성을 나타내는 데 사용되는 드래그 앤 드롭 타일과 같이 규칙을 작성하고 편집하기 위한 직관적인 컨트롤을 제공합니다.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 시간 제한 리팩터화

Adobe Experience Platform용 2020년 10월 릴리스에서는 OR 및 AND 논리 연산자 사용에 새로운 제한을 추가하는 Adobe Experience Platform 세그멘테이션 서비스에 성능 변경 사항이 적용되었습니다. 이러한 변경 사항은 세그먼트 빌더 UI를 사용하여 새로 만들거나 편집한 세그먼트에 영향을 줍니다. 이 안내서에서는 이러한 변경 사항을 완화하는 방법을 설명합니다.

2020년 10월 릴리스 이전에는 동일한 타임스탬프를 참조하는 모든 규칙 수준, 그룹 수준 및 이벤트 수준 시간 제한이 중복 할당되었습니다. 시간 제한 사용을 명확히 하기 위해 규칙 수준 및 그룹 수준 시간 제한이 제거되었습니다. 이 변경 사항을 수용하려면 모든 시간 제한을 이벤트 수준 시간 제약 조건으로 다시 작성해야 합니다.

이전에는 개별 이벤트에 여러 시간 제한 규칙을 연결할 수 있었습니다.

![](../images/ui/segment-refactoring/former-time-constraint.png)

보시다시피 이 세그먼트에는 규칙 수준에서 2개의 제한 사항이 있습니다.하나는 &quot;[!UICONTROL Today]&quot;이고 다른 하나는 &quot;[!UICONTROL Yesterday]&quot;입니다.

이전 세그먼트는 다음 세그먼트와 같습니다. 두 이벤트 수준 시간 제약 조건이 모두 AND 연산자를 사용하여 연결되었습니다. 첫 번째 이벤트 수준 시간 제약 조건은 이름이 &quot;교육&quot;이고 오늘 일어나고 있는 클릭 이벤트를 참조하지만, 두 번째 이벤트 수준 시간 제약 조건은 이름이 &quot;애완 동물&quot;이고 어제 발생한 클릭 이벤트를 참조합니다.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

시간 제약 조건의 이 리팩토링은 OR 연산자를 사용하여 연결된 시간 제한 사항에도 영향을 줍니다.
