---
title: 속성 기반 액세스 제어 권한 관리자
description: 보고서를 생성하고 액세스 권한을 확인하는 Adobe Experience Platform의 권한 관리자를 사용하는 방법을 알아봅니다.
source-git-commit: 3f2a899705d2c05b12300b6d5b0b860ad2c05bfd
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# 권한 관리자

>[!NOTE]
>
>[!UICONTROL 권한 관리자]에 액세스하려면 제품 관리자여야 합니다. 관리자 권한이 없는 경우 시스템 관리자에게 문의하여 액세스 권한을 받으십시오.

[!UICONTROL 권한 관리자]에서 간단한 쿼리를 사용하여 액세스 관리를 이해하고 여러 워크플로우 및 세부 기간 수준에서 액세스 권한을 확인하는 데 걸리는 시간을 절약할 수 있는 간결한 보고서를 만드십시오. [!UICONTROL 권한 관리자]를 사용하여 사용자 그룹에 속하고 지정된 액세스 권한을 가진 사용자와 특정 레이블을 가진 역할을 찾을 수 있습니다.

## 지정된 사용자 그룹 내에서 사용자 검색 수행 {#search-users}

>[!CONTEXTUALHELP]
>id="platform_permission_manager"
>title="권한 관리자"
>abstract="페이지의 드롭다운 선택기를 사용하여 사용자 및 역할에 대해 서로 다른 세부 기간 수준의 액세스 수준 보고서를 가져옵니다."
<!-- >additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-manager/permissions.html" text="Permission manager" -->

드롭다운을 사용하여 **[!UICONTROL 사용자]** 특성을 선택합니다.

![특성 드롭다운에서 사용자를 강조 표시합니다.](../../images/permission-manager/users-select.png)

그런 다음 드롭다운을 사용하여 검색할 **[!UICONTROL 사용자 그룹]**&#x200B;을(를) 선택합니다.

>[!INFO]
>
>[!UICONTROL 사용자 그룹]은(는) 필수 필드가 아닙니다. 각 보고서에 대해 하나의 사용자 그룹만 선택할 수 있습니다.

![사용자 그룹 드롭다운이 강조 표시되었습니다.](../../images/permission-manager/user-group-select.png)

보다 세분화된 보고서의 경우 특정 샌드박스의 작업에서 리소스를 지정할 수 있습니다. 드롭다운을 사용하여 **[!UICONTROL 리소스]**, **[!UICONTROL 작업]** 및 **[!UICONTROL 샌드박스]**&#x200B;를 선택한 다음 **[!UICONTROL 결과 표시]**&#x200B;를 선택합니다.

>[!INFO]
>
>[!UICONTROL 리소스], [!UICONTROL 작업] 및 [!UICONTROL 샌드박스]는 필수 필드가 아닙니다. 각 보고서에 대해 하나의 [!UICONTROL 리소스]만 선택할 수 있습니다. 제거할 선택 항목 옆의 **&#39;x&#39;**&#x200B;을(를) 선택하여 작업 또는 샌드박스를 추가한 후 제거할 수 있습니다.

![리소스, 작업, 샌드박스 드롭다운 및 강조 표시된 결과 표시](../../images/permission-manager/users-additional-attributes-select.png)

사용자 목록과 사용자 이메일 주소는 선택한 기준에 따라 보고됩니다. 왼쪽의 필터 메뉴를 사용하여 속성 및 결과를 업데이트합니다. 특정 사용자에 대한 자세한 내용을 보려면 목록에서 사용자 이름을 선택합니다.

![강조 표시된 특성을 기반으로 생성된 보고서](../../images/permission-manager/users-report.png)

## 특정 레이블이 있는 역할 검색 {#search-roles}

드롭다운을 사용하여 **[!UICONTROL 역할]** 특성을 선택합니다.

>[!INFO]
>
>[!UICONTROL 레이블]은(는) 필수 필드가 아닙니다. 여러 레이블을 선택할 수 있으며, 선택하면 이 드롭다운 아래에 나열됩니다. 작업 옆의 **&#39;x&#39;**&#x200B;을(를) 선택하여 레이블을 추가하면 제거할 수 있습니다.

![역할을 강조 표시하는 특성 드롭다운입니다.](../../images/permission-manager/roles-select.png)

그런 다음 드롭다운을 사용하여 검색할 **[!UICONTROL 레이블]**&#x200B;을 선택합니다.

![강조 표시된 레이블 드롭다운입니다.](../../images/permission-manager/roles-labels-select.png)

보다 세분화된 보고서의 경우 특정 샌드박스의 작업에서 리소스를 지정할 수 있습니다. 드롭다운을 사용하여 **[!UICONTROL 리소스]**, **[!UICONTROL 작업]** 및 **[!UICONTROL 샌드박스]**&#x200B;를 선택한 다음 **[!UICONTROL 결과 표시]**&#x200B;를 선택합니다.

>[!INFO]
>
>[!UICONTROL 리소스], [!UICONTROL 작업] 및 [!UICONTROL 샌드박스]는 필수 필드가 아닙니다. 각 보고서에 대해 하나의 [!UICONTROL 리소스]만 선택할 수 있습니다. 제거할 선택 항목 옆의 **&#39;x&#39;**&#x200B;을(를) 선택하여 작업 또는 샌드박스를 추가한 후 제거할 수 있습니다.

![리소스, 작업, 샌드박스 드롭다운 및 강조 표시된 결과 표시](../../images/permission-manager/roles-additional-attributes-select.png)

선택한 기준에 따라 역할 목록이 보고됩니다. 왼쪽의 필터 메뉴를 사용하여 속성 및 결과를 업데이트합니다. 특정 역할에 대한 자세한 내용을 보려면 목록에서 역할을 선택합니다.

기준에 일치하는 각 역할에 대해 다음 정보가 표시됩니다.

| 속성 | 설명 |
| --- | --- |
| 설명 | 역할에 대한 간략한 설명. |
| 레이블 | 역할과 연결된 레이블 목록입니다. |
| 샌드박스 | 이 역할을 포함하는 Sanbox 목록입니다. |
| 수정된 위치 | 역할이 마지막으로 업데이트된 날짜 및 타임스탬프입니다. |
| 생성된 위치 | 역할을 만든 날짜 및 타임스탬프입니다. |
| 제작자 | 역할 작성자에 대한 세부 정보. |

![강조 표시된 특성을 기반으로 생성된 보고서](../../images/permission-manager/roles-report.png)

## 다음 단계

이제 사용자 및 역할에 대한 보고서를 생성하는 방법을 배웠습니다. 특성 기반 액세스 제어에 대한 자세한 내용은 [특성 기반 액세스 제어 개요](../overview.md)를 참조하세요.
