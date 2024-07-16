---
title: Commerce 범위 데이터 유형
description: Commerce 범위 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: c2888c3a-a49c-43c4-8d36-0a485cb76a58
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 8%

---

# [!UICONTROL Commerce 범위] 데이터 형식

[!UICONTROL Commerce 범위]는 상거래 에코시스템 내에서 이벤트가 발생한 위치에 대한 식별자를 정의하는 표준 XDM(경험 데이터 모델) 데이터 형식입니다. 환경, 웹 사이트, 스토어 및 스토어 조회수를 구분합니다.

![Commerce 범위 데이터 형식의 다이어그램입니다.](../images/data-types/commerce-scope.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|---------------------------------|-------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 환경 ID] | `environmentID` | 문자열 | 환경 ID. 32자리 영숫자 ID입니다. |
| [!UICONTROL 웹 사이트 코드] | `websiteCode` | 문자열 | 환경 내의 고유한 웹 사이트 코드. |
| [!UICONTROL 스토어 코드] | `storeCode` | 문자열 | 웹 사이트 내의 고유한 스토어 코드. |
| [!UICONTROL 보기 코드 저장] | `storeViewCode` | 문자열 | 저장소 내의 고유한 저장소 보기 코드입니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/commercescope.schema.json)
