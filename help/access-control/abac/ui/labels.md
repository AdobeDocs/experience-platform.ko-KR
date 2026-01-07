---
keywords: Experience Platform;홈;자주 찾는 항목;액세스 제어;속성 기반 액세스 제어
title: 속성 기반 액세스 제어 관리 레이블
description: Adobe Experience Cloud의 권한 인터페이스를 통해 레이블을 관리합니다.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 11%

---

# 레이블 관리

레이블을 사용하여 데이터 사용 및 속성 기반 액세스 제어 정책에 따라 데이터 세트와 필드를 분류할 수 있습니다. 레이블은 언제든지 적용할 수 있으므로 데이터를 제어하는 방법을 유연하게 선택할 수 있습니다. 우수 사례는 데이터가 Adobe Experience Platform에 수집되는 즉시 또는 데이터를 사용할 수 있게 되는 즉시 데이터에 레이블을 지정하는 것을 권장합니다. 권한 UI에서 레이블을 관리하는 방법을 알아보려면 이 문서를 참조하십시오.

포괄적인 레이블 목록 및 해당 거버넌스 정책은 [핵심 데이터 사용 레이블](../../../data-governance/labels/reference.md){target="_blank"}에 대한 안내서를 참조하십시오.

>[!NOTE]
>
>지정된 레이블이 포함된 필드가 있는 [계산 특성](../../../profile/computed-attributes/overview.md){target="_blank"}을 만들거나 보려면 해당 레이블에 대한 액세스 권한이 있어야 합니다.

## 레이블 탐색 {#explore-labels}

사용 가능한 모든 레이블을 보려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 ](https://experience.adobe.com/){target="_blank"}(으)로 이동하십시오. 왼쪽 패널에서 **[!UICONTROL Labels]**&#x200B;을(를) 선택합니다.

![왼쪽 패널에서 레이블이 강조 표시된 사용 권한의 레이블 작업 영역입니다.](../../images/ui/labels/labels-home.png){zoomable="yes"}

레이블은 유형별로 분류되며 다음 범주 중 하나에 속합니다.

| 유형 | 설명 |
| --- | --- |
| [계약](../../../data-governance/labels/reference.md#contract){target="_blank"} | 이 범주는 계약 의무가 있거나 조직의 데이터 거버넌스 정책과 관련된 데이터를 분류하는 데 사용됩니다. |
| [ID](../../../data-governance/labels/reference.md#identity){target="_blank"} | 이 범주는 개인을 직접 또는 간접적으로 식별할 수 있는 데이터를 분류하는 데 사용됩니다. |
| [중요](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | 이 범주는 조직에서 중요하다고 간주하는 데이터를 분류하는 데 사용됩니다. |
| [파트너 에코시스템](../../../data-governance/labels/reference.md#partner){target="_blank"} | 이 범주는 조직 외부의 소스에서 가져온 데이터를 분류하는 데 사용됩니다. |
| 책임 있는 참여 | 이 범주에는 편의를 초래할 가능성이 있는 데이터를 반영하는 단일 레이블 **[!UICONTROL Potential for Bias]**&#x200B;이(가) 포함되어 있습니다. |
| 사용자 정의 | 이 카테고리에는 조직에서 만든 레이블이 포함됩니다. |

레이블을 필터링하려면 필터 아이콘(![필터 아이콘](/help/images/icons/filter.png))을 선택한 다음 **[!UICONTROL Type]** 드롭다운에서 원하는 레이블 유형을 선택합니다.

![필터 옵션이 확장되고 형식 드롭다운 목록이 강조 표시된 레이블 작업 영역입니다.](../../images/ui/labels/label-filter.png){zoomable="yes"}

개별 레이블을 보려면 목록에서 레이블 이름을 선택합니다. 레이블의 세부 사항 페이지가 나타납니다. Adobe의 핵심 레이블을 **편집할 수 없습니다**.

![개별 레이블의 세부 정보 페이지입니다.](../../images/ui/labels/label-details.png){zoomable="yes"}

## 사용자 지정 레이블 만들기 {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="레이블 사용"
>abstract="사용자 정의 레이블을 사용하여 데이터에 데이터 거버넌스 및 액세스 제어 구성을 적용할 수 있습니다."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="새 레이블 만들기"
>abstract="조직의 요구 사항에 맞게 고유한 사용자 정의 레이블을 만들 수 있습니다. 사용자 정의 레이블을 사용하여 데이터 거버넌스와 액세스 제어 구성을 모두 데이터에 적용할 수 있습니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html#manage-labels" text="사용자 정의 레이블 관리"

>[!NOTE]
>
>사용자 지정 레이블을 만들려면 **[!UICONTROL Manage Usage Labels]** 권한과 `Prod` 샌드박스가 포함된 역할이 필요합니다.

새 레이블을 만들려면 **[!UICONTROL Labels]** 작업 영역의 왼쪽 패널에서 **[!UICONTROL Permissions]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Create label]**&#x200B;을(를) 선택하십시오.

![레이블 만들기 옵션이 강조 표시된 레이블 작업 영역입니다.](../../images/ui/labels/create-label.png){zoomable="yes"}

**[!UICONTROL Create new label]** 대화 상자가 나타나고 **[!UICONTROL Name]**, **[!UICONTROL Friendly name]** 및 **[!UICONTROL Description]**&#x200B;을(를) 입력하라는 메시지가 표시됩니다.

>[!IMPORTANT]
>
> 레이블을 만들고 레이블 삭제가 현재 지원되지 않는 경우에는 레이블의 [!UICONTROL Name]을(를) 변경할 수 없습니다.

레이블 만들기를 완료하려면 **[!UICONTROL Confirm]**&#x200B;을(를) 선택하십시오.

![이름, 알기 쉬운 이름, 설명을 입력하고 확인 옵션이 강조 표시된 새 레이블 만들기 대화 상자.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## 사용자 지정 레이블 편집 {#edit-custom-label}

사용자 지정 레이블의 **[!UICONTROL Name]**&#x200B;을(를) 편집할 수 없지만 **[!UICONTROL Friendly name]** 및 **[!UICONTROL Description]**&#x200B;을(를) 편집할 수 있습니다. 사용자 지정 레이블을 편집하려면 **[!UICONTROL Labels]** 작업 영역의 목록에서 레이블을 선택합니다.

![레이블이 강조 표시된 레이블 작업 영역입니다.](../../images/ui/labels/select-label.png){zoomable="yes"}

두 필드 중 하나를 편집한 다음 텍스트 상자 외부의 아무 곳이나 클릭하여 변경 내용을 저장합니다. 확인 메시지가 화면에 나타나고 **[!UICONTROL Modified by]** 이름 및 **[!UICONTROL Modified]** 날짜가 변경됩니다.

![&quot;업데이트 완료&quot; 메시지가 표시된 레이블의 세부 정보 페이지입니다.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## 다음 단계

이제 레이블을 더 깊이 이해했으므로 [스키마에 적용](../../../xdm/tutorials/labels.md)을 시작할 수 있습니다.
