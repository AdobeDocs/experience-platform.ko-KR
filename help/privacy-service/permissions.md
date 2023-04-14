---
title: Privacy Service 권한 관리
description: Adobe Admin Console을 사용하여 Adobe Experience Platform Privacy Service의 사용자 권한을 관리하는 방법을 알아봅니다.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 1%

---

# Privacy Service 권한 관리

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service에 대한 권한을 개선하여 세부기간 수준을 늘렸습니다. 이러한 변경 사항으로 조직 관리자는 원하는 역할 및 권한 수준을 사용하여 더 많은 사용자에게 액세스 권한을 부여할 수 있습니다. 이 임박한 업데이트가 기술 계정 사용자에게 중요한 변경 사항이므로 기술 계정 사용자는 Privacy Service 권한을 업데이트해야 합니다. 이 권한 변경의 적용은 **2023년 4월 13일**. 다음 문서를 참조하십시오. [레거시 API 자격 증명 마이그레이션](#migrate-tech-accounts) 이 문제 해결에 대한 지침은
>
>기술 계정은 엔터프라이즈 고객이 사용할 수 있으며 Adobe 개발자 콘솔을 통해 만들 수 있습니다. 기술 계정 소유자의 Adobe ID은 `@techacct.adobe.com`. 기술 계정 보유자인지 확실하지 않은 경우 조직 관리자에게 문의하십시오.

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

>[!NOTE]
>
>모든 Privacy Service 및 [!UICONTROL 판매 거부] 권한은 서로 구분되고, 기능적 겹치지 않는 서로 구분됩니다. Privacy Service API가 idempotent로 간주되므로 가능한 작업입니다.

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| [!UICONTROL Privacy Service 권한] | [!UICONTROL 개인 정보 읽기 권한] | 사용자가 세부 정보와 함께 기존 액세스 및 삭제 요청을 볼 수 있는지 여부를 결정합니다. |
| [!UICONTROL Privacy Service 권한] | [!UICONTROL 개인 정보 쓰기 권한] | 사용자가 새 액세스 및 삭제 요청을 만들 수 있는지 여부를 결정합니다. |
| [!UICONTROL Privacy Service 권한] | [!UICONTROL 컨텐츠 전달 권한 읽기(액세스)] | 액세스 요청이 Privacy Service에 의해 처리되면 고객의 데이터가 포함된 ZIP 파일이 해당 고객에게 전송됩니다. 액세스 요청의 세부 사항을 조회할 때 이 권한은 사용자가 요청의 ZIP 파일에 대한 다운로드 링크에 액세스할 수 있는지 여부를 결정합니다. |
| [!UICONTROL 판매 중지 권한] | [!UICONTROL 읽기 권한 - 판매 중지] | 사용자가 세부 정보와 함께 기존 판매 중지 요청을 볼 수 있는지 여부를 결정합니다. |
| [!UICONTROL 판매 중지 권한] | [!UICONTROL 쓰기 권한 - 판매 중지] | 사용자가 새 판매 중지 요청을 만들 수 있는지 여부를 결정합니다. |

{style="table-layout:auto"}

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

이전에는 기술 계정에 통합 및 권한에 대한 제품 프로필이 필요하지 않았습니다. 그러나 Privacy Service 권한이 최근 개선되어 이제 레거시 API 자격 증명을 제품 프로필에 마이그레이션해야 합니다. 이 업데이트를 통해 기술 계정 담당자에게 세부 권한을 부여할 수 있습니다. Privacy Service에 대한 기술 계정 권한을 업데이트하려면 아래 제공된 단계를 따르십시오.

#### 기술 계정 권한 업데이트 {#update-tech-account-permissions}

기술 계정에 대한 권한 집합을 할당하는 첫 번째 단계는 로 이동하는 것입니다. [Adobe Admin Console](https://adminconsole.adobe.com/) Privacy Service을 위한 새 제품 프로필을 만듭니다.

Admin Console UI에서 **제품** 탐색 모음에서 를 차례로 클릭합니다. **[!UICONTROL Experience Cloud]** 및 **[!UICONTROL Adobe Experience Platform Privacy Service]** 왼쪽 사이드바 다음 [!UICONTROL 제품 프로필] 탭이 나타납니다. 선택 **새 프로필** Privacy Service에 사용할 새 제품 프로필을 만들려면

![새 프로필이 강조 표시된 Adobe Admin Console의 Experience Platform Privacy Service 제품 프로필 탭.](./images/permissions/create-product-profile.png)

다음 [!UICONTROL 새 제품 프로필 만들기] 대화 상자가 나타납니다. 제품 프로필을 만드는 방법에 대한 전체 지침은 [프로필 작성에 대한 UI 안내서](../access-control/ui/create-profile.md).

새 제품 프로필을 저장한 후 [Adobe Developer 콘솔](https://developer.adobe.com/console/home) 해당 제품이나 프로젝트에 로그인합니다. 선택 **[!UICONTROL 프로젝트]** 위쪽 탐색에서 프로젝트 카드가 옵니다.

>[!NOTE]
>
>캐시를 지우고 새 프로젝트가 개발자 콘솔 프로젝트 목록에 나타날 때까지 잠시 기다려야 할 수 있습니다.

프로젝트에 로그인한 후 을(를) 선택합니다. **[!UICONTROL Privacy Service API]** 왼쪽 사이드바에서 통합할 수 있습니다.

![프로젝트 및 Privacy Service API가 강조 표시된 Adobe Developer 콘솔의 프로젝트 탭.](./images/permissions/login-to-dev-console-project.png)

Privacy Service API 통합 대시보드가 나타납니다. 이 대시보드에서 해당 프로젝트와 연결된 제품 프로필을 편집할 수 있습니다. 선택 **[!UICONTROL 제품 프로필 편집]** 프로세스를 시작합니다. 다음 [!UICONTROL API 구성] 대화 상자가 나타납니다.

![Adobe Developer 콘솔에서 제품 프로필 편집이 강조 표시된 Privacy Service API 통합 대시보드](./images/permissions/edit-product-profiles.png)

다음 [!UICONTROL API 구성] 대화 상자에는 현재 서비스에 있는 사용 가능한 제품 프로필이 표시됩니다. 이 프로필은 Admin Console에서 만든 제품 프로필과 관련이 있습니다. 사용 가능한 제품 프로필 목록에서 Admin Console에서 기술 계정에 대해 만든 새 제품 프로필에 대한 확인란을 선택합니다. 이렇게 하면 이 기술 계정이 선택한 제품 프로필의 권한과 자동으로 연결됩니다. 선택 **[!UICONTROL 구성된 API 저장]** 설정을 확인합니다.

>[!NOTE]
>
>기술 계정이 이미 제품 프로필과 연결된 경우 사용 가능한 제품 프로필 목록의 확인란 중 하나가 이미 선택됩니다.

![제품 프로필 확인란과 구성된 API 저장 을 강조 표시한 Adobe Developer Console의 API 구성 대화 상자](./images/permissions/select-profile-for-tech-account.png)

#### 설정이 적용되었는지 확인합니다 {#confirm-applied-settings}

설정이 계정에 적용되었는지 확인하려면 로 돌아갑니다. [Admin Console](https://adminconsole.adobe.com/) 새로 만든 제품 프로필로 이동합니다. 을(를) 선택합니다 **[!UICONTROL API 자격 증명]** 탭하여 관련 프로젝트 목록을 확인합니다. 개발자 콘솔에 제품 프로필을 기술 계정에 할당한 프로젝트가 자격 증명 목록에 표시됩니다. 각 API 자격 증명의 이름은 끝에 허용되는 임의로 생성된 번호를 가진 프로젝트 이름으로 구성됩니다. 자격 증명을 선택하여 [!UICONTROL 세부 사항] 패널.

![API 자격 증명 탭 및 프로젝트 자격 증명 행이 강조 표시된 Admin Console의 제품 프로필입니다.](./images/permissions/confirm-credentials-in-admin-console.png)

다음 [!UICONTROL 세부 사항] 패널에는 관련 기술 ID, API 키, 생성 및 마지막 수정 날짜 및 관련 Adobe 제품을 포함한 API 자격 증명에 대한 정보가 포함되어 있습니다.

![Admin Console 내에서 API 자격 증명의 강조 표시된 세부 사항 패널.](./images/permissions/admin-console-details-panel.png)

## 다음 단계

이 안내서에서는 Privacy Service에 사용할 수 있는 권한과 Admin Console을 통해 관리하는 방법에 대해 다룹니다.

제품 프로필을 설정한 후 새 API 통합을 만드는 방법에 대한 단계는 다음을 참조하십시오. [Privacy Service API에 대한 시작 안내서](./api/getting-started.md). 다른 Adobe Experience Platform 기능에 대한 권한 관리에 대한 자세한 내용은 [액세스 제어 설명서](../access-control/home.md).
