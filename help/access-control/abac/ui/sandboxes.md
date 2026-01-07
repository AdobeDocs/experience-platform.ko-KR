---
keywords: Experience Platform;홈;인기 항목;액세스 제어;속성 기반 액세스 제어;ABAC
title: 속성 기반 액세스 제어 관리 샌드박스
description: Adobe Experience Cloud의 권한 인터페이스를 통해 샌드박스를 관리합니다.
exl-id: c21eb319-fc0d-442a-b778-bbfa2d6bb22d
source-git-commit: 8c9503c9923372ef919d485d4ec0e3ebda5a2413
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 16%

---

# 샌드박스 관리 {#mange-sandboxes}

>[!CONTEXTUALHELP]
>id="platform_permissions_sandboxes_about"
>title="샌드박스란 무엇입니까?"
>abstract="샌드박스는 Experience Platform의 단일 인스턴스 내 가상 파티션입니다. 샌드박스 내에서 수행되는 모든 콘텐츠와 작업은 해당 샌드박스에만 국한되며 다른 샌드박스에 영향을 미치지 않습니다. 샌드박스에 대한 액세스는 역할을 통해 관리됩니다."
>additional-url="https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/home" text="샌드박스 개요"

샌드박스는 디지털 경험 애플리케이션의 개발 프로세스를 원활하게 통합하는 단일 Adobe Experience Platform 인스턴스 내의 가상 파티션입니다. 샌드박스 내에서 수행되는 모든 콘텐츠 및 작업은 해당 샌드박스로만 제한되고 다른 샌드박스에는 영향을 주지 않습니다. 샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../../sandboxes/home.md)를 참조하십시오.

## 샌드박스 탐색 {#explore-sandboxes}

샌드박스의 세부 정보 및 관련 역할을 보려면 **[!UICONTROL Permissions]** Adobe Experience Cloud[의 &#x200B;](https://experience.adobe.com/){target="_blank"}(으)로 이동하십시오. 왼쪽 패널의 **[!UICONTROL Sandboxes]** 섹션에서 **[!UICONTROL Resources]** 선택

조직의 샌드박스 목록이 나타납니다. 목록에서 보려는 샌드박스를 선택합니다. 또는 검색 막대에 샌드박스 이름을 입력하여 샌드박스를 검색하거나 필터 아이콘(![필터 아이콘](../../../images/icons/filter.png))을 선택하고 **[!UICONTROL Sandbox Type]** 드롭다운 메뉴를 사용하여 샌드박스를 유형별로 필터링합니다.

![사용 권한 내의 샌드박스 작업 영역입니다.](../../images/ui/sandboxes/sandboxes-overview.png){zoomable="yes"}

>[!NOTE]
>
>권한의 샌드박스 작업 영역에서는 샌드박스 관리 작업을 허용하지 않습니다. 샌드박스를 관리하려면 작업 영역의 오른쪽 상단에서 **[!UICONTROL Open sandbox manager]** 옵션을 선택합니다.

**[!UICONTROL Details]** 탭은 샌드박스에 대한 개요를 제공합니다. 개요에는 샌드박스의 **[!UICONTROL Title]**, **[!UICONTROL Sandbox Name]**, **[!UICONTROL Type]**, **[!UICONTROL Region]**, **[!UICONTROL Modified]** 날짜, **[!UICONTROL Modified by]** 및 **[!UICONTROL Status]**&#x200B;이(가) 표시됩니다.

![샌드박스의 세부 정보 작업 영역입니다.](../../images/ui/sandboxes/sandbox-details.png){zoomable="yes"}

샌드박스가 할당된 역할을 보려면 **[!UICONTROL Roles]** 탭을 선택하십시오. 역할을 선택하면 해당 역할의 작업 영역으로 이동합니다.

<!-- To manage the role's sandboxes, follow the [](./roles.md) guide. -->

![샌드박스의 역할 작업 영역입니다.](../../images/ui/sandboxes/sandbox-roles.png){zoomable="yes"}


## 다음 단계

이제 샌드박스에 대한 세부 정보 및 역할을 보는 방법을 알 수 있습니다. 특성 기반 액세스 제어에 대한 자세한 내용은 [특성 기반 액세스 제어 개요](../overview.md)를 참조하세요.
