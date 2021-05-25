---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;통합 프로필;통합 프로필;통합;프로필;rtcp;프로필 사용;프로필 사용
title: 실시간 고객 프로필 API 안내서
description: 개발자는 실시간 고객 프로필 API를 사용하여 보기 프로필, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 또는 샘플 데이터 내보내기, 더 이상 필요하지 않거나 오류가 추가된 프로필 데이터 삭제 등 프로필 데이터를 탐색 및 작업할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법을 알아보려면 이 안내서를 따르십시오.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 1c2e4cd2b4070f3844a9848b5574e9d5b1688926
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] API 안내서

[!DNL Real-time Customer Profile] Adobe Experience Platform 내에서 각 개별 고객을 종합적으로 파악할 수 있습니다. [!DNL Profile] 을(를) 사용하면 온라인, 오프라인, CRM 및 타사 데이터와 같은 여러 채널의 서로 다른 고객 데이터를 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 통합할 수 있습니다.

[!DNL Real-time Customer Profile] API에는 아래에 요약된 여러 종단점이 포함되어 있습니다. 자세한 내용은 개별 종단점 안내서를 방문하여 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 보려면 [시작 안내서](getting-started.md)를 참조하십시오.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [실시간 고객 프로필 API 참조 swagger](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)를 방문하십시오.

[!DNL Experience Platform] UI에서 [!DNL Real-time Customer Profile] 데이터를 사용하는 방법에 대한 안내서는 [프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.

## (알파) 계산된 속성 {#computed-attributes}

>[!IMPORTANT]
>
>계산된 특성 기능은 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다.

계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않아도 라이프타임 구매 값, 구매 간 시간 또는 애플리케이션 열기 수와 같은 문제와 관련된 질문에 쉽게 답변할 수 있습니다. 그런 다음 이러한 계산된 속성 값을 프로필에서 보거나 세그먼트를 만드는 데 사용하거나 다양한 액세스 패턴을 통해 액세스할 수 있습니다.

`config/computedAttributes` 종단점을 사용하여 계산된 속성을 생성, 보기, 편집 및 삭제할 수 있습니다. 계산된 속성을 사용하는 방법에 대해 알아보려면 [계산된 속성 개요](../computed-attributes/overview.md)를 참조하십시오. API 작업의 경우 [계산된 속성 API 엔드포인트 가이드](../computed-attributes/ca-api.md)를 방문하십시오.

## 에지 예측 {#edge-projections}

Adobe Experience Platform을 사용하면 &quot;edges&quot;라는 전략적으로 위치한 서버에서 데이터에 쉽게 액세스할 수 있도록 하여 고객 경험을 실시간으로 개인화할 수 있습니다. [!DNL Real-time Customer Profile] API는 &quot;예측&quot;이라는 구성 요소를 통해 에지 작업을 위한 종단점을 제공합니다. 프로젝션 구성에는 각 에지에 투영해야 하는 데이터를 결정하는 투영 구성과 투영 경로 지정 위치를 정의하는 투영 대상도 포함됩니다. 에지 예측 작업에 대한 자세한 내용은 [프로젝션 구성 및 대상 엔드포인트 안내서](edge-projections.md)를 참조하십시오.

## 엔터티([!DNL Profile] 액세스) {#entities}

Adobe Experience Platform을 통해 RESTful API 또는 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile] 데이터에 액세스할 수 있습니다. API를 사용하여 &quot;프로필&quot;이라고도 하는 엔티티에 액세스하는 방법을 알려면 [엔티티 엔드포인트 가이드](entities.md)에 설명된 단계를 따르십시오. [!DNL Platform] UI를 사용하여 프로필에 액세스하려면 [프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.

## 작업 내보내기([!DNL Profile] 내보내기) {#profile-export}

[!DNL Real-time Customer Profile] 활성화를 위해 대상 세그먼트 내보내기 또는 보고를 위한 프로필 속성 내보내기와 같은 추가 처리를 위해 데이터 세트에 데이터를 내보낼 수 있습니다. 대상 세그먼트에 대한 내보내기 작업은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 자세한 내용은 [세그멘테이션 내보내기 작업 끝점 안내서](../../profile/api/export-jobs.md)를 참조하십시오. 프로필 특성에 대한 내보내기 작업을 만들고 관리하는 방법에 대한 단계별 지침은 [작업 내보내기 끝점 안내서](export-jobs.md)를 참조하십시오.

## 정책 병합 {#merge-policies}

[!DNL Experience Platform]에서 여러 소스의 데이터를 함께 가져올 때 병합 정책은 [!DNL Platform]에서 데이터의 우선 순위가 매겨지는 방식과 개별 고객 프로필을 만들기 위해 결합할 데이터를 결정하는 규칙입니다. [!DNL Real-time Customer Profile] API를 사용하여 새 병합 정책을 만들고, 기존 정책을 관리하고, 조직에 대한 기본 병합 정책을 설정할 수 있습니다. API를 사용하여 병합 정책으로 작업하려면 [병합 정책 엔드포인트 가이드](merge-policies.md)를 방문하십시오.

병합 정책 및 Platform 내의 해당 역할에 대해 자세히 알아보려면 [병합 정책 개요](../merge-policies/overview.md)를 읽어 보십시오.

## 샘플 상태 미리 보기([!DNL Profile] 미리 보기) {#profile-preview}

프로필에 대해 활성화된 데이터를 Experience Platform에 수집하므로 프로필 데이터 저장소 내에 저장됩니다. 프로필 저장소의 레코드 수가 증가하거나 감소하면 데이터 저장소에 있는 프로필 조각 및 병합된 프로필의 수에 대한 정보를 포함하는 샘플 작업이 실행됩니다. 프로필 API를 사용하여 성공적인 최신 샘플과 데이터 집합 및 ID 네임스페이스별 프로필 배포 목록을 미리 볼 수 있습니다. `/profilepreviewstatus` 종단점을 사용하여 시작하려면 [샘플 상태 엔드포인트 미리 보기 안내서](preview-sample-status.md)를 참조하십시오.

## 프로필 시스템 작업 {#profile-system-jobs}

[!DNL Platform]에 수집되는 프로필 사용 데이터는 [!DNL Data Lake] 및 [!DNL Real-time Customer Profile] 데이터 저장소에 저장됩니다. 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하려면 [!DNL Profile] 저장소에서 데이터 세트 또는 일괄 처리를 삭제해야 할 수 있습니다. 이를 위해서는 API를 사용하여 필요한 경우 수정, 모니터링 또는 삭제할 수 있는 [!DNL Profile System Job]&quot;를 만들어야 합니다. [!DNL delete request] [!DNL Real-time Customer Profile] API에서 `/system/jobs` 종단점을 사용하여 삭제 요청을 사용하는 방법을 알아보려면 [프로필 시스템 작업 종단점 안내서](profile-system-jobs.md)에 설명된 단계를 따르십시오.

## 다음 단계 {#next-steps}

[!DNL Real-time Customer Profile] API를 사용하여 호출을 시작하려면 [시작 안내서](getting-started.md)를 읽은 다음 엔드포인트 가이드 중 하나를 선택하여 특정 [!DNL Profile] 관련 엔드포인트를 사용하는 방법을 알아봅니다. [!DNL Experience Platform] UI를 사용하여 [!DNL Profile] 데이터로 작업하려면 [실시간 고객 프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.
