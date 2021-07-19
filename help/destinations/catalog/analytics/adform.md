---
keywords: adform 확장;adform
title: Adform 웹 사이트 추적 확장
description: Adform 확장은 Adobe Experience Platform의 분석 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: f616ecbf-6833-40cd-86be-7c13afe31180
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 4%

---

# Adform 웹 사이트 추적 확장 {#adform-extension}

## 개요 {#overview}

Adform 웹 사이트 추적 확장을 사용하면 광고주가 [!DNL Experience Platform Launch] 플랫폼을 사용하여 사이트 간에 Adform 추적 포인트를 쉽게 구현할 수 있습니다.

[!DNL Adform] 는 Adobe Experience Platform의 analytics 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)에서 확장 페이지를 참조하십시오

이 대상은 [!DNL Adobe Experience Platform Launch] 확장입니다. Platform에서 [!DNL Platform Launch] 확장이 작동하는 방법에 대한 자세한 내용은 [Experience Platform Launch 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![Adform 확장](../../assets/catalog/analytics/adform/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객의 [!DNL Destinations] 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 [!DNL Adobe Experience Platform Launch]에 액세스해야 합니다. [!DNL Platform Launch] 는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 확장을 설치할 수 있도록 [!DNL Platform Launch]manage_properties ]**권한을 부여하도록 조직 관리자에게 문의하십시오.**[!UICONTROL 

## 확장 설치 {#install-extension}

Adform 확장을 설치하려면 다음을 수행하십시오.

[플랫폼 인터페이스](http://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음, 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없는 것입니다. [사전 요구 사항](#prerequisites)을 참조하십시오.

**[!UICONTROL 사용 가능한 Launch 속성 선택]** 창에서 확장을 설치할 [!DNL Launch] 속성을 선택합니다. Launch에서 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. [!DNL Launch] 설명서의 [속성 페이지 섹션](../../../tags/ui/administration/companies-and-properties.md#properties-page)에 있는 속성에 대해 알아봅니다.

워크플로우에서 [!DNL Launch] 로 이동하여 설치를 완료합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103195.adform-website-tracking.html)의 [Adform 페이지를 참조하십시오.

[Adobe Experience Platform Launch 인터페이스](https://launch.adobe.com/)에 직접 확장을 설치할 수도 있습니다. [!DNL Platform Launch] 설명서에서 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)를 참조하십시오.

## 확장 사용 방법 {#how-to-use}

확장을 설치한 후에는 [!DNL Platform Launch]에서 직접 규칙 설정을 시작할 수 있습니다.

[!DNL Platform Launch]에서는 특정 상황에서 이벤트 데이터를 확장 대상에 보내도록 설치된 확장에 대한 규칙을 설정할 수 있습니다. 확장의 규칙 설정에 대한 자세한 내용은 [규칙 설명서](../../../tags/ui/managing-resources/rules.md)를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

[!DNL Platform Launch] 인터페이스에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 Platform UI에는 여전히 확장용 **[!UICONTROL Install]**&#x200B;이 표시됩니다. [Install extension](#install-extension)에 설명된 대로 설치 워크플로우를 시작하여 [!DNL Platform Launch]에 연결하고 확장을 구성하거나 삭제합니다.

확장을 업그레이드하려면 [!DNL Platform Launch] 설명서의 [확장 업그레이드](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)를 참조하십시오.
