---
keywords: 인보카와 인보카
title: 잘못된 태그 확장
description: Invoca 태그 확장은 Adobe Experience Platform의 고객 대상 음성입니다. 확장 기능에 대한 자세한 내용은 Adobe Exchange의 확장 페이지를 참조하십시오.
exl-id: f66a2e74-8d94-4b3a-9627-083ca875fad7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 3%

---

# [!DNL Invoca Tags] 확장 기능 {#invoca-extension}

## 개요 {#overview}

[!DNL Invoca]은(는) 디지털 고객 여정에 통화 데이터 및 음성 통찰력을 제공합니다. [!DNL Invoca’s] 통화 인텔리전스 플랫폼을 사용하면 마케터는 최종적으로 통화 결과를 측정하고 오프라인 전환을 다시 디지털 지출로 연결할 수 있는 분석을 보유합니다.

[!DNL Invoca Tags]은(는) Adobe Experience Platform의 고객 확장에 대한 음성입니다. 확장 기능에 대한 자세한 내용은 [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.100067.invoca.html)의 확장 페이지를 참조하십시오.

이 대상은 태그 확장입니다. Experience Platform에서 태그 확장이 작동하는 방법에 대한 자세한 내용은 [태그 확장 개요](../launch-extensions/overview.md)를 참조하십시오.

![잘못된 확장](../../assets/catalog/voice/invoca/catalog.png)

## 전제 조건 {#prerequisites}

이 확장은 Experience Platform을 구입한 모든 고객의 [!DNL Destinations] 카탈로그에서 사용할 수 있습니다.

이 확장을 사용하려면 Adobe Experience Platform의 태그에 액세스해야 합니다. 태그는 부가가치 기능으로 포함되어 Adobe Experience Cloud 고객에게 제공됩니다. 조직 관리자에게 문의하여 태그에 대한 액세스 권한을 받은 다음 확장을 설치할 수 있도록 **[!UICONTROL manage_properties]** 권한을 부여해 달라고 요청하십시오.

## 확장 설치 {#install-extension}

[!DNL Invoca Tags] 확장을 설치하려면:

[Experience Platform 인터페이스](https://platform.adobe.com/)에서 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]**(으)로 이동합니다.

카탈로그에서 확장을 선택하거나 검색 창을 사용합니다.

대상을 클릭하여 강조 표시한 다음 오른쪽 레일에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다. **[!UICONTROL Configure]** 컨트롤이 회색으로 표시되어 있으면 **[!UICONTROL manage_properties]** 권한이 없습니다. [필수 구성 요소](#prerequisites)를 참조하십시오.

확장을 설치할 속성을 선택합니다. 새 속성을 만들 수도 있습니다. 속성은 규칙, 데이터 요소, 구성된 확장, 환경 및 라이브러리의 컬렉션입니다. 태그 설명서의 [속성 페이지 섹션](../../../tags/ui/administration/companies-and-properties.md#properties-page)에서 속성에 대해 알아봅니다.

워크플로는 설치를 완료하는 단계를 안내합니다.

확장 구성 옵션 및 설치 지원에 대한 자세한 내용은 [Adobe Exchange의 잘못된 태그 페이지](https://exchange.adobe.com/experiencecloud.details.100067.invoca.html)를 참조하십시오.

[데이터 수집 UI](https://experience.adobe.com/#/data-collection/)에서 바로 확장을 설치할 수도 있습니다. 자세한 내용은 태그 설명서의 [새 확장 추가](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension)에 대한 섹션을 참조하십시오.

## 확장 사용 방법 {#how-to-use}

확장을 설치하면 규칙 설정을 시작할 수 있습니다.

설치된 확장에 대한 규칙을 설정하여 이벤트 데이터를 특정 상황에서만 확장 대상으로 보낼 수 있습니다. 확장에 대한 규칙 설정에 대한 자세한 내용은 [태그 설명서](../../../tags/ui/managing-resources/rules.md)를 참조하세요.

## 확장 구성, 업그레이드 및 삭제 {#configure-upgrade-delete}

데이터 수집 UI에서 확장을 구성, 업그레이드 및 삭제할 수 있습니다.

>[!TIP]
>
>확장이 속성 중 하나에 이미 설치되어 있는 경우에도 Experience Platform UI에 확장에 대한 **[!UICONTROL 설치]**&#x200B;가 표시됩니다. 확장을 구성하거나 삭제하려면 [확장 설치](#install-extension)에 설명된 대로 설치 워크플로를 시작합니다.

확장을 업그레이드하려면 태그 설명서의 [확장 업그레이드 프로세스](../../../tags/ui/managing-resources/extensions/extension-upgrade.md)에 대한 안내서를 참조하십시오.
