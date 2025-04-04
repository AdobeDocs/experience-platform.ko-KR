---
keywords: Experience Platform;홈;인기 항목;액세스 제어;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI에 대한 액세스 제어
description: 이 문서에서는 기여도 AI의 속성 기반 액세스 제어에 대한 정보를 제공합니다.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Attribution AI의 액세스 제어

기여도 AI에 대한 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com/)의 Adobe Experience Platform을 통해 제공됩니다. 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다.

액세스 제어에 대한 자세한 내용은 [액세스 제어 개요](../../../access-control/home.md)를 참조하십시오.

## 속성 기반 액세스 제어

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 제한된 릴리스에서만 사용할 수 있습니다.

[특성 기반 액세스 제어](../../../access-control/abac/overview.md)는 관리자가 특성을 기반으로 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있도록 해주는 Adobe Experience Platform의 기능입니다. 속성은 스키마 필드 또는 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위해 속성이 포함된 액세스 정책을 정의합니다.

이 기능을 사용하면 XDM(Experience Data Model) 스키마 필드에 조직 또는 데이터 사용 범위를 정의하는 레이블로 레이블을 지정할 수 있습니다. 이와 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 또한 속성 기반 액세스 제어를 통해 관리자는 특정 세그먼트에 대한 액세스를 관리할 수 있습니다.

속성 기반 액세스 제어를 통해 관리자는 모든 Experience Platform 워크플로 및 리소스에서 중요한 개인 데이터(SPD)와 개인 식별 정보(PII) 모두에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

속성 기반 액세스 제어로 인해 일부 필드 및 기능은 액세스가 제한되어 특정 Attribution AI 서비스 모델에 사용할 수 없을 수 있습니다. 예를 들면 &quot;ID&quot;, &quot;점수 정의&quot; 및 &quot;복제&quot;가 있습니다.

Attribution AI 작업 영역 **인사이트 페이지**&#x200B;의 맨 위에서 사이드바에 표시되는 세부 정보에 대한 액세스가 제한됩니다.

![제한된 스키마 필드가 강조 표시된 Attribution AI 작업 영역입니다.](../images/user-guide/access-restricted.png)

**[!UICONTROL 모델 워크플로 만들기]** 페이지에서 제한된 스키마가 있는 데이터 집합을 선택하면 데이터 집합 이름 옆에 [!UICONTROL 제한된 정보가 제외됨] 메시지가 있는 경고 기호가 나타납니다.

![제한된 데이터 세트 필드가 강조 표시된 Attribution AI 작업 영역입니다.](../images/user-guide/restricted-info-excluded.png)

**[!UICONTROL 모델 워크플로 만들기]** 페이지에서 제한된 스키마가 있는 데이터 집합을 미리 보면 [!UICONTROL 액세스 제한으로 인해 특정 정보가 데이터 집합 미리 보기에 표시되지 않습니다.]

![제한된 미리 보기 스키마 필드의 결과가 강조 표시된 Attribution AI 작업 영역입니다.](../images/user-guide/restricted-dataset-preview.png)

제한된 정보가 있는 모델을 만들고 **[!UICONTROL 목표 정의]** 단계로 진행하면 맨 위에 경고가 표시됩니다. [!UICONTROL 액세스 제한으로 인해 특정 정보가 구성에 표시되지 않습니다.]

![모델 결과의 제한된 필드가 강조 표시된 Attribution AI 작업 영역입니다.](../images/user-guide/information-not-displayed-save-and-exit.png)

## 다음 단계

이 안내서를 읽으면 [!DNL Experience Platform]에서 액세스 제어의 주요 원칙에 대해 알아보게 됩니다. 이제 [!DNL Admin Console]을(를) 사용하여 제품 프로필을 만들고 [!DNL Experience Platform]에 대한 권한을 할당하는 방법에 대한 자세한 단계를 보려면 [액세스 제어 사용 안내서](../overview.md)로 계속할 수 있습니다.
