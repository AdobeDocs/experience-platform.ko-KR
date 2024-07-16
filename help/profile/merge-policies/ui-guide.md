---
keywords: Experience Platform;프로필;실시간 고객 프로필;병합 정책;UI;사용자 인터페이스;타임스탬프 정렬;데이터 세트 우선 순위
title: 병합 정책 UI 안내서
type: Documentation
description: 여러 소스의 데이터를 Experience Platform으로 가져올 때 병합 정책은 Platform에서 데이터를 우선 순위가 매겨지는 방법과 어떤 데이터가 결합되어 통합 보기를 생성할 것인지 결정하는 데 사용하는 규칙입니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 병합 정책 작업에 대한 단계별 지침을 제공합니다.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '2327'
ht-degree: 0%

---


# 병합 정책 UI 안내서

Adobe Experience Platform을 사용하면 여러 소스에서 데이터 조각을 한데 모아 결합하여 각 개별 고객에 대한 전체 보기를 볼 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 [!DNL Platform]이(가) 데이터의 우선 순위 지정 방법 및 통합 보기를 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하며 조직의 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 Adobe Experience Platform UI(사용자 인터페이스)를 사용하여 병합 정책 작업에 대한 단계별 지침을 제공합니다.

병합 정책 및 Experience Platform 내에서 수행하는 역할에 대해 자세히 알아보려면 [병합 정책 개요](overview.md)를 읽어 보십시오.

## 시작하기

이 안내서를 사용하려면 몇 가지 중요한 [!DNL Experience Platform] 기능에 대해 제대로 이해하고 있어야 합니다. 이 안내서를 따르기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [실시간 고객 프로필](../home.md): 여러 소스의 집계 데이터를 기반으로 통합된 실시간 고객 프로필을 제공합니다.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): [!DNL Platform]에 수집되는 서로 다른 데이터 소스의 ID를 연결하여 실시간 고객 프로필을 활성화합니다.
* [XDM(경험 데이터 모델)](../../xdm/home.md): [!DNL Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.

## 병합 정책 보기 {#view-merge-policies}

[!DNL Experience Platform] UI 내에서 왼쪽 탐색에서 **[!UICONTROL 프로필]**&#x200B;을 선택한 다음 **[!UICONTROL 병합 정책]** 탭을 선택하여 병합 정책 작업을 시작할 수 있습니다. 이 탭에는 조직에 대한 모든 기존 병합 정책 목록과 정책 이름, 병합 정책이 기본 병합 정책인지 여부 및 병합 정책과 관련된 스키마 클래스를 비롯한 각 병합 정책에 대한 세부 정보가 포함됩니다.

![병합 정책 랜딩 페이지](../images/merge-policies/landing.png)

표시되는 세부 정보를 선택하거나 화면에 열을 추가하려면 **[!UICONTROL 열 구성]**&#x200B;을 선택하고 열 이름을 클릭하여 보기에서 추가하거나 제거합니다.

![](../images/merge-policies/adjust-view.png)

## 병합 정책 만들기 {#create-a-merge-policy}

새 병합 정책을 만들려면 병합 정책 탭에서 **[!UICONTROL 병합 정책 만들기]**&#x200B;를 선택하여 새 병합 정책 워크플로를 입력합니다.

![만들기 단추가 강조 표시된 병합 정책 랜딩 페이지입니다.](../images/merge-policies/create-new.png)

**[!UICONTROL 새 병합 정책]** 워크플로에서는 일련의 안내 단계를 통해 새 병합 정책에 대한 중요한 정보를 제공해야 합니다. 이러한 단계는 다음 섹션에 설명되어 있습니다.

![새 병합 정책 워크플로입니다.](../images/merge-policies/create.png)

## [!UICONTROL 구성] {#configure}

워크플로우의 첫 번째 단계에서는 기본 정보를 제공하여 병합 정책을 구성할 수 있습니다. 이 정보에는 다음이 포함됩니다.

* **[!UICONTROL 이름]**: 병합 정책의 이름은 설명적이어야 하며 간결해야 합니다.
* **[!UICONTROL 스키마 클래스]**: 병합 정책과 연결된 XDM 스키마 클래스입니다. 이 병합 정책이 생성되는 스키마 클래스를 지정합니다. 조직은 스키마 클래스당 여러 병합 정책을 생성할 수 있습니다. 현재 UI에서는 [!UICONTROL XDM 개별 프로필] 클래스만 사용할 수 있습니다. **[!UICONTROL 유니온 스키마 보기]**&#x200B;를 선택하여 스키마 클래스의 유니온 스키마를 미리 볼 수 있습니다. 자세한 내용은 다음에 나오는 [유니온 스키마 보기](#view-union-schema)에 대한 섹션을 참조하십시오.
* **[!UICONTROL ID 결합]**: 이 필드는 고객의 관련 ID를 확인하는 방법을 정의합니다. ID 결합에는 두 가지 가능한 값이 있으며, 선택하는 ID 결합 유형이 데이터에 어떤 영향을 미치는지 이해하는 것이 중요합니다. 자세한 내용은 [병합 정책 개요](overview.md)를 참조하세요.
   * **[!UICONTROL 없음]**: ID 결합을 수행하지 않습니다.
   * **[!UICONTROL 개인 그래프]**: 개인 ID 그래프를 기반으로 ID 결합을 수행합니다.
* **[!UICONTROL 기본 병합 정책]**: 이 병합 정책이 조직의 기본값이 되는지 여부를 선택할 수 있는 전환 단추입니다. 선택기가 전환되면 조직의 기본 병합 정책을 변경할 것인지 확인하는 경고가 나타납니다. 기본 병합 정책에 대한 자세한 내용은 [병합 정책 개요](overview.md)를 참조하십시오.
  ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge 병합 정책]**: 이 병합 정책을 Edge에서 활성화할지 여부를 선택할 수 있는 전환 단추입니다. 모든 프로필 소비자가 에지에서 동일한 보기로 작업할 수 있도록 병합 정책을 에지에서 활성으로 표시할 수 있습니다. 대상이 Edge에서 활성화되려면(Edge Audience로 표시됨) Edge에서 활성으로 표시된 병합 정책에 연결되어 있어야 합니다. 대상이 Edge에서 활성으로 표시된 병합 정책에 연결된 **not**&#x200B;인 경우 대상은 Edge에서 활성으로 표시되지 않고 스트리밍 대상으로 표시됩니다. 또한 조직의 각 샌드박스는 Edge에서 활성화된 **one** 병합 정책만 가질 수 있습니다.

