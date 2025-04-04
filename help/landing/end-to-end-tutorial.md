---
keywords: Experience Platform;홈;인기 항목;CJA;여정 분석;고객 여정 분석;campaign orchestration;오케스트레이션;고객 여정;여정;여정 오케스트레이션;기능;지역
title: Adobe Experience Platform 전체 예제 워크플로
description: Adobe Experience Platform의 기본 종단 간 워크플로를 높은 수준에서 알아봅니다.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 1%

---

# Adobe Experience Platform 전체 예제 워크플로

Adobe Experience Platform은 고객 경험을 주도하는 완벽한 솔루션을 구축하고 관리하기 위해 시장에서 가장 강력하고 유연하며 개방적인 시스템입니다. Experience Platform을 통해 조직은 모든 시스템의 고객 데이터와 콘텐츠를 중앙 집중화 및 표준화하고 데이터 과학 및 시스템 학습을 적용하여 풍부한 개인별 경험을 더 잘 설계하고 전달할 수 있습니다.

RESTful API를 기반으로 구축된 Experience Platform은 시스템의 모든 기능을 개발자에게 공개하여 친숙한 도구를 사용하여 엔터프라이즈 솔루션의 손쉬운 통합을 지원합니다. Experience Platform을 사용하면 고객 데이터를 수집하고, 데이터를 타겟팅할 대상으로 세그먼트화하고, 이러한 대상을 외부 대상으로 활성화하여 고객에 대한 거시적인 보기를 파생할 수 있습니다. 다음 튜토리얼에서는 소스를 통한 수집에서 대상을 통한 대상자 활성화까지의 모든 단계를 보여 주는 전체 워크플로우를 보여 줍니다.

