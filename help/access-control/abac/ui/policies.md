---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 액세스 제어 정책 관리
description: Adobe Experience Cloud의 권한 인터페이스를 통해 액세스 제어 정책을 관리합니다.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 8%

---

# 액세스 제어 정책 관리

액세스 제어 정책은 속성을 함께 가져와서 허용 가능한 작업과 허용 불가능한 작업을 설정하는 명령문입니다. Adobe은 즉시 또는 조직에서 [labels](./labels.md){target="_blank"}을(를) 기반으로 특정 개체에 대한 액세스 제어를 시작할 준비가 되었을 때 활성화할 수 있는 기본 정책을 제공합니다. 기본 정책 **[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;은(는) 사용자가 일치하는 레이블을 가진 역할에 있지 않는 한 리소스에 적용된 레이블을 활용하여 액세스를 거부합니다.

>[!IMPORTANT]
>
>액세스 제어 정책은 Adobe Experience Platform에서 데이터가 사용되는 방식을 제어하는 데이터 사용 정책과 혼동하면 안 됩니다. 자세한 내용은 [데이터 사용 정책](../../../data-governance/policies/create.md){target="_blank"} 만들기에 대한 안내서를 참조하세요.

## 정책에 대한 샌드박스 구성 {#configure-policy}

정책은 레이블 기반 액세스 제어를 적용하는 샌드박스를 제어하기 위해 샌드박스 수준에서 적용됩니다. 기본적으로 **[!UICONTROL Auto-include]** 기능이 설정되어 있습니다. 즉, 현재 및 이후의 모든 샌드박스가 정책에 자동으로 추가됩니다. **[!UICONTROL Auto-include]**&#x200B;이(가) 꺼져 있으면 수동으로 추가하는 샌드박스만 정책의 액세스 제어 규칙을 따릅니다.

>[!NOTE]
>
>**[!UICONTROL Default-Label-Based-Access-Control-Policy]** 정책만 현재 구성할 수 있습니다.

정책의 샌드박스 구성을 시작하려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[에서 ](https://experience.adobe.com/){target="_blank"}(으)로 이동합니다. 왼쪽 패널에서 **[!UICONTROL Policies]**&#x200B;을(를) 선택한 다음 목록에서 **[!UICONTROL Default-Label-Based-Access-Control-Policy]**&#x200B;을(를) 선택합니다.

![기존 정책 목록을 표시하는 정책 작업 영역입니다.](../../images/ui/policies/policies-home.png){zoomable="yes"}

정책의 세부 정보 작업 영역이 나타납니다. 정책과 연결된 샌드박스 목록을 보고 샌드박스 구성 옵션에 액세스하려면 **[!UICONTROL Sandboxes]** 탭을 선택하십시오.

![연결된 샌드박스 목록을 표시하는 정책의 샌드박스 작업 영역입니다.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### 자동 포함 관리 {#manage-auto-include}

>[!IMPORTANT]
>
>기본적으로 **[!UICONTROL Auto-include]**&#x200B;이(가) 설정되어 있습니다. 즉, 현재 및 이후의 모든 샌드박스가 정책에 자동으로 추가됩니다.

정책에 포함된 샌드박스를 제어하려면 **[!UICONTROL Auto-include]** 기능을 켜거나 끌 수 있습니다. **[!UICONTROL Auto-include]**&#x200B;을(를) 끄면 향후 샌드박스가 정책에 자동으로 추가되지 않습니다. 그러나 기능 **을(를) 끄면 정책에 이미 포함된 샌드박스가 제거되지 않습니다**.

![자동 포함 토글이 강조 표시되고 &quot;꺼짐&quot; 상태인 정책의 샌드박스 탭입니다.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

**[!UICONTROL Auto-include]**&#x200B;을(를) 다시 사용하도록 설정하려면 토글을 사용하여 다시 켜세요. 선택 내용을 확인하는 대화 상자가 나타납니다. **[!UICONTROL Enable Auto-include]** 구성 설정을 완료하려면 **[!UICONTROL Enable]**&#x200B;을(를) 선택하십시오.

>[!NOTE]
>
>**[!UICONTROL Auto-include]**&#x200B;을(를) 다시 사용하면 이전에 정책에서 제거한 모든 샌드박스가 다시 추가됩니다.

![사용 옵션이 강조 표시된 자동 포함 사용 대화 상자.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### 샌드박스 수동 관리 {#manually-manage-sandboxes}

**[!UICONTROL Auto-include]**이(가) 꺼져 있으면 정책에서 특정 샌드박스를 수동으로 추가하거나 제거할 수 있습니다. 이렇게 하면 정책의 액세스 제어 규칙을 적용하는 샌드박스를 정확하게 제어할 수 있습니다.

>[!NOTE]
>
>샌드박스를 수동으로 추가하거나 제거하려면 **[!UICONTROL Auto-include]** 토글 **must**&#x200B;이(가) 꺼져 있습니다.

**샌드박스를 추가하려면:**

정책의 샌드박스 작업 영역에서 **[!UICONTROL Add Sandboxes]**&#x200B;을(를) 선택합니다.

![샌드박스 추가 옵션이 강조 표시된 정책 작업 영역입니다.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

사용 가능한 샌드박스 라이브러리를 표시하는 **[!UICONTROL Add Sandboxes]** 대화 상자가 나타납니다. 정책에 추가할 샌드박스를 선택한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오.

![샌드박스를 선택하고 저장 옵션을 강조 표시한 샌드박스 추가 대화 상자.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>사용 가능한 모든 샌드박스가 정책에 이미 포함되어 있는 경우 대화 상자 내에 &quot;라이브러리에 아무 것도 없습니다.&quot;라는 메시지가 표시됩니다.

**샌드박스를 제거하려면:**

목록에서 제거할 샌드박스를 찾은 다음 이름 옆에 있는 **X** 아이콘을 선택합니다.

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
