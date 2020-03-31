---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 실시간 고객 프로필 자습서
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# 실시간 고객 프로필 및 ID 서비스 구성

조직의 실시간 고객 프로필을 구성하려면 여러 개의 개별 워크플로우를 완료해야 합니다. 이 문서에서는 관련 단계에 대해 간략하게 설명하고 각 개별 워크플로우를 완료하기 위한 자습서 링크를 제공합니다. 실시간 고객 프로파일에 대한 자세한 내용은 프로필 개요를 [참조하십시오](../profile/home.md).

## 프로필 및 ID에 대한 스키마 활성화

데이터를 Adobe Experience Platform으로 인제스트하여 실시간 고객 프로파일 만들기에 사용하려면 인제스트될 데이터의 구조를 제공하고 해당 스키마를 프로필 및 Adobe Experience Platform Identity Service에서 사용할 수 있도록 활성화해야 합니다. 프로필 및 ID 서비스에 대해 활성화된 스키마를 만드는 방법에 대한 단계별 지침은 스키마 레지스트리 API를 사용하여 스키마를 [만들거나 스키마 빌더 UI를 사용하여 스키마를](../xdm/tutorials/create-schema-api.md) 만드는 [자습서를 참조하십시오](../xdm/tutorials/create-schema-ui.md).

## 프로필 및 ID에 대한 데이터 집합 구성

데이터를 프로필로 인제스트하려면 실시간 고객 프로필 및 ID 서비스에서 사용하도록 적절하게 구성된 데이터 집합이 있어야 합니다. 시작하려면 프로필 및 ID용 데이터 세트 [구성 자습서를](../profile/tutorials/dataset-configuration.md)따르십시오.

## 병합 정책 구성

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 개별 고객의 전체 상황을 파악할 수 있습니다. 이러한 데이터를 취합할 때 병합 정책은 Platform에서 데이터의 우선 순위를 정하는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 사용하는 규칙입니다. RESTful API 또는 사용자 인터페이스를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. 플랫폼 UI에서 병합 정책을 사용하려면 [병합 정책 사용 안내서를](../profile/ui/merge-policies.md)참조하십시오. 실시간 고객 프로파일 API를 사용하여 병합 정책을 사용하려면 [병합 정책 개발자 안내서를](../profile/api/merge-policies.md)참조하십시오.

## 가장자리 예측 구성

여러 채널에서 실시간으로 고객의 기대에 부응하는 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 정확한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe Experience Platform을 사용하면 데이터를 실시간으로 액세스할 수 있습니다. Edge는 지리적으로 배치된 서버로서 데이터를 저장하고 애플리케이션에서 쉽게 액세스할 수 있습니다. 데이터는 투영에 의해 가장자리로 라우팅되고, 투영 대상은 데이터를 전송할 가장자리를 정의하고, 모서리에서 사용할 수 있는 특정 정보를 정의하는 투영 구성을 사용합니다. 자세한 내용을 살펴보고 가장자리로 작업을 시작하려면 가장자리 예상치에 대한 실시간 고객 프로필 API [하위 안내서를 참조하십시오](../profile/api/edge-projections.md).

## 다음 단계

조직에 대한 실시간 고객 프로필을 구성한 후에는 개별 고객 프로필에 데이터를 추가하고 특정 고객 속성을 기반으로 고객 세그먼트를 만들 수 있습니다. 시작하려면 다음 자습서를 참조하십시오.

* [실시간 고객 프로필에 데이터 추가](../profile/tutorials/add-profile-data.md)
* [세그먼트 만들기](../segmentation/tutorials/create-a-segment.md)