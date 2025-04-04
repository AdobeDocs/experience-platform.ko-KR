---
keywords: Experience Platform;통찰력;고객 ai;인기 주제;고객 ai 세그먼트
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 예측된 점수로 고객 세그먼트 생성
description: 예측 실행이 완료되면 예측된 성향 점수가 프로필에서 자동으로 사용됩니다. 고객 AI 점수로 프로필을 보강하면 고객 세그먼트를 만들어 성향 점수에 따라 대상자를 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 설명합니다.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# 예측된 점수로 고객 세그먼트 생성

예측 실행이 완료되면 예측된 성향 점수가 프로필에서 자동으로 사용됩니다. 고객 AI 점수로 프로필을 보강하면 고객 세그먼트를 만들어 성향 점수에 따라 대상자를 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 설명합니다. 세그먼트 만들기에 대한 강력한 튜토리얼을 보려면 [세그먼트 빌더 사용 안내서](../../../segmentation/ui/segment-builder.md)를 참조하세요.

>[!IMPORTANT]
>
>이 방법을 활용하려면 데이터 세트에 대해 실시간 고객 프로필 을 활성화해야 합니다.

Experience Platform UI에서 왼쪽 탐색에서 **[!UICONTROL 세그먼트]**&#x200B;를 클릭한 다음 **[!UICONTROL 세그먼트 만들기]**&#x200B;를 클릭합니다.

![](../images/user-guide/segments_new.png)

**세그먼트 빌더**&#x200B;가 나타납니다. 왼쪽 **[!UICONTROL 필드]** 열과 **[!UICONTROL 특성]** 탭에서 **[!UICONTROL XDM 개인 프로필]**&#x200B;이라는 폴더를 클릭한 다음 조직의 네임스페이스가 있는 폴더를 클릭합니다. **[!UICONTROL Customer AI]** 폴더에 예측 실행 결과가 포함되어 있으며 점수가 속한 인스턴스의 이름을 따서 명명됩니다. 원하는 인스턴스의 결과에 액세스하려면 인스턴스 폴더를 클릭합니다.

![](../images/user-guide/results_new.png)

세그먼트 빌더 중앙에 있으며 **[!UICONTROL Score]** 특성을 *규칙 빌더 캔버스*(으)로 끌어다 놓아 규칙을 정의합니다.

오른쪽 *세그먼트 속성* 열 아래에서 세그먼트 이름을 입력합니다.

![](../images/user-guide/properties_new.png)

왼쪽 *필드* 열 위에서 **톱니바퀴** 아이콘을 클릭하고 드롭다운에서 *병합 정책*&#x200B;을 선택합니다. 세그먼트를 만들려면 **[!UICONTROL 저장]**&#x200B;을 클릭합니다.

![](../images/user-guide/merge_policy_new.png)

## 다음 단계

이 자습서에 따라 세그먼트 빌더를 사용하여 성향 점수를 기반으로 대상자를 성공적으로 찾았습니다. 이제 대상을 대상으로 활성화하여 대상을 타기팅할 수 있습니다. 자세한 내용은 [대상 개요](../../../destinations/home.md)를 참조하십시오.
