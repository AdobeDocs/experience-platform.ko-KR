---
keywords: Experience Platform;홈;인기 항목;액세스 제어;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Attribution AI 액세스 제어
description: 이 문서에서는 Attribution AI에 대한 속성 기반 액세스 제어에 대한 정보를 제공합니다.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# 액세스 제어

Attribution AI에 대한 액세스 제어는 [Adobe Admin Console](https://adminconsole.adobe.com/). 이 기능은 사용 권한 및 샌드박스를 사용자와 연결하는 Admin Console의 제품 프로필을 활용합니다.

액세스 제어에 대한 자세한 내용은 [액세스 제어 개요](../../access-control/home).

## 속성 기반 액세스 제어

>[!IMPORTANT]
>
>속성 기반 액세스 제어는 현재 제한된 릴리스에서만 사용할 수 있습니다.

[속성 기반 액세스 제어](../../../help/access-control/abac/overview.md) 는 관리자가 속성을 기반으로 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있도록 해주는 Adobe Experience Platform의 기능입니다. 속성은 스키마 필드나 세그먼트에 추가된 레이블과 같이 객체에 추가된 메타데이터일 수 있습니다. 관리자는 사용자 액세스 권한을 관리하기 위한 속성을 포함하는 액세스 정책을 정의합니다.

이 기능을 사용하면 조직 또는 데이터 사용 범위를 정의하는 레이블을 사용하여 XDM(Experience Data Model) 스키마 필드에 레이블을 지정할 수 있습니다. 동시에 관리자는 사용자 및 역할 관리 인터페이스를 사용하여 XDM 스키마 필드를 둘러싼 액세스 정책을 정의하고 사용자 또는 사용자 그룹(내부, 외부 또는 타사 사용자)에 부여된 액세스를 더 잘 관리할 수 있습니다. 또한 속성 기반 액세스 제어를 사용하여 관리자가 특정 세그먼트에 대한 액세스를 관리할 수 있습니다.

속성 기반 액세스 제어를 통해 관리자는 모든 플랫폼 워크플로우 및 리소스에서 중요한 SPD(개인 데이터)와 PII(개인 식별 정보)에 대한 사용자의 액세스를 제어할 수 있습니다. 관리자는 해당 필드에 해당하는 특정 필드 및 데이터에만 액세스할 수 있는 사용자 역할을 정의할 수 있습니다.

특성 기반 액세스 제어로 인해 일부 필드 및 기능에는 액세스가 제한되어 특정 Attribution AI 서비스 모델에 사용할 수 없을 수 있습니다. 예를 들면 &quot;Identity&quot;, &quot;Score Definition&quot; 및 &quot;Clone&quot;이 있습니다.

Attribution AI 작업 공간 상단에서 **통찰력 페이지**&#x200B;로 지정하는 경우, 사이드바에 표시되는 세부 정보는 액세스가 제한되었습니다.

![제한된 스키마 필드가 강조 표시된 Attribution AI 작업 영역입니다.](./images/user-guide/access-restricted.png)

에서 제한된 스키마가 있는 데이터 세트를 선택하는 경우 **[!UICONTROL 모델 만들기 워크플로우]** 페이지가 표시되면 메시지가 있는 데이터 세트 이름 옆에 경고 기호가 나타납니다. [!UICONTROL 제한된 정보는 제외됩니다].

![제한된 데이터 세트 필드가 강조 표시된 Attribution AI 작업 공간입니다.](./images/user-guide/restricted-info-excluded.png)

에서 제한된 스키마가 있는 데이터 세트를 미리 볼 때 **[!UICONTROL 모델 만들기 워크플로우]** 페이지를 보면 [!UICONTROL 액세스 제한 사항으로 인해 데이터 집합 미리 보기에 특정 정보가 표시되지 않습니다.]

![제한된 미리 보기 스키마 필드 결과가 강조 표시된 Attribution AI 작업 영역입니다.](./images/user-guide/restricted-dataset-preview.png)

제한된 정보로 모델을 만든 후 **[!UICONTROL 목표 정의]** 단계에서 경고가 맨 위에 표시됩니다. [!UICONTROL 액세스 제한 사항으로 인해 구성에 특정 정보가 표시되지 않습니다.]

![모델의 제한된 필드가 포함된 Attribution AI 작업 영역이 강조표시됩니다.](./images/user-guide/information-not-displayed-save-and-exit.png)

## 다음 단계

이 안내서를 읽으면에서 액세스 제어의 주요 원리를 소개합니다 [!DNL Experience Platform]. 이제 다음을 계속 수행할 수 있습니다. [액세스 제어 사용 안내서](./ui/overview.md) 를 사용하는 방법에 대한 자세한 단계 [!DNL Admin Console] 제품 프로필을 만들고 권한을 할당합니다. [!DNL Platform].
