---
title: 구현 세부 사항 데이터 유형
description: 구현 세부 사항 XDM(Experience Data Model) 데이터 유형에 대해 알아봅니다.
exl-id: d3d16bae-196b-489d-8590-fd22150eedf1
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 6%

---

# [!UICONTROL 구현 세부 정보] 데이터 형식

[!UICONTROL 구현 세부 사항]은(는) API 또는 SDK와 같은 기술 구현을 설명하는 표준 XDM(Experience Data Model) 데이터 형식입니다.

![데이터 형식 구조](../images/data-types/implementation-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `environment` | 문자열 | 구현 환경. |
| `name` | 문자열 | SDK 또는 엔드포인트에 대한 식별자. 모든 SDK 또는 끝점은 확장을 포함하여 URI를 통해 식별됩니다. |
| `version` | 문자열 | API 또는 SDK의 버전입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
