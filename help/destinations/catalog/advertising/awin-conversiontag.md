---
keywords: Win Advertiser 변환 태그 확장;변환 태그;Win;Win;AWIN
title: Win Advertiser 변환 태그 확장
description: Win Advertiser 변환 태그 확장 은 Adobe Experience Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: 99feb169-acf3-4e68-8785-3f4cf565e5a9
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# Win Advertiser 변환 태그 확장 {#awin-conversiontag-extension}

## 개요 {#overview}

Conversion Tag는 AWIN.Tracking.Sale JavaScript 개체의 선언이며, 이 선언은 Master Tag에서 전환이 발생했음을 지시하도록 합니다. 그런 다음 필요한 추적 요청을 수행합니다.

Win Advertiser Conversion Tag는 Adobe Experience Platform의 광고 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe 교환](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

이 대상은 태그 확장입니다. Platform에서 태그 확장이 작동하는 방식에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md).

![UI의 Win Advertiser Conversiontag 확장](../../assets/catalog/advertising/awin-conversion-tag/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객을 위한 대상 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Platform에서 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 UI의 데이터 수집 기능에 대한 액세스 권한을 받으십시오 **[!UICONTROL manage_properties]** 확장을 설치할 수 있는 권한.

## 확장 설치 {#install-extension}

를 설치하려면 [!DNL Awin Advertiser Conversion Tag] 확장:

에서 [플랫폼 인터페이스](https://platform.adobe.com/), 이동 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음 선택합니다 **[!UICONTROL 구성]** 오른쪽 레일에 있습니다. 만약 **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되며 **[!UICONTROL manage_properties]** 권한. 자세한 내용은 [전제 조건](#prerequisites).

확장을 설치할 태그 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 에서 속성에 대해 알아보기 [태그 설명서](../../../tags/ui/administration/companies-and-properties.md).

워크플로우를 통해 데이터 수집 UI로 이동하여 설치를 완료합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 [Adobe Exchange의 Win Advertiser 변환 태그 페이지](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html).

확장을 직접 [데이터 수집 UI](https://experience.adobe.com/#/data-collection/). 다음 안내서를 참조하십시오. [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 추가 정보.


## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙](../../../tags/ui/managing-resources/rules.md) 태그 설명서에 추가했습니다.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 UI가 계속 표시됩니다 **[!UICONTROL 설치]** 확장 프로그램에 대해 설명합니다. 에 설명된 대로 설치 워크플로우를 시작합니다. [확장 설치](#install-extension) 확장을 구성하거나 삭제하려면

확장을 업그레이드하려면 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 태그 설명서에 추가했습니다.
