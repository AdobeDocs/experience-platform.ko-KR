---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
solution: Adobe Experience Platform
title: 실시간 고객 프로필 개요
topic: guide
description: 실시간 고객 프로필은 다양한 엔터프라이즈 데이터 자산의 데이터를 수집한 다음 개별 고객 프로필 및 관련 시간 시리즈 이벤트의 형태로 해당 데이터에 대한 액세스를 제공하는 범용 조회 엔티티 스토어입니다. 이 기능을 통해 마케터는 다양한 채널에서 고객과 연관성 있고 조율된 경험을 제공할 수 있습니다.
translation-type: tm+mt
source-git-commit: cef27082fec97530031061476b46f60859717825
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]개요

Adobe Experience Platform을 사용하면 고객이 브랜드와 언제 어디에서나 고객의 기대에 부응하는 일관된 경험을 제공할 수 있습니다. 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널의 데이터를 결합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Real-time Customer Profile] [!DNL Profile] 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다. 이 개요는 에서 의 역할과 사용 방법을 이해하는 데 도움이 [!DNL Real-time Customer Profile] 됩니다 [!DNL Experience Platform].


## [!DNL Profile] experience platform

실시간 고객 프로필과 Experience Platform 내의 다른 서비스 간의 관계는 다음 다이어그램에서 강조됩니다.

![Adobe Experience Platform 서비스.](images/profile-overview/profile-in-platform.png)

## 프로필 데이터

[!DNL Real-time Customer Profile] 은 다양한 엔터프라이즈 데이터 자산의 데이터를 병합한 다음 개별 고객 프로필 및 관련 시계열 이벤트의 형태로 해당 데이터에 대한 액세스를 제공하는 범용 조회 엔티티 스토어입니다. 이 기능을 통해 마케터는 다양한 채널에서 고객과 연관성 있고 조율된 경험을 제공할 수 있습니다.

### 프로필 가드레일

Experience Platform은 실시간 고객 프로필에서 지원할 수 없는 [경험 데이터 모델(XDM) 스키마를 만들지 않도록](../xdm/home.md) 하는 데 도움이 되는 일련의 지침을 제공합니다. 여기에는 성능 저하를 초래할 수 있는 소프트 한도 뿐만 아니라 오류 및 시스템 중단으로 이어질 수 있는 하드 제한이 포함됩니다. 지침 목록 및 사용 사례 예를 비롯한 자세한 내용은 [프로필 지침을 참조하십시오](guardrails.md) .

### 프로필 스토어

데이터 수집 [!DNL Real-time Customer Profile] 을 처리하고 ID 매핑을 통해 관련 데이터 [!DNL Identity Service] 를 병합하기 위해 Adobe Experience Platform을 사용하지만 스토어의 자체 데이터를 [!DNL Profile] 유지합니다. 즉, 스토어 [!DNL Profile] 는 [!DNL Catalog] 데이터([!DNL Data Lake]) 및 [!DNL Identity Service] 데이터(ID 그래프)와 별개입니다.

### 데이터 기록

프로필은 제목, 조직 또는 개인을 레코드 데이터라고 하는 표현입니다. 예를 들어 제품 프로필에는 SKU와 설명이 포함될 수 있지만 개인 프로필에는 이름, 성 및 이메일 주소와 같은 정보가 포함되어 있습니다. 를 [!DNL Experience Platform]사용하면 프로파일을 사용자 정의하여 비즈니스와 관련된 데이터 유형을 사용할 수 있습니다. 표준 [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] 클래스는 고객 레코드 데이터를 설명할 때 스키마를 작성하고 플랫폼 서비스 간의 다양한 상호 작용에 데이터 통합 요소를 제공하는 기본 클래스입니다. 스키마 작업에 대한 자세한 내용 [!DNL Experience Platform]은 [XDM 시스템 개요를 읽어 보십시오](../xdm/home.md).

### 시계열 이벤트

시간 시리즈 데이터는 작업이 대상에 의해 직접 또는 간접적으로 수행되는 시점에 시스템의 스냅숏과 이벤트 자체를 자세히 설명하는 데이터를 제공합니다. 표준 스키마 클래스 XDM ExperienceEvent로 표현되는 시간 시리즈 데이터는 장바구니에 추가되는 항목, 클릭되는 링크 및 본 비디오와 같은 이벤트를 설명할 수 있습니다. 시간 시리즈 데이터를 사용하여 세분화 규칙을 기반으로 할 수 있으며, 이벤트는 프로필 컨텍스트에서 개별적으로 액세스할 수 있습니다.

