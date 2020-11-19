---
keywords: TMMData;tmm data;tmmdata;TMM data
title: TMMData 확장
seo-title: TMMData 확장
description: TMMData 익스텐션은 실시간 고객 데이터 플랫폼의 분석 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
seo-description: TMMData 익스텐션은 실시간 고객 데이터 플랫폼의 분석 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
translation-type: tm+mt
source-git-commit: 6eabcd70b133051205b669253f280cb92c24412f
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 4%

---


# [!DNL TMMData] 확장 {#tmmdata-extension}

## 개요 {#overview}

[!DNL TMMData's] Adobe Marketing Cloud의 기본 플랫폼은 자동화된 캠페인 설정 및 Adobe 및 기타 분석 및 BI 툴로 직접 가져오는 기능을 통해 내부/외부 및 온라인/오프라인 데이터를 비롯한 모든 중요한 데이터 소스를 액세스하고 혼합하여 안전하고 포괄적인 크로스채널 분석을 수행할 수 있는 툴을 마케팅 팀에 제공합니다.

[!DNL TMMData] 실시간 고객 데이터 플랫폼의 분석 확장입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange의 확장 페이지를 참조하십시오](hhttps://exchange.adobe.com/experiencecloud.details.100148.tmmdata-foundation-platform.html).

이 목적지는 Adobe Experience Platform Launch 확장선입니다 Adobe 실시간 CDP에서 플랫폼 실행 확장 기능이 작동하는 방법에 대한 자세한 내용은 [Adobe Experience Platform Launch 확장 개요를 참조하십시오](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![TMMData 확장](assets/tmmdata-extension.png)

## 전제 조건 {#prerequisites}

이 익스텐션은 실시간 CDP Adobe을 구입한 모든 고객을 위해 [!DNL Destinations] 카탈로그에서 제공됩니다.

이 확장 기능을 사용하려면 Adobe Experience Platform Launch에 액세스해야 합니다. Platform Launch는 Adobe Experience Cloud 고객에게 부가가치 기능으로 제공됩니다. Platform Launch에 액세스할 수 있도록 조직 관리자에게 문의하여 **[!UICONTROL manage_properties]** 권한을 부여받아 Extension을 설치할 수 있도록 요청하십시오.

## 확장 설치 {#install-extension}

익스텐션을 설치하려면 [!DNL TMMData] 다음을 수행하십시오.

1. Adobe [실시간 CDP 인터페이스에서](http://platform.adobe.com/)대상 **[!UICONTROL >]** 카탈로그 **[!UICONTROL 로]**&#x200B;이동합니다.
2. 카탈로그에서 익스텐션을 선택하거나 검색 막대를 사용합니다.
3. 대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL 구성을]** 선택합니다. 구성 **[!UICONTROL 컨트롤이]** 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없습니다. 전제 조건 [을 참조하십시오](#prerequisites).
4. 사용 **[!UICONTROL 가능한 플랫폼 시작 속성]** 선택 창에서 확장을 설치할 플랫폼 실행 속성을 선택합니다. 플랫폼 론치에서 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 플랫폼 실행 설명서의 [속성 페이지](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 섹션에서 속성에 대해 알아봅니다.
5. Platform Launch로 이동하여 설치를 완료합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 Adobe Exchange의 [TMMData 페이지를 참조하십시오](https://exchange.adobe.com/experiencecloud.details.100148.tmmdata-foundation-platform.html).

또한 [Adobe Experience Platform Launch 인터페이스에서 직접 익스텐션을 설치할 수 있습니다](https://launch.adobe.com/). 플랫폼 [실행 설명서에서 새 확장](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 추가를 참조하십시오.

## 익스텐션 사용 방법 {#how-to-use}

익스텐션을 설치한 후에는 플랫폼 론치에서 바로 규칙 설정을 시작할 수 있습니다.

플랫폼 론치에서 특정 상황에서만 이벤트 데이터를 확장 대상에 전송하기 위해 설치된 확장 기능에 대한 규칙을 설정할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙 설명서를 참조하십시오](https://docs.adobe.com/help/ko-KR/launch/using/reference/manage-resources/rules.html).

## 확장 기능 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

Platform Launch 인터페이스에서 익스텐션을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 이미 속성 중 하나에 설치되어 있는 경우 Adobe Real-time CDP UI에 **[!UICONTROL Install for the extension]** 이 여전히 표시됩니다. Platform Launch에 도달하고 확장 기능을 [구성하거나 삭제하려면 Install extension](#install-extension) 에 설명된 대로 설치 워크플로우를 시작합니다.

익스텐션을 업그레이드하려면 Platform Launch 설명서에서 [Extension](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 업그레이드를 참조하십시오.