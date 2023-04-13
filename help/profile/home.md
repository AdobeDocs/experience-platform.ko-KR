---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;통합 프로필;통합 프로필;통합;프로필;rtcp;XDM 그래프
title: 실시간 고객 프로필 개요
description: 실시간 고객 프로필은 다양한 소스의 데이터를 병합하고 개별 고객 프로필 및 관련 시계열 이벤트 형태로 해당 데이터에 대한 액세스를 제공합니다. 이 기능을 통해 마케터는 여러 채널에서 대상과 잘 조정되고 일관되며 적절한 경험을 제공할 수 있습니다.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1991'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 개요

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 사용 [!DNL Real-Time Customer Profile]를 사용하면 온라인, 오프라인, CRM 및 타사 등 여러 채널의 데이터를 결합하여 각 개별 고객을 전체적으로 확인할 수 있습니다. [!DNL Profile] 고객 데이터를 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 통합할 수 있습니다. 이 개요는 역할 및 을 이해하는 데 도움이 됩니다 [!DNL Real-Time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] Experience Platform

실시간 고객 프로필과 Experience Platform 내의 다른 서비스 간의 관계는 다음 다이어그램에서 강조 표시됩니다.

![Adobe Experience Platform의 실시간 고객 프로필과 다른 서비스 간의 관계입니다. 이 다이어그램은 프로필이 Adobe Experience Platform의 핵심 구성 요소 중 하나임을 보여줍니다.](images/profile-overview/profile-in-platform.png)

## 프로필 이해

[!DNL Real-Time Customer Profile] 여러 엔터프라이즈 시스템의 데이터를 병합한 다음 관련 시계열 이벤트가 있는 고객 프로필 형태로 해당 데이터에 대한 액세스를 제공합니다. 이 기능을 통해 마케터는 여러 채널에서 대상과 잘 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 다음 섹션에서는 플랫폼 내에서 프로필을 효과적으로 작성하고 유지 관리하기 위해 이해해야 하는 몇 가지 핵심 개념을 강조 표시합니다.

### 프로필 엔티티 구성

실시간 고객 프로필은 **기본 엔티티**&#x200B;및 다양한 지원 엔티티 Experience Platform 컨텍스트에서 기본 엔티티는 일반적으로 다음과 같습니다 **프로필 엔티티**- 개별 개인의 트레이트, 행동 및 세그먼트 멤버십으로 구성됩니다. 다른 엔티티를 사용하면 세분화 엔진이 프로필의 기본 엔티티 외부에서 데이터를 활용할 수 있으며 다음을 포함합니다.

- **차원 엔티티**: 이벤트 또는 프로필 레코드 간에 공유된 정보에 대한 데이터 모델링 프로세스를 간소화하는 데 사용되는 엔티티입니다. 이것을 조회 엔티티 또는 분류 엔티티라고도 합니다.
- **B2B 엔티티**: Business-to-Business 계정 및 기회와의 프로필의 관계를 설명하는 개체입니다.

