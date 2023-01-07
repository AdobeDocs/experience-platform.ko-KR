---
keywords: Experience Platform;홈;인기 항목;CJA;여정 분석;고객 여정 분석;캠페인 오케스트레이션;오케스트레이션;고객 여정;여정;여정 오케스트레이션;기능;영역
title: Adobe Experience Platform 종단 간 예제 워크플로우
description: 높은 수준에서 Adobe Experience Platform을 위한 기본 종단 간 워크플로우를 학습합니다.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Adobe Experience Platform 종단 간 예제 워크플로우

Adobe Experience Platform은 고객 경험을 이끄는 완벽한 솔루션을 구축하고 관리할 수 있는 시장에서 가장 강력하고 유연하며 개방적인 시스템입니다. Platform을 사용하면 조직 내 모든 시스템의 고객 데이터와 컨텐츠를 중앙 집중화 및 표준화하고 데이터 과학 및 시스템 학습을 적용하여 풍부한 개인별 경험을 더 잘 설계하고 전달할 수 있습니다.

RESTful API를 기반으로 구축된 Platform은 친숙한 도구를 사용하여 엔터프라이즈 솔루션을 쉽게 통합할 수 있도록 시스템의 전체 기능을 개발자에게 제공합니다. Platform을 사용하면 고객 데이터를 섭취하고 타겟팅하려는 대상으로 데이터를 세그먼트화하고 이러한 대상을 외부 대상으로 활성화하여 고객의 전체적인 보기를 도출할 수 있습니다. 다음 자습서에서는 소스를 통해 수집에서 대상을 통한 대상 활성화까지 모든 단계를 표시하는 종단 간 워크플로우를 보여줍니다.

![엔드 투 엔드 워크플로우 Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 시작하기

이 종단간 워크플로우는 여러 Adobe Experience Platform 서비스를 사용합니다. 다음은 이 워크플로우에서 개요 링크와 함께 사용되는 서비스 목록입니다.

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): 표준화된 프레임워크 [!DNL Platform] 고객 경험 데이터를 구성합니다. 세그멘테이션을 가장 잘 사용하려면 데이터가 [데이터 모델링 우수 사례](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): 장치 및 시스템 전반에서 ID를 브리징하여 고객 및 고객의 행동에 대한 포괄적인 보기를 제공합니다.
- [소스](../sources/home.md): [!DNL Experience Platform] 을(를) 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다. [!DNL Platform] 서비스.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] 에 저장된 데이터를 나눌 수 있습니다. [!DNL Experience Platform] 개인(예: 고객, 잠재 고객, 사용자 또는 조직)과 관련이 있습니다.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [데이터 세트](../catalog/datasets/overview.md): 의 데이터 지속성을 위한 스토리지 및 관리 구성 [!DNL Experience Platform].
- [대상](../destinations/home.md): 대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 플랫폼에서 데이터를 원활하게 활성화할 수 있도록 일반적으로 사용되는 애플리케이션과의 사전 구축된 통합입니다.

## XDM 스키마 만들기

데이터를 Platform에 수집하려면 먼저 해당 데이터의 구조를 설명하는 XDM 스키마를 만들어야 합니다. 다음 단계에서 데이터를 수집하면 들어오는 데이터를 이 스키마에 매핑합니다. 예제 XDM 스키마를 만드는 방법에 대해 알아보려면 [스키마 편집기를 사용하여 스키마 만들기](../xdm/tutorials/create-schema-ui.md).

위의 자습서에서는 스키마에 대한 ID 필드를 설정하는 방법을 보여줍니다. ID 필드는 레코드 또는 시계열 이벤트와 관련된 개별 개인을 식별하는 데 사용할 수 있는 필드를 나타냅니다. ID 필드는 고객 ID 그래프가 플랫폼에서 구성되는 방식을 결정하는데 중요한 구성 요소로서, 실시간 고객 프로필에서 서로 다른 데이터 조각을 병합하여 고객을 완전히 파악합니다. Platform에서 ID 그래프를 보는 방법에 대한 자세한 내용은 [id 그래프 뷰어 사용 방법](../identity-service/ui/identity-graph-viewer.md).

