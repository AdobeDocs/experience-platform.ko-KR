---
title: 스키마에 대한 데이터 사용 레이블 관리
description: Adobe Experience Platform UI에서 XDM(Experience Data Model) 스키마 필드에 데이터 사용 레이블을 추가하는 방법을 알아봅니다.
exl-id: 92284bf7-f034-46cc-b905-bdfb9fcd608a
source-git-commit: 27842e7e07b6fc5884587fb75cc89bcfb4320938
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 7%

---

# 스키마에 대한 데이터 사용 레이블 관리

>[!IMPORTANT]
>
>스키마 기반 레이블 지정은 [속성 기반 액세스 제어](../../access-control/abac/overview.md): 현재 미국 기반 의료 서비스 고객을 위해 제한된 릴리스에서 사용할 수 있습니다. 이 기능은 완전히 출시되면 모든 Adobe Real-time Customer Data Platform 고객이 사용할 수 있습니다.

Adobe Experience Platform으로 가져오는 모든 데이터는 XDM(Experience Data Model) 스키마의 제한을 받습니다. 이 데이터에는 조직 규정이나 법적 규정에 따른 사용 제한이 적용될 수 있습니다. 이 문제를 해결하기 위해 플랫폼에서 을(를) 사용하여 특정 데이터 세트 및 필드의 사용을 제한할 수 있습니다. [데이터 사용 레이블](../../data-governance/labels/overview.md).

스키마 필드에 적용되는 레이블은 해당 특정 필드에 포함된 데이터에 적용되는 사용 정책을 나타냅니다.

레이블은 개별 스키마 및 해당 스키마 내의 필드에 적용되는 데 적용할 수 있습니다. 레이블이 스키마에 직접 적용되면 해당 레이블은 해당 스키마를 기반으로 하는 모든 기존 및 향후 데이터 세트에 전파됩니다.

또한 한 스키마에 추가하는 필드 레이블은 공유 클래스 또는 필드 그룹의 동일한 필드를 사용하는 다른 모든 스키마로 전파됩니다. 이렇게 하면 유사한 필드에 대한 사용 규칙이 전체 데이터 모델에서 일관되도록 할 수 있습니다.

이 자습서에서는 Platform UI에서 스키마 편집기를 사용하여 스키마에 레이블을 추가하는 단계를 다룹니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM) System]](../home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 편집기](../ui/overview.md): Platform UI에서 스키마 및 기타 리소스를 만들고 관리하는 방법을 알아봅니다.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): 레이블이 지정된 데이터에 대해 수행할 수 있는(또는 수행할 수 없는) 마케팅 작업을 정의하는 정책을 사용하여 플랫폼 작업에 대한 데이터 사용 제한을 적용하기 위한 인프라를 제공합니다.

## 레이블을 추가할 스키마 또는 필드 선택 {#select-schema-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_editgovernancelabels"
>title="거버넌스 레이블 편집"
>abstract="레이블을 스키마 필드에 적용하여 해당 특정 필드에 포함된 데이터에 적용되는 사용 정책을 표시합니다."

>[!CONTEXTUALHELP]
>id="platform_schemas_labelusageacknowledgement"
>title="레이블 사용"
>abstract="이 객체의 레이블을 편집하기 전에 다음 다운스트림 효과를 기록해 두십시오.<br>거버넌스 정책: 레이블을 사용하여 데이터를 다운스트림 대상으로 활성화할 수 있는지 여부를 관리합니다. 잘못된 레이블 사용으로 인해 다운스트림에서 데이터에 액세스할 수 없습니다.<br>동의 정책: 세그먼트에 프로필을 포함할 때 레이블을 사용하여 고객 동의 및 환경 설정을 적용합니다. 잘못된 레이블 사용으로 인해 다운스트림에서 데이터에 액세스할 수 없습니다.<br>액세스 정책: 속성 기반 액세스 컨트롤은 레이블을 사용하여 특정 자산에 액세스할 수 있는 사용자 역할을 결정합니다. 의도하지 않은 레이블 사용으로 인해 조직의 일부 직원이 이전에 액세스한 자산을 사용하지 못할 수 있습니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/overview.html?lang=ko" text="속성 기반 액세스 제어 개요"

