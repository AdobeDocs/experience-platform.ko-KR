---
title: 구현 세부 사항 데이터 유형
description: 이 문서에서는 구현 세부 사항 XDM(Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 6%

---

# [!UICONTROL 구현 세부 사항] 데이터 유형

[!UICONTROL 구현 세부 사항] 는 API 또는 SDK와 같은 기술 구현을 설명하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

![데이터 유형 구조](../images/data-types/implementation-details.png)

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `environment` | 문자열 | 구현의 환경입니다. |
| `name` | 문자열 | SDK 또는 종단점에 대한 식별자입니다. 모든 SDK 또는 종단점은 확장을 포함하여 URI를 통해 식별됩니다. |
| `version` | 문자열 | API 또는 SDK의 버전입니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json)
