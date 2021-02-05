---
keywords: Experience Platform;인사이트;고객 아이디;인기 있는 항목;고객 아이지 세그먼트
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 예측된 점수가 있는 고객 세그먼트 만들기
topic: Create a segment
description: 예측 실행이 완료되면 예측된 성향 점수가 프로파일에서 자동으로 사용됩니다. 고객 AI 점수로 프로파일을 강화하면 고객 세그먼트를 만들어 고객 성향 점수를 기반으로 고객을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# 예측된 점수가 있는 고객 세그먼트 만들기

예측 실행이 완료되면 예측된 성향 점수가 프로파일에서 자동으로 사용됩니다. 고객 AI 점수로 프로파일을 강화하면 고객 세그먼트를 만들어 고객 성향 점수를 기반으로 고객을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다. 세그먼트 만들기에 대한 보다 강력한 자습서는 [세그먼트 빌더 사용자 안내서](../../../segmentation/ui/segment-builder.md)를 참조하십시오.

>[!IMPORTANT]
>
>이 방법을 활용하려면 데이터 세트에 대해 실시간 고객 프로필을 활성화해야 합니다.

플랫폼 UI에서 왼쪽 탐색 영역에서 **[!UICONTROL 세그먼트]**&#x200B;를 클릭한 다음 **[!UICONTROL 세그먼트 만들기]**&#x200B;를 클릭합니다.

![](../images/user-guide/segments.png)

**세그먼트 빌더**&#x200B;가 나타납니다. 왼쪽 **[!UICONTROL 필드]** 열과 **[!UICONTROL 속성]** 탭에서 **[!UICONTROL XDM 개별 프로필]**&#x200B;이라는 폴더를 클릭한 다음 조직의 네임스페이스가 있는 폴더를 클릭합니다. **[!UICONTROL 고객 AI]**&#x200B;라는 폴더에는 예측 실행 결과가 포함되며 점수가 속한 인스턴스 이름을 기준으로 이름이 지정됩니다. 인스턴스 폴더를 클릭하여 원하는 인스턴스의 결과에 액세스합니다.

![](../images/user-guide/results.png)

세그먼트 빌더의 중심에 있는 **[!UICONTROL 점수]** 속성을 *규칙 빌더 캔버스*&#x200B;로 드래그하여 놓아 규칙을 정의합니다.

오른쪽 *세그먼트 속성* 열에서 세그먼트의 이름을 입력합니다.

![](../images/user-guide/properties.png)

왼쪽 *필드* 열 위에 **기어** 아이콘을 클릭하고 드롭다운에서 *병합 정책*&#x200B;을 선택합니다. **[!UICONTROL 저장]**&#x200B;을 클릭하여 세그먼트를 만듭니다.

![](../images/user-guide/merge_policy.png)

## 다음 단계

이 튜토리얼을 따라 세그먼트 빌더를 사용하여 성향 점수를 기반으로 대상을 찾았습니다. 이제 대상을 대상으로 활성화하여 대상을 타깃팅할 수 있습니다. 자세한 내용은 [대상 개요](../../../destinations/home.md)를 참조하십시오.