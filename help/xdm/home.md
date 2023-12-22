---
keywords: Experience Platform;홈;인기 주제;XDM;XDM 시스템;XDM 개별 프로필;XDM 경험 이벤트;XDM 경험 이벤트;experienceEvent;경험 이벤트;필드 그룹;필드 그룹;필드 그룹;필드 그룹;경험 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;experienceEvent;experienceEvent;experienceEvent;XDM 경험 이벤트;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 레지스트리;스키마 라이브러리;스키마 라이브러리;스키마;스키마;레코드 데이터;시계열;시계열
solution: Experience Platform
title: XDM 시스템 개요
description: 표준화와 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 4%

---

# XDM 시스템 개요

표준화와 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 작업입니다.

XDM은 디지털 경험의 성능을 개선하기 위해 설계된 공개적으로 문서화된 사양입니다. 모든 애플리케이션이 를 사용하여 Platform 서비스와 통신할 수 있도록 하는 일반적인 구조 및 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 표현할 수 있습니다.

XDM은 Experience Platform을 기반으로 한 Adobe Experience Cloud이 적절한 사람에게 적절한 채널에서 정확한 순간에 올바른 메시지를 전달할 수 있는 기본 프레임워크입니다. Experience Platform이 구축된 방법론인 XDM 시스템은 플랫폼 서비스에서 사용할 Experience Data Model 스키마를 운영합니다.

Experience Platform 내에서 XDM 시스템의 역할에 대해 알아봅니다.

## XDM 스키마 {#xdm-schemas}

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 Platform에 수집하려면 먼저 데이터의 구조를 설명하고 각 필드 내에 포함할 수 있는 데이터 유형에 제약 조건을 제공하는 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다.

디자인 원칙 및 모범 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 [스키마 컴포지션 기본 사항](schema/composition.md).

### 표준 XDM 구성 요소 {#Standard-xdm-components}

XDM은 다양한 산업에서 일반적인 개념과 사용 사례를 캡처하기 위한 강력한 표준 필드 그룹 및 데이터 유형 컬렉션을 제공합니다. Experience Platform을 사용하면 이러한 구성 요소를 업종별로 필터링하여 특정 비즈니스 요구 사항을 가장 잘 지원하는 스키마를 빠르고 자신 있게 구성할 수 있습니다.

Experience Platform UI에서 스키마를 구성할 때 인기 지표와 함께 나열된 필드 그룹이 표시됩니다. 이 지표는 다른 Platform 사용자가 스키마에서 필드 그룹을 사용하는 빈도에 따라 결정됩니다. 숫자가 높을수록 필드 그룹의 인기가 높다. 기본적으로 검색 결과가 최고 인기 항목에서 최저 인기 항목에 걸쳐 표시되므로 업계의 데이터 모델링 트렌드를 파악할 수 있습니다.

