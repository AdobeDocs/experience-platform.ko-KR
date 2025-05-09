---
solution: Experience Platform
title: 대상 UI 안내서
description: Adobe Experience Platform UI의 대상 구성은 프로필 데이터 요소와 상호 작용할 수 있는 풍부한 작업 영역을 제공합니다. 작업 영역에서는 조직의 대상을 작성하고 편집할 수 있는 직관적인 컨트롤을 제공합니다.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 16%

---

# 대상 구성 UI 안내서

>[!AVAILABILITY]
>
>이 기능을 사용하려면 다음 권한이 있어야 합니다.
>
>- 세그먼트 관리
>- 프로필 관리
>- 병합 정책 관리
>
>Experience Platform의 권한에 대한 자세한 내용은 [액세스 제어 개요](../../access-control/home.md#permissions)를 참조하십시오.

>[!NOTE]
>
>이 안내서에서는 대상 구성을 사용하여 대상을 만드는 방법을 설명합니다. 세그먼트 빌더를 사용하여 세그먼트 정의를 통해 대상자를 만드는 방법에 대해 알아보려면 [세그먼트 빌더 UI 안내서](./segment-builder.md)를 참조하십시오.

대상 컴포지션은 다양한 작업을 나타내는 데 사용되는 블록을 사용하여 대상을 작성하고 편집할 수 있는 작업 영역을 제공합니다.

![대상 구성 UI.](../images/ui/audience-composition/audience-composition.png)

제목과 설명을 포함하여 컴포지션의 세부 정보를 변경하려면 ![슬라이더](/help/images/icons/properties.png) 버튼을 선택합니다.

**[!UICONTROL 컴포지션 속성]** 팝오버가 나타납니다. 여기에 제목과 설명을 포함하여 컴포지션의 세부 정보를 삽입할 수 있습니다.

![컴포지션 속성 팝오버가 표시됩니다.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>**not**&#x200B;을(를) 통해 컴포지션에 제목을 지정하면 기본적으로 &quot;컴포지션&quot; 제목 다음에 만든 날짜와 시간이 표시됩니다. 또한 각 컴포지션 **must**&#x200B;에는 고유한 이름이 있습니다.

컴포지션의 세부 정보를 업데이트한 후 **[!UICONTROL 저장]**&#x200B;을 선택하여 업데이트를 확인합니다. 대상자 구성 캔버스가 다시 나타납니다.

대상 구성 캔버스는 **[[!UICONTROL 대상]](#audience-block)**, **[[!UICONTROL 제외]](#exclude-block)**, **[[!UICONTROL 순위]](#rank-block)** 및 **[[!UICONTROL 분할]](#split-block)** 블록의 네 가지 다른 유형으로 구성됩니다.

## [!UICONTROL 대상자] {#audience-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_audience"
>title="대상자 블록"
>abstract="대상자 블록을 사용하면 새로운 대상자를 구성하는 데 사용할 하위 대상자를 추가할 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_merge_types"
>title="병합 유형"
>abstract="병합 유형은 선택한 하위 대상자가 결합되는 방식을 결정합니다. 지원되는 값에는 합집합, 교집합, 중첩 제외가 있습니다."

**[!UICONTROL 대상]** 블록 형식을 사용하면 더 큰 새 대상을 구성하는 데 사용할 하위 대상을 추가할 수 있습니다. 기본적으로 **[!UICONTROL 대상]** 블록은 컴포지션 캔버스의 맨 위에 포함됩니다.

**[!UICONTROL 대상]** 블록을 선택하면 오른쪽 레일에 대상 레이블을 지정하고, 블록에 대상을 추가하고, 대상 블록에 대한 사용자 지정 규칙을 작성하는 컨트롤이 표시됩니다.

>[!NOTE]
>
>대상을 **추가하거나**&#x200B;하여 사용자 지정 규칙을 만들 수 있습니다. 이 두 기능은 **함께 사용할 수 없습니다**.

![대상자 블록 세부 정보가 표시됩니다.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL 대상 추가] {#add-audience}

대상 블록에 대상을 추가하려면 **[!UICONTROL 대상 추가]**&#x200B;를 선택합니다.

![대상자 추가 단추가 강조 표시됩니다.](../images/ui/audience-composition/select-add-audience.png)

>[!IMPORTANT]
>
>기본 병합 정책을 사용하여 정의된 **대상만**&#x200B;개 표시됩니다.
>
>또한 세그먼트 빌더를 사용하여 만든 **게시된** 대상만 사용할 수 있습니다. 대상 구성을 사용하여 만든 대상 및 외부에서 생성된 대상은 **사용할 수 없습니다**.

대상자 목록이 나타납니다. 포함할 대상을 선택한 다음 **[!UICONTROL 추가]**&#x200B;를 선택하여 대상 블록에 추가합니다.

![대상자 목록이 나타납니다. 이 대화 상자에서 추가할 대상을 선택할 수 있습니다.](../images/ui/audience-composition/select-audience.png)

**[!UICONTROL 대상자]** 블록을 선택하면 선택한 대상자가 이제 오른쪽 레일 내에 표시됩니다. 여기에서 결합된 대상자의 병합 유형을 변경할 수 있습니다.

![대상에 대해 가능한 병합 유형이 강조 표시됩니다.](../images/ui/audience-composition/merge-types.png)

| 병합 유형 | 설명 |
| ---------- | ----------- |
| [!UICONTROL 결합] | 대상은 하나의 대상으로 결합됩니다. 이는 OR 작업과 동일합니다. |
| [!UICONTROL 교차] | 대상은 결합되어 **모두**&#x200B;에서 공유된 대상만 추가됩니다. 이는 AND 작업과 동일합니다. |
| [!UICONTROL 중복 제외] | 대상자가 결합되어 **one에서 공유되는 대상자만**&#x200B;이(가) 모두 추가되지 않습니다. 이것은 XOR 연산과 같은 결과가 될 것이다. |

### [!UICONTROL 규칙 작성] {#build-rule}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rule_builder"
>title="세그먼트 빌더"
>abstract="세그먼트 빌더를 사용하면 컴포지션에 대한 사용자 정의 규칙을 추가할 수 있습니다."

대상 블록에 사용자 지정 규칙을 추가하려면 **[!UICONTROL 규칙 빌드]**&#x200B;를 선택하십시오.

![빌드 규칙 단추가 강조 표시되어 있습니다.](../images/ui/audience-composition/select-build-rule.png)

세그먼트 빌더 가 나타납니다. 세그먼트 빌더를 사용하여 대상자가 따라야 할 사용자 지정 규칙을 만들 수 있습니다. 세그먼트 빌더 사용에 대한 자세한 내용은 [세그먼트 빌더 안내서](./segment-builder.md)를 참조하세요.

![세그먼트 빌더 UI가 표시됩니다.](../images/ui/audience-composition/segment-builder.png)

사용자 지정 규칙을 추가한 후 **[!UICONTROL 저장]**&#x200B;을 선택하여 대상자에 규칙을 추가합니다.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL 제외] {#exclude-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude"
>title="블록 제외"
>abstract="블록 제외를 사용하면 지정된 대상자 또는 속성을 컴포지션에서 제외할 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_type"
>title="제외 유형"
>abstract="특정 대상자에 속하는 프로필을 제외(대상자별 제외)하거나, 특정 속성을 기준으로 프로필을 제외(속성별 제외)할 수 있습니다."

**[!UICONTROL 제외]** 블록 형식을 사용하면 지정된 하위 대상이나 특성을 더 큰 새 대상에서 제외할 수 있습니다.

**[!UICONTROL Exclude]** 블록을 추가하려면 **+** 아이콘을 선택한 다음 **[!UICONTROL Exclude]** 아이콘을 선택하십시오.

![제외 옵션을 선택했습니다.](../images/ui/audience-composition/add-exclude-block.png)

**[!UICONTROL Exclude]** 블록이 추가되었습니다. 이 블록을 선택하면 제외에 대한 세부 정보가 오른쪽 레일에 표시됩니다. 여기에는 블록의 레이블 및 제외 유형이 포함됩니다. 대상별로 [&#128279;](#exclude-audience)또는 특성별로 [을(를) 제외할 수 있습니다](#exclude-attribute).

![사용 가능한 두 가지 제외 유형을 강조 표시하는 제외 블록입니다.](../images/ui/audience-composition/exclude.png)

### 대상별로 제외 {#exclude-audience}

대상별로 제외하는 경우 **[!UICONTROL 대상자 추가]**&#x200B;를 선택하여 제외할 대상을 선택할 수 있습니다.

![제외할 대상을 선택할 수 있는 [!UICONTROL 대상 추가] 단추가 선택되어 있습니다.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>세그먼트 빌더를 사용하여 만든 **게시된** 대상만 사용할 수 있습니다. 대상 구성을 사용하여 만든 대상 및 외부에서 생성된 대상은 **사용할 수 없습니다**.

대상자 목록이 나타납니다. 제외할 대상을 제외 블록에 추가하려면 **[!UICONTROL 추가]**&#x200B;를 선택하십시오.

![대상자 목록이 나타납니다. 이 대화 상자에서 추가할 대상을 선택할 수 있습니다.](../images/ui/audience-composition/select-audience.png)

### 속성별 제외 {#exclude-attribute}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_attribute"
>title="속성별 제외"
>abstract="속성별로 제외하면 선택한 속성에 따라 특정 프로필이 컴포지션에 나타나지 않도록 제외할 수 있습니다."

특성별로 제외하는 경우 **[!UICONTROL 제외 규칙]** 섹션 내에서 ![필터](/help/images/icons/project-edit.png) 아이콘을 선택하여 제외할 특성을 선택할 수 있습니다. 속성을 제외하면 이 속성을 포함하는 모든 프로필을 결과 대상자에서 제외할 수 있습니다.

![특성 섹션이 강조 표시되어 제외할 특성을 선택할 위치를 표시합니다.](../images/ui/audience-composition/exclude-attribute.png)

프로필 속성 목록이 나타납니다. 제외할 특성 유형을 선택한 다음 **[!UICONTROL Select]**&#x200B;을(를) 선택하여 제외 블록에 추가합니다.

![특성 목록이 표시됩니다.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>특성별로 제외할 때는 제외할 **one** 값만 지정할 수 있습니다. 쉼표나 세미콜론과 같은 모든 종류의 구분 기호를 사용하면 해당 정확한 값만 제외됩니다. 예를 들어 값을 `red, blue`(으)로 설정하면 특성에서 용어 `red, blue`이(가) 제외되지만 **not**&#x200B;은(는) 용어 `red` 또는 `blue`이(가) 제외됩니다.

## [!UICONTROL 강화] {#enrich-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich"
>title="블록 보강"
>abstract="블록 보강을 사용하여 Adobe Experience Platform 데이터 세트에서 제공되는 추가 속성으로 대상자를 보강합니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_dataset"
>title="보강 데이터 세트"
>abstract="보강 데이터 세트에는 컴포지션과 연관시키려는 데이터가 포함되어 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_criteria"
>title="보강 기준"
>abstract="보강 기준에는 소스 조인 키와 보강 데이터 세트 조인 키가 포함됩니다. 이 두 가지 키는 소스 데이터 세트와 보강 데이터 세트를 조정합니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_attributes"
>title="보강 속성"
>abstract="보강 속성은 컴포지션과 연관시키고자 하는 속성입니다."

>[!IMPORTANT]
>
>이 시점에서 데이터 보강 특성은 다운스트림 Adobe Journey Optimizer 시나리오에서 **만**&#x200B;할 수 있습니다.

**[!UICONTROL 강화]** 블록 형식을 사용하면 데이터 집합의 추가 특성으로 대상을 강화할 수 있습니다. 개인화 사용 사례에서 이러한 속성을 사용할 수 있습니다.

**[!UICONTROL 강화]** 블록을 추가하려면 **+** 아이콘을 선택한 다음 **[!UICONTROL 강화]**&#x200B;를 선택하십시오.

![[!UICONTROL 강화] 옵션을 선택했습니다.](../images/ui/audience-composition/add-enrich-block.png)

**[!UICONTROL 강화]** 블록이 추가되었습니다. 이 블록을 선택하면 데이터 보강에 대한 세부 정보가 오른쪽 레일에 표시됩니다. 여기에는 블록의 레이블 및 데이터 보강 세트가 포함됩니다.

대상자를 보강할 데이터 집합을 선택하려면 ![필터](/help/images/icons/project-edit.png) 아이콘을 선택하십시오.

![필터 단추가 강조 표시되어 있습니다. 이 옵션을 선택하면 [!UICONTROL 데이터 세트 선택] 팝오버가 표시됩니다.](../images/ui/audience-composition/enrich-select-dataset.png)

**[!UICONTROL 데이터 집합 선택]** 팝오버가 나타납니다. 데이터 강화를 위해 추가할 데이터 세트를 선택한 다음 데이터 강화를 위해 데이터 세트를 추가하려면 **[!UICONTROL 선택]**&#x200B;합니다.

![선택한 데이터 집합을 선택했습니다.](../images/ui/audience-composition/select-dataset.png)

>[!IMPORTANT]
>
>선택한 데이터 집합 **must**&#x200B;은(는) 다음 기준을 충족합니다.
>
>- 데이터 집합 **must**&#x200B;은(는) 레코드 형식입니다.
>   - 데이터 집합 **은(는) 이벤트 유형이거나 시스템 생성이거나 프로필로 표시할 수 없습니다**.
>- 데이터 집합 **must**&#x200B;은(는) 1GB 이하여야 합니다.

이제 **[!UICONTROL 데이터 보강 기준]** 섹션이 오른쪽 레일에 나타납니다. 이 섹션에서는 **[!UICONTROL Source 조인 키]** 및 **[!UICONTROL 데이터 보강 데이터 세트 조인 키]**&#x200B;를 선택하여 데이터 보강 데이터 세트를 만들려는 대상자와 연결할 수 있습니다.

![데이터 보강 기준] 영역이 강조 표시되어 있습니다.(../images/ui/audience-composition/enrichment-criteria.png)

**[!UICONTROL Source 가입 키]**&#x200B;를 선택하려면 ![필터](/help/images/icons/project-edit.png) 아이콘을 선택하십시오.

**[!UICONTROL 프로필 특성 선택]** 팝오버가 나타납니다. 소스 조인 키로 사용할 프로필 특성을 선택한 다음 **[!UICONTROL Select]**&#x200B;을(를) 선택하여 해당 특성을 소스 조인 키로 선택합니다.

![원본 조인 키로 사용할 특성이 강조 표시됩니다.](../images/ui/audience-composition/select-source-join-key.png)

**[!UICONTROL 데이터 보강 데이터 집합 조인 키]**&#x200B;를 선택하려면 ![필터](/help/images/icons/project-edit.png) 아이콘을 선택하십시오.

**[!UICONTROL 데이터 보강 특성]** 팝오버가 나타납니다. 데이터 보강 데이터 세트 조인 키로 사용할 특성을 선택한 다음 **[!UICONTROL Select]**&#x200B;을(를) 선택하여 데이터 보강 데이터 세트 조인 키로 해당 특성을 선택합니다.

![데이터 보강 데이터 집합 조인 키로 사용할 특성이 강조 표시됩니다.](../images/ui/audience-composition/select-enrichment-dataset-join-key.png)

조인 키를 모두 추가했으므로 **[!UICONTROL 데이터 보강 특성]** 섹션이 나타납니다. 이제 대상자를 향상시킬 특성을 추가할 수 있습니다. 이러한 특성을 추가하려면 **[!UICONTROL 특성 추가]**&#x200B;를 선택하십시오.

**[!UICONTROL 데이터 보강 특성]** 팝오버가 나타납니다. 데이터 집합에서 특성을 선택하여 대상자를 강화한 다음 **[!UICONTROL 선택]**&#x200B;하여 대상자에 특성을 추가할 수 있습니다.

![추가하려는 데이터 보강 특성이 강조 표시됩니다.](../images/ui/audience-composition/select-enrichment-attribute.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL 순위] {#rank-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_ranking"
>title="블록 순위"
>abstract="블록 순위를 통해 특정 속성을 기반으로 프로필의 순위를 지정하고 컴포지션에 포함할 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rank_profilelimit_text"
>title="프로필 제한 추가"
>abstract="프로필 제한 추가 토글을 사용하면 순위 지정 프로세스에 포함할 최대 프로필 수를 지정할 수 있습니다."

**[!UICONTROL Rank]** 블록 형식을 사용하면 지정된 특성을 기준으로 프로필의 등급을 매기고 정렬하고 이러한 등급 프로필을 컴포지션에 포함할 수 있습니다.

**[!UICONTROL Rank]** 블록을 추가하려면 **+** 아이콘을 선택한 다음 **[!UICONTROL Rank]**&#x200B;을(를) 선택하십시오.

![순위 옵션을 선택했습니다.](../images/ui/audience-composition/add-rank-block.png)

블록을 선택하면 블록의 레이블, 순위를 지정할 속성, 순위 순서 및 순위를 지정할 프로필 수를 제한하기 위한 토글을 포함하여 순위에 대한 세부 정보가 오른쪽 레일에 표시됩니다.

![등급 블록의 세부 정보와 함께 등급 블록이 강조 표시됩니다.](../images/ui/audience-composition/rank.png)

대상의 등급을 지정할 특성을 선택하려면 ![filter](/help/images/icons/project-edit.png) 아이콘을 선택하십시오.

![필터 아이콘이 강조 표시되어 프로필 특성 선택 화면에 액세스하기 위해 선택할 항목을 보여 줍니다.](../images/ui/audience-composition/select-rank-attribute.png)

프로필 속성 목록이 나타납니다. 이 팝오버에서는 대상 순위를 지정할 속성 유형을 선택할 수 있습니다. **[!UICONTROL 선택]**&#x200B;을(를) 선택하여 등급 블록에 추가하십시오. 선택한 특성은 **만**&#x200B;일 수 있습니다.

![특성 목록이 표시됩니다.](../images/ui/audience-composition/rank-attribute.png)

속성을 선택한 후 등급 지정 순서를 선택할 수 있습니다. 오름차순(가장 낮은 순에서 가장 높은 순까지) 또는 내림차순(가장 높은 순에서 가장 낮은 순까지)입니다.

또한 **[!UICONTROL 프로필 제한 추가]** 전환을 활성화하여 반환되는 프로필 수를 제한할 수 있습니다. 이 토글이 활성화되면 **[!UICONTROL 포함된 프로필]** 필드 내에서 반환되는 최대 프로필 수를 설정할 수 있습니다.

![프로필 제한 추가 토글이 강조 표시되어 반환된 프로필 수를 제한할 수 있습니다.](../images/ui/audience-composition/add-profile-limit-rank.png)

## [!UICONTROL 분할] {#split-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split"
>title="분할 블록"
>abstract="분할 블록을 사용하면 컴포지션을 여러 경로로 나눌 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_type"
>title="분할 유형"
>abstract="컴포지션을 백분율 분할이나 속성 분할로 나눌 수 있습니다. 백분율 분할은 프로필을 여러 경로로 임의 분할합니다. 속성 분할을 사용하면 지정된 속성을 기준으로 프로필을 분할할 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_otherprofiles_text"
>title="기타 프로필"
>abstract="기타 프로필 토글을 사용하면 다른 경로의 지정된 조건과 일치하지 않는 나머지 프로필을 사용하여 추가 경로를 만들 수 있습니다."

**[!UICONTROL 분할]** 블록 형식을 사용하면 새 대상을 다양한 하위 대상으로 분할할 수 있습니다. 백분율이나 속성에 따라 이 대상을 분할할 수 있습니다.

**[!UICONTROL 분할]** 블록을 추가하려면 **+** 아이콘을 선택한 다음 **[!UICONTROL 분할]**&#x200B;을 선택하십시오.

![분할 옵션을 선택했습니다.](../images/ui/audience-composition/add-split-block.png)

대상을 분할할 때 백분율로 분할하거나 속성별로 분할할 수 있습니다.

### 백분율 분할 {#split-percentage}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_percentage"
>title="백분율 분할"
>abstract="제공된 경로 수와 백분율에 따라 대상 고객을 무작위로 여러 대상자로 분할할 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_persistent"
>title="분할 지속"
>abstract="이 옵션을 활성화하고 ID 네임스페이스를 선택하면 분할 비율을 지속적으로 적용할 수 있습니다."

백분율로 분할할 경우 대상은 제공된 경로 수와 백분율에 따라 무작위로 분할됩니다.

![분할율이 강조 표시됩니다.](../images/ui/audience-composition/split-by-percentage.png)

또는 ID를 제공하여 백분율 기반 분할을 지속되도록 할 수도 있습니다. 사용 가능한 ID 유형에는 조직에서 사용할 수 있는 모든 ID 네임스페이스가 포함됩니다.

![ID로 분할 확인란이 강조 표시되어 있습니다. 또한 분할할 ID로 선택할 수 있는 드롭다운이 강조 표시됩니다.](../images/ui/audience-composition/split-by-identity.png)

### 속성으로 분할 {#split-attribute}

속성별로 분할하면 제공된 속성을 기준으로 대상자가 분할됩니다. 분할할 특성을 선택하려면 **[!UICONTROL 분할]** 블록을 선택한 다음 ![필터](/help/images/icons/project-edit.png) 아이콘을 선택합니다.

![필터 단추를 선택하여 특성별로 필터링하는 방법을 표시합니다.](../images/ui/audience-composition/split-by-attribute.png)

프로필 속성 목록이 나타납니다. 특성 유형을 선택한 다음 **[!UICONTROL Select]**&#x200B;을(를) 선택하여 분할 블록에 추가합니다.

![특성 목록이 표시됩니다.](../images/ui/audience-composition/select-attribute.png)

특성을 선택한 후 **[!UICONTROL 값]** 필드 내에 값을 추가하여 어떤 프로필이 어떤 하위 대상에 속할지 선택할 수 있습니다.

![특성을 분할하려는 값이 추가됩니다.](../images/ui/audience-composition/attribute-split-values.png)

또한 **[!UICONTROL 기타 프로필]** 전환을 활성화하여 선택되지 않은 모든 프로필로 구성된 하위 대상을 만들 수 있습니다.

![다른 프로필 토글이 강조 표시됩니다.](../images/ui/audience-composition/split-other-profiles.png)

## 대상자 게시 {#publish}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_publish"
>title="게시"
>abstract="컴포지션을 게시하여 Adobe Experience Platform에서 최종 대상자를 만들 수 있습니다."

>[!IMPORTANT]
>
>대상 구성을 게시할 때 Real-Time CDP 대상 또는 Adobe Journey Optimizer 채널과 같은 다운스트림 서비스에서 사용하기 위해 대상 구성을 평가하고 활성화하는 데 최대 48시간이 걸릴 수 있습니다.

컴포지션을 만든 후 **[!UICONTROL 게시]**&#x200B;를 선택하여 저장하고 게시할 수 있습니다.

![게시 단추가 강조 표시되어 컴포지션을 저장하고 게시하는 방법을 보여 줍니다.](../images/ui/audience-composition/publish.png)

대상자를 만드는 동안 오류가 발생하면 문제를 해결하는 방법을 알려주는 경고가 표시됩니다.

![게시 단추가 강조 표시되어 컴포지션을 저장하고 게시하는 방법을 보여 줍니다.](../images/ui/audience-composition/audience-alert.png)

## 다음 단계

대상 컴포지션은 다양한 블록 유형에서 컴포지션을 만들 수 있는 풍부한 워크플로를 제공합니다. 세분화 서비스 UI의 다른 부분에 대한 자세한 내용은 [세분화 서비스 사용 안내서](./overview.md)를 참조하세요.
