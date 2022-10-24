---
keywords: 데이터 거버넌스 rtcdp;rtcdp 데이터 거버넌스;실시간 고객 데이터 프로필 데이터 거버넌스
title: 데이터 거버넌스 개요
description: 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 1%

---

# Real-Time CDP의 데이터 거버넌스

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP)은 여러 엔터프라이즈 시스템의 데이터를 함께 가져와서 마케터가 고객을 더 잘 식별, 이해 및 참여시킬 수 있도록 합니다. 이 데이터는 조직 또는 법적 규정에 의해 정의된 사용 제한을 받을 수 있습니다. 따라서 데이터를 처리할 때 Real-Time CDP이 사용 정책을 준수하도록 하는 것이 중요합니다.

Adobe Experience Platform 데이터 거버넌스를 사용하면 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수할 수 있습니다. Real-Time CDP 내에서 주요 역할을 수행하므로 사용 정책을 정의하고, 해당 정책을 기준으로 데이터를 분류하고, 특정 마케팅 작업을 수행할 때 정책 위반을 확인할 수 있습니다.

Real-Time CDP은 Adobe Experience Platform을 기반으로 구축되었으며, 따라서 데이터 거버넌스 기능의 대부분은 [!DNL Experience Platform] 설명서. 이 문서는 [데이터 거버넌스 개요](../../data-governance/home.md) 대상 [!DNL Experience Platform], 및 은 Real-Time CDP에서 사용할 수 있는 거버넌스 기능에 대해 간략하게 설명합니다. 다음 주제를 다룹니다.

* [데이터에 사용 레이블 적용](#labels)
* [데이터 사용 정책 관리](#policies)
* [데이터 사용 규정 준수 적용](#enforce)

## 데이터에 사용 레이블 적용 {#labels}

데이터 거버넌스를 사용하면 데이터 세트 또는 데이터 세트 필드 수준에서 데이터에 사용 레이블을 적용할 수 있습니다. 데이터 사용 레이블을 사용하면 해당 데이터에 적용되는 사용 정책에 따라 데이터를 분류할 수 있습니다.

데이터 사용 레이블 작업에 대한 자세한 내용은 [데이터 사용 레이블 사용 안내서](../../data-governance/labels/overview.md) Adobe Experience Platform용.

## 대상에 대한 마케팅 작업 구성 {#destinations}

대상에 대한 마케팅 작업(마케팅 사용 사례라고도 함)을 정의하여 대상에 대한 데이터 사용 제한을 설정할 수 있습니다. 대상에 대한 마케팅 작업은 해당 대상으로 내보낼 데이터의 의도를 나타냅니다.

>[!NOTE]
>
>마케팅 작업 및 데이터 사용 정책의 사용에 대한 자세한 내용은 다음을 참조하십시오. [데이터 사용 정책 개요](../../data-governance/policies/overview.md) 에서 [!DNL Experience Platform] 설명서.

대상에 대한 마케팅 작업을 정의하면 해당 대상으로 전송되는 모든 프로필 또는 세그먼트가 데이터 사용 정책을 준수하도록 할 수 있습니다. 따라서 활성화 정책에 대한 제한 사항을 적용해야 하는 조직의 요구 사항에 따라 대상에 적절한 마케팅 작업을 추가해야 합니다.

대상을 처음 설정할 때만 마케팅 작업을 선택할 수 있습니다. 작업 중인 대상 유형에 따라 마케팅 작업을 구성할 기회가 설정 워크플로우의 다른 시점에 나타납니다. 자세한 내용은 [대상 설명서](../destinations/overview.md) 를 참조하십시오.

## 데이터 사용 정책 관리 {#policies}

데이터 사용 레이블이 데이터 규정 준수를 효과적으로 지원하려면 데이터 사용 정책을 정의하고 활성화해야 합니다. 데이터 사용 정책은 Real-Time CDP 내에서 데이터를 수행할 수 있도록 허용하거나 제한하는 마케팅 작업 종류를 설명하는 규칙입니다. 의 &quot;데이터 사용 정책&quot; 섹션을 참조하십시오 [!DNL Experience Platform] [데이터 거버넌스 개요](../../data-governance/home.md) 추가 정보.

Adobe Experience Platform은 일반적인 고객 경험 사용 사례를 위한 몇 가지 핵심 정책을 제공합니다. 이러한 정책은 UI에서 **[!UICONTROL 정책]** 작업 공간 및 선택 **[!UICONTROL 찾아보기]** 탭. 자세한 내용은 [정책 사용 안내서](../../data-governance/policies/user-guide.md) 에서 [!DNL Experience Platform] 설명서에서 사용자 지정 정책을 만드는 방법을 비롯하여 UI에서 정책 작업에 대한 자세한 단계를 설명합니다.

## 데이터 사용 규정 준수 적용 {#enforce}

데이터가 레이블이 지정되고 사용 정책이 정의되면 정책에 따라 데이터 사용 규정을 적용할 수 있습니다. Real-Time CDP에서 대상 세그먼트를 대상으로 활성화할 때, 데이터 거버넌스에서는 위반이 발생하면 사용 정책을 자동으로 적용합니다.

다음 문서를 참조하십시오. [자동 정책 적용](../../data-governance/enforcement/auto-enforcement.md) 추가 정보.

## 다음 단계

이제 Real-Time CDP의 주요 데이터 거버넌스 기능과 그 방법을 소개합니다. [!DNL Experience Platform] 활성화하여 [Adobe Experience Platform의 데이터 거버넌스 설명서](../../data-governance/home.md). 이 설명서는 필수 데이터 거버넌스 개념에 대한 개요를 설명하고 데이터 사용 레이블 및 정책을 관리하는 단계별 워크플로우를 제공합니다.

다음 비디오에서는 대상에 마케팅 사용 사례 사용 및 다양한 시나리오를 위한 예제 워크플로우를 포함하여 Real-Time CDP의 데이터 거버넌스에 대한 개요를 제공합니다.

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
