---
title: 오류 세부 정보 데이터 유형
description: 오류 세부 정보 XDM(경험 데이터 모델) 데이터 유형에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 5%

---

# [!UICONTROL 오류 세부 정보] 데이터 유형

[!UICONTROL 오류 세부 정보] 는 오류 세부 정보를 설명하는 표준 경험 데이터 모델(XDM) 데이터 유형입니다. 사용 [!UICONTROL 오류 세부 정보] 오류 소스 및 식별에 대한 세부 정보를 캡처하는 데이터 유형입니다. 오류 ID는 오류를 식별하며 오류 소스는 플레이어에서 발생하는지 외부 소스에서 발생하는지 지정합니다.

![오류 세부 정보 데이터 유형의 다이어그램입니다.](../images/data-types/error-details-information.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|----------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL 오류 ID] | `name` | 문자열 | 오류 ID. |
| [!UICONTROL 오류 소스] | `source` | 문자열 | 오류 소스. 열거됨: 각각의 의미가 있는 &quot;player&quot;, &quot;external&quot; |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json)
