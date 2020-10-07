---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: 정책 병합 사용자 안내서
topic: guide
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '1441'
ht-degree: 0%

---


# 정책 병합 사용자 안내서

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 개별 고객의 전체 상황을 파악할 수 있습니다. 이 데이터를 취합할 때 병합 정책은 데이터의 우선 순위를 매기는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 [!DNL Platform] 사용하는 규칙입니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스를 사용한 병합 정책 작업에 대한 단계별 지침을 제공합니다.

API를 사용하여 병합 정책을 사용하고 싶으면 [!DNL Real-time Customer Profile] 병합 정책 API 자습서에 설명된 지침을 따르십시오 [](../api/merge-policies.md).

## 시작하기

이 가이드는 병합 정책과 관련된 다양한 [!DNL Experience Platform] 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [[!DNL 실시간 고객 프로필]](../home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Identity Service]](../../identity-service/home.md):인제스트되는 여러 데이터 소스의 ID를 결합함으로써 사용할 수 [!DNL Real-time Customer Profile] [!DNL Platform]있습니다.
* [[!DNL 경험 데이터 모델(XDM)]](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

## 병합 정책 보기

사용자 인터페이스 내에서 병합 정책을 사용하여 작업을 시작하고 왼쪽 레일에서 [!DNL Experience Platform] 프로필 **[!UICONTROL 을 선택한 다음 [정책]** 병합] 탭을 선택하여 조직의 기존 병합 정책 **[!UICONTROL 목록을 볼 수 있습니다]** .

![정책 병합 랜딩 페이지](../images/merge-policies/landing.png)

조직에서 사용할 수 있는 각 병합 정책에 대한 세부 사항은 랜딩 페이지에 정책 이름, 기본 병합 정책 및 스키마를 포함하여 볼 수 있습니다.

표시할 세부 사항을 선택하거나, 표시할 열을 추가하려면 열 선택기 아이콘을 선택하고 열 이름을 클릭하여 보기에서 추가 또는 제거합니다.

![](../images/merge-policies/adjust-view.png)

## 병합 정책 만들기

새 병합 정책을 만들려면 병합 정책 **[!UICONTROL 만들기를 선택합니다]**.

![정책 병합 랜딩 페이지](../images/merge-policies/create-new.png)

병합 정책 **[!UICONTROL 만들기]** 화면이 나타나 새 병합 정책에 대한 중요한 정보를 제공할 수 있습니다.

![](../images/merge-policies/create.png)

* **[!UICONTROL 이름]**:병합 정책의 이름은 설명적이지만 간결해야 합니다.
* **[!UICONTROL 스키마]**:병합 정책과 연결된 스키마입니다. 이 병합 정책을 만들 XDM 스키마를 지정합니다. 조직에서는 스키마당 여러 개의 병합 정책을 만들 수 있습니다.
* **[!UICONTROL ID 연결]**:이 필드는 고객의 관련 ID를 결정하는 방법을 정의합니다. 두 가지 가능한 값이 있습니다.
   * **[!UICONTROL 없음]**:ID를 결합하지 않습니다.
   * **[!UICONTROL 비공개 그래프]**:개인 ID 그래프를 기반으로 ID 스티칭을 수행합니다.
* **[!UICONTROL 속성 병합]**:프로필 조각에는 개별 고객에 대해 존재하는 ID 목록 중 하나의 ID에 대한 정보가 포함되어 있습니다. ID 그래프 유형이 사용한 경우 둘 이상의 ID가 있을 경우 충돌하는 프로필 속성과 우선 순위를 지정해야 합니다. &quot;[!UICONTROL 속성 병합]&quot;을 사용하면 키-값(레코드 데이터) 형식 데이터 집합 간에 병합 충돌이 발생하는 경우 우선 순위를 지정할 데이터 집합 프로필 값을 지정할 수 있습니다. 두 가지 가능한 값이 있습니다.
   * **[!UICONTROL 순차 타임스탬프]**:충돌이 발생하는 경우 가장 최근에 업데이트된 프로필에 우선 순위가 지정됩니다. [!UICONTROL 순서가 지정된] 타임스탬프는 동일한 데이터 세트(다중 ID) 또는 데이터 집합 간에 데이터를 병합할 때 시스템 타임스탬프보다 우선순위가 높은 사용자 지정 타임스탬프를 지원합니다. 자세한 내용은 다음에 나오는 [타임스탬프 순서](#timestamp-ordered) 섹션을 참조하십시오.
   * **[!UICONTROL 데이터 세트 우선 순위]** :충돌이 발생하는 경우 프로필 조각을 원래 있던 데이터 세트에 따라 우선 순위를 지정합니다. 이 옵션을 선택할 때는 관련 데이터 세트와 해당 우선 순위 순서를 선택해야 합니다. 자세한 내용은 아래 데이터 [세트 우선 순위](#dataset-precedence) 정보를 참조하십시오.
* **[!UICONTROL 기본 병합 정책]**:이 병합 정책이 조직의 기본값인지 여부를 선택할 수 있는 전환 단추입니다. 선택기가 전환되고 새 정책이 저장된 경우, 이전 기본 정책은 더 이상 기본값이 되지 않도록 자동으로 업데이트됩니다.

### 타임스탬프 순서 지정 {#timestamp-ordered}

프로필 레코드가 Experience Platform으로 수집되면 수집 시 시스템 타임스탬프를 획득하여 레코드에 추가됩니다. 병합 **[!UICONTROL 정책에 대한 &quot;]** 속성 병합&quot; 유형으로 순차적 타임스탬프를 선택하면 시스템 타임스탬프를 기반으로 프로필이 병합됩니다. 즉, 레코드를 플랫폼으로 인제스트한 때의 타임스탬프를 기반으로 병합이 수행됩니다.

경우에 따라 사용자 지정 타임스탬프를 제공하고 병합 정책이 시스템 타임스탬프가 아닌 사용자 지정 타임스탬프를 준수하도록 하는 데 필요한 경우도 있습니다. 이러한 예로는 데이터 채우기 또는 레코드가 순서가 틀린 경우 올바른 이벤트 순서 보장 등이 있습니다.

>[!NOTE]
>
>이 기능은 데이터 집합 간에 수집에만 사용할 수 있습니다. 동일한 데이터 세트를 사용하여 레코드를 인제스트하는 경우 기본 교체 동작이 발생합니다.

### 사용자 지정 타임스탬프 사용 {#custom-timestamps}

사용자 지정 타임스탬프를 사용하려면 &quot;[!UICONTROL 외부 소스 시스템 감사 세부 정보 혼합]&quot;을 프로필 스키마에 추가해야 합니다. 사용자 지정 타임스탬프가 추가되면 `lastUpdatedDate` 필드를 사용하여 채울 수 있습니다.

레코드가 채워지는 `lastUpdatedDate` 필드를 사용하여 수집되면 Experience Platform은 해당 필드를 사용하여 데이터 집합 간에 레코드를 병합합니다. If `lastUpdatedDate` is not present, or not pliced, will continue to use the system timestamp.

>[!NOTE]
>
>동일한 레코드에서 업데이트를 `lastUpdatedDate` 인제스트할 때 타임스탬프가 채워지는지 확인해야 합니다.

다음 스크린샷은 &quot;[!UICONTROL 외부 소스 시스템 감사 세부 정보 혼합&quot;의 필드를 보여줍니다]. 스키마에 믹스를 추가하는 방법을 비롯하여 UI를 사용하는 스키마 작업에 대한 단계별 지침을 보려면 [튜토리얼을 참조하여 UI를 사용하여 스키마를 생성하십시오](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-mixin.png)

API를 사용하여 사용자 지정 타임스탬프를 사용하려면 [병합 정책 끝점 안내서의 부록](../api/merge-policies.md) 및 사용자 지정 타임스탬프 [사용 섹션을 참조하십시오](../api/merge-policies.md#custom-timestamps).

### 데이터 세트 우선 순위 {#dataset-precedence}

속성 **[!UICONTROL 병합]** 값을 선택할 때 데이터 세트 우선 순위 **[!UICONTROL 를]** 선택하여 데이터 세트가 있었던 데이터 세트에 따라 프로필 조각에 우선 순위를 지정할 수 있습니다.

사용 사례는 조직에서 다른 데이터 세트에 있는 데이터보다 선호되거나 신뢰할 수 있는 하나의 데이터 세트에 정보가 있는 경우입니다.

데이터 세트 우선 순위 **[!UICONTROL 를]**&#x200B;선택하면 별도의 패널이 열리므로 **[!UICONTROL 데이터 세트를 포함할 사용 가능한 데이터 세트]** (또는 확인란을 사용하여 모두 선택)에서 선택해야 합니다. 그런 다음 해당 데이터 세트를 [**!UICONTROL 선택한 데이터 세트]** 패널에 드래그하여 놓고 올바른 우선 순위 순서로 드래그할 수 있습니다. 최상위 데이터 세트에 우선 순위가 가장 높은 경우 두 번째 데이터 세트에 두 번째 우선 순위가 되는 등

![](../images/merge-policies/dataset-precedence.png)

병합 정책 만들기를 완료한 후 **[!UICONTROL 저장을]** 선택하여 정책 **[!UICONTROL 목록에 새 병합 정책이 표시되는]** 병합 정책탭으로 돌아갑니다.

## 병합 정책 편집

편집할 병합 정책에 대한 [!UICONTROL 정책 이름을] 선택하여 [병합 정책 **** ] 탭을 통해 기존 병합 정책을 수정할 수 있습니다.

![정책 병합 랜딩 페이지](../images/merge-policies/select-edit.png)

병합 정책 **[!UICONTROL 편집]** 화면이 나타나면 이름, 스키마, ID 연결 유형 및 속성 병합 유형을 변경할 수 있을 뿐만 아니라 이 정책이 조직의 기본 병합 정책인지 여부를 선택할 수 있습니다.

>[!NOTE]
>
>편집 화면 상단에 표시되는 병합 정책 ID는 편집할 수 없습니다. 이 ID는 변경할 수 없는 읽기 전용 시스템 생성 ID입니다.

![](../images/merge-policies/edit-screen.png)

필요한 변경 사항을 적용한 후 **[!UICONTROL 저장을]** 선택하여 업데이트된 병합 정책 정보가 표시되는 **[!UICONTROL 병합 정책]** 탭으로 돌아갑니다.

![](../images/merge-policies/edited.png)

## 데이터 거버넌스 정책 위반

병합 정책을 만들거나 업데이트할 때 병합 정책이 조직에서 정의한 데이터 사용 정책을 위반하는지 여부를 확인하는 검사가 수행됩니다. 데이터 사용 정책은 Adobe Experience Platform [!DNL Data Governance] 의 일부이며 특정 [!DNL Platform] 데이터에 대해 수행할 수 있거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다. 예를 들어, 병합 정책을 사용하여 서드 파티 대상으로 활성화된 세그먼트를 만들고 조직에서 특정 데이터를 제3자로 내보낼 수 없도록 하는 데이터 사용 정책을 가지고 있는 경우 병합 정책을 저장하려고 하면 &quot;[!UICONTROL 데이터 거버넌스 정책 위반 감지]&quot; 알림을 받게 됩니다.

이 알림에는 위반된 데이터 사용 정책 목록이 포함되어 있으며 목록에서 정책을 선택하여 위반 세부 사항을 볼 수 있습니다. 위반된 정책을 선택할 때 **[!UICONTROL 데이터 연결]** 탭은 위반의 이유와 영향을 받는 활동]을 제공하며, 각 탭에서는 데이터 사용 정책 위반 방법에 대해 자세히 설명합니다.

Adobe Experience Platform 내에서 데이터 거버넌스 수행 방법에 대한 자세한 내용은 [데이터 거버넌스 개요를 읽어 보시기 바랍니다](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## 다음 단계

이제 IMS 조직에 대한 병합 정책을 만들고 구성했으므로 프로필 데이터에서 대상 세그먼트를 만들 수 있습니다. 세그먼트를 [만들고 사용하는 방법에 대한 자세한 내용은 세그멘테이션 개요를](../../segmentation/home.md) 참조하십시오 [!DNL Experience Platform].