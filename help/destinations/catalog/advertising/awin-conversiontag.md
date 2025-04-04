---
keywords: Awin 광고주 전환 태그 확장;전환 태그;Awin;Awin;AWIN
title: Awin 광고주 전환 태그 확장
description: Awin 광고주 전환 태그 확장 기능은 Adobe Experience Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 3%

---

# Awin 광고주 전환 태그 확장 {#awin-conversiontag-extension}

## 개요 {#overview}

전환 태그는 AWIN.Tracking.Sale JavaScript 개체의 선언으로, 확인 페이지에서 전환이 발생했음을 Mastertag에 지시하기 위해 수행됩니다. 그런 다음 필요한 추적 요청을 수행합니다.

Awin 광고주 전환 태그는 Adobe Experience Platform의 광고 확장 프로그램입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)의 확장 페이지를 참조하십시오.

이 대상은 태그 확장입니다. Experience Platform에서 태그 확장이 작동하는 방식에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![UI에서 Advertiser ConversionTag 확장 사용](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Experience Platform을 구입한 모든 고객의 대상 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Experience Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 UI의 데이터 수집 기능에 액세스하고 확장을 설치할 수 있도록 **[!UICONTROL manage_properties]** 권한을 부여하도록 요청하십시오.

## 확장 설치 {#install-extension}

[!DNL Awin Advertiser Conversion Tag] 확장을 설치하려면:

[Experience Platform 인터페이스](https://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**(으)로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL Configure]** 컨트롤이 회색으로 표시되어 있으면 **[!UICONTROL manage_properties]** 권한이 없습니다. [필수 구성 요소](#prerequisites)를 참조하십시오.

확장을 설치할 태그 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. [태그 설명서](../../../tags/ui/administration/companies-and-properties.md)에서 속성에 대해 알아보세요.

워크플로를 사용하면 데이터 수집 UI로 이동하여 설치를 완료할 수 있습니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 Adobe Exchange의 [Advertiser 전환 태그 만들기](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)를 참조하십시오.

[데이터 수집 UI](https://experience.adobe.com/#/data-collection/)에서 바로 확장을 설치할 수도 있습니다. 자세한 내용은 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)에 대한 안내서를 참조하십시오.


## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서만 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장의 규칙 설정에 대한 자세한 내용은 태그 설명서의 [규칙](../../../tags/ui/managing-resources/rules.md)에 대한 개요를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우에도 UI에 확장에 대한 **[!UICONTROL 설치]**&#x200B;가 표시됩니다. 확장을 구성하거나 삭제하려면 [확장 설치](#install-extension)에 설명된 대로 설치 워크플로를 시작합니다.

확장을 업그레이드하려면 태그 설명서의 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)에 대한 안내서를 참조하십시오.
