---
keywords: Experience Platform;사용 안내서;고객 ai;인기 주제;액세스 제어;모델 만들기;
solution: Experience Platform
feature: Customer AI
title: 고객 AI에 대한 액세스 제어
description: 이 문서에서는 고객 AI의 속성 기반 액세스 제어에 대한 정보를 제공합니다.
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# 고객 AI의 속성 기반 액세스 제어

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 제한된 릴리스에서만 사용할 수 있습니다.

[속성 기반 액세스 제어](../../../access-control/abac/overview.md) 는 관리자가 속성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있도록 해주는 Adobe Experience Platform의 기능입니다. 속성은 스키마 필드 또는 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위해 속성이 포함된 액세스 정책을 정의합니다.

이 기능을 사용하면 XDM(Experience Data Model) 스키마 필드에 조직 또는 데이터 사용 범위를 정의하는 레이블로 레이블을 지정할 수 있습니다. 이와 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 또한 속성 기반 액세스 제어를 통해 관리자는 특정 세그먼트에 대한 액세스를 관리할 수 있습니다.

속성 기반 액세스 제어를 통해 조직 관리자는 모든 플랫폼 워크플로 및 리소스에서 중요한 개인 데이터(SPD)와 개인 식별 정보(PII) 모두에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 특정 필드 및 해당 필드에 해당하는 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

속성 기반 액세스 제어로 인해 일부 필드 및 기능은 액세스가 제한되고 특정 고객 AI 서비스 모델에서 사용할 수 없습니다. 예를 들면 &quot;ID&quot;, &quot;점수 정의&quot; 및 &quot;복제&quot;가 있습니다.

![서비스 모델 결과의 제한된 필드가 강조 표시된 Customer AI 작업 영역입니다.](../images/user-guide/unavailable-functionalities.png)

Customer AI 작업 영역의 맨 위 **insights 페이지**, 사이드바, 점수 정의, id 및 프로필 속성의 세부 정보에 모두 &quot;액세스 제한됨&quot;이 표시됩니다.

![스키마의 제한된 필드가 강조 표시된 Customer AI 작업 영역](../images/user-guide/access-restricted.png)

에서 제한된 스키마를 사용하여 데이터 세트를 미리 볼 때 **[!UICONTROL 모델 워크플로우 만들기]** 페이지를 가리키면 다음과 같은 경고가 표시됩니다 [!UICONTROL 액세스 제한으로 인해 특정 정보가 데이터 세트 미리 보기에 표시되지 않습니다.]

![제한된 스키마 결과가 강조 표시된 미리보기 데이터 세트의 제한된 필드가 있는 Customer AI 작업 공간.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

제한된 정보가 있는 모델을 만든 후 **[!UICONTROL 목표 정의]** 단계: 맨 위에 경고가 표시됩니다. [!UICONTROL 액세스 제한으로 인해 특정 정보가 구성에 표시되지 않습니다.]

![서비스 모델 결과의 제한된 필드가 강조 표시된 Customer AI 작업 영역입니다.](../images/user-guide/information-not-displayed-save-and-exit.png)

액세스 제어를 사용할 때 **고객 AI 보기** 및 **고객 AI 관리** 권한은 고객 AI의 다양한 기능에 대한 액세스 권한을 부여합니다. 다음 **고객 AI 관리** 권한을 사용하면 다음 작업을 수행할 수 있습니다. **만들기**,**업데이트**, **삭제**, **활성화**, 또는 **disable** 모델 기간 **고객 AI 보기** 읽거나 볼 수 있습니다. 다음 **만들기**, **업데이트** 및 **삭제** 작업은 감사 로그로 기록됩니다.

자세한 내용은 설명서 를 참조하십시오 [액세스 제어에 대한 권한 할당](../../../access-control/home.md) 또는 방법 [감사 로그를 사용하여 액세스 및 활동 모니터링](../../../landing/governance-privacy-security/audit-logs/overview.md).

## 다음 단계

이 안내서를 읽으면에서 액세스 제어의 주요 원칙을 소개합니다 [!DNL Experience Platform]. 이제 을(를) 계속할 수 있습니다. [액세스 제어 사용 안내서](../overview.md) 를 사용하는 방법에 대한 자세한 단계는 [!DNL Admin Console] 제품 프로필을 만들고 다음에 대한 권한을 할당하려면 [!DNL Platform].
