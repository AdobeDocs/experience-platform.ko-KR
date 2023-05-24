---
solution: Experience Platform
title: Experience Platform 대시보드에 대한 액세스 권한을 획득 및 부여하는 방법
type: Documentation
description: 사용자에게 Adobe Admin Console을 사용하여 Experience Platform 대시보드를 보고, 편집하고, 업데이트할 수 있는 권한을 부여합니다.
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 6%

---

# 대시보드에 대한 액세스 권한

사용자에게 대시보드를 보고, 편집하고, 업데이트할 수 있는 권한을 부여하려면 먼저 권한을 활성화해야 합니다. Adobe Experience Platform에서 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com/). 사용자는 의 제품 프로필을 통해 권한 및 샌드박스와 연결됩니다. [!DNL Admin Console].

이 문서에서는 액세스 권한을 제공하는 기능 및 활성화 기능을 포함하여 대시보드에 대해 사용 가능한 권한에 대한 요약을 제공합니다. 액세스 권한 획득 및 할당에 대한 자세한 내용은 [액세스 제어 개요](../access-control/home.md).

## 사전 요구 사항

다음에 대한 액세스 제어를 구성하려면 [!DNL Experience Platform], 다음을 보유한 조직에 대한 관리자 권한이 있어야 합니다. [!DNL Experience Platform] 제품 통합. 에 대한 Adobe Help Center 문서 보기 [관리자 역할](https://helpx.adobe.com/enterprise/using/admin-roles.html) 추가 정보.

## 사용 가능한 대시보드 권한 {#available-permissions}

다음 [!DNL Dashboards] 서비스는 결합 시 다음에 대한 전체 액세스를 제공하는 세 가지 권한을 제공합니다. [!UICONTROL 프로필], [!UICONTROL 세그먼트], [!UICONTROL 대상], 및 [!UICONTROL 라이선스 사용] Adobe Experience Platform 내의 대시보드. 이러한 권한은 다음과 같습니다.

| 사용 권한 | 설명 |
|---|---|
| **표준 대시보드 관리** | 이 권한은 **글로벌 읽기 및 쓰기 권한**. 다음을 수행할 수 있습니다. [사용자 정의 위젯 만들기](./customize/custom-widgets.md) 및 [위젯 스키마 편집](./customize/edit-schema.md) 다음을 통해 [!UICONTROL 위젯 라이브러리]. |
| **표준 대시보드 보기** | 다음이 제공됩니다. **읽기 전용** 을 위한 기능 [!UICONTROL 프로필], [!UICONTROL 대상], 및 [!UICONTROL 세그먼트] 대시보드를 허용하고 플랫폼의 왼쪽 탐색을 통해 대시보드에 액세스할 수 있습니다. 또한 다음과 같은 기능이 추가됩니다. [!UICONTROL 대시보드] 왼쪽 탐색 및 액세스 권한 [!UICONTROL 대시보드] 인벤토리 및 통합 탭 |
| **라이선스 사용 대시보드 보기** | 이 권한을 통해 사용자는 **읽기 전용** 액세스 대상: [라이선스 사용량 대시보드](./guides/license-usage.md) Experience Platform UI 내. |

에는 포함되지 않은 5가지 권한이 있습니다. [!DNL Dashboard] 필요에 따라 잠재적으로 필요한 범주. 다음 표에는 Admin Console 내 해당 범주 위치가 간략하게 나와 있습니다.

>[!IMPORTANT]
>
>두 가지 모두 **[!DNL Manage Standard Dashboards]** 및 **[!DNL View Standard Dashboards]** 권한 **필요** 의 &quot;보기&quot; 또는 &quot;관리&quot; 권한 [!DNL Profile Management] 또는 [!DNL Destinations] 카테고리는 Platform UI 내에서 관련 섹션을 활성화하는 Admin Console에 있습니다.

| 사용 권한 | Admin Console 범주 위치 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 액세스 제어 매트릭스

다음 액세스 제어 매트릭스에서는 필요한 권한과 여러 대시보드 기능에 대한 액세스와 관련하여 제공하는 기능에 대한 분류를 제공합니다. 권한은 맨 위 가로 행에 나열되며 Platform UI 작업 영역은 왼쪽 열에 나열됩니다.

|  | [!UICONTROL 표준 대시보드 보기] 또는 [!UICONTROL 표준 대시보드 관리] | [!UICONTROL 프로필 보기],<br/>[!UICONTROL 세그먼트 보기],<br/> [!UICONTROL 대상 보기] | [!UICONTROL 쿼리 관리] 및 [!UICONTROL 샌드박스 관리] | [!UICONTROL 라이선스 사용 대시보드 보기] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 왼쪽 탐색. | 해당 없음 | **&quot;보기&quot; 또는 &quot;관리&quot; 권한이 필요합니다.** 각 대시보드에 대해 | N/A | N/A |
| [!DNL Dashboards] 왼쪽 탐색. | 활성화됨 | **최소 하나 이상 필요**. | N/A | N/A |
| [!DNL Dashboards] [!DNL Inventory] <br/>(찾아보기 탭) | 활성화됨 | N/A | N/A | N/A |
| [!DNL Dashboards] [!DNL Integrations] 탭 <br/>(Power BI 설치에 사용됨) | 활성화됨 | **최소 하나 이상 필요** | N/A | N/A |
| Power BI 설치 단추 및 워크플로 | 활성화됨 | 해당 없음 | **필수** | 해당 없음 |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 대시보드.<br/>위젯 스키마를 편집하고 위젯 사용자 정의를 위한 새 속성을 추가하는 기능 | **관리-표준-대시보드 필수** | **필수(각 대시보드에 대해)** | N/A | N/A |
| [!DNL License Usage Dashboard] | N/A | N/A | N/A | 활성화됨 |

{style="table-layout:auto"}

## 제품 프로필에 권한 추가

위에 제공된 정보를 사용하여 제품 프로필에 적절한 권한을 추가하십시오. 의 전체 지침은 설명서 를 참조하십시오. [액세스 제어 UI를 통해 권한을 추가하는 방법](../access-control/ui/permissions.md).

권한에 대한 설명은 다음을 참조하십시오. [사용 가능한 권한](#available-permissions) 이 문서의 앞부분에 있는 섹션입니다.

>[!NOTE]
>
>모든 사용자에 대해 모든 권한을 활성화할 필요는 없습니다. 조직의 구조에 따라 특정 사용자에 대해 별도의 제품 프로필을 만들고 제한된 액세스 권한(예: 읽기 전용)을 부여할 수 있습니다. 자세한 내용은 제품 프로필의 사용자 관리에 대한 설명서를 참조하십시오 [특정 사용자에 대한 권한을 할당하는 방법](../access-control/ui/users.md).

필요한 액세스 권한을 추가했으면 조직 내의 사용자는 Experience Platform UI 내에서 대시보드를 보기 시작하고, 지정한 권한에 따라 다른 작업을 수행할 수 있습니다.
