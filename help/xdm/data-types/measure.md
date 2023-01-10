---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;측정;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 측정값 데이터 유형
description: 이 문서에서는 XDM(측정 경험 데이터 모델) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# [!UICONTROL 측정] 데이터 유형

[!UICONTROL 측정] 는 특정 지표의 구체적인 수량화 가능한 데이터 포인트를 포함하는 표준 XDM(Experience Data Model) 데이터 유형입니다. 측정은 고유 식별자와 값으로 구성됩니다.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `id` | 문자열 | 이 측정의 고유 식별자입니다. 모바일 앱이나 오프라인 기능을 가진 웹 사이트 등과 같은 무선 통신 채널을 사용하는 데이터 수집에서 조치의 전송을 보장할 수 없는 경우, 이 속성은 클라이언트가 생성한 측정 단위의 고유 ID를 포함합니다. 이렇게 충분히 길게 설정하여 무작위성을 보장하는 것이 가장 좋습니다. <br><br> 타임스탬프, 장치 ID, IP, MAC 주소 또는 기타 잠재적 사용자 식별 값이 `id`를 채울 경우 결과를 해시해야 합니다. 이렇게 하면 목표가 사용자 또는 장치를 식별하는 것이 아니라 시간에 따른 특정 측정값을 식별하기 때문에 PII가 값에 인코딩되지 않습니다. |
| `value` | 이중 | 이 측정값의 수량화 가능한 값입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
