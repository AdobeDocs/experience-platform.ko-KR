---
title: Privacy Service 권한 관리
description: Adobe Admin Console을 사용하여 Adobe Experience Platform Privacy Service의 사용자 권한을 관리하는 방법을 알아봅니다.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 1%

---

# Privacy Service 권한 관리

액세스 권한 [Adobe Experience Platform Privacy Service](./home.md) 는 Adobe Admin Console의 세부적인 역할 기반 권한을 통해 제어됩니다. 사용자 그룹에 권한을 할당하는 제품 프로필을 만들어 Privacy Service에서 해당 기능에 액세스할 수 있는 사용자를 결정할 수 있습니다 [UI](./ui/overview.md) 및 [API](./api/overview.md).

>[!NOTE]
>
>Privacy Service API에 대한 통합을 생성할 때 통합에 대한 권한이 있는 기능 또는 작업을 결정하려면 기존 제품 프로필을 선택해야 합니다. 다음 안내서를 참조하십시오. [Privacy Service API 시작](./api/getting-started.md) 추가 정보.

이 안내서에서는 Privacy Service 권한을 관리하는 방법을 보여줍니다.

## 시작하기

Privacy Service에 대한 액세스 제어를 구성하려면 Adobe Experience Platform Privacy Service과 제품 통합이 있는 조직에 대한 관리자 권한이 있어야 합니다. 권한을 부여하거나 취소할 수 있는 최소 역할은 입니다 **제품 프로필 관리자**. 권한을 관리할 수 있는 기타 관리자 역할은 다음과 같습니다 **제품 관리자** (제품 내의 모든 프로필을 관리할 수 있음) 및 **시스템 관리자** (제한 없음) 다음 문서를 참조하십시오. [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html) 자세한 내용은 Adobe 엔터프라이즈 관리 안내서 를 참조하십시오.