스키마를 기반으로 하여 데이터에서 고객 프로필을 생성할 수 있도록 실시간 고객 프로필에서 사용할 스키마를 활성화해야 합니다. 의 섹션을 참조하십시오. [프로필에 대한 스키마 활성화](../xdm/ui/resources/schemas.md#profile) 스키마 UI 안내서에서 자세한 내용을 확인하십시오.

## Platform에 데이터 수집

XDM 스키마를 만들면 데이터를 시스템에 가져올 수 있습니다.

Platform으로 가져온 모든 데이터는 수집 시 개별 데이터 세트에 저장됩니다. 데이터 집합은 특정 XDM 스키마에 매핑되는 데이터 레코드의 컬렉션입니다. 에서 데이터를 사용하기 전에 [!DNL Real-Time Customer Profile]로 지정하는 경우 해당 데이터 세트를 명시적으로 구성해야 합니다. 프로필에 데이터 세트를 활성화하는 방법에 대한 전체 지침은 [데이터 세트 UI 안내서](../catalog/datasets/user-guide.md#enable-profile) 그리고 [데이터 집합 구성 API 자습서](../profile/tutorials/dataset-configuration.md). 데이터 세트가 구성되면 데이터 집합에 데이터 수집을 시작할 수 있습니다.

플랫폼을 사용하면 플랫폼 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 저장소, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다. 예를 들어 [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). 사용 가능한 소스의 전체 목록은 [소스 커넥터 개요](../sources/home.md).

Amazon S3를 소스 커넥터로 사용하는 경우 의 API 자습서에 있는 지침을 따를 수 있습니다 [Amazon S3 커넥터 만들기](../sources/tutorials/api/create/cloud-storage/s3.md) 또는 의 UI 자습서 [Amazon S3 커넥터 만들기](../sources/tutorials/ui/create/cloud-storage/s3.md) 커넥터 내에서 데이터를 작성, 연결 및 수집하는 방법을 알아봅니다.

소스 커넥터에 대한 자세한 지침은 [소스 커넥터 개요](../sources/home.md). 소스 기반 API인 플로우 서비스에 대해 자세히 알아보려면 [Flow Service API 참조](https://www.adobe.io/experience-platform-apis/references/flow-service/).

소스 커넥터를 통해 Platform으로 데이터를 가져오고 프로필 지원 데이터 세트에 저장하면 XDM 스키마에서 구성한 ID 데이터를 기반으로 고객 프로필이 자동으로 생성됩니다.

데이터를 새 데이터 세트에 처음 업로드하거나 새 ETL 프로세스 또는 데이터 소스를 설정할 때 데이터가 올바르게 업로드되고 생성된 프로필에 예상하는 데이터가 포함되도록 데이터를 신중하게 확인하는 것이 좋습니다. 플랫폼 UI에서 고객 프로필에 액세스하는 방법에 대한 자세한 내용은 [실시간 고객 프로필 UI 안내서](../profile/ui/user-guide.md). 실시간 고객 프로필 API를 사용하여 프로필에 액세스하는 방법에 대한 자세한 내용은 [엔티티 끝점 사용](../profile/api/entities.md).

## 데이터 평가

수집된 데이터에서 프로필을 성공적으로 생성했으면 세그멘테이션을 사용하여 데이터를 평가할 수 있습니다. 세그먼테이션은 마케팅 가능한 사람 그룹을 고객 기반과 구분하기 위해 개인 하위 집합에 의해 공유되는 특정 속성 또는 행동을 프로필 스토어와 정의하는 프로세스입니다. 세그멘테이션에 대해 자세히 알아보려면 [세분화 서비스 개요](../segmentation/home.md).

### 세그먼트 정의 만들기

시작하려면 고객을 클러스터링하는 세그먼트 정의를 만들어 타겟 대상자를 만들어야 합니다. 세그먼트 정의는 타깃팅할 대상을 정의하는 데 사용할 수 있는 규칙 모음입니다. 세그먼트 정의를 만들려면 [세그먼트 빌더](../segmentation/ui/segment-builder.md) 또는 [세그먼트 만들기](../segmentation/tutorials/create-a-segment.md).

세그먼트 정의를 만들었으면 세그먼트 정의 ID를 계속 기록해야 합니다.

### 세그먼트 정의 평가

세그먼트 정의를 만든 후 세그먼트 작업을 만들어 세그먼트를 일회성 인스턴스로 평가하거나 세그먼트를 지속적으로 평가하기 위한 일정을 만들 수 있습니다.

수요에 따라 세그먼트 정의를 평가하기 위해 세그먼트 작업을 만들 수 있습니다. 세그먼트 작업은 참조된 세그먼트 정의 및 병합 정책을 기반으로 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 병합 정책은 Platform이 고객 프로필을 만드는 데 사용할 데이터를 결정하는 데 사용하는 규칙 집합이며, 소스 간에 불일치가 있을 때 우선 순위가 지정되는 데이터입니다. 병합 정책을 사용하는 방법을 알아보려면 [병합 정책 UI 안내서](../profile/merge-policies/ui-guide.md).

세그먼트 작업을 만들고 평가하면, 대상 크기나 처리 중에 발생했을 수 있는 오류와 같은 세그먼트 관련 정보를 얻을 수 있습니다. 제공해야 하는 모든 세부 사항을 포함하여 세그먼트 작업을 만드는 방법을 알아보려면 [세그먼트 작업 개발자 안내서](../segmentation/api/segment-jobs.md).

지속적인 기준으로 세그먼트 정의를 평가하기 위해 예약을 만들고 활성화할 수 있습니다. 예약은 지정된 시간에 하루에 한 번 세그먼트 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. 예약을 생성 및 활성화하는 방법에 대해 알아보려면 [끝점 예약](../segmentation/api/schedules.md).

## 평가된 데이터 내보내기

1회 세그먼트 작업 또는 진행 중인 일정을 만든 후 세그먼트 내보내기 작업을 만들어 결과를 데이터 세트에 내보내거나 결과를 대상으로 내보낼 수 있습니다. 다음 섹션에서는 이 두 선택 사항에 대한 지침을 제공합니다.

### 평가된 데이터를 데이터 세트로 내보내기

일회성 세그먼트 작업 또는 진행 중인 일정을 만든 후 세그먼트 내보내기 작업을 만들어 결과를 내보낼 수 있습니다. 세그먼트 내보내기 작업은 평가된 대상에 대한 정보를 데이터 집합에 전송하는 비동기 작업입니다.

내보내기 작업을 만들기 전에 먼저 데이터를 내보낼 데이터 세트를 만들어야 합니다. 데이터 세트를 만드는 방법에 대해 알아보려면 [대상 데이터 세트 만들기](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) 세그먼트 평가에 대한 자습서에서 를 만든 후 데이터 세트 ID를 기록하도록 합니다. 데이터 세트를 만든 후 내보내기 작업을 만들 수 있습니다. 내보내기 작업을 만드는 방법에 대해 알아보려면 [작업 끝점 내보내기](../segmentation/api/export-jobs.md).

### 평가된 데이터를 대상으로 내보내기

또는 일회성 세그먼트 작업 또는 진행 중인 일정을 만든 후 결과를 대상으로 내보낼 수 있습니다. 대상은 대상을 활성화 및 전달할 수 있는 외부 서비스의 Adobe 애플리케이션과 같은 종단점입니다. 사용 가능한 대상 전체 목록은 [대상 카탈로그](../destinations/catalog/overview.md).

데이터를 일괄 처리 또는 이메일 마케팅 대상으로 활성화하는 방법에 대한 지침은 [플랫폼 UI를 사용하여 대상자 데이터를 묶음 프로필 내보내기 대상으로 활성화하는 방법](../destinations/ui/activate-batch-profile-destinations.md) 그리고 [흐름 서비스 API를 사용하여 배치 대상에 연결하고 데이터를 활성화하는 방법에 대한 안내서](../destinations/api/connect-activate-batch-destinations.md).

## 플랫폼 데이터 활동 모니터링

플랫폼 을 사용하면 데이터 흐름의 사용을 통해 데이터가 처리되는 방식을 추적할 수 있습니다. 데이터 흐름은 플랫폼의 다양한 구성 요소 간에 데이터를 이동하는 작업을 나타냅니다. 이러한 데이터 흐름은 다양한 서비스에 걸쳐 구성되어 있으므로, 소스 커넥터에서 대상 데이터 세트로 데이터를 이동한 다음 이 데이터 흐름을 사용 [!DNL Identity Service] 및 [!DNL Real-Time Customer Profile] 궁극적으로 대상에 활성화하기 전에. 모니터링 대시보드는 데이터 흐름 여정을 시각적으로 나타냅니다. Platform UI 내에서 데이터 흐름을 모니터링하는 방법에 대해 알아보려면 [소스에 대한 데이터 흐름 모니터링](../dataflows/ui/monitor-sources.md) 및 [대상에 대한 데이터 흐름 모니터링](../dataflows/ui/monitor-destinations.md).

를 사용하여 통계 지표 및 이벤트 알림을 사용하여 플랫폼 활동을 모니터링할 수도 있습니다 [!DNL Observability Insights]. 플랫폼 UI를 통해 경고 알림에 가입하거나 구성된 웹 후크에 보낼 수 있습니다. Experience Platform UI에서 사용 가능한 경고를 보고, 활성화, 비활성화 및 구독하는 방법에 대한 자세한 내용은 [[!UICONTROL 경고] UI 안내서](../observability/alerts/ui.md). 웹 후크를 통해 경고를 받는 방법에 대한 자세한 내용은 다음 안내서를 참조하십시오 [이벤트 알림 Adobe I/O](../observability/alerts/subscribe.md).

## 다음 단계

이 자습서를 읽음으로써 Platform에 대한 간단한 종단 간 흐름에 대한 기본적인 소개가 제공되었습니다. Adobe Experience Platform에 대한 자세한 내용은 [플랫폼 개요](./home.md). Platform UI 및 Platform API 사용에 대한 자세한 내용은 [플랫폼 UI 안내서](./ui-guide.md) 그리고 [플랫폼 API 안내서](./api-guide.md) 각각 사용할 수 있습니다.
