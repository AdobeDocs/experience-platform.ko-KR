---
title: 확장된 활성화를 통해 Audience Manager 대상 활성화
description: 확장된 Audience Manager 활성화를 통해 소셜 및 광고 대상에 Audience Manager 대상을 활성화하는 방법을 알아봅니다.
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Audience Manager 확장 활성화를 통해 대상자 활성화

이 페이지에서는 확장된 활성화에서 지원하는 대상 플랫폼에 대해 Audience Manager 대상을 활성화하기 위해 수행해야 하는 전체적인 워크플로에 대해 설명합니다.

## 시작하기에 앞서 {#before-you-begin}

이 안내서에 설명된 단계는 다음을 읽었다고 가정합니다. [확장된 활성화 개요 페이지](overview.md) 그리고 대상자 활성화를 위한 사전 요구 사항을 충족함을 확인했습니다.

>[!IMPORTANT]
>
>다음을 통해 대상자를 활성화하려면 [!DNL Expanded Activation], Audience Manager 대상이 다음을 기반으로 하는지 확인합니다. **해시된 이메일 주소**. 다음을 참조하십시오. [전제 조건](overview.md#prerequisites) 을 참조하십시오.

## 1단계: Audience Manager 소스 연결 구성 {#configure-source}

다음 [Audience Manager 소스 커넥터](../sources/connectors/adobe-applications/audience-manager.md) 확장된 활성화에서 지원하는 대상 플랫폼에서 활성화하기 위해 Adobe Audience Manager에서 수집된 대상 데이터를 보냅니다.

다음 방법에 대한 안내서를 따르십시오. [Audience Manager 소스 연결 만들기](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 소스 커넥터를 구성합니다.

![Audience Manager 소스 연결이 있는 소스 탭을 표시하는 플랫폼 UI 이미지입니다.](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager 소스 커넥터는 확장된 활성화에서 사용할 수 있는 유일한 소스 커넥터입니다.
>
>추가 식별자를 기반으로 대상을 수집하려면 다음 에디션을 구입해야 합니다. [Real-Time CDP](../rtcdp/overview.md). 자세한 내용은 Adobe 담당자에게 문의하십시오.

### 수집된 대상 보기 및 모니터링 {#view-audiences}

Audience Manager에서 확장된 활성화로 가져오는 대상은에서 볼 수 있습니다. **[!UICONTROL 대상]** 대시보드입니다.

대상자를 보려면 다음으로 이동하십시오. **[!UICONTROL 고객]** -> **[!UICONTROL 대상]** -> **[!UICONTROL 찾아보기]**.

![대상 페이지를 보여주는 플랫폼 UI 이미지입니다.](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* 대상자가 확장된 활성화에서 완전히 채워지는 데 최대 48시간이 걸릴 수 있습니다. 이는 기존 Audience Manager 대상에 대한 업데이트에도 적용됩니다.
>* 새로 만든 Audience Manager 대상은 확장된 정품 인증에 자동으로 표시되지 않습니다. 확장된 활성화에서 새 세그먼트를 수집하려면 Audience Manager 소스 커넥터를 통해 추가해야 합니다.

Audience Manager 소스 커넥터를 구성한 후 로 이동합니다. [2단계](#create-destination-connection).

## 2단계: 새 대상 연결 만들기 {#create-destination-connection}

선택한 대상 플랫폼으로 Audience Manager 대상을 보내려면 먼저 대상 플랫폼에 대한 연결을 만들어야 합니다.

왼쪽 사이드바에서 **[!UICONTROL 연결]** -> **[!UICONTROL 대상]** -> **[!UICONTROL 카탈로그]**.

에 사용 가능한 대상 범주 [!DNL Expanded Activation] 은(는) [advertising](../destinations/catalog/advertising/overview.md) 및 [소셜](../destinations/catalog/social/overview.md).

![확장된 활성화의 대상 카탈로그를 보여주는 플랫폼 UI 이미지입니다.](assets/destination-catalog.png)

대상 플랫폼에 대한 새 연결을 만들려면 다음 안내서를 따르십시오. [새 대상 연결을 만드는 방법](../destinations/ui/connect-destination.md). 그런 다음 로 이동합니다. [3단계](#activate-audiences).

## 3단계: 대상에 대한 대상자 활성화 {#activate-audiences}

성공 후 [수집된 Audience Manager 대상](#configure-source) 및 [새 대상 연결을 만들었습니다.](#create-destination-connection), 이제 대상을 원하는 대상 플랫폼에 활성화할 수 있습니다.

![확장된 활성화의 대상 카탈로그를 보여주는 플랫폼 UI 이미지입니다.](assets/activate-audiences.png)

대상을 활성화하려면 의 안내서를 따르십시오. [스트리밍 대상에 대상을 활성화하는 방법](../destinations/ui/activate-segment-streaming-destinations.md).

## 대상자 활성화 확인 {#verify}

다음 확인: [대상 모니터링 설명서](../dataflows/ui/monitor-destinations.md) 대상으로의 데이터 흐름을 모니터링하는 방법에 대한 자세한 정보.