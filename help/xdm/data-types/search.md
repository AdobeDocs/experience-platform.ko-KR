---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;스키마;검색;데이터 유형;데이터 유형;데이터 유형;
solution: Experience Platform
title: 데이터 유형 검색
description: XDM(검색 경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 11%

---

# [!UICONTROL 검색] 데이터 형식

[!UICONTROL Search]은(는) 웹 검색 활동에 대한 정보가 포함된 표준 XDM(경험 데이터 모델) 데이터 형식입니다.

<img src="../images/data-types/search.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `isPaid` | 부울 | 검색의 유료 여부를 나타내는 데 사용됩니다. |
| `keywords` | 문자열 | 검색용 키워드입니다. |
| `pageDepth` | 정수 | 검색 결과의 페이지 깊이입니다. |
| `position` | 정수 | 검색 결과 페이지 목록의 위치 또는 등급. |
| `searchEngine` | 문자열 | 검색에서 사용되는 검색 엔진. |
| `searchEngineID` | 문자열 | 검색 엔진 식별에 사용되는 애플리케이션별 식별자. |
| `slot` | 문자열 | 검색 결과가 표시되는 페이지의 명명된 섹션입니다. 이 속성의 값은 `top`, `side` 또는 `bottom`과 같이 사용자가 정의하는 알려진 열거형 값 중 하나와 같아야 합니다. |

{style="table-layout:auto"}

데이터 유형에 대한 자세한 내용은 공용 XDM 저장소를 참조하십시오.

* [채워진 예](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