![의 인기도 열 [!UICONTROL 필드 그룹 추가] 대화 상자.](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform은 Experience Platform의 모든 스키마 관련 리소스를 보고 관리할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다 **[!DNL Schema Library]**. 다음 [!DNL Schema Library] 에는 Adobe이 사용할 수 있는 표준 XDM 구성 요소와 사용하는 애플리케이션을 사용하는 Experience Platform 파트너 및 공급업체의 리소스가 포함되어 있습니다.

를 사용하여 조직에 고유한 새 스키마와 리소스를 만들고 관리할 수도 있습니다. [!DNL Schema Registry API]또는 [!UICONTROL 스키마] Platform UI의 작업 공간

Platform에서 스키마를 관리하고 상호 작용하는 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [XDM UI 안내서](./ui/overview.md)
* [스키마 레지스트리 API 안내서](./api/overview.md)

## XDM 시스템의 데이터 비헤이비어 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="데이터 비헤이비어"
>abstract="Experience Platform에서 사용할 데이터는 레코드, 시계열과 애드혹 등 세 가지 비헤이비어 유형으로 그룹화됩니다. 레코드 스키마는 주제 속성에 대한 정보를 제공하지만 시계열 스키마는 작업 수행 시 시스템 스냅샷을 캡처합니다. 임시 스키마는 단일 데이터 세트에서만 사용할 수 있도록 네임스페이스가 지정된 필드를 캡처합니다. Platform의 데이터 비헤이비어에 대한 자세한 내용은 설명서를 참조하십시오."

Experience Platform에서 사용하기 위한 데이터는 다음 세 가지 동작 유형으로 그룹화됩니다.

* **기록**: 제목의 속성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다.
* **시계열**: 레코드 주체가 직접 또는 간접적으로 작업을 수행한 시간에 시스템의 스냅샷을 제공합니다.
* **애드혹**: 단일 데이터 세트에서만 사용할 수 있도록 네임스페이스가 지정된 필드를 캡처합니다. 임시 스키마는 CSV 파일 수집 및 특정 종류의 소스 연결 생성 등 Experience Platform을 위한 다양한 데이터 수집 워크플로우에서 사용됩니다.

모든 XDM 스키마는 레코드 또는 시계열로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 비헤이비어는 스키마가 처음 생성될 때 스키마에 할당된 스키마의 클래스에 의해 정의됩니다. XDM 클래스는 특정 데이터 동작을 나타내기 위해 스키마에 포함해야 하는 최소 속성 수를 설명합니다.

내에서 고유한 클래스를 정의할 수는 있지만 [!DNL Schema Registry], 표준 클래스를 사용하는 것이 좋습니다 **[!UICONTROL XDM 개별 프로필]** 및 **[!UICONTROL XDM ExperienceEvent]** 레코드 및 시계열 데이터의 경우 각각 이러한 클래스는 아래에 자세히 설명되어 있습니다.

>[!NOTE]
>
>임시 동작을 기반으로 하는 표준 클래스는 없습니다. 임시 스키마는 이를 사용하는 Platform 프로세스에 의해 자동으로 생성되지만 다음과 같을 수도 있습니다. [스키마 레지스트리 API를 사용하여 수동으로 만들기](./tutorials/ad-hoc.md).

### [!UICONTROL XDM 개별 프로필] {#xdm-individual-profile}

[!UICONTROL XDM 개별 프로필] 는 식별된 주체와 부분적으로 식별된 주체 모두의 속성에 대한 단일 표현을 형성하는 레코드 기반 클래스입니다. 많이 식별된 프로필은 개인 커뮤니케이션 또는 타겟팅된 참여에 사용할 수 있습니다. 식별이 잘되는 프로필에는 이름, 성별, 생년월일, 위치 및 전화번호와 이메일 주소를 포함한 연락처 정보와 같은 자세한 개인 정보가 포함될 수 있습니다.

식별되지 않는 프로필은 브라우저 쿠키와 같은 익명 동작 신호로만 구성될 수 있습니다. 이 경우 스파스 프로필 데이터를 사용하여 익명 프로필의 관심 사항과 환경 설정을 수집하여 저장할 수 있는 정보 기반을 구축합니다. 이러한 식별자는 주체가 알림, 구독, 구매 등에 등록함에 따라 시간이 지남에 따라 더 자세히 표시될 수 있습니다. 프로필 속성의 이러한 증가는 결국 식별된 주제를 초래하고 더 높은 수준의 타겟팅된 참여를 허용할 수 있다.

프로필이 지속적으로 증가함에 따라 개인의 개인 정보, 식별 정보, 연락처 세부 정보 및 커뮤니케이션 환경 설정에 대한 강력한 저장소가 됩니다.

다음을 참조하십시오. [[!UICONTROL XDM 개별 프로필] 참조 안내서](./classes/individual-profile.md) 클래스에서 제공하는 필드의 구조 및 사용 사례에 대한 자세한 정보입니다.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent는 관련 주체의 시점 및 ID를 포함하여 이벤트(또는 이벤트 세트)가 발생했을 때 시스템 상태를 캡처하는 데 사용되는 시계열 기반 클래스입니다. 경험 이벤트는 해당 시점에 발생한 사항에 대한 사실상의 기록으로, 집계나 해석 없이 발생한 사항을 나타냅니다. 지정된 시간 내에 발생하는 변경 사항을 분석하고, 트렌드를 추적하기 위해 여러 시간 창을 비교하는 데 사용할 수 있으므로 시간 도메인 분석에 중요합니다.

경험 이벤트는 명시적이거나 암시적일 수 있습니다. 명시적 이벤트는 여정의 한 지점 동안 발생하는 관찰할 수 있는 인간 행동입니다. 암묵적 사건은 인간의 직접적인 행동 없이 제기되지만 여전히 개인과 관련된 사건이다. 암시적 이벤트들의 예들은 이메일 뉴스레터들의 스케줄링된 송신 또는 특정 임계치에 도달하는 배터리 전압을 포함할 수 있다.

모든 이벤트가 모든 데이터 소스에서 쉽게 분류하는 것은 아니지만, 처리를 위해 가능한 경우 유사한 이벤트를 유사한 유형으로 조화시키는 것은 매우 중요합니다.

![시간이 지남에 따라 경험 여정으로 시각화된 고객 이벤트의 인포그래픽입니다.](images/overview/experience-event-journey.png)

다음을 참조하십시오. [[!UICONTROL XDM ExperienceEvent] 참조 안내서](./classes/experienceevent.md) 클래스에서 제공하는 필드의 구조 및 사용 사례에 대한 자세한 정보입니다.

## XDM 스키마 및 Experience Platform 서비스 {#schemas-and-platform-services}

Experience Platform은 스키마와 관계없습니다. 즉, XDM 표준을 준수하는 모든 스키마를 Platform 서비스에서 사용할 수 있습니다. 다른 플랫폼 서비스가 스키마를 사용하는 방법은 아래에 더 자세히 설명되어 있습니다.

### 카탈로그 서비스, 데이터 수집 및 데이터 레이크 {#ingestion-catalog-and-storage}

카탈로그 서비스는 Experience Platform 에셋 및 관련 스키마에 대한 레코드 시스템입니다. 카탈로그에는 실제 데이터 파일 또는 디렉터리가 포함되어 있지 않지만, 이러한 파일 및 디렉터리에 대한 메타데이터와 설명이 들어 있습니다.

카탈로그 데이터는 원본 또는 파일 형식에 관계없이 플랫폼에서 관리하는 모든 데이터가 포함된 매우 세분화된 데이터 저장소인 데이터 레이크에 저장됩니다.

Experience Platform에 데이터 수집을 시작하려면 카탈로그 서비스 를 사용하여 데이터 세트를 만들 수 있습니다. 데이터 세트는 수집할 데이터의 구조를 설명하는 XDM 스키마를 참조합니다. 스키마 없이 데이터 세트를 만든 경우, Experience Platform은 수집된 데이터 필드의 유형 및 콘텐츠를 검사하여 &quot;관찰된 스키마&quot;를 파생합니다. 그런 다음 데이터 세트는 카탈로그 서비스에서 추적되고, 해당 데이터 세트가 기반으로 하는 스키마 및 관찰된 스키마와 함께 데이터 레이크에 저장됩니다.

다음을 참조하십시오. [카탈로그 서비스 개요](../catalog/home.md) 추가 정보. 다음을 참조하십시오. [데이터 수집 개요](../ingestion/home.md) Adobe Experience Platform 데이터 수집에 대한 자세한 내용.

### 쿼리 서비스 {#query-service}

표준 SQL을 사용하여 Experience Platform 데이터를 쿼리하여 Adobe Experience Platform 쿼리 서비스의 다양한 사용 사례를 지원할 수 있습니다.

스키마가 구성되고 해당 스키마를 참조하는 데이터 세트가 만들어지면 데이터가 수집되어 데이터 레이크에 저장됩니다. 그런 다음 쿼리 서비스 를 사용하여 데이터 레이크의 데이터 세트에 참여하고 쿼리 결과를 보고, 머신 러닝 또는 실시간 고객 프로필로의 수집에 사용할 새 데이터 세트로 캡처할 수 있습니다.

다음을 참조하십시오. [쿼리 서비스 개요](../query-service/home.md) 를 참조하십시오.

### 실시간 고객 프로필 {#real-time-customer-profile}

Real-Time Customer Profile은 타깃팅되고 개인화된 경험 관리를 위한 중앙 집중식 고객 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계된 데이터가 포함되어 있으며 프로필 주체와 관련된 이벤트의 실행 가능한 타임스탬프가 지정된 계정이 포함됩니다. 이러한 이벤트는 Experience Platform과 함께 사용하는 모든 시스템에서 발생했을 수 있습니다.

실시간 고객 프로필은 다음을 기반으로 스키마 형식의 데이터를 사용합니다. [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent] 클래스를 참조하고 해당 데이터를 기반으로 쿼리에 응답합니다.

>[!NOTE]
>
>실시간 고객 프로필은 다음을 수행합니다 **아님** 다른 클래스를 기반으로 하는 스키마 지원 [!UICONTROL XDM ExperienceEvent] 클래스.

시스템은 각 고객 프로필의 인스턴스를 유지 관리하며 데이터를 함께 병합하여 개인에 대한 &quot;단일 신뢰할 수 있는 소스&quot;를 구성합니다. 이러한 통합 데이터는 &quot;유니온 스키마&quot;(경우에 따라 &quot;유니온 뷰&quot;라고도 함)라고 하는 것을 사용하여 표시됩니다. 유니온 스키마는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 스키마로 집계합니다. UI 또는 API를 사용하여 스키마를 작성할 때 실시간 고객 프로필에 사용할 스키마를 활성화하고 태그를 지정하여 유니온에 포함할 수 있습니다. 그러면 태그가 지정된 스키마가 프로필에 제공되는 스키마 정의에 참여합니다.

다음으로: [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent] 데이터는 데이터 레이크로 수집되며 실시간 고객 프로필은 사용이 활성화된 모든 데이터를 수집합니다. 상호 작용과 세부 사항이 많을수록 개별 프로필이 더 강력해집니다.

[!UICONTROL XDM 개별 프로필] 데이터는 모든 채널 또는 Adobe 제품 통합 전반에 걸쳐 작업을 알리고 권한을 부여하는 데 도움이 됩니다. 행동 및 상호 작용 데이터의 풍부한 기록과 쌍을 이룰 때 이 데이터를 사용하여 머신 러닝을 수행할 수 있습니다. Real-Time Customer Profile API를 사용하여 서드파티 솔루션, CRM 및 독점 솔루션의 기능을 강화할 수도 있습니다.

다음을 참조하십시오. [실시간 고객 프로필 개요](../profile/home.md) 추가 정보.

### 데이터 과학 작업 영역 {#data-science-workspace}

Adobe Experience Platform 데이터 과학 작업 영역은 머신 러닝 및 인공 지능을 사용하여 Experience Platform 내에 저장된 데이터에서 통찰력을 얻습니다. Data Science Workspace 를 사용하면 데이터 과학자가 을 기반으로 레시피를 빌드할 수 있습니다. [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent] 고객 및 고객 활동에 대한 데이터. 이러한 레시피는 개인이 인식하고 사용할 가능성이 높은 구매 성향 및 추천 오퍼와 같은 예측을 용이하게 합니다.

Data Science Workspace 를 사용하면 데이터 과학자가 머신 러닝에서 제공하는 지능형 서비스 API를 쉽게 만들 수 있습니다. 이러한 서비스는 Adobe Target 및 Adobe Analytics Cloud을 포함한 다른 Adobe 솔루션과 함께 작동하여 개인화되고 타겟팅된 디지털 경험을 자동화할 수 있도록 지원합니다.

Experience Platform 데이터를 사용하여 통찰력을 강화하는 방법에 대한 자세한 내용은 [데이터 과학 작업 영역 개요](../data-science-workspace/home.md).

## 다음 단계 및 추가 리소스

이제 Experience Platform 전체에서 스키마의 역할을 더 잘 이해했으므로 나만의 작성을 시작할 준비가 되었습니다.

Experience Platform에 사용할 스키마를 구성하기 위한 디자인 원리와 모범 사례에 대해 알아보려면 [스키마 컴포지션 기본 사항](schema/composition.md). 스키마를 만드는 방법에 대한 단계별 지침은 스키마 만들기 튜토리얼 을 참조하십시오 [api 사용](tutorials/create-schema-api.md) 또는 [사용자 인터페이스 사용](tutorials/create-schema-ui.md).

에 대한 이해를 강화하기 위해 [!DNL XDM System] Experience Platform에서 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
