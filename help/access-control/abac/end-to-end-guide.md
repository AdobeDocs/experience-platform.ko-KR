---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;
title: 특성 기반 액세스 제어 종단간 안내서
description: 이 문서에서는 Adobe Experience Platform의 특성 기반 액세스 제어에 대한 종단 간 안내서를 제공합니다
hide: true
hidefromtoc: true
source-git-commit: 440176ea1f21db3c7c4b3572fb52771dc70c80a0
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 0%

---

# 특성 기반 액세스 제어 종단간 안내서

속성 기반 액세스 제어는 개인 정보 보호 관련 브랜드에게 사용자 액세스를 관리할 수 있는 보다 강력한 유연성을 제공하는 Adobe Experience Platform 기능입니다. 스키마 필드 및 세그먼트와 같은 개별 객체를 사용자 역할에 할당할 수 있습니다. 이 기능을 사용하면 조직의 특정 Platform 사용자에 대한 개별 개체에 대한 액세스 권한을 부여하거나 취소할 수 있습니다.

이 기능을 사용하면 조직 또는 데이터 사용 범위를 정의하는 레이블을 사용하여 스키마 필드, 세그먼트 등을 분류할 수 있습니다. Adobe Journey Optimizer에서는 여정 및 오퍼에 동일한 레이블을 적용할 수 있습니다. 동시에 관리자는 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 해당 필드에 액세스할 수 있는 사용자 또는 그룹(내부, 외부 또는 타사 사용자)을 보다 효율적으로 관리할 수 있습니다.

## 시작하기

이 자습서에서는 다음 플랫폼 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [Adobe Experience Platform 세그멘테이션 서비스](../../segmentation/home.md): 내의 세그먼테이션 엔진 [!DNL Platform] 고객 행동 및 속성을 기반으로 고객 프로필에서 대상 세그먼트를 만드는 데 사용됩니다.

### 사용 사례 개요

이 안내서에서는 중요한 데이터에 대한 액세스를 제한하는 사용 사례를 사용하여 워크플로우를 보여줍니다. 예를 들어, 역할, 레이블 및 정책을 만들어 사용자가 조직의 특정 리소스에 액세스할 수 있는지 여부를 구성하는 속성 기반 액세스 제어 워크플로우 예를 살펴보겠습니다. 이 사용 사례는 아래에 요약되어 있습니다.

의료 제공업체로서 조직의 리소스에 대한 액세스를 구성하려고 합니다.

* 내부 마케팅 팀이 **[!UICONTROL PHI/규제 상태 데이터]** 데이터.
* 외부 에이전시에 액세스할 수 없습니다 **[!UICONTROL PHI/규제 상태 데이터]** 데이터.

이를 수행하려면 역할, 리소스 및 정책을 구성해야 합니다.

다음을 수행합니다.

