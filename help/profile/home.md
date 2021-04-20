---
keywords: Experience Platform;프로파일;실시간 고객 프로파일;문제 해결;API;통합 프로파일;통합 프로파일;프로파일;rtcp;XDM 그래프
title: 실시간 고객 프로필 개요
topic: guide
description: 실시간 고객 프로필은 다양한 엔터프라이즈 데이터 자산의 데이터를 병합한 다음 개별 고객 프로필 및 관련 시간 시리즈 이벤트의 형태로 해당 데이터에 대한 액세스를 제공하는 범용 조회 엔티티 스토어입니다. 이 기능을 통해 마케터는 다양한 채널에서 고객과 연관성 높은 경험을 일관되게 제작할 수 있습니다.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile]개요

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소 또는 시기와 상관없이 고객의 관심사와 연관성 있는 경험을 일관되게 전달할 수 있습니다. [!DNL Real-time Customer Profile]을 사용하면 온라인, 오프라인, CRM 및 제3자 등 다양한 채널의 데이터를 취합하여 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Profile] 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다. 이 개요는 [!DNL Experience Platform]에서 [!DNL Real-time Customer Profile]의 역할과 사용 방법을 이해하는 데 도움이 됩니다.

## [!DNL Profile] Experience Platform

실시간 고객 프로필과 Experience Platform 내의 다른 서비스 간의 관계는 다음 다이어그램에서 강조됩니다.

![](images/profile-overview/profile-in-platform.png)

## 프로파일 이해

[!DNL Real-time Customer Profile] 다양한 엔터프라이즈 시스템의 데이터를 수집한 다음 고객 프로파일 형태로 해당 데이터에 대한 액세스를 관련 시계열 이벤트와 함께 제공합니다. 이 기능을 통해 마케터는 다양한 채널에서 고객과 연관성 높은 경험을 일관되게 제작할 수 있습니다. 다음 섹션에서는 플랫폼 내에서 프로파일을 효과적으로 구축하고 유지 관리하기 위해 이해해야 하는 핵심 개념 중 일부를 집중적으로 설명합니다.

### 프로필 데이터 저장소

[!DNL Real-time Customer Profile]은(는) 인제스트된 데이터를 처리하고 Adobe Experience Platform [!DNL Identity Service]을 사용하여 ID 매핑을 통해 관련 데이터를 병합하지만 [!DNL Profile] 데이터 저장소에 자체 데이터를 유지합니다. [!DNL Profile] 스토어는 데이터 레이크의 카탈로그 데이터와 ID 그래프의 [!DNL Identity Service] 데이터와 별개입니다.

프로필 저장소는 Microsoft Azure Cosmos DB 인프라를 사용하고 플랫폼 데이터 레이크는 Microsoft Azure Data Lake 저장소를 사용합니다.

### 프로필 가드레일

Experience Platform은 실시간 고객 프로필에서 지원할 수 없는 [XDM(Experience Data Model) 스키마](../xdm/home.md)을(를) 만들지 않도록 하는 데 도움이 되는 일련의 지침을 제공합니다. 여기에는 성능 저하를 초래할 수 있는 소프트 한도 뿐만 아니라 오류 및 시스템 중단으로 이어질 수 있는 하드 제한이 포함됩니다. 지침 목록 및 예제 사용 사례 등 자세한 내용은 [프로필 가드레일](guardrails.md) 설명서를 참조하십시오.

### (베타) 프로필 대시보드 {#profile-dashboard}

>[!IMPORTANT]
>
>대시보드 기능은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

Experience Platform UI는 일일 스냅샷 중에 캡처되는 실시간 고객 프로필 데이터에 대한 중요한 정보를 볼 수 있는 대시보드를 제공합니다. UI에서 [!DNL Profile] 대시보드에 액세스하고 작업하는 방법, 대시보드에 표시되는 지표에 대한 자세한 정보는 [프로필 대시보드 UI 안내서](ui/profile-dashboard.md)를 참조하십시오.

### 프로필 조각과 병합된 프로필 {#profile-fragments-vs-merged-profiles} 비교

각 개별 고객 프로필은 여러 프로필 조각으로 구성되며, 병합되어 해당 고객에 대한 단일 보기를 형성합니다. 예를 들어 고객이 여러 채널에서 브랜드와 상호 작용하는 경우 조직은 여러 데이터 세트에 나타나는 해당 단일 고객과 관련된 여러 프로필 조각을 갖게 됩니다. 이러한 조각을 Platform(플랫폼)으로 인제스트하면 해당 고객에 대한 단일 프로파일을 만들기 위해 병합됩니다.

