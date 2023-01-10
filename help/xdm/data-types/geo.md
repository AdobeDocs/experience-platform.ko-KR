---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 데이터 유형
description: 이 문서에서는 지역 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 5%

---

# [!UICONTROL 지역] 데이터 유형

[!UICONTROL 지역] 는 이벤트가 관찰되는 지역을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/geo.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 지역 좌표]](./geo-coordinates.md) | 위치의 지리적 좌표를 설명합니다. |
| `_id` | 문자열 | 좌표용의 고유한 시스템 생성 ID. |
| `city` | 문자열 | 도시의 이름입니다. |
| `countryCode` | 문자열 | 두 문자 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 국가 코드입니다. |
| `dmaID` | 정수 | Nielsen 미디어 연구는 시장지역을 지정했습니다. |
| `msaID` | 정수 | 관찰이 발생한 미국의 대도시 통계지역. |
| `postalCode` | 문자열 | 위치의 우편 번호입니다. 모든 국가에서는 우편 번호를 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만을 포함합니다. |
| `stateProvince` | 문자열 | 관찰의 주 또는 도 부분입니다. 형식은 다음과 같습니다 [ISO 3166-2(국가 및 세분)](https://www.unece.org/cefact/locode/subdivisions.html) 표준. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
