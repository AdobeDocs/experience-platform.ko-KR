---
solution: Experience Platform
title: Experience Platform 대시보드에 대한 액세스 권한을 얻고 부여하는 방법
type: Documentation
description: Adobe Admin Console을 사용하여 Experience Platform 대시보드를 보고 편집하고 업데이트할 수 있는 권한을 사용자에게 부여합니다.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f138bb0f1b8d289cc872afc065d31c5e55d4b05c
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 6%

---

# 대시보드에 대한 액세스 권한

사용자에게 대시보드를 보고 편집하고 업데이트할 수 있는 기능을 부여하려면 먼저 권한을 활성화해야 합니다. Adobe Experience Platform에서 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com/). 사용자는 [!DNL Admin Console].

이 문서에서는 대시보드에 사용할 수 있는 사용 가능한 권한에 대한 요약을 제공합니다. 여기에는 대시보드에서 액세스할 수 있는 기능과 사용 가능한 사용자 기능이 포함되어 있습니다. 액세스 권한 획득 및 할당에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md).

## 전제 조건

액세스 제어를 구성하려면 [!DNL Experience Platform]인 경우, 조직에 대한 관리자 권한이 있어야 합니다 [!DNL Experience Platform] 제품 통합. 의 Adobe Help Center 문서를 참조하십시오. [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html) 추가 정보.

## 사용 가능한 대시보드 권한 {#available-permissions}

다음 [!DNL Dashboards] 서비스는 결합될 때 세 가지 권한을 제공하여 [!UICONTROL 프로필], [!UICONTROL 세그먼트], [!UICONTROL 대상], 및 [!UICONTROL 라이선스 사용] Adobe Experience Platform 내의 대시보드 권한은 다음과 같습니다.

| 사용 권한 | 설명 |
|---|---|
| **표준 대시보드 관리** | 이 권한은 **글로벌 읽기 및 쓰기 권한**. 이를 통해 다음을 수행할 수 있습니다 [사용자 지정 위젯 만들기](./customize/custom-widgets.md) 및 [위젯 스키마 편집](./customize/edit-schema.md) 사용 [!UICONTROL 위젯 라이브러리]. |
| **표준 대시보드 보기** | 다음을 제공합니다 **읽기 전용** 기능 [!UICONTROL 프로필], [!UICONTROL 대상], 및 [!UICONTROL 세그먼트] 대시보드 및 Platform의 왼쪽 탐색을 통해 액세스할 수 있습니다. 또한 [!UICONTROL 대시보드] 를 클릭하고 [!UICONTROL 대시보드] 인벤토리 및 통합 탭 |
| **라이선스 사용 대시보드 보기** | 이 권한을 통해 사용자는 **읽기 전용** 액세스 [라이선스 사용 대시보드](./guides/license-usage.md) Experience Platform UI에 포함될 수도 있습니다. |

에는 포함되지 않은 5개의 권한이 있습니다 [!DNL Dashboard] 요구 사항에 따라 필요한 카테고리입니다. 다음 표에서는 Admin Console에서 카테고리 위치를 설명합니다.

>[!IMPORTANT]
>
>둘 다 **[!DNL Manage Standard Dashboards]** 그리고 **[!DNL View Standard Dashboards]** 권한 **필요** 다음에서 &quot;보기&quot; 또는 &quot;관리&quot; 권한 [!DNL Profile Management] 또는 [!DNL Destinations] Admin Console의 카테고리 를 사용하여 Platform UI 내에서 관련 섹션을 활성화합니다.

| 사용 권한 | Admin Console 카테고리 위치 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 액세스 제어 매트릭스

다음 액세스 제어 매트릭스는 필요한 권한과 여러 대시보드 기능에 대한 액세스 관련 기능을 분류합니다. 권한은 맨 위 가로 행에 나열되고 Platform UI 작업 영역은 왼쪽 열에 나열됩니다.

|  | [!UICONTROL 표준 대시보드 보기] 또는 [!UICONTROL 표준 대시보드 관리] | [!UICONTROL 프로필 보기],<br/>[!UICONTROL 세그먼트 보기],<br/> [!UICONTROL 대상 보기] | [!UICONTROL 쿼리 관리] &amp; [!UICONTROL 샌드박스 관리] | [!UICONTROL 라이선스 사용 대시보드 보기] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 을 클릭합니다. | 해당 없음 | **&quot;보기&quot; 또는 &quot;관리&quot; 권한이 필요합니다.** 각 대시보드 | 해당 없음 | 해당 없음 |
| [!DNL Dashboards] 을 클릭합니다. | 활성화됨 | **하나 이상의 필수**. | 해당 없음 | 해당 없음 |
| [!DNL Dashboards] [!DNL Inventory] <br/>(찾아보기 탭) | 활성화됨 | 해당 없음 | 해당 없음 | 해당 없음 |
| [!DNL Dashboards] [!DNL Integrations] 탭 <br/>(Power BI 설치에 사용됨) | 활성화됨 | **하나 이상의 필수** | 해당 없음 | 해당 없음 |
| Power BI 설치 단추 및 워크플로우 | 활성화됨 | 해당 없음 | **필수 여부** | 해당 없음 |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 대시보드 .<br/>위젯 스키마를 편집하고 위젯 사용자 지정을 위한 새로운 특성을 추가하는 기능 | **Manage-standard-dashboard 필수** | **필수(각 대시보드에 대해)** | 해당 없음 | 해당 없음 |
| [!DNL License Usage Dashboard] | 해당 없음 | 해당 없음 | 해당 없음 | 활성화됨 |

{style=&quot;table-layout:auto&quot;}

## 제품 프로필에 권한 추가

위에 제공된 정보를 사용하여 제품 프로필에 적절한 권한을 추가합니다. 에 대한 전체 지침은 설명서를 참조하십시오. [액세스 제어 UI를 통해 권한을 추가하는 방법](../access-control/ui/permissions.md).

권한에 대한 설명은 다음을 참조하십시오 [사용 가능한 권한](#available-permissions) 섹션을 참조하십시오.

>[!NOTE]
>
>모든 사용자에 대해 모든 권한을 활성화할 필요는 없습니다. 조직의 구조에 따라 특정 사용자에 대해 별도의 제품 프로필을 만들고 제한된 액세스(예: 읽기 전용)를 부여할 수 있습니다. 자세한 내용은 제품 프로필의 사용자 관리에 대한 설명서를 참조하십시오 [특정 사용자에 대한 권한을 할당하는 방법](../access-control/ui/users.md).

필요한 액세스 권한을 추가했으면 조직 내의 사용자가 Experience Platform UI 내에서 대시보드를 보고 지정된 권한에 따라 다른 작업을 수행할 수 있습니다.
