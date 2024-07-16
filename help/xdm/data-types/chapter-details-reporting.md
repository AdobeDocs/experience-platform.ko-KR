---
title: 챕터 세부 정보 보고 데이터 유형
description: 챕터 세부 사항 보고 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 73ebfbe3-66c3-4ef9-9944-d9cb5772127b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 8%

---

# [!UICONTROL 챕터 세부 정보] 보고 데이터 형식

[!UICONTROL 챕터 세부 정보] 보고는 미디어 콘텐츠 내의 챕터 또는 세그먼트와 관련된 다양한 특성을 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. [!UICONTROL 챕터 세부 정보] 보고 데이터 형식을 사용하여 챕터 이름, 기간, 위치, ID, 재생 상태(시작/완료) 및 각 챕터에서 보낸 시간과 같은 세부 정보를 캡처합니다. 미디어 보고 필드는 Adobe 서비스에서 사용자가 보낸 미디어 컬렉션 필드를 분석하는 데 사용됩니다. 이 데이터는 다른 특정 사용자 지표와 함께 계산되고 보고됩니다.

![챕터 세부 정보 보고 데이터 형식의 다이어그램입니다.](../images/data-types/chapter-details-reporting.png)

>[!NOTE]
>
>각 디스플레이 이름에는 해당 오디오 및 비디오 매개 변수에 대한 추가 정보를 볼 수 있는 링크가 포함되어 있습니다. 연결된 페이지에는 Adobe, 구현 값, 네트워크 매개 변수, 보고 및 중요 고려 사항으로 수집된 비디오 및 데이터에 대한 세부 사항이 포함되어 있습니다.

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|-----------|--------------------------------------------------------------|
| [[!UICONTROL 챕터 완료됨]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-complete) | `isCompleted` | 부울 | 챕터의 완료 여부. |
| [[!UICONTROL 챕터 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter) | `ID` | 문자열 | 자동으로 생성된 챕터의 ID입니다. |
| [[!UICONTROL 챕터 길이 또는 기간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-length) | `length` | 정수 | 챕터 길이(단위: 초). |
| [[!UICONTROL 챕터 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-name) | `friendlyName` | 문자열 | 챕터 및/또는 세그먼트의 이름입니다. |
| [[!UICONTROL 챕터 오프셋]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-offset) | `offset` | 정수 | 처음부터 콘텐츠 내에 있는 챕터의 오프셋(초)입니다. |
| [[!UICONTROL 챕터 위치]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-position) | `index` | 정수 | 콘텐츠 내에서 챕터의 위치(색인, 정수)입니다. |
| [[!UICONTROL 챕터 시작됨]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-start) | `isStarted` | 부울 | 챕터가 시작되었는지 여부. |
| [[!UICONTROL 챕터 재생 시간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/chapter-parameters.html#chapter-time-spent) | `timePlayed` | 정수 | 챕터에서 보낸 시간(초)입니다. |
