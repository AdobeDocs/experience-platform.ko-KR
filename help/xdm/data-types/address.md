---
title: 우편 주소 데이터 유형
description: 우편 주소 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 41%

---

# [!UICONTROL 우편 주소] 데이터 형식

[!UICONTROL 우편 주소]은(는) 주소 세부 정보를 제공하는 표준 XDM(Experience Data Model) 데이터 형식입니다.

![우편 주소] 데이터 형식의 다이어그램](../images/data-types/postal-address.png)[!UICONTROL 

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 기본] | `primary` | 부울 | 기본 주소 표시기. 프로필에는 특정 시점에 하나의 `primary` 주소만 있을 수 있습니다. |
| [!UICONTROL 레이블] | `label` | 문자열 | 자유 형식의 주소 이름. |
| [!UICONTROL 거리 1] | `street1` | 문자열 | 기본 도로 정보, 아파트 번지, 우편 번호 및 도로명. |
| [!UICONTROL 거리 2] | `street2` | 문자열 | 2차선 도로 정보(선택 사항). |
| [!UICONTROL 거리 3] | `street3` | 문자열 | 3차선 도로 정보(선택 사항). |
| [!UICONTROL 거리 4] | `street4` | 문자열 | 4차선 도로 정보(선택 사항). |
| [!UICONTROL 지역] | `region` | 문자열 | 지역, 국가 또는 주소상 지역. |
| [!UICONTROL Post Office Box] | `postOfficeBox` | 문자열 | 사서함 주소 |
| [!UICONTROL 국가] | `country` | 문자열 | 정부가 관리하는 지역의 이름입니다. ``countryCode``이(가) 아닌 모든 언어의 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| [!UICONTROL 상태] | `state` | 문자열 | 상태 이름. 이는 자유 형식의 필드입니다. |
| [!UICONTROL 상태] | `status` | 문자열 | 주소 사용 기능에 관한 표시. |
| [!UICONTROL 상태 이유] | `statusReason` | 문자열 | 현재 상태에 대한 설명. |
| [!UICONTROL 마지막으로 확인한 날짜] | `lastVerifiedDate` | 문자열 | 주소가 사용자와 연결된 것으로 마지막으로 확인된 날짜. |

{style="table-layout:auto"}

데이터 형식에 대한 자세한 내용은 공용 XDM 저장소의 [전체 스키마](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json)을(를) 참조하십시오.
