---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile
title: 실시간 고객 프로필 API 개발자 가이드
topic: guide
description: 실시간 고객 프로필 API에는 아래에 설명된 여러 끝점이 포함되어 있습니다.
translation-type: tm+mt
source-git-commit: 59cf089a8bf7ce44e7a08b0bb1d4562f5d5104db
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] API 개발자 가이드

[!DNL Real-time Customer Profile] adobe experience platform에서 각 개별 고객의 전체 상황을 파악할 수 있습니다. [!DNL Profile] 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널을 통해 얻은 서로 다른 고객 데이터를 하나의 통합 뷰로 통합할 수 있으므로 모든 고객 인터랙션에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

API에는 아래에 나와 있는 여러 끝점이 포함되어 있습니다. [!DNL Real-time Customer Profile] 자세한 내용은 개별 종단점 안내서를 참조하고 필요한 헤더, 샘플 API 호출 읽기 등에 대한 [자세한 내용은 시작 안내서](getting-started.md) 를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [실시간 고객 프로필 API 참조 스웨거를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

UI에서 [!DNL Real-time Customer Profile] 데이터 작업에 대한 [!DNL Experience Platform] 지침은 [프로필 사용 안내서를 참조하십시오](../ui/user-guide.md).

## (알파) 계산된 속성 {#computed-attributes}

>[!IMPORTANT]
>
>계산된 속성 기능은 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 프로필 수준에서 작동합니다. 즉, 모든 레코드와 이벤트에 대한 값을 합산할 수 있습니다. 계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성이나 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 시간 또는 애플리케이션 열기 횟수와 같은 문제와 관련된 질문에 쉽게 응답할 수 있습니다. 끝점을 사용하여 계산된 속성을 만들고, 보고, 편집하고, 삭제할 수 `config/computedAttributes` 있습니다. 이 종단점을 사용하는 방법을 알아보려면 [계산된 특성 끝점 안내서를 참조하십시오](computed-attributes.md).

## 에지 예상 {#edge-projections}

Adobe Experience Platform은 &quot;edges&quot;라는 전략적 서버에 있는 데이터를 손쉽게 액세스할 수 있도록 함으로써 고객 경험을 실시간으로 개인화할 수 있습니다. API는 &quot;투영&quot;이라는 구성 요소를 통해 가장자리를 사용하여 작업하는 끝점을 제공합니다. [!DNL Real-time Customer Profile] 프로젝션 지정 영역에는 프로젝션 경로를 정의하는 프로젝션 목적뿐만 아니라 각 가장자리에 투영해야 하는 데이터를 결정하기 위한 프로젝션 구성이 포함됩니다. 가장자리 투영 작업에 대한 자세한 내용은 [투영 구성 및 대상 엔드포인트 가이드를 참조하십시오](edge-projections.md).

## 엔티티([!DNL Profile] 액세스) {#entities}

Adobe Experience Platform을 통해 RESTful API 또는 사용자 인터페이스를 사용하여 [!DNL Real-time Customer Profile] 데이터에 액세스할 수 있습니다. API를 사용하여 &quot;프로필&quot;으로 더 일반적으로 알려진 엔터티에 액세스하는 방법을 알아보려면 [개체 끝점 안내서에 설명된 단계를 따르십시오](entities.md). UI를 사용하여 프로필에 액세스하려면 [!DNL Platform] 프로필 사용 [안내서를 참조하십시오](../ui/user-guide.md).

## 내보내기 작업([!DNL Profile] 내보내기) {#profile-export}

[!DNL Real-time Customer Profile] 데이터를 데이터 세트에 내보내 활성화를 위해 대상 세그먼트 내보내기 또는 보고를 위한 프로필 속성 내보내기 등의 추가 처리를 수행할 수 있습니다. 대상 세그먼트에 대한 내보내기 작업은 [!DNL Adobe Experience Platform Segmentation Service] API에 포함되어 있습니다. 자세한 내용은 [세그멘테이션 내보내기 작업 끝점 안내서](../../profile/api/export-jobs.md) 를 참조하십시오. 프로필 속성에 대한 내보내기 작업을 만들고 관리하는 방법에 대한 단계별 지침을 보려면 [내보내기 작업 끝점 안내서를 참조하십시오](export-jobs.md).

## 정책 병합 {#merge-policies}

여러 소스의 데이터를 여러 데이터 [!DNL Experience Platform]로 취합할 때 병합 정책은 데이터의 우선 순위를 [!DNL Platform] 결정하는 방법과 개별 고객 프로파일을 만들기 위해 결합할 데이터를 결정하는 데 사용하는 규칙입니다. API를 사용하여 [!DNL Real-time Customer Profile] 새 병합 정책을 만들고 기존 정책을 관리하고 조직에 대한 기본 병합 정책을 설정할 수 있습니다. API를 사용한 병합 정책 작업에 대한 자세한 내용은 [병합 정책 끝점 안내서를 참조하십시오](merge-policies.md).

UI를 사용한 병합 정책 작업에 대한 지침은 [!DNL Platform] 병합 정책 사용 설명서를 참조하십시오 [](../ui/merge-policies.md).

## 샘플 상태 미리 보기([!DNL Profile] 미리 보기) {#profile-preview}

프로필에 대해 활성화된 데이터가 Experience Platform으로 인제스트되면 프로필 데이터 저장소 내에 저장됩니다. 프로필 저장소의 레코드 수가 늘어나거나 줄어들면서 데이터 저장소에 있는 프로필 조각 및 병합된 프로필 수에 대한 정보가 포함된 샘플 작업이 실행됩니다. 프로필 API를 사용하면 성공적인 최신 샘플뿐만 아니라 데이터 세트 및 ID 네임스페이스별로 프로필 배포를 나열할 수 있습니다. 끝점을 사용하여 시작하려면 `/profilepreviewstatus` 미리 보기 샘플 상태 끝점 안내서를 참조하십시오 [](preview-sample-status.md).

## 프로필 시스템 작업 {#profile-system-jobs}

인제스트된 데이터 [!DNL Platform] 는 데이터 저장소와 [!DNL Data Lake] 함께 [!DNL Real-time Customer Profile] 저장됩니다. 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하기 위해 [!DNL Profile] 저장소에서 데이터세트 또는 일괄 처리를 삭제해야 할 수 있습니다. 이를 위해서는 API를 사용하여 &quot; [!DNL Profile System Job][!DNL delete request]&quot;라고 하는 API를 만들고, 필요한 경우 수정, 모니터링 또는 삭제할 수 있습니다. API의 끝점을 사용하여 삭제 요청 `/system/jobs` 을 사용하는 방법에 대해 알아보려면 [!DNL Real-time Customer Profile][프로필 시스템 작업 끝점 안내서에 설명된 단계를 따르십시오](profile-system-jobs.md).

## 다음 단계 {#next-steps}

API를 사용하여 호출을 시작하려면 [!DNL Real-time Customer Profile] 시작 안내서 [를 읽은 다음 끝점 안내서 중 하나를 선택하여 특정](getting-started.md) [!DNL Profile]관련 끝점의 사용 방법을 학습합니다. UI를 [!DNL Profile] 사용하여 데이터 [!DNL Experience Platform] 작업을 하려면 [실시간 고객 프로필 사용 안내서를 참조하십시오](../ui/user-guide.md).