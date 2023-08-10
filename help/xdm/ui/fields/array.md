---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 영역;배열;필드;
solution: Experience Platform
title: UI에서 배열 필드 정의
description: Experience Platform 사용자 인터페이스에서 배열 필드를 정의하는 방법을 알아봅니다.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 1%

---

# UI에서 배열 필드 정의

Adobe Experience Platform 사용자 인터페이스에서 XDM(Experience Data Model) 필드를 정의할 때 해당 필드를 배열로 지정할 수 있습니다.

배열의 콘텐츠는 다음에 따라 다릅니다. [!UICONTROL 유형] 이(가) 해당 필드에 대해 선택되었습니다. 예를 들어, 필드가 [!UICONTROL 유형] 이(가) &quot;[!UICONTROL 문자열]&quot;해당 필드를 배열로 설정하면 필드가 문자열 배열로 지정됩니다. 필드가 [!UICONTROL 유형] 은 와 같은 다중 필드 데이터 유형으로 설정됩니다.[!UICONTROL 우편 주소]그러면 데이터 유형을 준수하는 우편 주소 객체의 배열이 됩니다.

다음 작업을 수행한 후 [ui에서 새 필드를 정의했습니다.](./overview.md#define)를 선택하고, **[!UICONTROL 배열]** 오른쪽 레일의 확인란

![](../../images/ui/fields/special/array.png)

확인란을 선택하면 오른쪽 레일에 추가로 제어 기능이 표시되어 선택적으로 배열을 더 제한할 수 있습니다. 특정 제한을 적용하지 않으려면 필드를 비워 둡니다.

배열에 대한 추가 구성 컨트롤은 다음과 같습니다.

| 필드 속성 | 설명 |
| --- | --- |
| [!UICONTROL 최소 길이] | 수집이 성공하기 위해 배열에 포함되어야 하는 최소 항목 수입니다. |
| [!UICONTROL 최대 길이] | 수집이 성공하기 위해 배열에 포함되어야 하는 최대 항목 수입니다. |
| [!UICONTROL 고유 항목만] | 로 설정된 경우[!UICONTROL True]&quot;수집이 성공하려면 배열의 각 항목이 고유해야 합니다. |

{style="table-layout:auto"}

필드 구성을 마치면 을 선택합니다. **[!UICONTROL 적용]** 변경 사항을 스키마에 적용합니다.

![](../../images/ui/fields/special/array-config.png)

캔버스는 필드의 변경 사항을 반영하도록 업데이트됩니다. 캔버스에서 필드 이름 옆에 표시되는 데이터 유형은 대괄호( )로 추가됩니다.`[]`)는 필드가 해당 데이터 유형의 배열을 나타냅니다.

![](../../images/ui/fields/special/array-applied.png)

## 다음 단계

이 안내서에서는 UI에서 배열 필드를 정의하는 방법을 다룹니다. 의 개요 보기 [UI의 필드 정의](./overview.md#special) 에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [!DNL Schema Editor].
