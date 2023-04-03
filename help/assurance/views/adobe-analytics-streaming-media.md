---
title: Assurance의 스트리밍 미디어 보기용 Adobe Analytics
description: 이 안내서에서는 Adobe Experience Platform Assurance와 함께 Adobe Analytics for Streaming Media를 사용하는 방법을 설명합니다.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---


# Assurance의 Adobe Analytics for Streaming Media 보기

이제 스트리밍 미디어용 Adobe Analytics와 Adobe Experience Platform Assurance가 통합되었으므로 모바일 앱에서 Media Analytics 구현의 유효성을 검사할 수 있습니다. Media Analytics 보기 에는 미디어 세션에서 추적할 항목이 표시됩니다. 예:

- 세션 종료 및 세션 완료 이벤트는 물론 모든 컨텐츠 코어, 표준 메타데이터 및 사용자 지정 메타데이터 속성이 포함된 세션 시작 이벤트입니다.
- 모든 광고 속성이 첨부된 광고 브레이크 시작 및 광고 시작 이벤트와 두 이벤트에 대한 건너뛰기 및 완료 이벤트입니다.
- 장 시작 및 장 건너뛰기 및 장 완료 이벤트뿐만 아니라 모든 속성을 첨부합니다.
- 모든 재생 변경 이벤트(재생, 일시 정지, 버퍼, 오류, 비트율 변경)가 있습니다.
- 모든 플레이어 상태 변경 추적 이벤트(시작, 끝).

데이터가 Analytics에서 처리되면 사후 처리 상태 및 데이터(예: 미디어 체류 시간 및 총 일시 중지 기간)를 이벤트 세부 사항 보기에서 사용할 수도 있습니다.

## 시작하기

계속하기 전에 다음 서비스가 있는지 확인하십시오.

- 다음 [Adobe Experience Platform 데이터 수집 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform 보증](https://experience.adobe.com/assurance)

응용 프로그램에 Assurance를 설치하는 방법을 알아보려면 [보증 구현 안내서](../tutorials/implement-assurance.md).

## 스트리밍 미디어용 Adobe Analytics에서 Assurance 사용

Adobe Analytics용 앱을 연결하고 설정하면 스트리밍 미디어 분석에 맞게 구성할 수 있습니다. 왼쪽 패널 아래에서 을 선택합니다 **[!UICONTROL 구성]** media Analytics 이벤트 보기 및 **저장** 그래

![](./images/adobe-analytics-streaming-media/configure.png) 구성

추가한 후 **[!UICONTROL Media Analytics 이벤트]** 에서 보기 **[!UICONTROL Adobe Analytics]** 세션 추적의 유효성을 검사하는 섹션.

![선택](./images/adobe-analytics-streaming-media/select.png)

에서 **[!UICONTROL Media Analytics 이벤트]** 보기, VSID(세션 ID)별로 검색 및 필터링하여 특정 미디어 세션을 볼 수 있습니다. 추가 이벤트 세부 사항을 보려면 특정 이벤트를 선택합니다.

![미디어 이벤트](./images/adobe-analytics-streaming-media/media-events.png)

API 호출에 대한 보다 간결한 보기를 위해 를 선택하여 플레이헤드 업데이트 이벤트를 숨길 수도 있습니다 **[!UICONTROL 플레이헤드 업데이트 이벤트 숨기기]** 필터.

![플레이헤드 숨기기](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>사후 처리 미디어 분석 데이터를 보려면 SDK 버전을 사용해야 합니다. Android Media 2.1.2 및 iOS AEPMedia 3.0.1(또는 이상)

사후 처리 데이터를 보려면 세션 시작 이벤트를 찾고 상태 열에서 세션이 완료되었는지 확인합니다. 완료되면 이벤트를 클릭하여 이벤트 세부 사항 보기에서 미디어 세션 요약을 확인합니다. 자세한 내용을 보려면 아래로 스크롤하여 후 처리된 세부 정보를 찾습니다.

![후 처리된 보기](./images/adobe-analytics-streaming-media/post-processed-view.png)