레이블 추가를 시작하려면 먼저 다음을 수행해야 합니다 [편집할 기존 스키마 선택](../ui/resources/schemas.md#edit) 또는 [새 스키마 만들기](../ui/resources/schemas.md#create) 스키마 편집기에서 구조를 확인합니다.

개별 필드의 레이블을 편집하려면 캔버스에서 필드를 선택한 다음 를 선택할 수 있습니다 **[!UICONTROL 액세스 관리]** 오른쪽 레일에서.

>[!IMPORTANT]
>
>모든 스키마에 최대 300개의 레이블을 적용할 수 있습니다.

![스키마 편집기 캔버스에서 필드 선택](../images/tutorials/labels/manage-access.png)

다음을 선택할 수도 있습니다. **[!UICONTROL 레이블]** 탭을 클릭하고 목록에서 원하는 필드를 선택한 다음 를 선택합니다. **[!UICONTROL 액세스 및 데이터 거버넌스 레이블 적용]** 오른쪽 레일에서.

![다음에서 필드 선택 [!UICONTROL 레이블] 탭](../images/tutorials/labels/select-field-on-labels-tab.png)

전체 스키마에 대한 레이블을 편집하려면 **[!UICONTROL 레이블]** 탭에서 필터 아이콘 아래의 확인란을 선택합니다. 스키마에서 사용 가능한 모든 필드를 선택합니다. 그런 다음 을 선택합니다. **[!UICONTROL 액세스 및 데이터 거버넌스 레이블 적용]** 오른쪽 레일에서.

![에서 스키마 이름 선택 [!UICONTROL 레이블] 탭](../images/tutorials/labels/select-schema-on-labels-tab.png)

>[!NOTE]
>
>스키마 또는 필드에 대한 레이블을 처음 편집할 때 조직의 정책에 따라 레이블 사용이 다운스트림 작업에 미치는 영향을 설명하는 면책조항 메시지가 나타납니다. 선택 **[!UICONTROL 진행]** 을 눌러 편집을 계속합니다.
>
>![레이블 사용 면책조항](../images/tutorials/labels/disclaimer.png)

## 스키마 또는 필드의 레이블 편집 {#edit-labels}

선택한 필드의 레이블을 편집할 수 있는 대화 상자가 나타납니다. 개별 객체 유형 필드를 선택한 경우 오른쪽 레일에 적용된 레이블이 전파될 하위 필드가 나열됩니다.

![선택한 필드가 강조 표시된 액세스 및 데이터 거버넌스 레이블 적용 대화 상자](../images/tutorials/labels/edit-labels.png)

>[!NOTE]
>
>전체 스키마에 대한 필드를 편집하는 경우 오른쪽 레일에 해당 필드가 나열되지 않고 대신 스키마 이름이 표시됩니다.

표시된 목록을 사용하여 스키마나 필드에 추가할 레이블을 선택합니다. 레이블을 선택하면 **[!UICONTROL 적용된 레이블]** 지금까지 선택한 레이블을 표시하는 섹션이 업데이트되었습니다.

![적용된 레이블이 강조 표시된 액세스 및 데이터 거버넌스 레이블 적용 대화 상자](../images/tutorials/labels/applied-labels.png)

표시된 레이블을 유형별로 필터링하려면 왼쪽 레일에서 원하는 카테고리를 선택합니다. 새 사용자 지정 레이블을 만들려면 **[!UICONTROL 레이블 만들기]**.

![레이블 유형 필터가 적용된 액세스 및 데이터 거버넌스 레이블 적용 대화 상자와 레이블 만들기 가 강조 표시됩니다.](../images/tutorials/labels/filter-and-create-custom.png)

선택한 레이블이 만족스러우면 다음을 선택합니다. **[!UICONTROL 저장]** 필드 또는 스키마에 적용합니다.

![저장 이 강조 표시된 액세스 및 데이터 거버넌스 레이블 적용 대화 상자](../images/tutorials/labels/save-labels.png)

다음 **[!UICONTROL 레이블]** 스키마에 적용된 레이블을 표시하는 탭이 다시 나타납니다.

![적용된 필드 레이블이 강조 표시된 스키마 작업 영역의 레이블 탭](../images/tutorials/labels/field-labels-added.png)

## 다음 단계

이 안내서에서는 스키마 및 필드에 대한 데이터 사용 레이블을 관리하는 방법을 다룹니다. 스키마 수준이 아닌 특정 데이터 세트에 추가하는 방법을 포함하여 데이터 사용 레이블 관리에 대한 자세한 내용은 [데이터 사용 레이블 UI 안내서](../../data-governance/labels/user-guide.md).
