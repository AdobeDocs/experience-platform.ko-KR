---
solution: Experience Platform
title: 연도 시간 제한 업데이트 무시
description: 연도 시간 제한 무시 문제를 해결하는 방법에 대해 알아봅니다.
hidefromtoc: true
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 8%

---

# 연도 제한 무시 업데이트 {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="연도 업데이트 무시"
>abstract="연도 제한 무시 기능이 업데이트되었습니다. 대상자를 다시 저장해 주십시오."

>[!IMPORTANT]
>
>**일괄 처리 세분화**&#x200B;을 사용하여 평가된 세그먼트 정의에서만 &quot;연도 무시&quot; 시간 제약 조건을 사용할 수 있습니다. 세그먼트 정의에 &quot;연도 무시&quot; 시간 제한을 추가하면 스트리밍 또는 에지 세분화에 대해 결과 대상자가 **부적격**&#x200B;됩니다.

2024년 2월 Adobe Experience Platform 릴리스에는 대상 만들기 및 평가에서 &quot;연도 무시&quot; 옵션 문제를 해결하는 Adobe Experience Platform 세그멘테이션 서비스 변경 사항이 도입되었습니다.

&quot;연도 무시&quot; 옵션은 대상 평가를 수행할 때 날짜의 연도 구성 요소를 무시하도록 설계되었습니다. 생년월일 필드처럼 서로 다른 이벤트 간의 시간적 관계는 중요하지만 특정 연도가 중요하지 않은 상황에서 이 옵션을 사용할 수 있습니다.

그러나 2024년과 같은 윤년 동안 기본 시스템이 이 옵션을 제대로 처리하지 못해 대상 평가가 부정확해졌습니다. 그 결과 윤년에 &#39;연도 무시&#39;가 활성화되면 관객 평가는 어느 날 놓치게 된다.

이 수정 사항이 릴리스되기 전에 대상을 만든 경우 수정 사항을 적용하려면 세그먼트 빌더에 대상을 다시 저장하면 됩니다. 대상자가 이 해결의 영향을 받는지 확실하지 않은 경우 세그먼트 빌더는 기존 대상자가 이 문제의 영향을 받는지 사용자에게 묻습니다.
