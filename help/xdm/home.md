---
keywords: Experience Platform;home;popular topics;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;Mixins;mixins;mixin;Mixin;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema library;Schema Library;schema;record data;time series;time-series
solution: Experience Platform
title: XDM 시스템 개요
topic: overview
description: '표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다. '
translation-type: tm+mt
source-git-commit: b0b2f0c5aa91a5aeb5836d9795a580ccc69e3e17
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 1%

---


# XDM 시스템 개요

표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 공개적으로 문서화된 사양입니다. 서비스와 통신하는 데 사용할 응용 프로그램에 대한 일반적인 구조와 정의를 제공합니다 [!DNL Platform] . XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 전달할 수 있는 일반적인 표현으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 개인화를 위해 고객 속성을 표현할 수 있습니다.

XDM은 Adobe Experience Cloud이 제공하는 기본 프레임워크로, 정확한 타이밍에 적합한 [!DNL Experience Platform]채널을 통해 올바른 고객에게 올바른 메시지를 전달할 수 있습니다. XDM 시스템 [!DNL Experience Platform] 이 구축된 방법론은 서비스 [!DNL Experience Data Model] 에서 사용할 수 있도록 스키마를 공식화합니다 [!DNL Platform] .

이 문서에서는 XDM 시스템의 역할에 대한 개요를 제공합니다 [!DNL Experience Platform].

## XDM 스키마

[!DNL Experience Platform] 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 인제스트하려면 데이터 구조 [!DNL Platform]를 설명하고 각 필드에 포함할 수 있는 데이터 유형에 대한 제한을 제공하기 위해 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 혼합으로 구성됩니다.

디자인 원칙 및 모범 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 스키마 [컴포지션의 기본 사항을 참조하십시오](schema/composition.md).

### [!DNL Schema Registry] 및 [!DNL Schema Library]

이 **[!DNL Schema Registry]** 는 Adobe Experience Platform에서 모든 스키마 관련 리소스를 보고 관리할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다 **[!DNL Schema Library]**. 이 [!DNL Schema Library] [!DNL Experience Platform] 에는 Adobe에서 제공하는 업계 표준 리소스뿐만 아니라 애플리케이션을 사용하는 파트너 및 공급업체의 리소스도 포함되어 있습니다. 스키마 레지스트리 UI 및 API를 사용하여 조직 고유의 새 스키마 및 리소스를 만들고 관리할 수도 있습니다.

에서 제공되는 주요 작업에 대한 포괄적인 지침은 스키마 레지스트리 개발자 안내서 [!DNL Schema Registry]를 [참조하십시오](api/getting-started.md).

## XDM 시스템의 데이터 동작 {#data-behaviors}

에서 사용하기 위한 데이터 [!DNL Experience Platform] 는

* **데이터**&#x200B;기록:제목 속성에 대한 정보를 제공합니다. 대상은 조직 또는 개인일 수 있습니다.
* **시계열 데이터**:작업을 직접 또는 간접적으로 레코드 제목에 의해 수행한 시점에 시스템의 스냅샷을 제공합니다.

모든 XDM 스키마는 레코드 또는 시간 시리즈로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 동작은 스키마의 클래스에 의해 정의됩니다. 이 클래스는 스키마를 처음 만들 때 스키마에 할당됩니다. XDM 클래스는 특정 데이터 동작을 나타내려면 스키마에서 포함해야 하는 속성의 가장 작은 수를 설명합니다.

클래스 내에서 고유한 클래스를 정의할 수 있지만 [!DNL Schema Registry]기본 클래스 **[!DNL XDM Individual Profile]** **[!DNL XDM ExperienceEvent]** 와 레코드 및 시간 시리즈 데이터를 각각 사용하는 것이 좋습니다. 이러한 클래스는 아래에 자세히 설명되어 있습니다.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] 은 식별된 피사체와 부분적으로 식별된 피사체의 속성을 하나의 표현으로 구성하는 기록 기반 클래스입니다. 식별이 높은 프로필은 개인 커뮤니케이션 또는 타깃팅된 참여에 사용할 수 있으며 이름, 성별, 생년월일, 위치, 전화 번호 및 이메일 주소를 비롯한 연락처 정보와 같은 세부 개인 정보를 포함할 수 있습니다.

식별이 덜 된 프로필은 브라우저 쿠키와 같은 익명 행동 신호로만 구성할 수 있습니다. 이 경우 희소 프로필 데이터는 익명의 프로필의 관심사와 환경 설정이 수집되어 저장되는 정보 베이스를 만드는 데 사용됩니다. 주체가 알림, 구독, 구매 등에 등록함에 따라 이러한 식별자는 시간이 지남에 따라 더 자세히 표시될 수 있습니다. 이렇게 프로필 속성이 증가하면 결국 식별된 주제와 더 높은 수준의 타깃팅된 참여가 허용될 수 있습니다.

