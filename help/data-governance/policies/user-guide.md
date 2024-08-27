---
keywords: Experience Platform;홈;인기 항목;데이터 거버넌스;데이터 사용 정책 사용 안내서
solution: Experience Platform
title: UI의 데이터 사용 정책 관리
description: Adobe Experience Platform 데이터 거버넌스는 데이터 사용 정책을 만들고 관리할 수 있는 사용자 인터페이스를 제공합니다. 이 문서에서는 Experience Platform 사용자 인터페이스의 정책 작업 영역에서 수행할 수 있는 작업에 대한 개요를 제공합니다.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 16%

---

# UI에서 데이터 사용 정책 관리 {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_description"
>title="프로필 데이터에 고객 동의 통합 및 시행"
>abstract="<h2>설명</h2><p>플랫폼을 사용하면 고객으로부터 수집한 동의 데이터를 해당 프로필에 통합할 수 있습니다. 그런 다음 동의 정책을 설정하여 특정 대상에 대해 활성화된 세그먼트에 이 데이터를 포함할 수 있는지 여부를 결정할 수 있습니다.</p>"

이 문서에서는 Adobe Experience Platform UI에서 **[!UICONTROL 정책]** 작업 영역을 사용하여 데이터 사용 정책을 만들고 관리하는 방법을 다룹니다.

>[!NOTE]
>
>UI에서 액세스 제어 정책을 관리하는 방법에 대한 자세한 내용은 대신 [특성 기반 액세스 제어 UI 안내서](../../access-control/abac/ui/policies.md)를 참조하십시오.

