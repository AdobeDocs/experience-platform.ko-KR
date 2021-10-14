---
keywords: Experience Platform;통찰력;고객 ai;인기 항목;고객 ai 세그먼트
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 예측된 점수를 사용하여 고객 세그먼트 만들기
topic-legacy: Create a segment
description: 예측 실행이 완료되면 예측된 성향 점수가 프로필에서 자동으로 사용됩니다. 고객 AI 점수로 프로필을 보강하면 고객 세그먼트를 만들어 성향 점수에 따라 대상을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 예측된 점수로 고객 세그먼트 만들기

예측 실행이 완료되면 예측된 성향 점수가 프로필에서 자동으로 사용됩니다. 고객 AI 점수로 프로필을 보강하면 고객 세그먼트를 만들어 성향 점수에 따라 대상을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다. 세그먼트 만들기에 대한 더 강력한 자습서는 [세그먼트 빌더 사용 안내서](../../../segmentation/ui/segment-builder.md)를 참조하십시오.

>[!IMPORTANT]
>
>이 방법을 활용하려면 데이터 세트에 대해 실시간 고객 프로필을 활성화해야 합니다.

Platform UI에서 왼쪽 탐색에서 **[!UICONTROL 세그먼트]**&#x200B;를 클릭한 다음 **[!UICONTROL 세그먼트 만들기]**&#x200B;를 클릭합니다.

![](../images/user-guide/segments.png)

**세그먼트 빌더**&#x200B;가 나타납니다. 왼쪽 **[!UICONTROL 필드]** 열과 **[!UICONTROL 속성]** 탭에서 **[!UICONTROL XDM 개별 프로필]** 폴더를 클릭한 다음 조직의 네임스페이스가 있는 폴더를 클릭합니다. **[!UICONTROL Customer AI]** 폴더는 예측 실행 결과를 포함하며, 점수가 속한 인스턴스의 이름을 따서 이름이 지정됩니다. 인스턴스 폴더를 클릭하여 원하는 인스턴스의 결과에 액세스합니다.

![](../images/user-guide/results.png)

세그먼트 빌더 중심에 있는 **[!UICONTROL Score]** 속성을 *규칙 빌더 캔버스*&#x200B;에 끌어다 놓아 규칙을 정의합니다.

오른쪽 *세그먼트 속성* 열 아래에 세그먼트 이름을 입력합니다.

![](../images/user-guide/properties.png)

왼쪽 *필드* 열 위에 있는 **톱니바퀴** 아이콘을 클릭하고 드롭다운에서 *병합 정책*&#x200B;을 선택합니다. **[!UICONTROL 저장]** 을 클릭하여 세그먼트를 만듭니다.

![](../images/user-guide/merge_policy.png)

## 다음 단계

이 자습서를 따르면 세그먼트 빌더를 사용하여 성향 점수를 기반으로 대상을 찾았습니다. 이제 대상을 대상으로 활성화하여 대상을 타깃팅할 수 있습니다. 자세한 내용은 [대상 개요](../../../destinations/home.md)를 참조하십시오.
