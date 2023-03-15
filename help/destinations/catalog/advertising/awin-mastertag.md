---
keywords: Awin Advertiser 마스터태그 확장;마스터태그 태그;Awin;awin;AWIN
title: Awin Advertiser Mastertag 확장
description: Awin Advertiser Mastertag 확장은 Adobe Experience Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
exl-id: 99a9ea40-b89f-4503-91a7-60cc8e1cd6d3
source-git-commit: c8d6c156b3351324fe1be11144afeae91f7a2a59
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 3%

---

# [!DNL Awin Advertiser Mastertag] 확장 {#awin-mastertag-extension}

## 개요 {#overview}

다음 [!DNL MasterTag] 는 Awin 추적 솔루션에 필요한 모든 함수를 포함하는 JavaScript 라이브러리이며, 확인 페이지를 포함하여 사이트의 모든 페이지에 무조건 추가되어야 하며, 결제 정보를 표시하거나 처리하는 페이지는 제외되어야 합니다.

[!DNL Awin Advertiser Mastertag] 는 Adobe Experience Platform의 광고 확장 프로그램입니다. 확장 기능에 대한 자세한 내용은 의 확장 페이지를 참조하십시오 [Adobe 교환](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

이 대상은 태그 확장입니다. Platform에서 확장이 작동하는 방식에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md).

![UI의 Advertiser Mastertag 확장](../../assets/catalog/advertising/awin-mastertag/catalog.png)

## 전제 조건 {#prerequisites}

이 확장 프로그램은 다음에서 사용할 수 있습니다. [!DNL Destinations] Platform을 구입한 모든 고객을 위한 카탈로그.

이 확장을 사용하려면 Adobe Experience Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 태그에 대한 액세스 권한을 얻으려면 조직 관리자에게 연락하여 권한을 부여하도록 요청하십시오. **[!UICONTROL manage_properties]** 확장을 설치할 수 있는 권한.

## 확장 설치 {#install-extension}

을(를) 설치하려면 [!DNL Awin Advertiser Mastertag] 확장:

다음에서 [플랫폼 인터페이스](https://platform.adobe.com/)로 이동합니다. **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음 을(를) 선택합니다 **[!UICONTROL 구성]** 오른쪽 레일에서. 다음과 같은 경우 **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되어 있습니다. **[!UICONTROL manage_properties]** 권한. 다음을 참조하십시오 [전제 조건](#prerequisites).

확장을 설치할 태그 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 의 속성에 대해 알아보기 [태그 설명서](../../../tags/ui/administration/companies-and-properties.md).

워크플로를 사용하면 데이터 수집 UI로 이동하여 설치를 완료할 수 있습니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 [Adobe Exchange의 Awin Advertiser Mastertag 페이지](https://exchange.adobe.com/experiencecloud.details.103176.awin-advertiser-mastertag.html).

에서 바로 확장을 설치할 수도 있습니다. [데이터 수집 UI](https://experience.adobe.com/#/data-collection/). 다음 안내서를 참조하십시오 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 추가 정보.


## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서만 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장에 대한 규칙 설정에 대한 자세한 내용은 [규칙](../../../tags/ui/managing-resources/rules.md) 를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 UI가 계속 표시됩니다 **[!UICONTROL 설치]** 확장용. 에 설명된 대로 설치 워크플로우 시작 [확장 설치](#install-extension) 확장을 구성하거나 삭제합니다.

확장을 업그레이드하려면 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 를 참조하십시오.
