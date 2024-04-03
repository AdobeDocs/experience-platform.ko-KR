---
title: 오류 세부 정보 수집 데이터 유형
description: 오류 세부 정보 수집 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
source-git-commit: 899c656a7295896b291ac5c80df873711bc6f149
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 8%

---

# [!UICONTROL 오류 세부 정보] 컬렉션 데이터 유형

[!UICONTROL 오류 세부 정보] 컬렉션은 오류 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 사용 [!UICONTROL 오류 세부 정보] 오류 소스 및 식별에 대한 세부 정보를 캡처하는 컬렉션 데이터 유형입니다. 오류 ID는 오류를 식별하며 오류 소스는 플레이어에서 발생하는지 외부 소스에서 발생하는지 지정합니다.

![오류 세부 정보 데이터 유형의 다이어그램입니다.](../images/data-types/error-details-collection.png)

| 표시 이름 | 속성 | 데이터 유형 | 필수 여부 | 설명 |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL 오류 ID] | `name` | 문자열 | 아니요 | 오류 ID. |
| [!UICONTROL 오류 소스] | `source` | 문자열 | 아니요 | 오류 소스. 열거됨: 각각의 의미가 있는 &quot;player&quot;, &quot;external&quot; |

{style="table-layout:auto"}
