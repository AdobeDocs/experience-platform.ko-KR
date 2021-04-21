---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 영역;배열;field;home;popular topics;api;XDM system;experience data model;ui;workspace;array;field;
solution: Experience Platform
title: UI에서 배열 필드 정의
description: Experience Platform 사용자 인터페이스에서 배열 필드를 정의하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# UI에서 배열 필드 정의

Adobe Experience Platform 사용자 인터페이스에서 XDM(경험 데이터 모델) 필드를 정의할 때 해당 필드를 배열로 지정할 수 있습니다.

배열의 내용은 해당 필드에 대해 선택한 [!UICONTROL Type]에 따라 다릅니다. 예를 들어, 필드의 [!UICONTROL Type]이 &quot;[!UICONTROL String]&quot;로 설정된 경우 해당 필드를 배열로 설정하면 필드가 문자열 배열로 지정됩니다. 필드의 [!UICONTROL Type]이(가) &quot;[!UICONTROL Postal address]&quot;과 같은 다중 필드 데이터 유형으로 설정된 경우 데이터 유형을 준수하는 우편 주소 개체의 배열이 됩니다.

UI](./overview.md#define)에서 [새 필드를 정의했으면 오른쪽 레일의 **[!UICONTROL Array]** 확인란을 선택하여 배열 필드로 설정할 수 있습니다.

![](../../images/ui/fields/special/array.png)

확인란을 선택하면 오른쪽 레일에 추가 컨트롤이 표시되므로 배열을 추가로 제한할 수 있습니다. 특정 제한을 적용하지 않으려면 필드를 비워 두십시오.

배열에 대한 추가 구성 컨트롤은 다음과 같습니다.

| 필드 속성 | 설명 |
| --- | --- |
| [!UICONTROL Minimum length] | 인제스트를 성공적으로 수행하려면 배열에 포함해야 하는 최소 항목 수입니다. |
| [!UICONTROL Maximum length] | 인제스트를 성공적으로 수행하려면 배열에 포함해야 하는 최대 항목 수입니다. |
| [!UICONTROL Unique items only] | &quot;[!UICONTROL True]&quot;로 설정된 경우 통합 성공을 위해 배열의 각 항목이 고유해야 합니다. |

필드 구성이 완료되면 **[!UICONTROL Apply]**&#x200B;을 선택하여 스키마에 변경 사항을 적용합니다.

![](../../images/ui/fields/special/array-config.png)

캔버스는 필드의 변경 사항을 반영하도록 업데이트됩니다. 캔버스에서 필드 이름 옆에 표시되는 데이터 유형에는 해당 데이터 유형의 배열을 나타내는 대괄호(`[]`) 쌍()이 추가됩니다.

![](../../images/ui/fields/special/array-applied.png)

## 다음 단계

이 안내서에서는 UI에서 배열 필드를 정의하는 방법에 대해 설명합니다. [!DNL Schema Editor]에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [UI](./overview.md#special)의 필드 정의에 대한 개요를 참조하십시오.
