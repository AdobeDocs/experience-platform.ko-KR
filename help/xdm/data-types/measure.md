---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;측정값;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 측정값 데이터 유형
description: XDM(측정 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 5%

---

# [!UICONTROL 측정값] 데이터 형식

[!UICONTROL 측정값]은(는) 특정 지표의 구체적인 수량 가능한 데이터 포인트를 포함하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. 측정값은 고유 식별자와 값으로 구성됩니다.

![이미지 측정](../images/data-types/measure.PNG){width=500}

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `id` | 문자열 | 해당 측정의 고유 식별자. 조치 전송을 보장할 수 없는 오프라인 기능이 있는 모바일 앱 또는 웹 사이트와 같이 손실 통신 채널을 사용하여 데이터를 수집하는 경우, 이 속성에는 클라이언트에서 생성한 조치의 고유 ID가 포함됩니다. 무작위성이 충분하도록 충분히 길게 만드는 것이 가장 좋습니다. <br><br> 타임스탬프, 장치 ID, IP, MAC 주소 또는 기타 잠재적으로 사용자를 식별하는 값과 같은 정보가 `id` 생성에 통합되는 경우 결과를 해시해야 합니다. 이렇게 하면 사용자 또는 디바이스를 식별하는 것이 아니라 특정 측정값을 적시에 식별하는 것이 목표이므로, PII가 값에 인코딩되지 않습니다. |
| `value` | 더블 | 해당 측정의 수량 값. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