필수 필드가 완료되면 **[!UICONTROL 다음]**&#x200B;을 선택하여 워크플로우를 계속할 수 있습니다.

![다음 단추가 강조 표시된 전체 구성 화면입니다.](../images/merge-policies/create-complete.png)

## [!UICONTROL 유니온 스키마 보기] {#view-union-schema}

병합 정책을 만들거나 편집할 때 **[!UICONTROL 통합 스키마 보기]**&#x200B;를 선택하여 선택한 스키마 클래스에 대한 통합 스키마를 볼 수 있습니다.

![](../images/merge-policies/view-union-schema.png)

유니온 스키마와 연결된 모든 기여 스키마, ID 및 관계를 표시하는 [!UICONTROL 유니온 스키마 보기] 대화 상자가 열립니다. 대화 상자를 통해 Platform UI의 [!UICONTROL 프로필] 섹션에서 [!UICONTROL 유니온 스키마] 탭에 액세스하는 것과 같은 방식으로 유니온 스키마를 탐색할 수 있습니다.

병합 정책 워크플로에 표시된 [!UICONTROL 유니온 스키마] 탭 또는 [!UICONTROL 유니온 스키마 보기] 대화 상자에서 유니온 스키마와 상호 작용하는 방법을 포함하여 유니온 스키마에 대한 자세한 내용은 [유니온 스키마 UI 안내서](../ui/union-schema.md)를 참조하십시오.

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 프로필 데이터 세트 선택] {#select-profile-datasets}

**[!UICONTROL 프로필 데이터 세트 선택]** 화면에서 병합 정책에 사용할 **[!UICONTROL 병합 메서드]**&#x200B;를 선택해야 합니다. 또한 이전 화면에서 선택한 스키마 클래스와 관련된 조직의 총 [!UICONTROL 프로필 데이터 세트] 수가 화면에 표시됩니다.

선택한 병합 방법에 따라 모든 프로필 데이터 세트가 마지막으로 업데이트된 순서(타임스탬프 정렬)에 따라 병합되거나 병합 정책에 포함할 프로필 데이터 세트와 이를 병합할 순서(데이터 세트 우선 순위)를 선택해야 합니다.

병합 방법에 대한 자세한 내용은 [병합 정책 개요](overview.md)를 참조하십시오.

### 타임스탬프 정렬됨 {#timestamp-ordered-profile}

**[!UICONTROL 타임스탬프 정렬]**&#x200B;을(를) 병합 방법으로 선택하면 가장 최근에 업데이트된 데이터 세트의 특성이 우선합니다. 이는 모든 프로필 데이터 세트에 적용됩니다.

>[!NOTE]
>
>**[!UICONTROL 프로필 데이터 세트]** 옆의 대괄호 안에 있는 숫자(예: 표시된 이미지에서 `(37)`)는 포함될 총 프로필 데이터 세트 수를 보여줍니다.

![](../images/merge-policies/timestamp-ordered.png)

### 데이터 세트 우선 순위 {#dataset-precedence-profile}

병합 방법으로 **[!UICONTROL 데이터 세트 우선 순위]**&#x200B;를 선택하려면 프로필 데이터 세트를 선택하고 수동으로 우선 순위를 지정해야 합니다. 나열된 각 데이터 세트에는 마지막으로 수집된 일괄 처리의 상태도 포함되거나 해당 데이터 세트에 일괄 처리가 수집되지 않았다는 알림이 표시됩니다.

데이터 세트 목록에서 병합 정책에 포함할 최대 50개의 데이터 세트를 선택할 수 있습니다.

>[!NOTE]
>
>**[!UICONTROL 프로필 데이터 세트]** 옆의 대괄호 안에 있는 숫자(예: 표시된 이미지에서 `(37)`)는 선택할 수 있는 총 프로필 데이터 세트 수를 보여 줍니다.

데이터 세트를 선택하면 **[!UICONTROL 데이터 세트 선택]** 섹션에 데이터 세트가 추가되므로 데이터 세트를 끌어다 놓고 원하는 우선 순위에 따라 순서를 지정할 수 있습니다. 데이터 세트가 목록에서 조정되면 데이터 세트 옆에 있는 서수(1, 2, 3 등)가 업데이트되어 우선 순위(1이 가장 높은 우선 순위를 부여받고 2가 그 이후에)가 표시됩니다.

데이터 집합을 선택하면 **[!UICONTROL 유니온 스키마]** 섹션도 업데이트되어 각 데이터 집합이 데이터를 기여하는 유니온 스키마의 필드가 표시됩니다. UI의 시각화와 상호 작용하는 방법을 포함하여 유니온 스키마에 대한 자세한 내용은 [유니온 스키마 UI 안내서](../ui/union-schema.md)를 참조하십시오.

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL ExperienceEvent 데이터 세트 선택] {#select-experienceevent-datasets}

워크플로우의 다음 단계에서는 ExperienceEvent 데이터 세트를 선택해야 합니다. 이 화면은 [[!UICONTROL 프로필 데이터 세트 선택]](#select-profile-datasets) 화면에서 선택한 병합 방법의 영향을 받습니다.

### 타임스탬프 정렬됨 {#timestamp-ordered-experienceevent}

프로필 데이터 세트의 병합 방법으로 **[!UICONTROL 타임스탬프 정렬]**&#x200B;을(를) 선택한 경우 가장 최근에 업데이트된 ExperienceEvent 데이터 세트의 속성도 여기에서 우선합니다.

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent 데이터 세트]** 옆의 대괄호 안에 있는 숫자(예: 표시된 이미지에서 `(20)`)는 병합 정책 구성 화면에서 선택한 스키마 클래스와 관련하여 조직에서 만든 총 ExperienceEvent 데이터 세트 수를 보여줍니다.

![](../images/merge-policies/timestamp-experienceevent.png)

### 데이터 세트 우선 순위 {#dataset-precedence-experienceevent}

프로필 데이터 세트에 대한 병합 방법으로 **[!UICONTROL 데이터 세트 우선 순위]**&#x200B;를 선택한 경우 포함할 ExperienceEvent 데이터 세트를 선택해야 합니다. 데이터 세트 목록에서 최대 50개의 ExperienceEvent 데이터 세트를 선택할 수 있습니다.

>[!NOTE]
>
>**[!UICONTROL ExperienceEvent 데이터 세트]** 옆의 대괄호 안에 있는 숫자(예: 표시된 이미지에서 `(20)`)는 병합 정책 구성 화면에서 선택한 스키마 클래스와 관련하여 조직에서 만든 총 ExperienceEvent 데이터 세트 수를 보여줍니다.

데이터 세트를 선택하면 [!UICONTROL 데이터 세트 선택] 섹션에 표시됩니다.

ExperienceEvent 데이터 세트는 수동으로 정렬할 수 없습니다. 대신 ExperienceEvent 데이터 세트의 속성이 동일한 프로필 조각에 속하는 경우 프로필 데이터 세트에 추가됩니다.

프로필 데이터 세트를 선택하는 것과 마찬가지로 ExperienceEvent 데이터 세트를 선택하면 **[!UICONTROL 유니온 스키마]** 섹션도 업데이트되어 각 데이터 세트가 데이터를 기여하는 유니온 스키마의 필드를 표시합니다. UI의 시각화와 상호 작용하는 방법을 포함하여 유니온 스키마에 대한 자세한 내용은 [유니온 스키마 UI 안내서](../ui/union-schema.md)를 참조하십시오.

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 검토] {#review}

워크플로우의 마지막 단계는 병합 정책을 검토하는 것입니다. **[!UICONTROL 검토]** 화면에는 선택한 ID 결합 방법, 선택한 병합 방법 및 포함된 데이터 세트를 포함하여 병합 정책에 대한 정보가 표시됩니다. 포함된 모든 Profile 또는 ExperienceEvent 데이터 세트를 보려면 데이터 세트 수를 선택하여 드롭다운 목록을 확장합니다.

병합 정책을 사용하는 샘플 프로필 레코드를 표시하는 **[!UICONTROL 미리 보기 데이터]** 테이블도 검토 화면에 포함됩니다. 이를 통해 병합 정책을 저장하기 전에 고객 프로필의 모양을 미리 볼 수 있습니다.

**[!UICONTROL 완료]**&#x200B;를 선택하여 만들기 워크플로를 완료하기 전에 병합 정책 구성을 검토하고 데이터를 미리 보십시오.

### 타임스탬프 정렬됨 {#timestamp-ordered-review}

병합 정책에 대한 병합 방법으로 **[!UICONTROL 타임스탬프 정렬]**&#x200B;을(를) 선택한 경우, 프로필 데이터 세트 목록에는 스키마 클래스와 관련하여 조직에서 만든 모든 데이터 세트가 타임스탬프 순서대로 포함됩니다. ExperienceEvent 데이터 세트 목록에는 조직에서 선택한 스키마 클래스에 대해 만든 모든 데이터 세트가 포함되어 있으며 프로필 데이터 세트에 추가됩니다.

**[!UICONTROL 데이터 미리 보기]** 테이블은 데이터 세트의 타임스탬프 순서를 기반으로 하는 샘플 프로필 레코드를 보여 줍니다. 이를 통해 병합 정책을 저장하기 전에 고객 프로필의 모양을 미리 볼 수 있습니다.

![](../images/merge-policies/timestamp-review.png)

### 데이터 세트 우선 순위 {#dataset-precedence-review}

병합 정책에 대한 병합 방법으로 **[!UICONTROL 데이터 세트 우선 순위]**&#x200B;를 선택한 경우 Profile 및 ExperienceEvent 데이터 세트 목록에는 각각 생성 워크플로 중에 선택한 Profile 및 ExperienceEvent 데이터 세트만 포함됩니다. 프로필 데이터 세트의 순서는 작성 중에 지정한 우선 순위와 일치해야 합니다. 그렇지 않으면 [!UICONTROL 뒤로] 단추를 사용하여 이전 워크플로 단계로 돌아가서 우선 순위를 조정하십시오.

**[!UICONTROL 데이터 미리 보기]** 표에는 선택한 데이터 집합을 사용하는 샘플 프로필 레코드가 표시됩니다. 이를 통해 병합 정책을 저장하기 전에 고객 프로필의 모양을 미리 볼 수 있습니다.

![](../images/merge-policies/dataset-precedence-review.png)

### 업데이트된 병합 정책 목록 {#updated-list}

새 병합 정책을 만드는 워크플로를 완료한 후 **[!UICONTROL 병합 정책]** 탭으로 돌아갑니다. 이제 조직의 병합 정책 목록에 방금 만든 병합 정책이 포함됩니다.

![](../images/merge-policies/new-merge-policy-created.png)

## 병합 정책 편집

[!UICONTROL 병합 정책] 탭에서 편집할 병합 정책에 대해 **[!UICONTROL 정책 이름]**&#x200B;을(를) 선택하여 [!DNL XDM Individual Profile] 클래스에 대해 만들어진 기존 병합 정책을 수정할 수 있습니다.

![병합 정책 랜딩 페이지](../images/merge-policies/select-edit.png)

**[!UICONTROL 병합 정책 편집]** 화면이 나타나면 이름과 [!UICONTROL ID 결합] 메서드를 변경하고 이 정책이 조직의 기본 병합 정책인지 여부를 변경할 수 있습니다.

병합 정책 워크플로를 계속 진행하여 병합 정책에 포함된 병합 메서드 및 데이터 세트를 업데이트하려면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![](../images/merge-policies/edit-screen.png)

필요한 변경이 완료되면 병합 정책을 검토하고 **[!UICONTROL 완료]**&#x200B;를 선택하여 변경 내용을 저장하고 [!UICONTROL 병합 정책] 탭으로 돌아갑니다.

>[!WARNING]
>
>병합 정책을 변경하면 데이터 충돌이 해결되는 방식이 변경되므로 세그먼테이션 및 프로필 결과에 영향을 줄 수 있습니다. 병합 정책에 대한 변경 사항을 저장하기 전에 주의 깊게 검토하십시오.

![](../images/merge-policies/edit-review.png)

## 데이터 거버넌스 정책 위반

병합 정책을 만들거나 업데이트할 때, 병합 정책이 조직에서 정의한 데이터 사용 정책을 위반하는지 확인하기 위해 검사를 수행합니다. 데이터 사용 정책은 Adobe Experience Platform 데이터 거버넌스의 일부이며 특정 [!DNL Platform] 데이터에 대해 수행할 수 있거나 수행할 수 없는 마케팅 작업의 종류를 설명하는 규칙입니다. 예를 들어, 병합 정책을 사용하여 서드파티 대상으로 활성화된 대상을 만들고 조직에 특정 데이터를 서드파티로 내보내는 것을 방지하는 데이터 사용 정책이 있는 경우, 병합 정책을 저장하려고 할 때 **[!UICONTROL 데이터 거버넌스 정책 위반이 감지됨]** 알림을 받게 됩니다.

이 알림에는 위반된 데이터 사용 정책 목록이 포함되어 있으며 목록에서 정책을 선택하여 위반 세부 정보를 볼 수 있습니다. 위반한 정책을 선택하면 **[!UICONTROL 데이터 계보]** 탭에서 위반 이유 및 영향을 받는 활성화를 제공하고, 각 탭에서 데이터 사용 정책이 어떻게 위반되었는지 자세히 설명합니다.

Adobe Experience Platform 내에서 데이터 거버넌스를 수행하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md)를 읽는 것부터 시작하십시오.

![](../images/merge-policies/policy-violation.png)

## 다음 단계

조직에 대한 병합 정책을 만들고 구성했으므로 이를 사용하여 플랫폼 내에서 고객 프로필 보기를 조정하고 프로필 데이터에서 대상을 만들 수 있습니다. [!DNL Experience Platform] UI 및 API를 사용하여 대상을 만들고 작업하는 방법에 대한 자세한 내용은 [세그먼테이션 개요](../../segmentation/home.md)를 참조하십시오.
