---
keywords: Experience Platform;홈;자주 찾는 항목;세그먼테이션 서비스;세그먼테이션 서비스;세그먼테이션 서비스;사용 안내서;ui 안내서;대상 ui 안내서;대상 ui 안내서;대상 빌더;대상;대상;대상 ui 안내서;
solution: Experience Platform
title: 대상 UI 안내서
description: Adobe Experience Platform UI의 대상 빌더는 프로필 데이터 요소와 상호 작용할 수 있는 풍부한 작업 영역을 제공합니다. 작업 영역에서는 조직의 대상을 작성하고 편집할 수 있는 직관적인 컨트롤을 제공합니다.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Audience Builder UI 안내서

>[!IMPORTANT]
>
>Audience Builder는 현재 베타 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Audience Builder는 다양한 작업을 나타내는 데 사용되는 블록을 사용하여 대상을 만들고 편집할 수 있는 작업 영역을 제공합니다.

![대상 빌더 UI.](../images/ui/audience-builder/audience-builder.png)

대상 구성 캔버스는 다섯 가지 유형의 블록으로 구성됩니다. **[[!UICONTROL 대상자]](#audience-block)**, **[[!UICONTROL 제외]](#exclude-block)**, **[[!UICONTROL 가입]](#join-block)**, **[[!UICONTROL 등급]](#rank-block)**, 및 **[[!UICONTROL 분할]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

다음 **[!UICONTROL 대상자]** 블록 유형을 사용하면 더 큰 새 대상을 구성할 하위 대상을 추가할 수 있습니다. 기본적으로 **[!UICONTROL 대상자]** 블록은 컴포지션 캔버스의 맨 위에 포함됩니다.

다음을 선택하면 **[!UICONTROL 대상자]** 블록의 오른쪽 레일에는 블록에 레이블을 지정하고 대상자를 추가하는 컨트롤이 표시됩니다.

![대상 블록 세부 사항이 표시됩니다.](../images/ui/audience-builder/select-audience.png)

선택 후 **[!UICONTROL 대상 추가]**, 대상자 목록이 나타납니다. 포함할 대상을 선택한 다음, **[!UICONTROL 추가]** 대상 블록에 추가합니다.

![대상자 목록이 나타납니다. 이 대화 상자에서 추가할 대상을 선택할 수 있습니다.](../images/ui/audience-builder/select-audience.png)

이제 선택한 대상자가 다음의 경우 오른쪽 레일 내에 나타납니다. **[!UICONTROL 대상자]** 블록이 선택되어 있습니다. 여기에서 결합된 대상자의 병합 유형을 변경할 수 있습니다.

![대상에 대해 가능한 병합 유형이 강조 표시됩니다.](../images/ui/audience-builder/merge-types.png)

| 병합 유형 | 설명 |
| ---------- | ----------- |
| [!UICONTROL 합집합] | 대상은 하나의 대상으로 결합됩니다. 이는 OR 작업과 동일합니다. |
| [!UICONTROL 교차] | 대상은에서 공유되는 대상과만 결합됩니다 **모두** 개 중 개가 추가됩니다. 이는 AND 작업과 동일합니다. |
| [!UICONTROL 중복 제외] | 대상은에서 공유되는 대상과만 결합됩니다 **1개, 그러나 전부는 아님** 개 중 개가 추가됩니다. 이것은 XOR 연산과 같은 결과가 될 것이다. |

## [!UICONTROL 제외] {#exclude-block}

다음 **[!UICONTROL 제외]** 블록 유형을 사용하면 지정된 하위 대상이나 속성을 더 큰 새 대상에서 제외할 수 있습니다.

을(를) 추가하려면 **[!UICONTROL 제외]** 블록을 선택하고 **+** 아이콘, 뒤에 오는 **[!UICONTROL 제외]**.

![제외 옵션이 선택되어 있습니다.](../images/ui/audience-builder/add-exclude-block.png)

다음 **[!UICONTROL 제외]** 블록이 추가되었습니다. 이 블록을 선택하면 제외에 대한 세부 정보가 오른쪽 레일에 표시됩니다. 여기에는 블록의 레이블 및 제외 유형이 포함됩니다. 다음을 제외할 수 있습니다. [대상별](#exclude-audience) 또는 [속성별](#exclude-attribute).

![사용 가능한 두 가지 서로 다른 제외 유형을 강조 표시하는 제외 블록.](../images/ui/audience-builder/exclude.png)

### 대상별로 제외 {#exclude-audience}

대상별로 제외하는 경우 을 선택하여 제외할 대상을 선택할 수 있습니다 **[!UICONTROL 대상 추가]**.

![제외할 대상을 선택할 수 있는 대상 추가 버튼이 선택되어 있습니다.](../images/ui/audience-builder/add-excluded-audience.png)

대상자 목록이 나타납니다. 선택 **[!UICONTROL 추가]** 제외할 대상을 제외 블록에 추가합니다.

![대상자 목록이 나타납니다. 이 대화 상자에서 추가할 대상을 선택할 수 있습니다.](../images/ui/audience-builder/select-audience.png)

### 속성별 제외 {#exclude-attribute}

속성별로 제외하는 경우, 다음을 선택하여 제외할 속성을 선택할 수 있습니다. ![필터](../images/ui/audience-builder/filter-attribute.png) 아이콘 내 **[!UICONTROL 제외 규칙]** 섹션.

![속성 섹션이 강조 표시되어 제외할 속성을 선택할 위치를 보여 줍니다.](../images/ui/audience-builder/exclude-attribute.png)

프로필 속성 목록이 나타납니다. 제외할 속성 유형을 선택한 후 다음을 수행합니다 **[!UICONTROL 선택]** 제외 블록에 추가합니다.

![속성 목록이 표시됩니다.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL 가입] {#join-block}

다음 **[!UICONTROL 가입]** 블록 유형을 사용하면 Adobe Experience Platform에서 아직 처리하지 않은 데이터 세트에서 외부 대상을 추가할 수 있습니다.

을(를) 추가하려면 **[!UICONTROL 가입]** 블록을 선택하고 **+** 아이콘, 뒤에 오는 **[!UICONTROL 가입]**.

![조인 옵션이 선택되어 있습니다.](../images/ui/audience-builder/add-join-block.png)

블록을 선택하면 블록의 레이블 및 데이터 보강 데이터 세트에 대상을 추가하는 옵션을 포함하여 조인에 대한 세부 사항이 오른쪽 레일에 표시됩니다.

![조인 블록에 대한 세부 정보를 포함하여 조인 블록이 강조 표시됩니다.](../images/ui/audience-builder/join.png)

선택 후 **[!UICONTROL 대상 추가]**, 대상자 목록이 나타납니다. 포함할 대상을 선택한 다음, **[!UICONTROL 추가]** 조인 블록에 추가합니다.

![대상자 목록이 나타납니다. 이 대화 상자에서 추가할 대상을 선택할 수 있습니다.](../images/ui/audience-builder/select-audience.png)

이제 선택한 대상자가 다음의 경우 오른쪽 레일 내에 나타납니다. **[!UICONTROL 가입]** 블록이 선택되어 있습니다.

![조인의 일부로 추가된 대상이 표시됩니다.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL 등급] {#rank-block}

다음 **[!UICONTROL 등급]** 블록 유형을 사용하면 새 대상이 게시되기 전에 대상의 등급을 매기고 정렬할 수 있습니다.

을(를) 추가하려면 **[!UICONTROL 등급]** 블록을 선택하고 **+** 아이콘, 뒤에 오는 **[!UICONTROL 등급]**.

![[등급] 옵션이 선택되어 있습니다.](../images/ui/audience-builder/add-rank-block.png)

블록을 선택하면 블록의 레이블, 순위를 지정할 속성, 순위 순서 및 순위를 지정할 프로필 수를 제한하기 위한 토글을 포함하여 순위에 대한 세부 정보가 오른쪽 레일에 표시됩니다.

![rank 블록의 세부 사항은 물론 rank 블록이 강조 표시됩니다.](../images/ui/audience-builder/rank.png)

대상의 등급을 지정할 속성을 선택하려면 다음을 선택합니다. ![필터](../images/ui/audience-builder/filter-attribute.png) 아이콘.

![필터 아이콘이 강조 표시되어 프로필 속성 선택 화면에 액세스하기 위해 선택할 항목을 보여 줍니다.](../images/ui/audience-builder/select-rank-attribute.png)

프로필 속성 목록이 나타납니다. 이 팝오버에서는 대상 순위를 지정할 속성 유형을 선택할 수 있습니다. 선택 **[!UICONTROL 선택]** 등급 블록에 추가합니다. 선택한 속성은 다음 작업을 수행할 수 있습니다. **전용** be of type `int`.

![속성 목록이 표시됩니다.](../images/ui/audience-builder/select-attribute.png)

속성을 선택한 후 등급 지정 순서를 선택할 수 있습니다. 오름차순(가장 낮은 순에서 가장 높은 순까지) 또는 내림차순(가장 높은 순에서 가장 낮은 순까지)입니다.

또한 를 활성화하여 반환되는 대상 수를 제한할 수 있습니다. **[!UICONTROL 프로필 제한 추가]** 토글. 이 토글이 활성화되면 내에서 반환되는 최대 대상 수를 설정할 수 있습니다. **[!UICONTROL 포함된 프로필]** 필드.

![프로필 제한 추가 토글이 강조 표시되어 반환되는 대상자 수를 제한할 수 있습니다.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL 분할] {#split-block}

다음 **[!UICONTROL 분할]** 블록 유형을 사용하면 새 대상을 다양한 하위 대상으로 분할할 수 있습니다. 백분율을 기준으로 하거나 속성으로 이 대상을 분할할 수 있습니다.

을(를) 추가하려면 **[!UICONTROL 분할]** 블록을 선택하고 **+** 아이콘, 뒤에 오는 **[!UICONTROL 분할]**.

![분할(Split) 옵션이 선택됩니다.](../images/ui/audience-builder/add-split-block.png)

### 백분율로 분할 {#split-percentage}

백분율로 분할할 경우 대상은 제공된 경로 수와 백분율에 따라 무작위로 분할됩니다.

예를 들어 각각 프로필의 비율이 다른 세 개의 경로가 있을 수 있습니다.

![저장된 대상자 수와 백분율 분류가 표시됩니다.](../images/ui/audience-builder/percentages.png)

또한 분할된 대상 중 하나를 컨트롤 그룹으로 표시할 수 있습니다.

![컨트롤 그룹 토글이 활성화됩니다. 이렇게 하면 분할된 대상 중 하나를 컨트롤 그룹으로 표시할 수 있습니다.](../images/ui/audience-builder/control-group.png)

### 속성으로 분할 {#split-attribute}

속성별로 분할하면 제공된 속성을 기준으로 대상자가 분할됩니다. 분할할 속성을 선택하려면 **[!UICONTROL 분할]** 블록, 뒤에 오는 ![필터](../images/ui/audience-builder/filter-attribute.png) 아이콘.

![특성별로 필터링하는 방법을 보여주는 필터 버튼이 선택됩니다.](../images/ui/audience-builder/select-attribute-split.png)

프로필 속성 목록이 나타납니다. 속성 유형을 선택한 다음 를 선택합니다. **[!UICONTROL 선택]** 분할 블록에 추가합니다.

![속성 목록이 표시됩니다.](../images/ui/audience-builder/select-attribute.png)

속성을 선택한 후 내에 값을 추가하여 어떤 프로필이 어떤 하위 대상에 속할지 선택할 수 있습니다. **[!UICONTROL 값]** 필드.

![속성을 분할하려는 값이 추가됩니다.](../images/ui/audience-builder/attribute-split-values.png)

또한 **[!UICONTROL 기타 프로필]** 전환하여 선택되지 않은 모든 프로필로 구성되는 하위 대상을 만듭니다.

![기타 프로파일 토글이 강조 표시됩니다.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## 대상자 게시

대상을 작성한 후 을(를) 선택하여 대상자를 저장하고 게시할 수 있습니다. **[!UICONTROL 게시]**.

![[게시] 버튼이 강조 표시되어 대상을 저장하고 게시하는 방법을 보여 줍니다.](../images/ui/audience-builder/publish-audience.png)

대상자를 만드는 동안 오류가 발생하면 문제를 해결하는 방법을 알려주는 경고가 표시됩니다.

![[게시] 버튼이 강조 표시되어 대상을 저장하고 게시하는 방법을 보여 줍니다.](../images/ui/audience-builder/audience-alert.png)

## 다음 단계

대상 빌더는 다양한 블록 유형에서 대상을 만들 수 있는 풍부한 워크플로를 제공합니다. 세분화 서비스 UI의 다른 부분에 대해 자세히 알아보려면 다음을 참조하십시오. [세그먼테이션 서비스 사용 안내서](./overview.md).
