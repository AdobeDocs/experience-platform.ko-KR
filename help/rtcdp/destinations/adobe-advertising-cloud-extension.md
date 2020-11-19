---
keywords: Advertising Cloud;advertising cloud extension; advertising cloud destination
title: Adobe Advertising Cloud 확장
seo-title: Adobe Advertising Cloud 확장
description: Adobe Advertising Cloud 익스텐션은 실시간 고객 데이터 플랫폼의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
seo-description: Adobe Advertising Cloud 익스텐션은 실시간 고객 데이터 플랫폼의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 5%

---


# Adobe Advertising Cloud 익스텐션 {#adobe-advertising-cloud-extension}

## 개요 {#overview}

DSP과 검색 모두에 대한 [!DNL Advertising Cloud] [!DNL Advertising Cloud] 전환 및 세그먼트 태그를 구현하기 위한 확장입니다(현재 DCO는 지원되지 않음).

Adobe Advertising Cloud은 실시간 고객 데이터 플랫폼의 광고 확장입니다.

이 대상은 [!DNL Adobe Experience Platform Launch] 확장자입니다. Adobe 실시간 CDP에서 익스텐션이 작동하는 방법에 대한 자세한 내용은 [!DNL Platform Launch] Experience Platform Launch 확장 개요를 참조하십시오 [](/help/rtcdp/destinations/experience-platform-launch-extensions.md).

![Adobe Advertising Cloud 확장](/help/rtcdp/destinations/assets/adobe-advertising-cloud-extension.png)

## 전제 조건 {#prerequisites}

이 익스텐션은 실시간 CDP Adobe을 구입한 모든 고객의 대상 카탈로그에서 제공됩니다.

이 확장 기능을 사용하려면 액세스 권한이 필요합니다 [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] 이 포함된 부가 가치 기능으로 Adobe Experience Cloud 고객에게 제공됩니다. Extension을 설치할 수 [!DNL Launch] 있도록 조직 관리자에게 **[!UICONTROL manage_properties]** 권한을 부여하도록 요청하십시오.

## 확장 설치 {#install-extension}

Adobe Advertising Cloud 익스텐션을 설치하려면:

1. Adobe [실시간 CDP 인터페이스에서](http://platform.adobe.com/)대상 **[!UICONTROL >]** 카탈로그 **[!UICONTROL 로]**&#x200B;이동합니다.
2. 카탈로그에서 익스텐션을 선택하거나 검색 막대를 사용합니다.
3. 대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL 구성을]** 선택합니다. 구성 **[!UICONTROL 컨트롤이]** 회색으로 표시되면 **[!UICONTROL manage_properties]** 권한이 없습니다. 전제 조건 [을 참조하십시오](#prerequisites).
4. 사용 **[!UICONTROL 가능한 플랫폼 시작 속성]** 선택 창에서 확장을 설치할 [!DNL Platform Launch] 속성을 선택합니다. 에 새 속성을 만들 수도 있습니다 [!DNL Platform Launch]. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 설명서의 [속성 페이지 섹션](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 에서 속성에 대해 [!DNL Launch] 알아보십시오.
5. 워크플로우에서 설치를 완료하는 데 [!DNL Platform Launch] 가 사용됩니다.

또한 [Adobe Experience Platform Launch 인터페이스에서 직접 익스텐션을 설치할 수 있습니다](https://launch.adobe.com/). 설명서에서 [새 확장](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 추가를 [!DNL Platform Launch] 참조하십시오.


## 익스텐션 사용 방법 {#how-to-use}

익스텐션을 설치한 후 에서 바로 규칙을 설정할 수 있습니다 [!DNL Platform Launch].

에서 [!DNL Platform Launch]이벤트 데이터를 특정 상황에서만 확장 대상에 보내도록 설치된 확장 기능에 대한 규칙을 설정할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙 설명서를 참조하십시오](https://docs.adobe.com/help/ko-KR/launch/using/reference/manage-resources/rules.html).

## 확장 기능 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

인터페이스에서 익스텐션을 구성, 업그레이드 및 삭제할 수 [!DNL Platform Launch] 있습니다.

>[!TIP]
>
>확장이 이미 속성 중 하나에 설치되어 있는 경우 Adobe Real-time CDP UI에 **[!UICONTROL Install for the extension]** 이 여전히 표시됩니다. 확장 기능을 가져오고 구성하거나 삭제하려면 [설치 확장](#install-extension) 프로그램 [!DNL Platform Launch] 에 설명된 대로 설치 워크플로우를 시작합니다.

익스텐션을 업그레이드하려면 설명서의 [익스텐션 업그레이드](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 를 [!DNL Platform Launch] 참조하십시오.
