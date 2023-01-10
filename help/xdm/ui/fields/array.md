---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;배열;필드;
solution: Experience Platform
title: UI에서 배열 필드 정의
description: Experience Platform 사용자 인터페이스에서 배열 필드를 정의하는 방법을 알아봅니다.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# UI에서 배열 필드 정의

Adobe Experience Platform 사용자 인터페이스에서 XDM(Experience Data Model) 필드를 정의할 때 해당 필드를 배열로 지정할 수 있습니다.

배열의 내용은 [!UICONTROL 유형] 해당 필드에 대해 선택되었습니다. 예를 들어, [!UICONTROL 유형] 가 &quot;(으)로 설정되어 있습니다.[!UICONTROL 문자열]&quot; 필드를 배열로 설정하면 해당 필드가 문자열의 배열로 지정됩니다. 필드가 [!UICONTROL 유형] 이 &quot;&quot;과 같은 다중 필드 데이터 유형으로 설정되어 있습니다.[!UICONTROL 우편 주소]&quot;을 입력하면 데이터 유형을 준수하는 우편 주소 개체의 배열이 됩니다.

그러고 나면 [ui에서 새 필드 정의](./overview.md#define)를 채울 때는 배열 필드를 선택하여 설정할 수 있습니다 **[!UICONTROL 어레이]** 오른쪽 레일에 있는 확인란.

![](../../images/ui/fields/special/array.png)

확인란을 선택하면 오른쪽 레일에 어레이를 추가로 제한할 수 있는 추가 컨트롤이 나타납니다. 특정 제약 조건을 적용하지 않으려면 필드를 비워 둡니다.

배열에 대한 추가 구성 컨트롤은 다음과 같습니다.

| 필드 속성 | 설명 |
| --- | --- |
| [!UICONTROL 최소 길이] | 처리가 성공적으로 수행되려면 배열에 포함해야 하는 최소 항목 수입니다. |
| [!UICONTROL 최대 길이] | 성공적으로 수집하려면 배열에 포함해야 하는 최대 항목 수입니다. |
| [!UICONTROL 고유 항목만] | 을 &quot;(으)로 설정하면[!UICONTROL True]&quot;, 수집이 성공하려면 배열의 각 항목이 고유해야 합니다. |

{style=&quot;table-layout:auto&quot;}

필드 구성을 마치면 를 선택합니다 **[!UICONTROL 적용]** 스키마에 변경 사항을 적용하려면

![](../../images/ui/fields/special/array-config.png)

캔버스가 업데이트되어 필드에 수행된 변경 사항이 반영됩니다. 캔버스에서 필드 이름 옆에 표시되는 데이터 유형에는 대괄호(`[]`). 필드를 나타내는 것은 해당 데이터 유형의 배열을 나타냅니다.

![](../../images/ui/fields/special/array-applied.png)

## 다음 단계

이 안내서에서는 UI에서 배열 필드를 정의하는 방법을 다룹니다. 다음 사항에 대한 개요를 참조하십시오. [ui에서 필드 정의](./overview.md#special) 에서 다른 XDM 필드 유형을 정의하는 방법을 알아봅니다. [!DNL Schema Editor].
