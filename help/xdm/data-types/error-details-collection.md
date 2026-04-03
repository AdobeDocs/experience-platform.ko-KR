---
title: 오류 세부 정보 수집 데이터 유형
description: 오류 세부 정보 수집 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# [!UICONTROL Error Details] 컬렉션 데이터 형식

[!UICONTROL Error Details] 컬렉션은 오류 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 형식입니다. [!UICONTROL Error Details] 컬렉션 데이터 형식을 사용하여 오류 원본 및 식별에 대한 세부 정보를 캡처합니다. 오류 ID는 오류를 식별하며 오류 소스는 플레이어에서 발생하는지 외부 소스에서 발생하는지 지정합니다.

![오류 정보 데이터 형식의 다이어그램입니다.](../images/data-types/error-details-collection.png)

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | 문자열 | 아니요 | 오류 ID. |
| [!UICONTROL Error Source] | `source` | 문자열 | 아니요 | 오류 소스. 열거됨: 각각의 의미가 있는 &quot;player&quot;, &quot;external&quot; |

{style="table-layout:auto"}
