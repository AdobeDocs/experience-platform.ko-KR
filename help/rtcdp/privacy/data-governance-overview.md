---
keywords: 데이터 거버넌스 rtcdp;rtcdp 데이터 거버넌스;실시간 고객 데이터 프로필 데이터 거버넌스
title: 데이터 거버넌스 개요
description: 데이터 거버넌스를 통해 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Real-Time CDP의 데이터 거버넌스

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)는 여러 엔터프라이즈 시스템의 데이터를 함께 가져와서 마케터가 고객을 더 잘 식별하고, 이해하고, 참여하도록 합니다. 이 데이터에는 조직 규정이나 법적 규정에 따른 사용 제한이 적용될 수 있습니다. 따라서 데이터를 처리할 때는 Real-Time CDP이 사용 정책을 준수하는지 확인하는 것이 중요합니다.

Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수할 수 있습니다. Real-Time CDP 내에서 중요한 역할을 하며, 이를 통해 사용 정책을 정의하고, 이러한 정책을 기반으로 데이터를 분류하고, 특정 마케팅 작업을 수행할 때 정책 위반이 있는지 확인할 수 있습니다.

Real-Time CDP은 Adobe Experience Platform을 기반으로 구축되므로 대부분의 데이터 거버넌스 기능에 대해 설명합니다. [!DNL Experience Platform] 설명서를 참조하십시오. 이 문서는 다음을 보완하기 위한 것입니다. [데이터 거버넌스 개요](../../data-governance/home.md) 대상 [!DNL Experience Platform], 그리고 Real-Time CDP에서 사용할 수 있는 거버넌스 기능에 대해 설명합니다. 다음 주제를 다룹니다.

* [데이터에 사용 레이블 적용](#labels)
* [데이터 사용 정책 관리](#policies)
* [데이터 사용 규정 준수 적용](#enforce)

## 데이터에 사용 레이블 적용 {#labels}

데이터 거버넌스를 사용하면 데이터 세트 또는 데이터 세트 필드 수준에서 데이터에 사용 레이블을 적용할 수 있습니다. 데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

데이터 사용 레이블 작업에 대한 자세한 내용은 [데이터 사용 레이블 사용 안내서](../../data-governance/labels/overview.md) Adobe Experience Platform용

## 대상에 대한 마케팅 작업 구성 {#destinations}

대상에 대한 마케팅 작업(마케팅 사용 사례라고도 함)을 정의하여 대상에 대한 데이터 사용 제한을 설정할 수 있습니다. 대상에 대한 마케팅 작업은 해당 대상으로 내보낼 데이터의 의도를 나타냅니다.

>[!NOTE]
>
>마케팅 작업과 데이터 사용 정책에서의 사용에 대한 자세한 내용은 [데이터 사용 정책 개요](../../data-governance/policies/overview.md) 다음에서 [!DNL Experience Platform] 설명서를 참조하십시오.

대상에 대한 마케팅 작업을 정의하면 해당 대상으로 전송된 모든 프로필 또는 대상이 데이터 사용 정책을 준수하는지 확인할 수 있습니다. 따라서 활성화에 대한 정책 제한을 집행해야 하는 조직의 필요에 따라 대상에 적절한 마케팅 작업을 추가해야 합니다.

마케팅 작업은 대상을 처음 설정할 때만 선택할 수 있습니다. 작업 중인 대상 유형에 따라 마케팅 작업을 구성할 수 있는 기회가 설정 워크플로우의 다른 지점에 나타납니다. 다음을 참조하십시오. [대상 설명서](../destinations/overview.md) 특정 대상을 구성하는 방법에 대한 단계입니다.

## 데이터 사용 정책 관리 {#policies}

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 정의하고 활성화해야 합니다. 데이터 사용 정책은 Real-Time CDP 내에서 데이터 수행을 허용하거나 제한하는 마케팅 작업 종류를 설명하는 규칙입니다. 에서 &quot;데이터 사용 정책&quot; 섹션을 참조하십시오. [!DNL Experience Platform] [데이터 거버넌스 개요](../../data-governance/home.md) 추가 정보.

Adobe Experience Platform은 일반적인 고객 경험 사용 사례를 위한 몇 가지 핵심 정책을 제공합니다. 이러한 정책은 로 이동하여 UI에서 볼 수 있습니다. **[!UICONTROL 정책]** 작업 영역 및 선택 **[!UICONTROL 찾아보기]** 탭. 다음을 참조하십시오. [정책 사용 안내서](../../data-governance/policies/user-guide.md) 다음에서 [!DNL Experience Platform] 사용자 정의 정책을 만드는 방법을 포함하여 UI에서 정책 작업에 대한 자세한 단계는 설명서에서 확인할 수 있습니다.

## 데이터 사용 규정 준수 적용 {#enforce}

데이터에 레이블이 지정되고 사용 정책이 정의되면 데이터 사용을 정책에 따라 적용할 수 있습니다. Real-Time CDP에서 대상을 대상으로 활성화할 때 데이터 거버넌스에서 위반이 발생하면 사용 정책을 자동으로 적용합니다.

다음에 대한 문서 보기: [자동 정책 시행](../../data-governance/enforcement/auto-enforcement.md) 추가 정보.

## 다음 단계

이제 Real-Time CDP의 주요 데이터 거버넌스 기능과 방법에 대해 알아보았습니다 [!DNL Experience Platform] 활성화하십시오. [Adobe Experience Platform의 데이터 거버넌스에 대한 설명서](../../data-governance/home.md). 이 설명서는 데이터 사용 레이블 및 정책 관리를 위한 단계별 워크플로우뿐만 아니라 필수 데이터 거버넌스 개념에 대한 개요를 제공합니다.

다음 비디오에서는 대상에 대한 마케팅 사용 사례 및 다양한 시나리오에 대한 예제 워크플로의 사용을 포함하여 Real-Time CDP의 데이터 거버넌스에 대한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
