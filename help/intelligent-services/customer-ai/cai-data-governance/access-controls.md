---
keywords: Experience Platform;사용 안내서;고객 ai;인기 주제;액세스 제어;모델 작성
solution: Experience Platform
feature: Customer AI
title: 고객 AI에 대한 액세스 제어
description: 이 문서에서는 고객 AI에 대한 속성 기반 액세스 제어에 대한 정보를 제공합니다.
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# 속성 기반 액세스 제어

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 제한된 릴리스에서만 사용할 수 있습니다.

[속성 기반 액세스 제어](../../../access-control/abac/overview.md) 는 관리자가 속성을 기반으로 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있도록 해주는 Adobe Experience Platform의 기능입니다. 속성은 스키마 필드나 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위한 속성을 포함하는 액세스 정책을 정의합니다.

이 기능을 사용하면 조직 또는 데이터 사용 범위를 정의하는 레이블을 사용하여 XDM(Experience Data Model) 스키마 필드에 레이블을 지정할 수 있습니다. 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 또한 속성 기반 액세스 제어를 사용하여 관리자가 특정 세그먼트에 대한 액세스를 관리할 수 있습니다.

특성 기반 액세스 제어를 통해 조직의 관리자는 모든 플랫폼 워크플로우 및 리소스에서 중요한 SPD(개인 데이터)와 PII(개인 식별 정보)에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 해당 필드에 해당하는 특정 필드 및 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

특성 기반 액세스 제어로 인해 일부 필드 및 기능에는 액세스가 제한되고 특정 고객 AI 서비스 모델에 사용할 수 없습니다. 예를 들면 &quot;Identity&quot;, &quot;Score Definition&quot; 및 &quot;Clone&quot;이 있습니다.

![서비스 모델의 제한된 필드가 포함된 Customer AI 작업 공간 결과가 강조 표시됩니다.](../images/user-guide/unavailable-functionalities.png)

고객 AI 작업 공간 맨 위에서 **통찰력 페이지**&#x200B;사이드바, 점수 정의, ID 및 프로필 속성의 세부 사항이 모두 &quot;액세스 제한&quot;으로 표시됩니다.

![스키마의 제한된 필드가 강조 표시된 Customer AI 작업 영역입니다.](../images/user-guide/access-restricted.png)

에서 제한된 스키마가 있는 데이터 세트를 미리 볼 때 **[!UICONTROL 모델 만들기 워크플로우]** 페이지를 보면 [!UICONTROL 액세스 제한 사항으로 인해 데이터 집합 미리 보기에 특정 정보가 표시되지 않습니다.]

![제한된 스키마 결과가 강조 표시된 미리 보기 데이터 세트의 제한된 필드가 포함된 Customer AI 작업 영역입니다.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

제한된 정보로 모델을 만든 후 **[!UICONTROL 목표 정의]** 단계에서 경고가 맨 위에 표시됩니다. [!UICONTROL 액세스 제한 사항으로 인해 구성에 특정 정보가 표시되지 않습니다.]

![서비스 모델의 제한된 필드가 포함된 Customer AI 작업 공간 결과가 강조 표시됩니다.](../images/user-guide/information-not-displayed-save-and-exit.png)

액세스 제어를 사용하는 경우 **고객 AI 보기** 및 **고객 AI 관리** 권한은 고객 AI의 다양한 기능에 대한 액세스 권한을 부여합니다. 다음 **고객 AI 관리** 사용 권한 을 통해 **만들기**,**업데이트**, **delete**, **활성화**, 또는 **disable** 모델 **고객 AI 보기** 이를 읽거나 볼 수 있습니다. 다음 **만들기**, **업데이트** 및 **delete** 작업은 감사 로그에 기록됩니다.

자세한 내용은 설명서 를 참조하십시오 [액세스 제어 권한 할당](../../../help/access-control/home.md) 또는 방법 [감사 로그를 사용하여 액세스 및 활동 모니터링](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## 다음 단계

이 안내서를 읽으면에서 액세스 제어의 주요 원리를 소개합니다 [!DNL Experience Platform]. 이제 다음을 계속 수행할 수 있습니다. [액세스 제어 사용 안내서](./ui/overview.md) 를 사용하는 방법에 대한 자세한 단계 [!DNL Admin Console] 제품 프로필을 만들고 권한을 할당합니다. [!DNL Platform].