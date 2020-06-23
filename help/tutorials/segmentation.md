---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 세그멘테이션 자습서
topic: tutorial
translation-type: tm+mt
source-git-commit: 636fae71f9c826ce9715bd96a974e5f6afbffb42
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---


# 세그멘테이션 자습서

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 작성하고 실시간 고객 프로필 데이터를 통해 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 세그먼트는 Platform에 중앙에서 구성 및 관리되며, 모든 Adobe 솔루션에서 즉시 액세스할 수 있습니다. 세그멘테이션에 대한 자세한 내용은 세그멘테이션 [서비스 개요를 읽어 보십시오](../segmentation/home.md).

## 세그먼트 정의 만들기

세그먼트 정의는 대상 대상의 주요 특성이나 동작을 설명하는 데 사용되는 규칙 세트입니다. 개념을 종합하면 세그먼트 정의에 요약된 규칙이 세그먼트에 대한 적격한 대상 구성원을 결정하는 데 사용됩니다. 세그먼트 정의를 개발, 테스트, 미리 보기 및 저장하는 작업은 Platform 사용자 인터페이스 또는 API를 사용하여 수행할 수 있습니다. 세그먼트 정의를 만들려면 세그먼트 API [만들기 자습서](../segmentation/tutorials/create-a-segment.md) 또는 [세그먼트 빌더 UI 사용자 안내서를 따르십시오](../segmentation/ui/overview.md).

## 세그먼트 평가 및 결과 액세스

세그먼트 정의를 개발, 테스트 및 저장한 후에는 예약된 평가나 주문형 평가를 통해 세그먼트를 평가할 수 있습니다. 예약된 평가(일명 &#39;예약된 세그멘테이션&#39;이라고도 함)를 사용하면 특정 시간에 내보내기 작업을 실행하기 위한 반복 일정을 만들 수 있지만, on-demand 평가에서는 세그먼트 작업을 생성하여 대상을 즉시 작성합니다. 자세한 내용은 튜토리얼에서 세그먼트 결과를 [평가하고 액세스할 수 있습니다](../segmentation/tutorials/evaluate-a-segment.md).

## 세그먼트 데이터 내보내기

프로필 데이터가 포함된 세그먼트를 내보내려면 먼저 데이터를 내보낼 [](../segmentation/tutorials/create-dataset-export-segment.md)데이터 세트를 만든 다음 새 내보내기 작업을 시작해야 합니다. 내보내기 작업을 생성하는 단계는 [내보내기 API 자습서에서 확인할 수 있습니다](../segmentation/tutorials/export-data.md).

## 병합 정책 구성

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 각 개별 고객에 대한 전체 상황을 파악할 수 있습니다. 이 데이터를 취합할 때 병합 정책은 Platform에서 데이터의 우선 순위를 결정하는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 사용하는 규칙입니다. RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. Platform UI에서 병합 정책을 사용하려면 [병합 정책 사용 안내서를 참조하십시오](../profile/ui/merge-policies.md). 실시간 고객 프로필 API를 사용하여 병합 정책을 사용하려면 [병합 정책 개발자 안내서를 참조하십시오](../profile/api/merge-policies.md).

## 세그먼트에 대한 데이터 사용 규정 준수

실시간 고객 프로필에서 사용할 수 있는 세그먼트에는 해당 세그먼트 정의 내에 병합 정책 ID가 포함됩니다. 이 병합 정책에는 세그먼트에 포함할 데이터 집합에 대한 정보가 포함되며, 이 정보에는 적용 가능한 데이터 사용 레이블이 포함됩니다. 대상 세그먼트에 대한 데이터 사용 규정 준수를 적용하는 특정 단계에 대해서는 세그먼트에 대한 [데이터 사용 규정 준수 시행 자습서를 따르십시오](../segmentation/tutorials/governance.md).

## (베타) 스트리밍 세분화

>[!NOTE]
>스트리밍 세그멘테이션은 베타 버전이며 요청 시 이용할 수 있습니다. 기능 및 설명서는 변경될 수 있습니다.

스트리밍 세그멘테이션은 이벤트가 특정 세그먼트 그룹에 포함되면 즉시 고객을 평가하는 기능입니다. 이 기능을 사용하면 이제 데이터가 Adobe Experience Platform으로 전달되면 대부분의 세그먼트 규칙을 평가할 수 있으므로, 세그먼트 멤버십은 예약된 세그멘테이션 작업을 실행하지 않고 최신 상태로 유지됩니다. 자세한 내용은 [스트리밍 세그멘테이션 개요를 참조하십시오](../segmentation/api/streaming-segmentation.md).

## 다중 엔티티 세그먼테이션

다중 엔티티 세그먼테이션은 제품, 스토어 또는 기타 비프로필 클래스에 따라 추가 데이터로 프로필 데이터를 확장하는 기능입니다. 연결되면 추가 클래스의 데이터를 프로필 스키마가 기본인 것처럼 사용할 수 있습니다. 이동을 알아보려면 [다중 엔티티 세그먼테이션 설명서를 참조하십시오](../segmentation/multi-entity-segmentation.md).