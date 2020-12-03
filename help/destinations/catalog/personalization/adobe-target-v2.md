---
keywords: target extension;target;target v2;target v2 extension
title: Adobe Target v2 확장
seo-title: Adobe Target v2 확장
description: Adobe Target v2 익스텐션은 실시간 고객 데이터 플랫폼의 개인화 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
seo-description: Adobe Target v2 익스텐션은 실시간 고객 데이터 플랫폼의 개인화 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
translation-type: tm+mt
source-git-commit: 80db19822551883da272787affb6f7dc9dc3a745
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 12%

---


# Adobe Target v2 확장 {#adobe-target-v2-extension}

## 개요 {#overview}

Adobe Target은 웹 및 모바일 사이트, 앱, 소셜 미디어 및 기타 디지털 채널에서 매출을 극대화하기 위해 고객의 경험을 맞춤화하고 개인화하는 데 필요한 모든 것을 제공하는 Adobe Experience Cloud 솔루션입니다.

Adobe Target v2는 실시간 고객 데이터 플랫폼의 개인화 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange의 확장 페이지를 참조하십시오](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html).

이 목적지는 Adobe Experience Platform Launch 확장선입니다 실시간 CDP에서 플랫폼 실행 확장 기능이 작동하는 방법에 대한 자세한 내용은 [Adobe Experience Platform Launch 확장 개요를 참조하십시오](../launch-extensions/overview.md).

![Adobe Target v2 확장](../../assets/catalog/personalization/adobe-target-v2/catalog.png)

## 전제 조건 {#prerequisites}

이 익스텐션은 실시간 CDP를 구매한 모든 고객을 위한 [!DNL Destinations] 카탈로그에서 제공됩니다.

이 확장 기능을 사용하려면 액세스 권한이 필요합니다 [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] 이 포함된 부가 가치 기능으로 Adobe Experience Cloud 고객에게 제공됩니다. Extension을 설치할 수 [!DNL Platform Launch] 있도록 조직 관리자에게 **[!UICONTROL manage_properties]** 권한을 부여하도록 요청하십시오.

## 확장 설치 {#install-extension}

Adobe Target v2 익스텐션을 설치하려면:

실시간 [CDP 인터페이스에서](http://platform.adobe.com/)대상 **[!UICONTROL >]** 카탈로그 **[!UICONTROL 로]**&#x200B;이동합니다.

카탈로그에서 익스텐션을 선택하거나 검색 막대를 사용합니다.

대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL 구성을]** 선택합니다. 구성 **[!UICONTROL 컨트롤이]** 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없습니다. 전제 조건 [을 참조하십시오](#prerequisites).

사용 **[!UICONTROL 가능한 론치 속성]** 선택 창에서 확장자를 설치할 [!DNL Launch] 속성을 선택합니다. 에 새 속성을 만들 수도 있습니다 [!DNL Launch]. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 설명서의 [속성 페이지 섹션](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) 에서 속성에 대해 [!DNL Launch] 알아보십시오.

워크플로우에서 설치를 완료하는 데 [!DNL Launch] 가 사용됩니다.

확장 구성 옵션에 대한 자세한 내용은 설명서의 [Adobe Target v2 확장 페이지](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/targetv2-extension/adobe-target-extension-v2.html) 를 [!DNL Experience Launch] 참조하십시오.

또한 [Adobe Experience Platform Launch 인터페이스에서 직접 익스텐션을 설치할 수 있습니다](https://launch.adobe.com/). 설명서에서 [새 확장](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) 추가를 [!DNL Platform Launch] 참조하십시오.


## 익스텐션 사용 방법 {#how-to-use}

익스텐션을 설치한 후 에서 바로 규칙을 설정할 수 있습니다 [!DNL Platform Launch].

에서 [!DNL Platform Launch]이벤트 데이터를 특정 상황에서만 확장 대상에 보내도록 설치된 확장 기능에 대한 규칙을 설정할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙 설명서를 참조하십시오](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## 확장 기능 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

인터페이스에서 익스텐션을 구성, 업그레이드 및 삭제할 수 [!DNL Platform Launch] 있습니다.

>[!TIP]
>
>속성 중 하나에 익스텐션이 이미 설치되어 있는 경우 실시간 CDP UI에 **[!UICONTROL Install]** for Extension이 여전히 표시됩니다. 확장 기능을 가져오고 구성하거나 삭제하려면 [설치 확장](#install-extension) 프로그램 [!DNL Platform Launch] 에 설명된 대로 설치 워크플로우를 시작합니다.

익스텐션을 업그레이드하려면 설명서의 [익스텐션 업그레이드](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 를 [!DNL Platform Launch] 참조하십시오.
