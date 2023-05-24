---
title: Assurance의 스트리밍 미디어용 Adobe Analytics 보기
description: 이 안내서에서는 Adobe Experience Platform Assurance와 함께 스트리밍 미디어용 Adobe Analytics를 사용하는 방법을 설명합니다.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---

# Assurance의 스트리밍 미디어용 Adobe Analytics 보기

스트리밍 미디어용 Adobe Analytics와 Adobe Experience Platform Assurance의 통합을 통해 이제 모바일 앱에서 Media Analytics 구현의 유효성을 검사할 수 있습니다. Media Analytics 보기에는 다음과 같이 미디어 세션에서 추적된 것이 표시됩니다.

- 모든 컨텐츠 코어, 표준 메타데이터 및 사용자 지정 메타데이터 속성뿐만 아니라 세션 종료 및 세션 완료 이벤트를 포함하는 세션 시작 이벤트입니다.
- 모든 광고 속성이 첨부된 광고 브레이크 시작 및 광고 시작 이벤트와 두 이벤트에 대한 건너뛰기 및 완료 이벤트.
- 챕터 시작에는 모든 속성이 첨부되어 있고, 챕터 건너뛰기 및 챕터 완료 이벤트도 포함되어 있습니다.
- 모든 재생 변경 이벤트(재생, 일시 중지, 버퍼, 오류, 비트율 변경).
- 모든 플레이어 상태 변경 추적 이벤트(시작, 종료).

데이터가 Analytics에서 처리되면 후처리된 상태 및 데이터(예: 미디어 체류 시간 및 총 일시 중지 기간)도 이벤트 세부 사항 보기에서 사용할 수 있습니다.

## 시작하기

계속하기 전에 다음 서비스가 있는지 확인하십시오.

- 다음 [Adobe Experience Platform 데이터 수집 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

애플리케이션에 Assurance를 설치하는 방법을 알아보려면 [assurance 구현 안내서](../tutorials/implement-assurance.md).

## 스트리밍 미디어용 Adobe Analytics에서 보증 사용

Adobe Analytics용 앱을 연결하고 설정했으면 스트리밍 미디어용 앱을 구성할 준비가 되었습니다. 왼쪽 패널 하단에서 을 선택합니다. **[!UICONTROL 구성]** media Analytics 이벤트 보기 및 를 추가하려면 **저장** 그래.

![](./images/adobe-analytics-streaming-media/configure.png) 구성

추가되면 다음을 선택합니다. **[!UICONTROL 미디어 분석 이벤트]** 다음에서 보기 **[!UICONTROL Adobe Analytics]** 섹션 을 참조하십시오.

![선택](./images/adobe-analytics-streaming-media/select.png)

다음에서 **[!UICONTROL 미디어 분석 이벤트]** 보기: 세션 ID(VSID)별로 검색 및 필터링하여 특정 미디어 세션을 볼 수 있습니다. 추가 이벤트 세부 정보를 보려면 특정 이벤트를 선택합니다.

![미디어 이벤트](./images/adobe-analytics-streaming-media/media-events.png)

API 호출을 더 간결하게 보려면 를 선택하여 플레이헤드 업데이트 이벤트를 숨길 수도 있습니다. **[!UICONTROL 플레이헤드 업데이트 이벤트 숨기기]** 필터.

![플레이헤드 숨기기](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>후처리된 미디어 분석 데이터를 보려면 SDK 버전(Android Media 2.1.2 및 iOS AEPMedia 3.0.1 이상)을 사용해야 합니다

후처리된 데이터를 보려면 세션 시작 이벤트를 찾아 상태 열에서 세션이 완료되었는지 확인합니다. 완료되면 이벤트를 클릭하여 이벤트 세부 사항 보기의 미디어 세션 요약을 봅니다. 자세한 내용을 보려면 아래로 스크롤하여 사후 처리된 세부 정보를 찾습니다.

![후처리된 보기](./images/adobe-analytics-streaming-media/post-processed-view.png)
