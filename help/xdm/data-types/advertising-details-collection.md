---
title: Advertising 세부 정보 수집 데이터 유형
description: Advertising 세부 정보 수집 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 14%

---

# [!UICONTROL Advertising 세부 정보] 컬렉션 데이터 형식

[!UICONTROL Advertising 세부 정보] 컬렉션은 광고와 관련된 주요 특성을 캡처하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 여기에는 광고 ID, 광고주 및 캠페인 ID, 길이, 시퀀스 내 위치, 광고를 렌더링하는 플레이어에 대한 세부 정보 등이 포함됩니다. 이 데이터 유형을 사용하여 광고 성능 및 참여의 다양한 측면을 추적 및 분석하고, 대상자가 다양한 광고와 상호 작용하고 응답하는 방식에 대한 통찰력을 제공할 수 있습니다. 제공한 이 정보는 스트리밍 데이터를 추적하는 데 사용됩니다.

+++Advertising 세부 정보 수집 데이터 유형의 다이어그램을 표시하려면 선택합니다.
![Advertising Details Collection 데이터 형식의 다이어그램입니다.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>각 디스플레이 이름에는 해당 오디오 및 비디오 매개 변수에 대한 추가 정보를 볼 수 있는 링크가 포함되어 있습니다. 연결된 페이지에는 Adobe, 구현 값, 네트워크 매개 변수, 보고 및 중요 고려 사항으로 수집된 비디오 및 데이터에 대한 세부 사항이 포함되어 있습니다.

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------|-----------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL 광고 광고주]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | 문자열 | 아니요 | 광고에서 다루고 있는 제품의 회사 또는 브랜드입니다. |
| [[!UICONTROL 광고 캠페인]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | 문자열 | 아니요 | 광고 캠페인의 ID입니다. |
| [[!UICONTROL 광고 크리에이티브 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | 문자열 | 아니요 | 광고 크리에이티브 ID. |
| [[!UICONTROL 광고 크리에이티브 URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | 문자열 | 아니요 | 광고 크리에이티브 URL. |
| [[!UICONTROL Pod의 광고 위치(광고 시작)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | 정수 | 예 | 상위 광고 시작 내의 광고 색인. 예를 들어, 첫 번째 광고에는 색인 0이 있고 두 번째 광고에는 색인 1이 있습니다. |
| [[!UICONTROL 광고 길이 또는 기간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | 정수 | 예 | 비디오 광고 길이(초)입니다. |
| [[!UICONTROL 광고 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | 문자열 | 예 | 사람이 인식할 수 있는 광고 이름. 보고에서 &quot;광고 이름&quot;은 분류이고 &quot;광고 이름(변수)&quot;은 eVar입니다. |
| [[!UICONTROL 광고 배치 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | 문자열 | 아니요 | 광고의 배치 ID입니다. |
| [[!UICONTROL 광고 플레이어 이름]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | 문자열 | 예 | 광고 렌더링 책임 플레이어 이름. |
| [[!UICONTROL 광고 사이트 ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | 문자열 | 아니요 | 광고 사이트의 ID입니다. |

{style="table-layout:auto"}