이 안내서에서는 제품 프로필과 같은 기본 Admin Console 개념 및 개별 사용자 및 그룹에 제품 권한을 부여하는 방법에 대해 잘 알고 있다고 가정합니다. 자세한 내용은 [Admin Console 사용 안내서](https://helpx.adobe.com/kr/enterprise/using/admin-console.html).

## 사용 가능한 권한

다음 표에서는 Privacy Service이 액세스 권한을 부여하는 특정 기능에 대한 설명과 함께 사용 가능한 권한에 대해 설명합니다.

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| [!UICONTROL Privacy Service 권한] | [!UICONTROL 개인 정보 읽기 권한] | 사용자가 세부 정보와 함께 기존 액세스 및 삭제 요청을 볼 수 있는지 여부를 결정합니다. |
| [!UICONTROL Privacy Service 권한] | [!UICONTROL 개인 정보 쓰기 권한] | 사용자가 새 액세스 및 삭제 요청을 만들 수 있는지 여부를 결정합니다. |
| [!UICONTROL Privacy Service 권한] | [!UICONTROL 컨텐츠 전달 권한 읽기(액세스)] | 액세스 요청이 Privacy Service에 의해 처리되면 고객의 데이터가 포함된 ZIP 파일이 해당 고객에게 전송됩니다. 액세스 요청의 세부 사항을 조회할 때 이 권한은 사용자가 요청의 ZIP 파일에 대한 다운로드 링크에 액세스할 수 있는지 여부를 결정합니다. |
| [!UICONTROL 판매 중지 권한] | [!UICONTROL 읽기 권한 - 판매 중지] | 사용자가 세부 정보와 함께 기존 판매 중지 요청을 볼 수 있는지 여부를 결정합니다. |
| [!UICONTROL 판매 중지 권한] | [!UICONTROL 쓰기 권한 - 판매 중지] | 사용자가 새 판매 중지 요청을 만들 수 있는지 여부를 결정합니다. |

{style=&quot;table-layout:auto&quot;}

## 권한 관리 {#manage}

Privacy Service 권한을 관리하려면 로그인하십시오 [Admin Console](https://adminconsole.adobe.com/) 을(를) 선택합니다. **[!UICONTROL 제품]** 위쪽 탐색에서 를 클릭합니다. 여기에서 을 선택합니다. **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Admin Console에 Privacy Service 제품 카드를 표시하는 이미지](./images/permissions/privacy-service-card.png)

### 제품 프로필 선택 또는 만들기

다음 화면에는 조직 아래에서 Privacy Service에 사용할 수 있는 제품 프로필 목록이 표시됩니다. 제품 프로필이 없으면 을 선택합니다. **[!UICONTROL 새 프로필]** 만들 수 있습니다. 조직에 서로 다른 수준의 액세스가 필요한 여러 역할이나 사용자 그룹이 있는 경우 각 역할에 대해 별도의 제품 프로필을 만들어야 합니다.

![Admin Console에서 Privacy Service에 대한 제품 프로필을 보여주는 이미지](./images/permissions/select-or-create-profile.png)

제품 프로필을 선택한 후 **[!UICONTROL 권한]** 시작할 탭 [권한 편집](#edit-permissions) 프로파일에 대해 를 선택하거나 **[!UICONTROL 사용자]** 시작할 탭 [사용자 할당](#assign-users) 참조하십시오.

![제품 프로필 Admin Console에 대한 권한 탭을 보여주는 이미지](./images/permissions/users-permissions-tabs.png)

### 프로필에 대한 권한 편집 {#edit-permissions}

설정 **[!UICONTROL 권한]** 탭에서 표시된 권한 범주 중 하나를 선택하여 권한 편집 보기에 액세스합니다.

프로필에 대한 권한을 편집할 때 사용 가능한 권한이 왼쪽 열에 나열되고 프로필에 포함된 권한은 오른쪽 열에 나열됩니다. 두 열 간에 이동할 나열된 권한을 선택합니다.

![사용 가능하고 포함된 권한 열을 보여주는 이미지](./images/permissions/edit-permissions.png)

권한은 카테고리로 구성됩니다. 카테고리 간을 전환하려면 왼쪽 탐색에서 원하는 카테고리를 선택합니다.

![이미지를 보여주는 이미지 [!UICONTROL 판매 거부] 권한 아래의 섹션](./images/permissions/switch-category.png)

선택 **[!UICONTROL 저장]** 권한 구성을 완료하면

![제품 프로필에 대해 저장되는 권한 구성을 보여주는 이미지](./images/permissions/save-permissions.png)

추가된 권한이 반영되면 제품 프로필 보기가 다시 나타납니다.

![제품 프로필에 대해 추가된 권한을 보여주는 이미지](./images/permissions/permissions-added.png)

### 프로필에 사용자 할당 {#assign-users}

제품 프로필에 사용자를 할당(그리고 프로필에 구성된 권한을 부여)하려면 다음을 선택합니다 **[!UICONTROL 사용자]** 탭, 그 다음 **[!UICONTROL 사용자 추가]**.

![Admin Console에서 제품 프로필에 대한 사용자 탭을 보여주는 이미지](./images/permissions/manage-users.png)

제품 프로필의 사용자 관리에 대한 자세한 내용은 [Admin Console 설명서](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### 프로필로 이전 API 자격 증명 마이그레이션 {#migrate-tech-accounts}

>[!NOTE]
>
>이 섹션은 Privacy Service 권한이 Adobe Admin Console에 통합되기 전에 생성된 기존 API 자격 증명에만 적용됩니다. 새 자격 증명의 경우 제품 프로필(및 해당 권한)은 [Adobe Developer 콘솔 프로젝트](https://developer.adobe.com/developer-console/docs/guides/projects/) 을 가리키도록 업데이트하는 것이 좋습니다.<br><br>의 섹션을 참조하십시오. [프로젝트에 제품 프로필 할당](./api/getting-started.md#product-profiles) 자세한 내용은 Privacy Service API 시작 안내서를 참조하십시오.

레거시 API 자격 증명을 제품 프로필에 마이그레이션하려면 을 선택합니다 **[!UICONTROL API 자격 증명]**, 그 다음 **[!UICONTROL API 자격 증명 추가]**.

![[!UICONTROL API 자격 증명 추가] Admin Console에서 선택 [!UICONTROL API 자격 증명] 제품 프로필의 탭](./images/permissions/api-credentials.png)

목록에서 원하는 개발자 콘솔 프로젝트를 선택한 다음 을 선택합니다 **[!UICONTROL 저장]** 를 제품 프로필에 추가합니다. 이러한 프로젝트의 자격 증명을 사용하는 모든 API 호출은 제품 프로필에서 부여한 세부 권한을 상속합니다.

## 다음 단계

이 안내서에서는 Privacy Service에 사용할 수 있는 권한과 Admin Console을 통해 관리하는 방법에 대해 다룹니다.

제품 프로필을 설정한 후 새 API 통합을 만드는 방법에 대한 단계는 다음을 참조하십시오. [Privacy Service API에 대한 시작 안내서](./api/getting-started.md). 다른 Adobe Experience Platform 기능에 대한 권한 관리에 대한 자세한 내용은 [액세스 제어 설명서](../access-control/home.md).
