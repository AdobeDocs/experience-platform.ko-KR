---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;enum;field;
solution: Experience Platform
title: UI에서 열거형 필드 정의
description: Experience Platform 사용자 인터페이스에서 열거형 필드를 정의하는 방법을 알아봅니다.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# UI에서 열거형 필드 정의

XDM(경험 데이터 모델)에서 열거형 필드는 허용 가능한 값의 사전 정의된 목록으로 제한되는 필드를 나타냅니다.

Adobe Experience Platform 사용자 인터페이스에서 [새 필드](./overview.md#define)를 정의할 때 오른쪽 레일에서 **[!UICONTROL 열거형]** 확인란을 선택하여 이 필드를 열거형 필드로 설정할 수 있습니다.

![](../../images/ui/fields/special/enum.png)

확인란을 선택하면 열거형에 대한 값 제약 조건을 지정할 수 있는 추가 컨트롤이 표시됩니다. **[!UICONTROL 값]** 열에서 필드를 제한할 정확한 값을 제공해야 합니다. 이 값은 열거형 필드에 대해 선택한 [!UICONTROL Type]을 준수해야 합니다. 제약 조건에 대해 친숙한 **[!UICONTROL Label]**&#x200B;도 선택적으로 제공할 수 있습니다.

열거형에 추가 제약 조건을 추가하려면 **[!UICONTROL 행 추가]**&#x200B;를 선택합니다.

![](../../images/ui/fields/special/enum-add-row.png)

원하는 제약 조건과 선택적 레이블을 열거형에 계속 추가합니다. 완료되면 **[!UICONTROL 적용]**&#x200B;을 선택하여 스키마에 변경 사항을 적용합니다.

![](../../images/ui/fields/special/enum-configured.png)

캔버스가 업데이트되어 변경 사항이 반영됩니다. 나중에 이 스키마를 탐색할 때 오른쪽 레일 내의 열거형 필드에 대한 제약 조건을 보고 편집할 수 있습니다.

![](../../images/ui/fields/special/enum-applied.png)

## 다음 단계

이 안내서에서는 UI에서 열거형 필드를 정의하는 방법에 대해 설명합니다. [!DNL Schema Editor]에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [UI](./overview.md#special)의 필드 정의에 대한 개요를 참조하십시오.