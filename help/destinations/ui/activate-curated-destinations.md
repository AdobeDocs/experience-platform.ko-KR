---
title: LiveRamp 식별자를 기반으로 조정된 대상에 대상 활성화
type: Tutorial
description: LiveRamp Ramp Id를 사용하여 Adobe Experience Platform에서 연결된 TV 및 오디오 대상 및 기타 통합에 대한 대상을 활성화하는 방법을 알아봅니다.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# LiveRamp 식별자를 기반으로 조정된 대상에 대상 활성화

[!DNL LiveRamp]과(와) Adobe Real-Time CDP 통합을 사용하여 아래 나열된 대상과 같이 연결된 TV 및 오디오 대상을 포함하여 활성화를 위해 [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html)을(를) 사용하는 선별된 대상 목록에 대상을 활성화합니다.

>[!IMPORTANT]
>
>Experience Platform 인터페이스에서 LiveRamp RampID를 수집하거나 사용할 필요가 없습니다.
>
> 공식 [LiveRamp 설명서](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers)에 설명된 대로 PII 기반 식별자, 알려진 식별자 및 사용자 지정 ID와 같은 Real-Time CDP의 ID를 내보낼 수 있습니다. 그런 다음 이러한 ID는 활성화 프로세스에서 추가 다운스트림인 [!DNL LiveRamp RampIDs]과(와) 일치합니다.


