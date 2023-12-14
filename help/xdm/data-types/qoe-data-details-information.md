---
title: QoE(체감 품질) 데이터 세부 정보 데이터 유형
description: QoE(체감 품질) 데이터 세부 정보 데이터 유형 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# QoE(체감 품질) 데이터 세부 정보 데이터 유형

[!UICONTROL QoE 데이터 세부 정보] 는 표준 경험 데이터 모델(XDM) 데이터 유형으로, 미디어 재생 중 체감 품질(QoE)과 관련된 세부 지표를 제공합니다. 사용 [!UICONTROL QoE 데이터 세부 정보] 비트율 정보, 프레임 속도, 버퍼링 이벤트, 드롭된 프레임 등의 세부 정보를 캡처하는 데이터 유형입니다. 이 데이터 유형을 사용하면 재생 품질을 분석할 수 있으므로 스트리밍 성능, 사용자 경험 및 재생 세션 중에 발생하는 잠재적인 문제에 대한 통찰력을 얻을 수 있습니다.

+++QoE 데이터 세부 정보 데이터 유형을 표시하려면 선택합니다.
![QoE(체감 품질) 데이터 세부 정보 데이터 유형 다이어그램입니다.](../images/data-types/qoe-data-details-information.png)
+++

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------------------------------|----------------------------|-----------|--------------------------------------------------------------------------------------------------|
| [!UICONTROL 평균 비트율 버킷] | `bitrateAverageBucket` | 문자열 | 100kbps 간격으로 사전 정의된 버킷으로 분류된 평균 비트율(kbps)입니다. |
| [!UICONTROL 비트율] | `bitrate` | 정수 | 비트율 값(kbps)입니다. |
| [!UICONTROL 평균 비트율] | `bitrateAverage` | 숫자 | 평균 비트율(kbps, 정수)입니다. 비트율 값의 가중 평균으로 계산됩니다. |
| [!UICONTROL 비트율 변경의 영향을 받은 스트림] | `hasBitrateChangeImpactedStreams` | 부울 | 재생 중 스트림이 비트율 변경의 영향을 받았는지 여부를 나타냅니다. |
| [!UICONTROL 비트율 변경] | `bitrateChangeCount` | 정수 | 재생 중 비트율 변경의 총 횟수입니다. |
| [!UICONTROL 드롭된 프레임 영향을 받은 스트림] | `hasDroppedFrameImpactedStreams` | 부울 | 재생 중에 드롭된 프레임의 영향을 스트림이 받았는지 여부를 나타냅니다. |
| [!UICONTROL 드롭된 프레임] | `droppedFrames` | 정수 | 재생 도중 드롭된 총 프레임 수입니다. |
| [!UICONTROL 시작 전 드롭] | `isDroppedBeforeStart` | 부울 | 사용자가 광고에 상관없이 비디오가 시작되기 전에 비디오를 종료하는지 여부를 나타냅니다. |
| [!UICONTROL 초당 프레임] | `framesPerSecond` | 정수 | 현재 스트림 프레임 속도(초당 프레임 수)입니다. |
| [!UICONTROL 시작 시간] | `timeToStart` | 정수 | 비디오 로드와 시작 사이의 기간(초)입니다. |
| [!UICONTROL 버퍼의 영향을 받는 스트림] | `hasBufferImpactedStreams` | 부울 | 재생 중 스트림이 버퍼링의 영향을 받았는지 보여 줍니다. |
| [!UICONTROL 버퍼 이벤트] | `bufferCount` | 정수 | 재생 중 서로 다른 버퍼 상태의 수입니다. |
| [!UICONTROL 총 버퍼 지속 시간] | `bufferTime` | 정수 | 재생 중 버퍼링에 소요된 총 시간(초). |
| [!UICONTROL 오류 영향을 받은 스트림] | `hasErrorImpactedStreams` | 부울 | 재생 도중 스트림에 오류가 발생했는지 여부를 나타냅니다. |
| [!UICONTROL 오류] | `errorCount` | 정수 | 재생 도중 발생한 총 오류 수입니다. |
| [!UICONTROL 지연 영향을 받는 스트림] | `hasStallImpactedStreams` | 부울 | 재생 도중 스트림이 중단되었는지 여부를 나타냅니다. |
| [!UICONTROL 지연 이벤트] | `stallCount` | 정수 | 재생 중 지연 이벤트 수입니다. |
| [!UICONTROL 총 지연 기간] | `stallTime` | 정수 | 재생 도중 재생이 정지된 총 시간(초)입니다. |
| [!UICONTROL 플레이어 SDK 오류 ID] | `playerSdkErrors` | 문자열 배열 | 재생 중에 플레이어 SDK에서 생성한 고유 오류 ID입니다. |
| [!UICONTROL 외부 오류 ID] | `externalErrors` | 문자열 배열 | 외부 소스의 고유 오류 ID(예: CDN 오류). |
| [!UICONTROL Media SDK 오류 ID] | `mediaSdkErrors` | 문자열 배열 | 재생 중에 Media SDK에서 생성한 고유 오류 ID입니다. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json).

