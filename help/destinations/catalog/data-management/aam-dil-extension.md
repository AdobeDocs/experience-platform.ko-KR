---
keywords: Audience Manager DIL 확장;대상 audience manager;dil 확장
title: Audience Manager DIL 확장
description: Audience Manager DIL 확장은 Adobe Experience Platform의 DMP(데이터 관리 플랫폼) 대상입니다. 확장 기능에 대한 자세한 내용은 Exchange Adobe의 확장 페이지를 참조하십시오.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# Audience Manager DIL 확장 {#aam-dil-extension}

## 개요 {#overview}

Adobe Audience Manager Data Integration Library 확장(클라이언트측 구현)입니다. 참고: 이 확장은 Adobe Analytics 데이터의 서버측 전달(SSF)에 사용하기 위한 것이 아닙니다. SSF의 경우 Adobe Analytics 확장을 사용합니다. 중요 사항: 버전 8.0부터 DIL은 [!DNL Experience Cloud] ID 서비스, 버전 3.3 이상. 두 가지 모두 구현하십시오 [!DNL Experience Cloud] ID 서비스 및 전체 DIL [!DNL Audience Manager] 데이터 통합 기능.

[!DNL Audience Manager] DIL은 Adobe Experience Platform의 DMP(데이터 관리 플랫폼) 확장입니다. 확장 기능에 대한 자세한 내용은 [Audience Manager 확장 페이지](../../../tags/extensions/client/audience-manager/overview.md) 태그 설명서에 추가했습니다.

이 대상은 태그 확장입니다. Platform에서 확장이 작동하는 방식에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md).

![Audience Manager DIL 확장](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## 전제 조건 {#prerequisites}

이 확장은 [!DNL Destinations] Platform을 구입한 모든 고객을 위한 카탈로그

이 확장을 사용하려면 Adobe Experience Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 연락하여 태그에 대한 액세스 권한을 받고 사용자에게 **[!UICONTROL manage_properties]** 확장을 설치할 수 있는 권한.

## 확장 설치 {#install-extension}

를 설치하려면 [!DNL Audience Manager] DIL 확장:

에서 [플랫폼 인터페이스](https://platform.adobe.com/), 이동 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음 선택합니다 **[!UICONTROL 구성]** 오른쪽 레일에 있습니다. 만약 **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되며 **[!UICONTROL manage_properties]** 권한. 자세한 내용은 [전제 조건](#prerequisites).

확장을 설치할 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 에서 속성에 대해 알아보기 [태그 설명서](../../../tags/ui/administration/companies-and-properties.md#properties-page).

워크플로우는 설치를 완료하는 단계를 안내합니다.

확장 구성 옵션에 대한 자세한 내용은 [Audience Manager 확장 페이지](../../../tags/extensions/client/audience-manager/overview.md) 태그 설명서에 추가했습니다.

확장을 직접 [데이터 수집 UI](https://experience.adobe.com/#/data-collection/). 다음 안내서를 참조하십시오. [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 추가 정보.

## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장 규칙 설정에 대한 자세한 내용은 [규칙](../../../tags/ui/managing-resources/rules.md) 태그 설명서에 추가했습니다.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 UI가 계속 표시됩니다 **[!UICONTROL 설치]** 확장 프로그램에 대해 설명합니다. 에 설명된 대로 설치 워크플로우를 시작합니다. [확장 설치](#install-extension) 확장을 구성하거나 삭제하려면

확장을 업그레이드하려면 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 태그 설명서에 추가했습니다.
