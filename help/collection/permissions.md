---
title: Experience Platform의 데이터 수집을 위한 권한 관리
description: Adobe Experience Platform에서 권한을 관리하고 데이터 수집 기능에 대한 액세스를 제어하는 방법에 대한 높은 수준의 개요입니다.
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 5%

---

# Experience Platform의 데이터 수집을 위한 권한 관리

[Adobe Experience Platform의 데이터 수집](./home.md) 는 데이터를 수집하고 전송하기 위해 함께 작동하는 여러 가지 기술로 구성되어 있습니다. 이러한 기술에 대한 액세스는 Adobe Admin Console에서 세부적인 역할 기반 권한을 통해 제어됩니다.

이 안내서에서는 데이터 수집 기능에 대한 권한을 관리하는 방법을 보여줍니다.

## 시작하기

데이터 수집에 대한 액세스 제어를 구성하려면 Adobe Experience Platform 데이터 수집과 제품 통합이 있는 조직에 대한 관리자 권한이 있어야 합니다. 권한을 부여하거나 취소할 수 있는 최소 역할은 제품 프로필 관리자입니다. 권한을 관리할 수 있는 다른 관리자 역할은 제품 관리자(제품 내의 모든 프로필을 관리할 수 있음)와 시스템 관리자(제한 없음)입니다. 다음 문서를 참조하십시오. [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html) 자세한 내용은 Adobe 엔터프라이즈 관리 안내서 를 참조하십시오.

