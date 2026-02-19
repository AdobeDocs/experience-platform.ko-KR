---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 액세스 제어 정책 관리
description: Adobe Experience Cloud의 권한 인터페이스를 통해 액세스 제어 정책을 관리합니다.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: b0094920720c54990953f79de32ab95c2a5c7e1c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# 액세스 제어 정책 관리

액세스 제어 정책은 속성을 함께 가져와서 허용 가능한 작업과 허용 불가능한 작업을 설정하는 명령문입니다. Adobe은 즉시 또는 조직에서 [labels](./labels.md){target="_blank"}을(를) 기반으로 특정 개체에 대한 액세스 제어를 시작할 준비가 되었을 때 활성화할 수 있는 기본 정책을 제공합니다. 기본 정책 **[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;은(는) 사용자가 일치하는 레이블을 가진 역할에 있지 않는 한 리소스에 적용된 레이블을 활용하여 액세스를 거부합니다.

>[!IMPORTANT]
>
>액세스 제어 정책은 Adobe Experience Platform에서 데이터가 사용되는 방식을 제어하는 데이터 사용 정책과 혼동하면 안 됩니다. 자세한 내용은 [데이터 사용 정책](../../../data-governance/policies/create.md){target="_blank"} 만들기에 대한 안내서를 참조하세요.

## 샌드박스에 대한 정책 구성 {#configure-policy}

>[!NOTE]
>
>**[!UICONTROL Default-Label-Based-Access-Control-Policy]** 정책만 현재 구성할 수 있습니다.

정책 구성을 시작하려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 &#x200B;](https://experience.adobe.com/){target="_blank"}(으)로 이동합니다. 왼쪽 패널에서 **[!UICONTROL Policies]**&#x200B;을(를) 선택합니다. 목록에서 **[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;을(를) 선택합니다.

![기존 정책 목록을 표시하는 정책 작업 영역입니다.](../../images/ui/policies/policies-home.png){zoomable="yes"}

정책의 세부 정보 작업 영역이 표시됩니다. **[!UICONTROL Sandboxes]**&#x200B;을(를) 선택합니다. 정책과 연결된 샌드박스 목록이 표시됩니다.

![연결된 샌드박스 목록을 표시하는 정책의 샌드박스 작업 영역입니다.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### 모든 샌드박스에 정책 추가 {#add-policy-to-all}

>[!IMPORTANT]
>
>기본적으로 **[!UICONTROL Auto-include]**&#x200B;이(가) 설정되어 있습니다. 즉, 현재 및 이후의 모든 샌드박스가 정책에 자동으로 추가됩니다.

향후 샌드박스가 정책에 자동으로 추가되지 않도록 하려면 **[!UICONTROL Auto-include]** 기능을 끄십시오. **기능을 끄면 정책에서 샌드박스가 제거되지** 않습니다.

![자동 포함 토글이 강조 표시되고 &quot;꺼짐&quot; 상태인 정책의 샌드박스 탭입니다.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

정책에서 **[!UICONTROL Auto-include]**&#x200B;이(가) 활성화되지 않은 경우 토글을 사용하여 다시 켤 수 있습니다. 선택 내용을 확인하는 대화 상자가 나타납니다. **[!UICONTROL Enable Auto-include]** 구성 설정을 완료하려면 **[!UICONTROL Enable]**&#x200B;을(를) 선택하십시오.

>[!NOTE]
>
>**[!UICONTROL Auto-include]**&#x200B;이(가) 해제되어 있는 동안 정책에서 제거한 모든 샌드박스가 다시 추가됩니다.

![사용 옵션이 강조 표시된 자동 포함 사용 대화 상자.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### 정책에 대한 샌드박스 수동 선택 {#manually-select-sandboxes}

정책에 샌드박스를 수동으로 추가하거나 제거하려면 **[!UICONTROL Auto-include]** 토글 **must**&#x200B;이(가) 꺼져 있습니다.

#### 샌드박스 추가

정책에 샌드박스를 추가하려면 **[!UICONTROL Add Sandboxes]**&#x200B;을(를) 선택하십시오.

![샌드박스 추가 옵션이 강조 표시된 정책 작업 영역입니다.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

**[!UICONTROL Add Sandboxes]** 대화 상자가 나타납니다. 정책에 추가할 샌드박스를 선택한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오.

![샌드박스를 선택하고 저장 옵션을 강조 표시한 샌드박스 추가 대화 상자.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>사용 가능한 모든 샌드박스가 정책에 이미 추가된 경우 대화 상자 내에 &quot;라이브러리에 아무 것도 없습니다.&quot;라는 메시지가 표시됩니다.

#### 샌드박스 제거

정책에서 샌드박스를 제거하려면 목록에서 제거할 샌드박스를 찾은 다음 **X** 아이콘을 선택하십시오.

![샌드박스를 제거하기 위해 &quot;x&quot;가 강조 표시된 정책의 샌드박스 목록입니다.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

확인 대화 상자가 나타납니다. 정책에서 샌드박스 제거를 완료하려면 **[!UICONTROL Confirm]**&#x200B;을(를) 선택하십시오.

![확인 옵션이 강조 표시된 샌드박스의 확인 대화 상자입니다.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## 정책 활성화 {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="정책이란 무엇입니까?"
>abstract="정책은 속성을 함께 가져와서 허용되는 작업과 허용되지 않는 작업을 설정하는 문입니다. 모든 조직에는 레이블을 기반으로 특정 오브젝트에 대한 액세스를 제어하기 위해 활성화해야 하는 기본 정책이 있습니다. 리소스에 적용된 레이블은 사용자에게 레이블에 해당하는 역할이 할당된 경우가 아니라면 액세스를 거부합니다. 정책은 편집하거나 삭제할 수 없지만 활성화하거나 비활성화할 수 있습니다."
>additional-url="https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/abac/permissions-ui/labels" text="레이블 관리"

기존 정책을 활성화하려면 **[!UICONTROL Policies]**&#x200B;의 **[!UICONTROL Permissions]** 탭에서 정책을 선택합니다. 정책의 활성화 상태가 **[!UICONTROL Status]** 섹션에 표시됩니다.

![정책의 상태가 강조 표시된 정책 작업 영역입니다.](../../images/ui/policies/policy-status.png){zoomable="yes"}

정책의 세부 정보 작업 영역이 표시됩니다. **[!UICONTROL Activate]**&#x200B;를 선택합니다.

![활성화 옵션이 강조 표시된 정책의 세부 작업 영역입니다.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

**[!UICONTROL Activate Policy]** 대화 상자가 나타납니다. **[!UICONTROL Confirm]**&#x200B;을(를) 선택하여 정책 활성화를 완료합니다.

![확인 옵션이 강조 표시된 정책 활성화 대화 상자입니다.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## 다음 단계

정책이 활성화되면 [역할에 대한 권한을 관리](permissions.md)하기 위한 다음 단계로 진행할 수 있습니다.

<!--Policies are applied at the sandbox level to control which sandboxes enforce label-based access control. By default, the **[!UICONTROL Auto-include]** feature is turned on, which means all current and future sandboxes are automatically added to the policy. When **[!UICONTROL Auto-include]** is turned off, only the sandboxes you manually add will be subject to the policy's access control rules.

To begin configuring a policy's sandboxes, navigate to **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Select **[!UICONTROL Policies]** from the left panel, then select the **[!UICONTROL Default-Label-Based-Access-Control-Policy]** from the list.

The policy's details workspace appears. Select the **[!UICONTROL Sandboxes]** tab to view the list of sandboxes associated with the policy and access the sandbox configuration options.

### Manage Auto-include {#manage-auto-include}

To control which sandboxes are included in a policy, you can toggle the **[!UICONTROL Auto-include]** feature on or off. When you toggle off **[!UICONTROL Auto-include]**, future sandboxes will not be automatically added to the policy. However, toggling off the feature **will not** remove any sandboxes that are already included in the policy.

To re-enable **[!UICONTROL Auto-include]**, use the toggle to turn it back on. The **[!UICONTROL Enable Auto-include]** dialog appears prompting you to confirm your selection. Select **[!UICONTROL Enable]** to complete the configuration setting.

>[!NOTE]
>
>When you re-enable **[!UICONTROL Auto-include]**, any sandboxes you previously removed from the policy will be re-added.

### Manually manage sandboxes {#manually-manage-sandboxes}

When **[!UICONTROL Auto-include]**is turned off, you can manually add or remove specific sandboxes from the policy. This gives you precise control over which sandboxes enforce the policy's access control rules.

>[!NOTE]
>
>To manually add or remove sandboxes, the **[!UICONTROL Auto-include]** toggle **must** be off.

**To add sandboxes:**

Select **[!UICONTROL Add Sandboxes]** from the policy's sandbox workspace.

The **[!UICONTROL Add Sandboxes]** dialog appears, displaying your library of available sandboxes. Select the sandbox(es) you wish to add to the policy and then select **[!UICONTROL Save]**.

>[!NOTE]
>
>If all available sandboxes are already included in the policy, you will see a "You have nothing in your library" message within the dialog.

**To remove sandboxes:**

Find the sandbox you wish to remove from the list and select the **X** icon next to its name.

A confirmation dialog will appear. Select **[!UICONTROL Confirm]** to finish removing the sandbox from the policy.

-->