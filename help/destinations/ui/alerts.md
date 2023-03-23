---
keywords: Experience Platform;홈;인기 있는 주제 경고;대상
description: 데이터 흐름을 만들 때 경고에 가입하여 흐름 실행 상태, 성공 또는 실패와 관련된 경고 메시지를 받을 수 있습니다.
title: 컨텍스트 내 대상 경고 구독
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 3bb9858c236c91e1567fd8e78988f4049537ffe3
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 5%

---

# 컨텍스트 내 대상 경고 구독

Adobe Experience Platform에서는 Adobe Experience Platform 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 경고는 를 폴링할 필요가 없어지거나 없어집니다 [[!DNL Observability Insights] API](../../observability/api/overview.md) 작업이 완료되었는지, 워크플로우 내의 특정 이정표에 도달했는지 또는 오류가 발생했는지 확인하기 위해.

데이터 흐름을 만들 때 경고를 구독하면 흐름 실행 상태, 성공 또는 실패와 관련된 경고 메시지를 받을 수 있습니다.

이 문서에서는 대상 데이터 흐름에 대한 경고 메시지를 구독하는 방법에 대해 설명합니다.

## 시작하기

이 문서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [대상](../home.md): Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
* [가시성](../../observability/home.md): [!DNL Observability Insights] 통계 지표 및 이벤트 알림을 사용하여 플랫폼 활동을 모니터링할 수 있습니다.
   * [경고](../../observability/alerts/overview.md): 플랫폼 작업의 특정 조건 세트에 도달하면(예: 시스템이 임계값을 위반한 경우 발생할 수 있는 문제) Platform은 해당 조건을 구독한 조직의 모든 사용자에게 경고 메시지를 전달할 수 있습니다.

## UI에서 경고 구독 {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="대상 알림 구독"
>abstract="경고를 사용하여 대상 데이터 흐름 상태에 따라 알림을 수신할 수 있습니다. 데이터 흐름이 시작되거나 성공 또는 실패했을 경우 또는 데이터를 대상으로 보내지 않은 경우 경고 알림을 설정하여 업데이트를 받을 수 있습니다."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>데이터 흐름에 대한 이메일 기반 경고 알림을 받으려면 플랫폼 계정에 대해 전자 메일의 인스턴트 알림을 활성화해야 합니다.

다음 기간 동안 데이터 흐름에 대한 경고를 활성화할 수 있습니다 [!UICONTROL 새 대상 구성] 의 단계 [대상 연결](connect-destination.md) 워크플로우.

![대상 경고 섹션을 보여주는 UI 이미지입니다.](../assets/ui/alerts/destination-alerts.png)

가입하려는 경고를 선택한 다음 선택합니다 **[!UICONTROL 다음]** 데이터 흐름을 검토하고 완료하려면

대상 데이터 흐름에서 사용할 수 있는 경고는 아래 표에 설명되어 있습니다.

* 스트리밍 대상의 경우 [!DNL Activation Skipped Rate Exceeded] 경고를 사용할 수 있습니다.
* 파일 기반 대상의 경우 모든 경고를 사용할 수 있습니다.

| 경고 | 설명 |
| --- | --- |
| 대상 흐름 실행 지연 | 이 경고는 대상 흐름 실행이 세그먼트를 활성화하는 데 150분 이상 걸릴 때 알려줍니다. |
| 대상 흐름 실행 실패 | 이 경고는 세그먼트를 대상에 활성화하는 동안 오류가 발생하면 알려줍니다. |
| 대상 흐름 실행 성공 | 이 경고는 세그먼트가 대상에 성공적으로 활성화되면 알려줍니다. |
| 대상 흐름 실행 시작 | 이 경고는 대상 흐름 실행이 세그먼트 활성화를 시작할 때 사용자에게 알려줍니다. |
| 활성화 건너뛴 비율 초과 | 이 경고는 활성화 건너뛰기 비율이 총 활성화 중 1%를 초과하면 알려줍니다. 활성화 중에 속성 또는 동의 위반이 누락된 경우 ID를 건너뜁니다. |

## 경고 수신 {#receiving-alerts}

대상 데이터 흐름이 실행되면 UI 또는 이메일을 통해 경고를 받을 수 있습니다.

### UI에서 경고 받기 {#receiving-alerts-in-ui}

