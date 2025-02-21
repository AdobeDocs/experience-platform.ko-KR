---
title: 실시간 고객 프로필 개요
description: Real-Time Customer Profile은 다양한 소스의 데이터를 병합하고 개별 고객 프로필 및 관련 시계열 이벤트의 형태로 해당 데이터에 대한 액세스를 제공합니다. 이 기능을 통해 마케터는 여러 채널에서 대상자와 일관되고, 관련성이 높은 경험을 제공할 수 있습니다.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: fc53d1b32eb3fc0251f307d5b2f076b1153a2931
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] 개요

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. [!DNL Real-Time Customer Profile]을(를) 사용하면 온라인, 오프라인, CRM 및 서드파티를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. [!DNL Profile]을(를) 사용하면 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다. 이 개요는 [!DNL Experience Platform]에서 [!DNL Real-Time Customer Profile]의 역할 및 사용을 이해하는 데 도움이 됩니다.

## Experience Platform의 [!DNL Profile]

실시간 고객 프로필과 Experience Platform 내의 다른 서비스 간의 관계는 다음 다이어그램에서 강조 표시됩니다.

![실시간 고객 프로필과 Adobe Experience Platform의 다른 서비스 간의 관계입니다. 이 다이어그램은 프로필이 Adobe Experience Platform의 핵심 구성 요소 중 하나임을 보여 줍니다.](images/profile-overview/profile-in-platform.png)

## 프로필 이해

[!DNL Real-Time Customer Profile]은(는) 다양한 엔터프라이즈 시스템의 데이터를 병합한 다음 고객 프로필 형식으로 해당 데이터에 대한 액세스를 관련 시계열 이벤트와 함께 제공합니다. 이 기능을 통해 마케터는 여러 채널에서 대상자와 일관되고, 관련성이 높은 경험을 제공할 수 있습니다. 다음 섹션에서는 Platform 내에서 프로필을 효과적으로 구축하고 유지하기 위해 이해해야 하는 몇 가지 핵심 개념을 강조합니다.

### 프로필 엔티티 구성

실시간 고객 프로필은 **기본 엔터티**&#x200B;라는 기본 엔터티와 다양한 지원 엔터티로 구성됩니다. Experience Platform에서 기본 엔터티는 일반적으로 개별 사용자의 트레이트, 동작 및 대상 멤버십으로 구성된 **프로필 엔터티**&#x200B;입니다. 다른 엔티티를 사용하면 세그먼테이션 엔진이 프로필의 기본 엔티티 외부의 데이터를 활용할 수 있으며, 여기에는 다음이 포함됩니다.

- **차원 엔터티**: 이벤트 또는 프로필 레코드 간에 공유된 정보에 대한 데이터 모델링 프로세스를 단순화하는 데 사용되는 엔터티입니다. 이를 조회 엔티티 또는 분류 엔티티라고도 합니다.
- **B2B 엔터티**: Business-to-Business 계정 및 기회와 프로필의 관계를 설명하는 엔터티입니다.

