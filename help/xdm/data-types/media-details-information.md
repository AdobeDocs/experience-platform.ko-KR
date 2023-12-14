---
title: 미디어 세부 정보 데이터 유형
description: 미디어 세부 정보 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 1%

---

# [!UICONTROL 미디어 세부 정보] 데이터 유형

[!UICONTROL 미디어 세부 정보] 는 미디어 재생 이벤트에 대한 필수 세부 정보를 캡처하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 사용 [!UICONTROL 미디어 세부 정보] 컨텐츠 내의 플레이헤드 위치, 고유한 세션 식별자 및 세션과 관련된 다양한 중첩 속성과 같은 세부 정보를 캡처할 데이터 유형. 이 데이터 유형은 재생 경험에 대한 포괄적인 개요를 제공하며, 이를 통해 재생 세션 중 미디어 소비 패턴 및 관련 이벤트를 추적하고 분석할 수 있습니다.

+++을(를) 선택하여 다이어그램의 [!UICONTROL 미디어 세부 정보] 데이터 유형.
![의 다이어그램 [!UICONTROL 미디어 세부 정보] 데이터 유형.](../images/data-types/media-details-information.png)
+++

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
| --------------------- | --------------- | --------- | ----------- |
| [!UICONTROL 플레이헤드] | `playhead` | 정수 | 플레이헤드는 미디어 콘텐츠 내의 현재 재생 위치를 나타냅니다. 라이브 콘텐츠의 경우, 그 날의 현재 초(0 &lt;= 플레이헤드 &lt; 86400)를 나타냅니다. 기록된 콘텐츠의 경우, 콘텐츠 지속 시간의 현재 초(0 &lt;= 플레이헤드 &lt; 콘텐츠 길이)를 반영합니다. |
| [!UICONTROL 미디어 세션 ID] | `sessionID` | 문자열 | 미디어 세션 ID는 개별 재생 세션 중에 컨텐츠 스트림의 인스턴스를 고유하게 식별합니다. 사용자 또는 뷰어와 관련된 특정 재생 경험을 추적하고 관리하는 식별자로 사용됩니다. |
| [!UICONTROL 세션 세부 정보] | `sessionDetails` | [[!UICONTROL sessionDetails]](./session-details-information.md) | 세션 세부 정보는 경험 이벤트와 관련된 포괄적인 정보를 포함하며, 사용자 상호 작용, 기간 및 재생 세션과 관련된 컨텍스트 데이터에 대한 통찰력을 제공합니다. |
| [!UICONTROL 광고 세부 정보] | `advertisingDetails` | [[!UICONTROL advertisingDetails]](./advertising-details-information.md) | 광고 세부정보 는 경험 이벤트 동안 광고 활동과 관련된 특정 정보를 의미합니다. 여기에는 광고 메타데이터, 타깃팅 세부 사항 및 성능 지표가 포함됩니다. |
| [!UICONTROL Advertising Pod 세부 정보] | `advertisingPodDetails` | [[!UICONTROL advertisingPodDetails]](./advertising-pod-details-information.md) | 광고 Pod 세부 정보에는 경험 이벤트 내의 광고 Pod에 대한 정보가 포함되어 있습니다. 광고 시퀀스, 콘텐츠 및 참여 지표에 대한 통찰력을 제공합니다. |
| [!UICONTROL 챕터 세부 정보] | `chapterDetails` | [[!UICONTROL chapterDetails]](./chapter-details-information.md) | 챕터 세부 정보 는 챕터 또는 컨텐츠의 세그먼트화된 부분과 관련된 데이터를 캡처합니다. 챕터 마커, 타임라인 및 관련 메타데이터에 대한 정보를 제공합니다. |
| [!UICONTROL 오류 세부 정보] | `errorDetails` | [[!UICONTROL errorDetails]](./error-details-information.md) | 오류 세부 정보에는 경험 이벤트 동안 발생한 오류와 관련된 정보가 포함되어 있습니다. 여기에는 오류 코드, 설명, 타임스탬프 및 관련 컨텍스트 데이터가 포함됩니다. |
| [!UICONTROL Qoe 데이터 세부 정보] | `qoeDataDetails` | [[!UICONTROL qoeDataDetails]](./qoe-data-details-information.md) | QoE(체감 품질) 데이터 세부 정보 는 성능 관련 지표 및 사용자 경험 데이터를 캡처합니다. 품질, 응답성 및 사용자 상호 작용에 대한 통찰력을 제공합니다. |
| [!UICONTROL 상태 시작 목록] | `statesStart` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 상태 시작 은 경험 이벤트의 시작 시 상태를 나열하는 배열을 제공합니다. 재생, 사용자 작업 또는 콘텐츠 세부 사항과 관련된 데이터를 제공합니다. |
| [!UICONTROL 상태 목록 끝] | `statesEnd` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 상태 끝은 경험 이벤트가 끝날 때 상태를 나열하는 배열을 제공합니다. 여기에는 최종 재생 상태 또는 콘텐츠 상태에 대한 세부 사항이 포함됩니다. |
| [!UICONTROL 상태 목록] | `states` | [[!UICONTROL playerStateData]](./player-state-data-information.md) | 상태 속성은 경험 이벤트 전체에서 다양한 상태를 캡처하는 배열입니다. 이 속성은 재생, 사용자 작업 또는 콘텐츠 변경에 대한 순차적 데이터를 제공합니다. |
| [!UICONTROL 사용자 지정 메타데이터] | `customMetadata` | [[!UICONTROL customMetadataDetails]](./custom-metadata-details-information.md) | 사용자 지정 메타데이터에는 경험 이벤트와 관련된 사용자 정의 메타데이터 또는 추가 메타데이터가 포함됩니다. 이 메타데이터를 사용하면 개인화된 데이터 또는 특정 데이터를 이벤트 컨텍스트에 포함할 수 있습니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json)
