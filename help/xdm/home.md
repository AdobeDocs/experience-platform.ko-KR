---
keywords: Experience Platform;홈;인기 항목;XDM;XDM 시스템;XDM 개별 프로필;XDM ExperienceEvent;XDM 경험 이벤트;경험 이벤트;경험 이벤트;필드 그룹;필드 그룹;필드 그룹;경험 이벤트;XDM 경험 이벤트;XDM ExperienceEvent;experienceEvent;XDM ExperienceEvent;경험 이벤트;XDM 경험 이벤트;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;레지스트리 스키마;스키마 스키마 스키마;스키마;스키마;레코드 데이터;시계열;시계열
solution: Experience Platform
title: XDM 시스템 개요
topic-legacy: overview
description: 표준화와 상호 운용성은 Adobe Experience Platform의 주요 개념입니다. Adobe 기반의 XDM(경험 데이터 모델)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력입니다.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: a95e5cf02e993d6c761abd74c98c0967a89eb678
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 2%

---

# XDM 시스템 개요

표준화와 상호 운용성은 Adobe Experience Platform의 주요 개념입니다. [!DNL Experience Data Model] Adobe 기반의 XDM(Customer Experience Management)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력입니다.

XDM은 디지털 경험의 힘을 향상시키기 위해 설계된 문서화된 사양입니다. 모든 애플리케이션에서 플랫폼 서비스와 통신하는 데 사용할 수 있는 공통 구조 및 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있는 공통 표현으로 통합할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 표현할 수 있습니다.

XDM은 Experience Platform을 기반으로 하는 Adobe Experience Cloud이 올바른 사람에게 올바른 메시지를 올바른 채널에 정확히 적절한 시점에 전달할 수 있도록 하는 기본 프레임워크입니다. Experience Platform을 빌드하는 방법론인 XDM 시스템은 운영을 활성화합니다 [!DNL Experience Data Model] 플랫폼 서비스에서 사용할 스키마.

이 문서에서는 Experience Platform 내에서 XDM 시스템의 역할에 대한 개요를 제공합니다.

## XDM 스키마

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 Platform에 수집하려면 먼저 데이터 구조를 설명하고 각 필드 내에 포함할 수 있는 데이터 유형에 제한을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 스키마 필드 그룹으로 구성됩니다.

디자인 원칙 및 모범 사례를 포함한 스키마 구성 모델에 대한 자세한 내용은 다음을 참조하십시오. [스키마 구성 기본 사항](schema/composition.md).

### 표준 XDM 구성 요소

XDM은 다양한 업계에서 일반적인 개념과 사용 사례를 캡처하기 위한 표준 필드 그룹 및 데이터 유형의 강력한 컬렉션을 제공합니다. Experience Platform을 사용하면 이러한 구성 요소를 업종별로 필터링할 수 있으므로 특정 비즈니스 요구 사항을 가장 잘 지원하는 스키마를 빠르고 확실하게 구성할 수 있습니다.

Experience Platform UI에서 스키마를 구성할 때 나열된 필드 그룹이 인기도 지표와 함께 표시됩니다. 이 지표는 다른 Platform 사용자가 해당 스키마에서 필드 그룹을 사용하는 빈도에 따라 결정됩니다. 숫자가 많을수록 필드 그룹이 더 인기가 많습니다. 기본적으로 결과는 가장 인기 있는 것에서 가장 인기 없는 것으로 표시되므로 업계의 데이터 모델링 트렌드에 대해 파악할 수 있습니다.

