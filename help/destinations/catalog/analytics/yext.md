---
keywords: 다음 전환 추적;텍스트;텍스트;다음 전환 추적
title: 다음 전환 추적 확장
description: 다음 전환 추적 확장은 Adobe Experience Platform의 분석 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: 786ea14c-25a3-40ac-906d-6a8f7de04f41
source-git-commit: 6bbccf6751240637c861c2962b64e5247d8abb43
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 3%

---

# [!DNL Yext Conversion Tracking] 확장 {#yext-extension}

## 개요 {#overview}

[!DNL Yext Conversion Tracking] 확장을 사용하면 Ext 제품 사용에 따른 전환을 측정할 수 있습니다.

[!DNL Yext Conversion Tracking] 는 Adobe Experience Platform의 analytics 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103174.yext-conversion-tracking.html)에서 확장 페이지를 참조하십시오.

이 대상은 태그 확장입니다. Platform에서 태그 확장이 작동하는 방법에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![다음 전환 추적 확장](../../assets/catalog/analytics/yext/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객의 [!DNL Destinations] 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Adobe Experience Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 태그에 대한 액세스 권한을 얻고 **[!UICONTROL manage_properties]** 권한을 요청하십시오. 그러면 확장을 설치할 수 있습니다. 확장을 설치할 수 있도록 **[!UICONTROL manage_properties]** 권한을 부여하도록 이들에게 요청합니다.

## 확장 설치 {#install-extension}

[!DNL Yext Conversion Tracking] 확장을 설치하려면 다음을 수행하십시오.

[플랫폼 인터페이스](http://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음, 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없는 것입니다. [사전 요구 사항](#prerequisites)을 참조하십시오.

확장을 설치할 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 태그 설명서에서 의 [속성 페이지 섹션](../../../tags/ui/administration/companies-and-properties.md#properties-page)에 있는 속성에 대해 알아봅니다.

워크플로우는 설치를 완료하는 단계를 안내합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 Exchange](https://exchange.adobe.com/experiencecloud.details.103174.yext-conversion-tracking.html)Adobe의 [다음 변환 추적 페이지를 참조하십시오.

확장 프로그램은 [데이터 수집 UI](https://experience.adobe.com/#/data-collection/)에 직접 설치할 수도 있습니다. 자세한 내용은 태그 설명서에서 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)의 섹션을 참조하십시오.

## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다.

설치된 확장에 대한 규칙을 설정하여 이벤트 데이터를 특정 상황에서만 확장 대상에 보낼 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [태그 설명서](../../../tags/ui/managing-resources/rules.md)를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 Platform UI에는 여전히 확장용 **[!UICONTROL Install]**&#x200B;이 표시됩니다. [Install extension](#install-extension)에 설명된 대로 설치 워크플로우를 시작하여 확장을 구성하거나 삭제합니다.

확장을 업그레이드하려면 태그 설명서의 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)에 대한 안내서를 참조하십시오.
