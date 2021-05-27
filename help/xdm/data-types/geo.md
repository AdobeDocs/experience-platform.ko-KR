---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 데이터 유형
topic-legacy: overview
description: 이 문서에서는 지역 XDM 데이터 유형에 대한 개요를 제공합니다.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 4%

---

#  지리 데이터 유형

 Geois는 이벤트가 관찰되는 지역을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/geo.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 지역 좌표]](./geo-coordinates.md) | 위치의 지리적 좌표를 설명합니다. |
| `_id` | 문자열 | 좌표용의 고유한 시스템 생성 ID. |
| `city` | 문자열 | 도시의 이름입니다. |
| `countryCode` | 문자열 | 해당 국가의 두 문자 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 코드입니다. |
| `dmaID` | 정수 | Nielsen 미디어 연구는 시장지역을 지정했습니다. |
| `msaID` | 정수 | 관찰이 발생한 미국의 대도시 통계지역. |
| `postalCode` | 문자열 | 위치의 우편 번호입니다. 모든 국가에서는 우편 번호를 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만을 포함합니다. |
| `stateProvince` | 문자열 | 관찰의 주 또는 도 부분입니다. 형식은 [ISO 3166-2(국가 및 하위 분)](http://www.unece.org/cefact/locode/subdivisions.html) 표준을 따릅니다. |

{style=&quot;table-layout:auto&quot;}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)
