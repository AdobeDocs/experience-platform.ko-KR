---
title: LiveRamp 식별자를 기반으로 조정된 대상에 대상 활성화
type: Tutorial
description: LiveRamp Ramp Id를 사용하여 Adobe Experience Platform에서 연결된 TV 및 오디오 대상 및 기타 통합에 대한 대상을 활성화하는 방법을 알아봅니다.
exl-id: 37e5bab9-588f-40b3-b65b-68f1a4b868f1
source-git-commit: c2e308b5e743f07062be9a34e23c4bc700b27463
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# LiveRamp 식별자를 기반으로 조정된 대상에 대상 활성화

과 Adobe Real-Time CDP 통합 사용 [!DNL LiveRamp] 을 사용하는 조정된 대상 목록에 대해 대상자를 활성화하려면 [!DNL [LiveRamp RampID]](https://docs.liveramp.com/connect/en/interpreting-rampid,-liveramp-s-people-based-identifier.html) 아래 나열된 대상과 같이 연결된 TV 및 오디오 대상을 포함하는 활성화의 경우.

>[!IMPORTANT]
>
>Experience Platform 인터페이스에서 LiveRamp RampID를 수집하거나 사용할 필요가 없습니다.
>
> 공식 문서에 설명된 대로 PII 기반 식별자, 알려진 식별자 및 사용자 지정 ID와 같은 Real-Time CDP의 ID를 내보낼 수 있습니다 [LiveRamp 설명서](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers). 그런 다음 이 ID를 와 일치시킵니다. [!DNL LiveRamp RampIDs] 활성화 프로세스의 추가 다운스트림


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

2단계 프로세스를 거치고 를 사용하여 연결된 TV 및 오디오 대상에 대상을 활성화합니다. [라이브 램프 - 온보딩](../catalog/advertising/liveramp-onboarding.md) 및 [LiveRamp - 배포](../catalog/advertising/liveramp-distribution.md) 아래 이미지에 표시된 대상.

![LiveRamp를 통해 Real-Time CDP에서 조정된 대상으로 대상을 활성화하는 워크플로를 보여 주는 다이어그램입니다.](../assets/ui/activate-curated-destinations-liveramp/workflow-diagram.png){width="1920" zoomable="yes"}

먼저 대상을 Real-Time CDP에서 로 내보냅니다. [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상을 CSV 파일로 지정합니다.

대상을 내보낸 후에는 를 사용하여 대상을 활성화합니다. [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 대상.

>[!TIP]
>
>이 프로세스를 통해 다음과 같은 대상에 대한 대상자를 활성화할 수 있습니다. [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)등에 로그인할 필요 없이 Real-Time CDP UI에서 바로 사용이 가능합니다. [!DNL LiveRamp] 활성화 계정.

### 비디오 튜토리얼 {#video}

이 페이지에 설명된 워크플로에 대한 전체적인 설명은 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3425367)

### 1단계: 다음을 통해 대상을 Experience Platform에서 LiveRamp로 보내기 [!DNL LiveRamp - Onboarding] 대상 {#onboarding}

LiveRamp RampID를 기반으로 조정된 대상에 대상을 활성화하기 위해 가장 먼저 수행해야 하는 작업은 다음과 같습니다. **Experience Platform에서 (으)로 대상자 내보내기[!DNL LiveRamp]**.

다음을 사용하여 이 작업을 수행합니다. **[!DNL LiveRamp - Onboarding]** 대상.

![LiveRamp - 온보딩 대상 카드를 보여 주는 Experience Platform UI 이미지](../assets/ui/activate-curated-destinations-liveramp/liveramp-onboarding-catalog.png)

을(를) 구성하는 방법을 알아보려면 [!DNL LiveRamp - Onboarding] 대상 및 Experience Platform에서 대상을 내보내려면 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상 설명서.

>[!IMPORTANT]
>
>파일을 로 내보낼 때 [!DNL LiveRamp - Onboarding] 대상, 플랫폼은 각각에 대해 하나의 CSV 파일을 생성합니다. [병합 정책 ID](../../profile/merge-policies/overview.md). 다음을 참조하십시오. [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) LiveRamp로 데이터 내보내기의 유효성을 검사하는 방법에 대한 자세한 내용은 대상 설명서를 참조하십시오.


대상자를 LiveRamp로 내보내기했으면 계속 진행합니다. [2단계](#distribution).

>[!TIP]
>
>로 이동하기 전 [2단계](#distribution), [유효성 검사](../catalog/advertising/liveramp-onboarding.md#exported-data) 대상자를 LiveRamp로 내보냈습니다. 다음에서 설명서를 참조하십시오. [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 다음에 대한 특정 모니터링 세부 사항을 읽어 보십시오. [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

### 2단계: 를 통해 연결된 TV 및 오디오 대상에 온보딩된 대상 활성화 [!DNL LiveRamp - Distribution] 대상 {#distribution}

다음 작업을 수행한 후 [확인됨](../catalog/advertising/liveramp-onboarding.md#exported-data) 대상자를 LiveRamp로 성공적으로 내보냈으므로 다음과 같이 대상자를 선호하는 대상으로 활성화할 수 있습니다. [[!DNL Roku]](../catalog/advertising/liveramp-distribution.md#roku), [[!DNL Disney]](../catalog/advertising/liveramp-distribution.md#disney)등.

대상자(내보낸 항목)를 활성화합니다. [1단계](#onboarding))을 사용하여 다음을 수행합니다 **[!DNL LiveRamp - Distribution]** 대상.

![LiveRamp - 배포 대상 카드를 보여 주는 Experience Platform UI 이미지](../assets/ui/activate-curated-destinations-liveramp/liveramp-distribution-catalog.png)

을(를) 구성하는 방법을 알아보려면 **[!DNL LiveRamp - Distribution]** 내보낸 대상 및 대상 활성화 [1단계](#onboarding), 다음을 읽습니다 [[!DNL LiveRamp - Distribution]](../catalog/advertising/liveramp-distribution.md) 대상 설명서.

>[!IMPORTANT]
>
>다음에서 **대상자 선택** 의 단계 **[!DNL LiveRamp - Distribution]** 대상, 다음을 선택해야 합니다. *정확히 동일한 대상* (으)로 내보낸 [라이브 램프 - 온보딩](../catalog/advertising/liveramp-onboarding.md) 대상 위치: [1단계](#onboarding).

을(를) 구성할 때 **[!DNL LiveRamp - Distribution]** 대상, 사용하려는 각 다운스트림 대상(Roku, Disney 등)에 대해 전용 연결을 만들어야 합니다.

>[!TIP]
>
>대상 이름을 지정할 때 Adobe은 다음 형식을 권장합니다. `LiveRamp - Downstream Destination Name`. 이 이름 지정 패턴을 통해 [찾아보기](../ui/destinations-workspace.md#browse) 대상 작업 영역의 탭입니다.
><br>
>예: `LiveRamp - Roku`.

![여러 LiveRamp 대상을 보여 주는 Platform UI 스크린샷입니다.](../assets/ui/activate-curated-destinations-liveramp/liveramp-naming.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

대상자를 (으)로 성공적으로 내보내는 방법을 확인하려면 [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md) 대상, 다음 설명서에 대한 참조: [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) 다음에 대한 특정 모니터링 세부 사항을 읽어 보십시오. [[!DNL LiveRamp - Onboarding]](../catalog/advertising/liveramp-onboarding.md#exported-data).

선택한 광고 플랫폼(Roku, Disney 등)에 대한 대상자의 성공적인 활성화를 확인하려면 대상 플랫폼 계정에 로그인하고 활성화 지표를 확인합니다.
