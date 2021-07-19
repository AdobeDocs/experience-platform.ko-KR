---
keywords: beemray,빔선 확장
title: Beemray 확장
description: 빔레이 확장은 Adobe Experience Platform의 개인화 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: 5bb639f5-42b5-48ae-a3e9-7585595ab925
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# [!DNL Beemray] 확장 {#beemray-extension}

## 개요 {#overview}

[!DNL Beemray] 은 상황 컨텍스트를 통해 제품을 가속화할 수 있도록 도와줍니다. 통찰력을 확보하고 새로운 경험을 구축하며 상호 작용을 촉진하며 중요한 순간에 관여할 수 있습니다. Beemray는 기계 학습을 사용하여 컨텍스트 기반 인텔리전스를 자동화합니다. Adobe는 Adobe Experience Cloud 및 기타 기술 파트너에 연결합니다. 모든 것이 실시간으로 일어난다. 이 확장은 사이트에 [!DNL Beemray] SDK를 설치합니다.

Beamray는 Adobe Experience Platform의 개인화 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html)에서 확장 페이지를 참조하십시오.

이 대상은 [!DNL Adobe Experience Platform Launch] 확장입니다. Platform에서 [!DNL Platform Launch] 확장이 작동하는 방법에 대한 자세한 내용은 [Experience Platform Launch 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![Beemray 확장](../../assets/catalog/personalization/beemray/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객의 [!DNL Destinations] 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 [!DNL Adobe Experience Platform Launch]에 액세스해야 합니다. [!DNL Platform Launch] 는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 확장을 설치할 수 있도록 [!DNL Platform Launch]manage_properties ]**권한을 부여하도록 조직 관리자에게 문의하십시오.**[!UICONTROL 

## 확장 설치 {#install-extension}

[!DNL Beemray] 확장을 설치하려면 다음을 수행하십시오.

[플랫폼 인터페이스](http://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음, 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없는 것입니다. [사전 요구 사항](#prerequisites)을 참조하십시오.

**[!UICONTROL 사용 가능한 Platform launch 속성 선택]** 창에서 확장을 설치할 [!DNL Platform Launch] 속성을 선택합니다. 또한 [!DNL Platform Launch]에서 새 속성을 만드는 옵션이 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. [!DNL Launch] 설명서의 [속성 페이지 섹션](../../../tags/ui/administration/companies-and-properties.md#properties-page)에 있는 속성에 대해 알아봅니다.

워크플로우에서 [!DNL Platform Launch] 로 이동하여 설치를 완료합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.101063.beemray-human-context.html)의 [빔레이 페이지를 참조하십시오.

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
