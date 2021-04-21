---
keywords: Experience Platform;홈;인기 항목;XDM;XDM;XDM 시스템;XDM 개별 프로필;XDM ExperienceEvent;XDM 경험 이벤트;경험 이벤트;경험 이벤트;믹싱;믹싱;혼합;경험 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;XDM 경험 이벤트;경험 이벤트;경험;이벤트;XDM 경험;경험 XDM 경험 이벤트;경험 데이터 모델;경험 데이터 모델;경험 데이터 모델;데이터 모델;데이터 모델;스키마 레지스트리;스키마 라이브러리;스키마 라이브러리;스키마 라이브러리;스키마 데이터;기록 데이터;시간 시리즈;시간 시리즈
solution: Experience Platform
title: XDM 시스템 개요
topic-legacy: overview
description: 표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. Adobe을 기반으로 하는 XDM(Experience Data Model)은 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하려는 노력의 일환입니다.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 1%

---

# XDM 시스템 개요

표준화 및 상호 운용성은 Adobe Experience Platform의 핵심 개념입니다. [!DNL Experience Data Model] (XDM)은 Adobe을 기반으로 고객 경험 데이터를 표준화하고 고객 경험 관리를 위한 스키마를 정의하는 것입니다.

XDM은 디지털 경험의 강력함을 향상시키도록 고안된 문서화된 사양입니다. 이 서비스는 [!DNL Platform] 서비스와 통신하는 데 사용할 응용 프로그램에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 보다 빠르고 통합된 방식으로 통찰력을 전달할 수 있는 일반적인 표현으로 통합할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 개인화를 위해 고객 속성을 표현할 수 있습니다.

XDM은 [!DNL Experience Platform] 제공 Adobe Experience Cloud이 올바른 고객에게 올바른 메시지를 정확한 타이밍에 올바른 채널에 전달할 수 있도록 하는 기본 프레임워크입니다. [!DNL Experience Platform]이(가) 빌드된 방법론인 XDM System은 [!DNL Experience Data Model] 스키마를 [!DNL Platform] 서비스에 사용하여 사용합니다.

이 문서에서는 [!DNL Experience Platform] 내 XDM 시스템 역할에 대한 개요를 제공합니다.

## XDM 스키마

[!DNL Experience Platform] 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 여러 시스템에서 데이터를 일관되게 정의하면 의미를 쉽게 유지할 수 있으므로 데이터의 가치를 얻을 수 있습니다.

데이터를 [!DNL Platform]으로 인제스트하려면 데이터 구조를 설명하고 각 필드에 포함할 수 있는 데이터 유형에 대한 제약 조건을 제공하도록 스키마를 구성해야 합니다. 스키마는 기본 클래스와 0개 이상의 혼합으로 구성됩니다.

