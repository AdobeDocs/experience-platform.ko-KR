---
keywords: target 확장;target v2;target v2 확장
title: Adobe Target v2 확장
description: Adobe Target v2 확장은 Adobe Experience Platform의 개인화 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: d1d5ebbc-9093-42b0-8d88-58779df3ec89
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 13%

---

# Adobe Target v2 확장 {#adobe-target-v2-extension}

## 개요 {#overview}

Adobe Target은 웹 및 모바일 사이트, 앱, 소셜 미디어 및 기타 디지털 채널에서 매출을 극대화하기 위해 고객의 경험을 맞춤화하고 개인화하는 데 필요한 모든 것을 제공하는 Adobe Experience Cloud 솔루션입니다.

Adobe Target v2는 Adobe Experience Platform의 개인화 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102722.adobe-target-v2-launch-extension.html)에서 확장 페이지를 참조하십시오.

이 대상은 태그 확장입니다. Platform에서 태그 확장이 작동하는 방법에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![Adobe Target v2 확장](../../assets/catalog/personalization/adobe-target-v2/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객의 [!DNL Destinations] 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Adobe Experience Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 태그에 대한 액세스 권한을 얻고 **[!UICONTROL manage_properties]** 권한을 요청하십시오. 그러면 확장을 설치할 수 있습니다.

## 확장 설치 {#install-extension}

Adobe Target v2 확장을 설치하려면 다음을 수행하십시오.

[플랫폼 인터페이스](https://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음, 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없는 것입니다. [사전 요구 사항](#prerequisites)을 참조하십시오.

확장을 설치할 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 자세한 내용은 태그 설명서의 [속성](../../../tags/ui/administration/companies-and-properties.md#properties-page)에 있는 문서를 참조하십시오.

워크플로우는 설치를 완료하는 단계를 안내합니다.

확장 구성 옵션에 대한 자세한 내용은 태그 설명서의 [Adobe Target v2 확장 페이지](../../../tags/extensions/web/target-v2/overview.md)를 참조하십시오.

확장 프로그램은 [데이터 수집 UI](https://experience.adobe.com/#/data-collection/)에 직접 설치할 수도 있습니다. 자세한 내용은 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)에 대한 안내서를 참조하십시오.


## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장의 규칙 설정에 대한 자세한 내용은 태그 설명서의 [규칙](../../../tags/ui/managing-resources/rules.md)에 대한 개요를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 UI에 여전히 확장용 **[!UICONTROL Install]**&#x200B;이 표시됩니다. [Install extension](#install-extension)에 설명된 대로 설치 워크플로우를 시작하여 확장을 구성하거나 삭제합니다.

확장을 업그레이드하려면 태그 설명서의 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)에 대한 안내서를 참조하십시오.
