---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM 스키마 및 설명자
topic: tutorial
type: Tutorial
description: 표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다. 스키마는 Experience Platform에서 데이터를 설명하는 표준 방식으로서, 스키마를 따르는 모든 데이터를 조직 간의 충돌 없이 다시 사용할 수 있으며 여러 조직 간에 공유할 수도 있습니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---


# XDM( [!DNL Experience Data Model] 스키마) 스키마 및 관계 설명자 사용

표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다. 스키마는 데이터 [!DNL Experience Platform]를 설명하는 표준 방식이므로, 스키마를 따르는 모든 데이터를 조직 간의 충돌 없이 다시 사용할 수 있으며 여러 조직 간에 공유할 수도 있습니다. XDM 스키마에 대한 자세한 내용은 [XDM 시스템 개요를 읽어 보십시오](../xdm/home.md).

## 스키마 레지스트리를 사용하여 스키마 만들기

스키마 레지스트리는 Adobe Experience Platform 스키마 라이브러리의 모든 리소스를 보고 관리할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다. 스키마 라이브러리에는 Adobe, 파트너, 응용 프로그램을 사용하는 공급업체 및 사용자가 정의 및 스키마 레지스트리에 저장하는 리소스뿐만 아니라, 사용자가 사용 가능한 리소스 [!DNL Experience Platform] 가 포함되어 있습니다. 조직의 스키마를 만드는 방법에 대해 알아보려면 스키마 레지스트리 API를 사용하여 스키마 [를](../xdm/tutorials/create-schema-api.md) 만들거나 스키마 편집기 사용자 인터페이스를 사용하여 스키마 [를 만드는 자습서를 따르십시오](../xdm/tutorials/create-schema-ui.md).

## 두 스키마 간의 관계 정의

다양한 채널에서 고객과의 관계와 브랜드와의 상호 작용을 파악할 수 있는 기능은 Adobe Experience Platform의 중요한 부분입니다. XDM(Structure Relationship) 스키마 구조 내에서 이러한 관계를 정의하면 [!DNL Experience Data Model] 고객 데이터에 대한 복잡한 통찰력을 얻을 수 있습니다. 이러한 관계 설명자는 스키마 레지스트리 API 및 스키마 편집기 UI를 사용하여 정의할 수 있습니다. 자세한 내용은 API를 [사용하거나 UI를](../xdm/tutorials/relationship-api.md) 사용하는 두 스키마 간의 관계를 정의하는 자습서를 [참조하십시오](../xdm/tutorials/relationship-ui.md).

## 임시 스키마 만들기

특정 상황에서 단일 데이터 세트에 의해서만 사용하도록 지정된 필드가 있는 [!DNL Experience Data Model] (XDM) 스키마를 만들어야 할 수 있습니다. 이를 &quot;임시&quot; 스키마라고 합니다. 애드혹 스키마는 CSV 파일 인제스트 [및 특정 종류의](../ingestion/home.md) 소스 연결 만들기를 포함하여 다양한 데이터 수집 [!DNL Experience Platform]워크플로우에서 사용됩니다 [](../sources/home.md). 임시 스키마 만들기는 스키마 레지스트리 API를 사용하여 완료되며, 작업 과정의 일부로 임시 스키마를 만들어야 하는 다른 [!DNL Experience Platform] 자습서와 함께 사용됩니다. 임시 스키마 만들기를 시작하려면 API를 사용하여 임시 스키마 [를 만드는 자습서를 참조하십시오](../xdm/tutorials/ad-hoc.md).

## 다음 단계

조직의 스키마를 정의했으면 데이터를 수집할 수 있는 데이터 세트를 만들기 시작할 수 있습니다. 시작하려면 다음 설명서를 참조하십시오.

* [데이터 집합 개요](../catalog/datasets/overview.md)
* [데이터 통합 개요](../ingestion/home.md)