### ID

모든 비즈니스는 개인화된 방식으로 고객과 커뮤니케이션하기를 원합니다. 그러나 고객에게 연관성 있는 디지털 경험을 제공하려면 단절된 데이터를 서로 연결하는 방법을 이해하는 것이 중요합니다. 이러한 데이터는 일반적으로 태블릿, 휴대폰, 랩탑 등 다양한 디지털 채널에서 확산됩니다. [!DNL Identity Service] 다양한 채널에서 ID를 연결하고 각 고객에 대한 ID 그래프를 만들어 고객의 전체 상황을 파악할 수 있습니다. 자세한 내용은 [ID 서비스 개요를](../identity-service/home.md) 참조하십시오.

### 세그먼테이션

Adobe Experience Platform [!DNL Segmentation Service] 는 개별 고객의 경험을 향상시키는 데 필요한 고객을 제작합니다. 대상 세그먼트가 만들어지면 해당 세그먼트의 ID가 모든 적격한 프로필에 대한 세그먼트 구성원 자격 목록에 추가됩니다. 세그먼트 규칙은 RESTful API 및 세그먼트 빌더 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile] 데이터에 작성하고 적용됩니다. 세그멘테이션에 대한 자세한 내용은 세그멘테이션 [서비스 개요를 읽어 보십시오](../segmentation/home.md).

### 프로필 조각 및 결합 스키마 {#profile-fragments-and-union-schemas}

멀티 채널 데이터 통합 [!DNL Real-time Customer Profile] 의 주요 기능 중 하나는 엔티티 [!DNL Real-time Customer Profile] 에 액세스하는 데 사용될 경우, 조합 보기라고 하며 조합 스키마라고 하는 것을 통해 해당 엔티티에 대한 모든 프로필 조각에 대한 병합된 뷰를 제공할 수 있습니다. [!DNL Real-time Customer Profile] ID로 액세스하거나 세그먼트로 내보낼 때 데이터가 소스 간에 병합됩니다. API를 사용하여 프로필 및 조합 보기에 액세스하는 방법에 대한 자세한 내용은 [!DNL Real-time Customer Profile] 엔티티 끝점 안내서를 참조하십시오 [](api/entities.md).

### 정책 병합

여러 소스에서 데이터를 취합하여 각 개별 고객의 전체 상황을 파악할 수 있도록 결합하는 경우 병합 정책은 데이터의 우선 순위가 어떻게 지정되고 어떤 데이터가 결합되어 통합 뷰를 만들 것인지를 결정하는 데 [!DNL Platform] 사용하는 규칙입니다. RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. API를 사용한 병합 정책 작업에 대한 자세한 내용은 [!DNL Real-time Customer Profile] 병합 정책 끝점 안내서를 참조하십시오 [](api/merge-policies.md). UI를 사용하여 병합 정책을 사용하려면 [!DNL Experience Platform] 병합 정책 사용 안내서를 참조하십시오 [](ui/merge-policies.md).

### (알파) 계산된 속성 구성

>[!IMPORTANT]
>
>계산된 속성 기능은 alpha입니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 프로필 수준에서 작동합니다. 즉, 모든 레코드와 이벤트에 대한 값을 합산할 수 있습니다. 계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성이나 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 시간 또는 애플리케이션 열기 횟수와 같은 문제와 관련된 질문에 쉽게 응답할 수 있습니다. 계산된 속성에 대한 자세한 내용 및 [!DNL Real-time Customer Profile] API를 사용한 작업에 대한 단계별 지침을 보려면 [계산된 속성 끝점 안내서를 참조하십시오](api/computed-attributes.md). 이 안내서는 Adobe Experience Platform 내에서 작동하는 역할 계산 속성을 더 잘 이해하는 데 도움이 되며 기본 CRUD 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 실시간 구성 요소

이 섹션에서는 기록 및 시간 시리즈 데이터 [!DNL Real-time Customer Profile] 를 실시간으로 업데이트 및 모니터링할 수 있는 구성 요소를 소개합니다.

### 스트리밍 통합 및 스트리밍 세분화

