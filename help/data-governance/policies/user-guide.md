---
keywords: Experience Platform;home;popular topics;data governance;data usage policy user guide
solution: Experience Platform
title: 데이터 사용 정책 사용 안내서
topic: policies
description: Adobe Experience Platform 데이터 거버넌스는 데이터 사용 정책을 만들고 관리할 수 있는 사용자 인터페이스를 제공합니다. 이 문서에서는 Experience Platform 사용자 인터페이스의 정책 작업 영역에서 수행할 수 있는 작업에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# 데이터 사용 정책 사용 안내서

Adobe Experience Platform [!DNL Data Governance] 는 데이터 사용 정책을 만들고 관리할 수 있는 사용자 인터페이스를 제공합니다. 이 문서에서는 **사용자 인터페이스의 정책 작업 공간에서 수행할 수 있는 작업에** 대한 개요를 제공합니다 [!DNL Experience Platform] .

>[!IMPORTANT]
>
>모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화됩니다. 개별 정책이 적용을 위해 고려되려면 해당 정책을 수동으로 활성화해야 합니다. UI에서 [이 작업을 수행하는 방법에 대한 단계는 정책](#enable) 활성화에 대한 섹션을 참조하십시오.

## 전제 조건

이 안내서에서는 다음 [!DNL Experience Platform] 개념을 제대로 이해해야 합니다.

- [[!DNL Data Governance]](../home.md)
- [데이터 사용 정책](./overview.md)

## 데이터 사용 정책 보기 {#view-policies}

UI [!DNL Experience Platform] 에서 정책 **** 을 클릭하여 **[!UICONTROL 정책 작업 영역을]** 엽니다. 검색 **** 탭에서 관련 레이블, 마케팅 작업 및 상태를 비롯한 사용 가능한 정책 목록을 볼 수 있습니다.

![](../images/policies/browse-policies.png)

나열된 정책을 클릭하여 설명과 유형을 확인합니다. 사용자 지정 정책을 선택하면 정책을 편집, 삭제 또는 [활성화/비활성화하기 위한 추가 컨트롤이 표시됩니다](#enable).

![](../images/policies/policy-details.png)

## 사용자 지정 데이터 사용 정책 만들기 {#create-policy}

새 사용자 지정 데이터 사용 정책을 만들려면 **[!UICONTROL 정책]** 작업 영역의 **[!UICONTROL 찾아보기]** 탭 오른쪽 상단에서 정책 **[!UICONTROL 만들기를]** 클릭합니다.

![](../images/policies/create-policy-button.png)

정책 **[!UICONTROL 만들기]** 워크플로우가 나타납니다. 먼저 새 정책에 대한 이름과 설명을 입력합니다.

![](../images/policies/create-policy-description.png)

다음으로, 정책이 기반으로 할 데이터 사용 레이블을 선택합니다. 여러 레이블을 선택할 때 정책이 적용되도록 데이터가 모든 레이블을 포함해야 하는지 아니면 그 중 하나만 포함해야 하는지 선택할 수 있습니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을 클릭합니다.

![](../images/policies/add-labels.png)

마케팅 **[!UICONTROL 작업]** 선택 단계가 나타납니다. 제공된 목록에서 적절한 마케팅 작업을 선택한 다음 **[!UICONTROL 다음을]** 클릭하여 계속합니다.

>[!NOTE]
>
>여러 마케팅 작업을 선택할 때 정책은 이를 &quot;OR&quot; 규칙으로 해석합니다. 즉, 선택한 마케팅 작업 중 **하나라도** 수행된 경우 정책이 적용됩니다.

![](../images/policies/add-marketing-actions.png)

검토 **** 단계가 표시되어 새 정책을 만들기 전에 세부 사항을 검토할 수 있습니다. 만족하면 **[!UICONTROL 마침을]** 클릭하여 정책을 만듭니다.

![](../images/policies/policy-review.png)

이제 **[!UICONTROL 검색]** 탭이 다시 나타나며 새로 만든 정책이 &quot;초안&quot; 상태로 나열됩니다. 정책을 활성화하려면 다음 섹션을 참조하십시오.

![](../images/policies/created-policy.png)

## 데이터 사용 정책 활성화 또는 비활성화 {#enable}

모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화됩니다. 개별 정책이 적용을 위해 고려되도록 하려면 API 또는 UI를 통해 해당 정책을 수동으로 활성화해야 합니다.

정책 작업 영역의 **[!UICONTROL 찾아보기]** 탭에서 정책을 **[!UICONTROL 활성화하거나 비활성화할]** 수 있습니다. 목록에서 사용자 지정 정책을 선택하여 오른쪽에 세부 사항을 표시합니다. 상태 **[!UICONTROL 에서]**&#x200B;전환 단추를 선택하여 정책을 활성화하거나 비활성화합니다.

![](../images/policies/enable-policy.png)

## 마케팅 작업 보기 {#view-marketing-actions}

정책 **[!UICONTROL 작업]** 공간에서 **[!UICONTROL 마케팅 작업]** 탭을 선택하여 Adobe과 자체 조직에서 정의한 사용 가능한 마케팅 작업 목록을 봅니다.

![](../images/policies/marketing-actions.png)

## 마케팅 작업 만들기 {#create-marketing-action}

새 사용자 지정 마케팅 작업을 만들려면 **[!UICONTROL 정책 작업]** 작업 **[!UICONTROL 영역의]** 마케팅 작업 **[!UICONTROL 탭 오른쪽 상단에서 마케팅 작업]** 만들기를클릭합니다.

![](../images/policies/create-marketing-action.png)

마케팅 **[!UICONTROL 작업]** 만들기 대화 상자가 나타납니다. 마케팅 작업의 이름과 설명을 입력한 다음 만들기를 **[!UICONTROL 클릭합니다]**.

![](../images/policies/create-marketing-action-details.png)

새로 만든 작업이 **[!UICONTROL 마케팅 작업]** 탭에 나타납니다. 이제 새 데이터 사용 정책을 [만들 때 마케팅 작업을 사용할 수 있습니다](#create-policy).

![](../images/policies/created-marketing-action.png)

## 마케팅 작업 편집 또는 삭제 {#edit-delete-marketing-action}

>[!NOTE]
>
>조직에서 정의한 사용자 지정 마케팅 작업만 편집할 수 있습니다. Adobe에서 정의한 마케팅 작업은 변경하거나 삭제할 수 없습니다.

정책 **[!UICONTROL 작업]** 공간에서 **[!UICONTROL 마케팅 작업]** 탭을 선택하여 Adobe과 자체 조직에서 정의한 사용 가능한 마케팅 작업 목록을 봅니다. 목록에서 사용자 지정 마케팅 작업을 선택한 다음 오른쪽 섹션에 있는 제공된 필드를 사용하여 마케팅 활동의 세부 사항을 편집합니다.

![](../images/policies/edit-marketing-action.png)

기존 사용 정책에서 마케팅 작업을 사용하지 않는 경우 마케팅 작업 **[!UICONTROL 삭제를 클릭하여 삭제할 수 있습니다]**.

>[!NOTE]
>
>기존 정책에 사용되는 마케팅 작업을 삭제하려고 하면 삭제 시도가 실패했음을 나타내는 오류 메시지가 표시됩니다.

![](../images/policies/delete-marketing-action.png)

## 다음 단계

이 문서에서는 [!DNL Experience Platform] UI에서 데이터 사용 정책을 관리하는 방법에 대한 개요를 제공합니다. 를 사용하여 정책을 관리하는 방법에 대한 단계 [!DNL Policy Service API]는 [개발자 안내서를 참조하십시오](../api/getting-started.md). 데이터 사용 정책을 적용하는 방법에 대한 자세한 내용은 [정책 실행 개요를 참조하십시오](../enforcement/overview.md).

다음 비디오에서는 [!DNL Experience Platform] UI에서 사용 정책을 사용하는 방법에 대한 데모를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)