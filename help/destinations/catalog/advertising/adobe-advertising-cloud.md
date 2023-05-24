---
keywords: Advertising Cloud;advertising cloud 확장; advertising cloud 대상
title: Adobe Advertising Cloud 확장
description: Adobe Advertising Cloud 확장은 Adobe Experience Platform의 광고 대상입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 3%

---

# Adobe Advertising Cloud 확장 {#adobe-advertising-cloud-extension}

## 개요 {#overview}

다음 은 [!DNL Advertising Cloud] 구현을 위한 확장 [!DNL Advertising Cloud] DSP 및 검색 모두에 대한 변환 및 세그먼트 태그(DCO는 현재 지원되지 않음).

Adobe Advertising Cloud은 Adobe Experience Platform의 광고 확장 프로그램입니다.

이 대상은 태그 확장입니다. Platform에서 태그 확장이 작동하는 방식에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md).

![Adobe Advertising Cloud 확장](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## 사전 요구 사항 {#prerequisites}

이 확장은 Platform을 구입한 모든 고객의 대상 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 UI의 데이터 수집 기능에 액세스하고 사용자에게 권한을 부여하도록 요청하십시오. **[!UICONTROL manage_properties]** 확장을 설치할 수 있는 권한.

## 확장 설치 {#install-extension}

Adobe Advertising Cloud 확장을 설치하려면:

다음에서 [플랫폼 인터페이스](https://platform.adobe.com/)로 이동합니다. **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음 을(를) 선택합니다 **[!UICONTROL 구성]** 오른쪽 레일에서. 다음과 같은 경우 **[!UICONTROL 구성]** 컨트롤이 회색으로 표시되어 있습니다. **[!UICONTROL manage_properties]** 권한. 다음을 참조하십시오 [전제 조건](#prerequisites).

확장을 설치할 태그 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 의 속성에 대해 알아보기 [태그 설명서](../../../tags/ui/administration/companies-and-properties.md).

워크플로를 사용하면 데이터 수집 UI로 이동하여 설치를 완료할 수 있습니다.

에서 바로 확장을 설치할 수도 있습니다. [데이터 수집 UI](https://experience.adobe.com/#/data-collection/). 다음 안내서를 참조하십시오 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) 추가 정보.

## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다. 데이터 수집 UI에서 설치된 확장에 대한 규칙을 설정하여 특정 상황에서만 이벤트 데이터를 확장 대상으로 전송할 수 있습니다. 확장에 대한 규칙 설정에 대한 자세한 내용은 [규칙](../../../tags/ui/managing-resources/rules.md) 를 참조하십시오.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우 UI가 계속 표시됩니다 **[!UICONTROL 설치]** 확장용. 에 설명된 대로 설치 워크플로우 시작 [확장 설치](#install-extension) 확장을 구성하거나 삭제합니다.

확장을 업그레이드하려면 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) 를 참조하십시오.
