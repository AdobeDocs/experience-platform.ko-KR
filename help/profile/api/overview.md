---
keywords: Experience Platform;프로필;실시간 고객 프로필;문제 해결;API;통합 프로필;통합 프로필;통합;프로필;rtcp;프로필 활성화;프로필 활성화
title: 실시간 고객 프로필 API 안내서
description: 실시간 고객 프로필 API를 통해 개발자는 프로필 보기, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 또는 샘플, 더 이상 필요하지 않거나 오류로 추가된 프로필 데이터 삭제 등을 포함하여 프로필 데이터를 탐색하고 작업할 수 있습니다. 이 안내서를 따라 API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보십시오.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] API 안내서

[!DNL Real-Time Customer Profile]을(를) 사용하면 Adobe Experience Platform 내에서 각 개별 고객에 대한 거시적인 보기를 볼 수 있습니다. [!DNL Profile]을(를) 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터와 같은 여러 채널의 다양한 고객 데이터를 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 통합할 수 있습니다.

[!DNL Real-Time Customer Profile] API에는 아래에 요약된 여러 끝점이 포함되어 있습니다. 자세한 내용은 개별 엔드포인트 안내서를 참조하고 필수 헤더, 샘플 API 호출 읽기 등에 대한 중요한 정보는 [시작 안내서](getting-started.md)를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [실시간 고객 프로필 API 참조 스웨거](https://www.adobe.com/go/profile-apis-en)를 방문하세요.

[!DNL Experience Platform] UI에서 [!DNL Real-Time Customer Profile] 데이터를 사용하는 방법에 대한 지침은 [프로필 사용 안내서](../ui/user-guide.md)를 참조하세요.

## [!BADGE Beta]{type=Informative} 계산된 특성 {#computed-attributes}

>[!IMPORTANT]
>
계산된 속성 기능은 Beta 버전이며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세그먼테이션, 활성화 및 개인화에서 사용할 수 있도록 자동으로 계산됩니다.

계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 통해 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 수명 기간 내 구매 가격, 구매 간격 또는 응용 프로그램 열기 수와 같은 질문과 관련된 질문에 쉽게 답변할 수 있습니다. 그런 다음 이러한 계산된 속성 값을 프로필에서 보거나, 대상자를 만드는 데 사용하거나, 여러 다른 액세스 패턴을 통해 액세스할 수 있습니다.

`ca/attributes/` 끝점을 사용하여 계산된 특성을 만들고, 보고, 편집하고, 삭제할 수 있습니다. 계산된 특성을 사용하는 방법을 알아보려면 [계산된 특성 개요](../computed-attributes/overview.md)를 참조하세요. API 작업의 경우 [계산된 특성 API 끝점 안내서](../computed-attributes/api.md)를 참조하십시오.

## 엔터티([!DNL Profile] 액세스) {#entities}

Adobe Experience Platform을 통해 RESTful API 또는 사용자 인터페이스를 사용하여 [!DNL Real-Time Customer Profile] 데이터에 액세스할 수 있습니다. API를 사용하여 엔터티에 액세스하는 방법을 알아보려면 [엔터티 끝점 안내서](entities.md)에 설명된 단계를 따르십시오. &quot;프로필&quot;이라고도 합니다. [!DNL Platform] UI를 사용하여 프로필에 액세스하려면 [프로필 사용 안내서](../ui/user-guide.md)를 참조하세요.

## 내보내기 작업([!DNL Profile]개 내보내기) {#profile-export}

활성화를 위해 대상을 내보내거나 보고를 위해 프로필 특성을 내보내는 등 추가 처리를 위해 [!DNL Real-Time Customer Profile] 데이터를 데이터 세트로 내보낼 수 있습니다. 대상의 내보내기 작업은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 자세한 내용은 [세그먼테이션 내보내기 작업 끝점 안내서](../../profile/api/export-jobs.md)를 참조하십시오. 프로필 특성에 대한 내보내기 작업을 만들고 관리하는 방법에 대한 단계별 지침은 [내보내기 작업 끝점 안내서](export-jobs.md)를 참조하십시오.

## 병합 정책 {#merge-policies}

[!DNL Experience Platform]에서 여러 소스의 데이터를 함께 가져올 때 병합 정책은 [!DNL Platform]에서 데이터 우선 순위 지정 방법과 어떤 데이터를 결합하여 개별 고객 프로필을 만들 것인지 결정하는 데 사용하는 규칙입니다. [!DNL Real-Time Customer Profile] API를 사용하면 새 병합 정책을 만들고, 기존 정책을 관리하고, 조직의 기본 병합 정책을 설정할 수 있습니다. API를 사용하여 병합 정책으로 작업하려면 [병합 정책 끝점 안내서](merge-policies.md)를 참조하십시오.

병합 정책 및 Platform 내에서 해당 역할에 대한 자세한 내용은 [병합 정책 개요](../merge-policies/overview.md)를 읽어 보십시오.

## 샘플 상태 미리 보기([!DNL Profile] 미리 보기) {#profile-preview}

데이터가 Platform으로 수집되면 샘플 작업이 실행되어 프로필 수 및 기타 실시간 고객 프로필 데이터 관련 지표를 업데이트합니다. 이 샘플 작업의 결과는 실시간 고객 프로필 API의 일부인 `/previewsamplestatus` 끝점을 사용하여 볼 수 있습니다. 이 끝점을 사용하여 데이터 세트와 ID 네임스페이스 모두로 프로필 분포를 나열할 수 있을 뿐만 아니라 조직의 프로필 저장소 구성을 가시적으로 확인할 수 있도록 여러 보고서를 생성할 수도 있습니다.  `/profilepreviewstatus` 끝점을 사용하려면 [미리 보기 샘플 상태 끝점 안내서](preview-sample-status.md)를 참조하세요.

## 프로필 시스템 작업 {#profile-system-jobs}

[!DNL Platform]에 수집되는 프로필 사용 데이터는 [!DNL Data Lake] 및 [!DNL Real-Time Customer Profile] 데이터 저장소에 저장됩니다. 더 이상 필요하지 않거나 오류로 추가된 데이터를 제거하기 위해 프로필 저장소에서 데이터 세트와 연결된 프로필 데이터를 삭제해야 하는 경우가 있습니다. API를 사용하여 필요한 경우 수정, 모니터링 또는 삭제할 수 있는 &quot;[!DNL delete request]&quot;이라고도 하는 [!DNL Profile System Job]을(를) 만들어야 합니다. [!DNL Real-Time Customer Profile] API에서 `/system/jobs` 끝점을 사용하여 삭제 요청을 처리하는 방법에 대해 알아보려면 [프로필 시스템 작업 끝점 안내서](profile-system-jobs.md)에 설명된 단계를 따르십시오.

## 프로필 속성 업데이트 {#update-profile}

조직의 프로필 스토어에서 데이터를 업데이트해야 하는 경우가 있습니다. 예를 들어 레코드를 수정하거나 속성 값을 변경해야 할 수 있습니다. 이 작업은 일괄 처리 수집을 통해 수행할 수 있으며 업데이트 태그로 구성된 프로필 지원 데이터 세트가 필요합니다. 특성 업데이트에 대한 데이터 집합을 구성하는 방법에 대한 자세한 내용은 [프로필 및 업데이트에 대한 데이터 집합 활성화](../../catalog/datasets/enable-upsert.md)에 대한 자습서를 참조하십시오.

## 다음 단계 {#next-steps}

[!DNL Real-Time Customer Profile] API를 사용하여 호출을 시작하려면 [시작 안내서](getting-started.md)를 읽은 다음 끝점 안내서 중 하나를 선택하여 특정 [!DNL Profile] 관련 끝점을 사용하는 방법을 알아보세요. [!DNL Experience Platform] UI를 사용하여 [!DNL Profile] 데이터로 작업하려면 [실시간 고객 프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.
