---
title: QoE(체감 품질) 데이터 세부 정보 수집 데이터 유형
description: QoE(체감 품질) 데이터 세부 정보 데이터 수집 유형 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: e1c94635b691c68de6154d19e974bfdf2e250923
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# QoE(체감 품질) 데이터 세부 정보 수집 데이터 유형

[!UICONTROL QoE 데이터 세부 정보] 컬렉션은 표준 경험 데이터 모델(XDM) 데이터 유형으로, 미디어 재생 중 체감 품질(QoE)과 관련된 세부 지표를 제공합니다. 사용 [!UICONTROL QoE 데이터 세부 정보] 비트율 정보, 프레임 속도, 버퍼링 이벤트, 드롭된 프레임 등의 세부 정보를 캡처하는 컬렉션 데이터 유형입니다. 미디어 수집 필드는 데이터를 캡처하여 추가 처리를 위해 다른 Adobe 서비스로 보냅니다. 이 데이터 유형을 사용하면 재생 품질을 분석할 수 있으므로 스트리밍 성능, 사용자 경험 및 재생 세션 중에 발생하는 잠재적인 문제에 대한 통찰력을 얻을 수 있습니다.

+++QoE 데이터 세부 사항 데이터 유형을 표시하려면 선택합니다.
![QoE(체감 품질) 데이터 세부 정보 수집 데이터 유형 다이어그램입니다.](../images/data-types/qoe-data-details-collection.png)
+++

>[!NOTE]
>
>각 디스플레이 이름에는 해당 오디오 및 비디오 매개 변수에 대한 추가 정보를 볼 수 있는 링크가 포함되어 있습니다. 연결된 페이지에는 Adobe, 구현 값, 네트워크 매개 변수, 보고 및 중요 고려 사항으로 수집된 비디오 및 데이터에 대한 세부 사항이 포함되어 있습니다.

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------|-----------|-----------|---------------------------------------------------------------------------------------|
| [[!UICONTROL 비트율]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#average-bitrate) | `bitrate` | 정수 | 아니요 | 비트율 값(kbps)입니다. |
| [[!UICONTROL 드롭된 프레임]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#dropped-frames) | `droppedFrames` | 정수 | 아니요 | 재생 도중 드롭된 총 프레임 수입니다. |
| [[!UICONTROL 초당 프레임]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#frames-per-second) | `framesPerSecond` | 정수 | 아니요 | 현재 스트림 프레임 속도(초당 프레임 수)입니다. |
| [[!UICONTROL 시작 시간]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/quality-parameters.html#time-to-start-1) | `timeToStart` | 정수 | 아니요 | 비디오 로드와 시작 사이의 기간(초)입니다. |

{style="table-layout:auto"}
