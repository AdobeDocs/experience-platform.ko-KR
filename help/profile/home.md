---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로필 개요
topic: guide
translation-type: tm+mt
source-git-commit: e34b0b92a8fdf0986b10753d6c983b66dde42503
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 1%

---


# 실시간 고객 프로필 개요

Adobe Experience Platform을 사용하면 고객이 브랜드와 언제 어디에서나 고객의 기대에 부응하는 일관된 경험을 제공할 수 있습니다. 실시간 고객 프로파일을 이용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 다양한 채널의 데이터를 취합하는 각 개별 고객의 전체 상황을 파악할 수 있습니다. 프로필을 사용하면 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 고객 상호 작용에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다. 이 개요는 Experience Platform에서 실시간 고객 프로필의 역할 및 사용을 이해하는 데 도움이 됩니다.

## 실시간 고객 프로파일 이해

실시간 고객 프로필은 다양한 엔터프라이즈 데이터 자산의 데이터를 수집한 다음 개별 고객 프로필 및 관련 시간 시리즈 이벤트의 형태로 해당 데이터에 대한 액세스를 제공하는 범용 조회 엔티티 스토어입니다. 이 기능을 통해 마케터는 다양한 채널에서 고객과 연관성 있고 조율된 경험을 제공할 수 있습니다.

### 프로필 데이터 저장소

실시간 고객 프로필은 데이터를 수집하여 Adobe Experience Platform ID 서비스를 사용하여 ID 매핑을 통해 관련 데이터를 병합하지만 프로필 스토어에서 자체 데이터를 유지합니다. 즉, 프로필 저장소는 카탈로그 데이터(데이터 레이크) 및 ID 서비스 데이터(ID 그래프)와 별개입니다.

### 프로필 및 Platform 서비스

실시간 고객 프로필과 Experience Platform 내의 다른 서비스 간의 관계는 다음 다이어그램에서 강조됩니다.

![프로필 및 기타 Experience Platform 서비스 간의 관계.](images/profile-overview/profile-in-platform.png)

### 프로필 및 데이터 기록

프로필은 제목, 조직 또는 개인을 레코드 데이터라고 하는 표현입니다. 예를 들어 제품 프로필에는 SKU와 설명이 포함될 수 있지만 개인 프로필에는 이름, 성 및 이메일 주소와 같은 정보가 포함되어 있습니다. Experience Platform을 사용하여 비즈니스 관련 데이터 유형을 사용하도록 프로파일을 사용자 정의할 수 있습니다. 표준 XDM(Experience Data Model) 개별 프로필 클래스는 고객 레코드 데이터를 설명할 때 스키마를 작성하고 Platform 서비스 간의 여러 상호 작용에 데이터 필수 요소를 제공하는 기본 클래스입니다. Experience Platform에서 스키마 작업에 대한 자세한 내용은 [XDM 시스템 개요를 읽어 보십시오](../xdm/home.md).

### 시계열 이벤트

시간 시리즈 데이터는 작업이 대상에 의해 직접 또는 간접적으로 수행되는 시점에 시스템의 스냅숏과 이벤트 자체를 자세히 설명하는 데이터를 제공합니다. 표준 스키마 클래스 XDM ExperienceEvent로 표현되는 시간 시리즈 데이터는 장바구니에 추가되는 항목, 클릭되는 링크 및 본 비디오와 같은 이벤트를 설명할 수 있습니다. 시간 시리즈 데이터를 사용하여 세분화 규칙을 기반으로 할 수 있으며, 이벤트는 프로필 컨텍스트에서 개별적으로 액세스할 수 있습니다.

### ID

모든 비즈니스는 개인화된 방식으로 고객과 커뮤니케이션하기를 원합니다. 그러나 고객에게 연관성 있는 디지털 경험을 제공하려면 단절된 데이터를 서로 연결하는 방법을 이해하는 것이 중요합니다. 이러한 데이터는 일반적으로 태블릿, 휴대폰, 랩탑 등 다양한 디지털 채널에서 확산됩니다. ID 서비스를 사용하면 여러 채널의 ID를 연결하여 각 고객에 대한 ID 그래프를 만들어 고객의 전체 상황을 파악할 수 있습니다. 자세한 내용은 [ID 서비스 개요를](../identity-service/home.md) 참조하십시오.

### 세그먼테이션

Adobe Experience Platform 세그멘테이션 서비스는 개별 고객을 위한 경험을 제공하는 데 필요한 고객을 생성합니다. 대상 세그먼트가 만들어지면 해당 세그먼트의 ID가 모든 적격한 프로필에 대한 세그먼트 구성원 자격 목록에 추가됩니다. 세그먼트 규칙은 RESTful API 및 세그먼트 빌더 사용자 인터페이스를 사용하여 실시간 고객 프로필 데이터에 작성하고 적용됩니다. 세그멘테이션에 대한 자세한 내용은 세그멘테이션 [서비스 개요를 읽어 보십시오](../segmentation/home.md).

