---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;지역;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 지역 데이터 유형
description: 지역 XDM 데이터 유형에 대해 알아봅니다.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 34%

---

# [!UICONTROL 지역] 데이터 형식

[!UICONTROL 지역]은 이벤트가 관찰된 지역을 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/geo.png){width=400}

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `_schema` | [[!UICONTROL 지리적 좌표]](./geo-coordinates.md) | 장소의 지리적 좌표를 설명합니다. |
| `_id` | 문자열 | 좌표에 대한 시스템 생성 고유 ID. |
| `city` | 문자열 | 도시 이름. |
| `countryCode` | 문자열 | 두 문자 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 국가용 코드입니다. |
| `dmaID` | 정수 | 닐슨 미디어 리서치에 의해 지정된 마켓 구역. |
| `msaID` | 정수 | 관찰이 발생한 미국 대도시 통계 지역. |
| `postalCode` | 문자열 | 위치의 우편번호, 우편번호를 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편번호의 일부만 포함됩니다. |
| `stateProvince` | 문자열 | 관찰 대상 주 또는 시/도 부분. 형식은 [ISO 3166-2(국가 및 하위 부문)](https://www.unece.org/cefact/locode/subdivisions.html) 표준을 따릅니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
