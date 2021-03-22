---
keywords: bing;bing 광고 이벤트 추적;이벤트 추적 bing;UET;UET 확장
title: Bing 광고 유니버설 이벤트 추적(UET) 확장
description: Bing 광고 UET(Universal Event Tracking) 확장은 Adobe Experience Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 4%

---


# [!DNL Bing Ads Universal Event Tracking] (UET) 확장  {#bing-ads-extension}

## 개요 {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET) [!DNL Experience Platform Launch] 는 누군가 검색 광고를 클릭한 후 발생하는 상황을 추적하는 유용한 방법입니다. 단일 UET 태그를 사용하여 웹 사이트에서 고객의 작업을 기록하면 해당 데이터를 활용하여 전환율을 추적하거나 리마케팅 목록을 사용하여 고객을 타깃팅할 수 있습니다.

[!DNL Bing Ads Universal Event Tracking] (UET)는 Adobe Experience Platform의 광고 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html)의 확장 페이지를 참조하십시오.

이 대상은 [!DNL Adobe Experience Platform Launch] 확장자입니다. 플랫폼에서 [!DNL Platform Launch] 확장이 작동하는 방법에 대한 자세한 내용은 [Experience Platform Launch 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![Bing 광고 확장](../../assets/catalog/advertising/bing-ads/catalog.png)

## 전제 조건 {#prerequisites}

이 확장 프로그램은 Platform을 구입한 모든 고객의 [!DNL Destinations] 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 [!DNL Adobe Experience Platform Launch]에 액세스해야 합니다. [!DNL Platform Launch] Adobe Experience Cloud 고객에게 제공되는 부가 가치 기능 조직 관리자에게 문의하여 [!DNL Platform Launch]에 액세스할 수 있도록 **[!UICONTROL manage_properties]** 권한을 요청하십시오. 그러면 확장을 설치할 수 있습니다.

## 확장 설치 {#install-extension}

[!DNL Bing Ads Universal Event Tracking](UET) 확장을 설치하려면:

[플랫폼 인터페이스](http://platform.adobe.com/)에서 **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;으로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 막대를 사용합니다.

대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL Configure]**&#x200B;을 선택합니다. **[!UICONTROL Configure]** 컨트롤이 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없습니다. [사전 요구 사항](#prerequisites)을 참조하십시오.

**[!UICONTROL Select available Platform Launch property]** 창에서 확장을 설치할 [!DNL Platform Launch] 속성을 선택합니다. [!DNL Platform Launch]에 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. [!DNL Launch] 설명서의 [속성 페이지 섹션](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page)에서 속성에 대해 알아봅니다.

워크플로우에서 [!DNL Platform Launch]으로 이동하여 설치를 완료합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100154.html)의 [Bing 광고 UET(Universal Event Tracking) 페이지를 참조하십시오.

또한 [Adobe Experience Platform Launch 인터페이스](https://launch.adobe.com/)에 직접 확장을 설치할 수도 있습니다. [!DNL Platform Launch] 설명서에서 [새 확장](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) 추가를 참조하십시오.


## 확장 {#how-to-use} 사용 방법

확장을 설치한 후에는 [!DNL Platform Launch]에서 직접 해당 확장에 대한 규칙을 설정할 수 있습니다.

[!DNL Platform Launch]에서는 특정 상황에서 이벤트 데이터를 확장 대상에 전송하기 위해 설치된 확장의 규칙을 설정할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙 설명서](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html)를 참조하십시오.

## 확장 {#configure-upgrade-delete} 구성, 업그레이드 및 삭제

[!DNL Platform Launch] 인터페이스에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 이미 속성 중 하나에 설치되어 있는 경우 플랫폼 UI에 확장명에 대해 **[!UICONTROL Install]**&#x200B;이 여전히 표시됩니다. [!DNL Platform Launch]Install extension](#install-extension)에 설명된 대로 설치 작업 과정을 시작하고 확장을 구성하거나 삭제합니다.[

확장을 업그레이드하려면 [!DNL Platform Launch] 설명서의 [확장 업그레이드](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html)를 참조하십시오.
