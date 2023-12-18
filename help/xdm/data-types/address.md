---
title: 우편 주소 데이터 유형
description: 우편 주소 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 8%

---

# [!UICONTROL 우편 주소] 데이터 유형

[!UICONTROL 우편 주소] 는 주소 세부 정보를 제공하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다.

![의 다이어그램 [!UICONTROL 우편 주소] 데이터 유형.](../images/data-types/postal-address.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 기본] | `primary` | 부울 | 기본 주소 표시기. 프로필에는 하나만 있을 수 있습니다. `primary` 지정된 시점의 주소. |
| [!UICONTROL 레이블] | `label` | 문자열 | 자유 형식의 주소 이름. |
| [!UICONTROL 도로 1] | `street1` | 문자열 | 기본 도로 정보, 아파트 번호, 도로 번호 및 도로명. |
| [!UICONTROL 도로 2] | `street2` | 문자열 | 2차선 도로 정보(선택 사항). |
| [!UICONTROL 도로 3] | `street3` | 문자열 | 3차선 도로 정보(선택 사항). |
| [!UICONTROL 도로 4] | `street4` | 문자열 | 4차선 도로 정보(선택 사항). |
| [!UICONTROL 지역] | `region` | 문자열 | 주소의 지역, 국가 또는 지역 부분입니다. |
| [!UICONTROL 사서함] | `postOfficeBox` | 문자열 | 사서함 주소. |
| [!UICONTROL 국가] | `country` | 문자열 | 정부가 관리하는 지역의 이름입니다. 제외 ``countryCode``, 모든 언어로 국가 이름을 사용할 수 있는 자유 형식의 필드입니다. |
| [!UICONTROL 주/도] | `state` | 문자열 | 주 이름입니다. 자유 형식의 필드입니다. |
| [!UICONTROL 상태] | `status` | 문자열 | 주소 사용 기능에 대한 표시. |
| [!UICONTROL 상태 사유] | `statusReason` | 문자열 | 현재 상태에 대한 설명. |
| [!UICONTROL 마지막으로 확인한 날짜] | `lastVerifiedDate` | 문자열 | 주소가 사용자와 연결된 것으로 마지막으로 확인된 날짜. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 [전체 스키마](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) 공용 XDM 저장소에서:
