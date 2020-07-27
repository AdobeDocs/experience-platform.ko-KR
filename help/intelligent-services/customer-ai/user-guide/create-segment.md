---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: 예측된 점수가 있는 고객 세그먼트 만들기
topic: Create a segment
translation-type: tm+mt
source-git-commit: fba6ae701a38737812dccbf4f63e5a07f935ad8b
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# 예측된 점수가 있는 고객 세그먼트 만들기

예측 실행이 완료되면 예측된 성향 점수가 프로파일에서 자동으로 사용됩니다. 고객 AI 점수로 프로파일을 강화하면 고객 세그먼트를 만들어 고객 성향 점수를 기준으로 고객을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다. 세그먼트 만들기에 대한 더 강력한 자습서는 세그먼트 빌더 [사용 안내서를 참조하십시오](../../../segmentation/ui/overview.md).

>[!IMPORTANT]
>
>이 방법을 활용하려면 데이터 세트에 대해 실시간 고객 프로필을 활성화해야 합니다.

Platform UI에서 왼쪽 탐색 **[!UICONTROL 에서]** 세그먼트를 클릭한 다음 세그먼트 **[!UICONTROL 만들기를 클릭합니다]**.

![](../images/user-guide/segments.png)

세그먼트 *빌더가* 나타납니다. 왼쪽 *필드* 열과 *속성* 탭 아래에서 **[!UICONTROL XDM 개별]** 프로필이라는 폴더를클릭한 다음 조직의 네임스페이스가 있는 폴더를 클릭합니다. Customer **[!UICONTROL AI라는]** 폴더에는 예측 실행 결과가 포함되며 점수가 속한 인스턴스 이름을 기준으로 이름이 지정됩니다. 인스턴스 폴더를 클릭하여 원하는 인스턴스의 결과에 액세스합니다.

![](../images/user-guide/results.png)

세그먼트 빌더 가운데에 있는 **[!UICONTROL 점수]** 속성을 *규칙 빌더 캔버스로* 드래그하여 놓아 규칙을 정의합니다.

오른쪽 세그먼트 *속성* 열에서 세그먼트의 이름을 입력합니다.

![](../images/user-guide/properties.png)

왼쪽 필드 *열* 위에 있는 **톱니바퀴** 아이콘을 클릭하고 드롭다운에서 *병합 정책을* 선택합니다. Click **[!UICONTROL Save]** to create the segment.

![](../images/user-guide/merge_policy.png)

## 다음 단계

이 튜토리얼을 따라 세그먼트 빌더를 사용하여 성향 점수를 기준으로 대상을 찾았습니다. 대상을 활성화하여 대상을 타깃팅할 수 있습니다. 자세한 내용은 [대상 개요를](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) 참조하십시오.