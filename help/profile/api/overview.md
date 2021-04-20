---
keywords: Experience Platform;프로파일;실시간 고객 프로파일;문제 해결;API;통합 프로파일;통합 프로파일;통합 프로파일;프로파일;프로파일 사용;프로파일 사용;프로파일 사용;프로파일 사용
title: 실시간 고객 프로필 API 안내서
topic: guide
description: 개발자는 실시간 고객 프로필 API를 사용하여 프로필 보기, 병합 정책 만들기 및 업데이트, 프로필 데이터 내보내기 또는 샘플 데이터, 더 이상 필요하지 않거나 오류로 추가된 프로필 데이터를 포함하여 프로필 데이터를 탐색 및 작업할 수 있습니다. API를 사용하여 주요 작업을 수행하는 방법에 대해 알아보려면 이 안내서를 따르십시오.
translation-type: tm+mt
source-git-commit: 24a5af0440f58b4e1db639ec971c4e1611f107d8
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API 안내서

[!DNL Real-time Customer Profile] Adobe Experience Platform에서 각 개별 고객을 전체적으로 확인할 수 있습니다. [!DNL Profile] 온라인, 오프라인, CRM 및 제3자 데이터와 같은 다양한 채널에서 얻은 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하면 모든 고객 인터랙션에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

[!DNL Real-time Customer Profile] API에는 아래에 설명된 여러 끝점이 포함되어 있습니다. 자세한 내용은 개별 끝점 안내선을 참조하고 [시작 안내서](getting-started.md)에서 필수 머리글, 샘플 API 호출 읽기 등에 대한 중요한 정보를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [실시간 고객 프로필 API 참조 API 참조](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)를 방문하십시오.

