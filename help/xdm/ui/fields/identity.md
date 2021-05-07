---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 영역;ID;필드;home;popular topics;api;XDM system;experience data model;ui;workspace;identity;field
solution: Experience Platform
title: UI에서 ID 필드 정의
description: Experience Platform 사용자 인터페이스에서 ID 필드를 정의하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# UI에서 ID 필드 정의

XDM(경험 데이터 모델)에서 ID 필드는 레코드 또는 시간 시리즈 이벤트와 관련된 개별 사람을 식별하는 데 사용할 수 있는 필드를 나타냅니다. 이 문서에서는 Adobe Experience Platform UI에서 ID 필드를 정의하는 방법에 대해 설명합니다.

## 전제 조건

ID 필드는 고객 ID 그래프가 플랫폼에서 구성되는 방식을 결정하는 중요한 구성 요소로서, 이는 실시간 고객 프로파일을 통해 서로 다른 데이터 조각을 병합하여 고객을 전체적으로 확인할 수 있는 방법에 영향을 줍니다. 스키마에서 ID 필드를 정의하기 전에 다음 설명서를 참조하여 ID 필드와 관련된 주요 서비스 및 개념에 대해 알아보십시오.

* [Adobe Experience Platform ID 서비스](../../../identity-service/home.md):장치 및 시스템 간에 ID를 연결하며, 이들이 준수하는 XDM 스키마로 정의된 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
   * [ID 네임스페이스](../../../identity-service/namespaces.md):ID 네임스페이스는 한 사람과 관련될 수 있고 각 ID 필드에 필요한 구성 요소인 다양한 유형의 ID 정보를 정의합니다.
* [실시간 고객 프로필](../../../profile/home.md):고객 ID 그래프를 활용하여 다양한 소스의 데이터를 집계하여 거의 실시간으로 업데이트한 통합 소비자 프로파일을 제공합니다.

## ID 필드 정의

UI에서 [새 필드](./overview.md#define)를 정의할 때 오른쪽 레일의 **[!UICONTROL Identity]** 확인란을 선택하여 이 필드를 ID 필드로 설정할 수 있습니다.

![](../../images/ui/fields/special/identity.png)

확인란을 선택하면 추가 컨트롤이 표시됩니다. 이 필드를 스키마의 기본 ID로 지정하려면 **[!UICONTROL Primary identity]** 확인란을 선택합니다.

>[!NOTE]
>
>단일 스키마에는 ID 필드가 많이 정의되어 있지만 주 ID는 하나만 가질 수 있습니다. 모든 ID 필드(기본 또는 기타 항목)는 개별 고객의 ID 그래프에 기여하지만 실시간 고객 프로필은 데이터 조각을 함께 병합할 때 기본 ID만 진실의 소스로 사용합니다. 프로필에서 사용할 스키마를 활성화하려면 스키마에 기본 ID가 정의되어 있어야 합니다.

**[!UICONTROL Identity namespace]**&#x200B;에서 드롭다운 메뉴를 사용하여 ID 필드에 적합한 네임스페이스를 선택합니다. Adobe에서 제공하는 표준 네임스페이스와 조직에서 정의한 사용자 정의 네임스페이스가 함께 나열됩니다.

완료되면 **[!UICONTROL Apply]**&#x200B;을 선택하여 스키마에 변경 내용을 적용합니다.

![](../../images/ui/fields/special/identity-config.png)

캔버스는 변경 사항을 반영하도록 업데이트되며, 선택한 필드는 지문 기호(![](../../images/ui/fields/special/identity-symbol.png))를 획득하여 ID로 지정합니다. 왼쪽 레일에서 이제 ID 필드가 스키마에 필드를 제공하는 클래스 또는 스키마 필드 그룹의 이름 아래에 나열됩니다.

모든 ID 필드는 기본적으로 필요하므로 이제 왼쪽 레일의 **[!UICONTROL Required fields]** 아래에 필드가 나열됩니다. ID 필드가 스키마 구조 내에 중첩되면 모든 상위 필드도 필요에 따라 나열됩니다.

![](../../images/ui/fields/special/identity-applied.png)

스키마에 대한 기본 ID를 정의한 경우 이제 [실시간 고객 프로필](../resources/schemas.md#profile)에서 사용할 스키마 활성화를 진행할 수 있습니다.

## 다음 단계

이 안내서에서는 UI에서 ID 필드를 정의하는 방법에 대해 설명합니다. 이 스키마를 사용하여 데이터를 수집하면 사용자 고객 ID 그래프가 스키마의 ID 필드를 반영하도록 업데이트됩니다. UI에서 조직의 개인 그래프를 탐색하는 방법을 알아보려면 [ID 그래프 뷰어](../../../identity-service/ui/identity-graph-viewer.md)의 안내서를 참조하십시오.

[!DNL Schema Editor]에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [UI](./overview.md#special)의 필드 정의에 대한 개요를 참조하십시오.