* [사용자의 역할에 레이블 지정]{#label-roles}: 마케팅 그룹이 외부 에이전시와 작동하는 의료 공급자(ACME Business Group)의 예를 사용합니다.
* [리소스 레이블 지정(스키마 필드 및 세그먼트)]{#label-resources}: 을(를) 지정합니다. **[!UICONTROL PHI/규제 상태 데이터]** 스키마 리소스 및 세그먼트에 레이블을 지정합니다.
* [함께 연결할 정책을 만듭니다]{#policy}: 스키마 필드 및 세그먼트에 대한 액세스를 거부하는 역할에 따라 리소스의 레이블을 레이블에 연결하는 정책을 만듭니다. 이렇게 하면 일치하는 레이블이 없는 사용자를 위해 모든 샌드박스에서 스키마 필드 및 세그먼트에 대한 액세스를 거부합니다.

## 권한

[!UICONTROL 권한] 는 관리자가 사용자 역할 및 액세스 정책을 정의하여 제품 애플리케이션 내의 기능 및 개체에 대한 액세스 권한을 관리할 수 있는 Experience Cloud 영역입니다.

사용 [!UICONTROL 권한], 역할을 만들고 관리하며, 이러한 역할에 대해 원하는 리소스 권한을 지정할 수 있습니다. [!UICONTROL 권한] 또한 특정 역할과 연관된 레이블, 샌드박스 및 사용자를 관리할 수도 있습니다.

관리자 권한이 없는 경우 시스템 관리자에게 문의하여 액세스 권한을 얻으십시오.

관리자 권한이 있으면 다음 위치로 이동하십시오. [Adobe Experience Cloud](https://experience.adobe.com/) Adobe 자격 증명을 사용하여 로그인합니다. 로그인하면 **[!UICONTROL 개요]** 페이지에 관리자 권한이 있는 조직에 대한 페이지가 표시됩니다. 이 페이지에서는 사용자 및 관리자를 조직에 전체적으로 추가할 수 있는 다른 컨트롤과 함께 조직에서 가입한 제품을 보여줍니다. 선택 **[!UICONTROL 권한]** 을 클릭하여 플랫폼 통합을 위한 작업 공간을 엽니다.

![Adobe Experience Cloud에서 선택 중인 권한 제품을 보여주는 이미지](../images/flac-ui/flac-select-product.png)

플랫폼 UI에 대한 권한 작업 영역이 나타나고 **[!UICONTROL 역할]** 페이지.

## 역할에 레이블 적용 {#label-roles}

역할은 Platform 인스턴스와 상호 작용하고 액세스 제어 정책의 기본 구성원인 사용자 유형을 분류하는 방법입니다. 역할에는 주어진 권한 세트가 있으며 조직의 구성원은 필요한 액세스 범위에 따라 하나 이상의 역할에 할당할 수 있습니다.

시작하려면 다음을 선택합니다 **[!UICONTROL ACME 업무 그룹]** 에서 **[!UICONTROL 역할]** 페이지.

![역할에서 선택된 ACME 업무 역할을 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-select-role.png)

다음 을 선택합니다. **[!UICONTROL 레이블]** 그런 다음 **[!UICONTROL 레이블 추가]**.

![레이블 탭에서 선택 중인 레이블 추가를 표시하는 이미지](../images/abac-end-to-end-user-guide/abac-select-add-labels.png)

조직의 모든 레이블 목록이 나타납니다. 선택 **[!UICONTROL RHD]** 에 대한 레이블을 추가하려면 **[!UICONTROL PHI/규제 상태 데이터]**. 레이블 옆에 파란색 확인 표시가 나타날 때까지 잠시 기다렸다가 선택합니다 **[!UICONTROL 저장]**.

![선택 및 저장되는 RHD 레이블을 표시하는 이미지](../images/abac-end-to-end-user-guide/abac-select-role-label.png)

## 스키마 필드에 레이블 적용 {#label-resources}

이제 을(를) 사용하여 사용자 역할을 구성했으므로 [!UICONTROL RHD] 레이블에서 다음 단계는 해당 역할에 대해 제어할 리소스에 동일한 레이블을 추가하는 것입니다.

선택 **[!UICONTROL 스키마]** 왼쪽 탐색에서 를 선택하고 을 선택합니다. **[!UICONTROL ACME Healthcare]** 표시되는 스키마 목록에서 를 선택합니다.

![스키마 탭에서 선택한 ACME Healthcare 스키마를 표시하는 이미지](../images/abac-end-to-end-user-guide/abac-select-schema.png)

다음 을 선택합니다. **[!UICONTROL 레이블]** 를 클릭하여 스키마와 연결된 필드를 표시하는 목록을 확인합니다. 여기에서 한 번에 하나 이상의 필드에 레이블을 할당할 수 있습니다. 을(를) 선택합니다 **[!UICONTROL 혈당]** 및 **[!UICONTROL 인슐린 수준]** 필드를 선택한 다음 **[!UICONTROL 거버넌스 레이블 편집]**.

![선택한 혈당 및 인슐린 수준을 보여주는 이미지 및 선택한 관리 레이블을 편집합니다](../images/abac-end-to-end-user-guide/abac-select-schema-labels-tab.png)

다음 **[!UICONTROL 레이블 편집]** 스키마 필드에 적용할 레이블을 선택할 수 있는 대화 상자가 나타납니다. 이 사용 사례에서 **[!UICONTROL PHI/규제 상태 데이터]** 레이블을 지정한 다음 **[!UICONTROL 저장]**.

![선택 및 저장되는 RHD 레이블을 표시하는 이미지](../images/abac-end-to-end-user-guide/abac-select-schema-labels.png)

>[!NOTE]
>
>필드에 레이블을 추가하면 해당 레이블이 해당 필드의 상위 리소스(클래스 또는 필드 그룹)에 적용됩니다. 상위 클래스 또는 필드 그룹을 다른 스키마에서 사용하는 경우 해당 스키마는 동일한 레이블을 상속합니다.

## 세그먼트에 레이블 적용

스키마 필드에 레이블 지정을 완료한 후 이제 세그먼트 레이블 지정을 시작할 수 있습니다.

선택 **[!UICONTROL 세그먼트]** 왼쪽 탐색에서 를 클릭합니다. 조직에서 사용할 수 있는 세그먼트 목록이 표시됩니다. 이 예에서 다음 두 세그먼트에 중요한 상태 데이터가 포함되므로 레이블이 지정됩니다.

* 혈당 100 초과
* 인슐린 &lt;50

선택 **[!UICONTROL 혈당 100 초과]** 세그먼트 레이블 지정을 시작합니다.

![세그먼트 탭에서 선택한 혈당 100 이상을 표시하는 이미지](../images/abac-end-to-end-user-guide/abac-select-segment.png)

세그먼트 **[!UICONTROL 세부 사항]** 화면이 나타납니다. 선택 **[!UICONTROL 액세스 관리]**.

![액세스 관리 선택 항목을 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-segment-fields-manage-access.png)

다음 **[!UICONTROL 레이블 편집]** 세그먼트에 적용할 레이블을 선택할 수 있는 대화 상자가 나타납니다. 이 사용 사례에서 **[!UICONTROL PHI/규제 상태 데이터]** 레이블을 지정한 다음 **[!UICONTROL 저장]**.

![RHD 레이블 선택 및 선택 중인 저장을 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-select-segment-labels.png)

다음 작업을 수행하여 위의 단계를 반복합니다. **[!UICONTROL 인슐린 &lt;50]**.

## 액세스 제어 정책 만들기 {#policy}

액세스 제어 정책은 레이블을 활용하여 특정 플랫폼 리소스에 액세스할 수 있는 사용자 역할을 정의합니다. 정책은 로컬 또는 글로벌 정책일 수 있으며 다른 정책을 재정의할 수 있습니다. 이 예에서는 스키마 필드에 해당 레이블이 없는 사용자를 위해 모든 샌드박스에서 스키마 필드 및 세그먼트에 대한 액세스가 거부됩니다.

액세스 제어 정책을 만들려면 **[!UICONTROL 권한]** 왼쪽 탐색에서 를 선택하고 을 선택합니다. **[!UICONTROL 정책]**. 다음 을 선택합니다. **[!UICONTROL 정책 만들기]**.

![사용 권한에서 선택한 정책 만들기를 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-create-policy.png)

다음 **[!UICONTROL 새 정책 만들기]** 이름 및 선택적 설명을 입력하라는 대화 상자가 나타납니다. 선택 **[!UICONTROL 확인]** 완료됨.

![새 정책 만들기 대화 상자 및 확인 선택을 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-create-policy-details.png)

스키마 필드에 대한 액세스를 거부하려면 드롭다운 화살표를 사용하고 을(를) 선택합니다 **[!UICONTROL 액세스 거부]** 그런 다음 **[!UICONTROL 선택한 리소스가 없습니다.]**. 다음 을 선택합니다. **[!UICONTROL 스키마 필드]** 그런 다음 **[!UICONTROL 모두]**.

![거부 액세스 및 선택한 리소스를 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema.png)

아래 표에는 정책을 만들 때 사용할 수 있는 조건이 나와 있습니다.

| 조건 | 설명 |
| --- | --- |
| 다음은 false입니다 | &#39;액세스 거부&#39;를 설정하면 사용자가 선택한 기준을 충족하지 않으면 액세스가 제한됩니다. |
| 다음 내용이 참인 경우 | 액세스 권한 부여를 설정하면 사용자가 선택한 조건을 충족하면 액세스가 제한됩니다. |
| 임의 항목과 일치 | 사용자에게 리소스에 적용된 모든 레이블과 일치하는 레이블이 있습니다. |
| 모두 일치 | 사용자에게 리소스에 적용된 모든 레이블과 일치하는 모든 레이블이 있습니다. |
| 코어 레이블 | 코어 레이블은 모든 플랫폼 인스턴스에서 사용할 수 있는 Adobe 정의 레이블입니다. |
| 사용자 지정 레이블 | 사용자 지정 레이블은 조직에서 만든 레이블입니다. |

선택 **[!UICONTROL 다음은 false입니다]** 그런 다음 **[!UICONTROL 속성을 선택하지 않았습니다.]**. 다음으로 사용자를 선택합니다 **[!UICONTROL 코어 레이블]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 모두 일치]**. 리소스를 선택합니다 **[!UICONTROL 코어 레이블]** 마지막으로 선택 **[!UICONTROL 리소스 추가]**.

![선택 중인 조건과 선택 중인 리소스 추가 를 보여주는 이미지](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-schema-expression.png)

>[!TIP]
>
>리소스는 주체가 액세스할 수 있거나 액세스할 수 없는 자산 또는 개체입니다. 리소스는 세그먼트나 스키마일 수 있습니다.

세그먼트에 대한 액세스를 거부하려면 드롭다운 화살표를 사용하고 을 선택합니다 **[!UICONTROL 액세스 거부]** 그런 다음 **[!UICONTROL 선택한 리소스가 없습니다.]**. 다음 을 선택합니다. **[!UICONTROL 세그먼트]** 그런 다음 **[!UICONTROL 모두]**.

선택 **[!UICONTROL 다음은 false입니다]** 그런 다음 **[!UICONTROL 속성을 선택하지 않았습니다.]**. 다음으로 사용자를 선택합니다 **[!UICONTROL 코어 레이블]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 모두 일치]**. 리소스를 선택합니다 **[!UICONTROL 코어 레이블]** 마지막으로 선택 **[!UICONTROL 저장]**.

![선택한 조건을 보여주는 이미지 및 선택한 저장](../images/abac-end-to-end-user-guide/abac-create-policy-deny-access-segment.png)

선택 **[!UICONTROL 활성화]** 정책을 활성화하기 위해 활성화 여부를 확인하는 대화 상자가 나타납니다. 선택 **[!UICONTROL 확인]** 그런 다음 **[!UICONTROL 닫기]**.

![활성화 중인 정책을 보여주는 이미지 ](../images/abac-end-to-end-user-guide/abac-create-policy-activation.png)

## 다음 단계

역할, 스키마 필드 및 세그먼트에 레이블 적용을 완료했습니다. 이러한 역할에 지정된 외부 에이전시는 스키마, 데이터 세트 및 프로필 보기에서 이러한 레이블과 해당 값을 볼 수 없도록 제한됩니다. 이러한 필드는 세그먼트 빌더를 사용할 때 세그먼트 정의에서 사용할 수도 없습니다.

속성 기반 액세스 제어에 대한 자세한 내용은 [속성 기반 액세스 제어 개요](./overview.md).
