---
solution: Experience Platform
title: Experience Platform 대시보드에 대한 액세스 권한을 획득 및 부여하는 방법
type: Documentation
description: 사용자에게 Adobe Admin Console을 사용하여 Experience Platform 대시보드를 보고, 편집하고, 업데이트할 수 있는 권한을 부여합니다.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 6%

---

# 대시보드에 대한 액세스 권한

사용자에게 대시보드를 보고, 편집하고, 업데이트할 수 있는 권한을 부여하려면 먼저 권한을 활성화해야 합니다. Adobe Experience Platform에서는 [Adobe Admin Console](https://adminconsole.adobe.com/)을 통해 액세스 제어를 제공합니다. 사용자가 [!DNL Admin Console]의 제품 프로필을 통해 권한 및 샌드박스와 연결되어 있습니다.

이 문서에서는 액세스 권한을 제공하는 기능 및 활성화 기능을 포함하여 대시보드에 대해 사용 가능한 권한에 대한 요약을 제공합니다. 액세스 권한 획득 및 할당에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md)를 읽는 것부터 시작하십시오.

## 전제 조건

[!DNL Experience Platform]에 대한 액세스 제어를 구성하려면 [!DNL Experience Platform] 제품 통합이 있는 조직에 대한 관리자 권한이 있어야 합니다. 자세한 내용은 [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html)에 대한 Adobe Help Center 문서를 참조하십시오.

## 사용 가능한 대시보드 권한 {#available-permissions}

[!DNL Dashboards] 서비스는 결합할 경우 Adobe Experience Platform 내의 [!UICONTROL 프로필], [!UICONTROL 세그먼트], [!UICONTROL 대상] 및 [!UICONTROL 라이선스 사용] 대시보드에 대한 전체 액세스를 제공하는 세 가지 권한을 제공합니다. 이러한 권한은 다음과 같습니다.

| 사용 권한 | 설명 |
|---|---|
| **표준 대시보드 관리** | 이 권한은 **전역 읽기 및 쓰기 권한**&#x200B;입니다. [!UICONTROL 위젯 라이브러리]를 통해 [사용자 정의 위젯을 만들고](./customize/custom-widgets.md) [위젯 스키마를 편집](./customize/edit-schema.md)할 수 있습니다. |
| **표준 대시보드 보기** | [!UICONTROL 프로필], [!UICONTROL 대상] 및 [!UICONTROL 세그먼트] 대시보드에 대한 **읽기 전용** 기능을 제공하며 플랫폼의 왼쪽 탐색을 통해 해당 대시보드에 액세스할 수 있습니다. 또한 왼쪽 탐색에 [!UICONTROL 대시보드]를 추가하고 [!UICONTROL 대시보드] 인벤토리 및 통합 탭에 액세스합니다. |
| **라이선스 사용 대시보드 보기** | 이 권한을 통해 **읽기 전용** 사용자는 Experience Platform UI 내의 [라이선스 사용 대시보드](./guides/license-usage.md)에 액세스할 수 있습니다. |

[!DNL Dashboard] 범주에 포함되지 않은 5개의 권한은 필요에 따라 필요할 수 있습니다. 다음 표에는 Admin Console 내 해당 범주 위치가 간략하게 나와 있습니다.

>[!IMPORTANT]
>
>**[!DNL Manage Standard Dashboards]** 및 **[!DNL View Standard Dashboards]** 권한 **은(는) 모두 Platform UI 내에서 관련 섹션을 활성화하려면 Admin Console의 [!DNL Profile Management] 또는 [!DNL Destinations] 범주에서 &quot;보기&quot; 또는 &quot;관리&quot; 권한을 필요**&#x200B;합니다.

| 사용 권한 | Admin Console 범주 위치 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 액세스 제어 매트릭스

다음 액세스 제어 매트릭스에서는 필요한 권한과 여러 대시보드 기능에 대한 액세스와 관련하여 제공하는 기능에 대한 분류를 제공합니다. 권한은 맨 위 가로 행에 나열되며 Platform UI 작업 영역은 왼쪽 열에 나열됩니다.

|   | [!UICONTROL 표준 대시보드 보기] 또는 [!UICONTROL 표준 대시보드 관리] | [!UICONTROL 프로필 보기],<br/>[!UICONTROL 세그먼트 보기],<br/> [!UICONTROL 대상 보기] | [!UICONTROL 쿼리 관리] 및 [!UICONTROL 샌드박스 관리] | [!UICONTROL 라이선스 사용 대시보드 보기] |
|---|---|---|---|---|
| 왼쪽 탐색에서 [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations]. | N/A | **각 대시보드에 대해 &quot;보기&quot; 또는 &quot;관리&quot; 권한이 필요합니다**. | N/A | N/A |
| 왼쪽 탐색 영역에 [!DNL Dashboards]이(가) 있습니다. | 활성화됨 | **하나 이상의 필수**. | N/A | N/A |
| [!DNL Dashboards] [!DNL Inventory] <br/>(찾아보기 탭) | 활성화됨 | N/A | N/A | N/A |
| [!DNL Dashboards] [!DNL Integrations] 탭 <br/>(Power BI 설치에 사용됨) | 활성화됨 | **최소 하나 이상 필요** | N/A | N/A |
| Power BI 설치 단추 및 워크플로 | 활성화됨 | N/A | **필수** | N/A |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 대시보드입니다.<br/>위젯 스키마를 편집하고 위젯 사용자 지정을 위한 새 특성을 추가하는 기능 | **관리-표준-대시보드 필요** | **필수(각 대시보드에 대해)** | N/A | N/A |
| [!DNL License Usage Dashboard] | N/A | N/A | N/A | 활성화됨 |

{style="table-layout:auto"}

## 제품 프로필에 권한 추가

위에 제공된 정보를 사용하여 제품 프로필에 적절한 권한을 추가하십시오. [액세스 제어 UI를 통해 권한을 추가하는 방법](../access-control/ui/permissions.md)에 대한 전체 지침은 설명서를 참조하세요.

권한에 대한 설명은 이 문서의 앞부분에 있는 [사용 가능한 권한](#available-permissions) 섹션을 참조하십시오.

>[!NOTE]
>
>모든 사용자에 대해 모든 권한을 활성화할 필요는 없습니다. 조직의 구조에 따라 특정 사용자에 대해 별도의 제품 프로필을 만들고 제한된 액세스 권한(예: 읽기 전용)을 부여할 수 있습니다. [특정 사용자에 대한 권한을 할당하는 방법](../access-control/ui/users.md)을 알아보려면 제품 프로필의 사용자 관리에 대한 설명서를 참조하세요.

필요한 액세스 권한을 추가했으면 조직 내의 사용자는 Experience Platform UI 내에서 대시보드를 보기 시작하고, 지정한 권한에 따라 다른 작업을 수행할 수 있습니다.
