---
keywords: Experience Platform;홈;인기 항목;csv 매핑;csv 파일 매핑;csv 파일을 xdm에 매핑;csv를 xdm에 매핑;ui 안내서;맵;매핑;데이터 준비;데이터 준비;데이터 준비
solution: Experience Platform
title: 데이터 준비 개요
topic-legacy: overview
description: 이 문서에서는 Adobe Experience Platform 내의 데이터 준비를 소개합니다.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 2cc72708b77396e70d006ecd1e21fd2d495ddf61
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# 계산된 필드

계산된 필드를 사용하면 입력 스키마의 속성을 기반으로 값을 만들 수 있습니다. 그런 다음 이러한 값을 대상 스키마의 속성에 지정하고 쉽게 참조할 수 있도록 이름 및 설명을 제공할 수 있습니다.

계산된 필드를 만들려면 **[!UICONTROL 계산된 필드 추가]**&#x200B;를 선택합니다.

![](./images/calculated-fields/add-calculated-field.png)

**[!UICONTROL 계산된 필드 만들기]** 패널이 나타납니다. 왼쪽 대화 상자에는 계산된 필드에서 지원되는 필드, 함수 및 연산자가 포함되어 있습니다. 탭 중 하나를 선택하여 표현식 편집기에 함수, 필드 또는 연산자를 추가합니다.

![](./images/calculated-fields/create-calculated-field.png)

| 탭 | 설명 |
| --- | ----------- |
| 함수 | 함수 탭에는 데이터를 변형하는 데 사용할 수 있는 함수가 나열됩니다. 계산된 필드 내에서 사용할 수 있는 함수에 대한 자세한 내용은 [데이터 준비(Mapper) 함수](./functions.md)를 사용하여 안내서를 참조하십시오. |
| 필드 | 필드 탭에는 소스 스키마에서 사용할 수 있는 필드와 속성이 나열됩니다. |
| 연산자 | 연산자 탭에는 데이터를 변형하는 데 사용할 수 있는 연산자가 나열됩니다. |

가운데 표현식 편집기를 사용하여 필드, 함수 및 연산자를 수동으로 추가할 수 있습니다. 편집기를 선택하여 표현식 만들기를 시작합니다.

![](./images/calculated-fields/write-calculated-field.png)

계속하려면 **[!UICONTROL 저장]**&#x200B;을 선택하십시오.

새로 만든 소스 필드와 함께 매핑 화면이 다시 나타납니다. 적절한 대상 필드를 적용하고 **[!UICONTROL 완료]**&#x200B;를 선택하여 매핑을 완료합니다.

![](./images/calculated-fields/new-calculated-field.png)