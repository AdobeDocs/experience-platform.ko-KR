---
title: 분기 확장
seo-title: 분기 확장
description: 지점 익스텐션은 Adobe 실시간 고객 데이터 플랫폼의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
seo-description: 지점 익스텐션은 Adobe 실시간 고객 데이터 플랫폼의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# 분기 확장 {#branch-extension}

## 개요 {#overview}

Branch는 모든 디바이스, 채널 및 플랫폼에서 고객 확보, 참여 및 측정할 수 있는 강력한 링크 및 솔루션을 제공합니다.

Branch는 Adobe 실시간 고객 데이터 플랫폼의 광고 확장입니다. 확장 기능에 대한 자세한 내용은 분기 웹 사이트의 [기능 페이지를](https://branch.io/features/) 참조하십시오.

이 대상은 경험 플랫폼 론치 확장자입니다. Launch 익스텐션이 Adobe Real-time CDP에서 작동하는 방법에 대한 자세한 내용은 Experience Platform [Launch 익스텐션 개요를](/help/rtcdp/destinations/experience-platform-launch-extensions.md)참조하십시오.

## 전제 조건 {#prerequisites}

이 익스텐션은 Adobe Real-time CDP를 구매한 모든 고객의 대상 카탈로그에서 제공됩니다.

이 확장을 사용하려면 Experience Platform Launch에 액세스해야 합니다. Adobe Experience Platform Launch는 Adobe Experience Cloud 고객에게 부가 가치 기능으로 제공됩니다. 조직 관리자에게 문의하여 Launch에 액세스할 수 있도록 **[!UICONTROL manage_properties]** 권한을 부여받고 익스텐션을 설치하도록 요청하십시오.

## 확장 설치 {#install-extension}

분기 확장을 설치하려면:

1. Adobe [실시간 CDP 인터페이스에서](http://platform.adobe.com/)해당 사이트로 이동합니다 **[!UICONTROL Destinations > Catalog]**.
2. 카탈로그에서 익스텐션을 선택하거나 검색 막대를 사용합니다.
3. 대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL Install Extension]** 선택합니다. 컨트롤이 **[!UICONTROL Install Extension]** 회색으로 표시되면 권한이 없는 **[!UICONTROL manage_properties]** 것입니다. 전제 조건을 [참조하십시오](#prerequisites).
4. 창에서 **[!UICONTROL Select available Launch property]** 확장을 설치할 Launch 속성을 선택합니다. Launch에서 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 시작 설명서의 속성 [페이지 섹션에서](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) 속성에 대해 알아봅니다.
5. 워크플로우는 설치를 완료하기 위해 [시작]으로 이동합니다.

Experience Platform Launch 인터페이스에서 직접 익스텐션을 설치할 [수도](https://launch.adobe.com/)있습니다. 론치 [설명서에서 새 확장](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) 추가를 참조하십시오.

## 익스텐션을 사용하는 방법 {#how-to-use}

확장을 설치한 후에는 Launch에서 직접 확장 프로그램의 규칙을 설정할 수 있습니다.

Launch에서는 특정 상황에서만 이벤트 데이터를 확장 대상에 보내도록 설치된 확장 기능에 대한 규칙을 설정할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 규칙 [설명서를](https://docs.adobe.com/help/ko-KR/launch/using/reference/manage-resources/rules.html)참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

Launch 인터페이스에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 이미 속성 중 하나에 설치되어 있는 경우 Adobe Real-time CDP UI가 확장자에 **[!UICONTROL Install]** 대해 계속 표시됩니다. 설치 익스텐션에 설명된 대로 설치 [워크플로우를](#install-extension) 시작하고 Launch에 도달하여 확장 프로그램을 구성하거나 삭제합니다.

익스텐션을 업그레이드하려면 Launch [설명서의 익스텐션 업그레이드를](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) 참조하십시오.