디자인 원칙 및 우수 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 스키마 컴포지션](schema/composition.md)의 [기본 사항을 참조하십시오.

### [!DNL Schema Registry] 및 [!DNL Schema Library]

**[!DNL Schema Registry]**&#x200B;은 Adobe Experience Platform **[!DNL Schema Library]**&#x200B;에서 모든 스키마 관련 리소스를 보고 관리할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. [!DNL Schema Library]에는 Adobe이 제공하는 업계 표준 리소스와 [!DNL Experience Platform] 파트너 및 애플리케이션을 사용하는 공급업체의 리소스가 포함되어 있습니다. 스키마 레지스트리 UI 및 API를 사용하여 조직에 고유한 새 스키마 및 리소스를 만들고 관리할 수도 있습니다.

[!DNL Schema Registry]에서 사용할 수 있는 주요 작업에 대한 포괄적인 안내서는 [스키마 레지스트리 개발자 안내서](api/getting-started.md)를 참조하십시오.

## XDM 시스템 {#data-behaviors}의 데이터 동작

[!DNL Experience Platform]에서 사용하기 위한 데이터는 다음 두 가지 비헤이비어 유형으로 그룹화됩니다.

* **데이터** 기록:제목 속성에 대한 정보를 제공합니다. 대상은 조직 또는 개인일 수 있습니다.
* **시간 시리즈 데이터**:작업 수행 시 기록 제목에 의해 직접 또는 간접적으로 작업이 수행될 때 시스템의 스냅샷을 제공합니다.

모든 XDM 스키마는 레코드 또는 시간 시리즈로 분류할 수 있는 데이터를 설명합니다. 스키마의 데이터 동작은 스키마의 클래스에 의해 정의됩니다. 이 클래스는 스키마를 처음 만들 때 스키마에 할당됩니다. XDM 클래스는 특정 데이터 비헤이비어를 나타내기 위해 스키마에서 포함해야 하는 속성의 최소 수를 설명합니다.

[!DNL Schema Registry] 내에서 자신의 클래스를 정의할 수는 있지만, 레코드 및 시간 시리즈 데이터에 대해 각각 기본 설정 클래스 **[!DNL XDM Individual Profile]** 및 **[!DNL XDM ExperienceEvent]**&#x200B;를 사용하는 것이 좋습니다. 이러한 클래스는 아래에 자세히 설명되어 있습니다.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] 는 식별된 피사체와 부분적으로 식별된 피사체의 특성을 단일한 표현을 구성하는 기록 기반 클래스입니다. 식별이 높은 프로필은 개인 커뮤니케이션 또는 타깃팅된 참여에 사용할 수 있으며 이름, 성별, 생년월일, 위치 및 전화 번호 및 이메일 주소를 비롯한 연락처 정보와 같은 자세한 개인 정보를 포함할 수 있습니다.

식별되지 않은 프로필은 브라우저 쿠키와 같은 익명의 행동 신호로만 구성될 수 있습니다. 이 경우 스파스 프로필 데이터를 사용하여 익명의 프로필의 관심사와 환경 설정이 수집되어 저장되는 정보 베이스를 만듭니다. 대상이 알림, 구독, 구매 등을 등록함에 따라 이러한 식별자는 시간이 지남에 따라 더욱 상세해질 수 있습니다. 이렇게 프로필 속성이 증가하면 식별된 주제와 더 높은 수준의 타깃팅된 참여를 허용할 수 있습니다.

소비자 프로필이 지속적으로 성장함에 따라 개인 정보, 식별 정보, 연락처 정보 및 커뮤니케이션 환경 설정에 대한 강력한 저장소가 됩니다.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent는 관련 대상의 시점 및 ID를 포함하여 이벤트(또는 이벤트 집합)가 발생한 경우 시스템 상태를 캡처하는 데 사용되는 시간 시리즈 기반 클래스입니다. 경험 이벤트는 발생한 일의 팩트 레코드이므로 변경할 수 없으며 집계 또는 해석 없이 발생한 일을 나타냅니다. 특정 시간 동안 발생하는 변경 사항을 분석하고 트렌드를 추적하는 여러 시간 창 간을 비교할 수 있으므로 시간 도메인 분석에 매우 중요합니다.

경험 이벤트는 명시적이거나 암시적일 수 있습니다. 명시적 이벤트는 여정의 한 시점에서 일어나는 인간의 행동을 직접 관찰할 수 있습니다. 암묵적 이벤트는 직접적인 인간의 행동 없이 제기되지만 여전히 개인과 관련된 이벤트입니다. 암시적 이벤트의 예로는 특정 임계값에 도달하는 이메일 뉴스레터 또는 배터리 전압의 예약된 전송을 포함할 수 있습니다.

모든 데이터 소스에 걸쳐 모든 이벤트가 쉽게 분류되는 것은 아니지만 처리할 수 있는 유사한 이벤트를 유사한 유형으로 분류하는 것은 매우 중요합니다.

![ExperienceEvent 고객 여정](images/overview/experience-event-journey.png)

## XDM 스키마 및 [!DNL Experience Platform] 서비스

[!DNL Experience Platform] 는 스키마에 상관없이 모든 스키마입니다. 즉, XDM 표준을 준수하는 모든 스키마는 서비스에서 사용할 수  [!DNL Platform] 있습니다. 서로 다른 [!DNL Platform] 서비스에서 스키마를 사용하는 방법이 아래에 자세히 나와 있습니다.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 는 자산 및 관련 스키마에 대한 기록  [!DNL Experience Platform] 시스템입니다. [!DNL Catalog] 은 데이터를 포함하는 실제 파일 또는 디렉토리가 아니라 이러한 파일 및 디렉토리에 대한 메타데이터와 설명이 들어 있습니다.

[!DNL Catalog] 데이터는 원본 또는 파일 형식에 상관없이  [!DNL Data Lake]모든 데이터를 포함하는 매우 세분화된 데이터  [!DNL Platform]저장소에 저장됩니다.

데이터를 [!DNL Experience Platform]에 인제스트하기 시작하려면 [!DNL Catalog Service]을(를) 사용하여 데이터 세트를 만듭니다. 데이터 집합은 인제스트할 데이터의 구조를 설명하는 XDM 스키마를 참조합니다. 스키마 없이 데이터 세트를 만드는 경우 [!DNL Experience Platform]은 인제스트된 데이터 필드의 유형 및 내용을 검사하여 &quot;관측 스키마&quot;를 파생합니다. 그런 다음 데이터 집합은 [!DNL Catalog]에서 추적되고 스키마와 함께 [!DNL Data Lake]에 저장되며, 기반이 되는 스키마를 관찰합니다.

[!DNL Catalog]에 대한 자세한 내용은 [카탈로그 서비스 개요](../catalog/home.md)를 참조하십시오. Adobe Experience Platform 데이터 섭취에 대한 자세한 내용은 [데이터 통합 개요](../ingestion/home.md)를 참조하십시오.

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service]에서는 표준 SQL을 사용하여 [!DNL Experience Platform] 데이터를 쿼리하여 여러 가지 사용 사례를 지원합니다.

스키마를 작성하고 해당 스키마를 참조하는 데이터 세트를 만들면 데이터를 인제스트하여 [!DNL Data Lake]에 저장합니다. [!DNL Query Service]을 사용하여 [!DNL Data Lake]의 모든 데이터 세트에 참여하고 쿼리 결과를 보고, 기계 학습 또는 [!DNL Real-time Customer Profile]에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

