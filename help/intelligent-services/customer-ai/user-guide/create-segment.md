---
keywords: Experience Platform;통찰력;고객 ai;인기 항목;고객 ai 세그먼트
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 예측된 점수를 사용하여 고객 세그먼트 만들기
description: 예측 실행이 완료되면 예측된 성향 점수가 프로필에서 자동으로 사용됩니다. 고객 AI 점수로 프로필을 보강하면 고객 세그먼트를 만들어 성향 점수에 따라 대상을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 예측된 점수로 고객 세그먼트 만들기

예측 실행이 완료되면 예측된 성향 점수가 프로필에서 자동으로 사용됩니다. 고객 AI 점수로 프로필을 보강하면 고객 세그먼트를 만들어 성향 점수에 따라 대상을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다. 세그먼트 만들기에 대한 강력한 자습서를 보려면 [세그먼트 빌더 사용 안내서](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>이 방법을 활용하려면 데이터 세트에 대해 실시간 고객 프로필을 활성화해야 합니다.

플랫폼 UI에서 **[!UICONTROL 세그먼트]** 왼쪽 탐색에서 를 클릭하고 **[!UICONTROL 세그먼트 만들기]**.

![](../images/user-guide/segments.png)

다음 **세그먼트 빌더** 이 나타납니다. 왼쪽에서 **[!UICONTROL 필드]** 열 및 아래 **[!UICONTROL 속성]** 탭에서 라는 폴더를 클릭합니다. **[!UICONTROL XDM 개별 프로필]** 그런 다음 조직의 네임스페이스가 있는 폴더를 클릭합니다. 이름이 지정된 폴더 **[!UICONTROL 고객 AI]** 예측 실행 결과를 포함하며, 점수가 속하는 인스턴스의 이름을 기준으로 합니다. 인스턴스 폴더를 클릭하여 원하는 인스턴스의 결과에 액세스합니다.

![](../images/user-guide/results.png)

세그먼트 빌더 중심에 있는 를 드래그하여 놓습니다 **[!UICONTROL 점수]** 속성 *규칙 빌더 캔버스* 규칙을 정의하려는 경우.

오른쪽 아래 *세그먼트 속성* 열에서 세그먼트 이름을 입력합니다.

![](../images/user-guide/properties.png)

왼쪽 위 *필드* 열에서 **기어** 아이콘을 클릭하고 *병합 정책* 드롭다운 클릭 **[!UICONTROL 저장]** 세그먼트를 만듭니다.

![](../images/user-guide/merge_policy.png)

## 다음 단계

이 자습서를 따르면 세그먼트 빌더를 사용하여 성향 점수를 기반으로 대상을 찾았습니다. 이제 대상을 대상으로 활성화하여 대상을 타깃팅할 수 있습니다. 자세한 내용은 [대상 개요](../../../destinations/home.md) 추가 정보.
