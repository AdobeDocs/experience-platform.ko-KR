---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 역할 권한 관리
description: 이 문서에서는 Adobe Experience Cloud의 권한 인터페이스를 통해 역할에 대한 권한을 구성하는 방법에 대해 설명합니다
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 7c44683c8110d78654baba4bc53f2c3c2daf2831
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 6%

---

# 역할에 대한 권한 관리

>[!IMPORTANT]
>
>액세스 컨트롤은 권한 부여에 사용자 ID(사용자에게 할당된 내부 고유 ID)를 사용합니다. 조직이 Adobe ID에서 Business ID로 마이그레이션되면 사용자 ID가 변경되고 액세스 제어가 새로 생성된 사용자 ID를 사용하게 되므로 해당 사용자에 대해 설정된 모든 권한이 손실됩니다. 조직이 Business ID로 마이그레이션되는 경우 Adobe 담당자에게 문의하여 사용자 ID를 Adobe ID에서 Business ID로 마이그레이션하십시오.

권한은 관리자가 사용자 역할과 액세스 정책을 정의하여 제품 애플리케이션 내의 기능 및 개체에 대한 액세스 권한을 관리할 수 있는 Experience Cloud 영역입니다.

 권한을 통해 역할을 만들고 관리하며, 이러한 역할에 대해 원하는 리소스 권한을 지정할 수 있습니다. 또한 권한을 사용하여 레이블, 샌드박스 및 특정 역할과 연관된 사용자를 관리할 수 있습니다.

