---
title: 광고 세부 정보 보고 데이터 유형
description: Advertising Details 보고 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 11%

---

# [!UICONTROL 광고 세부 정보] 보고 데이터 유형

[!UICONTROL 광고 세부 정보] 보고는 광고와 관련된 주요 속성을 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 여기에는 광고 ID, 광고주 및 캠페인 ID, 길이, 시퀀스 내 위치, 광고를 렌더링하는 플레이어에 대한 세부 정보 등이 포함됩니다. 이 데이터 유형을 사용하여 광고 성능 및 참여의 다양한 측면을 추적 및 분석하고, 대상자가 다양한 광고와 상호 작용하고 응답하는 방식에 대한 통찰력을 제공할 수 있습니다.

+++광고 세부 정보 보고 데이터 유형의 다이어그램을 표시하려면 선택합니다.
![광고 세부 정보 보고 데이터 유형 다이어그램입니다.](../images/data-types/advertising-details-information.png)
+++

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 광고 이름] | `friendlyName` | 문자열 | 사람이 인식할 수 있는 광고 이름. 보고 시 &quot;광고 이름&quot;은 분류이고, &quot;광고 이름(변수)&quot;은 eVar입니다. |
| [!UICONTROL 광고 ID] | `name` | 문자열 | 광고 ID입니다. 모든 정수 및/또는 문자 조합입니다. |
| [!UICONTROL 광고 길이 또는 기간] | `length` | 정수 | 비디오 광고 길이(초)입니다. |
| [!UICONTROL Pod의 광고 위치(광고 시작)] | `podPosition` | 정수 | 상위 광고 시작 내의 광고 색인. 예를 들어, 첫 번째 광고에는 색인 0이 있고 두 번째 광고에는 색인 1이 있습니다. |
| [!UICONTROL 광고 플레이어 이름] | `playerName` | 문자열 | 광고 렌더링을 담당하는 플레이어의 이름입니다. |
| [!UICONTROL 광고 광고주] | `advertiser` | 문자열 | 광고에서 다루고 있는 제품의 회사 또는 브랜드입니다. |
| [!UICONTROL 광고 캠페인] | `campaignID` | 문자열 | 광고 캠페인의 ID입니다. |
| [!UICONTROL 광고 크리에이티브 ID] | `creativeID` | 문자열 | 광고 문안 ID. |
| [!UICONTROL 광고 사이트 ID] | `siteID` | 문자열 | 광고 사이트의 ID입니다. |
| [!UICONTROL 광고 크리에이티브 URL] | `creativeURL` | 문자열 | 광고 문안 URL. |
| [!UICONTROL 광고 배치 ID] | `placementID` | 문자열 | 광고의 배치 ID입니다. |
| [!UICONTROL 광고 완료됨] | `isCompleted` | 부울 | 광고가 완료되었는지 추적합니다. |
| [!UICONTROL 광고 시작됨] | `isStarted` | 부울 | 광고가 시작되었는지 추적합니다. |
| [!UICONTROL 광고 재생 시간] | `timePlayed` | 정수 | 광고를 시청하는 데 걸린 총 시간(즉, 재생되는 시간(초))입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
