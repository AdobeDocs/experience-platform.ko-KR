---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 사용자 관리
description: Adobe Experience Cloud의 권한 인터페이스를 통해 사용자 및 사용자 그룹을 관리합니다.
exl-id: 16450867-040a-4be1-a6c0-f03d0a1b90ba
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 4%

---

# 사용자 관리 및 사용자 그룹 추가 {#manage-users}

>[!CONTEXTUALHELP]
>id="platform_permissions_users_about"
>title="사용자란 무엇입니까?"
>abstract="사용자는 Experience Platform에 액세스할 수 있는 개인입니다. 조직의 리소스에 대한 개별 사용자의 액세스는 역할을 통해 관리됩니다."
>additional-url="https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/abac/permissions-ui/roles" text="역할 관리"

사용자는 Adobe Experience Platform에 액세스할 수 있는 개인입니다. 조직의 리소스에 대한 개별 사용자의 액세스 권한은 [역할](./roles.md){target="_blank"}을 통해 관리됩니다. 조직은 [사용자 그룹](#user-groups)을 만들어 여러 사용자의 그룹에 동시에 원활하게 액세스할 수도 있습니다. 사용자는 Admin Console에서 관리되고 Adobe Experience Platform 제품 카드와 연결된 사용자는 Experience Platform의 사용자 목록에 일부로 표시됩니다.

## 사용자 관리

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform users. To add users to Experience Platform, navigate to Adobe Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add users through the Admin Console, follow the [adding users to Experience Platform](...){#target="_blank"} guide.
-->

조직의 사용자를 보려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 &#x200B;](https://experience.adobe.com/){target="_blank"}(으)로 이동하십시오. 왼쪽 패널에서 **[!UICONTROL Users]**&#x200B;을(를) 선택합니다.

![사용 권한 내의 사용자 작업 영역입니다.](../../images/ui/users/users-overview.png){zoomable="yes"}

사용자 목록이 나타납니다. 목록에서 보려는 사용자를 선택합니다. 또는 검색 창을 사용하여 이름이나 이메일 주소를 입력하여 사용자를 검색합니다.

**[!UICONTROL Details]** 탭은 사용자에 대한 개요를 제공합니다. 개요에는 사용자의 **[!UICONTROL Name]**, **[!UICONTROL Preferred languages]**, **[!UICONTROL Account Type]**, **[!UICONTROL Authentication ID]**, **[!UICONTROL Email]**, **[!UICONTROL Email verified]** 상태, **[!UICONTROL Country code]** 및 **[!UICONTROL Phone number]**&#x200B;이(가) 표시됩니다.

![사용자의 세부 정보 작업 영역입니다.](../../images/ui/users/user-details.png){zoomable="yes"}

사용자가 할당된 역할을 보려면 **[!UICONTROL Roles]** 탭을 선택하십시오.

![사용자의 역할 작업 영역입니다.](../../images/ui/users/user-roles.png){zoomable="yes"}

### 사용자에게 역할 추가 {#add-user-role}

사용자에게 역할을 추가하려면 **[!UICONTROL Add Roles]**&#x200B;을(를) 선택하십시오.

![역할 추가 옵션이 강조 표시된 사용자의 역할 작업 영역입니다.](../../images/ui/users/user-add-roles.png){zoomable="yes"}

**[!UICONTROL Add Roles]** 대화 상자가 나타납니다. 사용자에게 추가할 역할을 선택한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오.

![역할을 선택하고 저장 옵션이 강조 표시된 역할 추가 대화 상자.](../../images/ui/users/user-roles-add-roles-confirm.png){zoomable="yes"}

### 사용자에서 역할 제거 {#remove-user-role}

사용자에서 역할을 제거하려면 역할 이름 옆에 있는 **X**&#x200B;을(를) 선택합니다.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW

>[!NOTE]
>
>Role's that have been added to a user through a user group cannot be removed through the user's role workspace. Role's that have been added through a user group will have an [!Info icon](/help/images/icons/info.png) beside the **X** containing information about the associated user group. To remove the role, the role would need to be [removed from the user group](#remove-user-group-role).
-->

![역할의 제거 옵션이 강조 표시된 사용자의 역할 작업 영역입니다.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

확인 대화 상자가 나타납니다. **[!UICONTROL Confirm]**&#x200B;을(를) 선택하여 역할 제거를 완료합니다.

![확인 옵션이 강조 표시된 역할을 제거하는 확인 대화 상자입니다.](../../images/ui/users/user-roles-remove.png){zoomable="yes"}

## 사용자 그룹 관리 {#user-groups}

사용자 그룹은 함께 그룹화된 여러 사용자이며 동일한 기능을 실행할 수 있는 액세스 권한을 갖습니다.

<!-- ADD LINKS INTO IMPORTANT NOTE BELOW
>[!IMPORTANT]
>
>[!UICONTROL Permissions] manages access control for existing Experience Platform user groups. To add user groups to Experience Platform, navigate to Admin Console through the **[!UICONTROL Edit in admin console]** option. To learn how to add user groups in the Admin Console, follow the [adding user groups to Experience Platform](...){#target="_blank"} guide.
 -->

조직의 사용자를 보려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 &#x200B;](https://experience.adobe.com/){target="_blank"}(으)로 이동합니다.왼쪽 패널의 **[!UICONTROL Groups]** 섹션에서 **[!UICONTROL Users]**&#x200B;을(를) 선택합니다.

![사용자가 권한 내에서 작업 영역을 그룹화합니다.](../../images/ui/users/user-groups-overview.png){zoomable="yes"}

사용자 그룹 목록이 나타납니다. 목록에서 보려는 그룹을 선택합니다.

**[!UICONTROL Details]** 탭은 사용자 그룹에 대한 개요를 제공합니다. 개요에는 그룹의 **[!UICONTROL Name]**, **[!UICONTROL Description]**, **[!UICONTROL User Count]** 및 **[!UICONTROL Admin count]**&#x200B;이(가) 표시됩니다.

![사용자 그룹의 세부 정보 작업 영역입니다.](../../images/ui/users/user-group-details.png){zoomable="yes"}

그룹에 할당된 사용자 목록을 보려면 **[!UICONTROL Users]** 탭을 선택하십시오.

![사용자 그룹의 사용자 작업 영역입니다.](../../images/ui/users/user-group-users.png){zoomable="yes"}

그룹에 현재 할당된 역할 목록을 보려면 **[!UICONTROL Roles]** 탭을 선택하십시오.

![사용자 그룹의 역할 작업 영역입니다.](../../images/ui/users/user-group-roles.png){zoomable="yes"}

### 사용자 그룹에 역할 추가 {#add-user-group-role}

그룹에 새 역할을 추가하려면 **[!UICONTROL Add Roles]**&#x200B;을(를) 선택하십시오.

![역할 추가 옵션이 강조 표시된 사용자 그룹의 역할 작업 영역입니다.](../../images/ui/users/user-group-add-roles.png){zoomable="yes"}

**[!UICONTROL Add Roles]** 대화 상자가 나타납니다. 추가할 역할을 선택한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오. 사용자 그룹에 속한 모든 사용자에 대해 역할이 추가됩니다.

![역할을 선택하고 [저장] 옵션이 강조 표시된 [역할 추가] 대화 상자.](../../images/ui/users/user-group-add-roles-select.png){zoomable="yes"}

### 사용자 그룹에서 역할 제거 {#remove-user-group-role}

사용자 그룹에서 역할을 제거하려면 역할 이름 옆에 있는 **X**&#x200B;을(를) 선택합니다.

![역할 제거 옵션이 강조 표시된 사용자 그룹의 역할 작업 영역입니다.](../../images/ui/users/user-group-remove-role.png){zoomable="yes"}

확인 대화 상자가 나타납니다. **[!UICONTROL Confirm]**&#x200B;을(를) 선택하여 역할 제거를 완료합니다.

![확인 옵션이 강조 표시된 역할을 제거하는 확인 대화 상자입니다.](../../images/ui/users/user-group-remove-role-confirm.png){zoomable="yes"}

## API 자격 증명

>[!IMPORTANT]
>
>시스템 관리자만 권한에서 API 자격 증명을 보고 관리할 수 있습니다.

Experience Platform API를 사용자 또는 개발자로 사용하려면 시스템 관리자가 역할에 지정된 권한 집합 외에 API 자격 증명을 추가해야 합니다. 권한을 사용하면 이전에 만든 API 자격 증명을 Experience Platform 제품에 할당하여 역할에 할당할 수 있습니다. API 자격 증명 만들기 및 할당과 필요한 권한에 대한 전체 안내서는 [Experience Platform API 인증 및 액세스](/help/landing/api-authentication.md){target="_blank"}의 단계별 자습서를 참조하십시오.

Experience Platform과 연결된 조직 API 자격 증명을 보려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 &#x200B;](https://experience.adobe.com/){target="_blank"}(으)로 이동하십시오. 왼쪽 패널의 **[!UICONTROL API Credentials]** 섹션에서 **[!UICONTROL Users]** 선택

![권한 내의 API 자격 증명 작업 영역입니다.](../../images/ui/users/api-credentials-overview.png){zoomable="yes"}

>[!NOTE]
>
> 조직의 모든 제품에 대한 조직의 API 자격 증명을 보거나 자격 증명에 대한 자세한 내용을 보려면 **[!UICONTROL Edit in admin console]**&#x200B;을(를) 선택하십시오.

API 자격 증명 목록이 나타납니다. 목록에서 보려는 API 자격 증명을 선택합니다.

**[!UICONTROL Details]** 탭은 API 자격 증명의 개요를 제공합니다. 개요에는 자격 증명의 **[!UICONTROL Name]**, **[!UICONTROL Modified]** 날짜, **[!UICONTROL Modified By]** 특성, **[!UICONTROL Created]** 날짜, **[!UICONTROL Created by]** 특성, **[!UICONTROL API key]**, **[!UICONTROL Technical ID]** 및 **[!UICONTROL Email]**&#x200B;이(가) 표시됩니다.

![API 자격 증명의 세부 정보 작업 영역입니다.](../../images/ui/users/api-credential-details.png){zoomable="yes"}

**[!UICONTROL Roles]** 탭을 선택합니다. API 자격 증명과 연결된 역할 목록이 나타납니다.

![API 자격 증명의 역할 작업 영역입니다.](../../images/ui/users/api-credential-roles.png){zoomable="yes"}

### API 자격 증명에 역할 추가 {#add-api-credential-role}

API 자격 증명에 역할을 추가하려면 **[!UICONTROL Add Roles]**&#x200B;을(를) 선택합니다.

![역할 추가 옵션이 강조 표시된 API 자격 증명의 작업 영역입니다.](../../images/ui/users/api-credential-add-roles.png){zoomable="yes"}

**[!UICONTROL Add Roles]** 대화 상자가 나타납니다. 사용자에게 추가할 역할을 선택한 다음 **[!UICONTROL Save]**&#x200B;을(를) 선택하십시오.

![역할을 선택하고 저장 옵션이 강조 표시된 역할 추가 대화 상자.](../../images/ui/users/api-credential-add-roles-select.png){zoomable="yes"}

### API 자격 증명에서 역할 제거 {#remove-api-credential-role}

API 자격 증명에서 역할을 제거하려면 API 자격 증명의 이름 옆에 있는 **X**&#x200B;을(를) 선택합니다.

![역할의 제거 옵션이 강조 표시된 API 자격 증명의 역할 작업 영역입니다.](../../images/ui/users/api-credential-remove-role.png){zoomable="yes"}

확인 대화 상자가 나타납니다. **[!UICONTROL Confirm]**&#x200B;을(를) 선택하여 역할 제거를 완료합니다.

![확인 옵션이 강조 표시된 역할을 제거하는 확인 대화 상자입니다.](../../images/ui/users/api-credential-remove-role-confirm.png){zoomable="yes"}

## 다음 단계

이제 사용자, 사용자 그룹 및 API 자격 증명에 대한 세부 정보 및 역할을 보는 방법을 알 수 있습니다. 특성 기반 액세스 제어에 대한 자세한 내용은 [특성 기반 액세스 제어 개요](../overview.md)를 참조하세요.

<!--
The following video is intended to support your understanding of developer and API credentials.

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)
-->