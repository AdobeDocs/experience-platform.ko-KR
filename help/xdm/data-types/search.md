---
keywords: Experience Platform;홈;인기 항목;스키마;스키마;XDM;필드;스키마;검색;데이터 유형;데이터 유형;데이터 유형;;home;popular topics;schema;XDM;fields;schemas;search;datatype;data-type;data-type;
solution: Experience Platform
title: 검색 데이터 유형
topic-legacy: overview
description: 이 문서에서는 XDM(Search Experience Data Model) 데이터 유형에 대한 개요를 제공합니다.
exl-id: 9893cb67-b0c7-4f91-a0d4-96f7b87d9510
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 4%

---

# [!UICONTROL Search] 데이터 유형

[!UICONTROL Search] 는 웹 검색 활동에 대한 정보를 포함하는 표준 XDM(Experience Data Model) 데이터 유형입니다.

<img src="../images/data-types/search.PNG" width="500" /><br />

| 속성 | 데이터 유형 | 설명 |
| --- | --- | --- |
| `isPaid` | 부울 | 검색이 유료 상태인지 여부를 나타내는 데 사용됩니다. |
| `keywords` | 문자열 | 검색에 대한 키워드입니다. |
| `pageDepth` | 정수 | 검색 결과의 페이지 깊이입니다. |
| `position` | 정수 | 검색 결과 페이지에 있는 목록의 위치 또는 등급. |
| `searchEngine` | 문자열 | 검색에 사용되는 검색 엔진. |
| `searchEngineID` | 문자열 | 검색 엔진을 식별하는 데 사용되는 응용 프로그램 특정 식별자입니다. |
| `slot` | 문자열 | 검색 결과가 나타나는 페이지의 이름이 지정된 섹션. 이 속성의 값은 `top`, `side` 또는 `bottom` 같이 정의한 알려진 열거형 값 중 하나와 같아야 합니다. |

데이터 유형에 대한 자세한 내용은 공개 XDM 저장소를 참조하십시오.

* [채워진 예제](https://github.com/adobe/xdm/blob/master/components/datatypes/search.example.1.json)
* [전체 스키마](https://github.com/adobe/xdm/blob/master/components/datatypes/search.schema.json)
