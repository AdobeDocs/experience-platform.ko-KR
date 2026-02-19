---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 역할 만들기
description: Adobe Experience Cloud의 권한 인터페이스를 통해 역할을 관리합니다.
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: b665d0edce713f1b252e07125aabab79d52a9cba
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 13%

---

# 역할 관리

<!-- UPDATE ROLES WITH A MORE COMPREHENSIVE EXPLANATION -->

역할 관리를 시작하려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[에서 &#x200B;](https://experience.adobe.com/){target="_blank"}(으)로 이동하고 왼쪽 패널에서 **[!UICONTROL Roles]**&#x200B;을(를) 선택합니다.

![권한 내의 역할 작업 영역입니다.](../../images/ui/roles/roles-overview.png)

## 새 역할 만들기 {#create-new-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about_create"
>title="새 역할 만들기"
>abstract="Experience Platform 인스턴스와 상호 작용하는 사용자를 더 잘 분류하기 위해 새로운 역할을 만듭니다. 예를 들어 내부 마케팅 팀의 역할을 생성하고 규제 건강 데이터(RHD) 레이블을 해당 역할에 적용하여 내부 마케팅 팀이 개인건강정보(PHI)에 액세스할 수 있도록 할 수 있습니다. 또는 외부 에이전시에 대한 역할을 생성하고 해당 역할에 RHD 레이블을 적용하지 않음으로써 PHI 데이터에 대한 해당 역할의 액세스를 거부할 수도 있습니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=ko" text="역할 관리"
>additional-url="https://experienceleague.adobe.com/ko/docs/experience-platform/access-control/abac/end-to-end-guide#label-roles" text="역할에 레이블 적용"

새 역할을 만들려면 **[!UICONTROL Create role]**&#x200B;을(를) 선택하십시오.

>[!TIP]
>
>읽기 전용 역할은 즉시 사용할 수 있습니다. 읽기 전용 역할은 시스템 상태를 변경하지 않고 사용자에게 데이터, 구성 및 UI 기능을 볼 수 있는 권한을 부여하는 역할입니다. 관리자는 이러한 역할을 편집할 수 없지만 사용자를 역할에 연결할 수 있습니다.

![역할 만들기 옵션이 강조 표시된 역할의 작업 영역입니다.](../../images/ui/roles/roles-create-role.png)

**[!UICONTROL Create new role]** 대화 상자가 나타납니다. 역할에 대해 **[!UICONTROL Name]**&#x200B;을(를) 입력하고 필요에 따라 **[!UICONTROL Description]**&#x200B;을(를) 입력한 다음 **[!UICONTROL Confirm]**&#x200B;을(를) 선택합니다.

![이름 및 설명을 입력하고 확인 옵션이 강조 표시된 새 역할 만들기 대화 상자.](../../images/ui/roles/roles-create-new-role.png)

**[!UICONTROL Resources]** 작업 영역이 나타납니다. 스크롤하거나 왼쪽 패널의 검색 막대에 리소스 이름을 입력하여 필요한 리소스를 찾습니다. 리소스 이름 옆에 있는 ![더하기 아이콘](/help/images/icons/plus.png)을 선택하여 리소스를 추가합니다.

![개별 리소스의 추가 옵션이 강조 표시된 리소스 작업 영역입니다.](../../images/ui/roles/roles-resources.png)

<!-- ADD IN NOTE ABOUT THE DEFAULT SANDBOX - THIS SHOULD BE MENTIONED IN THE HIGHER LEVEL DOCS, WE MAY BE ABLE TO LINK TO IT -->

리소스가 기본 작업 영역에 추가됩니다. 리소스 이름 옆에 있는 드롭다운을 선택하고 역할에 추가할 권한을 선택합니다. 검색 창에 권한 이름을 입력하여 개별적으로 선택하거나 **[!UICONTROL Add all]**&#x200B;을(를) 선택하거나 특정 권한을 찾을 수 있습니다.

![개별 리소스의 드롭다운 메뉴가 확장되고 강조 표시된 리소스 작업 영역입니다.](../../images/ui/roles/roles-resources-permissions.png)

계속해서 역할에 추가하려는 모든 리소스 및 권한을 선택합니다. 완료되면 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

![저장 옵션이 강조 표시된 리소스 작업 영역입니다.](../../images/ui/roles/roles-resources-permissions-save.png)

역할이 저장되었음을 나타내는 경고가 표시됩니다. **[!UICONTROL Close]** 작업 영역으로 돌아가려면 **[!UICONTROL Roles]**&#x200B;을(를) 선택하십시오.

![성공 경고와 닫기 옵션이 강조 표시된 리소스 작업 영역입니다.](../../images/ui/roles/roles-resources-permissions-close.png)

새 역할이 만들어졌고 **[!UICONTROL Roles]** 페이지로 리디렉션됩니다. 그러면 새로 만든 역할이 목록에 나타납니다.

<!-- The following video is intended to support your understanding of creating a new role and managing users for that role.

>[!VIDEO](https://video.tv.adobe.com/v/3475980/?captions=kor&learn=on) -->

## 역할 복제

역할을 복제하면 세부 정보, 권한, 레이블 및 샌드박스에 복사됩니다. 사용자, 사용자 그룹 및 API 자격 증명 **은(는) 복사되지 않습니다**. 역할에 수동으로 추가해야 합니다.

기존 역할을 복제하려면 **[!UICONTROL Roles]** 탭 내에서 복제할 역할을 찾습니다. 역할 이름 옆의 ![자세히 아이콘](/help/images/icons/more.png)을 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL Duplicate]**&#x200B;을(를) 선택합니다.

![역할 드롭다운 메뉴가 확장되고 복제 옵션이 강조 표시된 역할 작업 영역입니다.](../../images/ui/roles/role-duplicate.png)

중복 확인 대화 상자가 나타납니다. **[!UICONTROL Confirm]**&#x200B;을(를) 선택하여 역할 복제를 완료합니다. 새 역할은 `_Copy`이(가) 접미사로 추가된 동일한 이름으로 저장됩니다.

![확인 옵션이 강조 표시된 중복 확인 대화 상자입니다.](../../images/ui/roles/role-duplicate-confirm.png)

또는 개별 역할의 작업 영역 내에서 역할을 복제할 수도 있습니다. **[!UICONTROL Roles]** 작업 영역에서 복제할 역할을 선택한 다음 **[!UICONTROL Duplicate]**&#x200B;을(를) 선택합니다.

![복제 옵션이 강조 표시된 개별 역할의 작업 영역입니다.](../../images/ui/roles/role-duplicate-alt.png)

중복 확인 대화 상자가 나타납니다. **[!UICONTROL Confirm]**&#x200B;을(를) 선택하여 역할 복제를 완료합니다. 새 역할로 리디렉션됩니다.

![확인 옵션이 강조 표시된 중복 확인 대화 상자입니다.](../../images/ui/roles/role-duplicate-alt-confirm.png)

## 역할 삭제

역할을 삭제하려면 **[!UICONTROL Roles]** 탭에서 삭제할 역할을 찾습니다. 역할 이름 옆의 ![자세히 아이콘](/help/images/icons/more.png)을 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL Delete]**&#x200B;을(를) 선택합니다.

