---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;주소;xdm:address;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 우편 주소 데이터 유형
description: 우편 주소 XDM 데이터 유형에 대해 알아봅니다.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 23%

---

# [!UICONTROL 우편 주소] 데이터 형식

[!UICONTROL 우편 주소]은(는) 우편 주소의 세부 정보를 설명하는 표준 XDM 데이터 형식입니다.

![](../images/data-types/postal-address.png){width=450}

| 속성 | 설명 |
| --- | --- |
| `city` | 도시 이름. |
| `country` | 정부가 관리하는 지역의 이름입니다. 모든 언어로 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| `countryCode` | 두 문자 <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> 국가용 코드입니다. |
| `createdByBatchID` | 주소 레코드를 만든 수집된 배치 파일의 ID입니다. |
| `dmaID` | 닐슨 미디어 리서치에 의해 지정된 마켓 구역. |
| `label` | 자유 형식의 주소 이름. |
| `lastVerifiedDate` | 주소가 사용자와 연계되어 마지막으로 확인된 날짜. |
| `modifiedByBatchID` | 레코드를 마지막으로 수정한 수집된 배치 파일의 ID입니다. |
| `msaID` | 관찰이 발생한 미국 대도시 통계 지역. |
| `postOfficeBox` | 주소의 사서함. |
| `postalCode` | 위치의 우편번호, 우편번호를 모든 국가에서 사용할 수 없습니다. 일부 국가에서는 우편번호의 일부만 포함됩니다. |
| `primary` | 개인의 기본 주소인지 여부를 나타내는 부울 값. 프로필에는 특정 시점에 하나의 `primary` 주소만 있을 수 있습니다. |
| `region` | 지역, 국가 또는 주소상 지역. |
| `repositoryCreatedBy` | 레코드를 만든 사용자의 ID입니다. |
| `repositoryLastModifiedBy` | 레코드를 마지막으로 수정한 사용자의 ID입니다. |
| `stateProvince` | 관찰 대상 주 또는 시/도 부분. 형식은 [ISO 3166-2(국가 및 하위 부문)](https://www.unece.org/cefact/locode/subdivisions.html) 표준을 따릅니다. |
| `status` | 주소를 현재 사용할 수 있는지 여부를 나타냅니다. |
| `statusReason` | 현재 `status`에 대한 설명입니다. |
| `street1` - `street4` | 이 네 개의 필드는 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명을 포함합니다. `street2`부터 `street4`까지는 선택 사항입니다. |

{style="table-layout:auto"}

우편 주소 데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
