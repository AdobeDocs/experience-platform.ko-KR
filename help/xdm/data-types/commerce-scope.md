---
title: 상거래 범위 데이터 유형
description: Commerce Scope XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 6%

---

# [!UICONTROL 상거래 범위] 데이터 유형

[!UICONTROL 상거래 범위] 는 상거래 에코시스템 내에서 이벤트가 발생한 위치에 대한 식별자를 정의하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 환경, 웹 사이트, 스토어 및 스토어 조회수를 구분합니다.

![상거래 범위 데이터 유형 다이어그램입니다.](../images/data-types/commerce-scope.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 환경 ID] | `environmentID` | 문자열 | 환경 ID. 32자리 영숫자 ID입니다. |
| [!UICONTROL 웹 사이트 코드] | `websiteCode` | 문자열 | 환경 내의 고유한 웹 사이트 코드. |
| [!UICONTROL 코드 저장] | `storeCode` | 문자열 | 웹 사이트 내의 고유한 스토어 코드. |
| [!UICONTROL 보기 코드 저장] | `storeViewCode` | 문자열 | 저장소 내의 고유한 저장소 보기 코드입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
