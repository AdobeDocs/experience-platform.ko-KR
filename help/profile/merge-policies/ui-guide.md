---
keywords: Experience Platform;프로필;실시간 고객 프로필;병합 정책;UI;사용자 인터페이스;타임스탬프 순서;데이터 세트 우선순위
title: 병합 정책 UI 안내서
type: Documentation
description: Experience Platform에서 여러 소스의 데이터를 함께 가져올 때 병합 정책은 Platform이 데이터 우선 순위가 지정되는 방식과 통합 보기를 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 병합 정책 작업을 위한 단계별 지침을 제공합니다.
exl-id: 0489217a-6a53-428c-a531-fd0a0e5bb71f
source-git-commit: e94756254a24ecadd7359589cd14cfb0745c789c
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# 병합 정책 UI 안내서

Adobe Experience Platform을 사용하면 여러 소스에서 데이터 조각을 함께 가져와서 결합하여 각 개별 고객에 대한 전체 보기를 볼 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책이 [!DNL Platform] 는 데이터의 우선 순위가 지정되는 방식과 데이터를 결합하여 통합 보기를 만드는 방법을 결정합니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스(UI)를 사용하여 병합 정책 작업에 대한 단계별 지침을 제공합니다.

병합 정책 및 Experience Platform 내에서 수행하는 역할에 대해 자세히 알아보려면 [정책 병합 개요](overview.md).

## 시작하기

이 안내서에서는 몇 가지 중요한 사항에 대한 작업 이해를 필요로 합니다 [!DNL Experience Platform] 기능. 이 안내서를 따르기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [실시간 고객 프로필](../home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [Adobe Experience Platform Identity 서비스](../../identity-service/home.md): 수집할 여러 데이터 소스의 ID를 브리징하여 실시간 고객 프로필을 활성화합니다 [!DNL Platform].
* [XDM(경험 데이터 모델)](../../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다.

## 병합 정책 보기 {#view-merge-policies}

내 [!DNL Experience Platform] UI, 을 선택하여 병합 정책 작업을 시작할 수 있습니다 **[!UICONTROL 프로필]** 왼쪽 탐색에서 를 선택하고 **[!UICONTROL 병합 정책]** 탭. 이 탭에는 조직에 대한 모든 기존 병합 정책 목록과 정책 이름, 병합 정책이 기본 병합 정책인지 여부 및 병합 정책이 관련된 스키마 클래스 등 각 병합 정책에 대한 세부 정보가 포함되어 있습니다.

![병합 정책 랜딩 페이지](../images/merge-policies/landing.png)

표시되는 세부 사항을 선택하거나 디스플레이에 열을 추가하려면 을 선택합니다 **[!UICONTROL 열 구성]** 열 이름을 클릭하여 보기에서 추가하거나 제거합니다.

![](../images/merge-policies/adjust-view.png)

## 병합 정책 만들기 {#create-a-merge-policy}

새 병합 정책을 만들려면 **[!UICONTROL 병합 정책 만들기]** 병합 정책 탭에서 새 병합 정책 워크플로우를 입력합니다.

![정책 랜딩 페이지를 만들기 단추가 강조 표시된 상태로 병합합니다.](../images/merge-policies/create-new.png)

다음 **[!UICONTROL 새 병합 정책]** 워크플로우에서는 일련의 안내가 있는 단계를 통해 새 병합 정책에 대한 중요한 정보를 제공해야 합니다. 이러한 단계는 다음에 나오는 섹션에 요약되어 있습니다.

![새 병합 정책 워크플로입니다.](../images/merge-policies/create.png)

##  구성 {#configure}

워크플로우의 첫 번째 단계에서는 기본 정보를 제공하여 병합 정책을 구성할 수 있습니다. 이 정보에는 다음이 포함됩니다.

* **[!UICONTROL 이름]**: 병합 정책의 이름은 설명적이지만 간결해야 합니다.
* **[!UICONTROL 스키마 클래스]**: 병합 정책과 연결된 XDM 스키마 클래스입니다. 이 병합 정책을 만들 스키마 클래스를 지정합니다. 조직에서는 스키마 클래스당 여러 병합 정책을 만들 수 있습니다. 현재 [!UICONTROL XDM 개별 프로필] 클래스는 UI에서 사용할 수 있습니다. 스키마 클래스에 대한 결합 스키마를 미리 보려면 **[!UICONTROL 결합 스키마 보기]**. 자세한 내용은 [결합 스키마 보기](#view-union-schema) 그 다음은 이렇습니다.
* **[!UICONTROL ID 결합]**: 이 필드는 고객의 관련 ID를 결정하는 방법을 정의합니다. ID 결합에는 두 가지 가능한 값이 있으며, 선택하는 ID 결합 유형이 데이터에 미치는 영향을 이해하는 것이 중요합니다. 자세한 내용은 [정책 병합 개요](overview.md).
   * **[!UICONTROL 없음]**: ID 결합을 수행하지 않습니다.
   * **[!UICONTROL 개인 그래프]**: 개인 ID 그래프를 기반으로 ID 결합을 수행합니다.
* **[!UICONTROL 기본 병합 정책]**: 이 병합 정책이 조직의 기본값인지 여부를 선택할 수 있는 전환 단추입니다. 선택기가 켜진 경우 조직의 기본 병합 정책을 변경할지 확인하는 메시지가 나타납니다. 자세한 내용은 [정책 병합 개요](overview.md) 기본 병합 정책에 대해 자세히 알아보십시오.
   ![](../images/merge-policies/create-make-default.png)
* **[!UICONTROL Active-On-Edge 병합 정책]**: 이 병합 정책을 에지 상태에서 활성화할지 여부를 선택할 수 있는 전환 단추입니다. 모든 프로필 소비자가 모서리에서 동일한 보기를 사용하여 작업하도록 하기 위해 병합 정책을 에지 상태에서 활성으로 표시할 수 있습니다. 세그먼트가 에지(에지 세그먼트로 표시됨)에서 활성화되려면 에지에서 활성으로 표시된 병합 정책에 연결해야 합니다. 세그먼트가 **not** edge에서 활성으로 표시된 병합 정책에 연결된 세그먼트는 edge에서 활성으로 표시되지 않고 스트리밍 세그먼트로 표시됩니다. 또한 조직의 각 샌드박스는 **하나** 에지 상태에서 활성화된 병합 정책.

필수 필드가 완료되면 를 선택할 수 있습니다 **[!UICONTROL 다음]** 을 클릭하여 워크플로우 작업을 계속 진행합니다.

![다음 단추가 강조 표시된 전체 구성 화면.](../images/merge-policies/create-complete.png)

## [!UICONTROL 결합 스키마 보기] {#view-union-schema}

병합 정책을 만들거나 편집할 때 선택한 스키마 클래스에 대한 결합 스키마를 선택하여 볼 수 있습니다 **[!UICONTROL 결합 스키마 보기]**.

![](../images/merge-policies/view-union-schema.png)

이렇게 하면 [!UICONTROL 결합 스키마 보기] 대화 상자. 결합 스키마와 연결된 모든 기여 스키마, ID 및 관계를 표시합니다. 이 대화 상자를 사용하여 통합 스키마를 탐색하는 것과 같은 방식으로 [!UICONTROL 결합 스키마] 탭에서 다음을 수행합니다. [!UICONTROL 프로필] 플랫폼 UI의 섹션을 참조하십시오.

에서 결합 스키마와 상호 작용하는 방법 등 결합 스키마에 대한 자세한 내용은 [!UICONTROL 결합 스키마] 탭 또는 [!UICONTROL 결합 스키마 보기] 병합 정책 워크플로우에 표시된 대화 상자에서 [결합 스키마 UI 안내서](../ui/union-schema.md).

![](../images/merge-policies/view-union-schema-dialog.png)

## [!UICONTROL 프로필 데이터 세트 선택] {#select-profile-datasets}

설정 **[!UICONTROL 프로필 데이터 세트 선택]** 화면에서 **[!UICONTROL 병합 메서드]** 병합 정책에 사용할 수 있습니다. 화면에 표시되는 총 개수는 [!UICONTROL 프로필 데이터 세트] 이전 화면에서 선택한 스키마 클래스와 관련된 조직입니다.

선택한 병합 방법에 따라 모든 프로필 데이터 세트가 마지막으로 업데이트된 순서(타임스탬프 순서)로 병합되거나 병합 정책에 포함할 프로필 데이터 세트와 이를 병합하는 순서(데이터 세트 우선 순위)를 선택해야 합니다.

병합 방법에 대한 자세한 내용은 [정책 병합 개요](overview.md).

### 타임스탬프가 정렬됨 {#timestamp-ordered-profile}

선택 **[!UICONTROL 타임스탬프가 정렬됨]** 는 병합 메서드가 가장 최근에 업데이트된 데이터 세트의 속성이 우선함을 의미합니다. 모든 프로필 데이터 세트에 적용됩니다.

>[!NOTE]
>
>다음 옆의 대괄호 안에 있는 숫자 **[!UICONTROL 프로필 데이터 세트]** (예: `(37)` 표시된 이미지에서 )는 포함할 총 프로필 데이터 세트 수를 보여줍니다.

![](../images/merge-policies/timestamp-ordered.png)

### 데이터 집합 우선 순위 {#dataset-precedence-profile}

선택 **[!UICONTROL 데이터 집합 우선 순위]** 병합 메서드를 사용하려면 프로필 데이터 세트를 선택하고 수동으로 우선 순위를 지정해야 합니다. 나열된 각 데이터 세트에는 마지막으로 수집된 일괄 처리의 상태나 해당 데이터 세트에 일괄 처리가 수집되지 않았다는 알림이 표시됩니다.

데이터 세트 목록에서 병합 정책에 포함할 데이터 세트를 최대 50개까지 선택할 수 있습니다.

>[!NOTE]
>
>다음 옆의 대괄호 안에 있는 숫자 **[!UICONTROL 프로필 데이터 세트]** (예: `(37)` 표시된 이미지에서)는 선택할 수 있는 총 프로필 데이터 세트 수를 보여줍니다.

데이터 세트를 선택하면 데이터 세트가 **[!UICONTROL 데이터 세트 선택]** 섹션을 통해 데이터 세트를 드래그하여 삭제하고 원하는 우선 순위에 따라 순서를 지정할 수 있습니다. 데이터 세트가 목록에서 조정되면 데이터 세트 옆에 있는 서수(1, 2, 3 등)가 업데이트되어 우선 순위(1이 가장 높은 우선 순위를 지정한 다음 2, 그 이후)가 표시됩니다.

데이터 세트를 선택하면 도 업데이트됩니다 **[!UICONTROL 결합 스키마]** 섹션에 각 데이터 세트에 데이터가 기여하는 결합 스키마의 필드를 표시합니다. UI에서 시각화와 상호 작용하는 방법 등 결합 스키마에 대한 자세한 내용은 다음을 참조하십시오. [결합 스키마 UI 안내서](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence.png)

## [!UICONTROL ExperienceEvent 데이터 세트 선택] {#select-experienceevent-datasets}

워크플로우의 다음 단계에서는 ExperienceEvent 데이터 세트를 선택해야 합니다. 이 화면은 [[!UICONTROL 프로필 데이터 세트 선택]](#select-profile-datasets) 화면.

### 타임스탬프가 정렬됨 {#timestamp-ordered-experienceevent}

선택한 경우 **[!UICONTROL 타임스탬프가 정렬됨]** 프로필 데이터 세트에 대한 병합 메서드로서 가장 최근에 업데이트된 ExperienceEvent 데이터 세트의 속성도 여기에 우선합니다.

>[!NOTE]
>
>다음 옆의 대괄호 안에 있는 숫자 **[!UICONTROL ExperienceEvent 데이터 세트]** (예: `(20)` 아래 그림에서)는 병합 정책 구성 화면에서 선택한 스키마 클래스와 관련된 조직에서 만든 총 ExperienceEvent 데이터 세트 수를 보여줍니다.

![](../images/merge-policies/timestamp-experienceevent.png)

### 데이터 집합 우선 순위 {#dataset-precedence-experienceevent}

선택한 경우 **[!UICONTROL 데이터 집합 우선 순위]** 프로필 데이터 세트에 대한 병합 메서드로 포함할 ExperienceEvent 데이터 세트를 선택해야 합니다. 데이터 세트 목록에서 최대 50개의 ExperienceEvent 데이터 세트를 선택할 수 있습니다.

>[!NOTE]
>
>다음 옆의 대괄호 안에 있는 숫자 **[!UICONTROL ExperienceEvent 데이터 세트]** (예: `(20)` 아래 그림에서)는 병합 정책 구성 화면에서 선택한 스키마 클래스와 관련된 조직에서 만든 총 ExperienceEvent 데이터 세트 수를 보여줍니다.

데이터 세트를 선택하면 데이터 세트에 표시됩니다 [!UICONTROL 데이터 세트 선택] 섹션을 참조하십시오.

ExperienceEvent 데이터 세트는 수동으로 순서를 지정할 수 없습니다. 대신 ExperienceEvent 데이터 세트의 속성이 동일한 프로필 조각의 일부인 경우 프로필 데이터 세트에 추가됩니다.

프로필 데이터 세트를 선택하는 것과 유사하게 ExperienceEvent 데이터 세트를 선택하면 도 업데이트됩니다. **[!UICONTROL 결합 스키마]** 섹션에 각 데이터 세트에 데이터가 기여하는 결합 스키마의 필드를 표시합니다. UI에서 시각화와 상호 작용하는 방법 등 결합 스키마에 대한 자세한 내용은 다음을 참조하십시오. [결합 스키마 UI 안내서](../ui/union-schema.md)

![](../images/merge-policies/dataset-precedence-experienceevent.png)

## [!UICONTROL 검토] {#review}

워크플로우의 마지막 단계는 병합 정책을 검토하는 것입니다. 다음 **[!UICONTROL 검토]** 화면에는 선택한 ID 결합 방법, 선택한 병합 방법 및 포함된 데이터 세트를 포함하여 병합 정책에 대한 정보가 표시됩니다. 포함된 모든 프로필 또는 ExperienceEvent 데이터 세트를 보려면 드롭다운 목록을 확장할 데이터 세트 수를 선택합니다.

또한 검토 화면에 포함된 내용은 **[!UICONTROL 데이터 미리 보기]** 병합 정책을 사용하여 샘플 프로필 레코드를 표시하는 표입니다. 이렇게 하면 병합 정책을 저장하기 전에 고객 프로필의 모양을 미리 볼 수 있습니다.

선택하기 전에 병합 정책 구성을 검토하고 데이터를 신중하게 미리 확인하십시오 **[!UICONTROL 완료]** 을 클릭하여 만들기 워크플로우를 완료합니다.

### 타임스탬프가 정렬됨 {#timestamp-ordered-review}

선택한 경우 **[!UICONTROL 타임스탬프가 정렬됨]** 병합 정책을 위한 병합 메서드로 프로필 데이터 세트 목록에는 타임스탬프 순서로 스키마 클래스와 관련된 조직에서 만든 모든 데이터 세트가 포함됩니다. ExperienceEvent 데이터 세트 목록에는 조직에서 선택한 스키마 클래스에 대해 생성한 모든 데이터 세트가 포함되어 있으며 프로필 데이터 세트에 추가됩니다.

다음 **[!UICONTROL 데이터 미리 보기]** 표는 데이터 세트의 타임스탬프 순서를 기반으로 하는 샘플 프로필 레코드를 보여줍니다. 이렇게 하면 병합 정책을 저장하기 전에 고객 프로필의 모양을 미리 볼 수 있습니다.

![](../images/merge-policies/timestamp-review.png)

### 데이터 집합 우선 순위 {#dataset-precedence-review}

선택한 경우 **[!UICONTROL 데이터 집합 우선 순위]** 병합 정책을 위한 병합 메서드로 프로필 및 ExperienceEvent 데이터 세트 목록에는 만들기 워크플로우 동안 각각 선택한 프로필 및 ExperienceEvent 데이터 세트만 포함됩니다. 프로필 데이터 세트의 순서는 만드는 동안 지정한 우선 순위와 일치해야 합니다. 없는 경우 [!UICONTROL 뒤로] 이전 워크플로우 단계로 돌아가서 우선순위를 조정하는 단추입니다.

다음 **[!UICONTROL 데이터 미리 보기]** 표는 선택한 데이터 세트를 사용하는 샘플 프로필 레코드를 보여줍니다. 이렇게 하면 병합 정책을 저장하기 전에 고객 프로필의 모양을 미리 볼 수 있습니다.

![](../images/merge-policies/dataset-precedence-review.png)

### 병합 정책 목록이 업데이트되었습니다. {#updated-list}

새 병합 정책을 만드는 워크플로우를 완료하면 로 돌아갑니다. **[!UICONTROL 병합 정책]** 탭. 이제 조직의 병합 정책 목록에 방금 만든 병합 정책이 포함되어야 합니다.

![](../images/merge-policies/new-merge-policy-created.png)

## 병합 정책 편집

에서 [!UICONTROL 병합 정책] 탭에서 [!DNL XDM Individual Profile] 클래스 **[!UICONTROL 정책 이름]** 병합 정책에 대해 편집할 수 있습니다.

![병합 정책 랜딩 페이지](../images/merge-policies/select-edit.png)

이 **[!UICONTROL 병합 정책 편집]** 화면이 나타나면 이름과 [!UICONTROL ID 결합] 메서드 및 이 정책이 조직의 기본 병합 정책인지 여부를 변경할 수 있습니다.

선택 **[!UICONTROL 다음]** 병합 정책 워크플로우를 계속 진행하여 병합 정책에 포함된 병합 방법 및 데이터 세트를 업데이트합니다.

![](../images/merge-policies/edit-screen.png)

필요한 변경 작업을 수행한 후 병합 정책을 검토하고 를 선택합니다 **[!UICONTROL 완료]** 변경 사항을 저장하고 [!UICONTROL 병합 정책] 탭.

>[!WARNING]
>
>병합 정책을 변경하면 데이터 충돌이 해결되는 방식이 변경되므로 세그먼테이션 및 프로필 결과에 영향을 줄 수 있습니다. 병합 정책에 대한 변경 사항을 저장하기 전에 신중하게 검토하십시오.

![](../images/merge-policies/edit-review.png)

## 데이터 거버넌스 정책 위반

병합 정책을 만들거나 업데이트할 때 병합 정책이 조직에서 정의한 데이터 사용 정책을 위반하는지 여부를 확인하기 위해 검사가 수행됩니다. 데이터 사용 정책은 Adobe Experience Platform 데이터 거버넌스의 일부이며 특정 환경에서 수행하도록 허용되거나 제한되는 마케팅 작업의 종류를 설명하는 규칙입니다 [!DNL Platform] 데이터. 예를 들어, 병합 정책을 사용하여 서드파티 대상으로 활성화된 세그먼트를 만들었으며 조직에 데이터 사용 정책이 있어 특정 데이터를 타사에 내보내지 못하는 경우 **[!UICONTROL 데이터 거버넌스 정책 위반이 감지됨]** 병합 정책을 저장하려고 할 때 알림을 보냅니다.

이 알림에는 위반된 데이터 사용 정책 목록이 포함되어 있으며 목록에서 정책을 선택하여 위반 세부 사항을 볼 수 있습니다. 위반된 정책을 선택하면 **[!UICONTROL 데이터 계보]** 탭에는 위반 이유 및 영향을 받는 활동이 있으며, 각 탭에는 데이터 사용 정책이 위반되는 방식에 대한 자세한 내용이 표시됩니다.

Adobe Experience Platform 내에서 데이터 거버넌스가 수행되는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## 다음 단계

조직에 대한 병합 정책을 만들고 구성했으므로 이제 이 정책을 사용하여 플랫폼 내의 고객 프로필 보기를 조정하고 프로필 데이터에서 대상 세그먼트를 만들 수 있습니다. 자세한 내용은 [세분화 개요](../../segmentation/home.md) 를 사용하여 세그먼트를 만들고 작업하는 방법에 대한 자세한 정보 [!DNL Experience Platform] UI 및 API.
