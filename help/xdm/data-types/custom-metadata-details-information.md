---
title: 사용자 지정 메타데이터 세부 정보 데이터 유형
description: 사용자 지정 메타데이터 세부 정보 경험 데이터 모델(XDM) 데이터 유형에 대해 알아봅니다.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 4%

---

# [!UICONTROL 사용자 지정 메타데이터 세부 정보] 데이터 유형

[!UICONTROL 사용자 지정 메타데이터 세부 정보] 는 표준 경험 데이터 모델(XDM) 데이터 유형으로서, 사용자 지정 메타데이터를 저장하기 위한 구조를 정의합니다. 사용 [!UICONTROL 사용자 지정 메타데이터 세부 정보] 콘텐츠 또는 상호 작용과 연결된 사용자 지정 메타데이터의 이름 및 값과 같은 세부 정보를 캡처하는 데이터 유형입니다.

![사용자 지정 메타데이터 세부 정보 데이터 유형의 다이어그램입니다.](../images/data-types/custom-metadata-details-information.png)

| 표시 이름 | 속성 | 데이터 유형 | 설명 |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL 사용자 지정 메타데이터 필드 이름] | `name` | 문자열 | 사용자 정의 필드의 이름. |
| [!UICONTROL 사용자 지정 메타데이터 필드 값] | `value` | 문자열 | 사용자 정의 필드의 값. |

{style="table-layout:auto"}

필드 그룹에 대한 자세한 내용은 [공개 XDM 저장소](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