실시간 입력은 스트리밍 습득 과정을 통해 가능합니다. 프로필 및 시간 시리즈 데이터가 수집되면 기존 데이터와 병합하고 조합 보기를 업데이트하기 전에 스트리밍 세그멘테이션이라는 진행 중인 프로세스를 통해 세그먼트에서 해당 데이터를 포함하거나 제외하기로 [!DNL Real-time Customer Profile] 자동으로 결정합니다. 그 결과 계산을 즉시 수행하고 고객이 브랜드와 상호 작용할 때 개인화된 향상된 경험을 고객에게 제공할 수 있습니다. 인제스트되는 동안 데이터도 데이터 수집이 제대로 수행되고 데이터 세트가 기반이 되는 스키마를 따르는지 확인하기 위해 유효성 검사를 받습니다. 수집 중 수행되는 유효성 검사에 대한 자세한 내용은 [데이터 수집 품질 개요를 읽어 보십시오](../ingestion/quality/overview.md).

### 가장자리 투영 구성 및 대상

여러 채널에서 실시간으로 고객의 기대에 부응하는 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 정확한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe Experience Platform은 가장자리라고 하는 요소를 사용하여 데이터에 대한 실시간 액세스를 가능하게 합니다. Edge는 데이터를 저장하고 애플리케이션에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 예를 들어, Adobe Target 및 Adobe Campaign과 같은 Adobe 애플리케이션은 실시간으로 개인화된 고객 경험을 제공하기 위해 가장자리를 사용합니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터가 전송될 가장자리를 정의하며, 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다. 자세한 내용을 살펴보고 [!DNL Real-time Customer Profile] API를 사용하여 투영 작업을 시작하려면 [가장자리 투영 끝점 안내서를 참조하십시오](api/edge-projections.md).

## 데이터 인제스트 [!DNL Profile]

[!DNL Platform] 실시간 스트리밍 수집 및 일괄 처리를 지원하여 기록 및 시간 시리즈 데이터 [!DNL Profile]를 전송하도록 구성할 수 있습니다. 자세한 내용은 실시간 고객 프로필에 데이터를 [추가하는 방법에 대한 개요를 설명하는 자습서를 참조하십시오](tutorials/add-profile-data.md).

>[!NOTE]
>
>Adobe 솔루션을 통해 수집된 데이터(예: [!DNL Analytics Cloud], [!DNL Marketing Cloud]및 [!DNL Advertising Cloud]포함) [!DNL Experience Platform] 는 유입되어 수집됩니다 [!DNL Profile].

### [!DNL Profile] 지표 수집

통찰력 통찰력을 통해 Adobe Experience Platform의 주요 지표를 표시할 수 있습니다. 다양한 기능에 대한 [!DNL Platform] 사용량 통계 및 성과 지표 외에도, [!DNL Platform] 들어오는 요청률, 성공률, 인제스트된 레코드 크기 등을 파악할 수 있는 특정 [!DNL Profile]관련 지표가 있습니다. 자세한 내용은 관찰성 통찰력 API 개요 [를](../observability/api/overview.md)읽고 전체 지표 목록을 보려면 [!DNL Profile] 사용 가능한 지표에 대한 설명서를 참조하십시오 [](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] 및 [!DNL Privacy]

[!DNL Data governance] 는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다.

데이터 액세스와 관련되기 때문에 데이터 거버넌스는 다양한 수준 [!DNL Experience Platform] 에서 핵심적인 역할을 합니다.
* 데이터 사용 레이블 지정
* 데이터 액세스 정책
* 마케팅 작업을 위한 데이터 액세스 제어

[!DNL Data governance] 여러 지점에서 관리됩니다. 이러한 데이터에는 어떤 데이터가 수집되는지 [!DNL Platform] 와 해당 마케팅 작업에 대해 수집 후 액세스할 수 있는 데이터가 포함되는지 결정하는 것이 포함됩니다. 자세한 내용은 [데이터 거버넌스 개요를 읽어 보십시오](../data-governance/home.md).

### 옵트아웃 및 데이터 개인 정보 요청 처리

[!DNL Experience Platform] 고객은 자신의 데이터 사용 및 저장과 관련된 옵트아웃 요청을 보낼 수 있습니다 [!DNL Real-time Customer Profile]. 옵트아웃 요청을 처리하는 방법에 대한 자세한 내용은 옵트아웃 요청을 [존중하는 방법을 참조하십시오](../segmentation/honoring-opt-outs.md).

## 다음 단계 및 추가 리소스

자세한 내용 [!DNL Real-time Customer Profile]을 살펴보려면 설명서를 계속 읽고 아래 비디오를 시청하거나 다른 [Experience Platform 비디오 자습서를 살펴봄으로써 학습 내용을 보완하십시오](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!WARNING]
>
>다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 [실시간 고객 프로필 사용 안내서를](ui/user-guide.md) 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)