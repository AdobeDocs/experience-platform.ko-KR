---
keywords: Experience Platform;홈;인기 항목;api;API;XDM;XDM 시스템;경험 데이터 모델;데이터 모델;ui;작업 공간;ID;필드;
solution: Experience Platform
title: UI에서 ID 필드 정의
description: Experience Platform 사용자 인터페이스에서 ID 필드를 정의하는 방법을 알아봅니다.
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: 6020f1c294f123cbf57629405128580efc5642ec
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 6%

---

# UI에서 ID 필드 정의

XDM(Experience Data Model)에서 ID 필드는 레코드 또는 시계열 이벤트와 관련된 개인을 식별하는 데 사용할 수 있는 필드를 나타냅니다. 이 문서에서는 Adobe Experience Platform UI에서 ID 필드를 정의하는 방법을 다룹니다.

## 전제 조건

ID 필드는 플랫폼에서 고객 ID 그래프를 구성하는 방법에 대한 중요한 구성 요소이며, 이는 궁극적으로 실시간 고객 프로필이 서로 다른 데이터 조각을 병합하여 고객에 대한 완전한 보기를 얻는 방법에 영향을 줍니다. 스키마에서 ID 필드를 정의하기 전에 다음 설명서를 참조하여 ID 필드와 관련된 주요 서비스 및 개념에 대해 알아보십시오.

* [Adobe Experience Platform ID 서비스](../../../identity-service/home.md): 장치와 시스템 간에 ID를 브리징하여 준수하는 XDM 스키마에 의해 정의된 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
   * [ID 네임스페이스](../../../identity-service/features/namespaces.md): ID 네임스페이스는 한 사람과 관련된 다양한 유형의 ID 정보를 정의하며 각 ID 필드에 필요한 구성 요소입니다.
* [실시간 고객 프로필](../../../profile/home.md): 고객 ID 그래프를 활용하여 실시간으로 업데이트되는 여러 소스의 집계 데이터를 기반으로 통합 소비자 프로필을 제공합니다.

## ID 필드 정의 {#define-a-identity-field}

>[!CONTEXTUALHELP]
>id="platform_schemas_identityField_primaryIdentityRestriction"
>title="기본 ID에 대한 제한 사항"
>abstract="이 스키마는 특정 소스 연결에서 사용할 필드 그룹을 사용합니다. 연결에는 기본 ID로 사용되는 identityMap이 필요하며 자동으로 설정됩니다."

[UI에서 새 필드를 정의](./overview.md#define)할 때 오른쪽 레일에서 **[!UICONTROL ID]** 확인란을 선택하여 ID 필드로 설정할 수 있습니다.

![](../../images/ui/fields/special/identity.png)

확인란을 선택하면 추가 컨트롤이 나타납니다. 이 필드를 스키마의 기본 ID로 설정하려면 **[!UICONTROL 기본 ID]** 확인란을 선택하십시오.

>[!NOTE]
>
>단일 스키마에는 여러 ID 필드가 정의되어 있을 수 있지만 기본 ID는 하나만 있을 수 있습니다. 모든 ID 필드(기본 또는 기타 필드)는 개별 고객의 ID 그래프에 기여하지만, 실시간 고객 프로필은 데이터 조각을 함께 병합할 때 기본 ID만 소스로 사용합니다. 프로필에서 사용하기 위해 스키마를 활성화하려면 스키마에 기본 ID가 정의되어 있어야 합니다.

**[!UICONTROL ID 네임스페이스]**&#x200B;에서 드롭다운 메뉴를 사용하여 ID 필드에 적합한 네임스페이스를 선택합니다. 조직에서 정의한 사용자 정의 네임스페이스와 함께 Adobe에서 제공하는 표준 네임스페이스가 나열됩니다.

완료되면 **[!UICONTROL 적용]**&#x200B;을 선택하여 스키마에 변경 내용을 적용합니다.

![](../../images/ui/fields/special/identity-config.png)

캔버스는 변경 내용을 반영하도록 업데이트되며, 선택한 필드는 ID로 지정하기 위해 지문 기호(![](/help/images/icons/identity-service.png))를 받습니다. 왼쪽 레일에서 이제 ID 필드가 스키마에 필드를 제공하는 클래스 또는 스키마 필드 그룹의 이름 아래에 나열됩니다.

필드도 기본 ID로 설정된 경우 왼쪽 레일의 **[!UICONTROL 필수 필드]** 아래에 나열됩니다. 스키마 구조 내에 ID 필드가 중첩되면 모든 상위 필드도 필요에 따라 나열됩니다.

![](../../images/ui/fields/special/identity-applied.png)

스키마에 대한 기본 ID를 정의한 경우 이제 [실시간 고객 프로필에서 사용할 스키마를 활성화](../resources/schemas.md#profile)로 진행할 수 있습니다.

## 다음 단계

이 안내서에서는 UI에서 ID 필드를 정의하는 방법을 다룹니다. 이 스키마를 사용하여 데이터가 수집되면 고객 ID 그래프가 스키마의 ID 필드를 반영하도록 업데이트됩니다. UI에서 조직의 개인 그래프를 살펴보려면 [ID 그래프 뷰어](../../../identity-service/features/identity-graph-viewer.md)의 안내서를 참조하십시오.

[!DNL Schema Editor]에서 다른 XDM 필드 유형을 정의하는 방법을 알아보려면 [UI의 필드 정의](./overview.md#special)에 대한 개요를 참조하십시오.