여러 소스의 데이터가 충돌하면(예: 한 조각은 고객을 &quot;single&quot;로 나열하고 다른 조각은 고객을 &quot;기혼&quot;으로 나열합니다) [병합 정책](#merge-policies)은 개인에게 우선 순위를 지정하고 프로파일에 포함할 정보를 결정합니다. 따라서 각 프로파일이 여러 조각으로 구성되므로 플랫폼 내에서 총 프로필 조각 수는 항상 병합된 프로필의 총 수보다 클 수 있습니다.

### 데이터 기록

프로파일은 여러 속성(레코드 데이터라고도 함)으로 구성된 주제, 조직 또는 개인을 표현합니다. 예를 들어 제품 프로필에는 SKU와 설명이 포함될 수 있지만 개인 프로필에는 이름, 성 및 이메일 주소와 같은 정보가 포함되어 있습니다. [!DNL Experience Platform]을 사용하여 비즈니스와 관련된 특정 데이터를 사용하도록 프로파일을 사용자 정의할 수 있습니다. 표준 [!DNL Experience Data Model](XDM) 클래스 [!DNL XDM Individual Profile]는 고객 레코드 데이터를 설명할 때 스키마를 빌드하고 플랫폼 서비스 간 많은 상호 작용에 데이터 무결성을 제공하는 기본 클래스입니다. [!DNL Experience Platform]의 스키마 작업에 대한 자세한 내용은 [XDM 시스템 개요](../xdm/home.md)를 읽으십시오.

### 시간 시리즈 이벤트

시간 시리즈 데이터는 작업이 대상에 의해 직접 또는 간접적으로 수행될 때의 시스템 스냅숏과 이벤트 자체를 자세히 설명하는 데이터를 제공합니다. 표준 스키마 클래스 XDM ExperienceEvent로 표현되는 시간 시리즈 데이터는 장바구니에 추가되는 항목, 클릭되는 링크 및 본 비디오와 같은 이벤트를 설명할 수 있습니다. 시간 시리즈 데이터를 사용하여 세분화 규칙을 기반으로 할 수 있으며, 이벤트는 프로필의 컨텍스트에서 개별적으로 액세스할 수 있습니다.

### ID

모든 비즈니스는 고객의 기대에 부응하는 개인화된 커뮤니케이션을 원합니다. 그러나 고객에게 연관성 있는 디지털 경험을 제공하는 데 있어 여러 가지 문제 중 하나는 단절된 데이터를 서로 연결하는 방법을 이해하는 것입니다. 이러한 데이터는 일반적으로 태블릿, 휴대폰 및 노트북과 같은 다양한 디지털 채널에 분산되어 있습니다. [!DNL Identity Service] 여러 채널의 ID를 연결하고 각 고객에 대한 ID 그래프를 만들어 고객의 전체 상황을 파악할 수 있습니다. 자세한 내용은 [ID 서비스 개요](../identity-service/home.md)를 참조하십시오.

### 정책 병합

여러 소스에서 데이터 조각을 취합하여 각 개별 고객의 전체 보기를 확인하기 위해 결합할 때, 병합 정책은 데이터 우선 순위를 지정하는 방법과 고객 프로파일을 만드는 데 사용할 데이터를 결정하는 데 사용하는 규칙입니다. [!DNL Platform] 여러 데이터 세트에서 데이터가 충돌하는 경우 병합 정책에 따라 데이터가 어떻게 처리되어야 하는지, 어떤 값을 사용해야 하는지를 결정합니다. RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다.

[!DNL Real-time Customer Profile] API를 사용하여 병합 정책을 사용하는 방법에 대한 자세한 내용은 [병합 정책 끝점 안내서](api/merge-policies.md)를 참조하십시오. [!DNL Experience Platform] UI를 사용하여 병합 정책을 사용하려면 [정책 병합 UI 안내서](ui/merge-policies.md)를 참조하십시오.

### 공용 스키마 {#profile-fragments-and-union-schemas}

[!DNL Real-time Customer Profile]의 주요 기능 중 하나는 다중 채널 데이터를 통합하는 기능입니다. [!DNL Real-time Customer Profile]을(를) 사용하여 엔터티에 액세스하면 &quot;조합 보기&quot;라고 하며 조합 스키마로 알려진 것을 통해 데이터 세트에서 해당 엔티티에 대한 모든 프로필 조각에 대한 병합된 보기를 제공할 수 있습니다.

UI에서 결합 스키마에 액세스하는 방법을 포함한 결합 스키마에 대한 자세한 내용은 [공용 스키마 UI 안내서](ui/union-schema.md)를 참조하십시오.

### (알파) 계산된 속성

>[!IMPORTANT]
>
>계산된 특성 기능은 알파에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세분화, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 간 시간 또는 애플리케이션 열기 횟수와 같은 것과 관련된 질문에 쉽게 답변할 수 있습니다. Adobe Experience Platform 내에서 작동하는 역할 계산 속성을 이해하는 것을 비롯하여 계산된 속성에 대한 자세한 내용은 [계산된 속성 개요](computed-attributes/overview.md)를 읽으십시오.

## 프로필 및 세그먼트

Adobe Experience Platform [!DNL Segmentation Service]은(는) 개별 고객의 경험을 향상시키는 데 필요한 고객을 생성합니다. 대상 세그먼트가 만들어지면 해당 세그먼트의 ID가 모든 자격 프로필의 세그먼트 구성원 목록에 추가됩니다. 세그먼트 규칙은 RESTful API 및 세그먼트 빌더 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile] 데이터에 작성 및 적용됩니다. 세그멘테이션에 대한 자세한 내용은 [세그멘테이션 서비스 개요](../segmentation/home.md)를 읽으십시오.

