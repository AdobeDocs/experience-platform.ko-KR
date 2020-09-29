---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: 실시간 고객 프로필 자습서
topic: tutorial
type: Tutorial
description: 이 문서에서는 관련 단계에 대해 설명하고 각 개별 워크플로우를 완료하기 위한 자습서에 대한 링크를 제공합니다.
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# 구성 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]

조직에 대해 구성하려면 여러 개의 별도 워크플로우 [!DNL Real-time Customer Profile] 를 완료해야 합니다. 이 문서에서는 관련 단계에 대해 설명하고 각 개별 워크플로우를 완료하기 위한 자습서에 대한 링크를 제공합니다.

자세한 내용 [!DNL Real-time Customer Profile]은 프로필 [개요를 읽으십시오](../profile/home.md).

## 실시간 고객 프로필 UI 개요

실시간 고객 프로파일은 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 다양한 채널의 데이터를 취합하여 각 개별 고객에 대한 전체적인 관점을 생성합니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 프로필 [!UICONTROL UI] 및 사용 가능한 기능을 파악합니다.
- 프로필 데이터 보기 및 관리

자세한 내용은 [실시간 고객 프로필 사용 안내서를 참조하십시오](../profile/ui/user-guide.md)

## 실시간 고객 프로필 API

실시간 고객 프로필 API에는 여러 끝점이 포함되어 있습니다. 프로필을 사용하면 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널에서 생성된 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 모든 고객 인터랙션에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다. 사용 가능한 각 끝점과 사용 사례에 대한 자세한 내용은 [실시간 고객 프로필 API 개요를](../profile/api/overview.md) 참조하십시오.

**다음 API 개발자 가이드를 사용할 수 있습니다.**
- [계산된 속성(알파) ](../profile/api/computed-attributes.md) - 계산된 속성의 사용 사례와 계산된 속성을 구성, 액세스, 업데이트 및 삭제하는 방법에 대해 알아봅니다.
- [모서리 투영](../profile/api/edge-projections.md) - 투영 대상을 생성, 보기, 업데이트, 삭제 및 나열하는 방법을 살펴볼 수 있습니다. 또한 이 문서에는 투영 구성 나열 및 만들기에 대한 정보가 포함되어 있으며 선택기 사용 예를 제공합니다.
- [엔티티(프로필 액세스)](../profile/api/entities.md) - ID 또는 ID 목록별로 프로필 데이터에 액세스하는 방법을 알아봅니다. 또한 ID를 사용하여 여러 프로필의 시간 시리즈 이벤트에 액세스하고, ID별로 단일 프로파일을 사용하며, 여러 스키마 개체에 액세스하는 방법을 알아봅니다.
- [내보내기 작업(프로필 내보내기)](../profile/api/export-jobs.md) - 내보내기 작업을 만들고, 보고, 모니터하고, 취소하는 방법을 알아봅니다.
- [정책](../profile/api/merge-policies.md) 병합 - 병합 정책을 액세스하고, 만들고, 업데이트하고, 삭제하는 방법뿐만 아니라 병합 정책의 구성 요소에 대해 알아봅니다.
- [샘플 상태 미리 보기(프로필 미리 보기)](../profile/api/preview-sample-status.md) - 마지막 샘플 상태를 보고 데이터 세트별 프로필 배포를 나열하고 네임스페이스별 프로필 배포를 나열하는 방법을 알아봅니다.
- [프로필 시스템 작업(요청 삭제)](../profile/api/profile-system-jobs.md) - 프로필 스토어에서 데이터 세트 또는 일괄 처리에 대한 삭제 요청을 보고, 만들고, 제거하는 방법을 알아봅니다.

실시간 고객 프로필 API를 사용하여 CRUD 작업을 수행하는 데 필요한 값을 확인하고 자세한 내용을 보려면 [시작 안내서를 참조하십시오](../profile/api/getting-started.md).

## 서비스 [!DNL Profile] 및 서비스에 대한 스키마 [!DNL Identity] 활성화

데이터를 Adobe Experience Platform으로 인제스트하여 데이터 생성 시 사용하려면 인제스트할 데이터 구조를 제공하고 이 스키마를 [!DNL Real-time Customer Profiles]및 Adobe Experience Platform에서 사용하도록 설정해야 합니다 [!DNL Profile] [!DNL Identity Service].