![Experience Platform 전체 워크플로](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## 시작하기

이 통합 워크플로우는 여러 Adobe Experience Platform 서비스를 사용합니다. 다음은 개요에 대한 링크와 함께 이 워크플로에서 사용되는 서비스 목록입니다.

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그먼테이션을 최대한 활용하려면 [데이터 모델링 모범 사례](../xdm/schema/best-practices.md)에 따라 데이터가 프로필 및 이벤트로 수집되는지 확인하십시오.
- [[!DNL Identity Service]](../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 고객 및 고객 행동에 대한 포괄적인 보기를 제공합니다.
- [원본](../sources/home.md): [!DNL Experience Platform]에서는 데이터를 다양한 원본에서 수집할 수 있으며 [!DNL Experience Platform] 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 개선하는 기능을 제공합니다.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service]을(를) 사용하면 개인(예: 고객, 잠재 고객, 사용자 또는 조직)과 관련된 [!DNL Experience Platform]에 저장된 데이터를 더 작은 그룹으로 나눌 수 있습니다.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [데이터 집합](../catalog/datasets/overview.md): [!DNL Experience Platform]의 데이터 지속성을 위한 저장소 및 관리 구성입니다.
- [대상](../destinations/home.md): 대상은 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타깃팅된 광고 및 기타 다양한 사용 사례를 위해 Experience Platform의 데이터를 원활하게 활성화할 수 있도록 일반적으로 사용되는 애플리케이션과의 사전 빌드된 통합입니다.

## XDM 스키마 만들기

데이터를 Experience Platform으로 수집하기 전에 먼저 해당 데이터의 구조를 설명하는 XDM 스키마를 만들어야 합니다. 다음 단계에서 데이터를 수집하면 들어오는 데이터를 이 스키마에 매핑하게 됩니다. 예제 XDM 스키마를 만드는 방법을 알아보려면 [스키마 편집기를 사용하여 스키마 만들기](../xdm/tutorials/create-schema-ui.md)에 대한 자습서를 읽어 보십시오.

위의 자습서에서는 스키마에 대한 ID 필드를 설정하는 방법을 보여줍니다. ID 필드는 레코드 또는 시계열 이벤트와 관련된 개별 사용자를 식별하는 데 사용할 수 있는 필드를 나타냅니다. ID 필드는 Experience Platform에서 고객 ID 그래프를 구성하는 방법에 대한 중요한 구성 요소이며, 이는 궁극적으로 실시간 고객 프로필이 서로 다른 데이터 조각을 병합하여 고객을 완전히 볼 수 있는 방법에 영향을 줍니다. Experience Platform에서 ID 그래프를 보는 방법에 대한 자세한 내용은 [ID 그래프 뷰어 사용 방법](../identity-service/features/identity-graph-viewer.md)에 대한 자습서를 참조하십시오.

실시간 고객 프로필에서 사용할 스키마를 활성화해야 스키마를 기반으로 데이터에서 고객 프로필을 생성할 수 있습니다. 자세한 내용은 스키마 UI 안내서의 [프로필에 대한 스키마 활성화](../xdm/ui/resources/schemas.md#profile)에 대한 섹션을 참조하십시오.

## Experience Platform에 데이터 수집

XDM 스키마를 만들면 데이터를 시스템으로 가져올 수 있습니다.

Experience Platform으로 가져온 모든 데이터는 수집 시 개별 데이터 세트에 저장됩니다. 데이터 세트는 특정 XDM 스키마에 매핑되는 데이터 레코드 모음입니다. [!DNL Real-Time Customer Profile]에서 데이터를 사용하려면 먼저 해당 데이터 세트를 구체적으로 구성해야 합니다. 프로필에 데이터 세트를 활성화하는 방법에 대한 자세한 지침은 [데이터 세트 UI 안내서](../catalog/datasets/user-guide.md#enable-profile) 및 [데이터 세트 구성 API 자습서](../profile/tutorials/dataset-configuration.md)를 참조하십시오. 데이터 세트가 구성되면 데이터 세트로의 데이터 수집을 시작할 수 있습니다.

Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 저장소, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다. 예를 들어 [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md)을(를) 사용하여 데이터를 수집할 수 있습니다. 사용 가능한 소스의 전체 목록은 [소스 커넥터 개요](../sources/home.md)에서 찾을 수 있습니다.

Amazon S3을 소스 커넥터로 사용하는 경우 [Amazon S3 커넥터 만들기](../sources/tutorials/api/create/cloud-storage/s3.md)에 대한 API 자습서 또는 [Amazon S3 커넥터 만들기](../sources/tutorials/ui/create/cloud-storage/s3.md)에 대한 UI 자습서의 지침을 따라 커넥터 내에서 데이터를 만들고, 연결하고, 수집하는 방법을 배울 수 있습니다.

소스 커넥터에 대한 자세한 지침은 [소스 커넥터 개요](../sources/home.md)를 참조하십시오. 소스가 기반으로 하는 API인 Flow Service에 대해 자세히 알아보려면 [Flow Service API 참조](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 읽어 보십시오.

소스 커넥터를 통해 Experience Platform으로 데이터를 가져와 프로필 활성화 데이터 세트에 저장하면 XDM 스키마에서 구성한 ID 데이터를 기반으로 고객 프로필이 자동으로 만들어집니다.

데이터를 새 데이터 세트에 처음 업로드할 때, 또는 새 ETL 프로세스 또는 데이터 소스를 설정할 때, 데이터가 올바르게 업로드되었는지, 생성된 프로필에 예상한 데이터가 포함되어 있는지 꼼꼼히 확인하는 것이 좋습니다. Experience Platform UI에서 고객 프로필에 액세스하는 방법에 대한 자세한 내용은 [실시간 고객 프로필 UI 안내서](../profile/ui/user-guide.md)를 참조하십시오. Real-Time Customer Profile API를 사용하여 프로필에 액세스하는 방법에 대한 자세한 내용은 [엔터티 끝점 사용](../profile/api/entities.md)에 대한 안내서를 참조하십시오.

## 데이터 평가

수집된 데이터에서 프로필을 성공적으로 생성했으면 세그멘테이션을 사용하여 데이터를 평가할 수 있습니다. 세그먼테이션은 마케팅 가능한 사용자 그룹을 고객 기반과 구별하기 위해 프로필 스토어와 개인 하위 집합이 공유하는 특정 속성 또는 동작을 정의하는 프로세스입니다. 세그먼테이션에 대한 자세한 내용은 [세그먼테이션 서비스 개요](../segmentation/home.md)를 참조하세요.

### 세그먼트 정의 만들기

시작하려면 고객을 클러스터링하여 타겟 대상을 만들 세그먼트 정의를 만들어야 합니다. 세그먼트 정의는 타겟팅할 대상자를 정의하는 데 사용할 수 있는 규칙 컬렉션입니다. 세그먼트 정의를 만들려면 [세그먼트 빌더](../segmentation/ui/segment-builder.md) 사용에 대한 UI 안내서 또는 [세그먼트 만들기](../segmentation/tutorials/create-a-segment.md)에 대한 API 자습서의 지침을 따를 수 있습니다.

세그먼트 정의를 만들었으면 세그먼트 정의 ID를 계속 메모해 두십시오.

### 세그먼트 정의 평가

세그먼트 정의를 만든 후 세그먼트를 일회성 인스턴스로 평가하는 세그먼트 작업을 만들거나, 지속적으로 세그먼트를 평가하는 일정을 만들 수 있습니다.

요청 시 세그먼트 정의를 평가하기 위해 세그먼트 작업을 생성할 수 있습니다. 세그먼트 작업은 참조된 세그먼트 정의 및 병합 정책을 기반으로 새 대상 세그먼트를 만드는 비동기 프로세스입니다. 병합 정책은 Experience Platform에서 고객 프로필을 만드는 데 사용할 데이터와 소스 간에 불일치가 있을 때 우선 순위가 매겨지는 데이터를 결정하는 데 사용하는 규칙 세트입니다. 병합 정책으로 작업하는 방법에 대해 알아보려면 [병합 정책 UI 안내서](../profile/merge-policies/ui-guide.md)를 참조하십시오.

세그먼트 작업이 생성되고 평가되면 대상의 크기 또는 처리 중 발생했을 수 있는 오류 등 세그먼트에 대한 정보를 가져올 수 있습니다. 제공해야 하는 모든 세부 정보를 포함하여 세그먼트 작업을 만드는 방법에 대해 알아보려면 [세그먼트 작업 개발자 안내서](../segmentation/api/segment-jobs.md)를 읽어 보십시오.

지속적으로 세그먼트 정의를 평가하기 위해 일정을 만들고 활성화할 수 있습니다. 예약은 지정된 시간에 하루에 한 번 세그먼트 작업을 자동으로 실행하는 데 사용할 수 있는 도구입니다. 일정을 만들고 활성화하는 방법에 대해 알아보려면 [일정 끝점](../segmentation/api/schedules.md)에 있는 API 안내서의 지침을 따르십시오.

## 평가된 데이터 내보내기

일회성 세그먼트 작업을 만들거나 진행 중인 일정을 만든 후 세그먼트 내보내기 작업을 만들어 결과를 데이터 세트로 내보내거나 결과를 대상으로 내보낼 수 있습니다. 다음 섹션에서는 이러한 두 옵션 모두에 대한 지침을 제공합니다.

### 평가된 데이터를 데이터 세트로 내보내기

일회성 세그먼트 작업을 만들거나 진행 중인 일정을 만든 후 세그먼트 내보내기 작업을 만들어 결과를 내보낼 수 있습니다. 세그먼트 내보내기 작업은 평가된 대상에 대한 정보를 데이터 세트로 보내는 비동기 작업입니다.

내보내기 작업을 만들기 전에 먼저 데이터를 내보낼 데이터 세트를 만들어야 합니다. 데이터 집합을 만드는 방법에 대해 알아보려면 세그먼트 평가 자습서에서 [대상 데이터 집합 만들기](../segmentation/tutorials/evaluate-a-segment.md#create-dataset)에 대한 섹션을 읽어 데이터 집합 ID를 만든 후에 메모해 두십시오. 데이터 세트를 만든 후 내보내기 작업을 만들 수 있습니다. 내보내기 작업을 만드는 방법에 대해 알아보려면 [내보내기 작업 끝점](../segmentation/api/export-jobs.md)에 있는 API 안내서의 지침을 따르십시오.

### 평가된 데이터를 대상으로 내보내기

또는 일회성 세그먼트 작업 또는 진행 중인 일정을 작성한 후 결과를 대상으로 내보낼 수 있습니다. 대상은 대상을 활성화하고 전달할 수 있는 외부 서비스의 Adobe 애플리케이션과 같은 엔드포인트입니다. [대상 카탈로그](../destinations/catalog/overview.md)에서 사용 가능한 대상의 전체 목록을 찾을 수 있습니다.

데이터를 일괄 처리 또는 이메일 마케팅 대상으로 활성화하는 방법에 대한 지침은 [Experience Platform UI를 사용하여 대상 데이터를 일괄 처리 프로필 내보내기 대상으로 활성화하는 방법](../destinations/ui/activate-batch-profile-destinations.md)에 대한 자습서와 Flow Service API를 사용하여 일괄 처리 대상에 연결하고 데이터를 활성화하는 방법에 대한 [안내서](../destinations/api/connect-activate-batch-destinations.md)를 참조하십시오.

## Experience Platform 데이터 활동 모니터링

Experience Platform을 사용하면 Experience Platform의 다양한 구성 요소에서 데이터를 이동하는 작업의 표현인 데이터 흐름을 사용하여 데이터가 처리되는 방식을 추적할 수 있습니다. 이러한 데이터 흐름은 서로 다른 서비스에 걸쳐 구성되어 있으므로 데이터를 소스 커넥터에서 대상 데이터 세트로 이동하는 데 도움이 됩니다. [!DNL Identity Service] 및 [!DNL Real-Time Customer Profile]에서 해당 데이터를 사용한 후 최종적으로 대상으로 활성화할 수 있습니다. 모니터링 대시보드는 데이터 흐름의 여정을 시각적으로 표시합니다. Experience Platform UI 내에서 데이터 흐름을 모니터링하는 방법은 [소스에 대한 데이터 흐름 모니터링](../dataflows/ui/monitor-sources.md) 및 [대상에 대한 데이터 흐름 모니터링](../dataflows/ui/monitor-destinations.md)에 대한 튜토리얼을 참조하십시오.

[!DNL Observability Insights]을(를) 사용하여 통계 지표 및 이벤트 알림을 사용하여 Experience Platform 활동을 모니터링할 수도 있습니다. Experience Platform UI를 통해 경고 알림을 구독하거나 구성된 웹후크로 전송할 수 있습니다. Experience Platform UI에서 사용 가능한 경고를 보고, 활성화하고, 비활성화하고, 구독하는 방법에 대한 자세한 내용은 [[!UICONTROL 경고] UI 안내서](../observability/alerts/ui.md)를 참조하십시오. 웹후크를 통해 경고를 받는 방법에 대한 자세한 내용은 [Adobe I/O 이벤트 알림 구독](../observability/alerts/subscribe.md)에 대한 안내서를 참조하십시오.

## 다음 단계

이 자습서를 통해 Experience Platform의 간단한 종단 간 흐름에 대한 기본적인 소개를 받을 수 있습니다. Adobe Experience Platform에 대한 자세한 내용은 [Experience Platform 개요](./home.md)를 참조하세요. Experience Platform UI 및 Experience Platform API 사용에 대한 자세한 내용은 각각 [Experience Platform UI 안내서](./ui-guide.md) 및 [Experience Platform API 안내서](./api-guide.md)를 참조하십시오.
