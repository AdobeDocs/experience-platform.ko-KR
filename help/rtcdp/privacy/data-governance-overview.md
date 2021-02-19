---
keywords: 데이터 거버넌스 rtcdp;rtcdp 데이터 거버넌스;실시간 고객 데이터 프로파일 데이터 거버넌스
title: 데이터 거버넌스 개요
seo-title: 실시간 고객 데이터 플랫폼의 데이터 거버넌스
description: '데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. '
seo-description: '데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. '
translation-type: tm+mt
source-git-commit: 5435661d750c4138ea6a2d40619a48236b7b1e4f
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# [!DNL Data Governance] 실시간 CDP 활용

[!DNL Real-time Customer Data Platform] (실시간 CDP) 는 여러 엔터프라이즈 시스템의 데이터를 통합하여 마케터가 고객을 보다 효과적으로 식별, 이해 및 참여시킬 수 있도록 합니다. 이 데이터는 조직 또는 법률 규정에 의해 정의된 사용 제한 사항의 적용을 받을 수 있습니다. 따라서 데이터를 처리할 때 실시간 CDP가 사용 정책을 준수하도록 하는 것이 중요합니다.

Adobe Experience Platform [!DNL Data Governance]을 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. 실시간 CDP에서 중요한 역할을 하는 이 솔루션을 사용하면 사용 정책을 정의하고 해당 정책에 따라 데이터를 분류하고 특정 마케팅 작업을 수행할 때 정책 위반을 확인할 수 있습니다.

실시간 CDP는 Adobe Experience Platform 기반으로 구축되므로 대부분의 [!DNL Data Governance] 기능은 [!DNL Experience Platform] 설명서에서 다룹니다. 이 문서는 [!DNL Experience Platform]에 대한 [데이터 거버넌스 개요](../../data-governance/home.md)를 보완하고 실시간 CDP에서 사용할 수 있는 거버넌스 기능에 대해 간략히 설명합니다. 다음 주제를 다룹니다.

* [데이터에 사용 레이블 적용](#labels)
* [데이터 사용 정책 관리](#policies)
* [데이터 사용 규정 준수](#enforce)

## 데이터 {#labels}에 사용 레이블 적용

[!DNL Data Governance] 데이터 세트 또는 데이터 세트 필드 수준에서 데이터에 사용 레이블을 적용할 수 있습니다. 데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

데이터 사용 레이블 작업에 대한 자세한 내용은 Adobe Experience Platform용 [데이터 사용 레이블 사용자 안내서](../../data-governance/labels/overview.md)를 참조하십시오.

## 대상 {#destinations}에 대한 마케팅 작업 구성

대상에 대한 마케팅 작업(마케팅 사용 사례라고도 함)을 정의하여 대상에 대한 데이터 사용 제한을 설정할 수 있습니다. 대상에 대한 마케팅 작업은 해당 대상으로 내보낼 데이터의 의도를 나타냅니다.

>[!NOTE]
>
>마케팅 작업 및 데이터 사용 정책에 대한 자세한 내용은 [!DNL Experience Platform] 설명서의 [데이터 사용 정책 개요](../../data-governance/policies/overview.md)를 참조하십시오.

대상에 대한 마케팅 작업을 정의하면 해당 대상으로 전송된 프로파일 또는 세그먼트가 데이터 사용 정책을 준수하도록 할 수 있습니다. 따라서 활성화 정책에 대한 제한을 시행해야 하는 조직의 요구를 기반으로 적절한 마케팅 활동을 대상에 추가해야 합니다.

처음 대상을 설정할 때만 마케팅 작업을 선택할 수 있습니다. 작업 중인 대상 유형에 따라 마케팅 작업을 구성할 기회가 설정 워크플로우의 다른 지점에 나타납니다. 특정 대상을 구성하는 방법에 대한 단계는 [대상 설명서](../destinations/overview.md)를 참조하십시오.

## 데이터 사용 정책 관리 {#policies}

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 정의하고 활성화해야 합니다. 데이터 사용 정책은 실시간 CDP 내에서 데이터에 대해 수행하도록 허용되거나 제한된 마케팅 작업의 종류를 설명하는 규칙입니다. 자세한 내용은 [!DNL Experience Platform] [데이터 거버넌스 개요](../../data-governance/home.md)의 &quot;데이터 사용 정책&quot; 섹션을 참조하십시오.

Adobe Experience Platform은 일반적인 고객 경험 사용 사례를 위한 몇 가지 핵심 정책을 제공합니다. 이러한 정책은 **[!UICONTROL 정책]** 작업 영역으로 이동한 다음 **[!UICONTROL 찾아보기]** 탭을 선택하여 UI에서 볼 수 있습니다. 사용자 지정 정책을 만드는 방법을 포함하여 UI에서 정책 작업에 대한 자세한 단계는 [정책 사용 안내서](../../data-governance/policies/user-guide.md)를 참조하십시오.[!DNL Experience Platform]

## 데이터 사용 준수 적용 {#enforce}

데이터가 레이블이 지정되고 사용 정책이 정의된 후에는 데이터 사용 규정을 정책으로 준수할 수 있습니다. 실시간 CDP의 대상에 대상 세그먼트를 활성화할 때 위반이 발생하는 경우 [!DNL Data Governance]은(는) 사용 정책을 자동으로 적용합니다.

자세한 내용은 [자동 정책 적용](../../data-governance/enforcement/auto-enforcement.md)에 있는 문서를 참조하십시오.

## 다음 단계

실시간 CDP의 주요 [!DNL Data Governance] 기능과 [!DNL Experience Platform] 기능 사용 방법을 소개하였으므로 이제 Adobe Experience Platform](../../data-governance/home.md)의 데이터 거버넌스에 대한 [ 설명서를 계속 읽어 보십시오. 이 설명서는 데이터 사용 레이블 및 정책 관리를 위한 단계별 워크플로우뿐만 아니라 필수 [!DNL Data Governance] 개념에 대한 개요를 제공합니다.

다음 비디오에서는 대상에 대한 마케팅 사용 사례 및 다양한 시나리오를 위한 예제 워크플로우를 포함하여 실시간 CDP의 [!DNL Data Governance]에 대한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)