소비자 프로파일의 규모가 계속 커지면 개인 정보, 식별 정보, 연락처 정보 및 커뮤니케이션 환경 설정에 대한 강력한 저장소가 됩니다.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent는 이벤트(또는 이벤트 세트)가 발생한 시점과 관련된 대상의 ID를 포함하여 시스템 상태를 캡처하는 데 사용되는 시간 시리즈 기반 클래스입니다. 경험 이벤트는 발생한 사실에 대한 팩트 레코드이므로 변경할 수 없으며 집계 또는 해석 없이 발생한 사항을 나타냅니다. 특정 시간 동안 발생하는 변경 사항을 분석하고 트렌드를 추적하는 여러 시간 창 간에 비교할 수 있으므로 시간 도메인 분석에 매우 중요합니다.

경험 이벤트는 명시적이거나 암시적일 수 있습니다. 분명한 사건들은 여행중에 일어나는 인간의 행동을 직접 확인할 수 있다. 암묵적 사건은 직접적인 인간의 행동 없이 발생하지만 여전히 개인에게 관련 있는 사건입니다. 암묵적 이벤트의 예로는 특정 임계값에 도달하는 이메일 뉴스레터 또는 배터리 전압의 예약된 전송을 들 수 있습니다.

모든 데이터 소스에서 일부 이벤트가 쉽게 분류되는 것은 아니지만 처리할 수 있는 유사한 유형으로 비슷한 이벤트를 맞추는 것은 매우 중요합니다.

![ExperienceEvent 고객 경로](images/overview/experience-event-journey.png)

## XDM 스키마 및 [!DNL Experience Platform] 서비스

[!DNL Experience Platform] 는 스키마에 관계없이 XDM 표준을 준수하는 모든 스키마를 서비스에서 사용할 수 있음을 [!DNL Platform] 의미합니다. 다양한 서비스에서 스키마를 사용하는 방법은 아래에서 자세히 [!DNL Platform] 설명합니다.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 은 자산 및 관련 스키마에 대한 레코드 [!DNL Experience Platform] 시스템입니다. [!DNL Catalog] 은 데이터를 포함하는 실제 파일 또는 디렉토리가 아니라 이러한 파일 및 디렉토리에 대한 메타데이터와 설명이 들어 있습니다.

[!DNL Catalog] 데이터는 원본 또는 파일 포맷에 상관없이 [!DNL Data Lake]모든 데이터를 포함하는 매우 세분화된 데이터 저장소 [!DNL Platform]에 저장됩니다.

데이터를 인제스트하기 위해 데이터 세트 [!DNL Experience Platform]가 를 사용하여 만들어집니다 [!DNL Catalog Service]. 데이터 집합은 수집할 데이터 구조를 설명하는 XDM 스키마를 참조합니다. 스키마 없이 데이터 세트를 만들면 인제스트된 데이터 필드의 유형 및 컨텐츠를 검사하여 &quot;관측된 스키마&quot;를 파생하게 [!DNL Experience Platform] 됩니다. 그런 다음 데이터 집합 [!DNL Catalog] 을 추적하여 스키마와 함께 [!DNL Data Lake] 저장하며 이들이 기반으로 하는 스키마를 관찰합니다.

자세한 내용 [!DNL Catalog]은 [카탈로그 서비스 개요를 참조하십시오](../catalog/home.md). Adobe Experience Platform 데이터 섭취에 대한 자세한 내용은 [데이터 수집 개요를 참조하십시오](../ingestion/home.md).

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] 를 사용하면 표준 SQL을 사용하여 다양한 사용 사례를 지원하기 위해 [!DNL Experience Platform] 데이터를 쿼리할 수 있습니다.

스키마를 만들고 해당 스키마를 참조하는 데이터 세트를 만들면 데이터를 인제스트하여 데이터베이스에 저장됩니다 [!DNL Data Lake]. 를 [!DNL Query Service]사용하면 데이터 세트에 모든 데이터 세트 [!DNL Data Lake] 를 연결하고 쿼리 결과를 보고, 기계 학습 또는 수집 작업에 사용할 수 있는 새로운 데이터 세트로 캡처할 수 있습니다 [!DNL Real-time Customer Profile].

자세한 내용 [!DNL Query Service]은 [쿼리 서비스 소개를 참조하십시오](../query-service/home.md).

