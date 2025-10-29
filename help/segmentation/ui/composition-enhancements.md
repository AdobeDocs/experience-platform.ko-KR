---
title: 대상 구성 개선 사항
description: 대상 강화 및 빠른 활성화를 통해 대상 구성에 대한 개선 사항에 대해 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 42e639b403edbaf666d8bc21eb35b2b75530d6b0
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# 대상자 구성 개선 사항

이제 대상 구성에 대한 **2가지** 개선 사항에 액세스할 수 있습니다.

- [대상자 강화](#audience-enrichment)
- [더 빠른 활성화](#faster-activation)

## 대상자 강화 {#audience-enrichment}

대상 강화를 통해 프로필이 생성한 대상에 적합하도록 하는 값 배열을 출력할 수 있습니다.

컴포지션에 대상 강화를 추가하려면 캔버스 내에서 가장 높은 **[!UICONTROL Audience]** 블록을 선택하십시오. 대상에 이름을 지정한 후 **[!UICONTROL Build rule]**&#x200B;을(를) 선택하여 규칙 빌더 캔버스를 엽니다.

![대상 블록과 빌드 규칙 단추가 강조 표시됩니다.](/help/segmentation/images/ui/composition-enhancements/select-build-rule.png)

규칙 빌더 캔버스가 표시됩니다. 이제 대상 강화를 위한 필터 기준을 만들 수 있습니다. 이 필터 조건 **must**&#x200B;에는 배열 내에 있는 특성이 포함되어 있습니다. 배열인 속성은 조직의 스키마 구조에 따라 다릅니다. 필터 조건을 만든 후 오른쪽 패널에서 **[!UICONTROL Delivery]**&#x200B;을(를) 선택합니다.

![규칙 빌더 캔버스에는 다양한 기능을 사용할 수 있는 대상의 예가 표시됩니다. 게재 단추도 강조 표시됩니다.](/help/segmentation/images/ui/composition-enhancements/view-delivery.png)

왼쪽 패널의 목록에서 데이터 보강에 사용할 오브젝트 배열을 선택합니다. 프로필에 스토리지가 하나만 있는 경우 스토리지가 자동으로 선택됩니다. 대상 구성으로 돌아가려면 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오.

<!-- , as well as the fields you want to be used in the enrichment. -->

![데이터 보강 트리의 스키마 트리가 표시됩니다.](/help/segmentation/images/ui/composition-enhancements/view-schema-tree.png)

대상 구성 내에서 [!UICONTROL Audience] 블록은 이제 &quot;[!UICONTROL Rule builder with enhancement]&quot; 형식입니다. **[!UICONTROL Publish]**&#x200B;을(를) 선택하여 다음 일별 일괄 처리로 대상자를 활성화합니다.

![대상자 블록이 강조 표시되어 데이터 보강이 있는 대상자가 추가되었음을 나타냅니다.](/help/segmentation/images/ui/composition-enhancements/rule-builder-with-enrichment.png)

### 행동 세부 정보 및 보호

대상 강화를 사용하는 동안 다음 세부 사항 및 보호 기능을 염두에 두십시오.

- 대상 구성 내에서 생성된 대상 내에서만 대상 강화를 사용할 수 있습니다.
- 컴포지션 **must**&#x200B;에서 사용되는 첫 번째 블록은 규칙 기반 대상자입니다.
- **컴포지션 내에서 다른 작업을 사용할 수**&#x200B;없습니다.
- 게시되면 **규칙 기반 대상자에서 컴포지션을 편집할 수 없습니다**.

   - 기본 컴포지션 또는 규칙 기반 대상을 변경하려면 *할 수* 컴포지션을 초안으로 복사하고 초안을 편집할 수 있습니다.

- 단일 대상 내에서 데이터 보강 페이로드를 생성하는 데 **one** 개체 배열만 사용할 수 있습니다.

   - 페이로드 배열은 개체(프로필 스키마 내 최대 7개 레이어) 내에 중첩될 수 있지만 **다른 배열에 포함될 수 없습니다**.
   - 페이로드 배열 **must**&#x200B;에 50개 이하의 행이 있습니다.
   - 페이로드 **must** 내의 모든 열이 기본 형식입니다.
   - 배열의 처음 **20** 열만 출력됩니다.

- 지금은 **1}개의 대상자 구성만 사용할 수 있습니다.**

## 더 빠른 활성화 {#faster-activation}

빠른 활성화를 사용하면 컴포지션이 평가된 후 바로 다운스트림 대상으로 대상자를 활성화할 수 있습니다. 따라서 세그먼트 평가 후 대상이 활성화되도록 설정된 경우 평가 작업이 완료될 때까지 24시간 더 이상 기다릴 필요가 없습니다.

자세한 내용은 [프로필 대상을 일괄 처리하는 대상자 활성화 가이드](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)를 참조하세요.