이 안내서에서는 제품 프로필과 같은 기본 Admin Console 개념 및 개별 사용자 및 그룹에 제품 권한을 부여하는 방법에 대해 잘 알고 있다고 가정합니다. 자세한 내용은 [Admin Console 사용 안내서](https://helpx.adobe.com/kr/enterprise/using/admin-console.html).

## 사용 가능한 권한

데이터 수집에 대한 관련 권한은 Admin Console의 두 제품 지정을 통해 제공됩니다. **Adobe Experience Platform** 및 **Adobe Experience Platform 데이터 수집**. 아래 섹션에서는 각 제품에서 제공하는 권한에 대해 설명하고 액세스 권한을 부여하는 특정 기능에 대한 설명을 제공합니다.

### Adobe Experience Platform 권한

Adobe Experience Platform의 권한에는 데이터 저장소, ID, 스키마 및 샌드박스에 대한 액세스가 포함됩니다. Adobe Experience Platform 권한을 구성하는 방법에 대한 단계는 다음을 참조하십시오. [액세스 제어 사용 안내서](../access-control/ui/overview.md).

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| 샌드박스 | (해당 없음) | 에 따라 [샌드박스](../sandboxes/home.md) 조직 아래에 만들어진 권한은 Admin Console의 이 권한 카테고리를 통해 각 권한에 대한 액세스를 제어할 수 있습니다. |
| 데이터 모델링 | 스키마 관리 | 보고, 만들고, 편집할 수 있는 기능을 부여합니다 [Experience 데이터 모델(XDM) 스키마](../xdm/home.md). |
| 데이터 모델링 | 스키마 보기 | 스키마에 대한 읽기 전용 액세스 권한을 부여합니다. |
| ID 관리 | ID 네임스페이스 관리 | 보고, 만들고, 편집할 수 있는 기능을 부여합니다 [id 네임스페이스](../identity-service/namespaces.md). |
| ID 관리 | ID 네임스페이스 보기 | ID 네임스페이스에 대한 읽기 전용 액세스 권한을 부여합니다. |
| 데이터 수집 | 데이터 스트림 관리 | 보고, 만들고, 편집할 수 있는 기능을 부여합니다 [데이터 세트](../edge/datastreams/overview.md). |
| 데이터 수집 | 데이터 스트림 보기 | 데이터 세트에 대한 읽기 전용 액세스 권한을 부여합니다. |

{style=&quot;table-layout:auto&quot;}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Adobe Experience Platform 데이터 수집 권한

Adobe Experience Platform 데이터 수집의 권한은 속성, 확장 및 환경을 포함하여 태그 및 이벤트 전달 기능에 대한 액세스를 제어합니다. Adobe Experience Platform 데이터 수집 권한을 구성하는 방법에 대한 단계는 다음을 참조하십시오. [아래 섹션](#manage).

| 카테고리 | 사용 권한 | 설명 |
| --- | --- | --- |
| 플랫폼 | 웹 | 액세스 권한 부여 [웹 속성](../tags/ui/administration/companies-and-properties.md) 와 다른 속성 권한이 결합되는 경우입니다. |
| 플랫폼 | 모바일 | 액세스 권한 부여 [모바일 속성](../tags/ui/administration/companies-and-properties.md) 와 다른 속성 권한이 결합되는 경우입니다. |
| 속성 | (해당 없음) | 조직에서 생성한 속성에 따라 Admin Console의 이 권한 카테고리를 통해 각 속성에 대한 액세스를 제어할 수 있습니다.<br><br>사용자가 지정한 속성 권한은 이 권한 카테고리를 통해 액세스 권한이 부여된 속성에만 적용됩니다. |
| 속성 권한 | 승인 | 라이브러리 빌드를 의 일부로 승인할 수 있는 권한을 부여합니다 [게시 흐름](../tags/ui/publishing/publishing-flow.md). |
| 속성 권한 | 개발 | 라이브러리의 일부로 라이브러리 빌드를 개발하는 기능을 부여합니다 [게시 흐름](../tags/ui/publishing/publishing-flow.md). |
| 속성 권한 | 속성 편집 | 사용자가 액세스할 수 있는 속성에 대한 기본 구성을 편집할 수 있는 권한을 부여합니다. |
| 속성 권한 | 환경 관리 | 를 관리할 권한을 부여합니다 [환경](../tags/ui/publishing/environments.md) 의 경우 사용자가 액세스할 수 있는 속성입니다. |
| 속성 권한 | 확장 관리 | 를 관리할 권한을 부여합니다 [확장](../tags/ui/managing-resources/extensions/overview.md) 의 경우 사용자가 액세스할 수 있는 속성입니다. |
| 속성 권한 | 게시 | 라이브러리 빌드를 의 일부로 게시하는 권한을 부여합니다 [게시 흐름](../tags/ui/publishing/publishing-flow.md). |
| 회사 권한 | 확장 개발 | 비공개 릴리스 및 공개 릴리스 요청을 포함하여 조직이 소유한 확장 패키지를 만들고 수정하는 권한을 부여합니다. |
| 회사 권한 | 확장 관리 | 이 권한은 모바일 인앱 및 푸시 메시지에 대한 액세스 권한을 부여하는 Adobe Journey Optimizer 또는 다른 솔루션에 대한 라이센스가 있는 경우에만 적용할 수 있습니다. 이를 통해 Firebase Cloud 메시지 서비스 및 Apple 푸시 알림 서비스와 통신하는 데 필요한 푸시 자격 증명과 함께 Adobe Experience Cloud에서 알고 있는 앱을 관리할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>일반적인 시나리오에 대한 관리 전략 등 이러한 권한이 태그의 기능에 미치는 영향에 대한 자세한 내용은 태그 설명서를 참조하십시오. [사용자 권한](../tags/ui/administration/user-permissions.md).

## 권한 관리 {#manage}

이전 섹션에 요약된 대로 데이터 수집에 대한 권한은 Admin Console의 두 가지 제품 지정을 통해 관리됩니다. **Adobe Experience Platform** 및 **Adobe Experience Platform 데이터 수집**.

이러한 권한을 관리하려면 [Admin Console](https://adminconsole.adobe.com/) 을(를) 선택합니다. **[!UICONTROL 제품]** 위쪽 탐색에서 를 클릭합니다. 여기에서 구성할 권한에 대한 제품 카드를 선택합니다. Admin Console의 각 제품에서 관련 권한을 관리하는 방법에 대한 단계는 아래 하위 섹션을 참조하십시오.

* [Adobe Experience Platform 권한](#manage-platform)
* [Adobe Experience Platform 데이터 수집 권한](#manage-collection)

### Adobe Experience Platform에서 권한 관리 {#manage-platform}

에서 **[!UICONTROL 제품]** Admin Console에서 보기, 선택 **[!UICONTROL Adobe Experience Platform 데이터 수집]**. 권한을 편집할 제품 프로필을 선택한 다음 **[!UICONTROL 권한]** 탭.

데이터 수집 기능에 액세스하려면 **[!UICONTROL 샌드박스]**, **[!UICONTROL 데이터 모델링]**, **[!UICONTROL Identity Management]**, 및 **[!UICONTROL 데이터 수집]** 카테고리.

![Admin Console의 데이터 수집 제품 카드를 보여주는 이미지](./images/permissions/platform-permission-card.png)

자세한 내용은 [access control UI 안내서](../access-control/ui/overview.md) 플랫폼 권한 관리에 대한 자세한 지침입니다.

>[!NOTE]
>
>조직에서 액세스할 수 있는 제품 SKU에 따라 사용 가능한 모든 플랫폼 권한이 없을 수 있습니다.

### Adobe Experience Platform 데이터 수집에서 권한 관리 {#manage-collection}

에서 **[!UICONTROL 제품]** Admin Console에서 보기, 선택 **[!UICONTROL Adobe Experience Platform 데이터 수집]**.

![Admin Console의 데이터 수집 제품 카드를 보여주는 이미지](./images/permissions/data-collection-card.png)

#### 제품 프로필 선택 또는 만들기

다음 화면에는 조직 아래의 데이터 수집에 사용할 수 있는 제품 프로필 목록인 기본 프로필이 **[!DNL Default Data Collection All Access]**. 원할 경우 기본 제품 프로필을 편집하거나 선택할 수 있습니다 **[!UICONTROL 새 프로필]** 만들 수 있습니다. 조직에 서로 다른 수준의 액세스가 필요한 여러 역할이나 사용자 그룹이 있는 경우 각 역할에 대해 별도의 제품 프로필을 만들어야 합니다.

![Admin Console의 데이터 수집에 대한 제품 프로필을 보여주는 이미지](./images/permissions/new-profile.png)

제품 프로필을 선택하거나 만든 후 **[!UICONTROL 편집]** 시작할 아이콘 [권한 편집](#edit-permissions) 프로파일에 대해 를 선택하거나 **[!UICONTROL 사용자]** 시작할 탭 [사용자 할당](#assign-users) 참조하십시오.

![제품 프로필 Admin Console에 대한 권한 탭을 보여주는 이미지](./images/permissions/edit-permission-categories.png)

#### 제품 프로필에 대한 권한 편집 {#edit-permissions}

프로필에 대한 권한을 편집할 때 사용 가능한 권한이 왼쪽 열에 나열되고 프로필에 포함된 권한은 오른쪽 열에 나열됩니다. 두 열 간에 이동할 나열된 권한을 선택합니다.

![포함된 열 아래에 추가된 권한을 보여주는 이미지](./images/permissions/added-permissions.png)

권한은 카테고리로 구성됩니다. 카테고리 간을 전환하려면 왼쪽 탐색에서 원하는 카테고리를 선택합니다.

![사용 권한에 따라 회사 권한 섹션을 표시하는 이미지](./images/permissions/switch-category.png)

선택 **[!UICONTROL 저장]** 권한 구성을 완료하면

![제품 프로필에 대해 저장되는 권한 구성을 보여주는 이미지](./images/permissions/save-permissions.png)

추가된 권한이 반영되면 제품 프로필 보기가 다시 나타납니다.

![제품 프로필에 대해 추가된 권한을 보여주는 이미지](./images/permissions/permissions-added.png)

#### 제품 프로필에 사용자 할당 {#assign-users}

제품 프로필에 사용자를 할당(그리고 프로필에 구성된 권한을 부여)하려면 다음을 선택합니다 **[!UICONTROL 사용자]** 탭, 그 다음 **[!UICONTROL 사용자 추가]**.

![Admin Console에서 제품 프로필에 대한 사용자 탭을 보여주는 이미지](./images/permissions/manage-users.png)

제품 프로필의 사용자 관리에 대한 자세한 내용은 [Admin Console 설명서](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

## 다음 단계

이 안내서에서는 데이터 수집 UI에 사용할 수 있는 권한과 Admin Console을 통해 관리하는 방법에 대해 다룹니다. 다른 Adobe Experience Platform 기능에 대한 권한 관리에 대한 자세한 내용은 [액세스 제어 설명서](../access-control/home.md).