경고는 Platform UI의 상단 헤더에 있는 알림 아이콘으로 UI에 표시됩니다. 데이터 흐름과 관련된 특정 경고 메시지를 보려면 알림 아이콘을 선택합니다.

![Experience Platform에 알림 아이콘을 보여주는 UI 이미지](../assets/ui/alerts/notification.png)

알림 패널이 나타나고 생성한 데이터 플로에 상태 업데이트 목록이 표시됩니다.

![알림 패널을 표시하는 UI 이미지](../assets/ui/alerts/alert-window.png)

경고 메시지를 마우스로 가리키면 읽은 것으로 표시하거나 시계 아이콘을 선택하여 데이터 흐름 상태에 대한 향후 미리 알림을 설정할 수 있습니다.

![알림 미리 알림 옵션을 보여주는 UI 이미지](../assets/ui/alerts/remind-me.png)

데이터 집합에 대한 특정 정보를 보려면 경고 메시지를 선택하십시오.

![알림을 선택하는 방법을 보여주는 UI 이미지](../assets/ui/alerts/select-alert-message.png)

다음 [!UICONTROL 데이터 흐름 실행 세부 정보] 페이지가 나타납니다. 화면 상단에는 해당 속성, 해당 데이터 흐름 실행 ID 및 높은 수준의 오류 요약이 포함된 데이터 흐름 개요가 표시됩니다.

![데이터 흐름 실행 세부 사항 페이지를 보여주는 UI 이미지.](../assets/ui/alerts/dataflow-overview.png)

페이지 하단에는 모든 항목이 표시됩니다 [!UICONTROL 데이터 흐름 실행 오류] 데이터 흐름 실행 단계 동안 발생한 작업입니다. 여기에서 오류 진단을 미리 보거나 [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) 오류 진단 또는 데이터 플로우에 해당하는 파일 매니페스트를 다운로드하려면 다음을 수행하십시오.

![데이터 흐름 실행 세부 사항 페이지를 표시하는 UI 이미지(오류 섹션에 강조 표시가 있는 경우)](../assets/ui/alerts/dataflow-run-error.png)

데이터 흐름 오류 처리에 대한 자세한 내용은 [UI에서 대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md).

### 이메일로 경고 받기 {#receiving-alerts-by-email}

데이터 흐름에 대한 경고도 이메일로 사용자에게 전달됩니다. 데이터 흐름에 대한 자세한 내용을 보려면 전자 메일 본문에서 데이터 흐름 이름을 선택합니다.

![경고 전자 메일의 스크린샷](../assets/ui/alerts/email.png)

UI 경고와 유사하며, [!UICONTROL 데이터 흐름 실행 개요] 데이터 흐름과 관련된 오류를 조사할 수 있는 인터페이스를 제공하는 페이지가 나타납니다.

![데이터 흐름 개요](../assets/ui/alerts/dataflow-overview.png)

## 경고 구독 및 구독 취소 {#subscribe-and-unsubscribe}

추가 경고에 가입하거나 대상의 기존 대상 데이터 로드에 대해 설정된 경고의 구독을 취소할 수 있습니다 [!UICONTROL 찾아보기] 페이지.

![대상 찾아보기 페이지를 보여주는 UI 이미지](../assets/ui/alerts/destination-list.png)

경고를 받을 대상 연결을 찾아 줄임표( )를 선택합니다`...`) 를 클릭하여 옵션 드롭다운 메뉴를 확인합니다. 다음 을 선택합니다. **[!UICONTROL 경고 구독]** 대상 데이터 흐름의 경고 설정을 수정하려면 다음을 수행합니다.

![대상 옵션을 보여주는 UI 이미지](../assets/ui/alerts/destination-alerts-subscribe.png)

대상 경고 목록을 제공하는 팝업 창이 나타납니다. 가입하려는 경고를 선택하거나 가입을 해지할 경고를 선택 취소합니다. 완료되면 을 선택합니다 **[!UICONTROL 저장]**.

![대상 경고 가입 페이지를 보여주는 UI 이미지](../assets/ui/alerts/destination-alerts-list.png)

## 다음 단계 {#next-steps}

이 문서에서는 대상 데이터 흐름에 대한 컨텍스트 내 경고를 구독하는 방법에 대한 단계별 가이드를 제공합니다. 자세한 내용은 [경고 UI 안내서](../../observability/alerts/ui.md).
