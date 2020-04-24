---
source-git-commit: 1cf1e9c814601bdd4c7198463593be78452004dc
translation-type: tm+mt

---
# 예측된 점수가 있는 고객 세그먼트 만들기

예측 실행이 완료되면 예측된 성향 점수는 프로필에 의해 자동으로 사용됩니다. 고객 AI 점수와 프로파일 강화를 통해 고객 세그먼트를 만들어 고객 성향 점수를 기반으로 고객을 찾을 수 있습니다. 이 섹션에서는 세그먼트 빌더를 사용하여 세그먼트를 만드는 단계를 제공합니다. 세그먼트 만들기에 대한 보다 강력한 자습서는 세그먼트 빌더 [사용 안내서를](../../../segmentation/tutorials/create-a-segment.md)참조하십시오.

>[!IMPORTANT] 이 방법을 활용하려면 데이터 세트에 대해 실시간 고객 프로필을 활성화해야 합니다.

플랫폼 UI에서 왼쪽 탐색 **[!UICONTROL Segments]** 을 클릭한 다음 을 클릭합니다 **[!UICONTROL Create segment]**.

![](../images/user-guide/segments.png)

세그먼트 *빌더가* 나타납니다. 왼쪽 *필드* 열과 속성 *탭에서* 명명된 폴더를 **[!UICONTROL XDM Individual Profile]** 클릭한다음 조직의 네임스페이스가 있는 폴더를 클릭합니다. 명명된 폴더에는 예측 실행 결과가 **[!UICONTROL Customer AI]** 들어 있으며 점수가 속한 인스턴스 이름을 기준으로 이름이 지정됩니다. 인스턴스 폴더를 클릭하여 원하는 인스턴스의 결과에 액세스합니다.

![](../images/user-guide/results.png)

세그먼트 빌더 가운데에 있는 **[!UICONTROL Score]** 속성을 *규칙 빌더 캔버스로* 드래그하여 놓아 규칙을 정의합니다.

오른쪽 세그먼트 *속성* 열에서 세그먼트의 이름을 제공합니다.

![](../images/user-guide/properties.png)

왼쪽 필드 *열* 위에서 **기어** 아이콘을 클릭하고 드롭다운에서 *병합 정책을* 선택합니다. 을 **[!UICONTROL Save]** 클릭하여 세그먼트를 만듭니다.

![](../images/user-guide/merge_policy.png)

## 다음 단계

이 튜토리얼을 따라 세그먼트 빌더를 사용하여 성향 점수를 기반으로 대상을 찾은 것입니다. 이제 대상을 대상으로 활성화하여 대상을 타깃팅할 수 있습니다. 자세한 내용은 [대상 개요를](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) 참조하십시오.