---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 실시간 고객 프로필 API 개발자 가이드
topic: guide
translation-type: tm+mt
source-git-commit: fd6516d1c1d3792b41de65d0f44d78af1124ccc7
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# 실시간 고객 프로필 API 개발자 가이드

실시간 고객 프로필을 사용하면 Adobe Experience Platform 내에서 각 개별 고객을 전체적으로 파악할 수 있습니다. 프로필을 사용하면 온라인, 오프라인, CRM, 서드파티 데이터 등 다양한 채널에서 생성된 서로 다른 고객 데이터를 하나의 통합 뷰로 통합하여 모든 고객 인터랙션에 대해 실행 가능하고 타임스탬프가 지정된 계정을 제공할 수 있습니다.

실시간 고객 프로필 API에는 아래에 설명된 여러 끝점이 포함되어 있습니다. 자세한 내용은 개별 종단점 안내서를 참조하고 필요한 헤더, 샘플 API 호출 읽기 등에 대한 [자세한 내용은 시작 안내서](getting-started.md) 를 참조하십시오.

사용 가능한 모든 끝점 및 CRUD 작업을 보려면 [실시간 고객 프로필 API 참조 스웨거를 참조하십시오](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

## (알파) 계산된 속성

>[!IMPORTANT]
>계산된 속성 기능은 알파에 있으며 모든 사용자가 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

계산된 속성을 사용하면 다른 값, 계산 및 표현식을 기반으로 필드의 값을 자동으로 계산할 수 있습니다. 계산된 속성은 프로필 수준에서 작동합니다. 즉, 모든 레코드와 이벤트에 대한 값을 합산할 수 있습니다. 계산된 각 속성에는 들어오는 데이터를 평가하고 결과 값을 프로필 속성이나 이벤트에 저장하는 표현식 또는 &quot;규칙&quot;이 포함됩니다. 이러한 계산을 사용하면 정보가 필요할 때마다 복잡한 계산을 수동으로 수행하지 않고도 라이프타임 구매 값, 구매 시간 또는 애플리케이션 열기 횟수와 같은 문제와 관련된 질문에 쉽게 응답할 수 있습니다. 끝점을 사용하여 계산된 속성을 만들고, 보고, 편집하고, 삭제할 수 `config/computedAttributes` 있습니다. 이 종단점을 사용하는 방법을 알아보려면 [계산된 특성 끝점 안내서를 참조하십시오](computed-attributes.md).

## 에지 예상

Adobe Experience Platform을 사용하면 전략적으로 위치한 &quot;edges&quot;라는 서버에서 데이터에 쉽게 액세스할 수 있도록 함으로써 고객 경험을 실시간으로 개인화할 수 있습니다. 실시간 고객 프로필 API는 &quot;예측&quot;이라는 구성 요소를 통해 가장자리를 사용하여 작업하는 끝점을 제공합니다. 프로젝션 지정 영역에는 프로젝션 경로를 정의하는 프로젝션 목적뿐만 아니라 각 가장자리에 투영해야 하는 데이터를 결정하기 위한 프로젝션 구성이 포함됩니다. 가장자리 투영 작업에 대한 자세한 내용은 [투영 구성 및 대상 엔드포인트 가이드를 참조하십시오](edge-projections.md).

## 엔티티

Adobe Experience Platform을 통해 RESTful API 또는 사용자 인터페이스를 사용하여 실시간 고객 프로필 데이터에 액세스할 수 있습니다. API를 사용하여 &quot;프로필&quot;으로 더 일반적으로 알려진 엔터티에 액세스하는 방법을 알아보려면 [개체 끝점 안내서에 설명된 단계를 따르십시오](entities.md). Platform UI를 사용하여 프로필에 액세스하려면 프로필 사용 [안내서를 참조하십시오](../ui/user-guide.md).

## 정책 병합

Experience Platform에서 여러 소스의 데이터를 취합할 때 병합 정책은 Platform이 데이터의 우선 순위를 정하는 방법과 개별 고객 프로파일을 만들기 위해 결합할 데이터를 결정하는 규칙입니다. 실시간 고객 프로필 API를 사용하면 새로운 병합 정책을 만들고, 기존 정책을 관리하고, 조직에 대한 기본 병합 정책을 설정할 수 있습니다. API를 사용한 병합 정책 작업에 대한 자세한 내용은 [병합 정책 끝점 안내서를 참조하십시오](merge-policies.md).

Platform UI를 사용하여 병합 정책을 사용하는 방법에 대한 지침은 정책 [병합 사용자 안내서를 참조하십시오](../ui/merge-policies.md).

## 프로필 시스템 작업

Platform으로 인제스트된 데이터는 실시간 고객 프로필 데이터 저장소뿐만 아니라 데이터 레이크에 저장됩니다. 더 이상 필요하지 않거나 오류가 추가된 데이터를 제거하기 위해 프로필 저장소에서 데이터세트 또는 일괄 처리를 삭제해야 할 수 있습니다. 이를 위해서는 API를 사용하여 &quot;삭제 요청&quot;이라고 하는 프로필 시스템 작업을 만들어야 하며, 이 작업은 필요한 경우 수정, 모니터링 또는 삭제할 수도 있습니다. 실시간 고객 프로필 API의 끝점을 사용하여 삭제 요청 `/system/jobs` 작업을 수행하는 방법에 대해 알아보려면 [프로필 시스템 작업 끝점 안내서에 설명된 단계를 따르십시오](profile-system-jobs.md).

## 다음 단계

실시간 고객 프로필 API를 사용하여 호출을 시작하려면 시작 안내서 [를](getting-started.md) 읽은 다음 끝점 가이드 중 하나를 선택하여 특정 프로필 관련 끝점의 사용 방법을 학습합니다. Platform UI를 사용한 프로필 데이터 작업에 대한 자세한 내용은 [실시간 고객 프로필 사용 안내서를 참조하십시오](../ui/user-guide.md).