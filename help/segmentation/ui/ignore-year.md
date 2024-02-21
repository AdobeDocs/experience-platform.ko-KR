---
solution: Experience Platform
title: 연도 시간 제한 업데이트 무시
description: 연도 시간 제한 무시 문제를 해결하는 방법에 대해 알아봅니다.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 연도 시간 제한 업데이트 무시 {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="연도 업데이트 무시"
>abstract="연도 시간 제한 무시가 업데이트되었습니다. 대상을 다시 저장하십시오."

2024년 2월 Adobe Experience Platform 릴리스에는 대상 만들기 및 평가에서 &quot;연도 무시&quot; 옵션 문제를 해결하는 Adobe Experience Platform 세그멘테이션 서비스 변경 사항이 도입되었습니다.

&quot;연도 무시&quot; 옵션은 대상 평가를 수행할 때 날짜의 연도 구성 요소를 무시하도록 설계되었습니다. 생년월일 필드처럼 서로 다른 이벤트 간의 시간적 관계는 중요하지만 특정 연도가 중요하지 않은 상황에서 이 옵션을 사용할 수 있습니다.

그러나 2024년과 같은 윤년 동안 기본 시스템이 이 옵션을 제대로 처리하지 못해 대상 평가가 부정확해졌습니다. 그 결과 윤년에 &#39;연도 무시&#39;가 활성화되면 관객 평가는 어느 날 놓치게 된다.

이 수정 사항이 릴리스되기 전에 대상을 만든 경우 수정 사항을 적용하려면 세그먼트 빌더에 대상을 다시 저장하면 됩니다. 대상자가 이 해결의 영향을 받는지 확실하지 않은 경우 세그먼트 빌더는 기존 대상자가 이 문제의 영향을 받는지 사용자에게 묻습니다.