[!DNL Query Service]에 대한 자세한 내용은 [쿼리 서비스 소개](../query-service/home.md)를 참조하십시오.

### [!DNL Real-time Customer Profile]

실시간 고객 프로필은 타깃팅되고 개인화된 경험 관리를 위한 중앙 집중식 소비자 프로필을 제공합니다. 각 프로필에는 모든 시스템에 걸쳐 집계된 데이터와 [!DNL Experience Platform]과 함께 사용하는 시스템에서 발생한 개별 이벤트에 대해 실행 가능한 타임스탬프가 지정된 계정이 포함됩니다.

[!DNL Real-time Customer Profile] 또는 클래스를 기반으로 스키마 형식 데이터를  [!DNL XDM Individual Profile] 사용하고 해당  [!DNL XDM ExperienceEvent] 데이터를 기반으로 쿼리에 응답합니다. [!DNL Profile] 는 다른 클래스를 기반으로 하는 스키마 사용을 지원하지 않습니다.

[!DNL Profile] 각 고객 프로파일의 인스턴스를 유지하여 데이터를 병합하여 개인에 대한 &quot;하나의 진실&quot;을 형성합니다. 이 통합 데이터는 &quot;조합 뷰&quot;라고 하는 것을 사용하여 표시됩니다. 공용 구조체 뷰는 동일한 클래스를 구현하는 모든 스키마의 필드를 단일 스키마로 집계합니다.  UI 또는 API를 사용하여 스키마를 작성할 때 [!DNL Real-time Customer Profile]에 사용할 수 있도록 스키마를 활성화하고 이 스키마에 태그를 지정하여 조합 보기에 포함할 수 있습니다. 그러면 태그가 지정된 스키마가 [!DNL Profile]에 제공되는 스키마 정의에 참여하게 됩니다.

[!DNL XDM Individual Profile] 및 [!DNL XDM ExperienceEvent] 데이터가 인제스트되고 [!DNL Catalog]에 의해 관리되므로 [!DNL Real-time Customer Profile]이(가) 사용할 수 있도록 활성화된 데이터 인제링을 시작합니다. 인제스트된 인터랙션과 세부 사항이 많을수록 더욱 강력한 개별 프로필이 만들어집니다.

[!DNL XDM Individual Profile] 데이터는 모든 채널 또는 Adobe 솔루션 통합 전반에 걸쳐 동작을 알려주고 강화하며, 행동 데이터와 상호 작용 데이터의 풍부한 기록을 조합하면 이 데이터를 머신 러닝에 활용할 수 있습니다. 또한 [!DNL Real-time Customer Profile] API를 사용하여 타사 솔루션, CRM 및 독점 솔루션의 기능을 강화할 수 있습니다.

자세한 내용은 [실시간 고객 프로필 개요](../profile/home.md)를 참조하십시오.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace]은(는) 기계 학습과 인공 지능을 사용하여 [!DNL Experience Platform] 내에 저장된 데이터를 통해 통찰력을 얻습니다. [!DNL Data Science Workspace] 데이터 과학자는 XDM 개인 사용자 [!DNL Profile] 와 고객  [!DNL XDM ExperienceEvent] 활동 데이터를 기반으로 레서피를 작성할 수 있도록 하여 개인이 평가하고 사용할 가능성이 높은 고객 성향 및 추천 오퍼를 손쉽게 예측할 수 있습니다.

데이터 과학자는 [!DNL Data Science Workspace]을 사용하여 머신 러닝 기반의 지능형 서비스 API를 쉽게 만들 수 있습니다. 이러한 서비스는 Adobe Target 및 Adobe Analytics Cloud을 비롯한 다른 Adobe 솔루션과 연동되므로 개인화된 디지털 경험을 자동화할 수 있습니다.

통찰력을 얻기 위해 [!DNL Experience Platform] 데이터를 사용하는 방법에 대한 자세한 내용은 [데이터 과학 작업 공간 개요](../data-science-workspace/home.md)를 참조하십시오.

## 다음 단계 및 추가 리소스

이제 [!DNL Experience Platform] 전체에서 스키마 역할을 더 잘 이해하므로 직접 구성을 시작할 준비가 되었습니다. 학습에 대한 추가 작업을 계속하려면 제안된 설명서를 읽고 아래 비디오를 시청하십시오.

[!DNL Experience Platform]에 사용할 스키마 작성에 대한 디자인 원칙과 우수 사례를 알아보려면 스키마 컴포지션](schema/composition.md)의 [기본 사항을 읽으십시오. 스키마를 만드는 방법에 대한 단계별 지침은 사용자 인터페이스](tutorials/create-schema-ui.md)를 사용하여 [API](tutorials/create-schema-api.md) 또는 [스키마를 만드는 방법에 대한 자습서를 참조하십시오.

[!DNL Experience Platform]의 [!DNL XDM System]에 대한 이해를 강화하려면 다음 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
