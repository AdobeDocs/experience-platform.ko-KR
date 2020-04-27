---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 사용 정책 사용 안내서
topic: policies
translation-type: tm+mt
source-git-commit: 235a43ad72dee45db1b3d35ae84ce9a1c4d729b8

---


# 데이터 사용 정책 사용 안내서

Adobe Experience Platform 데이터 거버넌스는 데이터 사용 정책을 만들고 관리할 수 있는 사용자 인터페이스를 제공합니다. 이 문서에서는 Experience Platform UI의 정책 _작업_ 영역에서 수행할 수 있는 작업에 대한 개요를 제공합니다.

## 전제 조건

이 가이드는 다음과 같은 경험 플랫폼 개념에 대한 작업 이해를 필요로 합니다.

- [데이터 거버넌스](../home.md)
- [데이터 사용 정책](./overview.md)

## 데이터 사용 정책 보기

Experience Platform UI에서 을 클릭하여 **[!UICONTROL Policies]** *[!UICONTROL Policies]* 작업 영역을 엽니다. 이 **[!UICONTROL Browse]** 탭에서 관련 레이블, 마케팅 작업 및 상태를 포함한 사용 가능한 정책 목록을 볼 수 있습니다.

![](../images/policies/browse-policies.png)

나열된 정책을 클릭하여 설명과 유형을 봅니다. 사용자 지정 정책을 선택한 경우 정책을 편집, 삭제 또는 [활성화/비활성화하는 추가 컨트롤이 표시됩니다](#enable).

![](../images/policies/policy-details.png)

## 사용자 지정 데이터 사용 정책 만들기

새 사용자 지정 데이터 사용 정책을 만들려면 정책 작업 **[!UICONTROL Create policy]** 영역의 오른쪽 위 모서리에서 을 *클릭합니다* .

![](../images/policies/create-policy-button.png)

워크플로우가 *[!UICONTROL Create policy]* 나타납니다. 새 정책에 대한 이름과 설명을 제공하여 시작합니다.

![](../images/policies/create-policy-description.png)

그런 다음 정책이 기반으로 하는 데이터 사용 레이블을 선택합니다. 여러 레이블을 선택할 때 정책이 적용되도록 데이터에 모든 레이블이 포함되어야 하는지 아니면 해당 레이블 중 하나만 포함해야 하는지 선택할 수 있습니다. 완료되면 **[!UICONTROL Next]**&#x200B;를 클릭합니다.

![](../images/policies/add-labels.png)

단계가 *[!UICONTROL Select marketing actions]* 나타납니다. 제공된 목록에서 적절한 마케팅 작업을 선택한 다음 을 클릭하여 **[!UICONTROL Next]** 계속합니다.

>[!NOTE] 여러 마케팅 작업을 선택할 때 정책은 이를 &quot;OR&quot; 규칙으로 해석합니다. 즉, 선택한 마케팅 작업 _중 하나라도_ 수행되는 경우 정책이 적용됩니다.

![](../images/policies/add-marketing-actions.png)

새 정책을 만들기 전에 세부 사항을 검토할 수 있는 단계가 *[!UICONTROL Review]* 나타납니다. 원하는 경우 을 클릭하여 정책을 **[!UICONTROL Finish]** 만듭니다.

![](../images/policies/policy-review.png)

이제 새로 만든 정책을 &quot;초안&quot; 상태로 표시하는 탭이 다시 나타납니다. *[!UICONTROL Browse]* 정책을 활성화하려면 다음 섹션을 참조하십시오.

![](../images/policies/created-policy.png)

## 데이터 사용 정책 활성화 또는 비활성화 {#enable}

작업 영역의 *[!UICONTROL Browse]* 탭에서 사용자 지정 데이터 사용 정책을 활성화하거나 비활성화할 수 *[!UICONTROL Policies]* 있습니다. 목록에서 사용자 지정 정책을 선택하여 오른쪽에 세부 사항을 표시합니다. 아래에서 *[!UICONTROL Status]*&#x200B;전환 단추를 선택하여 정책을 활성화하거나 비활성화합니다.

![](../images/policies/enable-policy.png)

## 다음 단계

이 문서에서는 Experience Platform UI에서 데이터 사용 정책을 관리하는 방법에 대한 개요를 제공합니다. DULE 정책 API를 사용하여 정책을 관리하는 방법에 대한 단계는 [개발자 안내서를](../api/getting-started.md)참조하십시오. 데이터 사용 정책을 적용하는 방법에 대한 자세한 내용은 [정책 적용 개요를](../enforcement/overview.md)참조하십시오.