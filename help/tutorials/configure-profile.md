---
keywords: Experience Platform;홈;인기 항목;실시간 고객 프로필;ID 서비스
solution: Experience Platform
title: 실시간 고객 프로필 자습서
topic-legacy: tutorial
type: Tutorial
description: 이 문서에서는 관련 단계에 대해 간략히 설명하고 각 개별 워크플로우를 완료하기 위한 자습서에 대한 링크를 제공합니다.
exl-id: cda6e7a7-9498-454c-94df-c6271a5a4fd4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] 구성

조직에 대해 [!DNL Real-time Customer Profile]을(를) 구성하려면 여러 개의 별도의 워크플로우를 완료해야 합니다. 이 문서에서는 관련 단계에 대해 간략히 설명하고 각 개별 워크플로우를 완료하기 위한 자습서에 대한 링크를 제공합니다.

[!DNL Real-time Customer Profile]에 대한 자세한 내용은 [프로필 개요](../profile/home.md)를 읽으십시오.

## 실시간 고객 프로필 UI 개요

실시간 고객 프로파일은 온라인, 오프라인, CRM 및 제3자 데이터를 비롯한 여러 채널의 데이터를 취합하여 각 개별 고객을 전체적으로 파악할 수 있도록 지원합니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- [!UICONTROL Profiles] UI 및 사용 가능한 기능에 대해 이해합니다.
- 프로필 데이터를 보고 관리합니다.

자세한 내용은 [실시간 고객 프로필 사용 안내서](../profile/ui/user-guide.md)를 참조하십시오.

## 실시간 고객 프로필 API

실시간 고객 프로필 API에는 여러 끝점이 있습니다. 사용 가능한 각 끝점과 사용 사례에 대한 자세한 내용은 [실시간 고객 프로필 API 개요](../profile/api/overview.md)를 참조하십시오.

실시간 고객 프로필 API를 사용하여 CRUD 작업을 수행하는 데 필요한 값을 확인하고 자세한 내용을 보려면 [시작 안내서](../profile/api/getting-started.md)를 참조하십시오.

## [!DNL Profile] 및 [!DNL Identity] 서비스에 대한 스키마 사용

데이터를 Adobe Experience Platform으로 인제스트하여 [!DNL Real-time Customer Profiles] 만들기에 사용하려면 인제스트할 데이터의 구조를 제공하기 위해 스키마를 만들어야 하며, 이 스키마는 [!DNL Profile] 및 Adobe Experience Platform [!DNL Identity Service]에서 사용하도록 설정해야 합니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 기존 스키마를 찾아봅니다.
- 스키마를 만들고 이름을 지정합니다.
- XDM 믹스를 추가하고 정의합니다.
- 스키마 필드를 ID 필드로 설정합니다.
- 스키마에 대한 프로필 사용을 참조하십시오.

[!DNL Profile] 및 [!DNL Identity Service]에 대해 활성화된 스키마를 만드는 방법에 대한 단계별 지침은 [스키마 레지스트리 API](../xdm/tutorials/create-schema-api.md) 또는 [스키마 빌더 UI](../xdm/tutorials/create-schema-ui.md)를 사용하여 스키마 만들기에 대한 자습서를 참조하십시오.

## [!DNL Profile] 및 [!DNL Identity]에 대한 데이터 집합 구성

데이터를 [!DNL Profile]에 인제스트하려면 [!DNL Real-time Customer Profile] 및 [!DNL Identity Service]에서 사용하도록 올바르게 구성된 데이터 세트가 있어야 합니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 프로파일에 대해 활성화된 데이터 집합을 만듭니다.
- 기존 데이터 세트를 구성합니다.
- 데이터를 데이터 세트에 인제스트합니다.
- 데이터 세트에 프로필이 활성화되어 있고 ID 서비스를 사용하고 있는지 확인합니다.

시작하려면 [프로필 및 ID](../profile/tutorials/dataset-configuration.md)에 대한 데이터 세트 구성에 대한 API 자습서를 따르십시오.

## 병합 정책 구성

Adobe Experience Platform을 사용하면 여러 소스에서 데이터를 취합하여 각 개별 고객을 전체적으로 파악할 수 있습니다. 이 데이터를 함께 가져올 때 병합 정책은 데이터의 우선 순위를 지정하는 방법과 통합 보기를 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다.[!DNL Platform]

**이 가이드는 다음과 같은 도움을 줍니다.**
- 새로운 병합 정책을 만듭니다.
- 기존 병합 정책을 관리합니다.
- 조직에 대한 기본 병합 정책을 설정합니다.
- 병합 정책 위반을 파악합니다.

[!DNL Platform] UI에서 병합 정책을 사용하려면 [병합 정책 사용 안내서](../profile/ui/merge-policies.md)를 참조하십시오. 실시간 고객 프로필 API를 사용하여 병합 정책을 사용하려면 [병합 정책 개발자 안내서](../profile/api/merge-policies.md)를 참조하십시오.

## 에지 예상 구성

여러 채널에서 실시간으로 고객에게 일관되고 개인화된 경험을 제공하기 위해서는 변경 사항이 발생하면 즉시 적합한 데이터를 제공하고 지속적으로 업데이트해야 합니다. Adobe [!DNL Experience Platform]은(는) 가장자리라고 하는 항목을 사용하여 데이터에 대한 실시간 액세스를 가능하게 합니다. Edge는 데이터를 저장하고 응용 프로그램에서 쉽게 액세스할 수 있도록 하는 지리적으로 배치된 서버입니다. 데이터는 투영에 의해 모서리로 라우팅되고, 투영 대상은 데이터를 보낼 가장자리를 정의하고 가장자리에서 사용할 특정 정보를 정의하는 투영 구성이 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 가장자리 투영 대상을 나열, 생성, 보기, 업데이트 및 삭제합니다.
- 가장자리 투영 구성을 나열하고 만듭니다.
- 선택기를 파악합니다.

자세한 내용이나 가장자리 작업을 시작하려면 가장자리 예상치](../profile/api/edge-projections.md)에 대한 [!DNL Real-time Customer Profile] API [하위 안내서를 참조하십시오.

## 프로필 데이터가 UI에 표시되는 방법 사용자 정의

Experience Platform 유저 인터페이스 내에서 고객 프로파일 형태로 실시간 고객 프로파일 데이터를 보고 인터랙션할 수 있습니다. UI에 표시되는 프로필 정보는 여러 프로필 조각에서 병합되어 각 개별 고객의 단일 보기를 형성했습니다. 여기에는 기본 속성, 연결된 ID 및 채널 환경 설정과 같은 세부 사항이 포함됩니다. 프로파일에 표시된 기본 필드는 기본 프로필 속성을 표시하도록 조직 수준에서 변경할 수도 있습니다.

**이 가이드는 다음과 같은 도움을 줍니다.**
- 카드 순서 변경, 크기 조정, 편집 및 제거
- 속성을 추가합니다.
- 새 카드를 추가합니다.
- 기본값 복원

프로필 데이터 사용자 지정에 대한 자세한 내용은 [프로필 사용자 지정 설명서](../profile/ui/profile-customization.md)를 참조하십시오.

## 다음 단계

조직에 대해 [!DNL Real-time Customer Profile]을(를) 구성한 후에는 개별 고객 프로파일에 데이터를 추가하고 특정 고객 속성을 기반으로 대상 세그먼트를 만들 수 있습니다. 시작하려면 다음 자습서를 참조하십시오.

- [실시간 고객 프로필에 데이터 추가](../profile/tutorials/add-profile-data.md)
- [세그먼트 만들기](../segmentation/tutorials/create-a-segment.md)
