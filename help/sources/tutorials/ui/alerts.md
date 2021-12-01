---
keywords: Experience Platform;홈;인기 있는 주제 경고
description: 데이터 흐름을 만들 때 경고에 가입하여 흐름 실행 상태, 성공 또는 실패와 관련된 경고 메시지를 받을 수 있습니다.
title: UI에서 컨텍스트 내 경고 구독
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# UI에서 소스 데이터 흐름을 모니터링하려면 경고 메시지에 가입하십시오

Adobe Experience Platform에서는 Adobe Experience Platform 활동에 대한 이벤트 기반 경고를 구독할 수 있습니다. 경고는 를 폴링할 필요가 없어지거나 없어집니다 [[!DNL Observability Insights] API](../../../observability/api/overview.md) 작업이 완료되었는지, 워크플로우 내의 특정 이정표에 도달했는지 또는 오류가 발생했는지 확인하기 위해.

데이터 흐름을 만들 때 경고에 가입하여 흐름 실행 상태, 성공 또는 실패와 관련된 경고 메시지를 받을 수 있습니다.

이 문서에서는 경고를 구독하고 흐름 실행에 대한 경고 메시지를 받는 방법에 대해 설명합니다.

## 시작하기

이 문서를 사용하려면 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
* [가시성](../../../observability/home.md): [!DNL Observability Insights] 통계 지표 및 이벤트 알림을 사용하여 플랫폼 활동을 모니터링할 수 있습니다.
   * [경고](../../../observability/alerts/overview.md): 플랫폼 작업의 특정 조건 세트에 도달하면(예: 시스템이 임계값을 위반한 경우 발생할 수 있는 문제) Platform은 해당 조건을 구독한 조직의 모든 사용자에게 경고 메시지를 전달할 수 있습니다.

## UI에서 경고 구독 {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="소스 경고 구독"
>abstract="경고를 사용하면 소스 데이터 흐름의 상태에 따라 알림을 받을 수 있습니다. 데이터 흐름이 시작되었거나, 성공했거나, 실패했거나, 데이터를 수집하지 않은 경우 업데이트를 가져오도록 경고 알림을 설정할 수 있습니다."
>text="Learn more in documentation"