![역할 드롭다운 메뉴가 확장되고 복제 옵션이 강조 표시된 역할 작업 영역입니다.](../../images/ui/roles/role-delete.png)

삭제 확인 대화 상자가 나타납니다. 역할 삭제를 완료하려면 **[!UICONTROL Confirm]**&#x200B;을(를) 선택하십시오.

![확인 옵션이 강조 표시된 중복 확인 대화 상자입니다.](../../images/ui/roles/role-duplicate-confirm.png)

또는 개별 역할의 작업 영역 내에서 역할을 삭제할 수 있습니다. **[!UICONTROL Roles]** 작업 영역에서 삭제할 역할을 선택한 다음 **[!UICONTROL Delete]**&#x200B;을(를) 선택하십시오.

![삭제 옵션이 강조 표시된 개별 역할의 작업 영역입니다.](../../images/ui/roles/role-delete-alt.png)

삭제 확인 대화 상자가 나타납니다. 역할 삭제를 완료하려면 **[!UICONTROL Confirm]**&#x200B;을(를) 선택하십시오.

![확인 옵션이 강조 표시된 삭제 확인 대화 상자입니다.](../../images/ui/roles/role-delete-alt-confirm.png)

<!-- ADD PERMISSIONS TO THIS PAGE -->

## 다음 단계

새 역할이 만들어지면 [역할에 대한 권한을 관리](permissions.md)하는 다음 단계로 진행할 수 있습니다.
