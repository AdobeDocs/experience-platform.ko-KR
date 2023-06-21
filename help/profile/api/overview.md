---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;통합 프로필;통합 프로필;통합;프로필;rtcp;프로필 활성화;프로필 활성화
title: 실시간 고객 프로필 API 안내서
description: 실시간 고객 프로필 API를 통해 개발자는 프로필 보기, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 또는 샘플, 더 이상 필요하지 않거나 오류로 추가된 프로필 데이터 삭제 등을 포함하여 프로필 데이터를 탐색하고 작업할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API 안내서

[!DNL Real-Time Customer Profile] Adobe Experience Platform 내에서 각 개별 고객에 대한 거시적인 보기를 볼 수 있습니다. [!DNL Profile] 을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터와 같은 여러 채널의 다양한 고객 데이터를 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 통합할 수 있습니다.

다음 [!DNL Real-Time Customer Profile] API에는 아래에 요약된 여러 끝점이 포함되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 참조하고 [시작 안내서](getting-started.md) 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보를 제공합니다.

사용 가능한 모든 엔드포인트 및 CRUD 작업을 보려면 [Real-Time Customer Profile API 참조 Swagger](https://www.adobe.com/go/profile-apis-en).

작업에 대한 안내서용 [!DNL Real-Time Customer Profile] 의 데이터 [!DNL Experience Platform] UI, 다음을 참조하십시오. [프로필 사용 안내서](../ui/user-guide.md).

## [!BADGE 베타]{type=Informative} 계산된 속성 {#computed-attributes}

>[!IMPORTANT]
>
>계산된 속성 기능은 Beta 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화에서 사용할 수 있도록 자동으로 계산됩니다.

계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 통해 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 수명 기간 내 구매 가격, 구매 간격 또는 응용 프로그램 열기 수와 같은 질문과 관련된 질문에 쉽게 답변할 수 있습니다. 그런 다음 이러한 계산된 속성 값을 프로필에서 보거나, 세그먼트를 만드는 데 사용하거나, 다양한 액세스 패턴을 통해 액세스할 수 있습니다.

다음을 사용하여 계산된 속성을 작성, 보기, 편집 및 삭제할 수 있습니다. `ca/attributes/` 엔드포인트. 계산된 속성을 사용하는 방법에 대해 알아보려면 다음을 참조하십시오. [계산된 속성 개요](../computed-attributes/overview.md). API 작업은 다음을 참조하십시오. [계산된 속성 API 끝점 안내서](../computed-attributes/api.md).

## 가장자리 투영 {#edge-projections}

Adobe Experience Platform은 전략적으로 위치한 서버인 &quot;에지&quot;에서 데이터에 쉽게 액세스할 수 있도록 함으로써 고객 경험의 실시간 개인화를 지원합니다. 다음 [!DNL Real-Time Customer Profile] API는 &quot;예측&quot;이라는 구성 요소를 통해 에지 작업을 위한 끝점을 제공합니다. 여기에는 각 에지에 투영해야 하는 데이터를 결정하는 투영 구성과 투영을 라우팅할 위치를 정의하는 투영 대상이 포함됩니다. Edge 프로젝션을 사용한 작업에 대한 자세한 내용은 [투영 구성 및 대상 끝점 안내서](edge-projections.md).

## 엔티티([!DNL Profile] 액세스) {#entities}

Adobe Experience Platform을 통해 액세스할 수 있습니다. [!DNL Real-Time Customer Profile] restFul API 또는 사용자 인터페이스를 사용하는 데이터. API를 사용하여 &quot;프로필&quot;이라고도 하는 엔티티에 액세스하는 방법을 알아보려면 다음에 설명된 단계를 따르십시오. [엔티티 끝점 안내서](entities.md). 을 사용하여 프로필에 액세스하려면 다음을 수행하십시오. [!DNL Platform] UI에서 다음을 참조하십시오 [프로필 사용 안내서](../ui/user-guide.md).

## 내보내기 작업([!DNL Profile] 내보내기) {#profile-export}

[!DNL Real-Time Customer Profile] 활성화를 위해 대상 세그먼트를 내보내거나 보고를 위해 프로필 속성을 내보내는 등, 추가 처리를 위해 데이터를 데이터 세트로 내보낼 수 있습니다. 대상 세그먼트에 대한 내보내기 작업은 [!DNL Adobe Experience Platform Segmentation Service] API, 다음을 읽으십시오. [세그먼테이션 내보내기 작업 엔드포인트 안내서](../../profile/api/export-jobs.md) 자세히 알아보십시오. 프로필 속성에 대한 내보내기 작업을 만들고 관리하는 방법에 대한 단계별 지침은 다음을 참조하십시오. [내보내기 작업 엔드포인트 안내서](export-jobs.md).

## 병합 정책 {#merge-policies}

여러 소스의 데이터를 [!DNL Experience Platform], 병합 정책은 다음과 같은 규칙입니다 [!DNL Platform] 는 을 사용하여 데이터의 우선 순위 지정 방법 및 개별 고객 프로필을 만들기 위해 결합할 데이터를 결정합니다. 사용 [!DNL Real-Time Customer Profile] API를 사용하면 새 병합 정책을 만들고, 기존 정책을 관리하고, 조직의 기본 병합 정책을 설정할 수 있습니다. API를 사용하여 병합 정책으로 작업하려면 [병합 정책 끝점 안내서](merge-policies.md).

병합 정책 및 Platform 내에서 해당 역할에 대한 자세한 내용은 [병합 정책 개요](../merge-policies/overview.md).

## 샘플 상태 미리 보기([!DNL Profile] 미리 보기) {#profile-preview}

데이터가 Platform으로 수집되면 샘플 작업이 실행되어 프로필 수 및 기타 실시간 고객 프로필 데이터 관련 지표를 업데이트합니다. 이 샘플 작업의 결과는 `/previewsamplestatus` 실시간 고객 프로필 API의 일부인 종단점입니다. 이 끝점을 사용하여 데이터 세트와 ID 네임스페이스 모두로 프로필 분포를 나열할 수 있을 뿐만 아니라 조직의 프로필 스토어 구성에 대한 가시성을 확보할 수 있도록 여러 보고서를 생성할 수도 있습니다.  을(를) 사용하려면 `/profilepreviewstatus` 엔드포인트, 다음 참조 [샘플 상태 끝점 안내서 미리 보기](preview-sample-status.md).

## 프로필 시스템 작업 {#profile-system-jobs}

에 수집되는 프로필 활성화 데이터 [!DNL Platform] 에 저장됩니다. [!DNL Data Lake] 및 [!DNL Real-Time Customer Profile] 데이터 저장소입니다. 간혹 [!DNL Profile] 더 이상 필요하지 않거나 오류로 추가된 데이터를 제거하려면 저장합니다. API를 사용하여 다음을 생성해야 합니다. [!DNL Profile System Job], &quot;라고도 함[!DNL delete request]필요한 경우 수정, 모니터링 또는 삭제할 수 있는 &quot;. 을(를) 사용하여 삭제 요청으로 작업하는 방법을 알아보려면 `/system/jobs` 의 엔드포인트 [!DNL Real-Time Customer Profile] API에서 다음에 설명된 단계를 수행합니다. [프로필 시스템 작업 끝점 안내서](profile-system-jobs.md).

## 프로필 속성 업데이트 {#update-profile}

조직의 프로필 스토어에서 데이터를 업데이트해야 하는 경우가 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리 수집을 통해 수행할 수 있으며 업데이트 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 속성 업데이트를 위한 데이터 세트를 구성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [프로필 및 업데이트에 대한 데이터 세트 활성화](../../catalog/datasets/enable-upsert.md).

## 다음 단계 {#next-steps}

을 사용하여 호출을 시작하려면 [!DNL Real-Time Customer Profile] API, 읽기 [시작 안내서](getting-started.md) 그런 다음 엔드포인트 가이드 중 하나를 선택하여 특정 엔드포인트를 사용하는 방법을 알아봅니다 [!DNL Profile]-관련 종단점입니다. 작업 대상 [!DNL Profile] 를 사용하는 데이터 [!DNL Experience Platform] UI, 다음을 참조하십시오. [실시간 고객 프로필 사용 안내서](../ui/user-guide.md).