>[!IMPORTANT]
>
>모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화되어 있습니다. 개별 정책을 적용하여 시행하려면 해당 정책을 수동으로 활성화해야 합니다. UI에서 이 작업을 수행하는 방법에 대한 단계는 [정책 활성화](#enable)의 섹션을 참조하십시오.

## 전제 조건

이 안내서를 사용하려면 다음 [!DNL Experience Platform] 개념을 이해하고 있어야 합니다.

* [데이터 거버넌스](../home.md)
* [데이터 사용 정책](./overview.md)

## 기존 정책 보기 {#view-policies}

[!DNL Experience Platform] UI에서 **[!UICONTROL 정책]**&#x200B;을 선택하여 **[!UICONTROL 정책]** 작업 영역을 엽니다. **[!UICONTROL 찾아보기]** 탭에서 관련 레이블, 마케팅 작업 및 상태와 같은 사용 가능한 정책 목록을 볼 수 있습니다.

![](../images/policies/browse-policies.png)

동의 정책에 대한 액세스 권한이 있는 경우 **[!UICONTROL 동의 정책]** 전환을 선택하여 [!UICONTROL 찾아보기] 탭에서 봅니다.

![](../images/policies/consent-policy-toggle.png)

설명 및 유형을 보려면 나열된 정책을 선택합니다. 사용자 지정 정책을 선택하면 정책을 편집, 삭제 또는 [활성화/비활성화](#enable)하기 위한 추가 컨트롤이 표시됩니다.

![](../images/policies/policy-details.png)

## 사용자 지정 정책 만들기 {#create-policy}

새 사용자 지정 데이터 사용 정책을 만들려면 **[!UICONTROL 정책]** 작업 영역의 **[!UICONTROL 찾아보기]** 탭에 있는 오른쪽 상단 모서리에서 **[!UICONTROL 정책 만들기]**&#x200B;를 선택하십시오.

![](../images/policies/create-policy-button.png)

동의 정책에 대한 Beta에 속하는지 여부에 따라 다음 중 하나가 발생합니다.

* Beta에 속하지 않는 경우 [데이터 거버넌스 정책 만들기](#create-governance-policy)를 위한 워크플로우로 즉시 이동합니다.
* Beta의 일부인 경우 대화 상자에서 [동의 정책을 만들기](#consent-policy)하는 추가 옵션을 제공합니다.
  ![](../images/policies/choose-policy-type.png)

### 데이터 거버넌스 및 동의 정책을 함께 사용 {#combine-policies}

>[!NOTE]
>
>동의 정책은 현재 Adobe Healthcare Shield 또는 Adobe Privacy &amp; Security Shield를 구입한 조직에서만 사용할 수 있습니다.

거버넌스 및 동의 정책을 함께 사용하여 대상에 매핑된 대상을 제어하는 강력한 규칙을 만들 수 있습니다. 동의 정책은 기본적으로 포함되며, 이는 각 마케팅 경험에 포함될 수 있는 프로필을 지시함을 의미합니다. 반대로 거버넌스 정책은 레이블이 지정된 특정 속성의 사용을 활성화를 위해 구성되지 않도록 제외합니다.

이 비헤이비어를 사용하면 올바른 프로필을 포함하는 정책 및 동의 규칙의 조합을 설정할 수 있지만, 설정된 조직 규칙과 어긋나는 데이터를 포함하지 못합니다. 예를 들어 중요한 데이터를 포함하지 않으려 하지만, 여전히 소셜 미디어를 통해 마케팅을 위해 동의한 사용자를 타겟팅할 수 있는 시나리오가 있습니다. 이 시나리오에 필요한 단계는 아래 인포그래픽에 설명되어 있습니다.

![거버넌스 및 동의 정책을 함께 사용하여 관리 대상을 위한 강력한 규칙을 만드는 단계를 요약한 인포그래픽입니다.](../images/policies/governance-and-consent-policies-infographic.png)

### 데이터 거버넌스 정책 만들기 {#create-governance-policy}

**[!UICONTROL 정책 만들기]** 워크플로가 나타납니다. 새 정책의 이름과 설명을 입력하여 시작합니다.

![](../images/policies/create-policy-description.png)

그런 다음 정책이 기준으로 사용할 데이터 사용 레이블을 선택합니다. 여러 레이블을 선택할 때 정책을 적용하기 위해 데이터에 모든 레이블을 포함할지 또는 한 개 레이블을 포함할지 선택하는 옵션이 제공됩니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![](../images/policies/add-labels.png)

**[!UICONTROL 마케팅 작업 선택]** 단계가 나타납니다. 제공된 목록에서 적절한 마케팅 작업을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속합니다.

>[!NOTE]
>
>여러 마케팅 작업을 선택할 때 정책은 이를 &quot;OR&quot; 규칙으로 해석합니다. 즉, 선택한 마케팅 작업 중 **any**&#x200B;을(를) 수행하면 정책이 적용됩니다.

![](../images/policies/add-marketing-actions.png)

**[!UICONTROL 검토]** 단계가 표시되어 새 정책을 만들기 전에 자세한 내용을 검토할 수 있습니다. 만족하면 **[!UICONTROL 완료]**&#x200B;를 선택하여 정책을 만드십시오.

![](../images/policies/policy-review.png)

**[!UICONTROL 찾아보기]** 탭이 다시 나타납니다. 이 탭에는 이제 새로 만든 정책이 &quot;초안&quot; 상태로 나열됩니다. 정책을 활성화하려면 다음 섹션을 참조하십시오.

![](../images/policies/created-policy.png)

### 동의 정책 만들기 {#consent-policy}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsagePolicies_instructions"
>title="지침"
>abstract="<ul><li>동의를 위해 OneTrust 소스 커넥터 또는 표준 XDM 스키마를 통해 환경 설정 데이터를 통합 스키마로 수집하고 있는지 확인하십시오.</li><li>왼쪽 탐색 메뉴에서 <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=ko">정책</a> 을 선택한 다음 <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html#create-governance-policy">정책 만들기</a>를 선택합니다.</li><li><b>If</b> 섹션에서 정책 확인을 트리거할 조건 또는 작업을 설명합니다.</li><li><b>Then</b> 섹션에서 프로필이 정책을 트리거한 작업에 포함되기 위해 있어야 하는 동의 속성을 입력합니다.</li><li><b>저장</b> 을 선택하여 정책을 생성합니다. 정책을 활성화하려면 오른쪽 레일에서 <b>상태</b> 토글을 선택합니다.</li><li>Experience Platform은 대상에 대한 세그먼트를 활성화할 때 활성화된 동의 정책을 자동으로 적용하고 각 정책이 대상자 크기에 미치는 영향에 대한 세부 정보를 제공합니다.</li><li>이 기능에 대한 자세한 내용은 Experience League의 <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=ko#consent-policy">동의 정책 생성</a> 안내서를 참조하십시오.</li></ul>"

>[!IMPORTANT]
>
>동의 정책은 **Adobe Healthcare Shield** 또는 **Adobe Privacy &amp; Security Shield**&#x200B;를 구입한 조직에서만 사용할 수 있습니다.

동의 정책을 만들도록 선택한 경우 새 정책을 구성할 수 있는 새 화면이 나타납니다.

![](../images/policies/consent-policy-dialog.png)

동의 정책을 사용하려면 프로필 데이터에 동의 속성이 있어야 합니다. 유니온 스키마에 필수 특성을 포함하는 방법에 대한 자세한 단계는 [Experience Platform의 동의 처리](../../landing/governance-privacy-security/consent/adobe/overview.md)에 대한 안내서를 참조하십시오.

동의 정책은 다음 두 가지 논리적 구성 요소로 구성됩니다.

* **[!UICONTROL If]**: 정책 검사를 트리거할 조건입니다. 이는 수행되는 특정 마케팅 작업, 특정 데이터 사용 레이블의 존재 또는 두 가지의 조합을 기반으로 할 수 있습니다.
* **[!UICONTROL Then]**: 정책을 트리거한 작업에 포함할 프로필에 대해 존재해야 하는 동의 특성입니다.

#### 조건 구성 {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="If 조건"
>abstract="정책 확인을 트리거할 조건을 정의하여 시작하십시오. 조건에는 수행 중인 특정 마케팅 조치, 존재하는 특정 데이터 거버넌스 레이블 또는 이 둘의 조합이 포함될 수 있습니다."

**[!UICONTROL If]** 섹션에서 이 정책을 트리거해야 하는 마케팅 작업 및/또는 데이터 사용 레이블을 선택합니다. 사용 가능한 마케팅 작업과 레이블의 전체 목록을 보려면 각각 **[!UICONTROL 모두 보기]**&#x200B;와 **[!UICONTROL 레이블 선택]**&#x200B;을 선택하십시오.

조건을 하나 이상 추가한 후에는 **[!UICONTROL 조건 추가]**&#x200B;를 선택하여 필요에 따라 조건을 계속 추가하고 드롭다운에서 적절한 조건 유형을 선택할 수 있습니다.

![](../images/policies/add-condition.png)

두 개 이상의 조건을 선택하는 경우 조건 사이에 나타나는 아이콘을 사용하여 &quot;AND&quot;와 &quot;OR&quot; 사이의 조건부 관계를 전환할 수 있습니다.

![](../images/policies/and-or-selection.png)

#### 동의 속성 선택 {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Then 조건"
>abstract="&#39;If&#39; 조건이 정의되면 &#39;Then&#39; 섹션을 사용하여 통합 스키마에서 하나 이상의 동의 속성을 선택합니다. 이 정책이 적용되는 작업에 프로필을 포함하려면 이 속성이 있어야 합니다."

**[!UICONTROL Then]** 섹션 아래에서 유니온 스키마에서 하나 이상의 동의 특성을 선택합니다. 프로필이 이 정책이 제어하는 작업에 포함되려면 이 속성이 있어야 합니다. 목록에서 제공된 옵션 중 하나를 선택하거나 **[!UICONTROL 모두 보기]**&#x200B;를 선택하여 공용 구조체 스키마에서 직접 특성을 선택할 수 있습니다.

동의 속성을 선택할 때 이 정책에서 확인할 속성의 값을 선택합니다.

![](../images/policies/select-schema-field.png)

하나 이상의 동의 특성을 선택한 후 **[!UICONTROL 정책 속성]** 패널이 업데이트되어 총 프로필 저장소 비율을 포함하여 이 정책에서 허용되는 예상 프로필 수를 표시합니다. 이 추정은 정책 구성을 조정할 때 자동으로 업데이트됩니다.

![](../images/policies/audience-preview.png)

정책에 동의 특성을 더 추가하려면 **[!UICONTROL 결과 추가]**&#x200B;를 선택하십시오.

![](../images/policies/add-result.png)

필요에 따라 정책에 조건 및 동의 속성을 계속 추가 및 조정할 수 있습니다. 구성에 만족하면 **[!UICONTROL 저장]**&#x200B;을 선택하기 전에 정책의 이름과 선택적 설명을 입력하십시오.

![](../images/policies/name-and-save.png)

이제 동의 정책이 만들어졌으며 기본적으로 동의 상태는 [!UICONTROL 사용 안 함](으)로 설정됩니다. 정책을 즉시 사용하려면 오른쪽 레일에서 **[!UICONTROL 상태]** 전환을 선택하십시오.

![](../images/policies/enable-consent-policy.png)

#### 정책 적용 확인

동의 정책을 만들고 활성화한 후 대상에 대한 세그먼트를 활성화할 때 동의한 대상자에 어떤 영향을 미치는지 미리 볼 수 있습니다. 자세한 내용은 [동의 정책 평가](../enforcement/auto-enforcement.md#consent-policy-evaluation)의 섹션을 참조하십시오.

## 정책 활성화 또는 비활성화 {#enable}

모든 데이터 사용 정책(Adobe에서 제공하는 핵심 정책 포함)은 기본적으로 비활성화되어 있습니다. 개별 정책을 적용하여 시행하려면 API 또는 UI를 통해 해당 정책을 수동으로 활성화해야 합니다.

**[!UICONTROL 정책]** 작업 영역의 **[!UICONTROL 찾아보기]** 탭에서 정책을 활성화하거나 비활성화할 수 있습니다. 목록에서 사용자 지정 정책을 선택하여 오른쪽에 세부 정보를 표시합니다. **[!UICONTROL 상태]**&#x200B;에서 정책을 사용하거나 사용하지 않도록 설정할 토글 단추를 선택하십시오.

![](../images/policies/enable-policy.png)

## 마케팅 액션 보기 {#view-marketing-actions}

**[!UICONTROL 정책]** 작업 영역에서 **[!UICONTROL 마케팅 작업]** 탭을 선택하여 Adobe 및 조직에서 정의한 사용 가능한 마케팅 작업 목록을 확인합니다.

![](../images/policies/marketing-actions.png)

## 마케팅 액션 만들기 {#create-marketing-action}

새 사용자 지정 마케팅 작업을 만들려면 **[!UICONTROL 정책]** 작업 영역의 **[!UICONTROL 마케팅 작업]** 탭에 있는 오른쪽 상단 모서리에서 **[!UICONTROL 마케팅 작업 만들기]**&#x200B;를 선택합니다.

![](../images/policies/create-marketing-action.png)

**[!UICONTROL 마케팅 액션 만들기]** 대화 상자가 나타납니다. 마케팅 액션의 이름과 설명을 입력한 다음 **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

![](../images/policies/create-marketing-action-details.png)

새로 만든 작업이 **[!UICONTROL 마케팅 작업]** 탭에 나타납니다. 이제 [새 데이터 사용 정책을 만드는 중](#create-policy)에 마케팅 작업을 사용할 수 있습니다.

![](../images/policies/created-marketing-action.png)

## 마케팅 액션 편집 또는 삭제 {#edit-delete-marketing-action}

>[!NOTE]
>
>조직에서 정의한 사용자 지정 마케팅 작업만 편집할 수 있습니다. Adobe이 정의한 마케팅 액션은 변경하거나 삭제할 수 없습니다.

**[!UICONTROL 정책]** 작업 영역에서 **[!UICONTROL 마케팅 작업]** 탭을 선택하여 Adobe 및 조직에서 정의한 사용 가능한 마케팅 작업 목록을 확인합니다. 목록에서 사용자 지정 마케팅 작업을 선택한 다음 오른쪽 섹션에 제공된 필드를 사용하여 마케팅 작업의 세부 정보를 편집합니다.

![](../images/policies/edit-marketing-action.png)

마케팅 액션이 기존 사용 정책에서 사용되고 있지 않은 경우 **[!UICONTROL 마케팅 액션 삭제]**&#x200B;를 선택하여 삭제할 수 있습니다.

>[!NOTE]
>
>기존 정책에서 사용 중인 마케팅 액션을 삭제하려고 하면 삭제 시도가 실패했음을 나타내는 오류 메시지가 표시됩니다.

![](../images/policies/delete-marketing-action.png)

## 다음 단계

이 문서에서는 [!DNL Experience Platform] UI의 데이터 사용 정책을 관리하는 방법에 대한 개요를 제공했습니다. [!DNL Policy Service API]을(를) 사용하여 정책을 관리하는 방법에 대한 단계는 [개발자 안내서](../api/getting-started.md)를 참조하십시오. 데이터 사용 정책을 적용하는 방법에 대한 자세한 내용은 [정책 적용 개요](../enforcement/overview.md)를 참조하세요.

다음 비디오에서는 [!DNL Experience Platform] UI에서 사용 정책으로 작업하는 방법에 대해 보여 줍니다.

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
