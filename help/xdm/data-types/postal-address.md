---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;address;xdm:address;datatype;data-type;data type;
solution: Experience Platform
title: 우편 주소 데이터 유형
topic: overview
description: 이 문서에서는 우편 주소 XDM 데이터 유형에 대한 개요를 제공합니다.
translation-type: tm+mt
source-git-commit: 6a7967ac9e652c7e73fd713e89a9079287cf0ae5
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---


# [!UICONTROL 우편 주소] 데이터 유형

[!UICONTROL 우편 주소는] 우편 주소의 세부 사항을 설명하는 표준 XDM 데이터 유형입니다.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| 속성 | 설명 |
| --- | --- |
| `city` | 도시 이름 |
| `country` | 정부 관리 구역의 이름. 모든 언어로 국가 이름을 지정할 수 있는 자유 형식 필드입니다. |
| `countryCode` | 해당 국가의 두 문자 <a href="https://datahub.io/core/country-list">ISO 3166-1 알파-2</a> 코드입니다. |
| `createdByBatchID` | 주소 레코드를 만든 인제스트된 일괄 처리 파일의 ID입니다. |
| `dmaID` | Nielsen 미디어 조사는 시장 지역을 지정했습니다. |
| `label` | 주소의 자유 형식 이름입니다. |
| `lastVerifiedDate` | 주소가 여전히 사람과 관련된 것으로 마지막으로 확인된 날짜. |
| `modifiedByBatchID` | 레코드를 마지막으로 수정한 인제스트된 일괄 처리 파일의 ID입니다. |
| `msaID` | 이 관찰이 일어난 미국의 도시 통계 지역. |
| `postOfficeBox` | 주소의 우체국 상자입니다. |
| `postalCode` | 위치의 우편 번호. 일부 국가에서는 우편 번호를 사용할 수 없습니다. 일부 국가에서는 우편 번호의 일부만을 포함합니다. |
| `primary` | 개인의 기본 주소인지 여부를 나타내는 부울 값입니다. 프로필은 지정된 시점에 한 `primary` 개의 주소만 가질 수 있습니다. |
| `region` | 주소의 지역, 군 또는 구 부분입니다. |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID. |
| `stateProvince` | 관찰 시 또는 도 부분. 형식은 [ISO 3166-2(국가 및 하위](http://www.unece.org/cefact/locode/subdivisions.html) ) 표준을 따릅니다. |
| `status` | 주소를 현재 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 설명 `status`. |
| `street1` - `street4` | 이 네 개의 필드는 1차 거리 수준 정보, 아파트 번호, 거리 번호, 그리고 거리 이름을 포함하도록 되어 있습니다. `street2` to `street4` 는 선택 사항입니다. |

우편 주소 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)