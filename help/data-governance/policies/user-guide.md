---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 정책 사용 안내서
solution: Experience Platform
title: UI에서 데이터 사용 정책 관리
topic-legacy: policies
description: Adobe Experience Platform 데이터 거버넌스는 데이터 사용 정책을 만들고 관리할 수 있는 사용자 인터페이스를 제공합니다. 이 문서에서는 Experience Platform 사용자 인터페이스의 정책 작업 공간에서 수행할 수 있는 작업에 대한 개요를 제공합니다.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# UI에서 데이터 사용 정책 관리

Adobe Experience Platform [!DNL Data Governance]은 데이터 사용 정책을 만들고 관리할 수 있는 사용자 인터페이스를 제공합니다. 이 문서에서는 [!DNL Experience Platform] 사용자 인터페이스의 **정책** 작업 영역에서 수행할 수 있는 작업에 대한 개요를 제공합니다.

>[!IMPORTANT]
>
>모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화됩니다. 개별 정책을 적용하려면 해당 정책을 수동으로 활성화해야 합니다. UI에서 이 작업을 수행하는 방법에 대한 자세한 내용은 [정책 활성화](#enable)의 섹션을 참조하십시오.

## 전제 조건

이 안내서에서는 다음 [!DNL Experience Platform] 개념에 대해 작업해야 합니다.

- [[!DNL Data Governance]](../home.md)
- [데이터 사용 정책](./overview.md)

## 기존 정책 보기 {#view-policies}

[!DNL Experience Platform] UI에서 **[!UICONTROL Policies]**&#x200B;을 선택하여 **[!UICONTROL Policies]** 작업 영역을 엽니다. **[!UICONTROL Browse]** 탭에서 관련 레이블, 마케팅 작업 및 상태를 포함한 사용 가능한 정책 목록을 볼 수 있습니다.

![](../images/policies/browse-policies.png)

설명 및 유형을 보려면 나열된 정책을 선택합니다. 사용자 지정 정책을 선택한 경우 정책](#enable)을(를) 편집, 삭제 또는 [활성화/비활성화하기 위한 추가 컨트롤이 표시됩니다.

![](../images/policies/policy-details.png)

## 사용자 지정 정책 {#create-policy} 만들기

새 사용자 지정 데이터 사용 정책을 만들려면 **[!UICONTROL Policies]** 작업 영역의 **[!UICONTROL Browse]** 탭 오른쪽 위 모서리에서 **[!UICONTROL Create policy]**&#x200B;을 선택합니다.

![](../images/policies/create-policy-button.png)

**[!UICONTROL Create policy]** 작업 과정이 나타납니다. 새 정책에 대한 이름과 설명을 입력하여 시작합니다.

![](../images/policies/create-policy-description.png)

그런 다음 정책이 기반으로 할 데이터 사용 레이블을 선택합니다. 여러 레이블을 선택할 때 정책이 적용되려면 데이터가 모든 레이블을 포함해야 하는지 아니면 그 중 하나만 포함해야 하는지 선택할 수 있습니다. 완료되면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![](../images/policies/add-labels.png)

**[!UICONTROL Select marketing actions]** 단계가 나타납니다. 제공된 목록에서 적절한 마케팅 작업을 선택한 다음 계속하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

>[!NOTE]
>
>여러 마케팅 작업을 선택할 때 정책은 이를 &quot;OR&quot; 규칙으로 해석합니다. 즉, 선택한 마케팅 작업의 **임의의**&#x200B;이(가) 수행된 경우 정책이 적용됩니다.

![](../images/policies/add-marketing-actions.png)

**[!UICONTROL Review]** 단계가 나타나 새 정책을 만들기 전에 세부 사항을 검토할 수 있습니다. 만족스러우면 **[!UICONTROL Finish]**&#x200B;을 선택하여 정책을 만듭니다.

![](../images/policies/policy-review.png)

**[!UICONTROL Browse]** 탭이 다시 나타납니다. 이 탭에는 새로 만든 정책이 &quot;초안&quot; 상태로 나열됩니다. 정책을 활성화하려면 다음 섹션을 참조하십시오.

![](../images/policies/created-policy.png)

## 정책 {#enable} 활성화 또는 비활성화

모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화됩니다. 개별 정책을 적용하려면 API 또는 UI를 통해 해당 정책을 수동으로 활성화해야 합니다.

**[!UICONTROL Policies]** 작업 영역의 **[!UICONTROL Browse]** 탭에서 정책을 활성화하거나 비활성화할 수 있습니다. 목록에서 사용자 지정 정책을 선택하여 오른쪽에 해당 세부 사항을 표시합니다. **[!UICONTROL Status]**&#x200B;에서 전환 버튼을 선택하여 정책을 활성화하거나 비활성화합니다.

![](../images/policies/enable-policy.png)

## 마케팅 작업 보기 {#view-marketing-actions}

**[!UICONTROL Policies]** 작업 영역에서 **[!UICONTROL Marketing actions]** 탭을 선택하여 Adobe 및 자체 조직에 의해 정의된 사용 가능한 마케팅 작업 목록을 봅니다.

![](../images/policies/marketing-actions.png)

## 마케팅 작업 {#create-marketing-action} 만들기

새 사용자 지정 마케팅 작업을 만들려면 **[!UICONTROL Policies]** 작업 영역의 **[!UICONTROL Marketing actions]** 탭의 오른쪽 위 모서리에서 **[!UICONTROL Create marketing action]**&#x200B;을(를) 선택합니다.

![](../images/policies/create-marketing-action.png)

**[!UICONTROL Create marketing action]** 대화 상자가 나타납니다. 마케팅 작업의 이름과 설명을 입력한 다음 **[!UICONTROL Create]**&#x200B;을 선택합니다.

![](../images/policies/create-marketing-action-details.png)

새로 만든 작업이 **[!UICONTROL Marketing actions]** 탭에 표시됩니다. 이제 [새 데이터 사용 정책](#create-policy)을 만들 때 마케팅 작업을 사용할 수 있습니다.

![](../images/policies/created-marketing-action.png)

## 마케팅 작업 {#edit-delete-marketing-action} 편집 또는 삭제

>[!NOTE]
>
>조직에서 정의한 사용자 지정 마케팅 작업만 편집할 수 있습니다. Adobe에서 정의한 마케팅 작업은 변경하거나 삭제할 수 없습니다.

**[!UICONTROL Policies]** 작업 영역에서 **[!UICONTROL Marketing actions]** 탭을 선택하여 Adobe 및 자체 조직에 의해 정의된 사용 가능한 마케팅 작업 목록을 봅니다. 목록에서 사용자 지정 마케팅 작업을 선택한 다음 오른쪽 섹션에 제공된 필드를 사용하여 마케팅 작업의 세부 사항을 편집합니다.

![](../images/policies/edit-marketing-action.png)

기존 사용 정책에서 마케팅 작업을 사용하지 않는 경우 **[!UICONTROL Delete marketing action]**&#x200B;을 선택하여 삭제할 수 있습니다.

>[!NOTE]
>
>기존 정책에서 사용 중인 마케팅 작업을 삭제하려고 하면 삭제 시도가 실패했음을 나타내는 오류 메시지가 표시됩니다.

![](../images/policies/delete-marketing-action.png)

## 다음 단계

이 문서에서는 [!DNL Experience Platform] UI에서 데이터 사용 정책을 관리하는 방법에 대한 개요를 제공합니다. [!DNL Policy Service API]을(를) 사용하여 정책을 관리하는 방법에 대한 단계는 [개발자 안내서](../api/getting-started.md)를 참조하십시오. 데이터 사용 정책을 적용하는 방법에 대한 자세한 내용은 [정책 적용 개요](../enforcement/overview.md)를 참조하십시오.

다음 비디오는 [!DNL Experience Platform] UI에서 사용 정책을 사용하는 방법에 대한 데모를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