![프로필 엔터티의 구성을 설명하는 다이어그램입니다.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>차원 및 B2B 엔티티는 기본 엔티티 외부에만 존재하므로 배치 세그먼테이션에만 사용됩니다.

Dimension 및 B2B 엔터티가 **스키마 관계**&#x200B;를 통해 기본 엔터티에 연결되어 있습니다. 자세한 내용은 다음 설명서를 참조하십시오.

- [조회 엔티티에 대한 일대일 스키마 관계 생성](../xdm/tutorials/relationship-ui.md)
- [B2B 엔티티에 대한 다대일 스키마 관계 생성](../xdm/tutorials/relationship-b2b.md)

### 프로필 데이터 저장소

[!DNL Real-Time Customer Profile]이(가) 수집된 데이터를 처리하고 Adobe Experience Platform [!DNL Identity Service]을(를) 사용하여 ID 매핑을 통해 관련 데이터를 병합하지만 [!DNL Profile] 데이터 저장소에 자체 데이터를 유지합니다. [!DNL Profile] 저장소는 데이터 레이크의 카탈로그 데이터와 ID 그래프의 [!DNL Identity Service] 데이터와 별개입니다.

프로필 저장소는 Microsoft Azure Cosmos DB 인프라를 사용하고 플랫폼 데이터 레이크는 Microsoft Azure 데이터 레이크 저장소를 사용합니다.

### 프로필 보호 기능

Experience Platform에서는 실시간 고객 프로필에서 지원하지 않는 [XDM(경험 데이터 모델) 스키마](../xdm/home.md)를 만들지 않도록 하는 데 도움이 되는 일련의 보호 기능을 제공합니다. 여기에는 성능 저하를 초래할 수 있는 소프트 제한과 오류 및 시스템 손상을 초래할 수 있는 하드 제한이 포함됩니다. 지침 목록 및 사용 사례 예시 등 자세한 내용은 [프로필 보호](guardrails.md) 설명서를 참조하십시오.

### 프로필 대시보드 {#profile-dashboard}

Experience Platform UI는 일별 스냅샷 중에 캡처한 대로 실시간 고객 프로필 데이터에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. UI에서 [!DNL Profile] 대시보드에 액세스하고 작업하는 방법 및 대시보드에 표시된 지표에 대한 자세한 정보를 알아보려면 [프로필 대시보드 UI 안내서](ui/profile-dashboard.md)를 참조하세요.

### 프로필 조각과 병합된 프로필 {#profile-fragments-vs-merged-profiles}

각 개별 고객 프로필은 해당 고객에 대한 단일 보기를 형성하기 위해 병합된 여러 프로필 조각으로 구성됩니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직에는 여러 데이터 세트에 표시되는 단일 고객과 관련된 여러 프로필 조각이 있습니다. 이러한 조각을 Platform에 수집하면 해당 고객을 위한 단일 프로필을 만들기 위해 함께 병합됩니다.

즉, 프로필 조각은 고유한 기본 ID와 주어진 데이터 세트 내의 해당 ID에 대한 해당 [레코드](#record-data) 또는 [이벤트](#time-series-events) 데이터를 나타냅니다.

여러 데이터 세트의 데이터가 충돌하면(예: 한 조각은 고객을 &quot;단일&quot;로 나열하고 다른 조각은 고객을 &quot;기혼&quot;으로 나열함) [병합 정책](#merge-policies)은 우선 순위를 지정하고 개인에 대한 프로필에 포함할 정보를 결정합니다. 따라서 각 프로필은 일반적으로 여러 데이터 세트의 여러 조각으로 구성되므로 플랫폼 내의 총 프로필 조각 수는 병합된 프로필의 총 수보다 항상 높을 수 있습니다.

### 레코드 데이터 {#record-data}

프로필은 많은 속성(레코드 데이터라고도 함)으로 구성된 주제, 조직 또는 개인의 표현입니다. 예를 들어, 제품 프로필에는 SKU 및 설명이 포함될 수 있지만, 개인 프로필에는 이름, 성 및 이메일 주소와 같은 정보가 포함됩니다. [!DNL Experience Platform]을(를) 사용하여 비즈니스와 관련된 특정 데이터를 사용하도록 프로필을 사용자 지정할 수 있습니다. 표준 [!DNL Experience Data Model]&#x200B;(XDM) 클래스 [!DNL XDM Individual Profile]은(는) 고객 레코드 데이터를 설명할 때 스키마를 구축하는 기본 클래스이며, 플랫폼 서비스 간의 여러 상호 작용에 필수적인 데이터를 제공합니다. [!DNL Experience Platform]의 스키마 작업에 대한 자세한 내용은 [XDM 시스템 개요](../xdm/home.md)를 읽는 것부터 시작하십시오.

### 시계열 이벤트 {#time-series-events}

시계열 데이터는 주체가 직접 또는 간접적으로 작업을 수행한 시점의 시스템 스냅샷과 이벤트 자체를 자세히 설명하는 데이터를 제공합니다. 표준 스키마 클래스 XDM ExperienceEvent로 표시되며, 시계열 데이터는 장바구니에 추가되는 항목, 클릭되는 링크 및 시청한 비디오와 같은 이벤트를 설명할 수 있습니다. 시계열 데이터를 사용하여 를 기반으로 세분화 규칙을 만들 수 있으며 프로필의 컨텍스트에서 이벤트에 개별적으로 액세스할 수 있습니다.

### ID

모든 기업은 개인적 느낌이 드는 방식으로 고객과 소통하기를 원합니다. 그러나 고객에게 적절한 디지털 환경을 제공하는 데 있어 어려운 점 중 하나는 자주 태블릿, 휴대폰 및 노트북과 같은 다양한 디지털 채널에 걸쳐 확산되는 연결이 끊어진 데이터를 함께 연결하는 방법을 이해하는 것입니다. [!DNL Identity Service]을(를) 사용하면 여러 채널의 id를 연결하고 각 고객에 대한 id 그래프를 만들어 고객의 전체 상황을 파악할 수 있습니다. 자세한 내용은 [ID 서비스 개요](../identity-service/home.md)를 참조하세요.

### 병합 정책

여러 소스에서 데이터 조각을 가져와서 각 개별 고객에 대한 전체 보기를 볼 수 있도록 결합할 때 병합 정책은 [!DNL Platform]에서 데이터의 우선 순위 지정 방법과 고객 프로필을 만드는 데 사용할 데이터를 결정하는 데 사용하는 규칙입니다.

여러 데이터 세트의 데이터가 충돌하는 경우 병합 정책에 따라 데이터를 처리하는 방법과 사용할 값이 결정됩니다. RESTful API 또는 사용자 인터페이스를 통해 새 병합 정책을 만들고 기존 정책을 관리하며 조직의 기본 병합 정책을 설정할 수 있습니다.

Experience Platform 내의 병합 정책 및 역할에 대해 자세히 알아보려면 [병합 정책 개요](merge-policies/overview.md)를 읽어 보십시오.

### 유니온 스키마 {#profile-fragments-and-union-schemas}

[!DNL Real-Time Customer Profile]의 주요 기능 중 하나는 다중 채널 데이터를 통합하는 기능입니다. [!DNL Real-Time Customer Profile]을(를) 사용하여 엔터티에 액세스하면 여러 데이터 세트에서 해당 엔터티에 대한 모든 프로필 조각의 병합된 보기를 제공할 수 있습니다. &quot;유니온 보기&quot;라고 하며 유니온 스키마라고 하는 것을 통해 가능합니다.

UI의 유니온 스키마에 액세스하는 방법을 포함하여 유니온 스키마에 대한 자세한 내용은 [유니온 스키마 UI 안내서](ui/union-schema.md)를 참조하십시오.

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## 프로필 및 대상자

Adobe Experience Platform [!DNL Segmentation Service]은(는) 개별 고객을 위한 경험을 제공하는 데 필요한 대상을 생성합니다. 대상자가 만들어지면 해당 대상자의 ID가 모든 자격 있는 프로필의 대상자 멤버십 목록에 추가됩니다. 세그먼트 규칙은 RESTful API 및 세그먼트 빌더 사용자 인터페이스를 사용하여 [!DNL Real-Time Customer Profile] 데이터에 빌드되고 적용됩니다. 세분화에 대해 자세히 알아보려면 [세분화 서비스 개요](../segmentation/home.md)를 읽는 것부터 시작하십시오.

### 스트리밍 수집 및 스트리밍 세분화

실시간 입력은 스트리밍 수집이라는 과정을 통해 가능하게 된다. 프로필 및 시계열 데이터가 수집되면 [!DNL Real-Time Customer Profile]은(는) 기존 데이터와 병합하고 유니온 보기를 업데이트하기 전에 스트리밍 세그먼테이션이라는 진행 중인 프로세스를 통해 해당 데이터를 대상에서 포함하거나 제외하도록 자동으로 결정합니다. 따라서 고객이 브랜드와 상호 작용할 때 즉시 계산을 수행하고 고객에게 향상된 개인화된 경험을 제공하기 위한 결정을 내릴 수 있습니다. 데이터를 수집하는 동안 데이터가 제대로 수집되고 데이터 세트가 기반으로 하는 스키마를 준수하는지 확인하는 유효성 검사도 수행합니다. 수집 중 유효성 검사가 수행되는 방법에 대한 자세한 내용은 [데이터 수집 품질 개요](../ingestion/quality/overview.md)를 읽는 것부터 시작하십시오.

## [!DNL Profile]에 데이터 수집 중

[!DNL Platform]은(는) 실시간 스트리밍 수집 및 일괄 처리 수집을 지원하면서 기록 및 시계열 데이터를 [!DNL Profile]에 보내도록 구성할 수 있습니다. 자세한 내용은 [실시간 고객 프로필에 데이터를 추가](tutorials/add-profile-data.md)하는 방법에 대한 개요를 설명하는 자습서를 참조하십시오.

>[!NOTE]
>
>[!DNL Analytics Cloud], [!DNL Marketing Cloud] 및 [!DNL Advertising Cloud]을(를) 포함하여 Adobe 솔루션을 통해 수집된 데이터는 [!DNL Experience Platform]&#x200B;(으)로 흘러 [!DNL Profile]&#x200B;(으)로 수집됩니다.

### 프로필 수집 지표

가시성 인사이트를 통해 Adobe Experience Platform의 주요 지표를 노출할 수 있습니다. 다양한 [!DNL Platform] 기능에 대한 [!DNL Experience Platform] 사용 통계 및 성능 지표 외에도 수신 요청 비율, 성공적인 수집 비율, 수집된 레코드 크기 등에 대한 통찰력을 얻을 수 있는 특정 프로필 관련 지표가 있습니다. 자세한 내용은 [Observability Insights API 개요](../observability/api/overview.md)를 읽는 것부터 시작하고, Real-Time Customer Profile 지표의 전체 목록에 대해서는 [사용 가능한 지표](../observability/api/metrics.md#available-metrics)에 대한 설명서를 참조하십시오.

## 프로필 저장소 데이터 업데이트

조직의 프로필 스토어에서 데이터를 업데이트해야 하는 경우가 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리 수집을 통해 수행할 수 있으며 업데이트 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 특성 업데이트에 대한 데이터 집합을 구성하는 방법에 대한 자세한 내용은 [프로필 및 업데이트에 대한 데이터 집합 활성화](../catalog/datasets/enable-upsert.md)에 대한 자습서를 참조하십시오.

## 데이터 거버넌스 및 [!DNL Privacy]

데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하는 데 사용되는 일련의 전략 및 기술입니다.

데이터 액세스와 관련된 데이터 거버넌스는 [!DNL Experience Platform] 내에서 다양한 수준에서 핵심 역할을 합니다.

- 데이터 사용 레이블 지정
- 데이터 액세스 정책
- 마케팅 액션을 위한 데이터에 대한 액세스 제어

데이터 거버넌스는 여러 지점에서 관리됩니다. 여기에는 [!DNL Platform]에 수집할 데이터와 지정된 마케팅 작업에 대한 수집 후 액세스할 수 있는 데이터를 결정하는 작업이 포함됩니다. 자세한 내용은 [데이터 거버넌스 개요](../data-governance/home.md)를 읽는 것부터 시작하십시오.

### 옵트아웃 및 데이터 개인 정보 보호 요청 처리

[!DNL Experience Platform]을(를) 통해 고객은 [!DNL Real-Time Customer Profile] 내의 데이터 사용 및 저장과 관련된 옵트아웃 요청을 보낼 수 있습니다. 옵트아웃 요청을 처리하는 방법에 대한 자세한 내용은 [옵트아웃 요청 준수](../segmentation/tutorials/consents.md)에 대한 설명서를 참조하십시오.

## 다음 단계 및 추가 리소스

Experience Platform UI 또는 프로필 API를 사용하여 실시간 고객 프로필 데이터를 사용하는 방법에 대한 자세한 내용은 각각 [프로필 UI 안내서](ui/user-guide.md) 또는 [API 개발자 안내서](api/overview.md)를 참조하십시오.
