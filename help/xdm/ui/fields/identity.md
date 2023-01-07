---
keywords: Experience Platform;홈;인기 항목;api;XDM;XDM 시스템;경험 데이터 모델;ui;작업 공간;id;필드;
solution: Experience Platform
title: UI에서 ID 필드 정의
description: Experience Platform 사용자 인터페이스에서 ID 필드를 정의하는 방법을 알아봅니다.
topic-legacy: user guide
exl-id: 11a53345-4c3f-4537-b3eb-ee7a5952df2a
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# UI에서 ID 필드 정의

XDM(Experience Data Model)에서 ID 필드는 레코드 또는 시계열 이벤트와 관련된 개별 개인을 식별하는 데 사용할 수 있는 필드를 나타냅니다. 이 문서에서는 Adobe Experience Platform UI에서 ID 필드를 정의하는 방법을 설명합니다.

## 전제 조건

ID 필드는 고객 ID 그래프가 플랫폼에서 구성되는 방식을 결정하는데 중요한 구성 요소로서, 실시간 고객 프로필에서 서로 다른 데이터 조각을 병합하여 고객을 완전히 파악합니다. 스키마에서 ID 필드를 정의하기 전에 다음 설명서를 참조하여 ID 필드와 관련된 주요 서비스 및 개념에 대해 알아보십시오.

* [Adobe Experience Platform Identity 서비스](../../../identity-service/home.md): 장치 및 시스템 간에 ID를 브리징하여 XDM 스키마에서 정의한 ID 필드를 기반으로 데이터 세트를 함께 연결합니다.
   * [ID 네임스페이스](../../../identity-service/namespaces.md): ID 네임스페이스는 한 개인을 연결할 수 있는 다양한 유형의 ID 정보를 정의하며 각 ID 필드에 필요한 구성 요소입니다.
* [실시간 고객 프로필](../../../profile/home.md): 고객 ID 그래프를 활용하여 거의 실시간으로 업데이트되는 여러 소스에서 집계된 데이터를 기반으로 통합된 소비자 프로필을 제공합니다.

## ID 필드 정의

When [새 필드 정의](./overview.md#define) ui에서 **[!UICONTROL ID]** 오른쪽 레일에 있는 확인란.

![](../../images/ui/fields/special/identity.png)

확인란을 선택하면 추가 컨트롤이 표시됩니다. 이 필드를 스키마의 기본 ID로 지정하려면 **[!UICONTROL 기본 ID]** 확인란을 선택합니다.

>[!NOTE]
>
>단일 스키마에는 많은 ID 필드가 정의되어 있을 수 있지만, 기본 ID는 하나만 있을 수 있습니다. 모든 ID 필드(기본 또는 기타 항목)는 개별 고객에 대한 ID 그래프에 기여하지만 실시간 고객 프로필은 데이터 조각을 함께 병합할 때 기본 ID만 진리의 소스로 사용합니다. 프로필에 사용할 스키마를 활성화하려면 스키마에 기본 ID가 정의되어 있어야 합니다.

아래 **[!UICONTROL ID 네임스페이스]**&#x200B;드롭다운 메뉴를 사용하여 id 필드에 적합한 네임스페이스를 선택합니다. Adobe이 제공하는 표준 네임스페이스와 조직에서 정의한 사용자 정의 네임스페이스가 함께 나열됩니다.

완료되면 을 선택합니다 **[!UICONTROL 적용]** 스키마에 변경 사항을 적용하려면

![](../../images/ui/fields/special/identity-config.png)

캔버스는 변경 사항을 반영하도록 업데이트되며 선택한 필드는 지문 기호(![](../../images/ui/fields/special/identity-symbol.png))를 ID로 지정합니다. 왼쪽 레일에서 이제 ID 필드가 스키마에 필드를 제공하는 클래스 또는 스키마 필드 그룹의 이름 아래에 나열됩니다.

필드가 기본 ID로도 설정된 경우 다음 항목도 표시됩니다. **[!UICONTROL 필수 필드]** 왼쪽 레일에 있습니다. ID 필드가 스키마 구조 내에 중첩된 경우 모든 상위 필드도 필요에 따라 나열됩니다.

![](../../images/ui/fields/special/identity-applied.png)

스키마에 대한 기본 ID를 정의한 경우, 이제 다음을 수행할 수 있습니다 [실시간 고객 프로필에서 사용할 스키마 활성화](../resources/schemas.md#profile).

## 다음 단계

이 안내서에서는 UI에서 ID 필드를 정의하는 방법을 다룹니다. 이 스키마를 사용하여 데이터를 수집하면 고객 ID 그래프가 스키마의 ID 필드를 반영하도록 업데이트됩니다. 의 안내서를 참조하십시오. [id 그래프 뷰어](../../../identity-service/ui/identity-graph-viewer.md) ui에서 조직의 개인 그래프를 살펴보는 방법을 알아봅니다.

다음 사항에 대한 개요를 참조하십시오. [ui에서 필드 정의](./overview.md#special) 에서 다른 XDM 필드 유형을 정의하는 방법을 알아봅니다. [!DNL Schema Editor].
