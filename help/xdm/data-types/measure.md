---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;측정;데이터 유형;데이터 유형;데이터 유형;a;
solution: Experience Platform
title: 측정 데이터 유형
topic-legacy: overview
description: 이 문서에서는 XDM(Measure Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 1%

---

# [!UICONTROL Measure] 데이터 유형

[!UICONTROL Measure] 은 특정 지표의 구체적인 수량화 가능한 데이터 포인트를 포함하는 표준 XDM(Experience Data Model) 데이터 유형입니다. 측정값은 고유 식별자와 값으로 구성됩니다.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `id` | 문자열 | 이 측정값의 고유 식별자입니다. 방안의 전송을 보장할 수 없는 오프라인 기능이 있는 모바일 앱 또는 웹 사이트와 같은 손실 통신 채널을 사용하는 데이터 수집의 경우, 이 속성에는 수행되는 측정의 클라이언트 생성 고유 ID가 포함됩니다. 이것을 충분히 길게 만들어 충분히 무작위 주의를 하는 것이 가장 좋은 방법입니다. <br><br> 타임스탬프, 장치 ID, IP, MAC 주소 또는 기타 잠재적으로 사용자 식별 값을 생성하는 동안 이러한 정보가 통합되면 결과가  `id`해시 처리됩니다. 따라서 PII가 값으로 인코딩되지 않도록 할 수 있습니다. 목표는 사용자 또는 장치를 식별하지 않고 특정 측정값을 적시에 식별하기 위한 것입니다. |
| `value` | 이중 | 이 측정값의 수량화 가능한 값입니다. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