* [[!DNL 4C Insights]](#insights)
* [[!DNL Acast]](#acast)
* [[!DNL Ampersand.tv]](#ampersand-tv)
* [[!DNL Captify]](#captify)
* [[!DNL Cardlytics]](#cardlytics)
* [[!DNL Disney (Hulu/ESPN/ABC)]](#disney)
* [[!DNL iHeartMedia]](#iheartmedia)
* [[!DNL Index Exchange]](#index-exchange)
* [[!DNL Magnite CTV Platform]](#magnite)
* [[!DNL Magnite DV+ (Rubicon Project)]](#magnite-dv)
* [[!DNL Nexxen]](#nexxen)
* [[!DNL One Fox]](#fox)
* [[!DNL Pandora]](#pandora)
* [[!DNL Reddit]](#reddit)
* [[!DNL Roku]](#roku)
* [[!DNL Spotify]](#spotify)
* [[!DNL Taboola]](#taboola)
* [[!DNL TargetSpot]](#targetspot)
* [[!DNL Teads]](#teads)
* [[!DNL WB Discovery]](#wb-discovery)

이 문서에서는 Real-Time CDP UI에서 직접 Real-Time CDP의 대상을 위에 나열된 대상으로 활성화하는 데 필요한 워크플로에 대해 설명합니다.

## 활성화 워크플로 {#workflow}

아래 그림과 같이 2단계 프로세스를 거치고 [LiveRamp - 온보딩](../catalog/advertising/liveramp-onboarding.md) 및 [LiveRamp - 배포](../catalog/advertising/liveramp-distribution.md) 대상을 사용하여 연결된 TV 및 오디오 대상에 대상을 활성화합니다.

![LiveRamp를 통해 Real-Time CDP에서 조정된 대상으로 대상을 활성화하는 워크플로를 보여 주는 다이어그램입니다.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

먼저 대상을 Real-Time CDP에서 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상으로 CSV 파일로 내보냅니다.

대상을 내보낸 후에는 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 대상을 사용하여 대상자를 활성화합니다.

>[!TIP]
>
>이 프로세스를 사용하면 활성화를 위해 [!DNL LiveRamp] 계정에 로그인할 필요 없이 Real-Time CDP UI에서 직접 [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) 등의 대상에 대상을 활성화할 수 있습니다.

### 비디오 튜토리얼 {#video}

이 페이지에 설명된 워크플로에 대한 전체적인 설명은 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### 1단계: 대상을 [!DNL LiveRamp - Onboarding] 대상을 통해 Experience Platform에서 LiveRamp로 보내기 {#onboarding}

LiveRamp RampID를 기반으로 대상자를 조정된 대상으로 활성화하기 위해 가장 먼저 수행해야 하는 작업은 **Experience Platform에서[!DNL LiveRamp]**(으)로 대상자를 내보내는 것입니다.

**[!DNL LiveRamp - Onboarding]** 대상을 사용하여 이 작업을 수행합니다.

![LiveRamp - 온보딩 대상 카드를 표시하는 Experience Platform UI 이미지](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

[!DNL LiveRamp - Onboarding] 대상을 구성하고 Experience Platform에서 대상을 내보내는 방법에 대해 알아보려면 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상 설명서를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL LiveRamp - Onboarding] 대상으로 파일을 내보낼 때 플랫폼에서는 각 [병합 정책 ID](../../profile/merge-policies/overview.md)에 대해 하나의 CSV 파일을 생성합니다. LiveRamp로 데이터 내보내기를 확인하는 방법에 대한 자세한 내용은 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상 설명서를 참조하십시오.


대상을 LiveRamp로 내보냈으면 [2단계](#distribution)를 계속 진행하세요.

>[!TIP]
>
>[2](#distribution)단계로 이동하기 전에 대상을 LiveRamp로 내보냈는지 [확인](../catalog/advertising/liveramp-onboarding.md#exported-data)하세요. [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)에 대한 설명서를 참조하고 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data)에 대한 특정 모니터링 세부 정보를 읽어 보십시오.

### 2단계: [!DNL LiveRamp - Distribution] 대상을 통해 연결된 TV 및 오디오 대상에 온보딩된 대상을 활성화합니다. {#distribution}

대상을 LiveRamp로 내보내는 데 성공했는지 [확인](../catalog/advertising/liveramp-onboarding.md#exported-data)한 후에는 [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney) 등과 같이 원하는 대상으로 대상을 활성화할 수 있습니다.

**[!DNL LiveRamp - Distribution]** 대상을 사용하여 대상([단계 1](#onboarding)에서 내보냄)을 활성화합니다.

![LiveRamp - 배포 대상 카드를 표시하는 Experience Platform UI 이미지](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

[단계 1](#onboarding)에서 내보낸 대상을 활성화하고 **[!DNL LiveRamp - Distribution]** 대상을 구성하는 방법에 대해 알아보려면 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 대상 설명서를 읽어 보십시오.

>[!IMPORTANT]
>
>**[!DNL LiveRamp - Distribution]** 대상의 **대상 선택** 단계에서는 [단계 1](#onboarding)에서 [LiveRamp - Onboarding](../catalog/advertising/liveramp-onboarding.md) 대상으로 내보낸 *정확히 동일한 대상*&#x200B;을 선택해야 합니다.

**[!DNL LiveRamp - Distribution]** 대상을 구성할 때 사용할 각 다운스트림 대상(Roku, Disney 등)에 대해 전용 연결을 만들어야 합니다.

>[!TIP]
>
>대상 이름을 지정할 때 Adobe은 `LiveRamp - Downstream Destination Name` 형식을 권장합니다. 이 이름 지정 패턴을 통해 대상 작업 영역의 [찾아보기](../ui/destinations-workspace.md#browse) 탭에서 대상을 빠르게 식별할 수 있습니다.
><br>
>예: `LiveRamp - Roku`.

![여러 LiveRamp 대상을 표시하는 Platform UI 스크린샷입니다.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

대상을 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상으로 성공적으로 내보내는 방법을 확인하려면 [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)에 대한 설명서를 참조하고 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data)에 대한 특정 모니터링 세부 정보를 읽어 보십시오.

선택한 광고 플랫폼(Roku, Disney 등)에 대한 대상자의 성공적인 활성화를 확인하려면 대상 플랫폼 계정에 로그인하고 활성화 지표를 확인합니다.