의 바로 뒤에 [새 역할 만들기](#create-a-new-role), (으)로 돌아갑니다 **[!UICONTROL 역할]** 탭. 기존 역할에 대한 권한을 편집하는 경우 **[!UICONTROL 역할]** 탭. 또는 필터 옵션을 사용하여 결과를 필터링하여 역할을 찾습니다.

## 역할 필터링

단계 아이콘(![필터 아이콘](../../images/icon.png)) 필터 컨트롤 목록을 표시하여 결과의 범위를 좁힐 수 있습니다.

![flac 필터](../../images/flac-ui/flac-filters.png)

UI의 역할에 사용할 수 있는 필터는 다음과 같습니다.

| 필터 | 설명 |
| --- | --- |
| [!UICONTROL 다음 기간 동안 생성됨] | 시작 날짜 및/또는 종료 날짜를 선택하여 결과를 필터링할 날짜 범위를 정의합니다. |
| [!UICONTROL 작성자] | 드롭다운에서 사용자를 선택하여 역할 생성자별로 필터링합니다. |
| [!UICONTROL 다음 기간 동안 수정됨] | 시작 날짜 및/또는 종료 날짜를 선택하여 결과를 필터링할 날짜 범위를 정의합니다. |
| [!UICONTROL 수정한 사람] | 드롭다운에서 사용자를 선택하여 역할 수정자로 필터링합니다. |

필터를 제거하려면 해당 필터의 알약 아이콘에서 &quot;X&quot;를 선택하거나 을 선택합니다 **[!UICONTROL 모두 지우기]** 모든 필터를 제거합니다.

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## 역할 세부 정보

에서 역할 선택 **[!UICONTROL 역할]** 탭으로 전환하면 역할의 세부 정보 페이지가 열립니다.

![flac-details](../../images/flac-ui/flac-details.png)

세부 정보 탭에서는 역할에 대한 개요를 제공합니다. 개요에는 역할 이름, 역할 설명, 역할을 만들고 수정한 사용자의 이름, 역할을 만들고 수정한 시기 및 역할에 첨부된 권한이 표시됩니다. 필요한 경우 역할 이름 및 역할 설명을 수정할 수 있습니다.

## 역할에 대한 레이블 관리

다음 항목 선택 **[!UICONTROL 레이블]** 탭을 사용하여 역할 레이블 페이지를 연 다음, **[!UICONTROL 레이블 추가]** 을 눌러 역할에 레이블을 지정합니다.

![flac 레이블](../../images/flac-ui/flac-labels.png)

이 페이지에는 레이블이 나열됩니다. 이 목록에는 레이블 이름, 친숙한 이름, 범주 및 해당 설명이 표시됩니다.

역할에 추가할 목록에서 레이블을 선택한 다음 을(를) 선택합니다 **[!UICONTROL 저장]**

![flac 추가 레이블](../../images/flac-ui/flac-add-labels.png)

추가된 레이블은 아래에 표시됩니다. **[!UICONTROL 레이블]** 탭.

![flac 추가 레이블](../../images/flac-ui/flac-added-labels.png)

역할에서 레이블을 제거하려면 **X** 아이콘 레이블 이름 옆에 있습니다.

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 역할에 대한 샌드박스 관리

다음 항목 선택 **[!UICONTROL 샌드박스]** 탭하여 역할 샌드박스 페이지를 엽니다. 여기에 역할에 추가된 샌드박스 목록이 표시됩니다.

![flac-sandbox](../../images/flac-ui/flac-sandboxes.png)

역할에 샌드박스를 더 추가하려면 을 선택합니다. **[!UICONTROL 편집]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

다음 화면에서는 드롭다운을 사용하여 역할에 포함할 샌드박스에 있는 리소스 권한을 선택하라는 메시지가 표시됩니다. 완료되면 다음을 선택합니다. **[!UICONTROL 저장 및 종료]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 역할에 대한 사용자 관리

다음 항목 선택 **[!UICONTROL 사용자]** 탭을 눌러 [롤 사용자] 페이지를 연 다음 을 선택합니다. **[!UICONTROL 사용자 추가]** 을 눌러 역할에 사용자를 할당합니다.

![flac 사용자](../../images/flac-ui/flac-users.png)

목록에서 역할에 추가할 사용자를 선택합니다. 또는 검색 창을 사용하여 이름이나 이메일 주소를 입력한 다음 을(를) 선택하여 사용자를 검색합니다. **[!UICONTROL 저장]**

![flac 추가 사용자](../../images/flac-ui/flac-add-users.png)

추가된 사용자는 아래에 표시됩니다. **[!UICONTROL 사용자]** 탭.

![flac 추가 사용자](../../images/flac-ui/flac-added-users.png)

역할에서 사용자를 제거하려면 **X** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

## 역할에 대한 API 자격 증명 관리 {#manage-api-credentials-for-role}

다음 항목 선택 **[!UICONTROL API 자격 증명]** 탭을 사용하여 역할 API 자격 증명 페이지를 연 다음 를 선택합니다 **[!UICONTROL API 자격 증명 추가]** 을 눌러 역할에 API 자격 증명을 할당할 수 있습니다.

![flac-api-자격 증명](../../images/flac-ui/flac-api-credentials.png)

역할에 추가할 목록에서 API 자격 증명을 선택한 다음 를 선택합니다 **[!UICONTROL 저장]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

추가된 API 자격 증명은 **[!UICONTROL API 자격 증명]** 탭.

![flac-added-api-credential](../../images/flac-ui/flac-added-api-credentials.png)

역할에서 API 자격 증명을 제거하려면 **X** 아이콘 API 자격 증명 이름 옆에 있습니다.

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

다음 **[!UICONTROL API 자격 증명 제거]** 대화 상자가 나타나고 삭제를 확인하는 메시지가 표시됩니다.

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

(으)로 반환됩니다. **[!UICONTROL API 자격 증명]** 탭.

## 역할에 대한 사용자 그룹 관리

사용자 그룹은 함께 그룹화된 여러 사용자이며 동일한 기능을 실행할 수 있는 액세스 권한을 갖습니다.

다음 항목 선택 **[!UICONTROL 사용자 그룹]** 탭을 눌러 [롤 사용자 그룹] 페이지를 연 다음 을 선택합니다 **[!UICONTROL 그룹 추가]** 사용자 그룹을 역할에 할당할 수 있습니다.

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

역할에 추가할 목록에서 사용자 그룹을 선택합니다. 또는 검색 창을 사용하여 그룹 이름을 입력한 다음 을 선택하여 사용자 그룹을 검색합니다. **[!UICONTROL 저장]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

추가된 사용자 그룹은 **[!UICONTROL 사용자 그룹]** 탭.

![flac 추가된 사용자 그룹](../../images/flac-ui/flac-added-user-groups.png)

역할에서 사용자 그룹을 제거하려면 **X** 아이콘 을 클릭하여 제품에서 사용할 수 있습니다.

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

다음 **[!UICONTROL 사용자 그룹 제거]** 대화 상자가 나타나고 삭제를 확인하는 메시지가 표시됩니다.

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

(으)로 반환됩니다. **[!UICONTROL 사용자 그룹]** 탭.

## 제품 프로필을 통해 Experience Platform에 사용자 추가

제품 프로필에 사용자를 추가하려면 Admin Console에 로그인한 다음 **[!UICONTROL 사용자 추가]**&#x200B;를 선택합니다

![product-profile-add-user](../../images/flac-ui/product-profile-add-users.png)

다음 **[!UICONTROL 팀에 사용자 추가]** 대화 상자가 나타납니다. 사용자 이메일 주소, 이름(선택 사항) 및 성(선택 사항)을 입력합니다.

연필 아이콘을 선택하여 제품 및 사용자 그룹을 선택하고 **[!UICONTROL Adobe Experience Platform]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL AEP-Default-All-Users]**&#x200B;을 선택한 다음 을 선택합니다.  **[!UICONTROL 저장]**.

![product-profile](../../images/flac-ui/product-profile.png)

## 다음 단계

권한이 설정되면 다음 단계로 이동하여 [사용자 관리](users.md).
