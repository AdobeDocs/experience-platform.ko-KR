---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: XDM 스키마 및 설명자
topic-legacy: tutorial
type: Tutorial
description: 표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력의 일환입니다. 스키마는 Experience Platform에서 데이터를 설명하는 표준 방식이며, 스키마를 따르는 모든 데이터는 조직 간의 충돌 없이 다시 사용할 수 있으며 여러 조직 간에 공유할 수도 있습니다.
exl-id: 1cdc45d7-57ca-4a2d-99a4-9a8cd885a511
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# [!DNL Experience Data Model](XDM) 스키마 및 관계 설명자로 작업

표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다. 스키마는 [!DNL Experience Platform]에서 데이터를 설명하는 표준 방식이므로 스키마를 따르는 모든 데이터를 조직 간의 충돌 없이 다시 사용할 수 있으며 여러 조직 간에 공유할 수도 있습니다. XDM 스키마에 대한 자세한 내용은 [XDM 시스템 개요](../xdm/home.md)를 읽어 보십시오.

## 스키마 레지스트리를 사용하여 스키마 만들기

스키마 레지스트리는 Adobe Experience Platform 스키마 라이브러리의 모든 리소스를 보고 관리할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 스키마 라이브러리에는 Adobe, [!DNL Experience Platform] 파트너, 응용 프로그램을 사용하는 공급업체 및 사용자가 정의하고 스키마 레지스트리에 저장하는 리소스가 포함되어 있습니다. 조직의 스키마를 만드는 방법에 대해 알아보려면 스키마 레지스트리 API](../xdm/tutorials/create-schema-api.md) 또는 [스키마 편집기 사용자 인터페이스](../xdm/tutorials/create-schema-ui.md)를 사용하여 스키마 만들기에 대한 자습서를 따르십시오.[

## 두 스키마 간의 관계 정의

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 이해할 수 있는 기능은 Adobe Experience Platform에서 중요한 부분입니다. [!DNL Experience Data Model](XDM) 스키마 구조 내에서 이러한 관계를 정의하면 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다. 이러한 관계 설명자는 스키마 레지스트리 API 및 스키마 편집기 UI를 사용하여 정의할 수 있습니다. 자세한 내용은 API](../xdm/tutorials/relationship-api.md) 또는 UI](../xdm/tutorials/relationship-ui.md)를 사용하여 [두 스키마 간의 관계를 정의하는 자습서를 참조하십시오.[

## 임시 스키마 만들기

특정 상황에서는 단일 데이터 집합에서만 사용하도록 지정된 필드가 있는 [!DNL Experience Data Model](XDM) 스키마를 만들어야 할 수 있습니다. 이를 &quot;임시&quot; 스키마라고 합니다. 애드혹 스키마는 CSV 파일 인제스트 및 특정 유형의 [소스 연결](../sources/home.md)을 만드는 것을 포함하여 [!DNL Experience Platform]에 대한 다양한 데이터 통합](../ingestion/home.md) 워크플로에서 사용됩니다. [ 임시 스키마 만들기는 스키마 레지스트리 API를 사용하여 수행되며 작업 과정의 일부로 임시 스키마를 만들어야 하는 다른 [!DNL Experience Platform] 튜토리얼과 함께 사용하도록 만들어졌습니다. 임시 스키마 만들기를 시작하려면 API](../xdm/tutorials/ad-hoc.md)를 사용하여 [임시 스키마 만들기에 대한 자습서를 참조하십시오.

## 다음 단계

조직에 대한 스키마를 정의했으면 데이터를 수집할 수 있는 데이터 세트를 만들기 시작할 수 있습니다. 시작하려면 다음 설명서를 참조하십시오.

* [데이터 세트 개요](../catalog/datasets/overview.md)
* [데이터 통합 개요](../ingestion/home.md)
