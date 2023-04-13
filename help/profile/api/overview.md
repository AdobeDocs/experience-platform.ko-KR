---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;통합 프로필;통합 프로필;통합;프로필;rtcp;프로필 사용;프로필 사용
title: Real-Time Customer Profile API 안내서
description: 개발자는 실시간 고객 프로필 API를 사용하여 보기 프로필, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 또는 샘플 데이터 내보내기, 더 이상 필요하지 않거나 오류가 추가된 프로필 데이터 삭제 등 프로필 데이터를 탐색 및 작업할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API 안내서

[!DNL Real-Time Customer Profile] Adobe Experience Platform 내에서 각 개별 고객을 종합적으로 파악할 수 있습니다. [!DNL Profile] 을(를) 사용하면 온라인, 오프라인, CRM 및 타사 데이터와 같은 여러 채널의 서로 다른 고객 데이터를 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 통합할 수 있습니다.

다음 [!DNL Real-Time Customer Profile] API에는 아래에 요약된 여러 엔드포인트가 포함되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 방문하여 을 참조하십시오. [시작 안내서](getting-started.md) 필요한 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 제공합니다.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [실시간 고객 프로필 API 참조 Swagger](https://www.adobe.com/go/profile-apis-en).

사용 안내서 [!DNL Real-Time Customer Profile] 의 데이터 [!DNL Experience Platform] UI는 [프로필 사용 안내서](../ui/user-guide.md).

<!-- ## (Alpha) Computed attributes {#computed-attributes}

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization.

Each computed attribute contains an expression, or "rule", that evaluates incoming data and stores the resulting value in a profile attribute. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. These computed attribute values can then be viewed in a profile, used to create a segment, or accessed through a number of different access patterns.

You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. To learn how to use computed attributes, refer to the [computed attributes overview](../computed-attributes/overview.md). For API operations, visit the [computed attributes API endpoint guide](../computed-attributes/ca-api.md). -->

## 에지 예측 {#edge-projections}

Adobe Experience Platform을 사용하면 &quot;edges&quot;라는 전략적으로 위치한 서버에서 데이터에 쉽게 액세스할 수 있도록 하여 고객 경험을 실시간으로 개인화할 수 있습니다. 다음 [!DNL Real-Time Customer Profile] API는 &quot;예측&quot;이라는 구성 요소를 통해 에지 작업을 위한 종단점을 제공합니다. 프로젝션 구성에는 각 에지에 투영해야 하는 데이터를 결정하는 투영 구성과 투영 경로 지정 위치를 정의하는 투영 대상도 포함됩니다. 에지 예측 작업에 대한 자세한 내용은 [프로젝션 구성 및 대상 엔드포인트 안내서](edge-projections.md).

## 엔티티 ([!DNL Profile] access) {#entities}

Adobe Experience Platform을 통해 다음 항목에 액세스할 수 있습니다 [!DNL Real-Time Customer Profile] RESTful API 또는 사용자 인터페이스를 사용한 데이터. API를 사용하여 일반적으로 &quot;프로필&quot;이라고 하는 엔티티에 액세스하는 방법을 배우려면 [엔티티 끝점 안내서](entities.md). 를 사용하여 프로필에 액세스하려면 [!DNL Platform] UI에서 [프로필 사용 안내서](../ui/user-guide.md).

## 작업 내보내기([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] 활성화를 위해 대상 세그먼트 내보내기 또는 보고를 위한 프로필 속성 내보내기와 같은 추가 처리를 위해 데이터 세트에 데이터를 내보낼 수 있습니다. 대상 세그먼트에 대한 내보내기 작업은 의 일부입니다 [!DNL Adobe Experience Platform Segmentation Service] API입니다. [세그먼테이션 내보내기 작업 끝점 안내서](../../profile/api/export-jobs.md) 추가 정보 프로필 속성에 대한 내보내기 작업을 만들고 관리하는 방법에 대한 단계별 지침은 [작업 끝점 내보내기 안내서](export-jobs.md).

## 병합 정책 {#merge-policies}

여러 소스의 데이터를 [!DNL Experience Platform], 병합 정책 은 [!DNL Platform] 은(는) 데이터의 우선 순위가 지정되는 방식과 개별 고객 프로필을 만들기 위해 결합할 데이터를 판별하는 데 사용됩니다. 사용 [!DNL Real-Time Customer Profile] API를 사용하면 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. API를 사용하여 병합 정책을 작업하려면 [정책 엔드포인트 가이드 병합](merge-policies.md).

병합 정책 및 Platform 내의 해당 역할에 대해 자세히 알아보려면 [정책 병합 개요](../merge-policies/overview.md).

## 샘플 상태 미리 보기([!DNL Profile] 미리 보기) {#profile-preview}

데이터를 Platform에 수집하면 샘플 작업이 실행하여 프로필 수 및 기타 실시간 고객 프로필 데이터 관련 지표를 업데이트합니다. 이 샘플 작업의 결과는 `/previewsamplestatus` 실시간 고객 프로필 API의 일부인 끝점입니다. 이 종단점을 사용하여 데이터 세트와 ID 네임스페이스별로 프로필 배포를 나열할 수 있을 뿐만 아니라 조직의 프로필 저장소 구성을 표시하기 위해 여러 보고서를 생성할 수도 있습니다.  를 사용하여 시작하려면 `/profilepreviewstatus` 엔드포인트 [샘플 상태 엔드포인트 가이드 미리 보기](preview-sample-status.md).

## 프로필 시스템 작업 {#profile-system-jobs}

수집된 프로필 사용 데이터 [!DNL Platform] 에 저장됩니다. [!DNL Data Lake] 뿐만 아니라 [!DNL Real-Time Customer Profile] 데이터 저장소. 경우에 따라 [!DNL Profile] 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하려면 을 저장합니다. 이를 위해서는 API를 사용하여 [!DNL Profile System Job]이라고도 하는 &quot;[!DNL delete request]&quot;(필요한 경우 수정, 모니터링 또는 삭제할 수 있습니다.) 를 사용하여 삭제 요청을 처리하는 방법을 알아봅니다. `/system/jobs` 의 엔드포인트 [!DNL Real-Time Customer Profile] API에 설명된 단계를 수행합니다. [프로필 시스템 작업 끝점 안내서](profile-system-jobs.md).

## 프로필 속성 업데이트 {#update-profile}

간혹 조직의 프로필 저장소에서 데이터를 업데이트해야 할 수 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리를 통해 수행할 수 있으며, 후속 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 속성 업데이트를 위한 데이터 세트를 구성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [프로필 및 업데이트에 대한 데이터 세트 활성화](../../catalog/datasets/enable-upsert.md).

## 다음 단계 {#next-steps}

를 사용하여 호출을 시작하려면 [!DNL Real-Time Customer Profile] API에서 다음을 참조하십시오. [시작 안내서](getting-started.md) 그런 다음 엔드포인트 가이드 중 하나를 선택하여 특정 [!DNL Profile]- 관련 끝점입니다. 을 사용하여 작업하려면 [!DNL Profile] 데이터를 [!DNL Experience Platform] UI는 [Real-Time Customer Profile 사용 안내서](../ui/user-guide.md).
