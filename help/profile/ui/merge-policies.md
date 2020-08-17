---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 정책 병합 사용자 안내서
topic: guide
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 0%

---


# 정책 병합 사용자 안내서

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 개별 고객의 전체 상황을 파악할 수 있습니다. 이 데이터를 취합할 때 병합 정책은 데이터의 우선 순위를 매기는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 [!DNL Platform] 사용하는 규칙입니다.

RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 이 안내서에서는 Adobe Experience Platform 사용자 인터페이스를 사용한 병합 정책 작업에 대한 단계별 지침을 제공합니다.

API를 사용하여 병합 정책을 사용하고 싶으면 [!DNL Real-time Customer Profile] 병합 정책 API 자습서에 설명된 지침을 따르십시오 [](../api/merge-policies.md).

## 시작하기

이 가이드는 병합 정책과 관련된 다양한 [!DNL Experience Platform] 서비스에 대해 작업해야 합니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

* [!DNL Real-time Customer Profile](../home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [!DNL Identity Service](../../identity-service/home.md):인제스트되는 여러 데이터 소스의 ID를 결합함으로써 사용할 수 [!DNL Real-time Customer Profile] [!DNL Platform]있습니다.
* [!DNL Experience Data Model (XDM)](../../xdm/home.md):고객 경험 데이터를 [!DNL Platform] 구성하는 표준화된 프레임워크

## 병합 정책 보기

사용자 인터페이스 내에서 병합 정책을 사용하여 작업을 시작하고 왼쪽 레일에서 [!DNL Experience Platform] 프로필 **[!UICONTROL 을 클릭한 다음 정책]** 병합 **[!UICONTROL 탭을 선택하여 조직의 기존 병합 정책 목록을 볼 수]** 있습니다.

![정책 병합 랜딩 페이지](../images/merge-policies/landing.png)

조직에서 사용할 수 있는 각 병합 정책에 대한 세부 사항은 랜딩 페이지에서 *[!UICONTROL 정책 이름]*, *[!UICONTROL 기본 병합 정책]*&#x200B;및 *[!UICONTROL 스키마]*&#x200B;를 비롯한볼 수있습니다.

표시할 세부 사항을 선택하거나, 표시할 열을 추가하려면 오른쪽의 열 선택기 아이콘을 선택하고 열 이름을 클릭하여 보기에서 추가 또는 제거합니다.

![](../images/merge-policies/adjust-view.png)

## 병합 정책 만들기

새 병합 정책을 만들려면 [정책 **[!UICONTROL 병합] 탭]** 오른쪽 상단 근처에 있는 [병합 정책 **** 만들기]를 클릭합니다.

![정책 병합 랜딩 페이지](../images/merge-policies/create-new.png)

병합 정책 **[!UICONTROL 만들기]** 화면이 나타나 새 병합 정책에 대한 중요한 정보를 제공할 수 있습니다.

![](../images/merge-policies/create.png)

* **[!UICONTROL 이름]**:병합 정책의 이름은 설명적이지만 간결해야 합니다.
* **[!UICONTROL 스키마]**:병합 정책과 연결된 스키마입니다. 이 병합 정책을 만들 XDM 스키마를 지정합니다. 조직에서는 스키마당 여러 개의 병합 정책을 만들 수 있습니다.
* **[!UICONTROL ID 연결]**:이 필드는 고객의 관련 ID를 결정하는 방법을 정의합니다. 두 가지 가능한 값이 있습니다.
   * **[!UICONTROL 없음]**:ID를 결합하지 않습니다.
   * **[!UICONTROL 비공개 그래프]**:개인 ID 그래프를 기반으로 ID 스티칭을 수행합니다.
* **[!UICONTROL 속성 병합]**:프로필 조각은 개별 고객에 대해 존재하는 ID 목록 중 하나의 ID에 대한 프로필 정보입니다. ID 그래프 유형이 사용한 경우 둘 이상의 ID가 있을 경우 프로필 속성 값과 우선 순위가 충돌할 가능성이 있습니다. 속성 병합 *을* 사용하면 병합 충돌이 발생하는 경우 우선 순위를 지정할 데이터 세트 프로필 값을 지정할 수 있습니다. 두 가지 가능한 값이 있습니다.
   * **[!UICONTROL 순차 타임스탬프]**:충돌이 발생하는 경우 가장 최근에 업데이트된 프로필에 우선 순위를 지정합니다.
   * **[!UICONTROL 데이터 세트 우선 순위]** :프로파일 단편이 있었던 데이터 세트에 따라 우선적으로 프로필 조각을 지정합니다. 이 옵션을 선택할 때는 관련 데이터 세트와 해당 우선 순위 순서를 선택해야 합니다. 자세한 내용은 아래 데이터 [세트 우선 순위](#dataset-precedence) 정보를 참조하십시오.
* **[!UICONTROL 기본 병합 정책]**:이 병합 정책이 조직의 기본값인지 여부를 선택할 수 있는 전환 단추입니다. 선택기가 전환되고 새 정책이 저장된 경우, 이전 기본 정책은 더 이상 기본값이 되지 않도록 자동으로 업데이트됩니다.

### 데이터 세트 우선 순위 {#dataset-precedence}

속성 *[!UICONTROL 병합]* 값을 선택할 때 데이터 세트 우선 순위 *[!UICONTROL 를]* 선택하여 데이터 세트가 있었던 데이터 세트에 따라 프로필 조각에 우선 순위를 지정할 수 있습니다.

사용 사례는 조직에서 다른 데이터 세트에 있는 데이터보다 선호되거나 신뢰할 수 있는 하나의 데이터 세트에 정보가 있는 경우입니다.

데이터 세트 우선 순위 *[!UICONTROL 를]*&#x200B;선택하면 별도의 패널이 열리므로 *[!UICONTROL 사용할 수 있는 데이터 세트]* (또는 확인란을 모두 선택하여 모두 선택)에서 데이터 세트를 선택해야 합니다. 그런 다음 해당 데이터 세트를 *[!UICONTROL 선택한 데이터 세트]* 패널에 드래그하여 놓고 올바른 우선 순위 순서로 드래그할 수 있습니다. 최상위 데이터 세트에 우선 순위가 가장 높은 다음 두 번째 데이터 세트가 두 번째로 높은 순서로 표시됩니다.

![](../images/merge-policies/dataset-precedence.png)

병합 정책을 모두 만들었으면 **[!UICONTROL 저장을]** 클릭하여 정책 *[!UICONTROL 목록에 새 병합 정책이 표시되는]* 병합 정책탭으로 돌아갑니다.

## 병합 정책 편집

편집하려는 병합 정책에 대한 *[!UICONTROL 정책 이름]* ** 을 클릭하여 병합 정책 탭을 통해 기존 병합 정책을 수정할 수 있습니다.

![정책 병합 랜딩 페이지](../images/merge-policies/select-edit.png)

[병합 정책 *[!UICONTROL 편집] 화면이 나타나면]* 스키마 *[!UICONTROL 이름]*&#x200B;을 변경할 수 있습니다. *[!UICONTROL 스키마]*&#x200B;이름 *[!UICONTROL , ID 스티칭하는 유형, Facebook 속성 병합 유형 및 FacebookType과 함께Facebook과 Facebook의 병합 유형]* ** ** 및 이 정책을 선택할지 또는 선택하지 않으면 조직의 기본 병합 정책이 될지 여부를 선택할 수 있습니다.

>[!NOTE]
>
>편집 화면 상단에 표시되는 병합 정책 ID는 편집할 수 없습니다. 이 ID는 변경할 수 없는 읽기 전용 시스템 생성 ID입니다.

![](../images/merge-policies/edit-screen.png)

필요한 변경 사항을 적용한 후 **[!UICONTROL 저장을]** 클릭하여 업데이트된 병합 정책 정보가 표시되는 *[!UICONTROL 병합 정책]* 탭으로 돌아갑니다.

![](../images/merge-policies/edited.png)

## 데이터 거버넌스 정책 위반

병합 정책을 만들거나 업데이트할 때 병합 정책이 조직에서 정의한 데이터 사용 정책을 위반하는지 여부를 확인하는 검사가 수행됩니다. 데이터 사용 정책은 Adobe Experience Platform [!DNL Data Governance] 의 일부이며 특정 [!DNL Platform] 데이터에 대해 수행할 수 있거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다. 예를 들어 병합 정책을 사용하여 서드 파티 대상으로 활성화된 세그먼트를 만들고 조직에서 특정 데이터를 서드 파티로 내보낼 수 없도록 하는 데이터 사용 정책을 가지고 있는 경우 병합 정책을 저장하려고 하면 &quot;데이터 거버넌스 정책 위반이 감지됨&quot; 알림을 받게 됩니다.

이 알림에는 위반된 데이터 사용 정책 목록이 포함되어 있으며 목록에서 정책을 선택하여 위반 세부 사항을 볼 수 있습니다. 위반된 정책을 선택할 때 *데이터 연결* 탭은 위반의 *원인* 및 영향을 받는 *활동*&#x200B;을 제공하며, 각 탭에서는 데이터 사용 정책 위반 방법에 대한 자세한 내용을 제공합니다.

Adobe Experience Platform 내에서 데이터 거버넌스 수행 방법에 대한 자세한 내용은 [데이터 거버넌스 개요를 읽어 보시기 바랍니다](../../data-governance/home.md).

![](../images/merge-policies/policy-violation.png)

## 다음 단계

이제 IMS 조직에 대한 병합 정책을 만들고 구성했으므로 프로필 데이터에서 대상 세그먼트를 만들 수 있습니다. 세그먼트를 [만들고 사용하는 방법에 대한 자세한 내용은 세그멘테이션 개요를](../../segmentation/home.md) 참조하십시오 [!DNL Experience Platform].