### [!DNL Real-time Customer Profile]

실시간 고객 프로필은 타깃팅되고 개인화된 경험 관리를 위한 중앙 집중식 소비자 프로필을 제공합니다. 각 프로필에는 모든 시스템에서 집계된 데이터와 함께 사용 중인 시스템에서 발생한 개별 이벤트에 대해 실행 가능한 타임스탬프가 지정된 계정이 포함됩니다 [!DNL Experience Platform].

[!DNL Real-time Customer Profile] 스키마 형식 데이터는 [!DNL XDM Individual Profile] 또는 [!DNL XDM ExperienceEvent] 클래스를 기반으로 사용하고 해당 데이터를 기반으로 쿼리에 응답합니다. [!DNL Profile] 은 다른 클래스를 기반으로 하는 스키마 사용을 지원하지 않습니다.

[!DNL Profile] 각 고객 프로파일의 인스턴스를 유지하여 데이터를 병합하여 개인에 대한 &quot;하나의 진실&quot;을 형성합니다. 이 통합 데이터는 &quot;조합 뷰&quot;라고 하는 것을 사용하여 표현됩니다. 조합 뷰는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 스키마로 집계합니다.  UI 또는 API를 사용하여 스키마를 작성할 때 함께 사용할 스키마를 활성화하고 결합 보기에 포함되도록 태그 [!DNL Real-time Customer Profile] 를 지정할 수 있습니다. 그러면 태그가 지정된 스키마가 제공되 [!DNL Profile]는 스키마 정의에 포함됩니다.

데이터 [!DNL XDM Individual Profile] 와 [!DNL XDM ExperienceEvent] 데이터가 수집 및 관리되므로 [!DNL Catalog]데이터 사용 [!DNL Real-time Customer Profile] 이 활성화된 데이터를 인제스트하기 시작합니다. 수집되는 인터랙션과 세부 사항이 많을수록 더욱 강력한 개별 프로필이 만들어집니다.

[!DNL XDM Individual Profile] 데이터는 모든 채널 또는 Adobe 솔루션 통합 전반에서 동작을 알려주고 강화하며, 행동 및 상호 작용 데이터의 풍부한 내역을 연결하는 경우 이 데이터를 시스템 학습에 활용합니다. 또한 [!DNL Real-time Customer Profile] API를 사용하여 타사 솔루션, CRM 및 독점 솔루션의 기능을 강화할 수 있습니다.

자세한 내용은 [실시간 고객 프로필 개요를](../profile/home.md) 참조하십시오.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] 는 기계 학습과 인공 지능을 사용하여 안에 저장된 데이터를 통해 통찰력을 얻고 [!DNL Experience Platform]있습니다. [!DNL Data Science Workspace] 데이터 과학자는 XDM 개인 사용자 [!DNL Profile] 와 고객 및 고객 활동에 대한 [!DNL XDM ExperienceEvent] 데이터를 기반으로 레시피를 제작하여 개인이 평가하고 사용할 가능성이 높은 고객 성향 및 제안 등을 손쉽게 예측할 수 있도록 합니다.

데이터 [!DNL Data Science Workspace]과학자는 머신 러닝 기반의 지능형 서비스 API를 쉽게 만들 수 있습니다. 이러한 서비스는 Adobe Target, Adobe Analytics Cloud 등 다른 Adobe 솔루션과 연동되므로 개인화된 디지털 경험을 자동화할 수 있습니다.

데이터를 사용하여 인사이트를 도출하는 방법에 대한 자세한 내용은 [!DNL Experience Platform] 데이터 과학 작업 공간 개요를 참조하십시오 [](../data-science-workspace/home.md).

## 다음 단계 및 추가 리소스

전체 스키마 역할을 더 잘 이해하게 되었으므로 [!DNL Experience Platform]직접 구성을 시작할 준비가 되었습니다. 학습 자료를 계속 보완하려면 제안된 설명서를 읽고 아래 비디오를 시청하십시오.

함께 사용할 스키마 작성에 대한 디자인 원칙 및 우수 사례 [!DNL Experience Platform]를 학습하려면 스키마 컴포지션의 [기본 사항을 읽으십시오](schema/composition.md). 스키마를 만드는 방법에 대한 단계별 지침은 API를 [사용하거나 사용자 인터페이스를](tutorials/create-schema-api.md) 사용하여 스키마를 만드는 방법에 대한 자습서를 [참조하십시오](tutorials/create-schema-ui.md).

다음 비디오 [!DNL XDM System] 를 [!DNL Experience Platform]통해 이해도를 높이십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

