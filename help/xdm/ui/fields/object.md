---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;개체;필드;
solution: Experience Platform
title: UI에서 개체 필드 정의
description: Experience Platform 사용자 인터페이스에서 개체 유형 필드를 정의하는 방법을 알아봅니다.
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# UI에서 개체 필드 정의

Adobe Experience Platform을 사용하면 사용자 지정 XDM(Experience Data Model) 클래스, 스키마 필드 그룹 및 데이터 유형의 구조를 완전히 사용자 지정할 수 있습니다. 사용자 지정 XDM 리소스에서 관련 필드를 구성하고 중첩하기 위해 추가 하위 필드를 포함할 수 있는 개체 유형 필드를 정의할 수 있습니다.

When [새 필드 정의](./overview.md#define) Adobe Experience Platform 사용자 인터페이스에서 **[!UICONTROL 유형]** 드롭다운 및 &quot; 선택[!UICONTROL 개체]&quot;&quot;을 클릭합니다.

![](../../images/ui/fields/special/object.png)

선택 **[!UICONTROL 적용]** 를 눌러 스키마에 객체를 추가합니다. 캔버스가 업데이트되어 [!UICONTROL 개체] 적용된 데이터 형식(개체에 하위 필드를 편집하고 추가하는 컨트롤 포함)

![](../../images/ui/fields/special/object-applied.png)

하위 필드를 추가하려면 **더하기(+)** 캔버스에서 개체 필드 옆에 있는 아이콘을 클릭합니다. 개체 아래에 새 필드가 나타나고 오른쪽 레일에서 하위 필드를 구성하는 컨트롤이 있습니다.

![](../../images/ui/fields/special/object-add-field.png)

하위 필드를 구성하고 선택했으면 **[!UICONTROL 적용]**&#x200B;동일한 프로세스를 사용하여 객체에 필드를 계속 추가할 수 있습니다. 또한 객체 자체인 하위 필드를 추가하여 원하는 만큼 필드를 중첩할 수 있습니다.

객체 구성을 완료하면 해당 구조를 다른 클래스 및 필드 그룹에서 재사용할 수 있습니다. 이 경우 개체를 데이터 형식으로 변환하도록 선택할 수 있습니다. 의 섹션을 참조하십시오. [개체를 데이터 형식으로 변환](../resources/data-types.md#convert) 자세한 내용은 데이터 유형 UI 안내서를 참조하십시오.

## 다음 단계

이 안내서에서는 UI에서 개체 필드를 정의하는 방법을 다룹니다. 다음 사항에 대한 개요를 참조하십시오. [ui에서 필드 정의](./overview.md#special) 에서 다른 XDM 필드 유형을 정의하는 방법을 알아봅니다. [!DNL Schema Editor].