### 프로필 조각 및 결합 스키마 {#profile-fragments-and-union-schemas}

실시간 고객 프로필의 주요 기능 중 하나는 멀티채널 데이터를 통합하는 기능입니다. 실시간 고객 프로필을 사용하여 엔터티에 액세스하면 통합 보기라고 하며 조합 스키마로 알려진 것을 통해 가능한 데이터 세트에서 해당 엔터티에 대한 모든 프로필 조각에 대한 병합된 보기를 제공할 수 있습니다. 실시간 고객 프로필 데이터는 엔티티 또는 프로필의 ID로 액세스하거나 세그먼트로 내보낼 때 소스 간에 병합됩니다. 실시간 고객 프로필 API를 사용하여 프로필 및 조합 보기에 액세스하는 방법에 대한 자세한 내용은 [개체 끝점 안내서를 참조하십시오](api/entities.md).

### 정책 병합

여러 소스에서 데이터를 취합하여 각 개별 고객의 전체 상황을 파악하기 위해 취합하는 경우 병합 정책은 Platform이 데이터의 우선 순위를 매기는 방식과 데이터를 결합해 통합 뷰를 생성하는 데 사용하는 규칙입니다. RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 실시간 고객 프로필 API를 사용한 병합 정책 작업에 대한 자세한 내용은 [병합 정책 끝점 안내서를 참조하십시오](api/merge-policies.md). Experience Platform UI를 사용하여 병합 정책을 사용하려면 [병합 정책 사용 안내서를 참조하십시오](ui/merge-policies.md).

## (알파) 계산된 속성 구성

>[!IMPORTANT]
>이 문서에 요약된 계산된 속성 기능은 alpha입니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 프로필 수준에서 작동합니다. 즉, 모든 레코드와 이벤트에 대한 값을 합산할 수 있습니다. 계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성이나 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 시간 또는 애플리케이션 열기 횟수와 같은 문제와 관련된 질문에 쉽게 응답할 수 있습니다. 계산된 속성에 대한 자세한 내용과 실시간 고객 프로필 API를 사용한 작업에 대한 단계별 지침을 보려면 [계산된 속성 끝점 안내서를 참조하십시오](api/computed-attributes.md). 이 안내서는 Adobe Experience Platform 내에서 작동하는 역할 계산 속성을 더 잘 이해하는 데 도움이 되며 기본 CRUD 작업을 수행하기 위한 샘플 API 호출을 포함합니다.

## 실시간 구성 요소

이 섹션에서는 실시간 고객 프로파일을 통해 기록 및 시간 시리즈 데이터를 실시간으로 업데이트 및 모니터링할 수 있는 구성 요소를 소개합니다.

### 스트리밍 통합 및 스트리밍 세분화

실시간 입력은 스트리밍 습득 과정을 통해 가능합니다. 프로필 및 시간 시리즈 데이터가 수집되면 실시간 고객 프로필은 기존 데이터와 병합하고 조합 뷰를 업데이트하기 전에 스트리밍 세그먼테이션이라는 진행 중인 프로세스를 통해 해당 데이터를 세그먼트에서 포함하거나 제외하기로 자동으로 결정합니다. 그 결과 계산을 즉시 수행하고 고객이 브랜드와 상호 작용할 때 개인화된 향상된 경험을 고객에게 제공할 수 있습니다. 인제스트되는 동안 데이터도 데이터 수집이 제대로 수행되고 데이터 세트가 기반이 되는 스키마를 따르는지 확인하기 위해 유효성 검사를 받습니다. 수집 중 수행되는 유효성 검사에 대한 자세한 내용은 [데이터 수집 품질 개요를 읽어 보십시오](../ingestion/quality/overview.md).

### 가장자리 투영 구성 및 대상

여러 채널에서 실시간으로 고객의 기대에 부응하는 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 정확한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe Experience Platform을 사용하면 가장자리라고 하는 요소를 사용하여 데이터에 대한 실시간 액세스를 가능하게 합니다. Edge는 데이터를 저장하고 애플리케이션에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 예를 들어 Adobe Target 및 Adobe Campaign과 같은 Adobe 애플리케이션은 실시간으로 개인화된 고객 경험을 제공하기 위해 가장자리를 사용합니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터가 전송될 가장자리를 정의하며, 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다. 실시간 고객 프로필 API를 사용하여 자세한 내용을 살펴보고 예측 작업을 시작하려면 [가장자리 투영 엔드포인트 가이드를 참조하십시오](api/edge-projections.md).