**이 가이드는 다음과 같은 도움을 줍니다.**
- 기존 스키마를 찾아봅니다.
- 스키마를 만들고 이름을 지정합니다.
- XDM 믹스를 추가하고 정의합니다.
- 스키마 필드를 ID 필드로 설정합니다.
- 스키마에 대한 프로필 사용을 참조하십시오.

스키마 레지스트리 API를 사용하여 스키마 [!DNL Profile] 를 [!DNL Identity Service]생성하거나 스키마 빌더 UI를 사용하여 스키마 [를](../xdm/tutorials/create-schema-api.md) 만드는 방법에 대한 단계별 지침을 참조하십시오 [](../xdm/tutorials/create-schema-ui.md).

## 데이터 세트 구성 [!DNL Profile] 및 [!DNL Identity]

데이터 인제스트를 시작하려면 및 [!DNL Profile]과 함께 사용할 수 있도록 적절하게 구성된 데이터 세트 [!DNL Real-time Customer Profile] 가 있어야 합니다 [!DNL Identity Service].

**이 가이드는 다음과 같은 도움을 줍니다.**
- 프로필에 대해 활성화된 데이터 세트를 만듭니다.
- 기존 데이터 세트를 구성합니다.
- 데이터를 데이터 세트에 인제스트합니다.
- 데이터 세트에 프로필이 활성화되어 있고 ID 서비스를 사용하고 있는지 확인합니다.

시작하려면 API 자습서에 따라 프로필 및 ID에 대한 데이터 세트 [를 구성합니다](../profile/tutorials/dataset-configuration.md).

## 병합 정책 구성

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 개별 고객의 전체 상황을 파악할 수 있습니다. 이 데이터를 취합할 때 병합 정책은 데이터의 우선 순위를 매기는 방법과 데이터를 결합하여 통합 뷰를 생성하는 데 [!DNL Platform] 사용하는 규칙입니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 새로운 병합 정책을 만듭니다.
- 기존 병합 정책을 관리합니다.
- 조직에 대한 기본 병합 정책을 설정합니다.
- 병합 정책 위반을 파악합니다.

UI에서 병합 정책을 [!DNL Platform] 사용하려면 [병합 정책 사용 안내서를 참조하십시오](../profile/ui/merge-policies.md). 실시간 고객 프로필 API를 사용하여 병합 정책을 사용하려면 [병합 정책 개발자 안내서를 참조하십시오](../profile/api/merge-policies.md).

## 에지 예측 구성

여러 채널에서 실시간으로 고객의 기대에 부응하는 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 정확한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe [!DNL Experience Platform] 를 사용하면 가장자리라고 하는 요소를 사용하여 데이터에 대한 실시간 액세스를 구현할 수 있습니다. Edge는 데이터를 저장하고 애플리케이션에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터가 전송될 가장자리를 정의하며, 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 모서리 투영 대상을 목록, 생성, 보기, 업데이트 및 삭제합니다.
- 모서리 투영 구성을 나열하고 생성합니다.
- 선택기를 이해합니다.

자세한 내용을 살펴보고 가장자리 예상 [!DNL Real-time Customer Profile] 부분에 대한 [API](../profile/api/edge-projections.md)하위 안내서를 참조하십시오.

## 프로필 데이터가 UI에 표시되는 방법 사용자 정의

Experience Platform 유저 인터페이스 내에서 고객 프로파일 형태로 실시간 고객 프로파일 데이터를 보고 인터랙션할 수 있습니다. UI에 표시되는 프로필 정보는 여러 프로필 조각에서 병합되어 각 개별 고객의 단일 보기를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정과 같은 세부 사항이 포함됩니다. 프로필에 표시된 기본 필드는 기본 프로필 속성을 표시하도록 조직 수준에서 변경할 수도 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 카드 순서 변경, 크기 조정, 편집 및 제거
- 속성을 추가합니다.
- 새 카드를 추가합니다.
- 기본값 복원

프로필 데이터 사용자 지정에 대한 자세한 내용은 [프로필 사용자 정의 설명서를 참조하십시오](../profile/ui/profile-customization.md)

## 다음 단계

조직 [!DNL Real-time Customer Profile] 에 대해 구성한 후에는 개별 고객 프로필에 데이터를 추가하고 특정 고객 특성을 기반으로 고객 세그먼트를 만들 수 있습니다. 시작하려면 다음 자습서를 참조하십시오.

- [실시간 고객 프로필에 데이터 추가](../profile/tutorials/add-profile-data.md)
- [세그먼트 만들기](../segmentation/tutorials/create-a-segment.md)