### 스트리밍 통합 및 스트리밍 세분화

실시간 입력은 스트리밍 습제스트라는 프로세스를 통해 가능합니다. 프로필 및 시간 시리즈 데이터를 인제스트할 때, [!DNL Real-time Customer Profile]은 기존 데이터와 병합하고 조합 뷰를 업데이트하기 전에 스트리밍 세그먼테이션이라는 진행 중인 프로세스를 통해 세그먼트에서 해당 데이터를 포함하거나 제외하기로 자동으로 결정합니다. 그 결과, 계산을 즉시 수행하고 고객이 브랜드와 상호 작용할 때 개인화된 향상된 경험을 고객에게 제공하는 결정을 내릴 수 있습니다. 인제스트하는 동안 데이터도 제대로 인제스트되고 데이터 세트가 기반이 되는 스키마를 따르기 위해 유효성 검사를 수행합니다. 수집 중 유효성 검사가 수행되는 작업에 대한 자세한 내용은 [데이터 통합 품질 개요](../ingestion/quality/overview.md)를 읽으십시오.

## 가장자리 예상

여러 채널에서 실시간으로 고객에게 일관되고 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 적합한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe Experience Platform을 사용하면 가장자리라고 하는 요소를 사용하여 데이터에 실시간으로 액세스할 수 있습니다. Edge는 데이터를 저장하고 응용 프로그램에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 예를 들어 Adobe Target 및 Adobe Campaign과 같은 Adobe 애플리케이션은 실시간으로 개인화된 고객 경험을 제공하기 위해 가장자리를 사용합니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터를 보낼 가장자리를 정의하고 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다. 자세한 내용을 살펴보고 [!DNL Real-time Customer Profile] API를 사용하여 투영 작업을 시작하려면 [가장자리 투영 끝점 안내서](api/edge-projections.md)를 참조하십시오.

## 데이터를 [!DNL Profile]에 인제스트

[!DNL Platform] 기록 및 시간 시리즈 데이터를 전송하도록 구성할 수 있으므로 실시간 스트리밍  [!DNL Profile]통합 및 일괄 처리를 지원합니다. 자세한 내용은 [실시간 고객 프로필에 데이터를 추가하는 방법에 대한 개요를 설명하는 자습서](tutorials/add-profile-data.md)를 참조하십시오.

>[!NOTE]
>
>[!DNL Analytics Cloud], [!DNL Marketing Cloud] 및 [!DNL Advertising Cloud]를 비롯한 Adobe 솔루션을 통해 수집된 데이터는 [!DNL Experience Platform]로 플로우되어 [!DNL Profile]로 인제스트됩니다.

### 프로필 수집 지표

통찰력 통찰력을 통해 Adobe Experience Platform에서 주요 지표를 표시할 수 있습니다. 다양한 [!DNL Platform] 기능에 대한 사용 통계 및 성과 지표 외에도, 들어오는 요청률, 성공적인 통합률, 인제스트된 기록 크기 등에 대한 통찰력을 얻을 수 있도록 해주는 특정 프로필 관련 지표가 있습니다. [!DNL Experience Platform] 자세한 내용은 [Observability Insights API 개요](../observability/api/overview.md)를 읽고, 실시간 고객 프로필 지표의 전체 목록을 보려면 [사용 가능한 지표](../observability/api/metrics.md#available-metrics)에 대한 설명서를 참조하십시오.

## [!DNL Data governance] 및 [!DNL Privacy]

[!DNL Data governance] 는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다.

데이터 액세스와 관련되므로 데이터 거버넌스는 다양한 수준에서 [!DNL Experience Platform] 내에서 주요 역할을 합니다.
* 데이터 사용 레이블 지정
* 데이터 액세스 정책
* 마케팅 작업을 위한 데이터에 대한 액세스 제어

[!DNL Data governance] 는 여러 지점에서 관리됩니다. 여기에는 [!DNL Platform]에 수집할 데이터와 지정된 마케팅 작업에 대해 수집 후 액세스할 수 있는 데이터를 결정하는 것이 포함됩니다. 자세한 내용은 [데이터 거버넌스 개요](../data-governance/home.md)를 읽으십시오.

### 옵트아웃 및 데이터 개인 정보 보호 요청 처리

[!DNL Experience Platform] 고객은 자신의 데이터 사용 및 저장과 관련된 옵트아웃 요청을 보낼 수 있습니다 [!DNL Real-time Customer Profile]. 옵트아웃 요청을 처리하는 방법에 대한 자세한 내용은 [수신 거부 요청](../segmentation/honoring-opt-outs.md)에 대한 설명서를 참조하십시오.

## 다음 단계 및 추가 리소스

Experience Platform UI 또는 프로필 API를 사용하여 [!DNL Real-time Customer Profile] 데이터를 사용하여 작업하는 방법에 대한 자세한 내용은 각각 [프로필 UI 안내서](ui/user-guide.md) 또는 [API 개발자 안내서](api/overview.md)를 읽으십시오.