## 실시간 고객 프로필에 데이터 추가

실시간 스트리밍 수집 및 일괄 처리 수거를 지원하여 기록 및 시간 시리즈 데이터를 프로필에 보내도록 Platform을 구성할 수 있습니다. 자세한 내용은 실시간 고객 프로필에 데이터를 [추가하는 방법에 대한 개요를 설명하는 자습서를 참조하십시오](tutorials/add-profile-data.md).

>[!N참고]
>Analytics Cloud, Marketing Cloud, Advertising Cloud을 비롯한 Adobe 솔루션을 통해 수집된 데이터는 Experience Platform으로 플로우되어 프로필에 수집됩니다.

### 프로필 스트리밍 통합 지표

통찰력 통찰력을 사용하면 Adobe Experience Platform에서 주요 지표를 표시할 수 있습니다. 다양한 Platform 기능에 대한 Platform 사용량 통계 및 성과 지표 외에도, 들어오는 요청률, 성공적인 통합률, 인제스트된 기록 크기 등에 대한 통찰력을 얻을 수 있도록 해주는 특정 프로필 관련 지표가 있습니다. 자세한 내용은 관찰성 통찰력 개요 [를](../observability/home.md)읽고, 전체 프로필 지표 목록을 보려면 [사용 가능한 지표에 대한 설명서를 참조하십시오](../observability/metrics.md).

## 데이터 거버넌스 및 개인 정보

데이터 거버넌스는 고객 데이터를 관리하고 데이터 사용에 적용되는 규정, 제한 사항 및 정책을 준수하는 데 사용되는 일련의 전략과 기술입니다.

데이터 액세스와 관련되기 때문에 데이터 거버넌스는 다양한 수준에서 Experience Platform 내에서 중요한 역할을 합니다.
* 데이터 사용 레이블 지정
* 데이터 액세스 정책
* 마케팅 작업을 위한 데이터 액세스 제어

데이터 거버넌스는 여러 지점에서 관리합니다. 이러한 데이터에는 Platform에 수집되는 데이터와 해당 마케팅 작업에 대해 수집 후 액세스할 수 있는 데이터를 결정하는 것이 포함됩니다. 자세한 내용은 [데이터 거버넌스 개요를 읽어 보십시오](../data-governance/home.md).

### 옵트아웃 및 데이터 개인 정보 요청 처리

Experience Platform을 통해 고객은 실시간 고객 프로필 내에서 데이터의 사용 및 저장과 관련된 옵트아웃 요청을 보낼 수 있습니다. 옵트아웃 요청을 처리하는 방법에 대한 자세한 내용은 옵트아웃 요청을 [존중하는 방법을 참조하십시오](../segmentation/honoring-opt-outs.md).

## 프로필 지침

Experience Platform에는 프로필을 효과적으로 사용하기 위해 따라야 할 일련의 지침이 있습니다.

| 섹션 | 경계 |
| ------- | -------- |
| 프로필 결합 스키마 | 최대 **20** 개의 데이터 세트가 프로필 결합 스키마에 기여할 수 있습니다. |
| 다중 엔티티 관계 | 최대 **5개의** 다중 엔티티 관계를 만들 수 있습니다. |
| 다중 엔티티 연결을 위한 JSON 깊이 | 최대 JSON 깊이는 **4입니다**. |
| 시계열 데이터 | 비인물 엔티티의 경우 프로필에서 시간 시리즈 데이터를 사용할 **수 없습니다** . |
| 비사용자 스키마 관계 | 사람들이 아닌 스키마 관계는 허용되지 **않습니다** . |
| 프로필 조각 | 프로필 조각의 권장 최대 크기는 **10kB입니다**.<br><br> 프로필 조각의 절대 최대 크기는 **1MB입니다**. |
| 비개인 엔티티 | 개인이 아닌 단일 엔티티의 최대 총 크기는 **200MB입니다**. |
| 개인 엔터티당 데이터 집합 | 개인이 아닌 엔터티에 최대 **1** 개의 데이터 세트를 연결할 수 있습니다. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>개인이 아닌 엔터티는 프로필의 일부가 **아닌** 모든 XDM 클래스를 참조합니다.

## 다음 단계 및 추가 리소스

실시간 고객 프로파일에 대한 자세한 내용을 살펴보려면 설명서를 계속 읽고 아래 비디오를 시청하거나 다른 [Experience Platform 비디오 자습서를 통해 학습 내용을 보완하십시오](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html).

>[!WARNING]
>다음 비디오에 표시된 Platform UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 [실시간 고객 프로필 사용 안내서를](ui/user-guide.md) 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)