![필드 그룹 인기도](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform은 Experience Platform에서 모든 스키마 관련 리소스를 보고 관리할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다 **[!DNL Schema Library]**. 다음 [!DNL Schema Library] 에는 Adobe이 제공하는 표준 XDM 구성 요소와 사용자가 애플리케이션을 사용하는 Experience Platform 파트너 및 공급업체의 리소스가 포함되어 있습니다.

사용 [!DNL Schema Registry API] 또는 [!UICONTROL 스키마] 작업 공간 을 사용하면 플랫폼 UI에서 조직에 고유한 새 스키마와 리소스를 만들고 관리할 수도 있습니다.

Platform에서 스키마를 관리하고 상호 작용하는 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [XDM UI 안내서](./ui/overview.md)
* [스키마 레지스트리 API 안내서](./api/overview.md)

## XDM 시스템의 데이터 동작 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="데이터 비헤이비어"
>abstract="Experience Platform에 사용하기 위한 데이터는 다음 세 가지 동작 유형으로 그룹화됩니다. 레코드, 시계열 및 ad hoc. 레코드 스키마는 주체의 속성에 대한 정보를 제공하는 반면, 시간 시리즈 스키마는 작업을 수행할 때 시스템의 스냅샷을 캡처합니다. Ad Hoc 스키마는 단일 데이터 세트에서만 사용할 네임스페이스인 필드를 캡처합니다. Platform의 데이터 행동에 대한 자세한 내용은 설명서를 참조하십시오."

Experience Platform에 사용하기 위한 데이터는 다음 세 가지 동작 유형으로 그룹화됩니다.

* **레코드**: 주체의 특성에 대한 정보를 제공합니다. 주제는 조직 또는 개인일 수 있습니다.
* **시계열**: 작업 수행 시 레코드 주체가 직접 또는 간접적으로 시스템의 스냅샷을 제공합니다.
* **애드혹**: 단일 데이터 집합에서만 사용하도록 지정된 필드를 캡처합니다. 임시 스키마는 CSV 파일 섭취와 특정 종류의 소스 연결 만들기를 포함하여, Experience Platform을 위한 다양한 데이터 수집 워크플로우에서 사용됩니다.

모든 XDM 스키마에서는 레코드 또는 시계열로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 동작은 처음 만들 때 스키마에 할당된 스키마 클래스에 의해 정의됩니다. XDM 클래스는 특정 데이터 동작을 나타내려면 스키마에 포함해야 하는 가장 작은 수의 속성을 설명합니다.

에서는 고유한 클래스를 정의할 수 있지만 [!DNL Schema Registry]를 지정하는 경우에는 표준 클래스를 사용하는 것이 좋습니다 **[!UICONTROL XDM 개별 프로필]** 및 **[!UICONTROL XDM ExperienceEvent]** 레코드 및 시계열 데이터의 경우 각각. 이러한 클래스는 아래에 자세히 설명되어 있습니다.

>[!NOTE]
>
>임시 동작을 기반으로 하는 표준 클래스는 없습니다. 임시 스키마는 활용하는 플랫폼 프로세스에 의해 자동으로 생성되지만, 다음과 같은 것일 수도 있습니다 [스키마 레지스트리 API를 사용하여 수동으로 만들기](./tutorials/ad-hoc.md).

### [!UICONTROL XDM 개별 프로필] {#xdm-individual-profile}

[!UICONTROL XDM 개별 프로필] 는 식별된 주제와 부분적으로 식별된 주제의 속성을 단일 표현으로 구성하는 레코드 기반 클래스입니다. 식별이 높은 프로필은 개인 통신 또는 타겟팅된 계약에 사용할 수 있으며 이름, 성별, 생년월일, 위치, 전화 번호 및 이메일 주소 등 자세한 개인 정보를 포함할 수 있습니다.

식별되지 않는 프로필은 브라우저 쿠키와 같은 익명의 행동 신호로만 구성될 수 있습니다. 이 경우 스파스 프로필 데이터는 익명 프로필의 관심사와 선호도가 순서대로 순서대로 정렬되어 저장되는 정보 베이스를 만드는 데 사용됩니다. 주체가 알림, 구독, 구매 등에 등록함에 따라 시간이 지남에 따라 이러한 식별자가 더 자세히 표시될 수 있습니다. 이러한 프로필 속성 증가로 인해 결국 식별된 주제가 생성되고 더 높은 타깃팅된 참여도를 허용할 수 있습니다.

프로필의 규모가 계속 커지면 개인 정보, 식별 정보, 연락처 세부 정보 및 커뮤니케이션 환경 설정이 견고한 저장고가 됩니다.

자세한 내용은 [[!UICONTROL XDM 개별 프로필] 참조 안내서](./classes/individual-profile.md) 클래스에서 제공하는 필드의 구조 및 사용 사례에 대한 자세한 내용을 참조하십시오.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent는 관련 주체의 시간과 ID를 포함하여 이벤트(또는 이벤트 세트)가 발생한 경우 시스템의 상태를 캡처하는 데 사용되는 시계열 기반 클래스입니다. 경험 이벤트는 해당 시점에 발생한 내용에 대한 사실상 레코드를 변경할 수 없으며, 합계 또는 해석 없이 발생한 사항을 나타냅니다. 지정된 시간 창에서 발생하는 변경 사항을 분석하고 트렌드를 추적하기 위해 여러 시간 창 간을 비교하는 데 사용할 수 있으므로 시간 도메인 분석에 매우 중요합니다.

경험 이벤트는 명시적이거나 암시적일 수 있습니다. 명시적 이벤트는 여정의 한 지점에서 발생하는 직접 확인할 수 있는 인간의 작업입니다. 암시적 이벤트는 직접적인 인간의 행동 없이 제기되지만 여전히 개인과 관련된 이벤트입니다. 암시적 이벤트의 예로는 특정 임계값에 도달하는 이메일 뉴스레터 또는 배터리 전압의 예약된 전송을 들 수 있습니다.

모든 이벤트가 모든 데이터 소스에서 쉽게 분류되는 것은 아니지만 유사한 이벤트를 처리할 수 있는 유사한 유형으로 일치시키는 것이 매우 중요합니다.

![ExperienceEvent 고객 여정](images/overview/experience-event-journey.png)

자세한 내용은 [[!UICONTROL XDM ExperienceEvent] 참조 안내서](./classes/experienceevent.md) 클래스에서 제공하는 필드의 구조 및 사용 사례에 대한 자세한 내용을 참조하십시오.

## XDM 스키마 및 Experience Platform 서비스

Experience Platform은 스키마에 관계없이, 즉 XDM 표준을 준수하는 모든 스키마를 Platform 서비스에서 사용할 수 있습니다. 다양한 Platform 서비스에서 스키마를 사용하는 방법은 아래에 자세히 설명되어 있습니다.

### 카탈로그 서비스, 데이터 수집 및 데이터 레이크

카탈로그 서비스는 Experience Platform 자산 및 관련 스키마에 대한 레코드 시스템입니다. 카탈로그에는 실제 데이터 파일 또는 디렉터리가 들어 있지 않지만, 해당 파일 및 디렉터리에 대한 메타데이터와 설명이 들어 있습니다.

카탈로그 데이터는 원본 또는 파일 형식에 관계없이 Platform에서 관리하는 모든 데이터를 포함하는 매우 세분화된 데이터 저장소인 데이터 레이크에 저장됩니다.

데이터를 Experience Platform으로 수집하기 위해 카탈로그 서비스를 사용하여 데이터 세트를 만들 수 있습니다. 데이터 집합은 수집할 데이터의 구조를 설명하는 XDM 스키마를 참조합니다. 스키마 없이 데이터 세트를 만드는 경우 Experience Platform은 수집된 데이터 필드의 유형 및 컨텐츠를 검사하여 &quot;관찰된 스키마&quot;를 도출합니다. 그런 다음 데이터 세트가 카탈로그에서 추적되고 스키마와 함께 데이터 레이크에 저장되고 데이터 세트가 기반으로 하는 스키마를 관찰했습니다.

카탈로그에 대한 자세한 내용은 [카탈로그 서비스 개요](../catalog/home.md). Adobe Experience Platform 데이터 처리에 대한 자세한 내용은 [데이터 수집 개요](../ingestion/home.md).

### 쿼리 서비스

Adobe Experience Platform Query Service를 사용하면 표준 SQL을 사용하여 Experience Platform 데이터를 쿼리하여 다양한 사용 사례를 지원할 수 있습니다.

스키마를 구성하고 해당 스키마를 참조하는 데이터 세트를 만들면 데이터를 수집하여 Data Lake에 저장합니다. Query Service를 사용하여 데이터 레이크에서 모든 데이터 세트를 결합하고 쿼리 결과를 보고, 머신 러닝 또는 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처할 수 있습니다.

자세한 내용은 [쿼리 서비스 개요](../query-service/home.md) 를 참조하십시오.

### 실시간 고객 프로필

실시간 고객 프로필은 타겟팅되고 개인화된 경험 관리를 위한 중앙 집중식 소비자 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계되는 데이터와, Experience Platform에 사용하는 시스템에서 발생한 개별 이벤트와 관련된 실행 가능한 타임스탬프 계정이 포함되어 있습니다.

실시간 고객 프로필은 [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent] 클래스와 해당 데이터를 기반으로 하는 쿼리에 응답합니다. 프로필은 다른 클래스를 기반으로 한 스키마 사용을 지원하지 않습니다.

이 시스템은 각 고객 프로필의 인스턴스를 유지 관리하여 데이터를 병합하여 개인에게 대한 &quot;단일 진실의 소스&quot;를 생성합니다. 이러한 통합 데이터는 &quot;결합 스키마&quot;라고도 하는 를 사용하여 표시됩니다(&quot;결합 보기&quot;라고도 함). 결합 스키마는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 스키마에 집계합니다.  UI 또는 API를 사용하여 스키마를 작성할 때 실시간 고객 프로필에서 사용할 수 있도록 스키마를 활성화하고 태그에 태깅하여 결합에 포함할 수 있습니다. 그러면 태그가 지정된 스키마가 프로필에 제공되는 스키마 정의에 참여합니다.

로서의 [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent] 데이터는 데이터 레이크에 수집됩니다. 실시간 고객 프로필은 사용하기 위해 활성화된 모든 데이터를 수집합니다. 수집된 상호 작용 및 세부 사항이 많을수록 더 강력한 개별 프로필이 생성됩니다.

[!UICONTROL XDM 개별 프로필] 데이터는 모든 채널 또는 Adobe 제품 통합에서 작업을 알리고 강화하는 데 도움이 됩니다. 행동 및 상호 작용 데이터의 풍부한 내역과 쌍을 이루는 경우 이 데이터를 머신 러닝을 지원하는 데 사용할 수 있습니다. 또한 실시간 고객 프로필 API를 사용하여 타사 솔루션, CRM 및 독점 솔루션의 기능을 보강할 수 있습니다.

자세한 내용은 [실시간 고객 프로필 개요](../profile/home.md) 추가 정보.

### 데이터 과학 작업 영역

Adobe Experience Platform Data Science Workspace은 기계 학습 및 인공 지능을 사용하여 Experience Platform 내에 저장된 데이터를 통해 통찰력을 얻을 수 있습니다. 데이터 과학 작업 공간 을 통해 데이터 과학자들이 다음을 기반으로 레시피를 작성할 수 있습니다 [!UICONTROL XDM 개별 프로필] 및 [!UICONTROL XDM ExperienceEvent] 고객 및 해당 활동에 대한 데이터로, 개인이 평가하고 사용할 가능성이 있는 성향 및 권장 오퍼 구매와 같은 예측을 용이하게 합니다.

데이터 과학자들은 Data Science Workspace를 사용하여 머신 러닝을 기반으로 한 지능형 서비스 API를 손쉽게 만들 수 있습니다. 이러한 서비스는 Adobe Target 및 Adobe Analytics Cloud을 포함한 다른 Adobe 솔루션과 연동하여 개인화된 타깃팅된 디지털 경험을 자동화할 수 있습니다.

인사이트를 제공하는 Experience Platform 데이터를 사용하는 방법에 대한 자세한 내용은 [Data Science Workspace 개요](../data-science-workspace/home.md).

## 다음 단계 및 추가 리소스

Experience Platform 전체에서 스키마의 역할을 더 잘 이해했으므로 이제 직접 작성할 준비가 되었습니다.

Experience Platform에 사용할 스키마를 구성하기 위한 디자인 원칙 및 모범 사례를 알아보려면 [스키마 구성 기본 사항](schema/composition.md). 스키마를 만드는 방법에 대한 단계별 지침은 스키마 만들기에 대한 자습서를 참조하십시오 [api 사용](tutorials/create-schema-api.md) 또는 [사용자 인터페이스 사용](tutorials/create-schema-ui.md).

이해도를 높이기 위해 [!DNL XDM System] Experience Platform에서 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
