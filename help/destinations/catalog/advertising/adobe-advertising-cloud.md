---
keywords: Advertising Cloud;advertising cloud 확장 advertising cloud 대상
title: Adobe Advertising Cloud 확장
description: Adobe Advertising Cloud 확장은 Adobe Experience Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 3%

---

# Adobe Advertising Cloud 확장 {#adobe-advertising-cloud-extension}

## 개요 {#overview}

DSP과 검색 모두에 대한 [!DNL Advertising Cloud] 변환 및 세그먼트 태그를 구현하는 [!DNL Advertising Cloud] 확장입니다(DCO는 현재 지원되지 않음).

Adobe Advertising Cloud은 Adobe Experience Platform의 광고 확장입니다.

이 대상은 태그 확장입니다. Platform에서 태그 확장이 작동하는 방식에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![Adobe Advertising Cloud 확장](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객을 위한 대상 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Platform에서 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 데이터 수집 UI에 액세스하고 확장을 설치할 수 있도록 **[!UICONTROL manage_properties]** 권한을 요청하십시오.

## 확장 설치 {#install-extension}

Adobe Advertising Cloud 확장을 설치하려면 다음을 수행하십시오.

[플랫폼 인터페이스](https://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**&#x200B;로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음, 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없는 것입니다. [사전 요구 사항](#prerequisites)을 참조하십시오.

확장을 설치할 태그 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. [태그 설명서](../../../tags/ui/administration/companies-and-properties.md)의 속성에 대해 알아봅니다.

워크플로우를 통해 데이터 수집 UI로 이동하여 설치를 완료합니다.

확장 프로그램은 [데이터 수집 UI](https://experience.adobe.com/#/data-collection/)에 직접 설치할 수도 있습니다. 자세한 내용은 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)에 대한 안내서를 참조하십시오.

## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장의 규칙 설정에 대한 자세한 내용은 태그 설명서의 [규칙](../../../tags/ui/managing-resources/rules.md)에 대한 개요를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 UI에 여전히 확장용 **[!UICONTROL Install]**&#x200B;이 표시됩니다. [Install extension](#install-extension)에 설명된 대로 설치 워크플로우를 시작하여 확장을 구성하거나 삭제합니다.

확장을 업그레이드하려면 태그 설명서의 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)에 대한 안내서를 참조하십시오.
