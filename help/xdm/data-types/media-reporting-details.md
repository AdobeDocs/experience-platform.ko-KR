---
title: 미디어 보고 세부 정보 데이터 유형
description: 미디어 보고 세부 사항 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: e8bf20a9-9ac0-4339-8200-5d6d9328ce3b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---

# [!UICONTROL 미디어 보고 세부 정보] 데이터 형식

>[!NOTE]
>
>미디어 컬렉션 필드는 데이터를 캡처하여 추가 처리를 위해 다른 Adobe 서비스로 보냅니다. 미디어 보고 필드는 Adobe 서비스에서 사용자가 보낸 미디어 컬렉션 필드를 분석하는 데 사용됩니다. 이 데이터는 다른 특정 사용자 지표와 함께 계산되고 보고됩니다.

[!UICONTROL 미디어 보고 세부 정보]는 미디어 재생 이벤트에 대한 필수 세부 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. [!UICONTROL 미디어 보고 세부 정보] 데이터 형식을 사용하여 콘텐츠 내의 플레이헤드 위치, 고유한 세션 식별자 및 세션과 관련된 다양한 중첩 속성과 같은 세부 정보를 캡처합니다. 이 데이터 유형은 재생 세션 중에 미디어 소비 패턴 및 관련 이벤트를 추적하고 분석할 수 있는 재생 경험에 대한 포괄적인 개요를 제공합니다.

>[!NOTE]
>
>아래 필드는 요청을 만드는 데 직접 사용되지 않습니다. 대신, Adobe Experience Platform 또는 Adobe Analytics으로 전송된 필드 컬렉션은 요청 데이터에서 어셈블되고, 지표는 서버 인프라에 의해 통합되거나 처리됩니다. Experience Platform에서 다양한 유형의 사용자 이벤트를 수집하는 동안 반환된 보고서는 `media.sessionStart`, `media.adStart` 및 `media.sessionComplete`과(와) 같은 특정 이벤트에 중점을 둡니다. 즉, 수집 중에 12가지 유형의 이벤트를 전송하지만, 보고서에는 아래 나열된 5가지 이벤트를 기반으로 하는 분류만 표시됩니다.

+++[!UICONTROL 미디어 보고 세부 정보] 데이터 형식의 다이어그램을 표시하려면 선택하십시오.
![[!UICONTROL 미디어 보고 세부 정보] 데이터 형식의 다이어그램입니다.](../images/data-types/media-reporting-details.png)
+++

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL Advertising 세부 정보] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-reporting.md) | Advertising 세부 정보 는 경험 이벤트 동안 광고 활동과 관련된 특정 정보를 참조합니다. 여기에는 광고 메타데이터, 타깃팅 세부 사항 및 성능 지표가 포함됩니다. |
| [!UICONTROL Advertising Pod 세부 정보] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-reporting.md) | Advertising Pod 세부 정보에는 경험 이벤트 내의 광고 Pod에 대한 정보가 포함되어 있습니다. 광고 시퀀스, 콘텐츠 및 참여 지표에 대한 통찰력을 제공합니다. |
| [!UICONTROL 챕터 세부 정보] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-reporting.md) | 챕터 세부 정보 는 챕터 또는 컨텐츠의 세그먼트화된 부분과 관련된 데이터를 캡처합니다. 챕터 마커, 타임라인 및 관련 메타데이터에 대한 정보를 제공합니다. |
| [!UICONTROL 상태 목록] | `states` | [[!UICONTROL playerStateData]](./player-state-data-reporting.md) | 상태 속성은 경험 이벤트 전체에서 다양한 상태를 캡처하는 배열입니다. 이 속성은 재생, 사용자 작업 또는 콘텐츠 변경에 대한 순차적 데이터를 제공합니다. |
| [!UICONTROL Qoe 데이터 세부 정보] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-reporting.md) | QoE(체감 품질) 데이터 세부 정보 는 성능 관련 지표 및 사용자 경험 데이터를 캡처합니다. 품질, 응답성 및 사용자 상호 작용에 대한 통찰력을 제공합니다. |
| [!UICONTROL 세션 세부 정보] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-reporting.md) | 세션 세부 정보는 경험 이벤트와 관련된 포괄적인 정보를 포함하며, 사용자 상호 작용, 기간 및 재생 세션과 관련된 컨텍스트 데이터에 대한 통찰력을 제공합니다. |
| [!UICONTROL 사용자 지정 메타데이터] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-reporting.md) | 사용자 지정 메타데이터에는 경험 이벤트와 관련된 사용자 정의 메타데이터 또는 추가 메타데이터가 포함됩니다. 이 메타데이터를 사용하면 개인화된 데이터 또는 특정 데이터를 이벤트 컨텍스트에 포함할 수 있습니다. |
| [!UICONTROL 플레이헤드] | `playhead` | 정수 | 플레이헤드는 미디어 콘텐츠 내의 현재 재생 위치를 나타냅니다. 라이브 콘텐츠의 경우, 그 날의 현재 초(0 &lt;= 플레이헤드 &lt; 86400)를 나타냅니다. 기록된 콘텐츠의 경우, 콘텐츠 지속 시간의 현재 초(0 &lt;= 플레이헤드 &lt; 콘텐츠 길이)를 반영합니다. |

{style="table-layout:auto"}