![프로필 엔티티의 구성을 설명하는 다이어그램입니다.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>차원 및 B2B 엔티티는 기본 엔티티 외부에만 존재하므로 배치 세그먼테이션에만 사용됩니다.

차원 및 B2B 엔티티는 **스키마 관계**. 자세한 내용은 다음 설명서를 참조하십시오.

- [조회 엔터티에 대한 일대일 스키마 관계 만들기](../xdm/tutorials/relationship-ui.md)
- [B2B 엔터티에 대한 다대다 스키마 관계 만들기](../xdm/tutorials/relationship-b2b.md)

### 프로필 데이터 저장소

하지만 [!DNL Real-Time Customer Profile] 수집된 데이터 처리 및 Adobe Experience Platform 사용 [!DNL Identity Service] id 매핑을 통해 관련 데이터를 병합하려면 데이터 집합에서 자체 데이터를 유지 관리합니다 [!DNL Profile] 데이터 저장소. 다음 [!DNL Profile] 저장소는 data lake 및 [!DNL Identity Service] ID 그래프의 데이터.

프로필 저장소는 Microsoft Azure Cosmos DB 인프라를 사용하고 Platform Data Lake는 Microsoft Azure Data Lake 저장소를 사용합니다.

### 프로필 보호 기능

Experience Platform은 작성하는 것을 방지하는 일련의 보안 기능을 제공합니다 [Experience 데이터 모델(XDM) 스키마](../xdm/home.md) 실시간 고객 프로필을 지원할 수 없는 고객 여기에는 성능 저하를 초래할 수 있는 소프트 제한이 포함되며, 오류 및 시스템 중단으로 이어지는 하드 제한이 있습니다. 지침 및 예제 사용 사례 등 자세한 내용은 [프로필 보호 기능](guardrails.md) 설명서.

### 프로필 대시보드 {#profile-dashboard}

Experience Platform UI는 일별 스냅샷 중에 캡처된 실시간 고객 프로필 데이터에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. 에 액세스하고 작업하는 방법을 배우려면 [!DNL Profile] UI의 대시보드와 대시보드에 표시된 지표에 대한 자세한 정보는 [프로필 대시보드 UI 안내서](ui/profile-dashboard.md).

### 프로필 조각과 병합된 프로필 비교 {#profile-fragments-vs-merged-profiles}

각 개별 고객 프로필은 병합되어 해당 고객의 단일 보기를 구성하는 여러 프로필 조각으로 구성됩니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 해당 단일 고객과 관련된 여러 프로필 조각이 있습니다. 이러한 조각을 Platform에 수집하면 병합되어 해당 고객에 대한 단일 프로필을 만듭니다.

즉, 프로필 조각은 고유한 기본 ID와 해당 ID를 나타냅니다 [레코드](#record-data) 또는 [이벤트](#time-series-events) 지정된 데이터 세트 내에 있는 해당 ID에 대한 데이터입니다.

여러 데이터 세트의 데이터가 충돌하면(예: 한 조각은 고객을 &quot;단일&quot;로 나열하고 다른 조각은 고객을 &quot;기혼&quot;으로 나열함) [병합 정책](#merge-policies) 개인에게 대해 프로필에 우선 순위를 지정하고 포함할 정보를 결정합니다. 따라서 각 프로필은 일반적으로 여러 데이터 세트의 여러 조각으로 구성되므로 플랫폼 내 총 프로필 조각 수는 병합된 총 프로필 수보다 항상 클 수 있습니다.

### 데이터 기록 {#record-data}

프로필은 여러 속성(레코드 데이터라고도 함)으로 구성된 주체, 조직 또는 개인을 표현한 것입니다. 예를 들어 제품 프로필에 SKU 및 설명이 포함될 수 있지만, 사람의 프로필에 이름, 성 및 이메일 주소와 같은 정보가 포함되어 있습니다. 사용 [!DNL Experience Platform]을(를) 사용하면 프로필 을 사용자 지정하여 사업과 관련된 특정 데이터를 사용할 수 있습니다. 표준 [!DNL Experience Data Model] (XDM) 클래스, [!DNL XDM Individual Profile]는 고객 레코드 데이터를 설명할 때 스키마를 구축하고 Platform 서비스 간의 많은 상호 작용에 필수 데이터를 제공하는 기본 클래스입니다. 에서 스키마 작업에 대한 자세한 내용은 [!DNL Experience Platform]먼저 읽어보세요 [XDM 시스템 개요](../xdm/home.md).

### 시계열 이벤트 {#time-series-events}

시계열 데이터는 작업이 직접 또는 간접적으로 수행될 때의 시스템 스냅샷과 이벤트 자체를 설명하는 데이터를 제공합니다. 표준 스키마 클래스 XDM ExperienceEvent로 표시되는 시계열 데이터는 장바구니에 추가되는 항목, 클릭되는 링크, 열람된 비디오와 같은 이벤트를 설명할 수 있습니다. 시계열 데이터를 사용하여 세그먼테이션 규칙을 기반으로 하고, 프로필의 컨텍스트에서 개별적으로 이벤트에 액세스할 수 있습니다.

### ID

모든 기업은 고객과의 개인적인 커뮤니케이션을 위해 합니다. 그러나 관련 디지털 경험을 고객에게 전달해야 하는 과제 중 하나는 연결이 끊어진 데이터를 서로 연결하는 방법을 이해하는 것입니다. 이 데이터는 종종 태블릿, 휴대폰, 노트북과 같은 다양한 디지털 채널에 분산됩니다. [!DNL Identity Service] 여러 채널에서 ID를 연결하고 각 고객을 위한 ID 그래프를 만들어 고객의 전체 그림을 결합할 수 있습니다. 다음 방문 [ID 서비스 개요](../identity-service/home.md) 추가 정보.

### 병합 정책

여러 소스에서 데이터 조각을 함께 가져와서 각 개별 고객에 대한 전체 보기를 확인하기 위해 결합할 때 병합 정책이 [!DNL Platform] 는 데이터의 우선 순위가 지정되는 방식과 고객 프로필을 만드는 데 사용할 데이터를 판별하는 데 사용됩니다.

여러 데이터 세트에서 데이터가 충돌하는 경우 병합 정책은 데이터를 처리하는 방법과 사용해야 하는 값을 결정합니다. RESTful API 또는 사용자 인터페이스를 통해 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다.

병합 정책 및 Experience Platform 내의 역할에 대해 자세히 알아보려면 [정책 병합 개요](merge-policies/overview.md).

### 결합 스키마 {#profile-fragments-and-union-schemas}

의 주요 기능 중 하나 [!DNL Real-Time Customer Profile] 은 다중 채널 데이터를 통합하는 기능입니다. When [!DNL Real-Time Customer Profile] 는 엔티티에 액세스하는 데 사용되며 데이터 세트에서 해당 엔티티에 대한 모든 프로필 조각에 대한 병합된 보기를 &quot;결합 보기&quot;라고 하며 결합 스키마라고 하는 것을 통해 가능하게 할 수 있습니다.

UI에서 결합 스키마에 액세스하는 방법 등 결합 스키마에 대한 자세한 내용은 [결합 스키마 UI 안내서](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## 프로필 및 세그먼트

Adobe Experience Platform [!DNL Segmentation Service] 은 개별 고객을 위한 경험을 제공하는 데 필요한 대상을 만듭니다. 대상 세그먼트가 만들어지면 해당 세그먼트의 ID가 모든 자격 프로필에 대한 세그먼트 멤버십 목록에 추가됩니다. 세그먼트 규칙은 빌드되고 [!DNL Real-Time Customer Profile] RESTful API 및 Segment Builder 사용자 인터페이스를 사용한 데이터. 세그멘테이션에 대해 자세히 알아보려면 [세그먼테이션 서비스 개요](../segmentation/home.md).

### 스트리밍 수집 및 스트리밍 세그멘테이션

실시간 입력은 스트리밍 수집이라는 프로세스를 통해 가능합니다. 프로필 및 시계열 데이터를 수집할 때 [!DNL Real-Time Customer Profile] 는 기존 데이터와 병합하고 결합 보기를 업데이트하기 전에 스트리밍 세그먼테이션이라는 진행 중인 프로세스를 통해 해당 데이터를 세그먼트에서 포함하거나 제외하도록 자동으로 결정합니다. 결과적으로 고객이 브랜드와 상호 작용할 때 즉시 계산을 수행하고 개인화된 향상된 경험을 고객에게 제공할 수 있습니다. 또한 데이터를 수집하는 동안 데이터가 제대로 수집되고 데이터 세트가 기반으로 하는 스키마를 따르는지 확인하기 위해 유효성 검사를 받습니다. 수집 중 유효성 검사가 수행되는 작업에 대한 자세한 내용은 [데이터 수집 품질 개요](../ingestion/quality/overview.md).

## 에지 예측

여러 채널에서 고객을 위해 조정되고, 일관되고, 개인화된 경험을 실시간으로 유도하려면 변경 사항이 발생하면 적합한 데이터를 손쉽게 이용할 수 있고 지속적으로 업데이트해야 합니다. Adobe Experience Platform을 사용하면 가장자리라고 하는 것을 사용하여 데이터에 실시간으로 액세스할 수 있습니다. 에지(Edge)는 데이터를 저장하고 응용 프로그램에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 예를 들어, Adobe Target 및 Adobe Campaign과 같은 Adobe 애플리케이션은 에지를 사용하여 개인화된 고객 경험을 실시간으로 제공합니다. 데이터는 투영에 의해 가장자리로 라우팅되며, 투영 대상은 데이터를 전송할 에지를 정의하며, 에지에서 사용할 수 있게 될 특정 정보를 정의하는 투영 구성입니다. 자세한 내용을 알고 을 사용하여 예측 작업을 시작하려면 [!DNL Real-Time Customer Profile] API는 [edge 투영 엔드포인트 가이드](api/edge-projections.md).

## 데이터를에 수집 [!DNL Profile]

[!DNL Platform] 는 레코드 및 시계열 데이터를 로 보내도록 구성할 수 있습니다 [!DNL Profile], 실시간 스트리밍 수집 및 일괄 처리를 지원합니다. 자세한 내용은 방법에 대한 개요를 설명하는 자습서를 참조하십시오 [실시간 고객 프로필에 데이터 추가](tutorials/add-profile-data.md).

>[!NOTE]
>
>다음을 포함한 Adobe 솔루션을 통해 수집된 데이터 [!DNL Analytics Cloud], [!DNL Marketing Cloud], 및 [!DNL Advertising Cloud]: [!DNL Experience Platform] 및에 수집됩니다. [!DNL Profile].

### 프로필 수집 지표

Observability Insights를 사용하면 Adobe Experience Platform에서 주요 지표를 노출할 수 있습니다. 추가 [!DNL Experience Platform] 사용 통계 및 성능 지표 [!DNL Platform] 기능에는 들어오는 요청률, 성공적인 수집률, 수집된 레코드 크기 등에 대한 통찰력을 얻을 수 있는 특정 프로필 관련 지표가 있습니다. 자세한 내용은 [가시성 통찰력 API 개요](../observability/api/overview.md), 및 실시간 고객 프로필 지표의 전체 목록을 보려면 [사용 가능한 지표](../observability/api/metrics.md#available-metrics).

## 프로필 저장소 데이터 업데이트

간혹 조직의 프로필 저장소에서 데이터를 업데이트해야 할 수 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리를 통해 수행할 수 있으며, 후속 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 속성 업데이트를 위한 데이터 세트를 구성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [프로필 및 업데이트에 대한 데이터 세트 활성화](../catalog/datasets/enable-upsert.md).

## 데이터 거버넌스 및 [!DNL Privacy]

데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다.

데이터 액세스와 관련된 데이터 거버넌스는 [!DNL Experience Platform] 다양한 수준에서 다음을 수행합니다.

- 데이터 사용 레이블 지정
- 데이터 액세스 정책
- 마케팅 작업을 위한 데이터에 대한 액세스 제어

데이터 거버넌스는 몇 가지 지점에서 관리됩니다. 여기에는 수집할 데이터를 결정하는 작업이 포함됩니다 [!DNL Platform] 지정된 마케팅 활동에 대해 섭취 후 액세스할 수 있는 데이터입니다. 자세한 내용은 [데이터 거버넌스 개요](../data-governance/home.md).

### 옵트아웃 및 데이터 개인 정보 보호 요청 처리

[!DNL Experience Platform] 에서는 고객이 자신의 데이터 사용 및 저장과 관련된 옵트아웃 요청을 보낼 수 있도록 합니다. [!DNL Real-Time Customer Profile]. 옵트아웃 요청을 처리하는 방법에 대한 자세한 내용은 [옵트아웃 요청 준수](../segmentation/consents.md).

## 다음 단계 및 추가 리소스

Experience Platform UI 또는 프로필 API를 사용하여 실시간 고객 프로필 데이터 작업에 대한 자세한 내용은 [프로필 UI 안내서](ui/user-guide.md) 또는 [API 개발자 안내서](api/overview.md)각각 입니다.