[!DNL Experience Platform] UI에서 [!DNL Real-time Customer Profile] 데이터를 사용하여 작업하는 방법에 대한 지침은 [프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.

## (알파) 계산된 특성 {#computed-attributes}

>[!IMPORTANT]
>
>계산된 속성 기능은 알파에 있으며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성은 이벤트 수준 데이터를 프로필 수준 속성으로 집계하는 데 사용되는 함수입니다. 이러한 함수는 세분화, 활성화 및 개인화 간에 사용할 수 있도록 자동으로 계산됩니다.

계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 간 시간 또는 애플리케이션 열기 횟수와 같은 것과 관련된 질문에 쉽게 답변할 수 있습니다. 이러한 계산된 속성 값은 프로필에서 보거나, 세그먼트를 만드는 데 사용하거나, 여러 다른 액세스 패턴을 통해 액세스할 수 있습니다.

`config/computedAttributes` 끝점을 사용하여 계산된 특성을 만들고, 보고, 편집하고, 삭제할 수 있습니다. 계산된 속성을 사용하는 방법에 대해 알아보려면 [계산된 속성 개요](../computed-attributes/overview.md)를 참조하십시오. API 작업의 경우 [계산된 특성 API 끝점 안내서](../computed-attributes/ca-api.md)를 방문하십시오.

## 가장자리 예상 {#edge-projections}

Adobe Experience Platform을 사용하면 전략적으로 위치한 &quot;edges&quot;라는 서버에서 데이터에 쉽게 액세스할 수 있도록 함으로써 고객 경험을 실시간으로 개인화할 수 있습니다. [!DNL Real-time Customer Profile] API는 &quot;투영&quot;이라는 구성 요소를 통해 가장자리를 사용하여 작업하는 끝점을 제공합니다. 프로젝션 경로지정 위치를 정의하는 투영 대상 및 각 가장자리에 투영할 데이터를 결정하는 투영 구성이 포함됩니다. 가장자리 투영 작업에 대한 자세한 내용은 [투영 구성 및 대상 끝점 안내서](edge-projections.md)를 참조하십시오.

## 엔터티([!DNL Profile] 액세스) {#entities}

Adobe Experience Platform을 통해 RESTful API 또는 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile] 데이터에 액세스할 수 있습니다. API를 사용하여 &quot;프로파일&quot;로 더 일반적으로 알려진 엔터티에 액세스하는 방법을 알아보려면 [개체 끝점 안내서](entities.md)에 설명된 단계를 따르십시오. [!DNL Platform] UI를 사용하여 프로파일에 액세스하려면 [프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.

## 내보내기 작업([!DNL Profile] 내보내기) {#profile-export}

[!DNL Real-time Customer Profile] 데이터를 데이터 세트에 내보내 활성화를 위해 대상 세그먼트 내보내기 또는 보고를 위한 프로필 속성 내보내기 등의 추가 처리를 수행할 수 있습니다. 대상 세그먼트에 대한 내보내기 작업은 [!DNL Adobe Experience Platform Segmentation Service] API의 일부입니다. 자세한 내용은 [세그멘테이션 내보내기 작업 끝점 안내서](../../profile/api/export-jobs.md)를 참조하십시오. 프로필 특성에 대한 내보내기 작업을 만들고 관리하는 방법에 대한 단계별 지침을 보려면 [내보내기 작업 끝점 안내서](export-jobs.md)를 방문하십시오.

## 정책 병합 {#merge-policies}

여러 소스의 데이터를 [!DNL Experience Platform]에 취합할 때 병합 정책은 데이터의 우선 순위를 결정하는 방법과 개별 고객 프로파일을 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다. [!DNL Platform] [!DNL Real-time Customer Profile] API를 사용하여 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. API를 사용하여 병합 정책을 사용하는 방법에 대한 자세한 내용은 [병합 정책 끝점 안내서](merge-policies.md)를 참조하십시오.

[!DNL Platform] UI를 사용하여 병합 정책을 사용하는 방법에 대한 지침은 [병합 정책 사용 안내서](../ui/merge-policies.md)를 참조하십시오.

## 샘플 상태 미리 보기([!DNL Profile] 미리 보기) {#profile-preview}

프로파일에 대해 활성화된 데이터가 Experience Platform에 수집되면 프로필 데이터 저장소 내에 저장됩니다. 프로필 저장소의 레코드 수가 증가하거나 감소하면 데이터 저장소에 있는 프로필 조각 및 병합된 프로필 수에 대한 정보가 포함된 샘플 작업이 실행됩니다. 프로필 API를 사용하면 성공적인 최신 샘플뿐만 아니라 데이터 세트 및 ID 네임스페이스별 프로필 배포를 나열할 수도 있습니다. `/profilepreviewstatus` 끝점을 사용하여 시작하려면 [미리 보기 샘플 상태 끝점 안내서](preview-sample-status.md)를 참조하십시오.

## 프로필 시스템 작업 {#profile-system-jobs}

[!DNL Platform]으로 인제스트된 프로필 사용 데이터는 [!DNL Data Lake] 및 [!DNL Real-time Customer Profile] 데이터 저장소에 저장됩니다. 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하기 위해 [!DNL Profile] 저장소에서 데이터 세트 또는 일괄 처리를 삭제해야 하는 경우가 있습니다. 이를 위해서는 API를 사용하여 &quot;[!DNL delete request]&quot;라고도 하는 [!DNL Profile System Job]을 만들어야 하며, 이 작업은 필요한 경우 수정, 모니터링 또는 삭제할 수 있습니다. [!DNL Real-time Customer Profile] API의 `/system/jobs` 끝점을 사용하여 삭제 요청을 사용하는 방법에 대해 알아보려면 [ 프로파일 시스템 작업 끝점 안내서](profile-system-jobs.md)에 설명된 단계를 따르십시오.

## 다음 단계 {#next-steps}

[!DNL Real-time Customer Profile] API를 사용하여 호출을 시작하려면 [시작 안내서](getting-started.md)를 읽은 다음 끝점 안내선 중 하나를 선택하여 특정 [!DNL Profile] 관련 끝점의 사용 방법을 학습합니다. [!DNL Experience Platform] UI를 사용하여 [!DNL Profile] 데이터로 작업하려면 [실시간 고객 프로필 사용 안내서](../ui/user-guide.md)를 참조하십시오.