---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;geo;datatype;data-type;data type;
solution: Experience Platform
title: 지역 데이터 유형
topic: overview
description: 이 문서에서는 지리 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---


# [!UICONTROL 지역] 데이터 유형

[!UICONTROL 지리적] 유형은 이벤트가 관측된 지리적 영역을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/geo.png" width="400" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 지역 좌표]](./geo-coordinates.md) | 장소의 지리적 좌표를 설명합니다. |
| `_id` | 문자열 | 좌표에 대한 고유한 시스템 생성 ID. |
| `city` | 문자열 | 도시 이름 |
| `countryCode` | 문자열 | 해당 국가의 두 문자 <a href="https://datahub.io/core/country-list">ISO 3166-1 알파-2</a> 코드입니다. |
| `dmaID` | 정수 | Nielsen 미디어 조사는 시장 지역을 지정했습니다. |
| `msaID` | 정수 | 이 관찰이 일어난 미국의 도시 통계 지역. |
| `postalCode` | 문자열 | 위치의 우편 번호. 일부 국가에서는 우편 번호를 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만을 포함합니다. |
| `stateProvince` | 문자열 | 관찰 시 또는 도 부분. 형식은 [ISO 3166-2(국가 및 하위](http://www.unece.org/cefact/locode/subdivisions.html) ) 표준을 따릅니다. |

혼합에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)